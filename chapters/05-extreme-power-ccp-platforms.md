# Chapter 5: Extreme-Power CCP Platforms

## Overview

Book #29's capacitor chamber ran 12 kW of low-frequency bias. R1 runs 20 kW, with a sheath voltage swing near 10 kV, and the chamber must deliver it to a 300 mm wafer with sub-degree control of the ion angle at the edge. Few tools in any industry put so much RF power into so small a gap with such tight demands on uniformity. This chapter explains why the capacitor etch stays in capacitively coupled chambers, where the power goes, how the source and bias frequencies are chosen, what high voltage does to the chuck and the chamber parts, and how many chambers a fab needs.

**Learning Objectives:**
- Explain why extreme-aspect-ratio dielectric etch uses CCP rather than ICP
- Build the power balance of a 23 kW chamber
- Estimate the heat load on the wafer and the chuck
- Explain the choice of source and bias frequencies and the standing-wave limit
- Identify the high-voltage failure modes of the chuck and RF path
- Size the chamber fleet for a given wafer start rate

---

## 5.1 Why CCP

### 5.1.1 What the Etch Needs from the Plasma

```
  Requirement                         Why at 91:1
  ─────────────────────────────────────────────────────────────────────
  Mean ion energy 4–6 keV            Yield, and resistance to deflection
                                     (θ ∝ 1/E_i)
  Narrow angular spread (≤ 0.2°)     The cone is 0.45° (Chapter 3)
  Moderate density (≈ 10¹⁶–10¹⁷ m⁻³) Enough ion flux for 700 nm/min, but a
                                     thick sheath that is not too collisional
  Polymerizing chemistry with a      Neutral-rich operation (χ ≈ 2%)
  long residence time
  Uniformity to ±1% across 300 mm    ∂h/∂w = 27 nm/nm
```

### 5.1.2 CCP Against ICP

An inductively coupled source produces dense plasma at low pressure with low ion energy, and adds bias separately. At 4–6 keV, however, the bias dominates the power anyway. An ICP's high density shrinks the sheath and raises the ion flux beyond what the neutrals can support without raising χ. The dissociation in an ICP is also higher, which destroys the large fluorocarbon molecules (C₄F₆, C₄F₈) whose fragments give selectivity to the mask. A capacitive chamber with a narrow gap, a large-area upper electrode, and a moderate-density VHF source keeps the chemistry polymer-rich, the sheath thick, and the ion energy high. Every production capacitor etch at 1b and beyond uses a capacitively coupled chamber of this kind.

---

## 5.2 Power Balance

### 5.2.1 Where 23 kW Goes

```
R1: 60 MHz source 3.0 kW + 400 kHz tailored bias 20 kW = 23 kW delivered

Illustrative power balance:

  Sink                                              kW      Share
  ────────────────────────────────────────────────────────────────
  Wafer: ions + fast neutrals (sheath)              4.6     20%
  Wafer secondary electrons accelerated to the
    upper electrode (γ ≈ 0.3 at kV)                 1.4      6%
  Focus ring and wafer edge                         0.9      4%
  Upper electrode and walls: ion bombardment        8.0     35%
  Plasma: ionization, excitation, electron heating  4.5     20%
  RF losses: match, cables, chuck dielectric,
    displacement currents                           3.6     16%
  ────────────────────────────────────────────────────────────────
  Total                                            23.0    100%
```

Only a fifth of the power reaches the wafer as useful ion energy. The upper electrode receives more than the wafer, which is why it erodes (Chapter 9). The secondary electrons that leave the wafer, accelerated through the full sheath, form a kilovolt electron beam that strikes the upper electrode and heats it. This beam is also the reason DC superposition works (Chapter 6).

### 5.2.2 Heat Load on the Wafer

```
Ions and fast neutrals: 4.6 kW
Plasma radiation, recombination, and chemistry:  ≈ 0.4 kW
Total: ≈ 5.0 kW over 707 cm² → 7.1 W/cm²
(Book #29: ≈ 4.5 W/cm²)
```

The chuck must remove 7.1 W/cm² through a helium-filled gap a few micrometres thick while holding the wafer within ±1 K. Chapter 7 does the heat transfer, for both +10 °C and −60 °C.

### 5.2.3 Power Scaling with Aspect Ratio

```
Bias power needed for a mean ion energy E and ion current I_i:
  P_ion ≈ I_i × E / e;  P_bias / P_ion ≈ 4.8–5.5 (Section 5.2.1; the
  ratio rises slowly with voltage as RF and secondary-electron losses grow)

  Generation   ⟨E_i⟩      J_i (mA/cm²)   P_ion (kW)   P_bias (kW)
  ─────────────────────────────────────────────────────────────────
  1b            3.0 keV     1.2            2.5          12
  1c            3.75 keV    1.17           3.1          15
  1d (R1)       4.5 keV     1.15           3.7          20
  1e            5.5 keV     1.12           4.4          ≈ 24
```

Bias power rises with ion energy, which rises to keep the deflection constant (Chapter 3). Each generation adds about 4 kW. Generators, matches, chucks, and RF feeds have been redesigned every generation to follow.

---

## 5.3 Frequencies

### 5.3.1 Bias Frequency

```
Ion transit time across a collisionless Child-law sheath, Ar⁺, s = 4 mm, 5 kV:
  final velocity v = √(2 × 5000 × 1.60×10⁻¹⁹ / 6.63×10⁻²⁶) = 1.55×10⁵ m/s
  τ_ion ≈ 3s / v = 3 × 4×10⁻³ / 1.55×10⁵ ≈ 0.08 µs

  f_bias      Period     τ_ion / τ_RF    IED
  ─────────────────────────────────────────────────────────────────
  400 kHz     2.5 µs      0.03           follows the waveform: bimodal for a
                                          sine, shaped for a tailored wave
  2 MHz       0.5 µs      0.16           partly averaged; narrower
  13.56 MHz   74 ns       1.1            averaged; narrow, but needs far more
                                          current for the same voltage
```

At 400 kHz the ions respond to the instantaneous sheath voltage. That is a disadvantage for a sine, which spreads the IED across the full voltage swing, and an advantage for a tailored waveform, which can place most of the period at the voltage wanted. It also gives the highest peak energy for a given generator current, because the displacement current through the sheath capacitance is small. R1 therefore uses 400 kHz as the fundamental of a tailored waveform (Chapter 6).

### 5.3.2 Source Frequency and the Standing Wave

The VHF source sets the plasma density. Higher frequency gives more density per watt and less source-driven sheath voltage, but the wavelength shortens:

```
Free-space wavelength: λ₀ = c/f → 60 MHz: 5.0 m; 100 MHz: 3.0 m
In the narrow-gap CCP, the surface wave is slowed by roughly √(1 + d/(2s))
  (d: plasma gap, s: sheath thickness)
  d = 25 mm, s = 4 mm (bias-dominated sheath on the wafer side, thinner
  at the top): slow-wave factor ≈ 2–3 → λ_eff ≈ 2 m at 60 MHz

Centre-to-edge voltage variation ≈ 1 − J₀(2π R / λ_eff)
  R = 0.15 m, λ_eff = 2.0 m: 2πR/λ = 0.47 → 1 − J₀(0.47) ≈ 5.5%
  at 100 MHz (λ_eff ≈ 1.2 m): 2πR/λ = 0.79 → ≈ 15%
```

A 5% centre-high source voltage is corrected by shaping the upper electrode, by a dielectric lens behind it, or by splitting the source power into zones. At 100 MHz the correction needed is three times larger. R1 uses 60 MHz as a compromise. The bias, at 400 kHz, has no standing-wave problem, but its sheath does vary at the wafer edge (Chapter 8).

---

## 5.4 High Voltage

### 5.4.1 Where 10 kV Appears

With V_pp ≈ 10 kV on the chuck, high voltage appears across:

1. **The electrostatic chuck dielectric**, between the RF baseplate and the wafer
2. **The helium distribution holes and grooves**, which connect the wafer back to the grounded gas line
3. **The edge**, between the wafer, the focus ring, and the insulating ring below it
4. **The RF feed**, from the match to the baseplate

### 5.4.2 The Helium Holes

```
Helium in the backside: 20–40 Torr; holes ≈ 0.5 mm in diameter
pd ≈ 30 Torr × 0.05 cm = 1.5 Torr·cm → near the Paschen minimum for He
  (V_min ≈ 150 V at pd ≈ 4 Torr·cm; still only a few hundred volts at
  1.5 Torr·cm)
```

Any RF potential difference of more than a few hundred volts across a helium path will ignite a discharge, which can arc to the wafer. The chuck must make the RF potential of the wafer back, the helium holes, and the baseplate nearly equal. Porous dielectric plugs in the holes, conductive coatings in the grooves, and careful control of the dielectric thickness at each hole are standard. Arcing at the helium holes is the most common high-voltage failure of capacitor chambers, and it appears on the wafer as a cluster of damaged or not-open holes above a helium hole (Chapter 9).

### 5.4.3 Chuck Dielectric

```
Coulombic ESC, alumina or AlN dielectric 0.3–1 mm:
  Field in the dielectric from the RF swing ≈ 10 kV / 1 mm = 10 kV/mm
  Typical dielectric strength of sintered alumina: 15–20 kV/mm at DC,
  lower at RF and at temperature extremes
```

The margin is less than 2×. Chuck designs for 1d and 1e use thicker or layered dielectrics, and some move part of the RF drive to a separate electrode below the edge to share the voltage.

### 5.4.4 Chamber Parts

```
Upper electrode:   single-crystal or polycrystalline Si (consumed; Chapter 9)
Focus ring:        SiC or Si (consumed); height-adjustable
Walls and liner:   Y₂O₃ or YOF plasma-sprayed or aerosol-deposited coatings
Confinement rings: Si, SiC, or quartz
Gas distribution:  Si showerhead with zoned plenums
```

Yttria-based coatings resist fluorine and oxygen and shed fewer particles than alumina. At 23 kW the coating's fluorination and its crystallinity change the wall recombination probabilities, and the polymer balance drifts with them (Chapter 9).

---

## 5.5 Throughput and the Fleet

### 5.5.1 Cycle Time

```
R1 per wafer:
  Transfer in, chuck, stabilize          25 s
  Etch (six steps)                      359 s
  Dechuck, transfer out                  20 s
  Waferless autoclean (WAC)              60 s
  Total                                 464 s ≈ 7.7 min → 7.8 wafers/hour

R2 per wafer (Chapter 7):
  Transfer in, chuck, cool to −60 °C     45 s
  Etch                                  190 s
  Warm-up and residue desorption         40 s
  Dechuck, transfer out                  20 s
  WAC                                    50 s
  Total                                 345 s ≈ 5.8 min → 10.4 wafers/hour
```

### 5.5.2 Fleet Size

```
Fab capacity: 100,000 wafer starts per month (one capacitor etch per wafer)
  → 100,000 / (30 × 24) = 139 wafers/hour

Effective chamber rate: rate × availability (0.85) × utilization (0.90)
  R1: 7.8 × 0.85 × 0.90 = 6.0 wph → 23 chambers
  R2: 10.4 × 0.85 × 0.90 = 8.0 wph → 18 chambers
  Book #29 at 1b (7 min cycle): ≈ 20 chambers
```

The fleet grows with the aspect ratio even as the chambers improve. A two-tier mold (Chapter 14), which needs two capacitor etches per wafer, roughly doubles it.

### 5.5.3 Matching

Twenty-three chambers must produce the same hole. At ∂h/∂w = 27 nm/nm and an edge-tilt budget of 0.10°, the matching specifications are tighter than for any other dielectric etch:

```
Chamber-to-chamber matching targets (illustrative):
  Mean bottom CD           ± 0.4 nm
  Mean bow CD              ± 0.4 nm
  Edge tilt at 147 mm      ± 0.03°
  Time to bottom stop      ± 3 s
  Mask remaining           ± 30 nm
```

Chapter 9 describes how chambers are matched and kept matched as their consumables wear.

---

## Summary and Key Takeaways

1. **CCP is the only choice.** Kilovolt ions, moderate density, a thick sheath, and polymer-rich chemistry are what a narrow-gap VHF/LF CCP provides.

2. **A fifth of the power reaches the wafer as ions.** 4.6 of 23 kW; the upper electrode receives more than the wafer.

3. **The wafer takes 7.1 W/cm².** About 60% more than at 1b.

4. **Bias power follows ion energy.** About 4 kW more per generation, to hold deflection constant.

5. **400 kHz is chosen for its response, 60 MHz for its wavelength.** The low bias frequency lets a tailored waveform set the IED; the source frequency balances density against the standing wave.

6. **High voltage is the failure mode.** Helium holes near the Paschen minimum and chuck dielectrics at half their strength limit how far the voltage can rise.

7. **The fleet grows.** About 23 R1 chambers or 18 R2 chambers per 100,000 wafers per month.

---

## Study Questions

1. Using the power-balance table, estimate the bias power needed for a mean ion energy of 5.5 keV at 1.12 mA/cm², assuming the same fractional losses. What wafer heat flux results?

2. Compute 1 − J₀(2πR/λ_eff) for a 300 mm wafer at 40, 60, and 100 MHz with a slow-wave factor of 2.5. Which would you choose if the electrode could correct up to 8%?

3. The helium pressure is raised from 20 to 40 Torr to improve heat transfer. How does pd change in a 0.5 mm hole, and what does that mean for arcing?

4. Recompute the fleet for R1 if the WAC is shortened to 30 s and availability rises to 0.88.

5. A two-tier process needs two etches of 200 s each, with the R1 overheads per etch. How many chambers are needed for 100,000 wafers per month?

---

**Next Chapter:** [Chapter 6: Ion Energy Engineering — Tailored Waveforms, Pulsing & DC Augmentation](./06-ion-energy-engineering.md)

---

**Chapter 5 Development Status:** Complete  
**Version:** 1.0
