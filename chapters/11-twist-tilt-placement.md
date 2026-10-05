# Chapter 11: Twist, Tilt & Bottom Placement at Extreme Depth

## Overview

A capacitor hole that is not straight lands in the wrong place. Two kinds of error move the bottom. **Tilt** is systematic: every hole in a region leans the same way, usually outward at the wafer edge, because the sheath there is not parallel to the wafer. **Twist** is random: each hole wanders on its own, because small asymmetries in its mask, its polymer, and its wall charge bend the ions that cut it. At 57:1 both were real but within budget. At 91:1 they are three-quarters of the placement variance, and twist, which grows faster than the depth, is the larger.

This chapter builds a model in which twist is a random walk in angle that starts at an onset aspect ratio, derives the 1.5-power growth law that follows, calibrates it to R1 and R2, describes edge tilt and how it is controlled, rebuilds the placement budget with lithographic pre-compensation, and treats the tail of the placement distribution.

**Learning Objectives:**
- Explain why twist appears only above an onset aspect ratio
- Derive the growth law σ_x ∝ (h − h_on)^1.5 from a random walk in angle
- Calibrate the twist model and use it to predict twist at other depths
- Model edge tilt and compute the ring and lithography corrections
- Rebuild the placement budget and identify the dominant terms
- Estimate the placement failure rate and explain why the tail is not Gaussian

---

## 11.1 Twist as an Instability

### 11.1.1 What Keeps a Hole Straight

A shallow hole is self-centring. If its front drifts slightly to one side, the narrow ion population, reflecting from the near wall more than the far wall, etches the far side of the front faster and pulls it back. The funnel of Chapter 3 is a restoring force.

### 11.1.2 What Bends It

Three things push the other way:

1. **Asymmetric charge.** A wall that has collected slightly more charge on one side deflects ions toward the other (Chapter 3).
2. **Asymmetric polymer.** A thicker polymer patch on one side narrows the hole there and sends reflected ions across.
3. **Asymmetric mask.** A mask opening that is not round, or a facet that is deeper on one side, launches ions with a preferred direction.

Each of these is self-reinforcing. A hole bent slightly to one side exposes more wall to ions on that side, which collects more charge and less polymer, which bends it further.

### 11.1.3 The Onset

The restoring force weakens as the hole deepens, because the narrow ions that reflect near the front are fewer and their reflections less frequent. The destabilizing forces strengthen, because more wall is charged. At an onset aspect ratio the two cross:

```
Onset aspect ratio (illustrative, from HV-SEM depth series):
  R1:  A_on ≈ 30  → h_on = 30 × 23 = 690 nm
  R2:  A_on ≈ 35  → h_on ≈ 800 nm (conductive wall layer)
  Book #29 (1b): A_on ≈ 28
```

Above the onset, holes begin to wander.

---

## 11.2 The Growth Law

### 11.2.1 A Random Walk in Angle

Treat the direction of each hole's front, θ, as a random walk that starts at the onset depth. Each increment of depth adds a small random change of angle, independent of the last:

```
⟨θ²⟩(h) = D_θ (h − h_on),   h > h_on

The lateral displacement of the front is the integral of the angle:
  x(h) = ∫ θ dh' from h_on to h

For a random walk in θ, the variance of the integral is
  ⟨x²⟩(h) = D_θ (h − h_on)³ / 3

→ σ_x ∝ (h − h_on)^1.5
```

The lateral wander of the bottom grows as the 1.5 power of the depth beyond onset. This is faster than linear, and it is why each generation's twist grows by more than its depth.

### 11.2.2 Calibration

```
R1 at h = 2100 nm: 3σ twist = 4.5 nm → σ_x = 1.5 nm
  D_θ = 3 σ_x² / (h − h_on)³ = 3 × 2.25 / 1410³ = 2.4×10⁻⁹ rad²/nm
  RMS angle at the bottom: √(D_θ × 1410) = 1.84×10⁻³ rad = 0.11°

R2 at h = 2100 nm: 3σ twist = 3.0 nm, h_on = 800 nm
  D_θ = 3 × 1.0 / 1300³ = 1.4×10⁻⁹ rad²/nm
  RMS angle at the bottom: 0.077°
```

The final angle of the hole near its bottom varies by about 0.1° RMS from hole to hole. That angle is measurable by HV-SEM and by cross-section, and it is a better early indicator of twist than the displacement, because it responds to D_θ directly.

### 11.2.3 Predictions

```
R1 model: 3σ twist = 8.5×10⁻⁵ × (h − 690)^1.5 nm  (h in nm)

  h (nm)     3σ twist (nm)    Comment
  ──────────────────────────────────────────────────
  1600         2.3            same chemistry, Book #29 depth
  1863         3.4            81:1 at w = 23
  2093         4.5            91:1 (reference)
  2350         5.7            1e depth at w = 23 (w = 21 is worse)
```

Going from 81:1 to 91:1 adds 31% to the twist. Going to 1e depth adds another 28%, before the narrower hole and the lower onset depth are counted. **Twist is the first term of the placement budget to fail at 1e.**

### 11.2.4 What Sets D_θ

```
D_θ scales with:
  (ΔV_wall / E_i)²    asymmetric charge relative to ion energy
  (Δt_poly / w)²      polymer asymmetry relative to hole size
  (e_mask)²           ellipticity and facet asymmetry of the mask opening
  1 / (narrow-ion share)  weaker restoring force

Illustrative effects on R1's 3σ twist:
  Ion energy 4.5 → 5.5 keV           4.5 → 3.8 nm
  Pulsing off (CW)                   4.5 → 6.0 nm
  DC superposition off               4.5 → 5.2 nm
  Mask ellipticity doubled           4.5 → 5.4 nm
  Pressure 15 → 20 mTorr             4.5 → 5.3 nm
  R2 chemistry                       4.5 → 3.0 nm
```

---

## 11.3 Edge Tilt

### 11.3.1 The Edge Sheath

At the wafer edge the sheath boundary bends toward the focus ring if the ring's sheath is thinner, and away if thicker. Ions cross the sheath perpendicular to its boundary and arrive tilted.

```
Edge-tilt model (illustrative):
  θ_tilt(r) = θ_edge × exp(−(R_w − r) / λ_e)
  R_w = 150 mm; λ_e ≈ 5 mm (sheath-scale decay)

  θ_edge = 0.12° (ring slightly low):
    r = 147 mm: 0.12 × exp(−0.6) = 0.066°
    r = 140 mm: 0.12 × exp(−2.0) = 0.016°
    r = 130 mm: 0.002°
```

Edge tilt is a problem of the outer 10–15 mm, but that region holds about 18% of the dies.

### 11.3.2 Controlling It

1. **Ring height.** The ring is lifted as it erodes (Chapter 9): about 0.08° per 100 µm.
2. **Ring RF.** Some chambers drive the ring, or an electrode beneath it, with a fraction of the bias, which adjusts its sheath electrically and can follow erosion without moving parts.
3. **Mask-open tilt.** The mask-open etch has its own edge tilt, which launches the capacitor ions along the mask's direction. The two tilts add, so the mask-open chamber must be matched to the capacitor chamber.

### 11.3.3 Lithographic Pre-Compensation

Tilt is systematic: at a given radius and ring age, its direction and magnitude are known. Only the bottom of the hole must land on the pad; the top lands on nothing. The lithography can therefore shift the hole pattern at the wafer edge radially inward by the expected tilt displacement, so that tilted holes land centred.

```
Mean tilt at 147 mm: 0.066° → displacement at 2.1 µm: 2.4 nm outward
Litho pre-compensation: shift the pattern 2.4 nm inward at 147 mm
  (a radial overlay correction term)

Residual tilt after pre-compensation: ring-wear variation ±0.02°
  → ±0.73 nm at 2.1 µm
```

The cost is that the top of the hole is offset relative to the lattice of the top support pattern, which is aligned later. That pattern can be shifted in the same way.

---

## 11.4 The Placement Budget

### 11.4.1 Without and With Pre-Compensation

```
Bottom-placement budget (3σ, illustrative):

  Term                               Ch. 1 (no pre-comp)   With pre-comp
  ───────────────────────────────────────────────────────────────────────
  Lithographic overlay                   3.0                  3.0
  Mask-open shift and tilt               1.5                  1.5
  Edge tilt residual                     3.7                  0.7
  Twist (R1)                             4.5                  4.5
  ───────────────────────────────────────────────────────────────────────
  RSS                                    6.7                  5.7

  With R2 (twist 3.0):                   5.6                  4.4
  Limit                                  7.0                  7.0
```

Pre-compensation frees about 1 nm of the budget. Twist is then the only large term. At 1e depth, with the R1 twist of 5.7 nm, even the pre-compensated budget reaches 6.7 nm on a pad that has also shrunk.

### 11.4.2 Scaling the Budget

```
Placement budget at 1e (illustrative): pad 19 nm, bottom CD 17 nm,
  required overlap 12 nm → |Δ| ≤ (19 + 17)/2 − 12 = 6 nm

  Overlay 2.7, mask open 1.3, tilt residual 0.8, twist (R1) 6.4 (w = 21):
  RSS = 7.1 nm → exceeds 6 nm
  Twist (R2) 4.2: RSS = 5.2 nm → meets 6 nm
```

At 1e, R1 cannot meet the placement budget. R2 can, with little margin. A two-tier mold, which restarts the twist at the tier boundary, is the other route (Chapter 14).

---

## 11.5 The Tail

### 11.5.1 When Placement Fails

The 7 nm budget is a design point for contact resistance. A hole fails functionally only when the overlap becomes very small:

```
Functional failure (high-resistance or open contact) at overlap < ≈ 5 nm
  → |Δ| > 20 − 5 = 15 nm

Gaussian estimate (σ = 5.7/3 = 1.9 nm with pre-comp):
  Z = 15 / 1.9 = 7.9 → P ≈ 3×10⁻¹⁵ per hole (two-sided) — negligible
```

### 11.5.2 Why the Tail Is Fatter

The random-walk model gives Gaussian displacements for each hole, but the D_θ of each hole is not the same. A hole with an elliptical mask opening, or a polymer defect, has a larger D_θ. The population is a mixture, and its tail is set by the worst subpopulation.

```
Mixture model (illustrative):
  99.9999% of holes: σ_x = 1.5 nm
  1 in 10⁶:          σ_x = 4.5 nm (3× D_θ^½, e.g., elliptical mask)
  Other terms (overlay, mask open, tilt residual): 3σ 3.4 nm → σ 1.1 nm
  P(|Δ| > 15 nm) ≈ 10⁻⁶ × 2 × P(Z > 15/√(4.5² + 1.1²)) = 10⁻⁶ × 2 × P(Z > 3.2)
               ≈ 10⁻⁶ × 1.2×10⁻³ ≈ 1.2×10⁻⁹ per hole → ≈ 32 per die
```

A subpopulation of one hole in a million with three times the normal twist produces about 32 misplaced contacts per die, six times the whole not-open budget of Chapter 1. **The placement tail is set by the mask and polymer outliers, not by the mean twist.** HV-SEM sampling of 10⁵–10⁶ holes per wafer can see the subpopulation; it cannot see the 10⁻⁹ tail directly. Electrical tests and bit maps find what is left (Chapter 16).

---

## 11.6 Measuring Twist and Tilt

```
Method                          What it sees                  Throughput
─────────────────────────────────────────────────────────────────────────────
HV-SEM (30–60 keV BSE)          Top and bottom of each hole    10⁵–10⁶ holes per
                                through 2 µm of oxide;         wafer in minutes
                                displacement per hole
Cross-section (FIB/TEM)         Full profile of a few holes;   hours per site
                                angle along depth
CD-SAXS                         Average tilt over the beam     minutes per site
                                spot from asymmetry of the
                                scattering
Electrical (contact chain)      Resistance tail                after electrode
```

Twist is reported as the 3σ of the bottom-minus-top displacement after removing the site mean. Tilt is the site mean. Appendix C gives the HV-SEM procedure.

---

## Summary and Key Takeaways

1. **Twist is an instability.** Below an onset aspect ratio (about 30 for R1), the ion funnel keeps holes straight; above it, asymmetries grow.

2. **A random walk in angle gives a 1.5-power law.** σ_x ∝ (h − h_on)^1.5. R1's 3σ twist is 4.5 nm at 2.1 µm and would be 5.7 nm at 2.35 µm.

3. **The bottom angle varies by about 0.1° RMS.** It is a direct measure of the twist diffusion D_θ.

4. **Edge tilt is systematic and pre-compensable.** Shifting the lithographic pattern inward at the edge removes the mean tilt and frees about 1 nm of budget.

5. **Twist decides 1e.** With pre-compensation, R1 meets the 1d budget but not the 1e budget; R2 meets both.

6. **The tail comes from outliers.** One hole in a million with three times the normal twist produces more misplaced contacts than the whole not-open budget.

---

## Study Questions

1. Using the R1 twist model, at what depth does the 3σ twist reach 6 nm? Express it as an aspect ratio at w = 23 nm.

2. Show that a random walk in angle gives ⟨x²⟩ = D_θ (h − h_on)³ / 3. What exponent would a constant random angle (set once at the onset) give?

3. Compute the edge tilt at 145 mm for θ_edge = 0.15° and λ_e = 5 mm. What litho pre-compensation is needed for a 2.1 µm hole?

4. Rebuild the 1e placement budget with an overlay of 2.4 nm and R2 twist. What margin remains?

5. In the mixture model, how rare must the high-twist subpopulation be for the misplacement rate to fall below 2×10⁻¹⁰ per hole?

---

**Next Chapter:** [Chapter 12: Etch Stop, Not-Open Holes & Rare-Event Statistics](./12-etch-stop-rare-events.md)

---

**Chapter 11 Development Status:** Complete  
**Version:** 1.0
