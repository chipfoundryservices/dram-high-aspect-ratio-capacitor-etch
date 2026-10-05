# Index: Book #31 Navigation Guide

## Quick Navigation

**Total Content:** 16 chapters + 7 appendices + glossary  
**Estimated Read Time:** 24–32 hours for the complete book; 5–10 hours for a focused reading path

| Part | Chapters | Theme |
|------|----------|-------|
| I | 1–4 | Fundamentals: capacitor scaling, mold and mask, ion transport and charging, neutral transport and the limits of ARDE |
| II | 5–9 | Hardware & chemistry: extreme-power CCP, ion energy engineering, cryogenic etch, depth-adaptive recipes, consumables and matching |
| III | 10–14 | Phenomena: bow and the 9 nm wall, twist and tilt, etch stop and rare events, mask and stochastic defects, beyond a single pass |
| IV | 15–16 | Production: modelling, metrology, APC, mold removal, yield, cost |

---

## Part I: Fundamentals of Extreme Aspect Ratio (Chapters 1–4)

### Chapter 1: [Why DRAM Capacitors Keep Getting Taller](./chapters/01-capacitor-scaling-aspect-ratio.md)
**Estimated Time:** 60 min | **Difficulty:** Foundation | **Reading Level:** All roles  
**Focus:** Why does the aspect ratio rise by a quarter every generation, and what must the 91:1 hole deliver?

**Key Topics:**
- Sense signal (108 mV at 9.7 fF) and the stalled EOT
- Scaling law: A ∝ 1/A_cell; roadmap from 36:1 to 112:1
- The 37 nm honeycomb, the 11 nm wall, the 9.7 fF cell
- Placement budget: 6.7 nm RSS against 7 nm; the etch owns three-quarters
- The specification sheet

**Critical Equations:** ΔV_BL = (V_DD/2)C_s/(C_s + C_BL); C_s = ε₀·3.9·π·CD_avg·H_eff/EOT; Δ = H tan θ  
**Study Questions:** 6

---

### Chapter 2: [The Extreme-Aspect-Ratio Mold, Pillar Mechanics & Hard-Mask Budget](./chapters/02-mold-pillar-mechanics-mask-budget.md)
**Estimated Time:** 60 min | **Difficulty:** Intermediate | **Reading Level:** Process/Integration  
**Focus:** What does the etch inherit, and what will stand in the hole afterwards?

**Key Topics:**
- The 2.1 µm five-layer mold; BPSG at the bottom
- Pillar stiffness ∝ (d/L)⁴; supports and the 7 nm collapse limit
- Undoped, B-doped, and W-doped carbon masks; 850 nm left, ≈ 120 s facet margin
- Stoney bow (≈ 230 µm) and incoming variation

**Critical Equations:** δ = qL⁴/(384EI); effective selectivity = H/mask lost; κ = 6σt_f/(M t_s²)  
**Study Questions:** 5

---

### Chapter 3: [Ion Transport & Charging at Extreme Aspect Ratio](./chapters/03-ion-transport-charging-extreme-ar.md)
**Estimated Time:** 75 min | **Difficulty:** Advanced | **Reading Level:** Process/Equipment/Research  
**Focus:** How many ions reach the bottom of a 91:1 hole, and what bends them?

**Key Topics:**
- 1.15 mA/cm² at 4.5 keV; 3.7 kW of ion power
- Narrow (55%, 0.2°) and broad (45%, 2°) populations
- Acceptance 0.45°; the ion funnel; Monte Carlo transmission 0.52 at A_tot 128
- Charging, deflection, and why ions alone do not explain ARDE

**Critical Equations:** θ ≈ √(T_i⊥/E_i); θ_acc = arctan(w/h_tot); θ_defl ≈ E⊥L/(2E_i)  
**Study Questions:** 5

---

### Chapter 4: [Neutral Transport, Surface Kinetics & the Limits of ARDE](./chapters/04-neutral-transport-ardelimits.md)
**Estimated Time:** 75 min | **Difficulty:** Advanced | **Reading Level:** Process/Research  
**Focus:** Where does linear ARDE come from, when does it bend, and how deep can a hole go?

**Key Topics:**
- Clausing and Coburn–Winters at L/d = 91 and 128; wall loss
- Series model: k = (3/4)χ
- R1/R2 time-to-depth; ∂h/∂w = 27.1 and 21.8 nm/nm
- Non-linear ARDE (k₂); mask- and facet-limited maximum depth

**Critical Equations:** ER = ER₀/(1 + kA + k₂A²); t = G(h)/ER₀; ∂h/∂w = (kh²/2w²)/(1 + kh/w)  
**Study Questions:** 6

---

## Part II: Hardware & Chemistry (Chapters 5–9)

### Chapter 5: [Extreme-Power CCP Platforms](./chapters/05-extreme-power-ccp-platforms.md)
**Estimated Time:** 50 min | **Difficulty:** Intermediate | **Reading Level:** Equipment  
**Key Topics:** Why CCP; 23 kW power balance (4.6 kW to the wafer); 7.1 W/cm²; bias and source frequency; standing wave; He-hole Paschen limit; fleet of 23 (R1) or 18 (R2) chambers; matching targets  
**Study Questions:** 5

### Chapter 6: [Ion Energy Engineering — Tailored Waveforms, Pulsing & DC Augmentation](./chapters/06-ion-energy-engineering.md)
**Estimated Time:** 55 min | **Difficulty:** Advanced | **Reading Level:** Equipment/Research  
**Key Topics:** Sinusoidal IED (31% below 2 keV); tailored waveform and 66 V/µs droop; collisional floor; pulsing above 70:1; DC-superposition electron beam; 12 kV limit; waveform by step  
**Study Questions:** 5

### Chapter 7: [Cryogenic & Low-Temperature Etch](./chapters/07-cryogenic-low-temperature-etch.md)
**Estimated Time:** 55 min | **Difficulty:** Advanced | **Reading Level:** Equipment/Process/Research  
**Key Topics:** Langmuir coverage ×220 at −60 °C; Y 5.8; k 0.010; chuck at −88 °C coolant; Coulombic clamping; salts and warm-up; R1 vs R2  
**Study Questions:** 5

### Chapter 8: [Depth-Adaptive Recipes, Gas Pulsing & Cyclic Etch](./chapters/08-depth-adaptive-cyclic-recipes.md)
**Estimated Time:** 55 min | **Difficulty:** Intermediate | **Reading Level:** Process  
**Key Topics:** Recipes in depth via G(h); ramps by parameter; six-step R1 (359 s); four-step R2 (190 s); cyclic sub-steps (−0.9 nm bow, +7% time); blended support steps; 2×2 edge tuning  
**Study Questions:** 5

### Chapter 9: [Consumables, Walls, Arcing & Fleet Matching at Extreme Power](./chapters/09-consumables-arcing-fleet-matching.md)
**Estimated Time:** 50 min | **Difficulty:** Intermediate | **Reading Level:** Equipment  
**Key Topics:** Electrode drift (−0.6 nm bottom CD over life); ring lift every 17 RF h; edge lag 10 s; WAC and seasoning; arcs; flakes as die killers; chamber constants worth 0.4 nm of 3σ  
**Study Questions:** 5

---

## Part III: Process Phenomena (Chapters 10–14)

### Chapter 10: [Bow, Neck & the 9 nm Wall](./chapters/10-bow-neck-wall.md)
**Estimated Time:** 60 min | **Difficulty:** Advanced | **Reading Level:** Process/Integration  
**Key Topics:** Reference profile; neck reflection Δz ≈ w/tan(2φ); bow growth 0.22 nm/min/side; gap-fill limit; bridging as an outlier problem; ion-side bow control  
**Study Questions:** 5

### Chapter 11: [Twist, Tilt & Bottom Placement at Extreme Depth](./chapters/11-twist-tilt-placement.md)
**Estimated Time:** 60 min | **Difficulty:** Advanced | **Reading Level:** Process/Integration/Research  
**Key Topics:** Twist onset A ≈ 30; random walk in angle → (h − h_on)^1.5; edge tilt and litho pre-compensation; budget 5.7 nm (R1) and 4.4 nm (R2); 1e budget; mixture-model tail  
**Study Questions:** 5

### Chapter 12: [Etch Stop, Not-Open Holes & Rare-Event Statistics](./chapters/12-etch-stop-rare-events.md)
**Estimated Time:** 60 min | **Difficulty:** Advanced | **Reading Level:** Process/Device  
**Key Topics:** Late arrival (5.2 s/nm); overetch coverage 4.2–6.6 nm; stop consumption, gouge, side punch; not-open budget; mask-tail model; OE 40 vs 50 s; VC and sensitized monitors  
**Study Questions:** 6

### Chapter 13: [Mask Erosion, Faceting, Striation, Distortion & Stochastic Defects](./chapters/13-mask-striation-stochastic-defects.md)
**Estimated Time:** 50 min | **Difficulty:** Advanced | **Reading Level:** Process/Research  
**Key Topics:** Facet descent 2.67 nm/s and 128 s margin; facet and bow; striation; ellipticity and hexagonal distortion; stochastic defect table; etch amplification; litho–etch dose trade  
**Study Questions:** 5

### Chapter 14: [Beyond a Single Pass — Two-Tier Molds, Cyclic Etch, 4F² & 3D DRAM](./chapters/14-two-tier-4f2-3d-dram.md)
**Estimated Time:** 55 min | **Difficulty:** Advanced | **Reading Level:** Integration/Research  
**Key Topics:** Etch–liner–etch; two tiers (twist 0.6 nm per tier, junction 3.3 nm); the 1e decision table; 4F² capacitor at ≈ 101:1; 3D DRAM vertical etches  
**Study Questions:** 5

---

## Part IV: Production Scale (Chapters 15–16)

### Chapter 15: [Feature-Scale Modelling, Metrology & Advanced Process Control](./chapters/15-modelling-metrology-apc.md)
**Estimated Time:** 55 min | **Difficulty:** Intermediate | **Reading Level:** Process/Equipment/Research  
**Key Topics:** Monte Carlo + site balance + level set; reduced-order models and surrogates; HV-SEM, CD-SAXS, OCD limits; ≈ 5% endpoint knee; feed-forward, EWMA feedback, consumable offsets; virtual metrology  
**Study Questions:** 5

### Chapter 16: [Mold Removal, Pillar Stability, Yield & Cost of Ownership](./chapters/16-mold-removal-yield-coo.md)
**Estimated Time:** 50 min | **Difficulty:** Intermediate | **Reading Level:** Integration/Management  
**Key Topics:** Strip and clean; ALD exposure ∝ A²; electrode voids from re-entrant bow; capillary drying; bit-map signatures; ≈ $47 per wafer; value of yield; economics of the next 10:1  
**Study Questions:** 5

---

## Appendices

| Appendix | Content |
|----------|---------|
| [A](./appendices/A-material-properties.md) | Mold, mask, pad, electrode, dielectric, chamber, and liquid properties; constants |
| [B](./appendices/B-chemistry-surface-kinetics.md) | Gases, sticking probabilities, reactions, cryogenic adsorption, volatility, Π, OES lines |
| [C](./appendices/C-standard-procedures.md) | Full-depth series, PM qualification, ring lift, HV-SEM, CD-SAXS, sensitized monitor, WAC, cryo chuck |
| [D](./appendices/D-process-windows.md) | R1 and R2 recipes, windows, sensitivity table, ARDE, capacitance, and tilt lookups |
| [E](./appendices/E-scaling-transport-calculations.md) | All closed-form models with reference values |
| [F](./appendices/F-metrology-modelling-reference.md) | Metrology methods, feature-scale model inputs/outputs, ROM parameters, pitfalls |
| [G](./appendices/G-troubleshooting-guide.md) | Symptom-driven troubleshooting |
| [Glossary](./GLOSSARY.md) | Terminology |

---

## Reading Paths by Role

### Process Engineer (≈ 9 hours)
Chapters 1, 3, 4, 8, 10, 11, 12 → Appendices D, G

### Equipment Engineer (≈ 8 hours)
Chapters 3, 5, 6, 7, 9, 15 → Appendices A, C

### Integration Engineer (≈ 8 hours)
Chapters 1, 2, 10, 11, 14, 16 → Appendix E

### Device Engineer (≈ 5 hours)
Chapters 1, 12, 16

### Researcher and Modeller (≈ 11 hours)
Chapters 3, 4, 6, 7, 11, 13, 15 → Appendices B, E, F

---

## Cross-Reference Map to Other Books

| Book | Title | Used in |
|------|-------|---------|
| #1–5 | Plasma Physics & Chemistry Fundamentals | Ch. 3, 5, 6 |
| #6–10 | Dielectric Etch & Fluorocarbon Chemistry | Ch. 4, 8 |
| #11–15 | Advanced Plasma Engineering | Ch. 5–9, 15 |
| #23 | Contact Hole Etch | Ch. 3, 12 |
| #24 | 3D NAND Slit Etch | Ch. 14 |
| #25 | 3D NAND High-Aspect-Ratio Oxide/Nitride Stack Etch | Ch. 3, 7, 11, 14 |
| #26 | DRAM Isolation Trench Etch | Ch. 1 |
| #27 | DRAM Word-Line Conductor Etch | Ch. 1 |
| #29 | DRAM Capacitor Hole Etch | Throughout (1b-class baseline) |
| Companion | DRAM Capacitor Mold Etch | Ch. 2, 16 |
| Companion | DRAM Bit-Line Contact Etch; DRAM Bit-Line Stack Etch | Ch. 1, 12 |
| Companion | Carbon Hard Mask Etch | Ch. 2, 13 |
| Companion | Silicon Nitride Etch | Ch. 2, 8 |

---

## Study Questions Summary

**Total Study Questions:** 83 (5–6 per chapter × 16 chapters)  
**Nature:** Mostly calculation-based  
**Topics:** Capacitance scaling, pillar deflection, mask budget, ion transmission, ARDE series model, maximum depth, power balance, IED and droop, cryogenic adsorption and heat balance, depth-to-time conversion, ring lift, bow geometry, twist growth, late-arrival statistics, facet margin, two-tier comparison, APC, cost

Examples:
- Derive the aspect-ratio scaling law at fixed C_s and EOT
- Compute pillar deflection for two support schemes
- Show that k = (3/4)χ from the series model
- Compute the facet-limited maximum depth for a narrower hole
- Convert a depth-linear O₂ ramp into a time schedule
- Derive σ_x ∝ (h − h_on)^1.5 from a random walk in angle
- Find the overetch that holds late-arrival not-opens below 0.5 per die
- Compare R1, R2, and two-tier options at 1e
- Apply EWMA feedback to five days of bottom-CD data
- Compare the cost of 10 s of overetch with the value of the yield it protects

---

## How to Use This Index

1. **First time?** Read PREFACE.md, then this INDEX, then Chapter 1.
2. **Focused reading?** Pick your role from the reading paths above.
3. **Reference mode?** Jump to the chapter. Use Appendix G for symptoms and Appendix E for formulas.
4. **Deep dive?** Read Chapters 1–16 in order and work the study questions.

---

**Index Version:** 1.0  
**Last Updated:** 2026-10-05  
**Next:** Begin [Chapter 1: Why DRAM Capacitors Keep Getting Taller](./chapters/01-capacitor-scaling-aspect-ratio.md)
