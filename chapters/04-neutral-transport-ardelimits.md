# Chapter 4: Neutral Transport, Surface Kinetics & the Limits of ARDE

## Overview

Chapter 3 showed that the ion flux at the bottom of a 91:1 hole falls only modestly from its value at 57:1, as long as the narrow ion population is well formed and the wall reflects. Yet the bottom etch rate falls to about 41% of the open-area rate. The rest of the slowdown comes from the neutrals and from the film of polymer and adsorbed species on the bottom surface. This chapter derives the linear ARDE law from a two-step surface model, shows what its coefficient means physically, explains why it bends at extreme aspect ratio, and computes the deepest hole that a chemistry and its mask can reach.

**Learning Objectives:**
- Apply the Clausing transmission and the Coburn–Winters model at L/d = 91 and 128
- Derive the linear ARDE law from an ion–neutral series model and interpret k
- Compute the time-to-depth curve, the bottom rate, and ∂h/∂w for R1 and R2
- Explain why ARDE becomes non-linear above about A = 100
- Compute the mask-limited and facet-limited maximum depth
- Describe the fluorocarbon and HF chemistry at the bottom of an extreme hole

---

## 4.1 Neutral Transport Beyond L/d = 90

### 4.1.1 Clausing Transmission

```
Long-tube limit: K ≈ 4d / (3L)  (or 1/(1 + 3L/(4d)) as a smooth form)

  Tube                          L/d     K
  ──────────────────────────────────────────
  Book #29 mold at stop          57     0.023
  R1 mold at stop                91     0.015
  R1 mask + mold at stop        128     0.010
  1e mold (2.35 µm, 21 nm)      112     0.012
```

### 4.1.2 Coburn–Winters

```
Γ_bottom / Γ_top = K / (K + β (1 − K))

At L/d = 128 (K = 0.0104):
  Species       β        Γ_bottom/Γ_top
  ─────────────────────────────────────
  F             0.01     0.51
  HF (cryo)     0.005    0.68
  CF₂           0.05     0.17
  CF / C₂F₄...  0.20     0.05
  O             0.05     0.17
```

Compared with the 1b hole (Book #29: F 0.70, CF₂ 0.32, CF 0.11), every species has lost about a third to a half of its bottom flux. The loss is largest for the polymer precursors and smallest for fluorine. **The bottom of the 91:1 hole is fluorine-rich and carbon-poor relative to the 57:1 hole.** This shifts the bottom balance toward etch and away from polymer, which is why extreme holes tend to taper less at the very bottom than the ARDE slowdown would suggest, and why they gouge the pad more easily once open (Chapter 12).

### 4.1.3 Wall Loss

Walls coated in polymer consume radicals. A wall reaction probability s_w adds an exponential attenuation to the Clausing transmission:

```
Decay length along the hole: λ_w ≈ d / √(2 s_w)  (s_w ≪ 1)
In aspect-ratio units: A_w = λ_w / d = 1 / √(2 s_w)

  s_w         A_w     Extra attenuation at A = 91
  ─────────────────────────────────────────────────
  1×10⁻⁴      71        exp(−91/71) = 0.28
  3×10⁻⁵     129        exp(−91/129) = 0.49
  1×10⁻⁵     224        exp(−91/224) = 0.67
```

At 57:1 a wall loss of 3×10⁻⁵ costs 36% of the flux. At 91:1 it costs 51%. Wall loss is the reason the polymer state of the wall, and therefore the wafer temperature and the chamber condition, matter more as the hole deepens.

---

## 4.2 Where the Linear ARDE Law Comes From

### 4.2.1 A Two-Step Surface Model

At the bottom, each oxide molecule needs an ion to supply energy and neutrals to supply the fluorine. Treat these as two resistances in series:

```
1/ER = 1/R_i + 1/R_n

R_i = Y Γ_i              (ion-driven step)
R_n = (s/ν) Γ_n,bottom   (neutral supply; s: reaction probability at the
                          bottom; ν: neutrals consumed per SiO₂)

Coburn–Winters for the neutral flux at the bottom:
  Γ_n,bottom = Γ_n0 K / (K + s(1 − K))
→ 1/R_n = ν/(s Γ_n0) + ν (1 − K) / (K Γ_n0)

Long tube: (1 − K)/K = 3A/4
→ 1/ER = [1/R_i + ν/(s Γ_n0)] + (3/4) ν A / Γ_n0
       = 1/ER₀ + (3/4) ν A / Γ_n0
```

So:

```
ER = ER₀ / (1 + k A),   k = (3/4) · χ,   χ = ν ER₀ / Γ_n0
```

### 4.2.2 What k Means

The ARDE coefficient is three-quarters of **χ, the ratio of the neutral consumption at the open surface to the neutral supply**. A small k means the open surface uses only a small fraction of the reactive neutrals that arrive, so that a long tube can still deliver enough.

```
R1:  k = 0.016 → χ = 0.021  (the open surface uses ≈ 2% of the supply)
R2:  k = 0.010 → χ = 0.013
Book #29: k = 0.020 → χ = 0.027
```

The design rule that follows is the most important in extreme-aspect-ratio etch: **run neutral-rich, so that the open surface is ion-limited by a wide margin.** Every change that raises χ, such as more ion flux at the same gas, a more polymerizing gas that reduces the effective etchant supply, or a lower flow, raises k. The ion fraction at the bottom (Chapter 3) and the polymer film (Section 4.4) add corrections, but the leading term is χ.

### 4.2.3 The Intercept Is Not the Blanket Rate

The broad ion population is lost in the first few hundred nanometres (Chapter 3). The intercept ER₀ of a fitted depth series is therefore a little below the blanket rate measured on an unpatterned wafer, typically by 5–10%. The reference ER₀ = 700 nm/min is the fitted intercept, not the blanket rate.

---

## 4.3 Time to Depth for R1 and R2

### 4.3.1 The Curves

```
t(h) = G(h) / ER₀,  G(h) = h + k h² / (2w),  w = 23 nm

                         R1 (k 0.016, ER₀ 700)     R2 (k 0.010, ER₀ 1100)
  h (nm)     A          ER/ER₀    t (min)           ER/ER₀    t (min)
  ─────────────────────────────────────────────────────────────────────
    200      8.7        0.88      0.31              0.92      0.19
    500     21.7        0.74      0.84              0.82      0.50
   1000     43.5        0.59      1.93              0.70      1.11
   1400     60.9        0.51      2.97              0.62      1.66
   2000     87.0        0.42      4.84              0.53      2.61
   2100     91.3        0.41      5.19              0.52      2.78
```

The last third of the depth (1400 to 2100 nm) takes 2.22 min in R1, 75% of the 2.97 min needed for the first two-thirds. In R2 it takes 1.12 min, 67% of 1.66 min.

### 4.3.2 Depth Sensitivity to CD

```
∂h/∂w = (k h² / (2 w²)) / (1 + k h / w)

R1 at h = 2100, w = 23:
  numerator   0.016 × 2100² / (2 × 23²) = 70,560 / 1058 = 66.7
  denominator 1 + 0.016 × 2100 / 23 = 2.46
  ∂h/∂w = 27.1 nm per nm

R2 at h = 2100: numerator 41.7, denominator 1.91 → 21.8 nm per nm
Book #29 at h = 1600, w = 28: 15.2 nm per nm
```

```
Scaling of ∂h/∂w with aspect ratio at fixed k:
  ∂h/∂w = (k A² / 2) / (1 + k A)
  kA ≪ 1:  ∝ A²      kA ≫ 1:  ∝ A / 2
  R1 at A = 91 (kA = 1.46): between the two regimes, growing ≈ A^1.4
```

### 4.3.3 What It Means for Overetch

```
Holes 3σ narrow (reference: 3σ = 1.0 nm on top CD → ≈ 0.9 nm on CD_avg):

  R1: 27 nm/nm × 0.9 nm = 24 nm behind; bottom rate in BPSG ≈ 335 nm/min
      → 4.3 s
  Family offset (SADP×2: one family 1.0 nm narrow) → 27 nm → 4.8 s
  Mold 3σ thick (Chapter 2): 4.3 s
  Wafer-edge lag (Chapter 9): ≈ 10 s
  Bottom-stop arrival spread and margin: ≈ 15 s
  RSS of the first four: √(4.3² + 4.8² + 4.3² + 10²) ≈ 13 s
  Plus margin: ≈ 13 + 15 ≈ 28 s → reference OE 40 s
  (rounded up for the slow-hole tail; Chapter 12)
```

---

## 4.4 Why ARDE Turns Non-Linear

### 4.4.1 Three Corrections

The linear law fits depth series well up to about A = 80–100. Beyond that the measured rate falls faster. Three mechanisms add terms:

1. **Ion fraction.** The narrow-ion transmission falls slowly with A (Chapter 3), adding a term that grows roughly linearly with A.
2. **Wall loss.** Section 4.1.3 multiplies the neutral supply by exp(−A/A_w). Expanded, this adds a term in A² to 1/ER.
3. **Polymer at the bottom.** As the hole deepens, the bottom sees fewer ions per depositing neutral at certain depths, and the steady-state film thickens. The yield per ion falls as exp(−t_fc/λ_E).

### 4.4.2 An Extended Fit

```
ER = ER₀ / (1 + k A + k₂ A²)

R1 (illustrative): k = 0.016, k₂ = 2×10⁻⁵

  A       Linear ER/ER₀     Extended ER/ER₀    Difference
  ──────────────────────────────────────────────────────────
   57        0.52              0.51               −3%
   91        0.41              0.38               −6%
  110        0.36              0.33               −8%
  130        0.32              0.29              −10%
  150        0.29              0.26              −12%
```

The quadratic term is invisible at 57:1 and costs 6% at 91:1. A recipe developed and fitted at 60:1 will under-predict the time to reach 2.1 µm by several seconds. **Extreme-aspect-ratio recipes must be fitted with depth series that reach the full depth**, which is one reason deep cross-sections at several times are part of every recipe qualification (Appendix C).

### 4.4.3 Etch Stop

At some depth the bottom stops etching altogether. The usual cause in fluorocarbon chemistry is the polymer: low-sticking, carbon-rich species reach the bottom, the ion energy flux there is no longer enough to clear them, and the film thickens until the yield collapses. The aspect ratio at which this happens is not a fixed property of the chemistry. It moves with O₂, with temperature, with the wall condition, and with the hole CD. Chapter 12 treats it as a statistical tail: a few holes in a billion stop long before the mean hole would.

---

## 4.5 The Deepest Hole

### 4.5.1 The Mask Limit

The mask erodes at a roughly constant rate while the hole slows down. The etch must end before the mask does.

```
R1 mask erosion rate: ≈ 600 nm / 359 s = 1.67 nm/s
Available mask: 1450 nm − 500 nm minimum = 950 nm
Facet grows ≈ 1.6× faster than the flat mask (Chapter 13)

Flat-mask limit:
  t_total = 950 / 1.67 = 569 s; minus bottom open 35 s → 534 s of main etch
  G = 700 × 534/60 = 6230 nm
  Solve h + (k/2w) h² = G, k/2w = 3.48×10⁻⁴ nm⁻¹:
  h = (−1 + √(1 + 4 × 3.48×10⁻⁴ × 6230)) / (2 × 3.48×10⁻⁴) = 3030 nm
  → A ≈ 132

Facet limit (facet reaches the top of the mold):
  usable time ≈ 284 s of main etch + 120 s of facet margin = 404 s
  G = 700 × 404/60 = 4713 nm → h ≈ 2510 nm → A ≈ 109
```

### 4.5.2 For R2

```
R2 mask erosion ≈ 420 nm / 190 s = 2.2 nm/s (faster per second, but the
etch is much faster per nanometre of depth)
Flat-mask limit: ≈ 400 s of main etch → G = 7330 nm → h ≈ 3.95 µm, A ≈ 172
Facet limit:     ≈ 300 s of main etch → G = 5560 nm → h ≈ 3.25 µm, A ≈ 141
```

### 4.5.3 Comparison

```
Maximum depth for a 23 nm hole with the reference B-ACL mask:

                       Facet-limited       Flat-mask limited
  ─────────────────────────────────────────────────────────────
  R1 fluorocarbon      2.5 µm (A ≈ 109)    3.0 µm (A ≈ 132)
  R2 cryogenic         3.25 µm (A ≈ 141)   3.95 µm (A ≈ 172)
  Reference mold       2.1 µm (A = 91)
```

R1 has about 20% of depth headroom against the facet. That is less than one generation. **R1 can make the 1d capacitor but not, with the same mask, the 1e capacitor.** A more selective mask, R2 chemistry, or a two-tier mold (Chapter 14) is needed for the next step. Placement (Chapter 11) and bow (Chapter 10) may bind before any of these.

---

## 4.6 Chemistry at the Bottom

### 4.6.1 Fluorocarbon (R1)

```
R1 main-etch gas (illustrative):
  C₄F₆ 30 sccm, C₄F₈ 15 sccm, O₂ 32 sccm, Ar 300 sccm, NF₃ 0–10 sccm
  (ramped with depth, Chapter 8)

Roles at extreme depth:
  C₄F₆     high C/F; protective sidewall polymer near the top; selectivity
           to the carbon mask
  C₄F₈     more F per C; deeper-reaching CF₂ precursors
  O₂       burns excess carbon at the bottom; controls the polymer index
  NF₃      extra fluorine late in the etch, when the bottom becomes polymer-
           limited
  Ar       carries the narrow ion population; dilutes the polymerizing gases
```

At 91:1, ion-borne fluorine (CF₃⁺, CF₂⁺, and fragments of C₄F₆⁺) becomes a significant share of the fluorine reaching the bottom, because ions are transmitted far better than CF₂ radicals (0.52 against 0.17). The ion composition, which depends on the dilution and the source power, therefore enters the bottom chemistry directly.

### 4.6.2 HF-Based and Cryogenic (R2)

At low wafer temperature, HF and H₂O adsorb on the oxide surface and form a thin layer that ions drive into SiF₄ and H₂O. The adsorbed layer is supplied not only by flux down the hole but also by surface diffusion along the wall, so the supply term of Section 4.2 is larger and χ smaller. Chapter 7 develops this.

```
R2 main-etch gas (illustrative):
  HF 200 sccm (or H₂ + fluorocarbon to form HF in the plasma),
  C₄F₈ 20 sccm, O₂ 10 sccm, Ar 100 sccm; wafer −60 °C
```

### 4.6.3 Selectivity Against Depth

```
Selectivity to B-ACL (blanket → effective):
  R1: 8 → 3.5        R2: 11 → 5.0
Oxide : SiN in the main-etch and overetch chemistry (at the hole bottom):
  R1: ≈ 6 in ME, ≈ 15 in the SiN-selective overetch
      (the supports are cut by separate blended steps at a nitride rate
      0.70 of the oxide rate, Chapter 8)
  R2: ≈ 1.1–1.2 (one chemistry cuts oxide and nitride alike)
SiN : W in the bottom-open step: ≈ 6 (both)
```

R2's low oxide-to-nitride selectivity is an advantage for the supports, which it cuts with no change of chemistry, and a disadvantage for the bottom stop, which it cannot rely on to stop the etch (Chapter 12).

---

## Summary and Key Takeaways

1. **Neutrals lose a third to a half.** At L/d = 128, F reaches the bottom at 51% of its top flux and CF₂ at 17%, both well below their 1b values.

2. **Linear ARDE is a series model.** k = (3/4)χ, with χ the fraction of the neutral supply the open surface consumes. R1 uses about 2% of its supply; R2 about 1.3%.

3. **Width becomes depth at 27 nm per nm.** R1's ∂h/∂w at full depth is 27.1; R2's is 21.8; Book #29's was 15.2.

4. **ARDE bends above 100:1.** A quadratic term from wall loss and polymer costs 6% at 91:1 and 10% at 130:1. Fit depth series all the way down.

5. **The mask sets the deepest hole.** R1 with the reference mask reaches about 2.5 µm before the facet reaches the mold; R2 reaches about 3.25 µm.

6. **The bottom chemistry changes with depth.** At 91:1, ions carry a growing share of the fluorine to the bottom, and the polymer precursors are the most depleted species.

---

## Study Questions

1. Compute K and the Coburn–Winters bottom fraction for F and CF₂ at L/d = 155 (1e with mask). Compare with the 1d values.

2. Show that the series model with Clausing transmission gives k = (3/4)χ. If the Ar dilution is reduced so that χ rises by 30%, what is the new k and the new t(2100) for R1?

3. A depth series in R1 gives 1000 nm at 1.95 min and 2000 nm at 5.05 min. Fit ER₀ and k with the linear law. Then compute what k₂ would be needed to explain the second point with the reference ER₀ and k.

4. Using the reference mask and R1, compute the facet-limited maximum depth for a 21 nm hole. Express it as an aspect ratio.

5. A W-ACL mask with effective selectivity 4.8 in R1 is introduced at the same thickness. Recompute the facet-limited maximum depth, assuming the erosion rate falls in proportion to the selectivity.

6. Explain why the bottom of a 91:1 hole can be fluorine-rich relative to a 57:1 hole while the etch rate there is lower.

---

**Next Chapter:** [Chapter 5: Extreme-Power CCP Platforms](./05-extreme-power-ccp-platforms.md)

---

**Chapter 4 Development Status:** Complete  
**Version:** 1.0
