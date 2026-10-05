# Appendix F: Metrology & Modelling Reference

Metrology methods, sampling, feature-scale modelling inputs and outputs, and common pitfalls for extreme-aspect-ratio capacitor holes.

---

## F.1 Metrology Methods

```
Method              Principle                         Strengths                       Limits at 91:1
───────────────────────────────────────────────────────────────────────────────────────────────────────────
CD-SEM              Secondary electrons, 0.5–1 keV    Top CD, fast, every lot         Sees only the top
HV-SEM              BSE at 30–60 keV through the      Bottom CD, per-hole placement,  Bottom CD precision
                    mold                              10⁵–10⁶ holes per wafer          ≈ 0.5 nm; charging
OCD                 Spectroscopic ellipsometry or     Top CD, mask, average CD;       Bottom and bow weakly
                    reflectometry + model             inline                           determined
CD-SAXS / XRS       Transmission X-ray scattering     Profile vs depth, bow, tilt,    Minutes per site;
                    vs tilt angle                     ellipticity                      large pads
FIB/TEM             Destructive cross-section         Full profile, interfaces,       Few holes; hours;
                                                      residues                         sample prep artefacts
VC inspection       E-beam charging contrast          Not-open holes                  Area throughput
Electrical          C_s, contact R, shorts, bit maps  Function; the final truth       Weeks of latency
OES endpoint        Emission line ratios              Every wafer, real time          ≈ 5% signal, smeared
```

---

## F.2 Sampling and Control Use

See Chapter 15, Section 15.2.3, for the full sampling plan. Summary:

```
Feed-forward (every lot):  mask top CD, mold thickness, B-ACL thickness,
                           BPSG dopant
Feedback (daily/chamber):  bottom CD (HV-SEM), bow (CD-SAXS), tilt and
                           twist (HV-SEM)
Anchors (weekly/chamber):  FIB/TEM, sensitized not-open monitor
Long loop (per lot):       C_s, shorts, bit maps
```

---

## F.3 HV-SEM Notes

```
Beam energy: high enough for BSE from the bottom to escape 2.1 µm of oxide
  (30 keV marginal, 45–60 keV preferred at 2.1 µm)
Charging: thick oxide charges under the beam; low dose and frame
  averaging keep the image stable
Bottom CD: BSE edge is blurred by scattering in the oxide; calibrate to
  TEM; precision ≈ 0.5 nm
Placement: top and bottom centroids; precision ≈ 0.3 nm per hole
Sampling: ≥ 10⁵ holes per site for tail weight estimation
```

---

## F.4 CD-SAXS Notes

```
Wavelength ≪ CD; transmission through the wafer (high-energy X-rays) or
  grazing geometry
Model: stacked trapezoids or a spline of CD vs depth; include tilt and
  ellipticity; constrain mold layer thicknesses from film metrology
Correlation pitfalls: bow depth vs bow CD; bottom CD vs taper; constrain
  with priors from TEM
Throughput: ≈ 5–15 min per site (illustrative)
```

---

## F.5 Feature-Scale Model Inputs and Outputs

```
Inputs
  Plasma: IEADs by species and radius (from reactor model or retarding-
          field / angle-resolved measurements); neutral fluxes by species
          (from OES actinometry or a reactor model)
  Surface: yields Y(E, θ) per material; thresholds; sticking and reaction
           probabilities; reflection probability and energy loss;
           polymer removal yield; wall conductivity
  Geometry: mask stack and opening shape (from CD-SEM/AFM); mold layers

Outputs
  Profile vs time; ER(A) and k, k₂; bow depth and CD; bottom CD; mask
  erosion and facet; twist distribution (with random mask perturbations);
  charging potentials; sensitivity to each input

Calibration targets (Chapter 15)
  Depth series to full depth; cross-sections; mask remaining; HV-SEM
  twist; edge tilt vs ring height
```

---

## F.6 Reduced-Order Model Parameters

```
Parameter   Meaning                           R1 value          Updated from
──────────────────────────────────────────────────────────────────────────────
ER₀         Fitted intercept rate             700 nm/min        depth series
k, k₂       ARDE coefficients                 0.016, 2×10⁻⁵     depth series
r_b         Bow recession rate                0.22 nm/min/side  CD-SAXS, TEM
C, h_on     Twist law                         8.5×10⁻⁵, 690 nm  HV-SEM
r_m, f      Mask erosion, facet factor        1.67 nm/s, 1.6    TEM, OCD
Δt/Δw       Arrival delay per nm              5.2 s/nm          model / series
Edge lag    Bottom-stop delay at 147 mm       10 s              depth series
```

---

## F.7 Pitfalls

1. **Fitting ARDE short of full depth.** Under-predicts time to the stop by several seconds (Chapter 4).
2. **Reporting twist with the site mean included.** Mixes tilt into twist; remove the site mean first.
3. **Trusting OCD bottom CD at 91:1.** Its bottom parameters are poorly determined; use HV-SEM or CD-SAXS.
4. **Cross-section sampling bias.** FIB sites are chosen for convenience; holes at the array edge or near dummy rows differ from the interior.
5. **Ignoring HV-SEM blur.** Bottom CD read from BSE images is biased by scattering in the oxide; calibrate against TEM by depth and material.
6. **Endpoint as a clock.** The stop signal is too weak and smeared to time the overetch; use it as a check.
7. **Extrapolating surrogates.** Machine-learned surrogates fail outside their training domain; retrain after hardware, mask, or chemistry changes.

---

**Appendix F Version:** 1.0
