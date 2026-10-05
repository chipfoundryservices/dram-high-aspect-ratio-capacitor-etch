# Chapter 2: The Extreme-Aspect-Ratio Mold, Pillar Mechanics & Hard-Mask Budget

## Overview

The capacitor etch inherits three things it cannot change: the mold it must cut, the mask it must cut through, and the pillar that will later stand in the hole. At 57:1 each was a constraint. At 91:1 each is a limit. The mold is 2.1 µm of oxide and nitride whose thickness variation alone moves the required etch time by several seconds. The pillar that fills the hole will stand 2.1 µm tall on a 23 nm base after the mold is removed, and its stiffness falls as the fourth power of its aspect ratio. The mask must survive about 2.1 µm of dielectric removal at ion energies that sputter carbon faster than ever.

This chapter describes the mold and why it is built as it is, derives the mechanics that make the supports essential, sets out the mask budget for undoped, boron-doped, and metal-containing carbon, and closes with stress, wafer bow, and incoming variation.

**Learning Objectives:**
- Describe the 2.1 µm mold and the role of each layer
- Compute the bending stiffness of a TiN pillar and its scaling with aspect ratio
- Estimate pillar deflection under a lateral load for different support schemes
- Compute the mask budget for undoped, boron-doped, and metal-containing carbon
- Explain why the mask, not the mold, often sets the etch end point
- Estimate wafer bow from the mask stress and its effect on the etch

---

## 2.1 The Mold

### 2.1.1 Layers

```
Reference mold, top to bottom (2100 nm):

  Layer                Thickness   Role
  ──────────────────────────────────────────────────────────────────────
  Top SiN support         100 nm   Holds pillar tops in a lattice after
                                    mold removal; thickest support because
                                    it carries the largest bending moment
  Upper oxide (TEOS)      800 nm   Mold; dense, slow in HF; stable profile
  Middle SiN support       40 nm   Halves the free span of the pillar
  Lower oxide (BPSG)     1140 nm   Mold; boron/phosphorus doping makes it
                                    etch ≈ 17% faster in plasma and several
                                    times faster in HF for mold removal
  Bottom SiN stop          20 nm   Etch stop above the W pads; protects
                                    the pad isolation during mold removal
```

The mold differs from Book #29 in three ways. The lower oxide is 50% thicker, because the extra height is added where the hole is already narrowest and the etch is already slowest. The top support is thinner (100 nm against 120 nm), because its etch costs depth-time at the top where the hole is still fast but costs mask throughout. The middle support has moved up relative to the mold, which shortens the upper span and lengthens the lower span, for reasons explained in Section 2.2.4.

### 2.1.2 Why the Lower Oxide Is Doped

Doping the lower oxide does three things at once:

1. **Plasma rate.** BPSG with about 4 wt% B and 4 wt% P etches about 17% faster than TEOS in the fluorocarbon plasma. The extra rate is spent at the bottom, where ARDE has already cut the rate to under half.
2. **Wet removal.** BPSG etches several times faster than TEOS in dilute HF, so the lower mold clears in about the same time as the upper mold, and the top support is not attacked from below for long.
3. **Reflow.** Doped glass relaxes at anneal temperatures, which lowers its stress and reduces wafer bow.

The price is a gradient. The dopant concentration varies through the film and across the wafer, and the plasma rate varies with it by roughly 2% per wt%. Chapter 15 feeds the measured composition forward.

### 2.1.3 Thickness Variation and Etch Time

```
Mold thickness variation (3σ, wafer-to-wafer and within-wafer):
  TEOS 800 ± 12 nm, BPSG 1140 ± 20 nm, supports ± 3 nm
  Total ≈ 2100 ± 24 nm (RSS)

Time to reach the stop at the bottom (R1 bottom rate in BPSG, Chapter 8):
  ER_bottom ≈ 335 nm/min
  Δt = 24 nm / 335 nm/min = 4.3 s per 3σ of mold
```

A 3σ-thick mold costs 4.3 s, about 11% of the overetch. Unlike Book #29, where mold variation was a small term, at 91:1 the bottom rate is so low that every nanometre of mold costs 0.18 s.

---

## 2.2 Pillar Mechanics

### 2.2.1 The Pillar After Mold Removal

The hole is filled with an ALD TiN electrode. The mold oxide is then removed in HF, leaving a field of TiN pillars 2.1 µm tall, 23 nm in average diameter, held at the bottom by the pad and laterally by the two nitride supports. The dielectric and plate are deposited around them. Between mold removal and dielectric deposition, the pillars are free in a liquid and then in air.

### 2.2.2 Bending Stiffness

```
Solid TiN pillar, diameter d, Young's modulus E (ALD TiN, illustrative):
  E ≈ 300 GPa
  Second moment of area: I = π d⁴ / 64

  d = 23 nm: I = π × (23×10⁻⁹)⁴ / 64 = 1.37×10⁻³² m⁴
  Flexural rigidity: EI = 300×10⁹ × 1.37×10⁻³² = 4.12×10⁻²¹ N·m²
```

### 2.2.3 Deflection Under a Lateral Load

During drying, a meniscus that is not symmetric around a pillar pulls it sideways. Uneven electrostatic charge and the stress in the dielectric do the same later. Represent all of these by a uniform effective lateral load q per unit length.

```
Uniform load q on a span L:
  Cantilever (free top):            δ = q L⁴ / (8 EI)
  Clamped at both ends (supported): δ = q L⁴ / (384 EI)   (at mid-span)

Illustrative effective load after IPA drying: q = 2×10⁻³ N/m

  Scheme                               Span L    δ (nm)
  ──────────────────────────────────────────────────────────
  No supports (free cantilever)        2000 nm    970
  Top support only (clamped–clamped)   2000 nm     20
  Top + middle: lower span             1140 nm     2.1
  Top + middle: upper span              800 nm     0.5
  Top + middle at mid-height (equal)  ≈1000 nm     1.3

  Collapse criterion: δ ≥ gap/2, gap = p − CD = 37 − 23 = 14 nm → 7 nm
```

Without supports, a pillar of this aspect ratio collapses on its neighbour under any realistic drying load. With the top support alone, the mid-span deflection is three times the collapse limit. With the middle support, the larger span deflects 2.1 nm and the array is stable with a margin of about 3×.

### 2.2.4 Scaling and the Choice of Support Height

Deflection scales as L⁴/d⁴, which is the fourth power of the span's aspect ratio. Going from Book #29's pillar (A = 57) to this one (A = 91) at the same support scheme makes each span (91/57)⁴ = 6.5 times more compliant.

```
Equal spans minimize the larger deflection: middle support at mid-height.
But a support at mid-height (≈ 1050 nm depth) must be etched where the
hole is already at A ≈ 46 and the bottom rate is 0.58 ER₀.
At 900–940 nm depth (A ≈ 40) the support costs less etch time and less
CD loss; the lower span grows to 1140 nm and its deflection to 2.1 nm,
still with margin.

The reference places the middle support at 900 nm for the etch's sake,
accepting the mechanical penalty.
```

At 1e (2.35 µm), the lower span grows to about 1380 nm and its deflection to 4.5 nm, two-thirds of the collapse limit. Most 1e designs add a third support or move to two-tier molds (Chapter 14), each of which costs etch time or alignment.

### 2.2.5 Etch Errors Become Mechanical Errors

A hole that twists or tilts produces a pillar that is not straight. Its closest approach to the neighbour moves away from the lattice gap:

```
Two neighbours twisting toward each other by 2.25 nm each (1.5σ) at the
bottom, plus a bow difference of 1 nm, leave a gap of
  14 − 2 × 2.25 − 1 = 8.5 nm  instead of 14 nm in the lower span.
The collapse margin (gap/2 vs δ) falls from 7/2.1 = 3.3× to 4.25/2.1 = 2.0×.
```

Placement and profile errors from the etch are therefore not only contact problems at the bottom. They are mechanical problems all along the pillar. Chapter 16 returns to leaning and capillary collapse as yield signatures.

---

## 2.3 The Hard Mask

### 2.3.1 Why Undoped Carbon Runs Out

Book #29 used 1.40 µm of undoped amorphous carbon (ACL) with a blanket selectivity to oxide of 5.5 and an effective selectivity of 2.6 once facets, early erosion, and the overetch were counted. At R1's higher ion energy, carbon sputters faster:

```
Carbon physical sputtering by Ar⁺ grows roughly as √E above threshold.
  ⟨E_i⟩: 3.0 keV (Book #29) → 4.5 keV (R1): √1.5 = 1.22
  Oxide yield grows by the same factor, so the blanket ratio barely moves,
  but facet erosion, which is purely physical, grows faster.

Effective selectivity of undoped ACL in R1 (illustrative): 2.3
  Mask consumed: 2100 / 2.3 = 913 nm
  For ≥ 500 nm remaining: ≥ 1413 nm after mask open → ≈ 1.5 µm deposited,
  with no margin for mold variation, overetch extension, or facet growth
  For the same margin as Book #29 (≈ 230 nm above minimum): ≈ 1.8 µm
```

An 1.8 µm undoped mask has two problems. The mask-open etch must itself cut a 26 nm hole through 1.8 µm of carbon, a 69:1 etch before the capacitor etch begins. And the hole starts deeper: after the mask open, about 1750 nm of carbon stands over a 26 nm opening, a 67:1 tube before the mold is reached, against 56:1 for the reference mask (Section 2.3.4).

### 2.3.2 Doped and Metal-Containing Carbon

```
Hard-mask options (illustrative, R1 conditions):

  Mask material                Blanket    Effective   Consumed for   Notes
                               sel.       sel.        2100 nm
  ────────────────────────────────────────────────────────────────────────────
  Undoped ACL (PECVD)            5.5        2.3          913 nm      baseline
  Boron-doped carbon (B-ACL)     8          3.5          600 nm      reference;
   (≈ 30–50 at% B)                                                   harder open
  Tungsten-doped carbon          11         4.8          438 nm      metal
   (W-ACL, ≈ 10 at% W)                                               contamination,
                                                                     strip harder
  Metal-oxide stacks             15–20      6–8          ≈ 300 nm    stress, open
   (e.g., WOₓ, ZrOₓ-based)                                           chemistry

R2 (cryogenic HF): carbon reacts slowly with HF at −60 °C;
  B-ACL effective selectivity ≈ 5 → ≈ 420 nm consumed
```

Boron forms B–C bonds that are harder to break physically and B–F products that are less volatile than CO at the mask surface. Tungsten adds a heavier, harder phase, but leaves W residues that must be stripped without damaging the TiN or the pad, and it must be kept out of the DRAM front end. The reference uses B-ACL as the compromise.

### 2.3.3 The Mask Budget

```
Reference mask budget (R1):
  B-ACL deposited                      1500 nm
  Lost in mask open (SiON clear, ACL
  top rounding)                          −50 nm
  At the start of the HAR etch          1450 nm
  Consumed by the HAR etch (sel. 3.5)   −600 nm
  Remaining (mean)                       850 nm
  Specification                         ≥ 500 nm
  Margin                                 350 nm

Margin in etch time at the mask erosion rate:
  Mask erosion rate ≈ 600 nm / 359 s = 1.67 nm/s
  350 nm / 1.67 nm/s = 210 s of extra etch time

But the facet, not the flat thickness, reaches the hole first (Chapter 13):
  facet depth grows ≈ 1.6× faster than the flat mask erodes
  usable margin before the facet reaches the top support ≈ 120 s
```

The margin looks generous in thickness but is about 120 s once the facet is counted, against a total etch of 359 s. **Any change that adds a third to the etch time, such as a mold 15% taller at fixed chemistry, consumes the whole margin.** This is why the mask, not the mold, is the clock of extreme-aspect-ratio etch.

### 2.3.4 Total Aspect Ratio Including the Mask

```
At the start of the etch:  mask 1450 nm over a 26 nm opening → 56:1 already
At the end of the main etch: (850 + 2100) / 23 = 128:1 (average CD)
```

Ions and neutrals see the whole tube, mask included. The transport models of Chapters 3 and 4 use the total height h_tot = h_mask + h for this reason.

---

## 2.4 Stress, Bow, and Incoming Variation

### 2.4.1 Wafer Bow from the Mask

```
Stoney's equation for a thin film on a thick substrate:
  κ = 6 σ_f t_f / (M_s t_s²),  M_s = E/(1 − ν) ≈ 180 GPa for Si(100)
  Bow b = κ r² / 2

B-ACL: σ_f ≈ −250 MPa (compressive), t_f = 1.5 µm; t_s = 775 µm
  κ = 6 × 250×10⁶ × 1.5×10⁻⁶ / (180×10⁹ × 6.01×10⁻⁷) = 0.0208 m⁻¹
  b at r = 150 mm: 0.0208 × 0.0225 / 2 = 234 µm
```

A bow of 234 µm is too large for reliable electrostatic clamping and for uniform helium cooling at the edge. Mold films add their own stress: TEOS is mildly compressive, BPSG near neutral after reflow, SiN supports tensile or compressive by recipe. A backside film, or a stress-tuned mask stack, brings the incoming bow below about 100 µm.

### 2.4.2 Why Bow Matters to the Etch

1. **Chucking.** Incomplete clamping at the edge raises the helium leak, warms the edge, and grows the edge bow CD (Chapter 8).
2. **Edge tilt.** A wafer that curves at the edge presents a surface that is not parallel to the sheath. A 100 µm bow over the outer 10 mm tilts the surface by about 0.01°, small next to the ring effect but not negligible against a 0.10° budget.
3. **Lithographic overlay.** In-plane distortion from bow appears as overlay error at the hole bottom (Chapter 1's 3.0 nm term).

### 2.4.3 Incoming Variation Summary

```
Incoming quantity        Variation (3σ)     Effect on the etch
──────────────────────────────────────────────────────────────────────────
Mask-open top CD          ± 1.0 nm           ± 27 nm depth at fixed time
Mold thickness            ± 24 nm            ± 4.3 s to reach the stop
BPSG dopant content       ± 0.3 wt%          ± 0.6% lower-oxide rate
B-ACL thickness           ± 30 nm            ± 18 s of facet margin
Wafer bow                 ± 40 µm            edge temperature, tilt
Pad recess (W top)        ± 3 nm             bottom-open time and gouge
```

The mask-open CD dominates. Chapter 3 derives the 27 nm per nm sensitivity, and Chapter 15 feeds the CD forward.

---

## Summary and Key Takeaways

1. **The mold grew at the bottom.** The 2.1 µm mold adds height mostly to the doped lower oxide, where the extra plasma and wet rates are most useful.

2. **Pillar stiffness falls as A⁴.** A 91:1 pillar is 6.5 times more compliant than a 57:1 pillar for the same support scheme. Without supports it collapses; with top and middle supports the larger span deflects about 2 nm against a 7 nm limit.

3. **Support position is an etch–mechanics trade.** The middle support at 900 nm favours the etch over the mechanics.

4. **Undoped carbon runs out.** At R1's ion energy its effective selectivity falls to about 2.3, which would require about 1.8 µm of mask and a 69:1 mask open.

5. **The mask is the clock.** B-ACL at effective selectivity 3.5 leaves 850 nm, but the facet limits the time margin to about 120 s.

6. **Bow must be balanced.** 1.5 µm of compressive B-ACL bows the wafer by about 230 µm unless compensated.

---

## Study Questions

1. Compute the flexural rigidity of a pillar with average CD 21 nm (1e) and the mid-span deflection of a 1380 nm clamped span at q = 2×10⁻³ N/m. Compare with the collapse limit for a 34 nm pitch.

2. A third support of 30 nm SiN is added at 1500 nm depth. What are the three spans, and what is the largest deflection? Estimate the extra etch time to cut the support at A ≈ 65 with the R1 bottom rate and a SiN rate ratio of 0.70.

3. Using the mask table, compute the remaining mask for each material if the mold grows to 2.4 µm at the same chemistry. Which materials still meet the 500 nm specification from a 1450 nm start?

4. A W-ACL mask with effective selectivity 4.8 is chosen. If the mask may now be thinned to keep the same 350 nm margin, what thickness is needed? What is the new total aspect ratio at the end of the etch?

5. A wafer arrives with 140 µm of bow. Estimate the extra edge tilt from the surface slope over the outer 10 mm, and state which other effect of the bow you would expect to dominate.

---

**Next Chapter:** [Chapter 3: Ion Transport & Charging at Extreme Aspect Ratio](./03-ion-transport-charging-extreme-ar.md)

---

**Chapter 2 Development Status:** Complete  
**Version:** 1.0
