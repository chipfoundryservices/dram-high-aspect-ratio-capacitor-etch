# Appendix A: Material Properties

Properties of the mold, mask, pad, electrode, dielectric, and chamber materials used in this book, with physical constants. Values are representative; film properties depend on deposition conditions and should be measured for each process.

---

## A.1 Mold Materials

```
Material             Density     Molecular density   Young's mod.  Stress (as dep.)  Plasma rate   HF wet rate
                     (g/cm³)     (cm⁻³)              (GPa)         (MPa)             (rel. TEOS)   (rel. TEOS)
──────────────────────────────────────────────────────────────────────────────────────────────────────────
TEOS oxide (PECVD)   2.20        2.21×10²² SiO₂      ≈ 70          −100 to −200       1.00 (R1)     1
                                                                                      1.00 (R2)
BPSG (4B/4P wt%)     2.25        ≈ 2.2×10²² SiO₂-eq  ≈ 60          ≈ 0 after reflow   1.17 (R1)     3–6
                                                                                      1.25 (R2)
Thermal SiO₂ (ref.)  2.27        2.27×10²² SiO₂      ≈ 72          −300               0.95          0.7
SiN support (PECVD   2.6–2.9     ≈ 4×10²² atoms      ≈ 200         −300 to +800       0.70 support  < 0.05
 or LPCVD)                                                          (recipe)           step (R1);
                                                                                      ≈ 0.85–0.9 (R2)
```

The reference uses the TEOS molecular density 2.27×10²² cm⁻³ from Book #29 for flux arithmetic (Chapter 3); the 3% difference from PECVD TEOS is within the uncertainty of the yields.

---

## A.2 Mask Materials

```
Material                Density    Stress        Blanket sel.   Eff. sel.     Strip
                        (g/cm³)    (MPa)         to oxide (R1)  (R1 / R2)
──────────────────────────────────────────────────────────────────────────────────────
Undoped ACL (PECVD)     1.8–1.9    −100 to −300   5.5           2.3 / 3.5     O₂ ash
B-doped carbon          2.0–2.2    −200 to −400   8             3.5 / 5.0     O₂ ash + wet
 (30–50 at% B)                                                                (B₂O₃)
W-doped carbon          2.6–3.2    −300 to −600   11            4.8 / ≈ 6     ash + W wet
 (≈ 10 at% W)
SiON cap                2.2–2.4    −200           —             —             removed in
                                                                              mask open
Metal-oxide masks       5–7        ± 500          15–20         6–8           wet
```

---

## A.3 Pad, Electrode, and Dielectric

```
Material             Property                                   Value
──────────────────────────────────────────────────────────────────────────────
W (landing pad)      Resistivity (thin film)                    10–15 µΩ·cm
                     Etch in BO (SiN : W ≈ 6)                   ≈ 7.5 nm/min
                     WF₆ boiling point                          17 °C
TiN (ALD electrode)  Young's modulus                            250–400 GPa (300 used)
                     Resistivity                                 100–200 µΩ·cm
                     Density                                     5.0–5.4 g/cm³
ZrO₂/Al₂O₃/ZrO₂      Effective k                                ≈ 35
 dielectric          EOT (reference)                            0.50 nm
                     Physical thickness at EOT 0.50              ≈ 4.5 nm
                     Leakage limit (Chapter 1)                  ≈ 7×10⁻⁷ A/cm² at ±0.5 V, 85 °C
Al₂O₃ (R2 stop)      Fluoride (AlF₃) volatility                 non-volatile (stop)
```

---

## A.4 Chamber Materials

```
Part                  Material                       Notes
──────────────────────────────────────────────────────────────────────────────────
Upper electrode       Si (single- or polycrystal)    ≈ 3 µm/RF h erosion (R1 + DC);
                                                     ≈ 2.4 mm usable
Focus ring            SiC (or Si)                    ≈ 1.5 µm/RF h; 1.2 mm lift range
Walls, liner          Y₂O₃ / YOF coatings            fluorinate to YOF; low particle
Chuck dielectric      Al₂O₃ or AlN, 0.5–1 mm         ε_r ≈ 9.8 (Al₂O₃); 15–20 kV/mm DC
                                                     strength; Coulombic for cryo
Helium plugs          Porous ceramic                 arc suppression
Confinement rings     Si, SiC, quartz
```

---

## A.5 Thermal Properties for the Chuck

```
Si wafer (300 mm, 775 µm): mass ≈ 128 g; c_p ≈ 0.70 J/g·K (300 K),
  ≈ 0.60 J/g·K (210 K) → heat capacity ≈ 77–90 J/K
Helium gap conductance (few µm gap): ≈ 0.25 W/cm²K at 20 Torr;
  ≈ 0.40 W/cm²K at 40 Torr (transition regime; illustrative)
Wafer thermal time constant on the chuck: C / (h A) ≈ 83 / (0.40 × 707) ≈ 0.3 s
```

---

## A.6 Liquids for Clean and Dry

```
Liquid        Surface tension (N/m, 25 °C)   Used for
──────────────────────────────────────────────────────────
Water         0.072                          rinse
IPA           0.022                          final rinse before dry
HFE fluids    0.012–0.016                    low-tension drying (option)
CO₂ (sc)      0 (supercritical)              capillary-free drying
```

---

## A.7 Constants

```
ε₀            8.854×10⁻¹² F/m
ε₀ × 3.9      3.453×10⁻¹¹ F/m (SiO₂-equivalent permittivity)
e             1.602×10⁻¹⁹ C
k_B           1.381×10⁻²³ J/K = 8.617×10⁻⁵ eV/K
m(Ar)         6.63×10⁻²⁶ kg (39.95 u)
1 sccm        4.48×10¹⁷ molecules/s = 0.01267 Torr·L/s
1 mTorr       0.1333 Pa
Ar⁺/Ar charge-exchange cross section at keV: ≈ 3×10⁻¹⁹ m²
```

---

**Appendix A Version:** 1.0
