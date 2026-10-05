# Chapter 8: Depth-Adaptive Recipes, Gas Pulsing & Cyclic Etch

## Overview

A capacitor recipe is written as a list of steps with times. The hole does not care about time. It cares about depth, because depth sets the aspect ratio, and the aspect ratio sets the ion fraction at the bottom, the neutral supply, the polymer balance, and the charge. At 57:1 a recipe of five fixed steps was enough. At 91:1 the conditions the bottom needs at 2 µm are so different from those the neck needs at 200 nm that no single setting serves both. The recipe must change continuously with depth.

This chapter shows how to write a recipe in depth and convert it to time, develops the six-step R1 reference with its ramps, introduces gas pulsing and cyclic deposition–etch for profile control, treats the step transitions at the supports, and closes with radial tuning.

**Learning Objectives:**
- Convert a depth schedule into a time schedule using G(h)
- Explain why each parameter ramps in the direction it does
- Construct the R1 six-step recipe and its step times
- Estimate the gas-switching limits on pulsed and cyclic recipes
- Estimate the spread in arrival times at a support interface
- Solve a 2×2 radial tuning problem

---

## 8.1 Recipes in Depth

### 8.1.1 From Depth to Time

```
G(h) = h + k h² / (2w);  time spent between depths in a layer of rate ratio r:
  Δt = [G(h₂) − G(h₁)] / (r · ER₀)

R1: ER₀ = 700 nm/min, k = 0.016, w = 23 nm, k/(2w) = 3.48×10⁻⁴ nm⁻¹
Rate ratios: SiN 0.70, TEOS 1.00, BPSG 1.17
```

### 8.1.2 The Lower-Oxide Step in Depth and Time

```
Step 4 (ME2), lower BPSG from 940 to 2080 nm:

  Depth (nm)   A      ER/ER₀    Elapsed from start of etch (s)
  ───────────────────────────────────────────────────────────────
    940       40.9    0.61       113.1   (start of ME2)
   1100       47.8    0.57       133.1
   1300       56.5    0.53       160.0
   1510       65.7    0.49       190.4   (half the ME2 depth)
   1700       73.9    0.46       219.9
   1900       82.6    0.43       252.9
   2080       90.4    0.41       284.3   (top of the bottom stop)
```

Half the depth of ME2 is reached after 77 s of a 171 s step, 45% of its time. A parameter ramp written linearly in time would put half its change into the first 45% of the depth. If the intended ramp is linear in depth, it must be written as a curve in time, compressed early and stretched late.

### 8.1.3 Why Each Parameter Ramps

```
Parameter          Direction with depth   Reason
───────────────────────────────────────────────────────────────────────────
O₂                 up (+20%)              The bottom becomes polymer-limited;
                                          less oxygen is released by the
                                          slower bottom (Book #29, Ch. 3)
NF₃                0 → 8 sccm             Extra fluorine when F transmission
                                          falls; scavenges carbon
C₄F₆               down (−15%)            The neck is formed; less sidewall
                                          protection needed below the bow
V_pp               9.5 → 10.5 kV          Deflection grows with depth; higher
                                          energy holds it constant
Pulse duty         0.90 → 0.85            More off time for charge relief
DC superposition   −500 → −900 V          More electrons down the hole
Pressure           16 → 14 mTorr          Raises the narrow-ion share as the
                                          cone closes
Wafer temperature  constant (zones)       Changes are too slow to follow depth
```

The ramps are interdependent. Raising O₂ and NF₃ opens the bottom but thins the sidewall polymer, which grows the bow and the twist. Raising V_pp and lowering the pressure counteract that by narrowing the ions. A depth-adaptive recipe is a path through a multi-dimensional space that holds the bottom open while holding the walls protected, at every depth.

---

## 8.2 The R1 Reference Recipe

### 8.2.1 Step Table

```
R1 SIX-STEP REFERENCE RECIPE (illustrative)

Step  Name          Depth (nm)   Time (s)  Gas (sccm)                         Bias / source
─────────────────────────────────────────────────────────────────────────────────────────────────
1     Top SiN       0–100          12.7    CHF₃ 40, CF₄ 40, O₂ 15, Ar 200     7 kV / 2.5 kW
2     ME1 (TEOS)    100–900        92.4    C₄F₆ 32, C₄F₈ 15, O₂ 30, Ar 300    9 kV / 3.0 kW
3     Middle SiN    900–940         8.0    C₄F₆ 20, CH₂F₂ 15, O₂ 25, Ar 300   8 kV / 3.0 kW
4     ME2 (BPSG)    940–2080      171.2    C₄F₆ 32→27, C₄F₈ 15, O₂ 30→36,     9.5→10.5 kV
                                           NF₃ 0→8, Ar 300                     3.0 kW
5     Overetch      2080 + slow    40      C₄F₆ 34, C₄F₈ 10, O₂ 28, Ar 300    10 kV / 3.0 kW
                    holes                  (no NF₃; SiN-selective, ≈ 15:1)
6     Bottom open   2080–2100      35      CHF₃ 50, O₂ 10, Ar 200             3 kV sine / 1.5 kW
─────────────────────────────────────────────────────────────────────────────────────────────────
Total                              359.3
Pressure 15 mTorr (16→14 in step 4); wafer +10 °C; pulsing and DC per Chapter 6
```

### 8.2.2 Where the Time Goes

```
  Step     Depth share   Time share
  ──────────────────────────────────
  1–3      45%           31%
  4        54%           48%
  5–6       1%           21%
```

More than half of the depth and nearly half of the time is in the lower oxide. A fifth of the time is spent after the mean hole has reached the stop, on the slow holes and the bottom open. That fifth is what Chapter 12 tries to shorten.

### 8.2.3 R2 for Comparison

```
R2 FOUR-STEP REFERENCE (illustrative)

Step  Name                   Depth (nm)   Time (s)
──────────────────────────────────────────────────
1     Top SiN + ME1          0–900         61
2     Mid SiN + ME2          900–2080      92
3     Overetch               slow holes    15
4     Bottom open            2080–2100     22
──────────────────────────────────────────────────
Total                                     190
```

Because R2 etches nitride at nearly the oxide rate, the supports need no separate chemistry and the recipe has fewer transitions.

---

## 8.3 Gas Pulsing and Cyclic Deposition–Etch

### 8.3.1 The Idea

Instead of finding one gas mixture that protects the wall and opens the bottom at the same time, alternate two: a deposition sub-step that coats the wall with polymer, and an etch sub-step that clears the bottom with high-energy ions while the wall polymer lasts.

```
Cyclic sub-steps (illustrative, applied in step 2 from 200 to 900 nm):
  D (deposit): C₄F₆ 45, Ar 200, O₂ 5; bias 3 kV; 1.5 s
  E (etch):    C₄F₈ 15, O₂ 35, Ar 300; bias 10 kV; 3.5 s
  Cycle 5.0 s; 70% of the time at full bias
```

### 8.3.2 Gas-Switching Limits

```
Chamber residence time:
  Gas flow 380 sccm = 380 × 0.01267 = 4.8 Torr·L/s
  Effective plasma volume ≈ 10 L at 15 mTorr → pV = 0.15 Torr·L
  τ_res = pV / Q = 0.15 / 4.8 = 31 ms

Mass-flow controller response: 100–300 ms
Gas line from the valve to the showerhead: 50–500 ms
Showerhead plenum mixing: tens of ms
```

The chamber itself exchanges gas in about 30 ms, but the controllers and lines take ten times longer. Sub-steps shorter than about 1 s are dominated by the transition. Fast-switching valves at the showerhead and divert-to-pump lines keep the flows steady and switch only the destination, bringing transitions to about 100 ms.

### 8.3.3 What It Buys

```
Effect of cyclic etch in step 2 (illustrative):
  Bow CD:               27.5 → 26.6 nm   (−0.9 nm)
  Neck CD:              25.0 → 25.4 nm   (less polymer pinch at the top)
  Step 2 time:          92 s → 118 s     (70% of time at full bias, plus
                                          transitions)
  Total etch time:      +26 s (+7%)
```

A 0.9 nm reduction of the bow buys 0.9 nm of wall at the bow, a tenth of the minimum wall. That is worth a 7% time penalty when the bow is near its limit. Cyclic sub-steps are used where the bow forms (upper oxide) and not in the lower oxide, where they would cost more time per nanometre and buy less.

### 8.3.4 Toward Atomic-Layer Precision

The limit of this approach is an atomic-layer etch: alternating self-limiting fluorocarbon deposition and low-energy ion removal. At a few angstroms per cycle and several seconds per cycle, a 2.1 µm hole would take hours. Cyclic etch in capacitor holes uses the idea, not the self-limitation: the sub-steps are long and far from self-limiting, and they trade a little time for profile.

---

## 8.4 Step Transitions at the Supports

### 8.4.1 Arrival Spread

Not every hole reaches the middle support at the same moment. The CD distribution spreads the arrival:

```
∂h/∂w at 900 nm:
  (k h² / (2w²)) / (1 + kh/w) = (0.016 × 810,000 / 1058) / (1 + 0.626) = 7.5 nm/nm

3σ CD spread of 1.0 nm → 7.5 nm depth spread → at a bottom rate of
  ≈ 0.63 × 700 ≈ 440 nm/min in TEOS: ≈ 1.0 s arrival spread
Wafer-edge lag (Chapter 9) at 900 nm: ≈ 3 s
```

The 40 nm middle support takes 8 s. Holes at the edge reach it 3 s later than holes at the centre. A step that switches chemistry abruptly at 113 s would catch edge holes still in the upper oxide and expose centre holes to the support chemistry for 3 s longer.

### 8.4.2 Blended Support Steps

The support chemistry is therefore not a nitride-selective chemistry but a blended one, which etches nitride at about 0.7 of the oxide rate and oxide at nearly the main-etch rate. Holes that arrive early or late lose little. The penalty is a support that is cut less cleanly, with a small notch above and below it.

```
Notch at the support interface (illustrative):
  Abrupt switch:  1.5–3 nm lateral notch at the upper interface
  Blended step:   ≤ 1 nm
  Specification:  ≤ 2 nm (Chapter 1)
```

---

## 8.5 Radial Tuning

### 8.5.1 Knobs and Responses

The edge of the wafer differs from the centre in temperature, gas composition, and sheath shape. The edge sheath is tuned by the focus ring (Chapter 9). The remaining edge profile is tuned with the edge gas split and the edge temperature zone.

```
Edge sensitivities (illustrative, R1, at 140–147 mm):

                                  Edge bottom CD   Edge bow CD
  ───────────────────────────────────────────────────────────────
  Edge O₂ split (+1% of O₂)       +0.20 nm         +0.10 nm
  Edge zone temperature (+1 K)    +0.04 nm         +0.13 nm
```

### 8.5.2 A 2×2 Solution

```
Measured at the edge: bottom CD 0.8 nm low, bow CD 0.3 nm high
Wanted: Δ(bottom) = +0.8, Δ(bow) = −0.3

  0.20 x + 0.04 y = +0.8
  0.10 x + 0.13 y = −0.3

  det = 0.20 × 0.13 − 0.04 × 0.10 = 0.022
  x = (0.8 × 0.13 − 0.04 × (−0.3)) / 0.022 = 0.116 / 0.022 = +5.3%
  y = (0.20 × (−0.3) − 0.10 × 0.8) / 0.022 = −0.14 / 0.022 = −6.4 K

→ Raise the edge O₂ share by 5.3% and cool the edge zone by 6.4 K
```

Cooling the edge grows its polymer and narrows its bow, while the extra edge oxygen clears its bottom. Chapter 15 automates this as an APC feedback loop.

### 8.5.3 What Radial Tuning Cannot Fix

Gas and temperature move the CD. They do not move the tilt, which comes from the sheath shape at the edge and must be corrected by the ring. They also cannot correct an azimuthal pattern (one side of the wafer different from the other), which usually comes from the pumping port, a gas-hole blockage, or a tilted electrode, and must be fixed in hardware.

---

## Summary and Key Takeaways

1. **Write the recipe in depth.** G(h) converts depth to time. Half the lower-oxide depth is reached in 45% of its step time.

2. **Every parameter ramps with depth.** O₂, NF₃, bias, DC, and duty rise; C₄F₆, pressure, and duty fall, to hold the bottom open while the wall stays protected.

3. **The R1 recipe takes 359 s in six steps.** The lower oxide takes 48% of the time; overetch and bottom open take 21%.

4. **Cyclic sub-steps buy profile for time.** A 0.9 nm bow reduction costs about 7% more etch time. Gas switching limits sub-steps to about 1 s or longer.

5. **Support steps must be blended.** Holes reach the middle support up to about 3 s apart; an abrupt switch would notch them.

6. **Radial tuning is a small linear problem.** Edge O₂ and edge temperature move the edge bottom and bow CD in different proportions, so both can be corrected together.

---

## Study Questions

1. Write an O₂ ramp that is linear in depth from 30 sccm at 940 nm to 36 sccm at 2080 nm. Give the O₂ setpoint at 20 s intervals from the start of ME2.

2. For R2 (ER₀ 1100 nm/min, k 0.010, BPSG ratio 1.25), compute the elapsed time at 1100, 1510, and 2080 nm from the start of a combined step beginning at 900 nm.

3. A cyclic sub-step design uses D = 1.0 s and E = 2.5 s, with 0.3 s transitions. What fraction of the time is at full bias? How does the step-2 time change from 92 s?

4. The 3σ CD spread grows to 1.5 nm and the edge lag to 4 s. Compute the arrival spread at the middle support and propose a blended-step duration.

5. With the sensitivity matrix of Section 8.5.1, solve for the edge knobs needed to raise the edge bottom CD by 0.5 nm without changing the edge bow.

---

**Next Chapter:** [Chapter 9: Consumables, Walls, Arcing & Fleet Matching at Extreme Power](./09-consumables-arcing-fleet-matching.md)

---

**Chapter 8 Development Status:** Complete  
**Version:** 1.0
