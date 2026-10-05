# Book #31: DRAM High-Aspect-Ratio Capacitor Etch — Scaling the Storage-Node Etch Beyond 70:1 for 1c/1d-Class and Next-Generation DRAM

## Overview

**Book #31** is a technical reference on **high-aspect-ratio (HAR) DRAM capacitor etch**: what happens to the storage-node etch when the hole stops being merely deep and becomes extreme. Book #29 described the capacitor hole of a 1b-class array, 1.6 µm deep and 28 nm wide on average, an aspect ratio near 57:1. This book follows the same etch two generations further. In the reference **1d-class 6F² array** of this book, the holes sit on a 37 nm hexagonal pitch. Each hole opens at 26 nm, averages 23 nm, and must still be at least 16 nm wide at the bottom of a **2.10 µm** mold. The aspect ratio at the average diameter is **91:1**, and about 128:1 if the remaining mask is counted. A 24 Gb die carries about **26 billion** of these holes.

The cell capacitance target has not moved: about 10 fF. The dielectric has stopped getting thinner, because leakage sets a floor near 0.5 nm EOT. The footprint keeps shrinking. The only lever left is height, so the aspect ratio climbs by roughly 15–20 per generation. Every effect that was manageable at 50:1 becomes a limit near 90:1:

- **The bottom rate falls to 41%** of the open-area rate, and the last third of the depth takes as long as the first two-thirds.
- **Width becomes depth twice as fast.** A hole 1 nm narrower ends **27 nm shallower** at fixed time, against 15 nm in Book #29.
- **The hole accepts less than half a degree.** Edge to edge, a finished hole with its mask accepts ions within 0.45°.
- **A fifth of a degree misses the pad.** A 0.2° tilt over 2.1 µm moves the bottom 7.3 nm, the whole placement budget.
- **The wall between holes is 11 nm** at the top and must stay above 9 nm at the bow.
- **The mask is the clock.** About 2.1 µm of oxide and nitride must come out through a doped-carbon mask, and the mask, not the mold, often decides when the etch must stop.

This book covers the physics that sets these limits and the technologies that push them back: ion energies near 5 keV with tailored-waveform bias, cryogenic and HF-based chemistry, doped and metal-containing carbon masks, depth-adaptive recipes, cyclic etch, two-tier molds, and feature-scale modelling tied to production control. **The question it answers is not how to etch a capacitor hole, but how far the capacitor hole can be pushed, and what it costs at each step.**

---

## Intended Audience

This book is written for **semiconductor industry professionals** with working knowledge of plasma processing:

- **Process Engineers**: extending a capacitor recipe from 60:1 to 90:1 and beyond; controlling depth, bottom CD, bow, twist, mask budget, and not-open tails as the aspect ratio rises
- **Equipment Engineers**: specifying extreme-power CCP chambers, tailored-waveform and pulsed bias generators, cryogenic chucks at −60 °C under 20 kW of RF, and consumables that survive the highest sheath voltages in the fab
- **Integration Engineers**: choosing between taller single-pass molds and two-tier molds; setting mold height, support positions, and pitch against capacitance, pillar stability, bridging, and placement
- **Device Engineers**: understanding how the capacitor scales when EOT stalls, and how extreme-aspect-ratio defects appear as low capacitance, shorts, opens, and retention tails
- **Researchers and Modellers**: studying ion and neutral transport beyond 90:1, charging at kilovolt sheaths, cryogenic surface chemistry, feature-scale Monte Carlo and level-set profile models, and the capacitor etch for 4F² vertical-channel and 3D DRAM

The material assumes a working knowledge of plasma physics (Books #1–5), fluorocarbon dielectric etch (Books #6–10), and advanced plasma engineering (Books #11–15). **Book #29 (DRAM Capacitor Hole Etch)** is the direct predecessor: it develops the 1b-class capacitor etch at 50:1, and this book builds on it rather than repeating it. Book #25 (3D NAND High-Aspect-Ratio Oxide/Nitride Stack Etch) covers the deepest holes in production. The companion volume *DRAM Capacitor Mold Etch* covers the mold module from the other side.

---

## Technical Scope

### Core Concepts Covered

**Scaling & Geometry:**
- Why the capacitor grows taller every generation: the stalled EOT and the fixed charge target
- The aspect-ratio roadmap from 10:1 to beyond 100:1
- The 1d-class honeycomb on a 37 nm pitch; wall, open fraction, capacitance
- The placement budget at the bottom of a 2.1 µm hole

**The Incoming Stack:**
- A 2.1 µm nitride-supported mold and the mechanics of 90:1 pillars
- Doped amorphous-carbon, boron-carbon, and metal-containing hard masks
- The mask budget as the clock of the etch
- Stress, wafer bow, and incoming variation at extreme film thickness

**Transport & Kinetics at Extreme Aspect Ratio:**
- Ion energy and angular distributions under a 10 kV sheath
- Specular reflection, the ion funnel, and ion flux at 90:1
- Neutral transport beyond L/d = 90; Knudsen and Clausing limits
- Why ARDE becomes non-linear, and the maximum achievable depth
- Charging at kilovolt sheaths and the scaling of deflection with depth

**Equipment & Chemistry:**
- Extreme-power CCP platforms (20+ kW of bias)
- Tailored-waveform, pulsed, and DC-augmented bias
- Cryogenic and low-temperature chucks; HF- and H-based chemistry
- Depth-adaptive recipes, gas pulsing, and cyclic deposition–etch
- Consumable wear, arcing, particles, and fleet matching at extreme power

**Process Phenomena:**
- Bow, neck, and the 9 nm wall
- Twist and tilt as instabilities that grow with aspect ratio
- Etch stop, not-open holes, and rare-event statistics at 10⁻⁹
- Mask faceting, striation, distortion, and stochastic defects
- Two-tier molds, cyclic etch, 4F² vertical-channel and 3D DRAM

**Production Integration:**
- Feature-scale modelling, virtual metrology, and APC
- HV-SEM, CD-SAXS, and electrical monitors for 90:1 holes
- Mold removal, pillar leaning, and capillary collapse as customers
- Yield, throughput, and cost of ownership as the aspect ratio rises

### Technology Context

- **Device architectures:** 6F² buried-channel DRAM from the 1b to the 1d generation (DDR5, LPDDR6, HBM4 core dies); 4F² vertical-channel and 3D DRAM as next forms
- **Capacitor structures:** single-sided TiN pillar capacitors in a nitride-supported mold (primary focus); two-tier molds; cryogenic single-pass alternatives
- **Process sequence:** Capacitor HAR etch follows the landing-pad module, the mold and mask depositions, and the hole patterning and mask open. It comes before the strip and clean, bottom-electrode deposition, support opening, mold removal, dielectric, and plate
- **Manufacturing scale:** 300 mm wafers, about 6 min of etch inside an 8 min chamber cycle for the fluorocarbon reference, 3.2 min for the cryogenic alternative; the largest dielectric etch fleet in a DRAM fab

---

## Book Organization

### Part I: Fundamentals of Extreme Aspect Ratio (4 Chapters)

**Chapter 1: Why DRAM Capacitors Keep Getting Taller**
- The charge target and the stalled EOT
- The aspect-ratio roadmap and its scaling law
- The 1d-class honeycomb, the 11 nm wall, and the 9.7 fF cell
- The placement budget and the specification sheet at 91:1

**Chapter 2: The Extreme-Aspect-Ratio Mold, Pillar Mechanics & Hard-Mask Budget**
- The 2.1 µm mold and why it needs supports
- Pillar stiffness, leaning, and the height limit
- Doped and metal-containing carbon masks; the mask as the clock
- Stress, bow, and incoming variation

**Chapter 3: Ion Transport & Charging at Extreme Aspect Ratio**
- Ion energy and angle under a 10 kV sheath
- The acceptance cone, specular reflection, and the ion funnel
- Ion flux at the bottom of a 90:1 hole
- Charging and deflection as functions of depth

**Chapter 4: Neutral Transport, Surface Kinetics & the Limits of ARDE**
- Clausing and Coburn–Winters beyond L/d = 90
- Ion–neutral synergy and the bottom balance
- Why ARDE turns non-linear; the maximum depth
- Fluorocarbon and HF chemistry at the bottom of the hole

### Part II: Hardware & Chemistry (5 Chapters)

**Chapter 5: Extreme-Power CCP Platforms**
- Power scaling from 12 kW to 20+ kW
- Frequency choice and plasma uniformity at high power
- RF delivery, voltage stress, and chamber materials
- Throughput and the fleet

**Chapter 6: Ion Energy Engineering — Tailored Waveforms, Pulsing & DC Augmentation**
- From bimodal to narrow IED at 5 keV
- Pulsing for charge relief at 90:1
- DC superposition and electron injection
- Voltage limits and arcing

**Chapter 7: Cryogenic & Low-Temperature Etch**
- Adsorption-controlled etch and the role of HF
- Cryogenic chucks under 20 kW
- Condensation, selectivity, and profile at −60 °C
- When cryogenic etch wins

**Chapter 8: Depth-Adaptive Recipes, Gas Pulsing & Cyclic Etch**
- Recipes as functions of depth, not of time
- Continuous ramps and the six-step reference
- Gas pulsing and cyclic deposition–etch
- Radial and center/edge control

**Chapter 9: Consumables, Walls, Arcing & Fleet Matching at Extreme Power**
- Electrode, ring, and window wear at 10 kV
- Wall conditioning and drift
- Arcing, particles, and not-opens
- Matching dozens of chambers to sub-degree tilt

### Part III: Process Phenomena (5 Chapters)

**Chapter 10: Bow, Neck & the 9 nm Wall**
- The profile at 91:1
- Why the bow moves down and grows as the hole deepens
- Bridging statistics on the honeycomb
- Bow control

**Chapter 11: Twist, Tilt & Bottom Placement at Extreme Depth**
- Twist as an instability and its onset aspect ratio
- Growth of twist with depth: the scaling law
- Edge tilt, mask tilt, and the 0.2° budget
- Detection and correction

**Chapter 12: Etch Stop, Not-Open Holes & Rare-Event Statistics**
- Why holes stop at 90:1
- The bottom CD and the minimum contact
- Rare events at 26 billion holes per die
- Bottom open and the landing pad

**Chapter 13: Mask Erosion, Faceting, Striation, Distortion & Stochastic Defects**
- The mask as it erodes
- Facets, the neck, and the bow below them
- Striation and hole distortion
- Stochastic patterning defects that the etch amplifies

**Chapter 14: Beyond a Single Pass — Two-Tier Molds, Cyclic Etch, 4F² & 3D DRAM**
- Two-tier molds and their alignment
- Cryogenic single pass versus two tiers
- Capacitors for 4F² vertical-channel DRAM
- Vertical etches in 3D DRAM

### Part IV: Production Scale (2 Chapters)

**Chapter 15: Feature-Scale Modelling, Metrology & Advanced Process Control**
- Feature-scale Monte Carlo and level-set models
- HV-SEM, CD-SAXS, OCD, and electrical monitors at 91:1
- Virtual metrology and model-based APC
- Feed-forward, feedback, and consumable offsets

**Chapter 16: Mold Removal, Pillar Stability, Yield & Cost of Ownership**
- Strip, clean, electrode, support open, mold removal
- Pillar leaning and capillary collapse
- Yield signatures at extreme aspect ratio
- Throughput, cost, and the economics of the next 10:1

---

## Key Technical Themes

1. **Height is the last lever.** With EOT stalled near 0.5 nm and the footprint shrinking about 20% per generation, the capacitor grows about 15% taller and its aspect ratio about 25% per generation. The aspect ratio rises from 57:1 (1b) to 91:1 (1d).
2. **Width becomes depth, faster.** ∂h/∂w = (kA²/2)/(1 + kA) grows faster than the aspect ratio itself. At 91:1 it is 27 nm per nm. The CD distribution, not the mean, sets the overetch.
3. **The cone closes.** The finished hole with its mask accepts ions within 0.45°. Ion angle, not ion energy, limits the bottom rate.
4. **Errors grow with depth.** Twist and tilt are angular errors. Their lateral effect grows linearly with depth, and twist itself grows faster than linearly once a hole passes its onset aspect ratio.
5. **The tail is the yield.** At 26 billion holes per die, a not-open rate of 10⁻⁸ is 260 dead cells per die. Extreme aspect ratio moves the problem from the mean to the tail.
6. **The mask is the clock.** With effective selectivity near 3.5 to doped carbon, the mask budget, not the mold, decides how long the etch may run.
7. **Every 10:1 costs.** Going from 81:1 to 91:1 at the same CD adds about 18% to the etch time, about 18% to ∂h/∂w, and roughly a third to the twist at the bottom.

---

## Cross-References to Prior Books

**Related Books in the Series:**

- **Books #1–5** (Plasma Physics & Chemistry Fundamentals): sheath physics, ion energy and angular distributions, free-molecular transport
- **Books #6–10** (Dielectric Etch & Fluorocarbon Chemistry): fluorocarbon polymer, oxide/nitride selectivity, CCP dielectric etch
- **Books #11–15** (Advanced Plasma Engineering): RF delivery, pulsing, gas delivery, temperature control, endpoint detection
- **Book #23** (Contact Hole Etch): lower-aspect-ratio oxide holes
- **Book #24** (3D NAND Slit Etch): high-aspect-ratio slots through oxide/nitride
- **Book #25** (3D NAND High-Aspect-Ratio Oxide/Nitride Stack Etch): channel holes at 60:1 and beyond; the cryogenic precedent
- **Book #26** (DRAM Isolation Trench Etch) and **Book #27** (DRAM Word-Line Conductor Etch): the 6F² array beneath the capacitor
- **Book #29** (DRAM Capacitor Hole Etch): the direct predecessor; the 1b-class capacitor hole at 57:1
- **Companion volumes:** *DRAM Capacitor Mold Etch*; *DRAM Bit-Line Contact Etch*; *DRAM Bit-Line Stack Etch*; *Carbon Hard Mask Etch*; *Silicon Nitride Etch*

Book #29 asked how to etch a capacitor hole. This book asks how far that hole can be pushed before the physics, the mask, or the yield says stop.

---

## File Organization

```
dram-high-aspect-ratio-capacitor-etch/
├── README.md            ← You are here
├── PREFACE.md
├── INDEX.md
├── GLOSSARY.md
│
├── chapters/
│   ├── 01-capacitor-scaling-aspect-ratio.md
│   ├── 02-mold-pillar-mechanics-mask-budget.md
│   ├── 03-ion-transport-charging-extreme-ar.md
│   ├── 04-neutral-transport-ardelimits.md
│   ├── 05-extreme-power-ccp-platforms.md
│   ├── 06-ion-energy-engineering.md
│   ├── 07-cryogenic-low-temperature-etch.md
│   ├── 08-depth-adaptive-cyclic-recipes.md
│   ├── 09-consumables-arcing-fleet-matching.md
│   ├── 10-bow-neck-wall.md
│   ├── 11-twist-tilt-placement.md
│   ├── 12-etch-stop-rare-events.md
│   ├── 13-mask-striation-stochastic-defects.md
│   ├── 14-two-tier-4f2-3d-dram.md
│   ├── 15-modelling-metrology-apc.md
│   └── 16-mold-removal-yield-coo.md
│
└── appendices/
    ├── A-material-properties.md
    ├── B-chemistry-surface-kinetics.md
    ├── C-standard-procedures.md
    ├── D-process-windows.md
    ├── E-scaling-transport-calculations.md
    ├── F-metrology-modelling-reference.md
    └── G-troubleshooting-guide.md
```

---

## Constraints & Scope

### What This Book Covers
✅ Storage-node capacitor etch for 6F² DRAM at aspect ratios from 60:1 to beyond 100:1 (primary focus)  
✅ The scaling physics of ion and neutral transport, charging, and surface kinetics at extreme depth  
✅ Fluorocarbon, cryogenic, and HF-based chemistries; tailored-waveform and pulsed bias  
✅ Mask budget, pillar mechanics, and the integration consequences of taller molds  
✅ Feature-scale modelling, metrology, APC, yield, and cost of ownership  
✅ Two-tier molds and the capacitor etch for 4F² and 3D DRAM  

### What This Book Does NOT Cover
❌ The 1b-class capacitor etch in full detail (see Book #29)  
❌ The amorphous-carbon mask-open etch in detail (see *Carbon Hard Mask Etch*)  
❌ High-k dielectric and electrode deposition chemistry in detail  
❌ 3D NAND channel holes, except as comparison (see Book #25)  
❌ Vendor-specific recipes or proprietary tool parameters  

### A Note on Numbers
Numbers in this book come from established plasma physics, published literature trends, and representative production practice. Worked examples use **illustrative values** chosen to show the method, and the arithmetic is written out so readers can substitute their own data. A single **reference process** ties the chapters together: a 1d-class 6F² array (F = 14 nm, cell area 1176 nm²), storage-node holes on a 37 nm hexagonal pitch, 26 nm top CD, 23 nm average CD, 19 nm bottom CD at the pad, a 2.10 µm mold (100 nm top SiN support, 800 nm upper oxide, 40 nm middle SiN support, 1140 nm lower oxide, 20 nm bottom SiN stop), a 1.50 µm boron-doped carbon mask, a W landing pad 21 nm wide, and a dielectric with EOT 0.50 nm. Two etch processes are carried through the book: **R1**, a fluorocarbon etch at +10 °C with a 20 kW tailored-waveform bias, and **R2**, a cryogenic HF-based etch at −60 °C. The transport, ARDE, placement, and capacitance numbers come from closed-form models collected in Appendix E. Treat recipe values as starting points for a design of experiments, never as qualified process conditions.

---

## Development Status

**Book #31 Foundation:** Complete  
**Part I (Chapters 1–4):** Complete  
**Part II (Chapters 5–9):** Complete  
**Part III (Chapters 10–14):** Complete  
**Part IV (Chapters 15–16):** Complete  
**Back Matter (Appendices A–G, Glossary):** Complete  

---

## Next Steps

1. **Read [PREFACE.md](./PREFACE.md)** for the motivation and reading guidance
2. **Read [INDEX.md](./INDEX.md)** for the detailed chapter outline and reading paths by role
3. **Begin [Chapter 1](./chapters/01-capacitor-scaling-aspect-ratio.md)**: Why DRAM Capacitors Keep Getting Taller

---

**Book #31 Version:** 1.0  
**Last Updated:** 2026-10-05  
**Series:** ChipFoundryServices Technical Series
