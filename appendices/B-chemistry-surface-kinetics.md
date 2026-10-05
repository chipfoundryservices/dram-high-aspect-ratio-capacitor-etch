# Appendix B: Chemistry & Surface-Kinetics Data

Gases, radicals, surface reactions, sticking and reaction probabilities, cryogenic adsorption, product volatility, and optical emission lines for extreme-aspect-ratio capacitor etch. Values are representative and are used in the illustrative models of Chapters 3, 4, 7, and 12.

---

## B.1 Feed Gases

```
Gas      Role                                         R1 (sccm)       R2 (sccm)
────────────────────────────────────────────────────────────────────────────────
C₄F₆     Polymerizing; mask and sidewall protection   27–34           —
C₄F₈     CF₂ source; deeper-reaching precursors       10–15           20
CHF₃     Nitride and bottom-open steps                40–50 (steps)   as R1 (BO)
CH₂F₂    Support-step nitride rate                     15 (step 3)     —
CF₄      Top SiN step                                  40 (step 1)     —
O₂       Carbon control; polymerization index          28–38           10
NF₃      Extra F late in ME2                           0–8             —
Ar       Dilution; narrow ion population               200–300         100
HF       Adsorbed etchant (cryogenic)                  —               200
H₂       In-situ HF formation (alternative to HF)      —               0–150
```

---

## B.2 Sticking and Reaction Probabilities (Illustrative)

```
Species          β at the bottom (oxide,       s_w on polymer walls
                 ion-bombarded)                (R1, +10 °C)
─────────────────────────────────────────────────────────────────────
F                0.01                          ≈ 1×10⁻⁴
CF₂              0.05                          ≈ 5×10⁻³
CF, C₂Fₓ         0.2                           ≈ 0.05
O                0.05                          ≈ 1×10⁻³
HF (−60 °C)      0.005 (adsorbs reversibly)    low; surface diffusion
Large CₓFᵧ       0.3–0.5                       high (deposits near top)
```

Coburn–Winters bottom fractions at L/d = 128 (K = 0.0104): F 0.51, HF 0.68, CF₂ 0.17, O 0.17, CF 0.05 (Chapter 4).

---

## B.3 Surface Reactions

```
Fluorocarbon oxide etch (ion-assisted, through a thin CFₓ film):
  SiO₂ + CFₓ(film) + ion → SiF₄ + CO, CO₂, COF₂
  Each SiO₂ needs ≈ 4 F; releases 2 O (burns polymer)

Nitride:
  Si₃N₄ + F, CFₓ + ion → SiF₄ + N₂, FCN, NF₃ (traces)
  CN emission at 388 nm marks nitride

Cryogenic HF:
  SiO₂ + 4 HF(ads) → SiF₄ + 2 H₂O(ads)   (water-catalysed; ion-driven)
  Si₃N₄ + HF, H → (NH₄)₂SiF₆ (salt; sublimes > ≈ 100 °C)

Carbon mask:
  C + O → CO; C + F → CFₓ (slow); physical sputtering ∝ √E (facets)
  B in B-ACL: B + F → BF₃ (volatile) but B–C bonds raise the sputter threshold

Tungsten (bottom open):
  W + 6 F → WF₆ (volatile, b.p. 17 °C)
  WOₓFᵧ residues after O₂-containing steps
```

---

## B.4 Cryogenic Adsorption

```
Langmuir coverage θ = Kp / (1 + Kp), K ∝ exp(E_ads / k_B T)
E_ads (HF on oxide with co-adsorbed H₂O), illustrative: 0.4 eV

  T (°C)     K / K(+10 °C)    θ if θ(+10 °C) = 1%
  ──────────────────────────────────────────────
   +10           1                0.01
   −20          ≈ 7               0.07
   −40          ≈ 34              0.25
   −60          ≈ 220             0.69
   −80          ≈ 2100            0.95 → multilayer, rate falls
```

---

## B.5 Product Volatility

```
Product        Boiling / sublimation point    Volatile at −60 °C (vacuum)?
──────────────────────────────────────────────────────────────────────────
SiF₄           −86 °C (sublimes)              yes
CO             −191 °C                        yes
COF₂           −85 °C                         yes
H₂O            —                              partly adsorbs (catalyst)
WF₆            17 °C                          yes at mTorr partial pressure
BF₃            −100 °C                        yes
(NH₄)₂SiF₆     ≈ 100 °C (sublimes)            no → warm-up required
AlF₃           ≈ 1290 °C (sublimes)           no → R2 etch stop
```

---

## B.6 Polymerization Index

```
Π = (C − O_feed − O_wafer) / F     (atom flows, Book #29)

R1 ME2 at its start (C₄F₆ 32, C₄F₈ 15, O₂ 30, NF₃ 0):
  C = 4×32 + 4×15 = 188; F = 6×32 + 8×15 = 312; O_feed = 60
  O_wafer at the start of ME2 ≈ 10 sccm O atoms (≈ 18 at the very start of
  the etch, Book #29 scaling; it falls as the bottom slows)
  Π ≈ (188 − 60 − 10) / 312 ≈ 0.38 at the start of ME2

R1 ME2 at its end (C₄F₆ 27, C₄F₈ 15, O₂ 36, NF₃ 8):
  C = 168; F = 162 + 120 + 24 = 306; O_feed = 72; O_wafer ≈ 6
  Π ≈ (168 − 72 − 6) / 306 ≈ 0.29
```

The ramp lowers Π by about a quarter over ME2, compensating for the fall in oxygen released by the slowing bottom and for the more polymer-limited bottom (Chapter 8).

---

## B.7 Optical Emission Lines

```
Species    Wavelength (nm)    Use
──────────────────────────────────────────────────────────────────
CO         483.5, 519.8       oxide etch product; endpoint knee
CN         387.1, 388.3       nitride (supports, bottom stop)
SiF        440, 443           etch product
F          703.7, 685.6       actinometry with Ar 750.4
CF₂        251.9 (band)       polymer precursor
H (Hα)     656.3              R2 hydrogen chemistry
Ar         750.4, 811.5       actinometer
O          777.2, 844.6       oxygen balance; WAC endpoint
```

---

**Appendix B Version:** 1.0
