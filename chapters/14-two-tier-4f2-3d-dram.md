# Chapter 14: Beyond a Single Pass — Two-Tier Molds, Cyclic Etch, 4F² & 3D DRAM

## Overview

Chapters 10 to 13 showed that a single fluorocarbon pass through a 2.1 µm mold is near its limits in bow, twist, mask, and tail. At the 1e generation, about 2.35 µm deep at 21 nm, R1 fails on all four. There are three ways forward. The first is a better single pass: cryogenic chemistry (Chapter 7), with or without a mid-etch liner. The second is to stop etching the whole mold at once and build it in two tiers. The third is to change the cell so that the capacitor no longer has to grow: the 4F² vertical-channel cell and, further out, 3D DRAM.

This chapter compares these routes quantitatively at the 1e generation, then describes what each does to the capacitor etch.

**Learning Objectives:**
- Describe the etch–liner–etch sequence and what it buys
- Describe the two-tier mold process and compute its etch time, twist, and alignment budget
- Compare single-pass R1, single-pass R2, and two-tier options at 1e
- Compute the capacitor geometry for a 4F² vertical-channel cell
- Identify the vertical etches of 3D DRAM and the physics they share with this book

---

## 14.1 A Better Single Pass: Etch–Liner–Etch

### 14.1.1 The Sequence

```
1. Etch the hole to ≈ 900 nm (through the middle support), R1 steps 1–3
2. Remove the wafer; deposit a conformal liner, 1.0–1.5 nm of SiO₂ or
   SiN by ALD, on the sidewall and the bottom
3. Return; break through the liner at the bottom (short, anisotropic)
4. Continue the etch to the bottom with steps 4–6
```

### 14.1.2 What It Buys and Costs

```
Effect (illustrative, at 2.1 µm with R1):
  Bow CD (upper region protected for the rest of the etch):
    27.5 → 26.3 nm   (the bow stops growing when the liner goes on)
  Twist: unchanged (the instability is in the lower hole)
  Time: +1 chamber transfer, + ALD (≈ 3 min in a separate tool),
        + 8 s liner breakthrough
  Cost: an ALD step and a second etch-chamber visit per wafer
```

The liner stops the bow from growing after it forms (Chapter 10 showed the growth rate of about 0.22 nm/min per side). It also thins the upper wall slightly with a material that must later be removed with the mold. It does nothing for twist or for the mask, which are the 1e problems that remain.

---

## 14.2 Two-Tier Molds

### 14.2.1 The Process

```
Two-tier capacitor module (illustrative):
  1. Lower mold (≈ 1.05 µm: bottom stop, BPSG, middle support)
  2. Lower-tier mask, honeycomb patterning, lower-tier hole etch (A ≈ 46)
  3. Fill the lower holes with a sacrificial material (poly-Si or carbon);
     planarize
  4. Upper mold (≈ 1.05 µm: TEOS, top support)
  5. Upper-tier mask; pattern aligned to the lower holes; upper-tier etch
     (A ≈ 46), landing on the sacrificial plugs
  6. Remove the sacrificial fill through the upper holes
  7. Continue as a single-tier module: electrode, support open, mold
     removal, dielectric, plate
```

### 14.2.2 Etch Time and Sensitivity per Tier

```
R1 chemistry, w = 23 nm, tier depth 1050 nm:
  G(1050) = 1050 + 3.48×10⁻⁴ × 1050² = 1433 nm → 2.05 min TEOS-equivalent
  Two tiers: ≈ 4.1 min, against 5.19 min for a single 2.1 µm pass
  ∂h/∂w at 1050 nm: 9.6 nm/nm (against 27.1 at 2.1 µm)
  Bottom rate at 1050 nm: 0.58 ER₀ (against 0.41)
```

Each tier is an easy etch by the standards of this book: an aspect ratio below 50, a CD sensitivity a third of the single pass, and a bottom rate well above half.

### 14.2.3 Twist Restarts

```
R1 twist model (Chapter 11), h_on = 690 nm:
  Each tier at 1050 nm: 3σ = 8.5×10⁻⁵ × (1050 − 690)^1.5 = 0.6 nm
  Single pass at 2100 nm: 4.5 nm
```

Twist depends on the depth beyond onset to the 1.5 power. Splitting the depth in half nearly eliminates it. This is the strongest argument for two tiers.

### 14.2.4 The Tier Junction

The upper hole must land on the lower hole. The alignment budget at the junction replaces the twist budget at the pad:

```
Tier-junction budget (3σ):
  Upper-tier litho overlay to lower tier    3.0 nm
  Upper-tier tilt (edge, after pre-comp)    0.4 nm
  Upper-tier twist                          0.6 nm
  Lower-tier top shift (planarization)      1.0 nm
  RSS                                        3.3 nm

Upper bottom CD ≈ 21 nm landing on a lower top CD ≈ 26 nm:
  overlap = (21 + 26)/2 − |Δ| = 23.5 − |Δ| → at |Δ| = 3.3 nm, 20 nm
```

The junction leaves a step in the hole wall, a "waist" or kink where the upper bottom (21 nm) meets the lower top (26 nm). The kink costs capacitance and concentrates stress in the pillar at mid-height.

```
Capacitance cost of the waist (illustrative):
  Upper tier tapers 26 → 21 nm and lower tier 26 → 19 nm, against
  26 → 19 nm over 2.1 µm for the single pass:
  CD_avg two-tier ≈ (23.5 × 1050 + 22.5 × 1050) / 2100 = 23.0 nm
  CD_avg single pass (as etched) ≈ 23.9 nm (Chapter 1, with the bow)
  → ΔC ≈ −0.9 nm × 0.42 fF/nm ≈ −0.4 fF
  Recovered by printing the upper tier ≈ 1 nm wider at its top, which its
  shallow etch, with little bow, can afford
```

### 14.2.5 Cost

A second tier adds a mold deposition, a mask deposition, a lithography exposure, a mask open, a sacrificial fill, a planarization, and a sacrificial removal. The lithography exposure alone, on an EUV scanner, costs more than the capacitor etch. Two tiers are chosen only when a single pass cannot meet the specification.

---

## 14.3 The 1e Decision

```
1e-class capacitor (illustrative): p = 34 nm, CD_avg 21 nm, H = 2.35 µm,
  A = 112; pad 19 nm; placement limit 6 nm; wall at bow ≥ 9 nm

                           R1 single    R2 single    R1 two-tier   R2 two-tier
  ──────────────────────────────────────────────────────────────────────────────
  Etch time (min, TEOS-eq.)   6.4          3.3          4.9           2.7
  ∂h/∂w at full depth          ≈ 36         ≈ 30         ≈ 13          ≈ 10
  Mask (facet limit)          fails        meets        meets         meets
  Bow / wall                  fails        meets        meets         meets
                              (8.7 nm)     (≈ 9.4)      (≈ 9.6)       (≈ 9.8)
  Twist 3σ (nm)               6.4          4.2          1.1           0.6
  Placement RSS at pad (nm)   7.1 (fails)  5.2          3.3           3.2
  Junction alignment (nm)     —            —            3.3           3.3
  Extra lithography layers    0            0            1             1
  Verdict                     no           yes, tight   yes, costly   yes, costliest
```

R2 single pass is the cheapest route that meets the 1e specification, with little margin in placement. Two-tier processes meet it with margin, at the cost of a lithography layer. **Cryogenic single pass and two-tier fluorocarbon are the two serious 1e candidates**, and the choice depends on the cost of the extra EUV layer against the cost and risk of cryogenic chambers.

---

## 14.4 Capacitors for 4F² Vertical-Channel DRAM

### 14.4.1 The Cell

In a 4F² cell, the access transistor stands vertically: the channel is a pillar of silicon, the word line wraps around it, the bit line runs beneath it, and the storage node sits on top. Each cell occupies 2F × 2F.

```
4F² at F = 15 nm: square grid of pitch 2F = 30 nm; area 900 nm²
  (versus 6F² at F = 14: 1176 nm²; 23% smaller)

Capacitor hole on the square grid:
  CD_top ≈ 21 nm, CD_avg ≈ 18 nm
  Wall on the axes:     30 − 21 = 9 nm
  Wall on the diagonal: 30√2 − 21 = 21.4 nm
```

### 14.4.2 How Tall?

The bit line beneath the vertical transistor is shorter and less loaded, so the 4F² cell needs less capacitance:

```
Target C_s ≈ 6.5 fF (illustrative), EOT 0.50 nm, CD_avg 18 nm:
  H_eff = C_s × EOT / (ε₀ × 3.9 × π × CD_avg)
        = 6.5×10⁻¹⁵ × 0.50×10⁻⁹ / (3.453×10⁻¹¹ × π × 18×10⁻⁹)
        = 1.66 µm
  H ≈ 1.66 + 0.16 (supports, stop) ≈ 1.82 µm → A ≈ 101
```

The 4F² capacitor is shorter than the 1d capacitor but narrower, and its aspect ratio is higher. The square grid has a 9 nm wall on its axes from the start, so its bow allowance is zero at the axes and generous on the diagonals. Bow control in 4F² must be directional: the hole may grow toward the diagonals but not toward its four axial neighbours. Hexagonal distortion (Chapter 13) becomes square distortion, and it is helpful rather than harmful if the flats face the axial neighbours.

### 14.4.3 Landing

The storage node lands on the top of the vertical channel pillar rather than on a landing pad. The target is smaller and is silicon (or a silicide) rather than tungsten. The bottom-open chemistry must stop on silicon without damaging the top of the channel, and the gouge budget is a fraction of the source/drain junction depth, perhaps 3 nm.

---

## 14.5 3D DRAM

### 14.5.1 The Architecture

3D DRAM stacks horizontal 1T1C cells in layers, much as 3D NAND stacks charge-trap cells. A superlattice of Si and SiGe (or Si and oxide) layers is grown or deposited; the active silicon of each layer becomes a horizontal transistor channel; the capacitor is built sideways, in a lateral cavity recessed from a vertical opening.

### 14.5.2 The Vertical Etches

```
Vertical etch in 3D DRAM             Purpose                      Analogue
──────────────────────────────────────────────────────────────────────────────
Deep slits or trenches through the   Separate cells; access to     3D NAND slit
Si/SiGe stack (A ≈ 30–60)            each layer for lateral        (Book #24)
                                     recess
Holes for vertical word lines or     Gate access through all       3D NAND memory
bit lines (A ≈ 40–80)                layers                        hole (Book #25)
Staircase                            Contact to each layer         Staircase etch
```

The capacitor is no longer a vertical hole. It is a horizontal cylinder formed by selectively recessing SiGe (or Si) from the side of a vertical opening, then lining and filling the cavity. Its length is set by the lateral recess, not by the plasma etch depth.

### 14.5.3 What Carries Over

The vertical etches of 3D DRAM etch alternating materials rather than oxide, and their chemistry (halogen-based for Si/SiGe) differs from the fluorocarbon oxide chemistry of this book. But the physics carries over directly: the acceptance cone, the ion funnel, linear ARDE and its non-linear correction, charging and twist as a random walk in angle, the mask as the clock, and rare-event statistics on billions of features. Every number in Chapters 3, 4, 11, and 12 has a 3D-DRAM counterpart.

---

## Summary and Key Takeaways

1. **A liner stops the bow.** Etch–liner–etch freezes the upper profile, reducing the bow by about 1 nm, but does nothing for twist or the mask.

2. **Two tiers nearly eliminate twist.** Each 1.05 µm tier twists by about 0.6 nm (3σ) against 4.5 nm for a single 2.1 µm pass; the tier junction adds a 3.3 nm alignment term.

3. **Two tiers cost a lithography layer.** They meet the 1e specification with margin, at a cost that exceeds the etch itself.

4. **R2 single pass is the cheapest 1e route.** It meets every specification with little margin.

5. **4F² capacitors are narrower and still about 100:1.** About 1.8 µm tall at 18 nm average CD, with a 9 nm axial wall from the start.

6. **3D DRAM moves the capacitor sideways.** Its vertical etches inherit the physics of this book; its capacitor is built by lateral recess.

---

## Study Questions

1. Compute the time and ∂h/∂w for a two-tier process with tiers of 900 nm (lower) and 1200 nm (upper) using R1. Which tier dominates the twist?

2. Rebuild the tier-junction budget if the upper-tier overlay improves to 2.4 nm. What upper bottom CD then keeps the junction overlap above 18 nm?

3. Using the 1e table, compute the placement RSS for R1 two-tier at the pad, assuming the lower-tier twist and tilt act at the pad and the overlay term is 2.7 nm.

4. A 4F² array needs C_s = 7.0 fF with CD_avg 18 nm. What mold height is needed? What is the aspect ratio?

5. For a 4F² hole, the wall on the axes is 9 nm at the top. What bow CD would the axial wall tolerate if the dielectric is 4.0 nm thick? Discuss whether directional bow control is possible.

---

**Next Chapter:** [Chapter 15: Feature-Scale Modelling, Metrology & Advanced Process Control](./15-modelling-metrology-apc.md)

---

**Chapter 14 Development Status:** Complete  
**Version:** 1.0
