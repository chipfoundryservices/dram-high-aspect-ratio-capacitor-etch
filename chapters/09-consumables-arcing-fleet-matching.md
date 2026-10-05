# Chapter 9: Consumables, Walls, Arcing & Fleet Matching at Extreme Power

## Overview

A capacitor chamber is never the same twice. Every wafer erodes the upper electrode and the focus ring, coats and cleans the walls, and adds a little to the fluorination of the yttria liner. At 23 kW these changes are fast, and at 91:1 the hole responds to them more strongly than at any earlier generation: a ring that has lost 100 µm tilts the edge holes by about 0.08°, nearly the whole edge-tilt budget. Twenty or more chambers must make the same hole while each ages on its own clock.

This chapter covers the wear of the upper electrode and focus ring and its effect on the hole, the walls and their conditioning, arcing and particles as sources of not-open holes, the matching of a fleet, and the maintenance schedule that holds it all together.

**Learning Objectives:**
- Estimate electrode and ring erosion per wafer and their effect on the hole
- Compute the ring-lift schedule needed to hold edge tilt within budget
- Describe the wall states of a capacitor chamber and how they are reset
- Estimate the hole loss from particles and flakes and set adder limits
- Identify arc sources and their wafer signatures
- Set chamber-matching targets and a preventive maintenance plan

---

## 9.1 The Upper Electrode

### 9.1.1 Erosion

```
Ion power to the upper electrode and walls (Chapter 5): ≈ 8 kW
Silicon upper electrode erosion rate (illustrative, R1 with DC
superposition): ≈ 3 µm per RF hour, centre-weighted

RF time per wafer (R1): 359 s → 10.0 wafers per RF hour
Electrode life (usable thickness ≈ 2.4 mm): ≈ 800 RF hours ≈ 8000 wafers
```

### 9.1.2 What Changes as It Wears

1. **The gap grows** by up to 2.4 mm in the centre. The plasma density moves outward a little; the centre ion flux falls.
2. **The gas holes widen.** Hole diameter grows with erosion. The gas distribution moves toward the centre and its jets weaken.
3. **The silicon release changes.** Silicon sputtered from the electrode scavenges fluorine in the gas phase. As the surface roughens, the release per ion rises, and the plasma becomes more polymerizing.

```
Drift without compensation over the electrode life (illustrative):
  Bottom CD (centre)   −0.6 nm
  Bow CD               −0.3 nm
  Time to stop         +4 s
  Not-open rate        rises ≈ 3× in the last 15% of life

Compensation: O₂ offset +0.7 sccm per 100 RF hours (APC, Chapter 15)
```

### 9.1.3 Electrode Change

A new electrode releases less silicon, so the first wafers after a change are less polymerizing than the last wafers before it. The APC offset is reset with the electrode, and the chamber is seasoned (Section 9.3) before production wafers run.

---

## 9.2 The Focus Ring and the Edge

### 9.2.1 Why the Ring Sets the Edge Tilt

At the wafer edge the sheath above the wafer meets the sheath above the ring. If the ring surface is lower than the wafer surface, or its sheath thinner, the sheath boundary bends downward at the edge and ions arrive tilted outward. The ring is set so that its sheath matches the wafer's. As the ring erodes, its surface falls and the tilt grows.

```
Edge tilt sensitivity (illustrative, at 147 mm): 0.08° per 100 µm of ring
  height loss (Book #29)
Effect on the bottom of a 2.1 µm hole: 2100 × tan(0.08°) = 2.9 nm
  per 100 µm of ring wear
```

### 9.2.2 Ring Erosion and the Lift Schedule

```
SiC ring erosion (R1, illustrative): ≈ 1.5 µm per RF hour at the inner edge
→ 100 µm in ≈ 67 RF hours (≈ 670 wafers)

Edge-tilt budget: 0.10° (Chapter 1); matching window ± 0.03°
Lift step to hold tilt within ±0.02° of target: 25 µm
  → a lift every ≈ 17 RF hours (≈ 170 wafers), or continuous lift
    computed from RF hours

Lift range 1.2 mm → ring life ≈ 800 RF hours (matched to the electrode)
```

The lift is calibrated by measuring the edge tilt on a monitor wafer after each ring change and periodically thereafter (Appendix C). Ring erosion is not uniform around the circumference, so the lift corrects the mean tilt but not its azimuthal variation, which grows with ring age.

### 9.2.3 Edge Lag

Edge holes also see a slightly lower ion flux and a different gas mix, and they reach the bottom stop later:

```
Edge lag at the bottom stop (R1, illustrative): ≈ 10 s at 147 mm
  (about 3 s at the middle support, Chapter 8)
Equivalent depth deficit at the stop: 10 s × 335 nm/min / 60 ≈ 56 nm
```

The edge lag is one of the largest terms in the overetch (Chapter 4). It is reduced by the edge gas split and edge temperature (Chapter 8), and it grows with ring wear because the ring takes ions from the edge as it erodes.

---

## 9.3 Walls and Seasoning

### 9.3.1 Wall States

```
State                       Cause                         Effect on the hole
──────────────────────────────────────────────────────────────────────────────
Clean Y₂O₃                  After wet clean               Low polymer on walls;
                                                          F recombination high;
                                                          bottom CD large, bow large
Fluorinated YOF surface     Hours of fluorocarbon plasma  F recombination lower;
                                                          stable
Polymer-coated              During each wafer             Walls source and sink
                                                          CFₓ; Π drifts within wafer
Overcoated (WAC failure)    Missing or short WAC          Π high; bottom CD small;
                                                          flakes
```

### 9.3.2 Waferless Autoclean

After each wafer, an O₂/NF₃ plasma without a wafer removes the polymer the previous wafer left on the walls. Every wafer then starts from the same wall state.

```
R1 WAC (illustrative): O₂ 500, NF₃ 100 sccm, 200 mTorr, source 2 kW, 60 s
Endpoint: CO and F emission return to the clean-wall baseline
```

### 9.3.3 Seasoning After Maintenance

A freshly cleaned chamber etches differently from a seasoned one. Seasoning wafers coat the walls to their production state before product runs.

```
Seasoning after a wet clean (illustrative):
  25 bare-Si or blanket-oxide wafers with the production recipe
  Qualification: depth series, edge-tilt monitor, particle wafer
```

---

## 9.4 Arcing

### 9.4.1 Sources

```
Arc source                  Signature on the wafer                 Prevention
────────────────────────────────────────────────────────────────────────────────────
Helium holes in the chuck   Craters in a pattern matching the      Porous plugs; potential
                            helium holes; clusters of not-opens    equalization; chuck age
Wafer-to-ring               Damage at the extreme edge; ring       Ring–wafer gap and
                            pitting                                potential control
Backside particles or       Single crater, often near the centre   Chuck cleaning; backside
films                                                              inspection
Wafer bevel films           Edge flakes; craters at the bevel      Bevel clean before etch
Mask defects (conductive    Local damage at the defect             Mask-open inspection
residues)
```

### 9.4.2 Detection and Response

Arc detection monitors the bias voltage and current for transients faster than about 1 µs. On an arc, the generator shuts down within a few microseconds and the wafer is flagged. A single arc can destroy thousands of holes and throw particles across the wafer; a chamber that arcs twice within a few hundred wafers is stopped for inspection.

```
Arc-rate target: < 1 per 1000 wafers per chamber
```

---

## 9.5 Particles and Not-Open Holes

### 9.5.1 How Particles Close Holes

A particle that lands on the mask before or during the etch shadows the holes beneath it. A particle that falls into a hole during the etch can block it. Either way, the holes do not open.

```
Holes covered by a particle of diameter D (hole site area 1186 nm²):
  D = 50 nm:  π/4 × 50² / 1186 ≈ 1.7 → 2 holes
  D = 200 nm: ≈ 26 holes
  D = 2 µm (flake): ≈ 2600 holes
```

### 9.5.2 The Particle Budget

```
24 Gb die, array area ≈ 2.58×10¹⁰ × 1186 nm² = 30.6 mm²; array efficiency
  0.55 → die ≈ 56 mm² = 0.56 cm²

Not-open budget: ≤ 5 per die from all causes (Chapter 1)
Allocation to particles: ≤ 1 per die

Adder limit for particles ≥ 45 nm (each blocking ≈ 2–3 holes):
  ≤ 1 / (0.55 × 0.56 cm² × 2.5) ≈ 1.3 per cm² is the extreme upper bound;
  production limit ≈ 0.02 per cm² (≈ 14 per wafer), giving ≈ 0.02 dead
  cells per die
```

Small particles are therefore not the problem; the adder limit is set by other concerns and leaves large margin. The problem is the rare large flake. A 2 µm flake kills about 2600 holes. Repair can replace a few hundred to a few thousand cells per die, with most of that capacity spent on other defects, so one flake in the array is usually a lost die.

```
Flake budget:
  Gross dies per wafer ≈ 70,700 mm² / 56 mm² × 0.87 (edge loss) ≈ 1100
  Fraction of the wafer area that is array ≈ 0.87 × 0.55 ≈ 0.48
  Die loss per flake landing anywhere on the wafer ≈ 0.48 / 1100 = 0.044%
  Target die loss from flakes ≤ 0.05% → < 1 flake (> 1 µm) per wafer
```

Flakes come from wall polymer that the WAC did not remove, from coatings that crack, and from the ring and confinement parts. Chapter 12 combines them with the other causes of not-open holes.

---

## 9.6 Fleet Matching

### 9.6.1 Where Chambers Differ

```
Source of chamber-to-chamber difference       Hole response
──────────────────────────────────────────────────────────────────────
Electrode gap and flatness (± 50 µm)          Bottom CD ± 0.2 nm; time ± 2 s
Showerhead hole size and pattern              Radial CD profile
Ring height after calibration (± 10 µm)       Edge tilt ± 0.008°
Chuck helium conductance by zone              Radial bow ± 0.3 nm
Generator waveform fidelity                   Low-energy fraction ± 2%;
                                              bow ± 0.3 nm
Wall coating age and fluorination             Π ± 2%
```

### 9.6.2 Matching Procedure

1. **Hardware match** at installation and after each major PM: gap, flatness, ring height, chuck conductance, generator waveform.
2. **Golden-wafer match**: a reference wafer etched in each chamber, with depth series, bow and bottom CD by cross-section and CD-SAXS, and edge tilt by HV-SEM.
3. **Chamber constants**: small per-chamber offsets in O₂, edge split, and time that bring each chamber to the fleet target (Chapter 15).
4. **Ongoing monitoring**: a daily monitor wafer per chamber and statistical comparison of product metrology by chamber.

### 9.6.3 How Much Matching Matters

```
Total bottom CD variance across the fleet:
  σ²_total = σ²_within-wafer + σ²_wafer-to-wafer + σ²_chamber
  Illustrative: 0.40² + 0.25² + 0.15² = 0.16 + 0.0625 + 0.0225 = 0.245
  σ_total = 0.49 nm → 3σ = 1.5 nm (meets ± 1.5 nm, Chapter 1)

Without chamber constants: σ_chamber ≈ 0.4 nm → σ_total = 0.62 → 3σ = 1.9 nm
```

Chamber constants are worth 0.4 nm of 3σ bottom CD, a quarter of the specification.

---

## 9.7 Preventive Maintenance

```
Preventive maintenance plan (R1, illustrative):

  Item                     Interval (RF hours)   Action
  ────────────────────────────────────────────────────────────────────
  Ring lift                every ≈ 17            automatic step
  Edge-tilt monitor        every 100             HV-SEM monitor wafer
  Particle monitor         daily                 bare-Si wafer, adders
  Upper electrode          ≈ 800                 replace; season; requalify
  Focus ring               ≈ 800                 replace with electrode
  Wet clean (liner, walls) ≈ 800                 with the electrode change
  Chuck                    ≈ 4000–8000           replace on helium leak or
                                                 arc history
```

Synchronizing the electrode, ring, and wet clean on one interval reduces the number of seasoning and requalification cycles. The cost is that parts with longer life are discarded early.

---

## Summary and Key Takeaways

1. **The electrode drifts the polymer.** About 3 µm of silicon per RF hour; without compensation, the bottom CD falls about 0.6 nm over an 800 RF-hour life.

2. **The ring sets the edge tilt.** About 0.08° per 100 µm of wear, or 2.9 nm at the bottom of a 2.1 µm hole; the ring is lifted about every 17 RF hours.

3. **The edge lags.** About 10 s at the bottom stop, one of the largest overetch terms.

4. **WAC resets the walls every wafer.** Seasoning resets them after every wet clean.

5. **Flakes, not particles, kill dies.** A 2 µm flake removes about 2600 holes, beyond repair.

6. **Chamber constants are worth a quarter of the CD spec.** Matching reduces 3σ bottom CD from about 1.9 to 1.5 nm across the fleet.

---

## Study Questions

1. The DC superposition is raised so that electrode erosion rises to 4 µm per RF hour. What is the new electrode life in wafers, and how should the APC O₂ offset rate change?

2. A ring erodes at 2.0 µm per RF hour. With the tilt sensitivity of Section 9.2.1, how often must it be lifted to hold the tilt within ±0.02°?

3. Compute the number of holes lost to a 500 nm particle. With 1000 dies per wafer and 0.55 array efficiency, what particle density of this size gives one lost cell per die on average?

4. A chamber's WAC endpoint is lost and the WAC times out at 30 s instead of 60 s. Predict the effect on the next wafer's bottom CD and not-open rate.

5. Recompute the fleet 3σ bottom CD if the within-wafer σ falls to 0.30 nm. How much would chamber constants then be worth?

---

**Next Chapter:** [Chapter 10: Bow, Neck & the 9 nm Wall](./10-bow-neck-wall.md)

---

**Chapter 9 Development Status:** Complete  
**Version:** 1.0
