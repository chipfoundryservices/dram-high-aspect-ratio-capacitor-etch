# Appendix D: Process Windows & Lookup Tables

Reference recipes, process windows, sensitivities, and lookup tables for R1 and R2. All values are illustrative starting points for a design of experiments.

---

## D.1 R1 Reference Recipe

```
Step  Name          Depth (nm)      Time (s)  Gas (sccm)                           Bias / source       Notes
──────────────────────────────────────────────────────────────────────────────────────────────────────────────────
1     Top SiN       0–100            12.7     CHF₃ 40, CF₄ 40, O₂ 15, Ar 200       7 kV / 2.5 kW       CW
2     ME1 (TEOS)    100–900          92.4     C₄F₆ 32, C₄F₈ 15, O₂ 30, Ar 300      9 kV / 3.0 kW       5 kHz, D 0.90
3     Middle SiN    900–940           8.0     C₄F₆ 20, CH₂F₂ 15, O₂ 25, Ar 300     8 kV / 3.0 kW       blended
4     ME2 (BPSG)    940–2080        171.2     C₄F₆ 32→27, C₄F₈ 15, O₂ 30→36,       9.5→10.5 kV         D 0.90→0.85;
                                              NF₃ 0→8, Ar 300                      / 3.0 kW            DC −500→−900 V
5     Overetch      slow holes        40      C₄F₆ 34, C₄F₈ 10, O₂ 28, Ar 300      10 kV / 3.0 kW      SiN-sel. ≈ 15:1
6     Bottom open   2080–2100         35      CHF₃ 50, O₂ 10, Ar 200               3 kV sine / 1.5 kW  CW
────────────────────────────────────────────────────────────────────────────────────────────────────────────────
Total 359.3 s; pressure 15 mTorr (16→14 in step 4); wafer +10 °C; 60 MHz source; 400 kHz tailored bias
```

---

## D.2 R2 Reference Recipe

```
Step  Name                  Depth (nm)      Time (s)   Gas (sccm)                              Notes
────────────────────────────────────────────────────────────────────────────────────────────────────────
1     Top SiN + ME1         0–900            61        HF 200, C₄F₈ 20, O₂ 10, Ar 100          −60 °C
2     Mid SiN + ME2         900–2080         92        as step 1, HF 220, C₄F₈ 18              ramped bias
3     Overetch              slow holes       15        as step 2, most selective setting
4     Bottom open           Al₂O₃ stop       22        Cl₂/BCl₃/Ar short step (stop material)
────────────────────────────────────────────────────────────────────────────────────────────────────────
Total ≈ 190 s; 20 mTorr; post-etch warm-up 120 °C, 40 s
```

---

## D.3 Process Windows (R1)

```
Parameter                  Window             Limiting failure at low / high end
──────────────────────────────────────────────────────────────────────────────────────
ME2 O₂ (end)               33–39 sccm         not-open, small bottom CD / bow, twist, mask
ME2 NF₃ (end)              4–10 sccm          not-open / bow, mask facet
C₄F₆ (ME1)                 28–36 sccm         bow / not-open, neck pinch
Pressure (ME2)             13–16 mTorr        rate / bow, twist (broad ions)
V_pp (ME2 end)             9.8–11 kV          twist, rate / arcing, mask, chuck
Pulse duty (ME2)           0.80–0.90          twist / time
DC superposition           −600 to −1000 V    twist / electrode life, Π
Wafer temperature          +5 to +15 °C       bottom CD, rate / bow
Overetch                   35–55 s            not-open (edge) / gouge, mask
Bottom open                30–40 s            BO not cleared / gouge, side punch
```

---

## D.4 Sensitivity Table (R1, Illustrative)

```
Change                       Δ bow CD   Δ bottom CD   Δ time to stop   Δ twist 3σ   Δ mask left
                             (nm)       (nm)          (s)              (nm)         (nm)
──────────────────────────────────────────────────────────────────────────────────────────────────
O₂ ME2 +1 sccm               +0.03      +0.12          −1.5            +0.05        −3
C₄F₆ ME1 +10%                −0.4       −0.5           +4              +0.1         +10
Wafer T +1 K                 +0.13      +0.04          −0.5            +0.03        −2
Pressure −1 mTorr            −0.15      +0.1           +3              −0.2         −2
V_pp +0.5 kV                 +0.1       +0.2           −6              −0.35        −15
Pulse duty −0.05             −0.1       +0.1           +8              −0.4         −5
Mask top CD +1 nm            +1.1       +1.2           −5.2            ≈ 0          0
Mold +24 nm (3σ)             0          0              +4.3            +0.1         −7
Electrode +100 RF h          −0.04      −0.08          +0.5            ≈ 0          0
Ring wear +100 µm (edge)     edge tilt +0.08° → +2.9 nm bottom displacement at 147 mm
```

---

## D.5 ARDE Lookup (w = 23 nm)

```
           R1 (ER₀ 700, k 0.016)          R2 (ER₀ 1100, k 0.010)
  h (nm)   ER/ER₀   t (min)   ∂h/∂w       ER/ER₀   t (min)   ∂h/∂w
  ────────────────────────────────────────────────────────────────────
   500     0.74     0.84       2.8         0.82     0.50       1.9
  1000     0.59     1.93       8.9         0.70     1.11       6.6
  1500     0.49     3.26      16.7         0.61     1.81      12.9
  2000     0.42     4.84      25.3         0.53     2.61      20.2
  2100     0.41     5.19      27.1         0.52     2.78      21.8
  2350     0.38     6.10      31.7         0.49     3.23      25.8
  (TEOS-equivalent, linear ARDE; add the k₂ correction above A ≈ 100)
```

---

## D.6 Capacitance Lookup (EOT 0.50 nm, H_eff = H − 160 nm)

```
               H = 1.8 µm   1.95 µm   2.1 µm   2.25 µm   2.4 µm
  CD_avg 21      7.5         8.2       8.8      9.5       10.2     (fF)
  CD_avg 22      7.8         8.5       9.3      10.0      10.7
  CD_avg 23      8.2         8.9       9.7      10.4      11.2
  CD_avg 24      8.5         9.3      10.1      10.9      11.7
```

C_s = ε₀ · 3.9 · π · CD_avg · (H − 160 nm) / EOT. The reference cell (CD_avg 23 nm, H 2.1 µm) is 9.7 fF. Each nanometre of CD_avg is worth about 0.42 fF and each 100 nm of height about 0.50 fF near the reference.

---

## D.7 Tilt and Placement Lookup

```
Bottom displacement Δ = H tan θ (nm):

  θ        H = 1.6 µm   2.1 µm   2.35 µm   2.6 µm
  ─────────────────────────────────────────────────
  0.02°      0.6         0.7       0.8       0.9
  0.05°      1.4         1.8       2.1       2.3
  0.10°      2.8         3.7       4.1       4.5
  0.20°      5.6         7.3       8.2       9.1

Twist 3σ (R1 model, h_on = 690 nm): 1.6 µm 2.3; 2.1 µm 4.5; 2.35 µm 5.7 nm
```

---

**Appendix D Version:** 1.0
