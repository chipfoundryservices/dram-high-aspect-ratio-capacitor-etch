# Chapter 3: Ion Transport & Charging at Extreme Aspect Ratio

## Overview

In Book #29 the energetic ions spread by about 0.3–0.6° and the finished hole accepted about 0.7°. The two numbers were comparable, and specular reflection off the walls carried the difference. In the reference hole of this book, with its mask, the acceptance falls to 0.45° edge to edge and 0.22° from the centre. The sheath must deliver ions that are both more energetic and more parallel, and the walls must reflect more of them more often. Where they do not, ions strike the wall and build the bow, or are deflected by charge and build the twist.

This chapter follows the ions: their energy and angle at the wafer, the acceptance cone of the hole and how it closes with depth, the fraction of ions that reach the bottom directly and by reflection, the energy they carry, and the charging that bends them. It ends with a table of how each quantity scales from 57:1 to beyond 120:1.

**Learning Objectives:**
- Estimate ion flux, ion power, and the ion energy distribution for R1
- Compute the collisionless and collisional angular spread at 15 mTorr
- Compute the acceptance cone through the mask and mold at any depth
- Use a Monte Carlo transport result to estimate the ion flux at the bottom
- Explain the ion funnel and the role of specular reflection
- Estimate bottom charging and lateral deflection, and how they scale with depth

---

## 3.1 Ion Flux and Power

### 3.1.1 What the Etch Needs

```
Reference open-area TEOS rate (R1): ER₀ = 700 nm/min = 11.7 nm/s
Removal flux: 11.7×10⁻⁷ cm/s × 2.27×10²² cm⁻³ = 2.65×10¹⁶ SiO₂ cm⁻² s⁻¹

Ion-driven fluorocarbon etch yield, rising roughly as √E:
  Y(3.0 keV) ≈ 3.0 (Book #29) → Y(4.5 keV) ≈ 3.0 × √1.5 = 3.7 SiO₂/ion
Ion flux needed: 2.65×10¹⁶ / 3.7 = 7.2×10¹⁵ cm⁻² s⁻¹ → J_i ≈ 1.15 mA/cm²
```

The ion flux is nearly the same as in Book #29. The extra rate comes from the extra energy per ion.

### 3.1.2 Ion Power

```
Ion power density: 1.15×10⁻³ A/cm² × 4500 V = 5.2 W/cm²
Over 707 cm²: 3.7 kW into the wafer from ions alone (2.5 kW in Book #29)
```

Chapter 7 shows how a cryogenic chuck must remove this heat plus about 1 kW of other loads while holding the wafer at −60 °C.

---

## 3.2 Ion Energy and Angle

### 3.2.1 The Sheath Under a Tailored Waveform

R1 drives the wafer with a tailored 400 kHz waveform rather than a sine (Chapter 6). The waveform holds the sheath near its maximum voltage for most of each period and collapses it briefly to admit electrons.

```
Reference sheath (illustrative):
  V_pp ≈ 10 kV, DC self-bias ≈ −4.8 kV
  Sinusoidal 400 kHz at the same mean: bimodal IED, low peak ≈ 0.5 keV,
    high peak ≈ 8 keV; ≈ 30% of ions below 2 keV
  Tailored waveform: dominant peak ≈ 5.5 keV; ≈ 10% of ions below 2 keV;
    mean ⟨E_i⟩ ≈ 4.5 keV
```

The low-energy ions matter far more at 91:1 than their numbers suggest. They are deflected more by charge (θ ∝ 1/E_i), and they strike the upper walls. Removing most of them is the chief reason for the tailored waveform.

### 3.2.2 Angular Spread

```
Collisionless:  θ ≈ √(T_i⊥ / E_i), T_i⊥ ≈ 0.05 eV
  E_i = 4500 eV: θ ≈ √(1.1×10⁻⁵) = 3.3×10⁻³ rad = 0.19°

Collisions at 15 mTorr (Ar-dominated, 300 K):
  n = 2.0 Pa / (1.38×10⁻²³ × 300) = 4.8×10²⁰ m⁻³
  σ_cx ≈ 3×10⁻¹⁹ m² → λ_cx = 1/(nσ) = 6.9 mm
  Sheath thickness (Child law, n_e ≈ 3×10¹⁶ m⁻³, ≈ 8 kV): s ≈ 4.0 mm
  s/λ ≈ 0.59 → collisionless fraction exp(−0.59) ≈ 0.55
```

The ion flux arrives as two populations:

```
  Population      Share   Energy           Angular spread (σ per axis)
  ────────────────────────────────────────────────────────────────────
  Narrow          ≈ 55%   ≈ 5–5.5 keV      ≈ 0.2°
  Broad           ≈ 45%   0.2–4 keV        ≈ 2°
```

Lowering the pressure from Book #29's 20 mTorr to 15 mTorr raised the narrow share from about 45% to about 55%. That ten-point gain is worth more at 91:1 than any increase in power, because only the narrow population reaches the bottom.

---

## 3.3 The Acceptance Cone

### 3.3.1 Total Height

Ions see the mask and the mold together:

```
h_tot = h_mask(t) + h(t)

  Point in the etch              h_mask   h      h_tot   w     Edge-to-edge   From centre
                                 (nm)     (nm)   (nm)    (nm)  arctan(w/h)    arctan(w/2h)
  ─────────────────────────────────────────────────────────────────────────────────────────
  Start of main etch             1450        0   1450    26    1.03°          0.51°
  Middle support (Book #29 depth) 1200     900   2100    24    0.65°          0.33°
  Two-thirds depth               1100     1400   2500    23    0.53°          0.26°
  Bottom stop                     850     2080   2930    23    0.45°          0.22°
  Book #29 at its stop (reference) 730    1600   2330    28    0.69°          0.34°
```

The cone at the end of the R1 etch is two-thirds of Book #29's. The narrow population, at σ ≈ 0.2° per axis, has an RMS polar angle of about 0.28°, already larger than the half-cone from the centre.

### 3.3.2 The Ion Funnel

Most ions that reach the bottom of a 91:1 hole do so after one or more grazing reflections from the wall. At kiloelectronvolt energies and incidence angles of a fraction of a degree to the surface, an ion reflects almost specularly and keeps most of its energy. The wall acts as a funnel that guides the ion down.

The funnel works only if the wall is smooth and straight. A bow, a step at a support interface, a striation, or a polymer bump changes the local wall angle by more than the ion's grazing angle. The ion then strikes at a steep angle and is lost, or is reflected across the hole into the opposite wall. Chapter 10 shows how this builds the bow.

---

## 3.4 Ion Flux at the Bottom

### 3.4.1 A Monte Carlo Estimate

The ion transmission of a cylinder with specularly reflecting walls is straightforward to compute by Monte Carlo. The model used here (illustrative, Appendix E.4) launches ions uniformly over the opening with Gaussian angles, reflects them specularly at the wall with a probability that falls with angle, R(θ) = 0.97 exp(−θ/2°), and counts arrivals at the bottom.

```
Ion fraction reaching the bottom, Γ_i,bot / Γ_i,top (illustrative):

  Total A    Narrow (σ 0.2°)        Broad (σ 2°)          Mixed
  (h_tot/w)  direct  incl. refl.    direct  incl. refl.   0.55N + 0.45B
  ──────────────────────────────────────────────────────────────────────
     20      0.89     0.98          0.20     0.39          0.72
     40      0.78     0.96          0.06     0.23          0.63
     57      0.69     0.95          0.03     0.18          0.60
     91      0.52     0.91          0.01     0.11          0.55
    128      0.37     0.88          0.006    0.08          0.52
    150      0.31     0.87          0.005    0.07          0.51
```

### 3.4.2 Reading the Table

1. **The broad population is lost high in the hole.** At the end of the R1 etch, only 8% of the broad ions reach the bottom. The other 92% strike the upper walls. Their energy goes into the bow and into wall charging.
2. **The narrow population mostly survives.** 88% of narrow ions reach the bottom at A_tot = 128, but only 37% directly. The rest arrive by reflection. Without specular reflection, the bottom would receive a third of the ions it does.
3. **The ion flux falls slowly.** From the 1b hole at its stop (A_tot = 83) to the 1d hole at its stop (A_tot = 128) the mixed ion fraction falls from 0.56 to 0.52, only 7%. The etch rate at the bottom falls far more (Chapter 4). **Ion transport alone does not explain ARDE at extreme aspect ratio.** The neutrals and the polymer balance at the bottom do.

### 3.4.3 Energy at the Bottom

```
Energy retained per grazing reflection: ≈ 97% (illustrative)
Mean reflections for narrow ions reaching the bottom at A_tot = 128: ≈ 1–2
Mean energy of narrow ions at the bottom: ≈ 0.96 × 5.3 keV ≈ 5.1 keV
```

The bottom receives about 52% of the incident ion flux, at about 5 keV. The ion energy flux at the bottom is about 2.7 W/cm², enough to etch oxide quickly if the surface chemistry allows.

### 3.4.4 The Sensitivity to Angle

```
Narrow population at A_tot = 128 (Monte Carlo, angle-dependent R):

  σ per axis    Direct    Including reflection
  ──────────────────────────────────────────────
  0.15°          0.50          0.93
  0.20°          0.38          0.88
  0.25°          0.28          0.83
  0.35°          0.17          0.73
```

The direct fraction is very sensitive to angle: it falls threefold from 0.15° to 0.35°. The total, carried by reflection, falls by only a fifth, as long as the wall reflects. This is why the bottom rate depends so strongly on the wall shape and so weakly on the bias power once the narrow population is well formed.

---

## 3.5 Charging

### 3.5.1 Electron Shading at 91:1

Electrons reach the wafer during the brief collapse of the sheath, with a nearly isotropic distribution and a few electronvolts of energy. The fraction of an isotropic flux that reaches the bottom of a tube directly falls roughly as (w/2h)²:

```
Direct isotropic transmission to the bottom (order of magnitude):
  A = 57:  (1/114)² ≈ 8×10⁻⁵
  A = 91:  (1/182)² ≈ 3×10⁻⁵
  A = 128: (1/256)² ≈ 1.5×10⁻⁵
```

Effectively no electrons reach the bottom of the hole. The upper walls charge negative, the bottom positive. The bottom potential rises until leakage along the wall and through the polymer, secondary electrons, and the few electrons that arrive balance the ion current.

```
Illustrative bottom potentials (oxide hole, landing on nitride over W):
  Sinusoidal CW bias, A = 57 (Book #29):        100–300 V
  Sinusoidal CW bias, A = 91:                   200–400 V
  Tailored waveform, pulsed with off-phase
  electron/negative-ion injection, A = 91:      30–80 V
```

### 3.5.2 Deflection and Its Scaling

```
Lateral deflection angle for an ion of energy E_i passing a length L of
lateral field E⊥ = ΔV/w:
  θ ≈ E⊥ L / (2 E_i)

Like-for-like with Book #29 (ΔV = 2 V across the hole, L = 200 nm):
  Book #29: w = 28, E_i = 3000 eV: θ = (2/28×10⁻⁹)(2×10⁻⁷)/(6000) = 2.4×10⁻³ rad = 0.14°
  R1:       w = 23, E_i = 4500 eV: θ = (2/23×10⁻⁹)(2×10⁻⁷)/(9000) = 1.9×10⁻³ rad = 0.11°

Lateral shift over the remaining depth below the deflection:
  Book #29: 800 nm × tan 0.14° = 1.9 nm
  R1:      1000 nm × tan 0.11° = 1.9 nm
```

The higher ion energy cancels the narrower hole and the longer lever arm, but only just. For the low-energy tail the picture is worse:

```
Ion at 500 eV in the same field:  θ = 0.11° × 4500/500 = 1.0°
→ strikes the wall within ≈ 23 nm / tan 1.0° ≈ 1.3 µm of travel,
  i.e., never reaches the bottom from mid-depth
```

### 3.5.3 Why Charging Grows with Depth

Three factors make charging worse as the hole deepens:

1. **More wall to charge.** The charged wall area grows with depth. Small asymmetries in polymer thickness or wall conductivity have more length over which to act.
2. **A longer lever arm.** A deflection at mid-depth moves the bottom by θ × (H − z). At 2.1 µm the lever arm is 30% longer than at 1.6 µm.
3. **Less neutralization.** Fewer electrons and negative ions reach the lower walls, so charge relaxes more slowly. Chapter 6 estimates the wall time constant at about 1–3 ms, longer than any pulse period.

Twisting (Chapter 11) is the visible result.

### 3.5.4 Charge Relief

```
  Method                                       Effect at A = 91
  ─────────────────────────────────────────────────────────────────────
  Tailored waveform (fewer low-E ions)         removes most of the ions that
                                               deflect strongly
  Bias pulsing (5–20% off duty, 1–10 kHz)      lets electrons and negative ions
                                               partially neutralize the walls
  DC superposition on the upper electrode      adds energetic secondary
                                               electrons that reach deeper
  Slightly conductive sidewall polymer         bleeds asymmetric charge
  Cryogenic HF chemistry (Chapter 7)           thinner, more conductive
                                               adsorbed film on the walls
```

---

## 3.6 Scaling Summary

```
Ion-side quantities against aspect ratio (illustrative, R1 conditions):

  Quantity                         A = 57    A = 73    A = 91    A = 112
                                   (1b)      (1c)      (1d)      (1e)
  ──────────────────────────────────────────────────────────────────────
  Mold height (µm)                 1.60      1.85      2.10      2.35
  h_tot at stop (µm)               2.33      2.65      2.93      3.25
  Edge-to-edge cone (°)            0.69      0.55      0.45      0.37
  Total A_tot = h_tot / w at stop   83        104       128       155
  Narrow ions at bottom            0.92      0.90      0.88      0.86
  Broad ions at bottom             0.12      0.10      0.08      0.07
  Mixed bottom ion fraction        0.56      0.54      0.52      0.50
  Bottom potential, CW (V)         ≈ 200     ≈ 250     ≈ 300     ≈ 350
  Mean ion energy (keV)            3.0       3.75      4.5       5.5
  Lateral shift per 2 V asym. (nm) 1.9       1.9       1.9       1.9
```

The ion side degrades slowly as long as the narrow population and the reflecting wall are maintained. Each generation must raise the ion energy to keep deflection constant. The limits come from elsewhere: the neutrals and the polymer at the bottom (Chapter 4), the mask (Chapters 2 and 13), and the twist (Chapter 11).

---

## Summary and Key Takeaways

1. **Same flux, more energy.** R1 uses about 1.15 mA/cm² of ions at 4.5 keV mean energy; 3.7 kW enters the wafer.

2. **Two populations.** About 55% of ions cross the sheath without collision and arrive within about 0.2°; the rest arrive broad and slower. Lowering the pressure raises the narrow share.

3. **The cone is 0.45°.** With the mask, the finished hole accepts ions within 0.45° edge to edge.

4. **Reflection carries the bottom.** About 88% of narrow ions reach the bottom at A_tot = 128, but only 37% directly. The broad population is almost entirely lost to the upper walls.

5. **Ions do not explain ARDE.** The bottom ion fraction falls only from 0.56 to 0.52 between the 1b and 1d holes at their stops. The rate falls further because of the neutrals and polymer.

6. **Charging is held constant only by more energy.** The lateral shift for a given asymmetry stays near 2 nm only because the ion energy rose from 3 to 4.5 keV. The low-energy tail must be removed.

---

## Study Questions

1. The pressure is lowered from 15 to 10 mTorr at the same sheath. Compute λ_cx and the collisionless fraction. Using the Monte Carlo table, estimate the change in the mixed bottom ion fraction at A_tot = 128.

2. Compute the edge-to-edge acceptance angle at the bottom stop if the mask is W-ACL and 1000 nm remains instead of 850 nm. Does a more selective mask open or close the cone?

3. An ion at 5.3 keV reflects twice on its way down, retaining 97% of its energy each time. What energy does it deliver, and by how much does Y(E) ∝ √E fall?

4. For a lateral asymmetry of 3 V acting over 300 nm at 1200 nm depth in a 23 nm hole, compute the bottom shift for 5.5 keV and for 1 keV ions.

5. Estimate the isotropic electron transmission to the bottom at A = 91 and explain why bias pulsing helps even though the off-phase electrons are still isotropic.

---

**Next Chapter:** [Chapter 4: Neutral Transport, Surface Kinetics & the Limits of ARDE](./04-neutral-transport-ardelimits.md)

---

**Chapter 3 Development Status:** Complete  
**Version:** 1.0
