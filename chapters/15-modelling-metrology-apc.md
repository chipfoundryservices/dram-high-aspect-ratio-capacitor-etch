# Chapter 15: Feature-Scale Modelling, Metrology & Advanced Process Control

## Overview

The 91:1 capacitor hole is hard to see. A CD-SEM measures its top. An HV-SEM sees its top and bottom, but not its profile. X-ray scatterometry measures its average profile over a beam spot, slowly. A cross-section shows the whole profile of a handful of holes, destructively, in hours. Endpoint signals from the bottom are faint and smeared. Yet the specification asks for 0.4 nm control of the chamber mean bottom CD and 0.03° control of edge tilt. At 57:1 a fab could close the loop with measurements alone. At 91:1 it closes the loop with models that are anchored by measurements.

This chapter describes feature-scale models and their reduced forms, the metrology toolkit and its sampling plan, endpoint at the bottom of a 91:1 hole, and the APC architecture that combines them: feed-forward from incoming metrology, feedback from post-etch metrology, consumable-age offsets, and virtual metrology.

**Learning Objectives:**
- Describe the components of a feature-scale etch model and what each needs as input
- Explain the role of reduced-order models and surrogates in production
- Choose metrology for each hole parameter and set a sampling plan
- Estimate the endpoint signal at the bottom stop and its usefulness
- Compute feed-forward and EWMA feedback corrections
- Describe virtual metrology and its limits

---

## 15.1 Feature-Scale Models

### 15.1.1 Structure

```
1. Plasma and sheath input (from a reactor model or measurement):
     ion energy–angle distributions (IEADs) by species and radius;
     neutral fluxes by species
2. Particle transport in the feature (Monte Carlo):
     ions with specular/diffuse reflection and energy loss (Chapter 3);
     neutrals with sticking and re-emission (Chapter 4);
     charging: surface charge, field solution, ion trajectories bent by it
3. Surface kinetics (site balance):
     coverages of fluorocarbon, F, O, H; yields as functions of energy,
     angle, and coverage; deposition and etch rates by material
4. Profile evolution:
     level-set, string, or cell-based surface advance; mask erosion
```

### 15.1.2 Calibration

```
Typical free parameters: 15–30
  sticking and reaction probabilities (CFₓ, F, O, HF)
  yield coefficients and thresholds by material (SiO₂, BPSG, SiN, B-ACL)
  reflection probability and energy loss for grazing ions
  polymer removal yield; wall conductivity for charge relaxation

Calibration data:
  depth series (depth vs time at 3–5 times) → ER₀, k, k₂
  cross-sections at full depth (profile, bow position, bottom CD)
  mask remaining and facet shape
  HV-SEM twist and tilt distributions
```

A calibrated model reproduces the reference profile, the time-to-depth curve, and the twist distribution, then predicts the response to changes that have not yet been run. Its value is in the predictions, and its risk is in extrapolation beyond the calibration data.

### 15.1.3 Cost

```
Single 3D hole with charging, full depth (illustrative):
  10⁷–10⁸ ion and neutral trajectories; 10³ profile time steps
  GPU run time: tens of minutes to hours
Twist statistics need hundreds of holes with random mask perturbations
  → days on a cluster
```

Feature-scale models are therefore used in development, for recipe design, for root-cause analysis, and to train faster models. They are too slow for wafer-by-wafer control.

### 15.1.4 Reduced-Order Models

The closed-form relations of this book are a reduced-order model of the hole:

```
Depth:      t(h) = G(h)/ER₀ with k, k₂ (Chapter 4)
Bow:        bow CD = CD_form + 2 r_b (t − t_form) (Chapter 10)
Twist:      3σ = C (h − h_on)^1.5 (Chapter 11)
Mask:       z_f = h_mask0 − f · r_m · t (Chapter 13)
Arrival:    Δt ≈ 5.2 s per nm of CD deficit (Chapter 12)
```

Each parameter (ER₀, k, r_b, C, r_m) is a function of the recipe and the chamber state. The feature-scale model and the production data together supply those functions. The reduced-order model then runs in milliseconds inside the APC system.

### 15.1.5 Surrogates

Machine-learned surrogates, trained on thousands of feature-scale runs and on production data, map recipe parameters and chamber sensors directly to profile metrics. They are fast and capture interactions that the closed forms miss. They inherit the domain of their training set, and they must be retrained when the chamber hardware, mask material, or chemistry changes.

---

## 15.2 Metrology

### 15.2.1 Toolkit

```
Method                      Measures                               Sampling      Notes
──────────────────────────────────────────────────────────────────────────────────────────
CD-SEM                      Top CD (mask and post-strip)           ≈ 20 sites,   fast; top only
                                                                   every lot
HV-SEM (30–60 keV BSE)      Bottom CD, top-to-bottom displacement  ≈ 10 sites,   10⁵–10⁶ holes
                            (twist, tilt)                          sampled lots  per wafer
OCD (spectroscopic          Average CD, depth, mask remaining     ≈ 10 sites,   weak sensitivity
ellipsometry/reflectometry) (model-based)                          every lot     at depth > 1 µm
CD-SAXS / X-ray             Average profile: CD vs depth, bow,     ≈ 5 sites,    minutes per site;
scatterometry               tilt, ellipticity                      sampled       best profile data
FIB/TEM cross-section       Full profile of a few holes            weekly per    destructive
                                                                   chamber
VC e-beam inspection        Not-open holes                         sampled area  Chapter 12
Electrical (capacitance,    C_s, contact R, shorts                 after the     weeks of latency
contact chains, bit maps)                                          module
```

### 15.2.2 Why OCD Weakens

Optical scatterometry relies on light reaching the features and returning. In a 2.1 µm mold with 45% open area at the top and 24% at the bottom, the light penetrating to the bottom is weak and the bottom parameters correlate strongly with the others. OCD remains useful for top CD, mask remaining, and average CD, but not for bottom CD or bow position at 91:1. X-ray scatterometry, whose wavelength is far below the feature size and which passes through the whole stack, takes over for the profile.

### 15.2.3 Sampling Plan

```
Sampling plan (R1, illustrative):

  Parameter          Method      Frequency                   Control use
  ───────────────────────────────────────────────────────────────────────
  Mask top CD        CD-SEM      every lot (pre-etch)        feed-forward
  Mold thickness     film        every lot (pre-etch)        feed-forward
  B-ACL thickness    film        every lot (pre-etch)        mask-margin check
  Top CD, post       CD-SEM      every lot                   feedback
  Bottom CD          HV-SEM      2 wafers/chamber/day        feedback
  Twist, tilt        HV-SEM      2 wafers/chamber/day        ring, alarms
  Profile, bow       CD-SAXS     1 wafer/chamber/day         feedback
  Cross-section      FIB/TEM     1 per chamber per week      model anchor
  Not-open           VC          sampled; sensitized monitor monitoring
                                 weekly per chamber
  C_s, shorts        electrical  per lot at module end       long-loop
```

---

## 15.3 Endpoint at the Bottom of a 91:1 Hole

### 15.3.1 The Signal

When the hole front passes from BPSG into the SiN stop, the bottom stops releasing oxygen and starts releasing nitrogen. Optical emission from CO and CN, and the ratio of SiF to Ar, change. The question is how much.

```
Fraction of the wafer area that is hole bottom:
  (π/4) × 19² / 1186 = 0.24 of the array; × 0.55 array efficiency = 0.13

Bottom etch rate relative to open area: 0.41 (R1)
Oxide removed at the bottom relative to the early etch (when 25% of the
  wafer etched at ≈ 0.9 ER₀): 0.13 × 0.41 / (0.25 × 0.9) ≈ 0.24

Change in CO emission when all holes reach the stop: ≈ 24% of the oxide
  contribution to CO, which is itself ≈ 20% of the total CO signal
  (the rest from C₄F₆ + O₂ chemistry and walls) → ≈ 5% total
Spread over the ≈ 20 s arrival distribution
```

A 5% change spread over 20 s is detectable as a knee in a filtered line ratio, but not sharp enough to time the overetch to a second. The knee is used as a check: if it arrives more than a few seconds from the expected time, the wafer is flagged and the overetch is extended by APC within limits.

### 15.3.2 Time-Based Control

The production etch is therefore time-based. The time is computed from the reduced-order model with feed-forward inputs, and the endpoint knee confirms it. For R2, where the stop is a metal oxide (Chapter 12), the endpoint signal at the stop is larger (the fluorine chemistry stops abruptly), and endpoint control is more practical.

---

## 15.4 Advanced Process Control

### 15.4.1 Feed-Forward

```
Inputs: mask top CD (CD-SEM), mold thickness, B-ACL thickness, BPSG dopant

Example: lot mean mask CD 0.5 nm below target
  Average CD deficit ≈ 0.45 nm → arrival delay ≈ 0.45 × 5.2 = 2.3 s
  Action: extend ME2 by 2.3 s (keeps the overetch margin for the tail)

Example: mold 18 nm thick (1.5σ)
  Arrival delay = 18 / 335 × 60 = 3.2 s → extend ME2 by 3.2 s

Mask-margin check: B-ACL 25 nm thin and the time extended by 5.5 s
  Facet margin: 128 − 25/2.67 − 5.5 = 113 s ≥ 60 s floor → proceed
```

### 15.4.2 Feedback

```
EWMA feedback on chamber offsets:
  offset_n+1 = offset_n + λ × (target − measured) / gain,  λ ≈ 0.3

Bottom CD feedback (knob: ME2 O₂; gain 0.12 nm per sccm):
  Measured 18.6 nm, target 19.0 → error +0.4 nm
  Full correction: +3.3 sccm; applied: 0.3 × 3.3 = +1.0 sccm

Bow feedback (knob: ME1 wafer temperature; gain 0.13 nm per K):
  Measured 27.9 nm, target 27.5 → error −0.4 nm
  Full correction: −3.1 K; applied: −0.9 K

Edge feedback: the 2×2 solution of Chapter 8 for edge O₂ split and edge
  temperature, with λ = 0.3
```

### 15.4.3 Consumable-Age Offsets

```
Electrode: O₂ +0.7 sccm per 100 RF hours (Chapter 9), reset at change
Ring: lift +25 µm per ≈ 17 RF hours, or continuous
Walls: first-wafer offset after WAC failure or idle > 2 h: dummy wafer or
  time offset
```

These offsets are predicted, not measured, and the feedback loop removes the residual. Without them, the feedback would chase a ramp and lag it by about 1/λ samples.

### 15.4.4 Virtual Metrology

Virtual metrology predicts the post-etch result of every wafer from data available during or right after the etch: chamber sensors (RF voltage and current harmonics, pressure, valve position, chuck temperatures, helium flows), optical emission spectra, and the incoming metrology. A surrogate model trained on the measured wafers predicts bottom CD, bow, and tilt for the unmeasured ones.

```
Virtual metrology performance (illustrative, R1 bottom CD):
  Prediction error σ ≈ 0.20 nm, against a wafer-to-wafer σ of 0.25 nm
  → explains ≈ 36% of the wafer-to-wafer variance
```

Virtual metrology does not replace measurement. It finds the wafers to measure, extends feedback to every wafer, and flags excursions minutes rather than days after the etch.

---

## Summary and Key Takeaways

1. **Feature-scale models are design tools.** Monte Carlo transport, site-balance kinetics, and level-set evolution, calibrated on depth series and cross-sections, predict the hole but run too slowly for control.

2. **Reduced-order models run the line.** The closed forms of this book, with chamber-dependent parameters, run in milliseconds inside APC.

3. **X-rays see what light cannot.** At 91:1, OCD loses the bottom; CD-SAXS and HV-SEM measure profile and placement.

4. **Endpoint is a check, not a clock.** The stop signal is about 5% and spread over 20 s; R1 runs on time with the knee as confirmation.

5. **APC has three layers.** Feed-forward from mask CD and mold, EWMA feedback on bottom CD, bow, and edge, and predicted consumable offsets.

6. **Virtual metrology extends the loop to every wafer.** It explains about a third of the wafer-to-wafer variance in bottom CD.

---

## Study Questions

1. A feature-scale model calibrated at 1.6 µm predicts k = 0.016 at 2.1 µm, but the full-depth depth series gives an apparent k of 0.018. Which term of Chapter 4 is the model missing, and how would you add it?

2. Estimate the endpoint signal change for R2, assuming a bottom rate of 0.52 ER₀ and an oxide share of CO of 30%.

3. A lot arrives with mask CD 0.8 nm small and mold 10 nm thin. Compute the feed-forward time change.

4. Bottom CD measurements over five days read 18.7, 18.8, 18.6, 18.9, 18.8 nm against a 19.0 target. Apply EWMA feedback with λ = 0.3 and a gain of 0.12 nm/sccm, starting from zero offset. What is the O₂ offset after day 5?

5. A virtual metrology model has prediction σ = 0.20 nm and the true wafer-to-wafer σ is 0.25 nm. If it is used to choose which wafers to measure, how many wafers per hundred would you measure to catch excursions of 0.6 nm with high probability?

---

**Next Chapter:** [Chapter 16: Mold Removal, Pillar Stability, Yield & Cost of Ownership](./16-mold-removal-yield-coo.md)

---

**Chapter 15 Development Status:** Complete  
**Version:** 1.0
