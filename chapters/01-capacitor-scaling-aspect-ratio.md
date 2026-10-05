# Chapter 1: Why DRAM Capacitors Keep Getting Taller

## Overview

Book #29 began with the cell and its charge and ended with a 1.6 µm capacitor hole at 57:1. This chapter starts from the same cell but asks a different question: **what happens to that hole as the array shrinks?** The answer is that the hole gets taller and narrower every generation, because the charge it must hold barely changes, the dielectric has stopped getting thinner, and the footprint keeps falling. The aspect ratio rises by about a quarter per generation. At the 1d generation of this book it is 91:1.

The chapter builds the scaling law, applies it to the 1d-class reference array, computes the capacitance and its sensitivities, constructs the placement budget at the bottom of a 2.1 µm hole, and ends with the specification sheet that the rest of the book works to.

**Learning Objectives:**
- Compute the sense signal and the minimum cell capacitance at the 1d generation
- Explain why EOT has stalled near 0.5 nm and what that means for the capacitor
- Derive the scaling of height and aspect ratio with cell area at fixed capacitance
- Compute pitch, wall, and open fraction for the 37 nm honeycomb
- Compute cell capacitance and its sensitivity to depth, CD, and EOT
- Build the bottom-placement budget and identify its largest term
- Read the extreme-aspect-ratio specification sheet

---

## 1.1 The Charge Target

### 1.1.1 The Sense Signal

The read operation is unchanged from Book #29. The bit line is precharged to half the array voltage, the word line opens the access transistor, and the cell shares its charge with the bit line:

```
ΔV_BL = (V_DD/2) · C_s / (C_s + C_BL)

Reference values at 1d (illustrative):
  V_DD (array) = 1.0 V, plate at 0.50 V, C_BL = 35 fF

  C_s (fF)    ΔV_BL (mV)
     7           83
     8           93
     9          102
     9.7        108   ← reference (Section 1.4)
    10.5        115   (full sidewall, no support loss)
    12          128

  Sense requirement (offset + noise + retention loss margin):
  ΔV_BL ≥ 95 mV at time zero  →  C_s ≥ 8.2 fF
```

Each generation trims the array voltage and shortens the bit line. The two roughly cancel. The minimum capacitance has stayed between 8 and 10 fF for twenty years, and at 1d it is about 8.2 fF with a design target near 9.5 fF to leave room for the distribution.

### 1.1.2 Retention and the Dielectric Leakage Floor

The cell must keep enough of its charge between refreshes:

```
Refresh interval at high temperature: 32 ms
Allowed signal loss: ΔV ≈ 0.20 V on the storage node
Allowed charge loss: ΔQ = 9.7 fF × 0.20 V = 1.94 fC
Total leakage allowed: 1.94 fC / 32 ms = 61 fA per cell

Junction and GIDL leakage (Books #26–27) take most of this budget.
Dielectric share (illustrative): ≤ 1 fA per cell

Capacitor area: π × 23 nm × 1940 nm = 1.40×10⁵ nm² = 1.40×10⁻⁹ cm²
Dielectric leakage limit: 1×10⁻¹⁵ A / 1.40×10⁻⁹ cm² ≈ 7×10⁻⁷ A/cm²
at ±0.5 V and 85 °C
```

Tunnelling leakage through a ZrO₂-based stack rises about a decade for every 0.05–0.08 nm of EOT removed below 0.5 nm. Higher-k phases (tetragonal ZrO₂, HfO₂/ZrO₂ laminates, TiO₂- and SrTiO₃-based films) have smaller band offsets, so the gain in permittivity is largely spent on leakage. **The EOT has therefore stalled near 0.5 nm since the 1b generation.** Every further shrink must be paid for in area, and area means height.

---

## 1.2 The Scaling Law

### 1.2.1 Capacitance of a Pillar

```
Single-sided pillar (Book #29, Section 1.3):
  C_s = ε₀ · 3.9 · π · CD_avg · H_eff / EOT

  CD_avg: average hole diameter (the pillar outer diameter)
  H_eff:  height exposed to the dielectric (mold height minus the
          supports and the bottom stop)
```

### 1.2.2 Holding C Constant as the Cell Shrinks

The cell area falls by a factor s per generation (s ≈ 0.80). The hole pitch, and therefore every lateral dimension of the hole, scales as √s:

```
CD ∝ p ∝ √(A_cell) → CD scales by √s ≈ 0.894 per generation

At fixed C_s and fixed EOT:
  CD × H = constant → H scales by 1/√s ≈ 1.118 per generation
  Aspect ratio A = H / CD scales by 1/s ≈ 1.25 per generation

If the target C_s rises slightly (lower V_DD) or the support loss grows,
H must rise faster: about 1.14–1.16 per generation in practice.
```

Height grows by about 15% per generation and the aspect ratio by about 25%. The aspect ratio grows **inversely with the cell area**, not with its square root.

### 1.2.3 The Roadmap

```
Illustrative capacitor roadmap (6F² cell, one hole per cell):

  Gen   F (nm)  p (nm)  CD_avg  H (µm)  A (H/CD)  EOT (nm)  Structure   C_s (fF)
  ──────────────────────────────────────────────────────────────────────────────
  1x     19      50      33      1.20      36      0.75     cylinder     ≈ 9*
  1z     18      47      31      1.35      44      0.62     cyl./pillar  ≈ 9*
  1b     17      45      28      1.60      57      0.50     pillar       8.6–8.9
  1c     15.5    41      25.5    1.85      73      0.50     pillar       9.3
  1d     14      37      23      2.10      91      0.50     pillar       9.7  ← this book
  1e     13      34      21      2.35     112      0.48     pillar/2-tier 10.4 (proj.)

  * Double-sided cylinders; the inner surface adds area that a pillar
    does not have. C_s for pillars from Section 1.2.1 with H_eff = H − 160 nm
    (1b: Book #29 values).
```

The aspect ratio rose by about 7 per generation in the cylinder era, when EOT was still falling. Once EOT stalled and the cylinder gave way to the pillar, the aspect ratio began rising by 16–20 per generation. **Every generation now adds about a 1b-class etch's worth of difficulty on top of the last.**

### 1.2.4 When Does It Stop?

Three things end the climb:

1. **The etch.** Chapter 4 derives the maximum depth a given chemistry can reach before its mask runs out. For the R1 fluorocarbon chemistry and the reference mask it lies between A ≈ 110 (where the mask facet reaches the mold) and A ≈ 130 (where the flat mask reaches its 500 nm minimum) for a 23 nm hole; for R2 cryogenic etch it lies between about 140 and 170. Placement (Chapter 11) bites earlier.
2. **The pillar.** After mold removal, the electrode stands as a free tube. Chapter 2 shows that pillar bending and capillary forces set a limit near A ≈ 100–120 even with three supports.
3. **The architecture.** 4F² vertical-channel cells (Chapter 14) gain 33% in area per bit at the same F, and 3D DRAM moves the capacitor sideways. Both reset the capacitor roadmap.

---

## 1.3 The 1d-Class Honeycomb

### 1.3.1 Layout

```
Hexagonal lattice, one hole per cell:
  area per site   = (√3/2) p² = 0.866 × 37² = 1186 nm²  (6F² = 1176 nm²)
  row spacing     = (√3/2) p = 32.0 nm
  triple point    = p / √3 = 21.4 nm from each of three holes

       ○   ○   ○   ○          ○ = storage-node hole, 26 nm at the top
     ○   ○   ○   ○            centre-to-centre 37 nm
       ○   ○   ○   ○          wall on the line of centres: 37 − 26 = 11 nm
```

### 1.3.2 Wall and Open Fraction

```
  CD (nm)   Wall p − CD (nm)   Open fraction (π/4)CD²/(0.866 p²)
  ──────────────────────────────────────────────────────────────
   19             18                   0.24     (bottom)
   23             14                   0.35     (average)
   26             11                   0.45     (top)
   28              9                   0.52     (bow limit)
   30              7                   0.60     (bridging risk)
```

At the top of the mold 45% of the array area is hole. The wall is 11 nm, less than half the hole diameter. The bow limit of 28 nm leaves 9 nm, the minimum the support nitride and the mold oxide need to survive the electrode deposition and mold removal without cracks (Chapter 10).

### 1.3.3 Comparison with Book #29

```
                         1b (Book #29)     1d (this book)    Ratio
  ─────────────────────────────────────────────────────────────────
  Pitch p                  45 nm             37 nm            0.82
  Top CD                   32 nm             26 nm            0.81
  Average CD               28 nm             23 nm            0.82
  Bottom CD                24 nm             19 nm            0.79
  Wall at top              13 nm             11 nm            0.85
  Mold height H            1.60 µm           2.10 µm          1.31
  Aspect ratio (avg)       57                91               1.60
  Landing pad width        26 nm             21 nm            0.81
  Holes per die            1.7×10¹⁰ (16 Gb)  2.6×10¹⁰ (24 Gb)  1.5
```

Every lateral dimension shrinks by about 18%. The height grows by 31%. The aspect ratio grows by 60%.

---

## 1.4 Capacitance and Its Sensitivities

### 1.4.1 The Reference Cell

```
ε₀ · 3.9 = 8.854×10⁻¹² × 3.9 = 3.453×10⁻¹¹ F/m

Full sidewall (H = 2100 nm):
  C = 3.453×10⁻¹¹ × π × 23×10⁻⁹ × 2.10×10⁻⁶ / 0.50×10⁻⁹
    = 3.453×10⁻¹¹ × 1.517×10⁻¹³ / 5.0×10⁻¹⁰
    = 1.048×10⁻¹⁴ F = 10.5 fF

After the supports and bottom stop (H_eff = 2100 − 100 − 40 − 20 = 1940 nm):
  C_s = 10.5 × 1940 / 2100 = 9.7 fF
```

### 1.4.2 Sensitivities

```
∂C_s/∂H_eff  = C_s / H_eff  = 9.7 / 1940 = 0.50 fF per 100 nm of depth
∂C_s/∂CD_avg = C_s / CD_avg = 9.7 / 23   = 0.42 fF per nm of average CD
∂C_s/∂EOT    = −C_s / EOT   = −9.7 / 0.50 = −0.19 fF per 0.01 nm of EOT
```

Relative to Book #29, a nanometre of CD is now worth 4.3% of the capacitance (3.5% at 1b), and 100 nm of depth 5.2% (6.7% at 1b). **Diameter has become more valuable and depth less**, which is why the bow and the bottom CD, both diameter terms, carry more weight at 1d.

### 1.4.3 The Profile, Not the Top CD

The average CD that sets C_s is the area-weighted mean over the profile:

```
CD_avg = (1/H) ∫ CD(z) dz

Reference profile (Chapter 10): top 26, neck 25 at 120 nm, bow 27.5 at
450 nm, then a linear taper to 19 at the bottom.
  Approximate average by segments:
    0–120 nm     25.5 nm   ×  120
    120–450 nm   26.3 nm   ×  330
    450–2100 nm  23.3 nm   × 1650
  CD_avg = (3060 + 8679 + 38445) / 2100 = 23.9 nm

The reference 23 nm uses the post-clean, post-electrode CD (the TiN
consumes ≈ 0.9 nm of radius-equivalent area through interface loss and
roughness); the etch must deliver ≈ 23.9 nm.
```

The bottom taper costs more than the bow gains. A hole whose bottom 600 nm tapers by an extra 2 nm loses about 0.25 fF.

---

## 1.5 The Bottom-Placement Budget

### 1.5.1 Contact Geometry

The hole must land on the W pad with enough overlap to give a low-resistance contact, and must not approach the neighbouring pad.

```
Pad width at its top: 21 nm; bottom CD: 19 nm (minimum 16 nm)
Overlap width along the displacement direction:
  overlap = (pad + CD_bot)/2 − |Δ| = (21 + 19)/2 − |Δ| = 20 − |Δ|

Required overlap for contact resistance: ≥ 13 nm  →  |Δ| ≤ 7 nm
Clearance to the neighbouring pad (centre at 37 nm):
  37 − 10.5 − 9.5 − |Δ| = 17 − |Δ|  → 10 nm at |Δ| = 7 (no short risk)
```

### 1.5.2 Contributions

```
Bottom-placement budget (3σ, illustrative):

  Term                                       3σ (nm)    Squared
  ───────────────────────────────────────────────────────────────
  Lithographic overlay, hole to pad           3.0        9.0
  Mask-open shift and mask tilt               1.5        2.3
  Edge tilt residual after ring control       3.7       13.7   (0.10° × 2.1 µm)
  Twist at the bottom (Chapter 11)            4.5       20.3
  ───────────────────────────────────────────────────────────────
  RSS                                         6.7       45.3   ≤ 7.0 ✓
```

The budget closes with 0.3 nm to spare. At Book #29's 1.6 µm depth, the same angular errors cost 2.8 nm (tilt) and about 3.2 nm (twist), and the budget had several nanometres of margin. **At 2.1 µm, the etch contributes three-quarters of the placement variance**, and the lithography that the fab spends heavily to control contributes a fifth.

### 1.5.3 Angle Is Distance

```
Lateral displacement at the bottom for an angle θ held over the full depth:
  Δ = H tan θ

  θ        H = 1.6 µm    H = 2.1 µm    H = 2.6 µm
  ─────────────────────────────────────────────────
  0.05°      1.4 nm        1.8 nm        2.3 nm
  0.10°      2.8 nm        3.7 nm        4.5 nm
  0.20°      5.6 nm        7.3 nm        9.1 nm
  0.50°     14.0 nm       18.3 nm       22.7 nm
```

A fifth of a degree held over the depth consumes the whole budget. Chapter 11 shows how the edge ring holds the wafer-edge tilt to 0.1° and why twist grows faster than linearly with depth.

---

## 1.6 Where the Etch Sits and What It Must Deliver

### 1.6.1 The Module

```
Landing pad (W) and pad isolation
  → Bottom SiN stop (20 nm), lower BPSG (1140), middle SiN (40),
    upper TEOS (800), top SiN (100)           [mold, Chapter 2]
  → B-doped carbon 1.50 µm + SiON 40 nm      [mask, Chapter 2]
  → Honeycomb patterning (EUV single exposure or SADP×2) and mask open
  → CAPACITOR HAR ETCH                        [this book]
  → Strip, clean
  → TiN bottom electrode (ALD), fill
  → Top support open, mold removal (HF wet), middle support open
  → High-k dielectric (ALD), TiN/SiGe plate
```

### 1.6.2 The Specification Sheet

```
DRAM HIGH-ASPECT-RATIO CAPACITOR ETCH — REFERENCE SPECIFICATION (1d-class)

Geometry
  Top CD (at top of mold)               26.0 ± 1.0 nm (3σ, within wafer)
  Bow CD (maximum, any depth)           ≤ 28.0 nm on every site mean;
                                         wall ≥ 9 nm
  Bottom CD (at pad)                    19.0 ± 1.5 nm; ≥ 16 nm on every hole
  Average CD (from profile)             23.9 ± 0.6 nm as etched
  Depth                                 all holes through the bottom stop

Placement
  Bottom placement |Δ|                  ≤ 7 nm (3σ RSS of all terms)
  Edge tilt                             ≤ 0.10° at 147 mm radius
  Twist (bottom displacement)           3σ ≤ 4.5 nm in the array interior

Defects
  Not-open holes                        ≤ 2×10⁻¹⁰ per hole (≈ 5 per die)
  Bridged pairs                         ≤ 1×10⁻¹⁰ per pair
  Pad gouge                             ≤ 8 nm into W

Mask and integration
  Remaining B-ACL after etch            ≥ 500 nm everywhere
  Support layer damage                  no notch > 2 nm at SiN interfaces
  Residue after strip and clean         none detectable by VC or EDX

Capacitance (electrical monitor)
  C_s                                   9.7 ± 0.4 fF; ≥ 8.2 fF on every cell
```

The not-open specification is tighter than Book #29's in rate because the die has 50% more holes and the repair capacity has not grown. Chapter 12 derives it.

---

## Summary and Key Takeaways

1. **The charge target is fixed.** About 9.7 fF at 1d gives 108 mV of signal; the minimum is about 8.2 fF.

2. **EOT has stalled.** The dielectric leakage budget of about 1 fA per cell holds the EOT near 0.5 nm.

3. **The aspect ratio scales as 1/A_cell.** At fixed C_s and EOT, height grows about 12–15% and the aspect ratio about 25% per generation.

4. **The reference hole is 91:1.** 2.1 µm deep, 23 nm average CD, on a 37 nm pitch with an 11 nm wall at the top.

5. **Diameter has become more valuable.** Each nanometre of average CD is 0.42 fF (4.3% of C_s); each 100 nm of depth is 0.50 fF.

6. **The etch owns the placement budget.** Tilt and twist contribute three-quarters of a 7 nm budget; a 0.2° error held over the depth uses all of it.

---

## Study Questions

1. The array voltage falls to 0.9 V at the 1e generation and C_BL to 32 fF. With the same 95 mV requirement, what is the minimum C_s?

2. Starting from the 1d reference, the cell area shrinks by 20% at fixed EOT and fixed C_s. Compute the new pitch, average CD, mold height, and aspect ratio. Compare with the 1e row of the roadmap.

3. A new dielectric reaches EOT 0.45 nm with acceptable leakage. How much can the mold be lowered at the same C_s? What aspect ratio results?

4. For the reference profile, compute CD_avg if the bottom taper is replaced by a straight wall at 24 nm from 450 nm to the bottom. How much capacitance does that gain?

5. Rebuild the placement budget for a 2.4 µm mold, keeping all angular errors constant and scaling the twist term as (h − 690 nm)^1.5. Does it close? Which term would you attack first?

6. On a 37 nm pitch, what bow CD reduces the wall to 7 nm? If bow scales linearly with mold height at fixed recipe, at what height does the reference recipe reach it, starting from 27.5 nm at 2.1 µm?

---

**Next Chapter:** [Chapter 2: The Extreme-Aspect-Ratio Mold, Pillar Mechanics & Hard-Mask Budget](./02-mold-pillar-mechanics-mask-budget.md)

---

**Chapter 1 Development Status:** Complete  
**Version:** 1.0
