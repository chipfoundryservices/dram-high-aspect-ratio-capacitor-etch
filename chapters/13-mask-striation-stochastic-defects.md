# Chapter 13: Mask Erosion, Faceting, Striation, Distortion & Stochastic Defects

## Overview

Everything the capacitor etch does, it does through the mask. The mask sets the opening, launches the ions, and shapes the top of the hole. As it erodes, its facets descend toward the mold, and the ions they reflect move with them. Its sidewall roughness becomes the striation of the hole. Its outliers, the few openings in a billion that are too small, too large, misshapen, or merged, become the not-open holes and bridged pairs of Chapters 10 and 12. At 91:1 the etch amplifies every one of these mask properties more than it did at 57:1.

This chapter follows the mask through the etch, quantifies the facet and its margin, explains striation and hole distortion including the hexagonal distortion peculiar to tight honeycombs, and treats stochastic patterning defects and the way the etch amplifies them.

**Learning Objectives:**
- Model mask erosion and facet descent and compute the facet margin
- Relate facet position to the top CD, the neck, and the bow
- Explain the transfer of mask sidewall roughness into hole striation
- Explain hexagonal and elliptical hole distortion and their depth dependence
- List the stochastic defects of hole patterning and their etch amplification factors
- Set mask-side requirements that keep the etch tails within budget

---

## 13.1 The Mask Through the Etch

### 13.1.1 Flat Erosion

```
R1, B-ACL at the start of the etch: 1450 nm
Flat erosion rate (average over the recipe): 600 nm / 359 s = 1.67 nm/s

  Time (s)    Front depth (nm)    Flat mask left (nm)
  ──────────────────────────────────────────────────
     0              0                 1450
   105            900                 1275
   200           1570                 1116
   284           2080                  976
   359           2100 (open)           850
```

The erosion is not uniform in time. It is faster in the high-bias lower-oxide step and slowest in the bottom open. The average is adequate for budgeting.

### 13.1.2 The Facet

At the top edge of each opening, ions strike the corner at oblique incidence, where the sputter yield of carbon is highest (near 60° from normal). The corner becomes a facet that descends faster than the flat surface.

```
Facet foot descent rate ≈ 1.6 × flat rate = 2.67 nm/s (illustrative)
Height of the facet foot above the mold top:
  z_f(t) = 1450 − 2.67 t

  t = 0 s:    1450 nm
  t = 284 s:   692 nm
  t = 359 s:   491 nm

Limit (the facet must stay ≥ 150 nm above the top support, or reflected
  ions open the top of the mold): reached at t ≈ 487 s
Facet margin after the reference recipe: 487 − 359 ≈ 128 s (≈ 120 s, Chapter 2)
```

### 13.1.3 What the Facet Does Below It

```
Facet angle ≈ 45–60° from vertical at its steepest
Ions striking the facet reflect at large angles and hit the mask sidewall
  just below; ions striking the lower, steeper part of the facet reflect at
  a few degrees and enter the hole

As z_f falls:
  the top CD of the mask opening grows (≈ +1 nm over the R1 etch)
  the neck moves up into the mask and the polymer that formed it thins
  the bow grows by ≈ 0.3 nm per 100 nm of facet descent in the last third
  of the etch (illustrative)
```

This is the link between the mask budget and the bow (Chapter 10): a thinner or less selective mask brings the facet down sooner, and the last part of the etch then cuts the bow with ions launched from a lower, steeper facet.

### 13.1.4 Mask Variation

```
Incoming B-ACL thickness: 1500 ± 30 nm (3σ)
Effect on facet margin: ± 30 / 2.67 ≈ ± 11 s
Selectivity variation (deposition-temperature driven, ± 5%):
  ± 30 nm of erosion → ± 11 s
```

A thin-mask, low-selectivity wafer loses about 20 s of the 128 s facet margin. The margin remains positive for R1 at 2.1 µm, which is why the reference specification of 500 nm remaining flat mask is sufficient. At 2.35 µm it would not be.

---

## 13.2 Mask Materials and the Hole

### 13.2.1 Beyond Selectivity

```
Mask property            Effect on the hole                            B-ACL vs ACL
─────────────────────────────────────────────────────────────────────────────────────
Selectivity              Facet margin; total aspect ratio              higher
Hardness / modulus       Wiggling of the mask lines between holes      higher (less
                         under stress; shape of the opening             wiggle)
Conductivity             Charge on the mask; deflection at entry       slightly higher
Etch residues            Strip difficulty after the etch               harder (B)
Sidewall roughness       Striation (Section 13.3)                      similar
```

### 13.2.2 Mask Wiggling

A tall carbon mask, patterned into a honeycomb, is a lattice of thin carbon walls 11 nm wide and 1.45 µm tall. Its own aspect ratio is 130:1. Under the compressive stress of the film and the heat of the etch, these walls can buckle slightly, distorting the openings. Doping the carbon raises its modulus and reduces wiggling; so does a lower deposition stress and a cooler wafer.

---

## 13.3 Striation

### 13.3.1 From Mask to Wall

The sidewall of the mask opening is never perfectly smooth. Its roughness, typically 1–1.5 nm (3σ) with correlation lengths of 10–30 nm around the circumference, is transferred into the hole wall as vertical grooves: striations.

```
Transfer of roughness into the hole (illustrative):
  Long-wavelength components (one or two lobes around the circumference):
    transferred and amplified with depth → ellipticity and twist
  Short-wavelength components (6+ lobes): smoothed by polymer and by
    the ion angular spread over the first few hundred nm
```

### 13.3.2 Why It Matters at 91:1

1. **Wall thickness.** A striation 1 nm deep on each of two neighbouring holes, aligned, thins the 9.5 nm bow wall to 7.5 nm locally.
2. **Twist seeding.** The low-order lobes are the "mask asymmetry" term in D_θ (Chapter 11).
3. **Electrode roughness.** The TiN replicates the wall; a striated electrode has higher local fields and higher dielectric leakage at the ridges.

---

## 13.4 Hole Distortion

### 13.4.1 Ellipticity

```
Ellipticity e = (a − b)/(a + b), a and b the major and minor diameters

At the top (from the mask):  e ≈ 0.02 (0.5 nm on 26 nm)
At the bottom, R1:           e ≈ 0.04–0.06
```

Ellipticity grows with depth because an elliptical hole collects charge and polymer asymmetrically, and its two axes have different aspect ratios and therefore different ARDE. The narrow axis lags and the hole becomes more elliptical as it deepens. Bottom ellipticity reduces the contact area and adds to the placement error along the long axis.

### 13.4.2 Hexagonal Distortion

On a tight honeycomb, the oxide around each hole is not uniform. It is thinnest toward each of the six neighbours and thickest toward the six triple points between them.

```
Wall toward a neighbour:            p − CD = 37 − 26 = 11 nm (5.5 nm per hole)
Oxide toward a triple point:        p/√3 − CD/2 = 21.4 − 13 = 8.4 nm per hole
  (shared among three holes; the triple-point oxide volume is larger)
```

During the etch, heat, charge, and the local supply of oxygen released from the walls differ between the two directions. Lateral etch is slightly faster toward the triple points, where there is more oxide to release oxygen and burn polymer, and slower toward neighbours, where the thin wall shares its supply between two holes. The holes become slightly hexagonal, with their flats facing the neighbours. This is benign as long as the flats do not thin the wall further. At the bow, however, a hexagonal hole of the same area as a round one has its flats closer to the neighbour by about 0.5 nm.

### 13.4.3 Distortion at the Array Edge

The outermost holes of the array have fewer neighbours, a richer neutral supply, and different charging. They are larger, more tilted toward the array interior, and more distorted. Dummy rows of holes (two to four rows) at the array edge absorb these effects so that the active cells see the interior environment.

---

## 13.5 Stochastic Patterning Defects

### 13.5.1 The Defect Types

```
Defect (at the mask)                Rate (illustrative,     Etch consequence
                                    per hole, EUV)
──────────────────────────────────────────────────────────────────────────────────
Missing opening (closed)            10⁻¹¹ – 10⁻¹⁰           Not-open
Partially open (micro-bridge or     10⁻⁸ – 10⁻⁷             Narrow hole → late
scum at the bottom of the resist)                           arrival or small
                                                            bottom CD (Ch. 12)
Oversized opening                   10⁻⁸ – 10⁻⁷             Large bow → wall
                                                            thinning, bridging
Merged openings                     10⁻¹¹ – 10⁻¹⁰           Bridged pair
Displaced opening                   10⁻⁹                    Placement tail
Elliptical opening (e > 0.1)        10⁻⁷ – 10⁻⁶             High twist (Ch. 11)
```

### 13.5.2 Amplification by the Etch

```
Etch amplification factors at 91:1 (R1):

  Mask property                    Etch output                      Factor
  ─────────────────────────────────────────────────────────────────────────
  CD deficit (nm)                  Depth lag at fixed time (nm)     27
                                   Arrival delay (s)                ≈ 5
                                   Bottom CD (nm)                   1.2
  CD excess (nm)                   Bow CD (nm)                      ≈ 1.1
  Ellipticity                      Bottom ellipticity               2–3
                                   Twist variance (D_θ)             ∝ e²
  Opening displacement (nm)        Bottom displacement (nm)         1.0
                                   (plus any tilt it seeds)

  At 57:1 (Book #29): depth lag factor 15; bow and twist factors smaller
```

### 13.5.3 The Lithography–Etch Trade

The stochastic defect rates fall steeply with exposure dose. A higher dose costs scanner throughput, which is expensive. The capacitor etch's amplification decides how much dose is needed:

```
Illustrative: partially-open rate P_po falls ≈ 10× for each +20% dose

  Required: late-arrival not-opens ≤ 0.5 per die (Chapter 12)
  With overetch 40 s (edge Δw coverage 4.2 nm): needs the tail model
    of Chapter 12 → P_po(at Δw > 4.2) ≤ 2×10⁻¹¹
  With overetch 50 s (coverage 5.5 nm): tolerates ≈ 40× more → saves ≈ 30%
    of dose
```

An overetch that is 10 s longer can save nearly a third of the exposure dose for the capacitor layer. Conversely, an etch that covers less CD deficit (taller mold, higher k) forces more dose. **Every gain in etch tolerance is a gain in lithography throughput**, and the two must be optimized together.

### 13.5.4 Self-Aligned Patterning

Double self-aligned double patterning (SADP×2) produces the honeycomb from line patterns and does not have EUV's stochastic missing-hole failures. It has its own tails: pitch walking between families, which appears as a CD offset between hole families, and line-edge roughness. The capacitor etch sees a family offset of about 1 nm as a 27 nm depth lag in one family, which is systematic and must be covered by the overetch for the whole family, not just its tail.

---

## Summary and Key Takeaways

1. **The facet is the clock.** The facet foot descends at about 2.7 nm/s and reaches the 150 nm limit about 128 s after the R1 etch ends.

2. **The facet shapes the bow.** As it descends, the top CD grows and the bow grows by about 0.3 nm per 100 nm of facet descent late in the etch.

3. **Striation comes from the mask.** Low-order lobes grow into ellipticity and twist; high-order lobes are smoothed.

4. **Holes become hexagonal.** On a tight honeycomb, lateral etch is faster toward the triple points; the flats face the neighbours.

5. **The etch amplifies mask defects.** A nanometre of CD deficit becomes 27 nm of depth lag and 5 s of delay; ellipticity becomes twist.

6. **Etch tolerance buys lithography dose.** Ten seconds of overetch can save nearly a third of the exposure dose needed to hold the not-open tail.

---

## Study Questions

1. Compute the facet margin if the B-ACL arrives 30 nm thin and its selectivity is 5% low.

2. A W-ACL mask erodes at 1.2 nm/s with a facet factor of 1.4. Compute the facet margin for the R1 recipe from a 1450 nm start.

3. For a hole with top ellipticity 0.03, estimate the bottom ellipticity and the increase in its twist variance relative to a hole with e = 0.02.

4. Show that the oxide from a hole edge to the triple point on a 37 nm hexagonal lattice with 26 nm holes is 8.4 nm. What is it at the bow (27.5 nm)?

5. A scanner dose increase of 20% reduces the partially-open rate tenfold and costs 12% of scanner throughput on this layer. Compare its value with a 10 s overetch extension that costs 2.2% of etch chamber throughput.

---

**Next Chapter:** [Chapter 14: Beyond a Single Pass — Two-Tier Molds, Cyclic Etch, 4F² & 3D DRAM](./14-two-tier-4f2-3d-dram.md)

---

**Chapter 13 Development Status:** Complete  
**Version:** 1.0
