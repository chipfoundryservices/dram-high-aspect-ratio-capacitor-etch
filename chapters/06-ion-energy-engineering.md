# Chapter 6: Ion Energy Engineering — Tailored Waveforms, Pulsing & DC Augmentation

## Overview

At 91:1 the ions that matter are those in a narrow cone at high energy. A sinusoidal low-frequency bias delivers a bimodal ion energy distribution in which nearly a third of the ions arrive below 2 keV. Those ions etch little at the bottom, deflect strongly in the charged hole, and strike the upper walls where they feed the bow. Removing them is the job of waveform engineering. The other job is charge: something must reach the bottom of the hole that carries negative charge, and isotropic electrons cannot.

This chapter covers the sinusoidal IED and its low-energy tail, tailored and pulse-shaped bias waveforms and the droop that limits them, bias pulsing and the neutralization of the hole in the off phase, DC superposition and the ballistic electron beam, the voltage limits of the hardware, and how the waveform is set step by step.

**Learning Objectives:**
- Compute the fraction of ions below a given energy for a sinusoidal bias
- Explain how a tailored waveform narrows the IED and compute its droop
- Estimate the collisional low-energy population that no waveform can remove
- Explain charge relief by bias pulsing and estimate its cost in etch time
- Explain how DC superposition sends electrons to the bottom of the hole
- Identify the voltage and arcing limits of the bias system

---

## 6.1 The Sinusoidal IED

### 6.1.1 Ions Follow the Sheath

At 400 kHz the ion transit time (≈ 0.08 µs) is 3% of the RF period (Chapter 5). Each ion gains the sheath voltage present when it crosses.

```
Sheath voltage for a sinusoidal bias that just collapses each cycle:
  V(t) = V_rf (1 + sin ωt),   0 ≤ V ≤ 2V_rf,  mean = V_rf

Ion flux to the wafer is nearly constant over the cycle (Bohm flux),
so the IED is the distribution of V over a uniform phase:
  P(E < E*) = 1/2 + arcsin(E*/V_rf − 1)/π
  dP/dE ∝ 1/√(1 − (E/V_rf − 1)²)   → peaks at both ends (bimodal)
```

### 6.1.2 The Low-Energy Tail

```
Mean ion energy 4.5 keV with a sine: V_rf = 4.5 kV, V_pp ≈ 9 kV

  E* (keV)     P(E < E*)
  ──────────────────────
   0.5           0.15
   1.0           0.21
   2.0           0.31
   3.0           0.39
```

Almost a third of the ions arrive below 2 keV, and one in seven below 0.5 keV. Their deflection by a given lateral field is 2–9 times that of a 4.5 keV ion. Chapter 10 shows that most of the bow at 91:1 is cut by ions from this tail and from the collisional population.

---

## 6.2 Tailored Waveforms

### 6.2.1 The Idea

If the generator can hold the wafer at a nearly constant negative voltage for most of the period and briefly let it rise to collapse the sheath, the ions that cross during the long negative phase all gain the same energy. The brief positive excursion admits electrons to neutralize the charge the ions brought.

```
Pulse-shaped bias (illustrative, 400 kHz):
  Period 2.5 µs
  Negative phase: −V₀ for ≈ 2.3 µs (92%)
  Positive excursion (sheath collapse): ≈ 0.2 µs (8%)
  Ions crossing in the negative phase: E ≈ V₀ − droop (Section 6.2.2)
  Ions crossing during transitions: spread from ≈ 0 to V₀
```

Such waveforms are produced by summing a fundamental and several harmonics with controlled phases, by switched-mode generators that synthesize the shape directly, or by a pulsed DC supply in series with an RF path. The details are vendor-specific; the effect on the IED is similar.

### 6.2.2 Droop

During the negative phase, the ion current charges the capacitance between the wafer surface and the RF electrode, so the surface voltage drifts toward zero:

```
Chuck dielectric: alumina, ε_r ≈ 9.8, thickness 0.5 mm
  C/A = ε₀ ε_r / t = 8.854×10⁻¹² × 9.8 / 5×10⁻⁴ = 1.74×10⁻⁷ F/m²
      = 1.74×10⁻¹¹ F/cm²

Droop rate: dV/dt = J_i / (C/A) = 1.15×10⁻³ / 1.74×10⁻¹¹
            = 6.6×10⁷ V/s = 66 V/µs
Over the 2.3 µs negative phase: ΔV ≈ 150 V
```

A droop of 150 V on a 5.5 kV level is a 3% energy spread, narrow enough. Generators can also add a compensating ramp to cancel it. The droop grows with ion current and with dielectric thickness, so a thicker chuck dielectric, chosen for voltage strength (Chapter 5), widens the IED unless compensated.

### 6.2.3 What No Waveform Can Remove

Ions that undergo charge exchange inside the sheath arrive with only the part of the voltage below their birth point.

```
Child-law sheath potential: φ(x) = V₀ (x/s)^(4/3), x from the sheath edge
Ion born by charge exchange at x arrives with E = V₀ [1 − (x/s)^(4/3)]

For births spread uniformly through the sheath:
  mean energy of collisional ions = V₀ (1 − 3/7) = 0.57 V₀
  fraction of collisional ions below 2 keV at V₀ = 5.5 kV:
    (x/s)^(4/3) > 1 − 2/5.5 = 0.636 → x/s > 0.71 → 29%

R1: collisional share ≈ 45% (Chapter 3) → 0.45 × 0.29 ≈ 13% of all ions
    below 2 keV; transition-phase ions add ≈ 1–2%
    Births are not quite uniform (fewer near the wafer, where ions are
    fast and σ_cx smaller), so the reference value is ≈ 10–15%;
    Chapter 3 uses 10%
```

The tailored waveform halves or thirds the low-energy fraction, from about 31% to about 10–15%. The rest is collisional, and only lower pressure removes it. **At 91:1 the waveform and the pressure are two halves of the same control.**

### 6.2.4 Mean Energy

```
R1 with V₀ ≈ 5.5 kV:
  narrow population (55%) at ≈ 5.3 keV (droop and transition)
  collisional population (45%) at ≈ 0.57 × 5.5 = 3.1 keV mean
  mean ≈ 0.55 × 5.3 + 0.45 × 3.1 = 4.3–4.5 keV
```

---

## 6.3 Bias Pulsing and Charge Relief

### 6.3.1 The Problem

The bottom of the hole charges positive because ions arrive and electrons do not (Chapter 3). The positive excursion of a tailored waveform admits electrons to the wafer surface, but they are still nearly isotropic and still cannot reach the bottom of a 91:1 hole. Something anisotropic and negative must go down the hole.

### 6.3.2 Pulsing

```
Bias pulsing: the bias waveform is switched on and off at f_p = 1–10 kHz
with duty cycle D (on fraction).

R1 (illustrative): f_p = 5 kHz (period 200 µs), D = 0.85 → off for 30 µs
Source power is pulsed synchronously or kept on at reduced level.
```

In the off phase the sheath collapses to the floating potential (tens of volts). If the source is also turned off, electrons cool and attach to electronegative species, and the plasma becomes an ion–ion plasma of positive and negative ions within 10–30 µs. A small positive bias in the late off phase then accelerates negative ions (F⁻, CF₃⁻) toward the wafer with an anisotropic distribution. Unlike electrons, they can reach the bottom of the hole.

### 6.3.3 How Much Charge Relief

```
Bottom charge brought by ions during the on phase (per unit area of hole
bottom): Q_on = J_i,bottom × D/f_p ≈ 0.6 mA/cm² × 170 µs
              ≈ 1.0×10⁻⁷ C/cm² per pulse

Wall capacitance of the lower hole (to the surrounding oxide, illustrative):
  ≈ 2×10⁻⁷ F/cm² of bottom area → ΔV ≈ 0.5 V per pulse if nothing relieves it
  (charging accumulates over many pulses until leakage balances)

Neutralization in the off phase needs a comparable negative charge:
  negative-ion flux ≈ 0.05–0.1 mA/cm² reaching the bottom for ≈ 15 µs
  → 0.75–1.5×10⁻⁹ C/cm² per pulse
```

The negative charge delivered per pulse is about 1% of the positive charge brought by the ions. Pulsing therefore does not neutralize the hole each pulse. What it does is shift the steady-state balance: the bottom potential settles where leakage, secondary electrons, and the off-phase negative flux together balance the ion current. Measured and modelled bottom potentials fall from 200–400 V under continuous bias to 30–80 V under well-tuned pulsing (Chapter 3). The wall charge, with a relaxation time of 1–3 ms, is smoothed over ten or more pulses.

### 6.3.4 The Cost

```
Average etch rate ∝ D (to first order): D = 0.85 → 15% longer etch
Partly recovered because the bottom rate falls less with depth (lower
effective k) and fewer holes stop:
  R1 with CW bias (illustrative): ER₀ ≈ 820, k ≈ 0.025 → t(2100) = 5.48 min
  R1 pulsed at D = 0.85:          ER₀ ≈ 700, k ≈ 0.016 → t(2100) = 5.19 min
```

At 91:1 the pulsed recipe is faster to full depth than the continuous one, even though its open-area rate is 15% lower. At 57:1 the same comparison favours continuous bias. **Pulsing pays for itself only above roughly 70:1**, which is why it became standard in capacitor etch at the 1c generation.

---

## 6.4 DC Superposition and the Electron Beam

### 6.4.1 How It Works

A negative DC voltage of 300–1500 V is applied to the silicon upper electrode, on top of its RF. Ions striking the electrode at that voltage release secondary electrons, which are accelerated through the upper sheath and cross the plasma almost without collisions. They arrive at the wafer as a beam of electrons with several hundred eV to over 1 keV and a narrow angular spread, during the part of the cycle when the wafer sheath is collapsed or thin.

```
Upper electrode area ≈ 1.5× wafer area; ion current density there ≈ 0.5 mA/cm²
Secondary electron yield at 1 kV on Si: γ ≈ 0.1
Beam current density reaching the wafer: ≈ 0.1 × 0.5 × 1.5 ≈ 0.07 mA/cm²
Fraction admitted during sheath collapse (≈ 8% of the period): ≈ 0.006 mA/cm²
```

Even this small anisotropic current reaches the bottom of the hole with high transmission and carries several times the negative charge per period that the off-phase negative ions carry. It is one of the most effective ways known to lower the bottom potential.

### 6.4.2 Side Effects

1. **Silicon sputtering.** The upper electrode is sputtered faster. Silicon scavenges fluorine in the gas phase, which raises the polymerization index. The O₂ flow is raised to compensate.
2. **Electrode life.** Consumption rises roughly in proportion to the DC voltage (Chapter 9).
3. **Hot spots.** The beam is not perfectly uniform; its pattern follows the electrode gas holes and its edge.

---

## 6.5 Voltage Limits and Arcing

### 6.5.1 Limits

```
Limits on the bias voltage (illustrative, 1d-class chamber):

  Limit                                    Approx. V_pp limit
  ───────────────────────────────────────────────────────────
  Chuck dielectric strength (0.5–1 mm)     12–15 kV
  Helium-hole breakdown (Paschen)          set by design; arcs at a few
                                           hundred V of local mismatch
  Edge-ring to wafer potential             ≈ 1–2 kV difference
  RF feed and match components             15–20 kV
  Wafer bevel and backside films           arcs if conductive residues
```

The practical limit in production is near V_pp ≈ 12 kV. R1 runs at 10 kV. The 1e generation, which needs about 5.5 keV mean energy, runs close to the limit, and its chucks are being redesigned with thicker, layered dielectrics and edge electrodes.

### 6.5.2 Arcs

An arc on the wafer releases the energy stored in the sheath and the RF path in microseconds. It melts a spot of mask and mold a few tens of micrometres across, removes or damages thousands of holes, and throws particles. Arc detection watches the bias voltage and current for transients faster than about 1 µs and shuts the generator off within a few microseconds.

```
Stored energy, wafer sheath + chuck at 10 kV:
  C ≈ 1.74×10⁻¹¹ F/cm² × 707 cm² ≈ 12 nF → E = ½ C V² ≈ 0.6 J
  Energy in a local arc (few % of the area) ≈ tens of mJ → enough to
  vaporize ≈ 10⁻⁵ cm³ of oxide
```

Arc rates must be below about one per thousand wafers. Chapter 9 treats arcs as a defect source.

---

## 6.6 The Waveform Step by Step

```
Bias settings by recipe step (R1, illustrative):

  Step               V_pp      Waveform       Pulsing         DC (upper)
  ────────────────────────────────────────────────────────────────────────
  1 Top SiN          7 kV      tailored       CW              −300 V
  2 ME1 (upper ox)   9 kV      tailored       5 kHz, D 0.90   −500 V
  3 Middle SiN       8 kV      tailored       5 kHz, D 0.90   −500 V
  4 ME2 (lower ox)   10 kV     tailored       5 kHz, D 0.85   −800 V
                     (ramped from 9.5 to 10.5 with depth, Chapter 8)
  5 Overetch         10 kV     tailored       5 kHz, D 0.80   −800 V
  6 Bottom open      3 kV      sine           CW              −300 V
```

The bias rises as the hole deepens, the duty falls, and the DC rises, because the charging problem grows with depth. The bottom-open step drops the energy to about 1.5 keV to limit the gouge into the W pad (Chapter 12).

---

## Summary and Key Takeaways

1. **A sine sends a third of the ions below 2 keV.** At 4.5 keV mean, 31% of the ions arrive below 2 keV and 15% below 0.5 keV.

2. **A tailored waveform narrows the IED.** Holding the wafer at −V₀ for 92% of the period puts most uncollided ions within about 3% of V₀; the droop is about 66 V/µs.

3. **Collisions set the floor.** About 13% of R1's ions arrive below 2 keV because of charge exchange in the sheath; only lower pressure removes them.

4. **Pulsing shifts the charge balance.** It does not neutralize the hole each pulse, but lowers the steady bottom potential from 200–400 V to 30–80 V. Above about 70:1 it shortens the etch to full depth.

5. **DC superposition sends electrons down the hole.** A small anisotropic electron beam from the upper electrode is among the most effective charge-relief methods, at a cost in electrode life and polymer balance.

6. **The voltage is near its limit.** Production chucks hold about 12 kV peak to peak; R1 runs at 10 kV.

---

## Study Questions

1. For a sinusoidal bias with V_rf = 5.5 kV, compute the fraction of ions below 1, 2, and 3 keV. Compare with the tailored waveform at the same peak.

2. A chuck dielectric is thickened from 0.5 to 0.8 mm. Compute the new droop over a 2.3 µs negative phase at 1.15 mA/cm². What compensating ramp would be needed?

3. The pressure is lowered so that the collisional share falls from 45% to 35%. With V₀ = 5.5 kV, how does the fraction of ions below 2 keV change?

4. Using the illustrative CW and pulsed parameters, compute t(1600) for both at w = 28 nm. At which depth do the two curves cross?

5. A DC superposition of −1200 V raises the electrode consumption by 40% and the beam current by 30%. Discuss whether you would use it in step 4 only or in steps 2–5.

---

**Next Chapter:** [Chapter 7: Cryogenic & Low-Temperature Etch](./07-cryogenic-low-temperature-etch.md)

---

**Chapter 6 Development Status:** Complete  
**Version:** 1.0
