# Chapter 7: Cryogenic & Low-Temperature Etch

## Overview

Fluorocarbon chemistry has built every DRAM capacitor so far. Its strength is the polymer it deposits, which protects the mask and the sidewall. Its weakness at extreme aspect ratio is the same polymer: it starves the bottom, raises the effective ARDE coefficient, and charges the walls unevenly. Cryogenic etch takes a different route. At wafer temperatures between −40 and −80 °C, hydrogen fluoride and water adsorb on the oxide surface in quantity, and ions drive the adsorbed layer into volatile products. The etch is faster, the ARDE coefficient lower, the mask selectivity higher, and twist smaller. The cost is a chuck that must hold −60 °C under 5 kW of heat, a chamber that must handle HF, and new residues.

This chapter explains the adsorption-controlled mechanism, the hardware it needs, its effect on profile and selectivity, and the conditions under which R2 is the better choice.

**Learning Objectives:**
- Explain why the oxide etch rate in HF-based plasma rises as the wafer cools
- Estimate the increase in surface coverage from Langmuir adsorption
- Explain why adsorption lowers the ARDE coefficient
- Compute the heat balance of a cryogenic chuck under the R2 load
- Identify the hardware and residue problems of cryogenic operation
- Compare R1 and R2 across time, profile, placement, mask, and cost

---

## 7.1 The Mechanism

### 7.1.1 An Etch That Speeds Up When Cold

In almost every plasma etch, cooling the wafer slows the reaction. In HF-based oxide etch, the rate rises as the wafer cools from room temperature to about −60 °C and then falls again at still lower temperature. The reason is adsorption. The etch is ion-driven, but each ion can only remove the molecules that the surface has supplied with fluorine. At room temperature the surface coverage of HF is low; at −60 °C it is high.

```
Overall surface reaction (catalyzed by adsorbed water):
  SiO₂ + 4 HF(ads) → SiF₄(g) + 2 H₂O(ads)
  The product water helps adsorb more HF, so the layer is self-sustaining
  as long as the temperature holds it on the surface and the ions keep
  it reacting.
```

### 7.1.2 Coverage

```
Langmuir coverage: θ = K p / (1 + K p),  K ∝ exp(E_ads / k_B T)

Ratio of K at −60 °C (213 K) to +10 °C (283 K), E_ads ≈ 0.4 eV (illustrative):
  E_ads / k_B = 0.4 / 8.617×10⁻⁵ = 4640 K
  (1/213 − 1/283) = 1.161×10⁻³ K⁻¹
  K ratio = exp(4640 × 1.161×10⁻³) = exp(5.39) ≈ 220
```

A coverage that is 1% at +10 °C becomes about 70% at −60 °C at the same pressure. The yield per ion rises with it:

```
R2 open-area rate ER₀ = 1100 nm/min → removal flux 4.2×10¹⁶ SiO₂ cm⁻² s⁻¹
At the same ion flux as R1 (7.2×10¹⁵ cm⁻² s⁻¹): Y ≈ 5.8 SiO₂ per ion
(R1: 3.7)
```

### 7.1.3 Why ARDE Is Lower

Chapter 4 showed that k = (3/4)χ, with χ the fraction of the reactive neutral supply the open surface consumes. In R2 the reactive species reach the bottom by two routes: down the hole as gas, and down the wall as an adsorbed layer that diffuses along the surface. HF also has a low reaction probability on the walls, which are not covered by thick polymer.

```
R2: k ≈ 0.010 (w = 23 nm), against 0.016 for R1
  χ ≈ 0.013: the open surface uses about 1.3% of the supply
  Bottom rate at 2100 nm: ER/ER₀ = 1/(1 + 0.010 × 91.3) = 0.52
```

### 7.1.4 Too Cold

Below about −80 °C, the adsorbed layer becomes so thick that ions spend their energy in it rather than at the oxide, and products such as SiF₄ and H₂O begin to remain on the surface. The rate falls and residues form. R2 operates at −60 °C, near the rate maximum with some margin against condensation.

---

## 7.2 Chemistry

### 7.2.1 R2 Gas

```
R2 main etch (illustrative):
  HF 200 sccm (or H₂ 150 + C₄F₈/CF₄ to form HF in the plasma)
  C₄F₈ 20 sccm      sidewall passivation, mask protection
  O₂ 10 sccm        controls carbon
  Ar 100 sccm       dilution
  Pressure 20 mTorr; wafer −60 °C; bias as R1 (10 kV tailored, pulsed)
```

### 7.2.2 Spontaneous Etch and the Chemical Bow

HF with water can etch oxide without ions. At −60 °C with abundant adsorbed water, the sidewall would etch laterally and the hole would bow chemically. R2 prevents this in three ways: the C₄F₈ deposits a thin passivating film on the walls; the water produced at the bottom is pumped out before it accumulates on the walls; and the HF partial pressure is kept below the threshold for a condensed liquid-like layer. If any of these fails, the result is a smooth, wide bow that differs from the sharp, ion-cut bow of R1 (Chapter 10).

### 7.2.3 Selectivity

```
                          R1 (+10 °C)     R2 (−60 °C)
  ─────────────────────────────────────────────────────
  Oxide : B-ACL (eff.)       3.5             5.0
  Oxide : SiN (main etch)    ≈ 6             1.1–1.2
  Oxide : SiN (overetch)     ≈ 15            ≈ 3 (most selective setting)
  BPSG : TEOS                1.17            1.25
  Bottom open, SiN : W       ≈ 6             ≈ 6
```

Carbon reacts slowly with HF at low temperature, and the reduced oxygen in R2 limits carbon oxidation, so mask selectivity rises. Silicon nitride etches at nearly the oxide rate, which makes the supports easy to cut but the bottom stop a weaker stop.

### 7.2.4 Ammonium Salts

HF and hydrogen react with silicon nitride to form ammonium fluorosilicate, (NH₄)₂SiF₆, which is not volatile at −60 °C. It forms on the supports and on the bottom stop during R2.

```
(NH₄)₂SiF₆ sublimation: significant above ≈ 100 °C
Consequence: a post-etch warm-up (≈ 120 °C, 30–40 s) in the chamber's
  lift-pin station or the load lock removes it; without warm-up, salt
  residues block the TiN deposition at the bottom and appear as
  high-resistance contacts
```

---

## 7.3 The Cryogenic Chuck

### 7.3.1 Heat Balance

```
Heat into the wafer under R2: ≈ 5.0 kW → 7.1 W/cm² (Chapter 5)

Thermal path (illustrative), wafer to coolant:
  Helium gap (40 Torr, few µm; h ≈ 0.40 W/cm²K)   ΔT = 7.1 / 0.40 = 18 K
  Dielectric and bond layers                       ΔT ≈ 5 K
  Baseplate to coolant film                        ΔT ≈ 5 K
  ─────────────────────────────────────────────────────────────
  Total                                           ≈ 28 K

Wafer at −60 °C → coolant at ≈ −88 °C
(R1: wafer +10 °C, coolant ≈ −15 °C at the same load)
```

The coolant must run near −90 °C. Fluorinated heat-transfer fluids remain liquid there but grow viscous, and direct-expansion refrigerant loops are an alternative. The chiller power rises steeply: removing 5 kW at −90 °C takes several times the electrical power of removing it at −15 °C.

### 7.3.2 Zones and Uniformity

```
∂(ER₀)/∂T near −60 °C (illustrative): ≈ −0.8% per K (rate rises as T falls)
Uniformity target for ER₀: ±1% → ±1.2 K across the wafer
Helium gap variation of ±10% → ±1.8 K → zone control required
```

R2 is more temperature-sensitive than R1 in rate, because adsorption is exponential in 1/T. R1 is more temperature-sensitive in profile (Chapter 10). Both need four or more radial zones.

### 7.3.3 Chucking at Low Temperature

1. **Johnsen–Rahbek chucks fail cold.** Their clamping relies on a leakage current through a slightly conductive ceramic. At −60 °C the ceramic's resistivity rises by orders of magnitude, the current vanishes, and the clamping force falls. Cryogenic chucks are Coulombic, with higher clamping voltages.
2. **Thermal mismatch.** The bonded ceramic and metal layers cycle from about −90 to +25 °C at every maintenance. Bonding layers must tolerate the strain.
3. **Residual charge.** Dechucking a cold wafer is slower because surface leakage is lower.

### 7.3.4 Frost and Condensation

The cold chuck must never see room air or moisture. Transfer chambers are kept dry, and the wafer is cooled only after it is on the chuck in vacuum. After the etch, the wafer is warmed above the dew point and above the salt sublimation temperature before it leaves the vacuum. Chapter 5 counted 45 s for cooling and stabilization and 40 s for warm-up.

---

## 7.4 Profile and Placement Under R2

```
Comparison at 2.1 µm (illustrative, Chapters 10–12):

                                R1 (+10 °C)       R2 (−60 °C)
  ───────────────────────────────────────────────────────────────
  Etch to full depth            5.19 min          2.78 min
  k                             0.016             0.010
  ∂h/∂w at 2.1 µm               27.1 nm/nm        21.8 nm/nm
  Bottom rate / ER₀             0.41              0.52
  Bow CD                        27.5 nm           26.8 nm
  Bow shape                     sharp, at 450 nm  broad, 300–900 nm
  Twist 3σ at bottom            4.5 nm            3.0 nm
  Bottom CD                     19 nm             20 nm
  Mask consumed (B-ACL)         600 nm            420 nm
  Bottom-stop margin            good              weaker (SiN ≈ oxide rate)
```

Twist is lower in R2 because the walls carry a thin adsorbed layer of HF and water whose surface conductivity is far higher than that of fluorocarbon polymer. Asymmetric charge leaks away before it deflects ions. The bottom CD is larger because there is less carbon polymer at the bottom to taper the hole.

---

## 7.5 When Cryogenic Etch Wins

### 7.5.1 Cost Factors

```
Per-wafer differences, R2 against R1 (illustrative):

  Factor                         Effect
  ─────────────────────────────────────────────────────────────────
  Chamber time                    5.8 min vs 7.7 min → −25% chambers
  Chiller energy                  +3–4 kW average per chamber
  Gas cost                        HF supply, abatement, safety systems
  Consumables                     similar; electrode wear per wafer lower
                                  (shorter RF time)
  Chuck cost and life             higher; cycling fatigue
  Yield                           lower twist → fewer misplaced contacts;
                                  salt residue risk if warm-up fails
  PFC emissions                   lower (less C₄F₆/C₄F₈ per wafer)
```

### 7.5.2 Decision

At 57:1 (1b) the cryogenic etch was already about twice as fast (Book #29: 1.95 against 4.19 min), but the fluorocarbon twist and mask were comfortably within budget, and the capital and safety cost of cryogenic chambers was hard to justify. At 91:1 R2 is still nearly twice as fast (2.78 against 5.19 min), and now the R1 twist consumes almost half the placement budget and the R1 mask has only about 20% depth headroom. At 112:1 (1e), R1 runs out of mask (Chapter 4). **Cryogenic etch becomes the better choice between 1c and 1d, and the necessary one at 1e unless a two-tier mold is chosen instead.**

---

## Summary and Key Takeaways

1. **Adsorption drives the rate.** At −60 °C the HF coverage is roughly 200 times higher than at +10 °C, and the yield per ion rises from about 3.7 to 5.8.

2. **ARDE falls because the supply rises.** Adsorbed HF reaches the bottom along the wall as well as through the gas; k falls from 0.016 to 0.010.

3. **The chuck must remove 7 W/cm² at −60 °C.** The coolant runs near −90 °C; Johnsen–Rahbek clamping fails cold, so Coulombic chucks are used.

4. **Salts and water are the new defects.** Ammonium fluorosilicate must be sublimed above 100 °C, and water must not condense on the walls.

5. **Twist falls by a third.** A conductive adsorbed wall layer bleeds asymmetric charge.

6. **Cryogenic etch wins at 1d and beyond.** It nearly halves the etch time and keeps the mask budget open for the next generation.

---

## Study Questions

1. Compute the Langmuir K ratio between −40 and +10 °C, and between −80 and +10 °C, for E_ads = 0.4 eV. Why does the rate nonetheless fall below about −80 °C?

2. With R2's ER₀ and k, compute t(2350) for a 21 nm hole. Compare with R1 at the same geometry.

3. The helium conductance falls to 0.30 W/cm²K at one zone because of a worn chuck surface. What is the wafer temperature there with the coolant at −88 °C, and what is the local change in ER₀?

4. A warm-up step is shortened from 40 to 20 s, leaving salt residue on 10⁻⁷ of holes. Using the not-open budget of Chapter 1, is this acceptable?

5. Estimate the chamber count for 100,000 wafers per month with R2 if the warm-up is moved to a separate station, shortening the chamber cycle by 40 s.

---

**Next Chapter:** [Chapter 8: Depth-Adaptive Recipes, Gas Pulsing & Cyclic Etch](./08-depth-adaptive-cyclic-recipes.md)

---

**Chapter 7 Development Status:** Complete  
**Version:** 1.0
