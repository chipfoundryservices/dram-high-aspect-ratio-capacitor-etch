# Chapter 12: Etch Stop, Not-Open Holes & Rare-Event Statistics

## Overview

A 24 Gb die carries 2.6×10¹⁰ capacitor holes. The repair circuits can replace a limited number of failing cells, and most of that capacity is needed for retention tails and other defects. The capacitor etch is allowed about five not-open holes per die: a rate of 2×10⁻¹⁰. No metrology measures a rate like that directly, and no Gaussian distribution of CD or depth produces it. Not-open holes come from tails: holes that started narrow because their mask opening was defective, holes shadowed by particles, holes clogged by residue, and holes that the overetch could not wait for.

This chapter explains how a hole stops, how much CD deficit the overetch can cover, how the bottom stop and the landing pad share the end of the etch, how gouge and side punch arise, how the not-open budget is allocated and checked, and how tails at 10⁻¹⁰ are made visible.

**Learning Objectives:**
- List the mechanisms that stop a hole and identify which dominate at 91:1
- Compute the arrival-time delay of a narrow hole and the CD deficit the overetch covers
- Compute the bottom-stop consumption and the pad gouge for early, mean, and late holes
- Estimate the side punch for a misplaced hole
- Allocate the not-open budget and test it with a tail model
- Describe how voltage-contrast inspection and sensitized monitors reveal rare events

---

## 12.1 How a Hole Stops

```
Mechanism                         What happens                         Share at 91:1
────────────────────────────────────────────────────────────────────────────────────────
Late arrival                      The hole is narrow, so it reaches     dominant in the
                                  the stop after the overetch has       etch-caused tail
                                  ended; the bottom-open step cannot
                                  finish the oxide
Polymer stop                      A carbon-rich film forms at the        rare with R1's
                                  bottom and the ion flux there          ramps; rises with
                                  cannot clear it                        Π drift
Taper closure                     The taper closes the hole before       only for very
                                  the stop                               narrow mask holes
Blocked entry                     Particle, flake, or mask scum          large share
Residue                           Polymer, salt (R2), or W-containing    after strip; not
                                  residue at the bottom insulates the    an etch stop, but
                                  contact                                an electrical open
```

At 91:1 the late-arrival mechanism and the blocked-entry mechanism dominate. Both are set by the incoming mask more than by the etch.

---

## 12.2 Late Arrival

### 12.2.1 Arrival Time Against CD

```
Arrival time at the top of the bottom stop (2080 nm) for a hole of average
CD w = 23 − Δw (R1 layered model, Chapter 8):

  Δw (nm)    Arrival (s)    Delay (s)
  ──────────────────────────────────
   0.0         284.4          0
   1.0         289.6          5.2
   2.0         295.3         10.9
   3.0         301.6         17.2
   4.0         308.6         24.2
   5.0         316.4         32.0
```

Each nanometre of CD deficit costs about 5 s, and the cost grows for larger deficits because a narrower hole is also slower at every depth.

### 12.2.2 What the Overetch Covers

```
Overetch: 40 s after the reference hole arrives (end at 324.4 s)

Location / condition                     Lag used    Left for CD   Δw covered
──────────────────────────────────────────────────────────────────────────────
Centre, nominal mold                       0 s         40 s          ≈ 6.6 nm
Centre, 3σ-thick mold                      4.3 s       35.7 s        ≈ 5.5 nm
Edge (147 mm), nominal mold               10 s         30 s          ≈ 4.7 nm
Edge, 3σ-thick mold                       14.3 s       25.7 s        ≈ 4.2 nm
```

A hole at the wafer edge, on a thick mold, opens only if its average CD is within about 4.2 nm of the reference. The Gaussian CD spread (σ ≈ 0.3 nm on CD_avg) never reaches that. What reaches it is the tail of the mask CD distribution.

### 12.2.3 Bottom CD Binds First

```
Bottom CD sensitivity to average CD (illustrative): ∂CD_bot/∂CD_avg ≈ 1.2
  (narrow holes taper more)
Bottom CD at Δw = 2.5 nm: 19 − 1.2 × 2.5 = 16 nm (the specification limit)
```

Holes with a deficit beyond about 2.5 nm open but with a bottom CD below 16 nm and a high contact resistance. Between Δw ≈ 2.5 and ≈ 4.2 nm the hole is a weak cell; beyond ≈ 4.2 nm at the edge it is a dead cell.

---

## 12.3 The Bottom Stop and the Pad

### 12.3.1 Consumption of the Stop

During the overetch the chemistry is made selective to nitride (≈ 15:1 at the hole bottom, Chapter 8). The stop still thins.

```
SiN rate at the bottom in the overetch: 335 / 15 ≈ 22 nm/min

Arrival spread before the mean hole (RSS of CD, mold, centre position):
  earliest holes ≈ 10 s ahead of the mean

  Hole        Time on stop before BO    SiN consumed    SiN left (of 20)
  ───────────────────────────────────────────────────────────────────────
  Earliest    50 s                      18.6 nm          1.4 nm
  Mean        40 s                      14.9 nm          5.1 nm
  Latest      ≈ 0 s                     0                20.0 nm
```

The stop survives the overetch everywhere, but the earliest holes have almost none left.

### 12.3.2 Bottom Open and Gouge

```
Bottom-open step (R1): CHF₃ 50, O₂ 10, Ar 200; 3 kV sine (≈ 1.5 keV); 35 s
  SiN rate at the bottom: ≈ 45 nm/min → 26 nm capacity
  W rate (SiN : W ≈ 6): ≈ 7.5 nm/min

  Hole        Time to clear SiN    Time on W    Gouge
  ─────────────────────────────────────────────────────
  Earliest    1.9 s                33.1 s       4.1 nm
  Mean        6.8 s                28.2 s       3.5 nm
  Latest     26.7 s                 8.3 s       1.0 nm
                                                 (8.3 s of margin to clear)

Specification: gouge ≤ 8 nm; all holes clear
```

### 12.3.3 The Overetch–Gouge Trade

```
Lengthening the overetch from 40 to 50 s:
  Δw covered at the edge on a thick mold: 4.2 → ≈ 5.5 nm
  Earliest holes: 60 s on stop → 22 nm > 20 → punch-through ≈ 5 s before
    the end of overetch at 10 kV, where W etches at ≈ 20 nm/min:
    ≈ 1.8 nm + 35 s of BO on W ≈ 4.4 nm → gouge ≈ 6.2 nm
  Mask: +10 s × 1.67 nm/s ≈ 17 nm more consumed (≈ 27 nm more facet)
```

Ten seconds of overetch buys 1.3 nm of CD-deficit coverage at the edge, costs 2 nm of gouge on the earliest holes, and eats a tenth of the facet margin. Section 12.4 shows that this trade decides the not-open rate.

### 12.3.4 Side Punch

Every hole is displaced a little from its pad. Where the hole bottom overhangs the pad edge, the bottom-open step etches the pad isolation beside the pad.

```
Bottom radius 9.5 nm; pad half-width 10.5 nm → overhang = |Δ| − 1 nm

  |Δ| (nm)    Overhang (nm)    Side-punch depth (mean hole, 28 s at 45 nm/min)
  ───────────────────────────────────────────────────────────────────────────
     2            1                ≈ 21 nm (a 1 nm sliver)
     5            4                ≈ 21 nm
     7            6                ≈ 21 nm

Specification: side-punch depth ≤ 25 nm (clearance to the bit-line
  spacer below); sliver width ≤ 6 nm
```

The side punch is filled by the TiN electrode. A punch that reaches the bit line, or a sliver wide enough to approach the neighbouring storage-node contact, shorts the cell. The depth is set by the bottom-open time, the width by placement. This is a second reason, after contact area, why placement matters.

### 12.3.5 R2 and the Bottom Stop

R2 etches nitride at nearly the oxide rate. A 20 nm SiN stop lasts about 5 s at the bottom in R2's most selective setting. R2 integrations therefore use a different stop, typically a thin metal oxide such as Al₂O₃, whose fluoride is not volatile and which stops the fluorine chemistry almost completely. The bottom-open step then needs a short chlorine-based or sputter-dominated step to clear it. R2 trades the overetch–gouge problem for an extra bottom-open chemistry.

---

## 12.4 Rare-Event Statistics

### 12.4.1 The Budget

```
Not-open and functionally open budget per die (illustrative):

  Cause                                         Allocation (per die)
  ─────────────────────────────────────────────────────────────────
  Mask defects: missing or merged openings              2
  Particles and flakes (Chapter 9)                      1
  Etch late arrival (CD tail)                           0.5
  Residue (polymer, salt, W compounds)                  1
  Bottom open not cleared                               0.5
  ─────────────────────────────────────────────────────────────────
  Total                                                 5   (2×10⁻¹⁰ per hole)
```

### 12.4.2 A Tail Model for the Mask CD

Stochastic effects in EUV exposure and in the mask open give the hole CD distribution an exponential tail on the narrow side, far above the Gaussian:

```
Illustrative narrow-side tail of average CD deficit Δw:
  P(Δw > x) ≈ 3×10⁻⁶ × exp(−(x − 1 nm) / 0.35 nm),  x > 1 nm

  x (nm)    P(Δw > x)
  ─────────────────────
   2.5       4×10⁻⁸
   4.2       3×10⁻¹⁰
   5.5       8×10⁻¹²
   6.6       3×10⁻¹³
```

### 12.4.3 The Late-Arrival Rate

```
Overetch 40 s:
  Edge holes (≈ 18% of dies, worst case thick mold): P(Δw > 4.2) = 3×10⁻¹⁰
  Centre holes: P(Δw > 6.6) ≈ 3×10⁻¹³
  Per-die average ≈ 0.18 × 3.2×10⁻¹⁰ + 0.82 × 3×10⁻¹³ ≈ 5.8×10⁻¹¹
  → 2.58×10¹⁰ × 5.8×10⁻¹¹ ≈ 1.5 not-opens per die (edge dies ≈ 8 each)

Overetch 50 s:
  Edge: P(Δw > 5.5) = 8×10⁻¹² → per-die average ≈ 1.4×10⁻¹² → 0.04 per die
```

With a 40 s overetch, edge dies exceed the whole budget from late arrival alone. With 50 s, late arrival is negligible, at the cost of 2 nm more gouge and a little mask. **The overetch at 91:1 is set by the tail of the mask CD distribution at the wafer edge.** Reducing the edge lag (Chapter 9) or the tail of the mask CD (Chapter 13) is worth more than any change in the main etch.

```
Reference decision (illustrative): overetch 40 s at the centre, 50 s
  effective at the edge by radial APC of the overetch chemistry (more edge
  O₂ in the last 15 s); the recipe table keeps 40 s nominal.
```

### 12.4.4 The Weak-Cell Rate

```
Holes with bottom CD < 16 nm: P(Δw > 2.5) ≈ 4×10⁻⁸ → ≈ 1000 per die
```

These holes open, but with high contact resistance. Most still work at time zero; some fail at speed or after stress. They are a retention and reliability concern rather than a not-open concern, and they are one reason for the 1 nm margin between the 19 nm reference and the 16 nm limit.

---

## 12.5 Seeing the Tail

### 12.5.1 Voltage-Contrast Inspection

```
E-beam voltage contrast after bottom open (or after strip):
  open holes, grounded through the pad, charge differently from not-open
  holes and appear brighter (or darker) at suitable beam conditions

Hole sites per cm²: 10¹⁴ nm² / 1186 nm² = 8.4×10¹⁰
Inspecting 1 cm² of array finds, at 2×10⁻¹⁰: ≈ 17 not-opens
```

Single-beam inspection covers a few square millimetres per hour. Multi-beam tools cover more. Either way, a production wafer can be sampled at the 10⁻¹⁰ level only over a small area, so VC monitoring is statistical, accumulated over many wafers and sorted by radius.

### 12.5.2 Sensitized Monitors

To see changes in the tail before they reach product, a monitor wafer is etched with the overetch shortened (for example from 40 to 5 s). Holes with much smaller CD deficits then fail, the not-open rate rises to 10⁻⁶–10⁻⁵, and a few thousand holes of VC inspection measure it. A shift in the monitor rate, or in the slope of not-open rate against overetch time, reveals a change in the tail of the mask CD or in the edge lag.

```
Sensitized monitor (illustrative):
  Overetch 5 s, centre sites → CD-deficit coverage ≈ 1.0 nm
  Expected not-open rate ≈ P(Δw > 1.0) ≈ 3×10⁻⁶
  VC sample 10⁷ holes → ≈ 30 counts (±18% at 1σ)
```

### 12.5.3 Electrical and Bit-Map Data

The final test is the bit map. Not-open holes appear as single-bit failures at zero time, randomly placed. Clusters point to particles; radial patterns point to edge lag or tilt; lithography-field patterns point to the mask. Chapter 16 reads these signatures.

---

## Summary and Key Takeaways

1. **Holes stop late, not early.** At 91:1 the etch-caused not-opens are mostly narrow holes that arrive after the overetch ends.

2. **A nanometre of CD is about 5 s.** The 40 s overetch covers a CD deficit of about 6.6 nm at the centre and only about 4.2 nm at the edge on a thick mold.

3. **The stop barely survives.** The earliest holes keep 1.4 nm of the 20 nm SiN stop; the gouge is 1–4 nm; the side punch is about 21 nm deep on every overhanging hole.

4. **Ten seconds of overetch is a yield decision.** It covers 1.3 nm more CD deficit at the edge and cuts late-arrival not-opens from about 1.5 to 0.04 per die, for 2 nm of gouge.

5. **The mask tail sets the overetch.** An exponential narrow-side tail, not the Gaussian width, determines how many holes arrive too late.

6. **Tails are measured by amplifying them.** Sensitized monitors with a shortened overetch raise the rate to 10⁻⁶, where VC inspection can count it.

---

## Study Questions

1. Using the arrival table, estimate the CD deficit covered at the edge on a nominal mold if the edge lag is reduced from 10 to 5 s.

2. Recompute the stop consumption and the gouge of the earliest hole if the overetch selectivity falls from 15:1 to 10:1.

3. A hole is displaced by 6 nm. What is the side-punch sliver width, and what bottom-open time would keep its depth below 15 nm?

4. With the tail model of Section 12.4.2, find the overetch time at which late-arrival not-opens fall to 0.5 per die, assuming edge holes dominate and the arrival delays of Section 12.2.1.

5. Design a sensitized monitor that measures P(Δw > 2 nm). What overetch time and VC sample size would you use?

6. Explain why R2 integrations change the bottom-stop material, and what new step this requires.

---

**Next Chapter:** [Chapter 13: Mask Erosion, Faceting, Striation, Distortion & Stochastic Defects](./13-mask-striation-stochastic-defects.md)

---

**Chapter 12 Development Status:** Complete  
**Version:** 1.0
