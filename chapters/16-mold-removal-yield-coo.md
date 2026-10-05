# Chapter 16: Mold Removal, Pillar Stability, Yield & Cost of Ownership

## Overview

The capacitor etch is judged by the module that follows it. The strip and clean must empty a 91:1 hole of residue. The electrode must coat a re-entrant profile without voids. The mold must be removed and the pillars dried without collapsing them onto each other. The dielectric and plate must fill gaps that the bow has narrowed. Finally the bit map, weeks later, shows which cells hold their charge. This chapter follows the hole through those steps, reads the yield signatures that point back to the etch, and closes with the cost of the etch per wafer and the economics of the next 10:1 of aspect ratio.

**Learning Objectives:**
- Identify the post-etch steps that depend most on the hole profile
- Explain how a re-entrant bow creates voids in the electrode
- Estimate capillary forces during drying and relate them to pillar collapse
- Read bit-map signatures and assign them to etch causes
- Build a cost-of-ownership estimate for R1, R2, and two-tier processes
- Compare the cost of the etch with the value of yield and of scaling

---

## 16.1 Strip and Clean

### 16.1.1 Removing the Mask

```
B-ACL strip: O₂/N₂ or O₂/H₂O plasma ash, ≈ 850 nm remaining
  Boron in the mask forms B₂O₃, which is not volatile in the ash; it is
  removed in the following wet clean (B₂O₃ dissolves in water and dilute
  acids)
W-ACL (if used): W oxides require a separate wet chemistry that must not
  attack the W pad at the hole bottom
```

### 16.1.2 Cleaning the Hole

```
Polymer and fluoride residues on the walls and the bottom; W fluorides
  and oxyfluorides on the pad
Wet clean: dilute HF-based or organic chemistry; removes 0.3–0.5 nm of
  oxide per side (0.6–1.0 nm of CD)

Liquid exchange in a 23 nm × 2.1 µm hole, by diffusion:
  t ≈ L² / D = (2.1×10⁻⁶)² / 10⁻⁹ m²/s ≈ 4 ms
```

Diffusion empties a filled hole quickly. The risk is not exchange but wetting: a hole that traps a gas bubble is never cleaned. Pre-wetting with a low-surface-tension liquid and controlled immersion avoid it.

### 16.1.3 Queue Time

Fluorine residues and moisture corrode the W pad. The time between etch and clean is limited, typically to about 4 hours, and wafers that exceed it are cleaned with a longer recipe.

---

## 16.2 The Electrode

### 16.2.1 ALD in a 91:1 Hole

```
Precursor exposure needed for conformal ALD in a hole of aspect ratio A
  grows roughly as A² (diffusion-limited saturation of the wall)
  57:1 → 91:1: (91/57)² = 2.5× the exposure per cycle
```

Electrode deposition time per wafer rises with the square of the aspect ratio unless pulse and purge times are shortened by better reactor design. At 1e it is a throughput concern for the ALD tools.

### 16.2.2 Voids from the Re-Entrant Bow

The single-sided pillar fills the hole with TiN. A hole whose neck (25 nm at 120 nm depth) is narrower than its bow (27.5 nm at 450 nm) closes at the neck first. The bow region below is left with a void.

```
Fill closes at the neck when the film thickness reaches 12.5 nm
Bow region at that moment: 27.5 − 2 × 12.5 = 2.5 nm wide void,
  extending ≈ 300 nm along the bow
```

A small, enclosed void does little harm. If the void opens during mold removal (when the support or the TiN seam is breached), the HF reaches the inside of the pillar and its surface, and the pillar weakens or breaks. Reducing the neck-to-bow ratio, not only the bow, is therefore an integration requirement.

---

## 16.3 Support Open, Mold Removal, and Drying

### 16.3.1 Sequence

```
1. Pattern and etch openings in the top SiN support
2. HF wet etch removes the upper TEOS through the openings
3. Open the middle support through the same openings
4. HF removes the lower BPSG (faster in HF than TEOS, Chapter 2)
5. Rinse; replace water with a low-surface-tension liquid (IPA); dry
```

### 16.3.2 Capillary Forces

```
Laplace pressure in a gap g between pillars:
  ΔP = 2γ cos θ / g
  Water (γ = 0.072 N/m, θ ≈ 0): g = 14 nm → ΔP ≈ 10 MPa
  IPA (γ = 0.022 N/m): ≈ 3.1 MPa
```

These pressures are enormous, but symmetric pressure on all sides of a pillar does no harm. The damage comes from asymmetry, where one side of a pillar dries before the other. Chapter 2 modelled that as an effective lateral load of about 2×10⁻³ N/m for IPA and showed that the reference supports keep the larger span's deflection near 2 nm against a 7 nm collapse limit. With water instead of IPA the effective load is about three times larger, and the lower span would collapse.

### 16.3.3 Etch Errors Reduce the Margin

```
Collapse margin = (gap/2) / δ
  Reference: 7 / 2.1 = 3.3
  Gap reduced by twist and bow toward a neighbour (Chapter 2): 4.25 / 2.1 = 2.0
  Wall thinned by a striation outlier to 7 nm: 3.5 / 2.1 = 1.7
```

A pillar pair with a margin below about 1.5 has a measurable collapse probability under real drying non-uniformity. Leaning pillars that touch stay stuck by adhesion and short the two cells.

### 16.3.4 Alternatives

Supercritical CO₂ drying has no liquid–gas interface and no capillary force. It is slower and more expensive, and it is being introduced at the generation where the support scheme no longer gives enough margin with IPA.

---

## 16.4 Yield Signatures

```
Bit-map signature                        Likely etch cause                     Chapter
─────────────────────────────────────────────────────────────────────────────────────────
Random single-bit fails, time zero       Not-open (late arrival, mask tail),   12, 13
                                          residue
Random single bits failing at speed      Weak cells: bottom CD < 16 nm,        12
or after stress                           high contact R
Pairs of failing bits on the line of     Bridging at the bow; pillar           10, 16
centres (twin-bit fails)                  collapse
Groups of 3–7 failing bits               Pillar leaning clusters; particles   9, 16
Clusters of thousands of bits            Flakes, arcs                          9
Ring of fails at the wafer edge          Edge lag (not-open), edge tilt        9, 11
                                          (placement), edge bow
Pattern repeating with litho fields      Mask CD or mask-open defects          13
Retention-time tail shifted low          C_s low: average CD, bow/bottom       1, 10
(whole wafer)                             balance, depth
Retention tail, few cells, very short    Dielectric weak spots at striations   13, 16
                                          or seams; side punch toward neighbours
Chamber-dependent shift in any of the    Chamber matching, consumable age      9, 15
above
```

The capacitor etch leaves fingerprints in at least half of the signatures a DRAM fab tracks. Linking each bit-map lot back to its etch chamber and consumable age is standard practice.

---

## 16.5 Repair and Die Yield

```
Repair capacity (illustrative, 24 Gb die): replacement of a few thousand
  rows and columns' worth of failing cells, shared among all defect types

Allocations from this book:
  Not-open holes                         ≤ 5 per die      (Chapter 12)
  Bridged pairs                          ≤ 8 per die      (Chapter 10)
  Misplaced contacts (functional)        ≪ 1 per die      (Chapter 11)
  Weak cells (bottom CD < 16 nm)         ≈ 1000 per die   (Chapter 12;
                                                           partly screened)

Die killers (beyond repair):
  Flakes (> 1 µm) in the array           < 0.05% of dies   (Chapter 9)
  Arc damage                             < 0.1% of wafers
  Clustered collapse                      rare with IPA + supports
```

Random single-cell fails are repairable within these budgets. Die loss comes from clustered defects and from a whole-wafer capacitance shift that moves the retention tail beyond what refresh margins can absorb.

---

## 16.6 Cost of Ownership

### 16.6.1 Per Wafer

```
Cost per wafer of the capacitor etch (illustrative, US$):

  Item                           R1          R2          R1 two-tier
  ───────────────────────────────────────────────────────────────────
  Chamber capital (5-year life)   30          28          ≈ 50 (2 etches,
    R1 $8M at 6.0 wph effective;                           shorter each)
    R2 $10M at 8.0 wph effective
  Consumables (electrode, ring,    6           4           ≈ 9
    liner, chuck share)
  Gases and abatement              4           6 (HF)      ≈ 6
  Electricity (RF + chiller)       1.5         3           ≈ 2.5
  Maintenance labour               3           3           ≈ 5
  Facilities and space             2           2           ≈ 3
  ───────────────────────────────────────────────────────────────────
  Etch total                     ≈ 47        ≈ 46        ≈ 76
  Added module steps (2nd mask,    —           —          ≈ 150–250
    EUV exposure, fill, CMP, strip)
```

### 16.6.2 The Value of Yield

```
Wafer value (illustrative): ≈ 1100 gross dies × 0.90 yield × $3.0 ≈ $3000

1% of die yield ≈ $30 per wafer ≈ two-thirds of the whole capacitor etch cost
```

A process change that costs $10 per wafer more and recovers 0.5% of yield pays for itself. The 10 s overetch extension of Chapter 12 costs about $1 per wafer in chamber time and saves edge dies worth far more. **The capacitor etch is cheap relative to the yield it controls**, which is why fabs accept longer etches, more monitoring, and more chambers for small yield gains.

### 16.6.3 The Economics of the Next 10:1

```
Going from 1d (A = 91) to 1e (A = 112):
  Bits per wafer: +25% (cell area 0.8×) → revenue per wafer ≈ +25%
  Capacitor etch cost with R2: ≈ +15% (longer etch, more chambers)
                    with R1 two-tier: ≈ +60% plus ≈ $200 of module steps
  As a share of the added revenue ($750 per wafer at $3000 base):
    R2: ≈ $7 (≈ 1%)     R1 two-tier: ≈ $230 (≈ 30%)
```

Scaling the cell remains enormously profitable as long as the capacitor can be made in a single pass. The two-tier route keeps scaling profitable but takes about a third of its gain. This is the economic case for cryogenic chemistry, for more selective masks, and for every improvement in this book that postpones the second tier.

---

## Summary and Key Takeaways

1. **The bow decides the electrode.** A neck narrower than the bow closes the TiN fill early and leaves a void in the bow region.

2. **Drying is a mechanical test of the etch.** Capillary pressures of 3–10 MPa are harmless when symmetric; twist, bow, and striation make them asymmetric.

3. **The bit map reads the etch.** Single bits point to not-opens, pairs to bridging or collapse, rings to the edge, field patterns to the mask, retention shifts to capacitance.

4. **The etch costs about $47 per wafer.** R2 costs about the same as R1; two-tier adds about $30 of etch and $150–250 of other steps.

5. **Yield is worth far more than etch time.** One percent of yield is worth about two-thirds of the etch cost.

6. **The next 10:1 is worth having if it stays single-pass.** R2 keeps the 1e capacitor at about 1% of the added revenue; two tiers take about 30%.

---

## Study Questions

1. Compute the void width in the bow region if the neck is 26 nm and the bow 27.5 nm. At what neck-to-bow ratio does the void vanish?

2. Estimate the Laplace pressure for IPA in a 9.5 nm gap at the bow and for water in the same gap. Why does the pressure itself not collapse a symmetric pillar?

3. Using the cost table, compute the R1 cost per wafer if chamber availability falls from 0.85 to 0.78.

4. A recipe change adds 20 s to R1 and reduces not-open holes from 5 to 2 per die. If each not-open hole beyond 4 per die causes a 0.1% die-yield loss through exhausted repair, is the change worth making?

5. Repeat the economics of Section 16.6.3 for a scenario where the wafer value is $2000 and the two-tier added module cost is $150.

---

**Book #31 Complete.** Continue with the appendices, beginning with [Appendix A: Material Properties](../appendices/A-material-properties.md).

---

**Chapter 16 Development Status:** Complete  
**Version:** 1.0
