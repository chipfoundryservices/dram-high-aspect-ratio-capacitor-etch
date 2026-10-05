# Preface: The Hole That Keeps Getting Deeper

## Why This Book Exists

Book #29 described the DRAM capacitor hole at the 1b generation: 1.6 µm deep, 28 nm wide on average, an aspect ratio near 57:1. It was already one of the hardest etches in the fab. Two generations later the same cell must hold the same charge in about two-thirds of the area. The dielectric cannot get thinner, because the leakage through it would drain the cell between refreshes. The only remaining lever is height. In the reference 1d-class process of this book, the mold is 2.10 µm tall, the hole averages 23 nm, and the aspect ratio is **91:1**. A 24 Gb die carries about 26 billion of these holes.

A 60% increase in aspect ratio sounds like a matter of etching longer. It is not. Every mechanism that makes a deep hole hard grows faster than the depth:

1. **The rate falls further.** At 91:1 the bottom etches at 41% of the open-area rate. The etch time grows as h + kh²/(2w), not as h. A mold 31% taller and a hole 18% narrower take about 24% longer to etch, even with a better chemistry, and 60% longer with the old one.

2. **Width becomes depth, much faster.** At fixed time, a hole 1 nm narrower ends 27 nm shallower. At 57:1 the figure was 15 nm. A CD distribution that was comfortable at the 1b generation now decides the overetch, and the overetch eats the mask and gouges the pad.

3. **The cone closes.** With the remaining mask on top, the finished hole accepts ions within 0.45° edge to edge. The sheath must deliver ions that are both energetic and almost perfectly parallel. Ion angle, not ion energy, limits the bottom rate.

4. **Angles become misses.** The landing pad is 21 nm wide. A tilt of 0.2° over 2.1 µm moves the bottom 7.3 nm, which is the entire placement budget. Twisting, which grows with depth once the hole passes about 30:1, adds to it.

5. **The tail becomes the product.** At 26 billion holes per die, a not-open rate that was invisible at 10⁻⁹ per hole is 26 dead cells per die. Rare events in the bottom 100 nm of the hole decide the yield.

6. **The mask becomes the clock.** About 2.1 µm of oxide and nitride must be removed. Undoped carbon would need to be so thick that the mask itself would add 60% to the aspect ratio. Doped and metal-containing carbon masks buy selectivity at the cost of a harder mask open and new defects.

This book treats extreme aspect ratio as **a regime with its own physics**, not as a longer version of the 50:1 etch.

---

## Unique Aspects of Extreme-Aspect-Ratio Capacitor Etch

### 1. Scaling Laws, Not Recipes

At 50:1 a capacitor recipe can be tuned by experiment. At 90:1 the experiments are slow, expensive, and hard to read, because a single cross-section shows one hole out of billions. The engineer needs scaling laws that say how time, CD sensitivity, bow, twist, and mask loss change with aspect ratio. Most of this book is built around such laws, written in closed form, with the reference values substituted.

### 2. Two Chemistries, Not One

The fluorocarbon chemistry that built every capacitor to date is near its limit. Cryogenic and HF-based chemistries etch faster, suffer less ARDE, and twist less, at the cost of new hardware and new failure modes. This book carries both through every chapter: **R1**, a fluorocarbon etch at +10 °C, and **R2**, a cryogenic etch at −60 °C.

### 3. The Instabilities Grow

Bow, twist, and striation are not simply larger at 90:1. Twist is an instability. Below an onset aspect ratio it does not appear; above it, it grows faster than the depth. Mask faceting feeds the bow, and the bow feeds the twist. The book treats these as coupled.

### 4. The Pillar Must Stand

After the etch and the electrode, the mold is removed and the electrode stands as a pillar 2.1 µm tall and 23 nm wide, an aspect ratio of 91:1 in a free-standing metal tube. Its stability limits mold height as surely as the etch does. Placement errors from the etch become bending moments on the pillar.

### 5. Modelling Becomes Production Control

At extreme aspect ratio the hole cannot be measured often enough. Feature-scale models, calibrated to occasional cross-sections and frequent scatterometry, become part of the control loop. The book shows how.

---

## Why This Book Is Organized This Way

Book #31 follows the same four-part structure as Books #19–29:

**Part I: Fundamentals (Chapters 1–4)**
- Why the capacitor keeps getting taller, the mold and mask that must support it, and the transport and kinetics that set the limits of extreme aspect ratio

**Part II: Hardware & Chemistry (Chapters 5–9)**
- Extreme-power chambers, tailored-waveform and pulsed bias, cryogenic etch, depth-adaptive and cyclic recipes, and the consumables and matching that keep dozens of chambers alike

**Part III: Phenomena (Chapters 10–14)**
- Bow and the 9 nm wall, twist and tilt, etch stop and rare-event statistics, mask erosion and stochastic defects, and schemes beyond a single pass

**Part IV: Production (Chapters 15–16)**
- Modelling, metrology, APC, mold removal, pillar stability, yield, and cost

### Reading Paths

**Process Engineers:** Chapters 3, 4, 8, 10, 11, 12  
→ Transport limits, ARDE, recipe design by depth, bow, twist, etch stop

**Equipment Engineers:** Chapters 5, 6, 7, 9, 15  
→ Power scaling, waveforms, cryogenic chucks, consumables, fleet matching

**Integration Engineers:** Chapters 1, 2, 11, 14, 16  
→ Capacitance scaling, mold and mask, placement, two-tier molds, pillar stability

**Device Engineers:** Chapters 1, 12, 16  
→ How the capacitor scales and how its defects become failing bits

**Researchers and Modellers:** Chapters 3, 4, 6, 7, 11, 15  
→ Ion and neutral transport, ARDE limits, waveforms, cryogenic kinetics, twist instability, feature-scale models

---

## Key Questions This Book Answers

1. **Why must the capacitor grow 25% taller every generation, and when does that stop?**
2. **How does etch time scale with aspect ratio, and what is the deepest hole a given chemistry can etch?**
3. **How narrow is the ion acceptance cone at 90:1, and what fraction of ions reach the bottom?**
4. **Why does a 1 nm narrower hole end 27 nm shallower, and how should the overetch be set?**
5. **How does twist grow with depth, and how much of the 7 nm placement budget does it consume?**
6. **What does a not-open rate of 10⁻⁹ mean on a die with 26 billion holes?**
7. **How long does a doped-carbon mask last, and when does the mask, not the mold, end the etch?**
8. **When does cryogenic etch beat fluorocarbon etch, and when does a two-tier mold beat both?**
9. **How can feature-scale models be used for production control?**
10. **What does each additional 10:1 of aspect ratio cost, per wafer and per die?**

---

## How to Read This Book

**Complete study (2–3 weeks):** Read Part I closely, then work through Parts II and III in order. Finish with Part IV.

**Focused study (3–5 days):** Read Chapters 1, 3, and 4, then follow the reading path for your role.

**Reference mode:** Go straight to the chapter you need. Use the INDEX, GLOSSARY, Appendix E for formulas, and the Appendix G troubleshooting guide.

**Every chapter includes:**
- Learning objectives
- Quantitative models with worked numerical examples
- Scaling relations that show how each result changes with aspect ratio
- Representative production values, labelled as illustrative where appropriate
- Summary and key takeaways
- Study questions

**Appendices provide:**
- A: Mold, mask, pad, and chamber material properties
- B: Chemistry and surface-kinetics data, including cryogenic adsorption
- C: Standard operating procedures
- D: Process windows and lookup tables for R1 and R2
- E: Scaling, transport, placement, and capacitance calculations
- F: Metrology and modelling reference
- G: Troubleshooting guide

---

## A Note on Data and Depth

The relationships in this book (sheath physics, ion angular distributions, free-molecular transport, fluorocarbon and HF surface kinetics, surface charging, beam mechanics, parallel-plate capacitance) are well established in the literature. The specific numbers in recipes, tables, and worked examples are **representative**. They are chosen to be physically consistent and close to typical practice, but they are not qualified conditions for any particular tool, layout, or node. Where a value is illustrative, the text says so and shows the arithmetic, so readers can repeat the analysis with their own measurements.

Throughout the book, a **reference process** ties the examples together:

```
Reference device:      1d-class DRAM, 6F² cell, buried-channel array transistor
                       (F = 14 nm, cell area 6F² = 1176 nm²); 24 Gb die,
                       ≈ 2.58×10¹⁰ cells (plus redundancy)
Reference layout:      storage-node holes on a hexagonal lattice, pitch p = 37 nm
                       (one hole per cell: (√3/2)p² = 1186 nm² ≈ 6F²)
Reference hole:        top CD 26 nm, average CD 23 nm, bottom CD 19 nm at the pad;
                       wall at top 11 nm; maximum bow CD 28 nm (spec, wall ≥ 9 nm);
                       bottom CD ≥ 16 nm (spec); aspect ratio 91:1 at average CD
Reference mold:        H = 2.10 µm total:
                         top SiN support      100 nm
                         upper oxide (TEOS)   800 nm
                         middle SiN support    40 nm
                         lower oxide (BPSG)  1140 nm
                         bottom SiN stop       20 nm
Reference mask:        boron-doped amorphous carbon (B-ACL) 1.50 µm + SiON 40 nm;
                       ≈ 1.45 µm after the mask open; ≥ 500 nm must remain
Reference pad:         W landing pad, 21 nm wide at its top; |Δ| ≤ 7 nm
                       bottom-placement budget; pad gouge ≤ 8 nm
Reference capacitor:   single-sided TiN pillar, ZrO₂/Al₂O₃/ZrO₂-class dielectric,
                       EOT 0.50 nm → C_s ≈ 10.5 fF for the full sidewall,
                       ≈ 9.7 fF after the supports and bottom stop
Reference etch R1:     fluorocarbon, dual-frequency CCP; 60 MHz source 3.0 kW;
                       400 kHz tailored-waveform bias 20 kW (V_pp ≈ 10 kV,
                       mean ion energy ≈ 4.5 keV); 15 mTorr; C₄F₆/C₄F₈/O₂/Ar/NF₃;
                       wafer +10 °C; ER₀ = 700 nm/min (TEOS);
                       ARDE coefficient k = 0.016 (w = 23 nm);
                       six steps ≈ 359 s (main etch 284 s, overetch 40 s,
                       bottom open 35 s)
Reference etch R2:     cryogenic, same chamber class with a −60 °C chuck;
                       HF/C₄F₈/H₂/O₂/Ar-based; ER₀ = 1100 nm/min (TEOS);
                       k = 0.010 (w = 23 nm); ≈ 190 s including overetch
                       and bottom open
```

We assume you know basic plasma physics, the general behaviour of fluorocarbon oxide etch, and, ideally, the 1b-class capacitor etch of Book #29. We do **not** assume you know the scaling of transport and charging beyond 60:1, cryogenic surface chemistry, the mechanics of tall pillars, or feature-scale modelling.

---

## Organization of This Repository

1. **README.md**: overview, scope, file structure, cross-references
2. **PREFACE.md**: this document
3. **INDEX.md**: detailed chapter outline, reading paths, estimated times
4. **chapters/**: Chapters 1–16
5. **appendices/**: Appendices A–G
6. **GLOSSARY.md**: technical terminology

---

## Acknowledgments & Scope

Book #31 is part of the **ChipFoundryServices Technical Series**. It draws on:

- The published plasma etch literature on high-aspect-ratio contact and capacitor etch, ARDE, charging, bowing, twisting, cryogenic etch, and tailored-waveform bias
- Classical results on free-molecular flow through tubes (Knudsen, Clausing) and on ion transport in collisionless and collisional sheaths
- Feature-scale modelling literature (Monte Carlo particle transport, level-set and string profile evolution)
- Published descriptions of DRAM capacitor scaling, support structures, high-k dielectrics, and pillar stability
- Representative industrial practice for DRAM storage-node modules
- The earlier books in this series, especially Books #25 and #29

It is a **technical reference for professionals**. Background in plasma processing is assumed.

---

## Final Thought

A capacitor 23 nm wide and 2.1 µm tall has the proportions of a pipe 2.3 cm wide and 2.1 m long. It is repeated 26 billion times on a lattice where the walls between the pipes are thinner than the pipes, and every generation asks for the pipe to be half a metre longer.

Mastering extreme-aspect-ratio capacitor etch means seeing that **the depth that buys capacitance also narrows the ion cone, starves the bottom, magnifies every angle, and moves the yield into the tail**, and knowing in numbers how much each of those costs. This book is meant to build that understanding.

---

**Welcome to Book #31: DRAM High-Aspect-Ratio Capacitor Etch — Scaling the Storage-Node Etch Beyond 70:1 for 1c/1d-Class and Next-Generation DRAM.**
