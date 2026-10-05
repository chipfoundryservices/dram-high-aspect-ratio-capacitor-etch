# Appendix E: Scaling, Transport, Placement & Capacitance Calculations

The closed-form models used in this book, with the reference values substituted. Chapter references point to the derivations and discussion.

---

## E.1 Cell, Layout, and Scaling (Chapter 1)

```
Sense signal:     ΔV_BL = (V_DD/2) C_s / (C_s + C_BL)
                  V_DD 1.0 V, C_BL 35 fF, C_s 9.7 fF → 108 mV; C_s,min 8.2 fF

Hexagonal lattice, pitch p:
  area per site     = (√3/2) p²         → 1186 nm² at p = 37 nm
  row spacing       = (√3/2) p          → 32.0 nm
  triple point      = p / √3            → 21.4 nm
  wall              = p − CD            → 11 nm at 26 nm
  open fraction     = (π/4) CD² / ((√3/2) p²) → 0.45 at 26 nm

Pitch from cell area: p = √(A_cell / 0.866); 6F² at F = 14 → 36.9 nm

Scaling at fixed C_s and EOT, cell area × s per generation:
  CD ∝ √s;  H ∝ 1/√s;  A = H/CD ∝ 1/s
  s = 0.8 → CD × 0.894, H × 1.118, A × 1.25
```

---

## E.2 Capacitance (Chapter 1)

```
C_s = ε₀ · 3.9 · π · CD_avg · H_eff / EOT

  Full sidewall (H 2100, CD 23, EOT 0.50):  10.5 fF
  H_eff = 2100 − 160 = 1940 nm:              9.7 fF

Sensitivities: ∂C/∂H_eff = 0.50 fF/100 nm; ∂C/∂CD = 0.42 fF/nm;
               ∂C/∂EOT = −0.19 fF per 0.01 nm

Height for a target: H_eff = C_s · EOT / (ε₀ · 3.9 · π · CD_avg)
  4F²: C_s 6.5 fF, CD 18 nm → H_eff 1.66 µm, H ≈ 1.82 µm, A ≈ 101

Retention: I_leak,max = C_s ΔV / t_ref = 9.7 fF × 0.2 V / 32 ms = 61 fA
```

---

## E.3 Pillar Mechanics and Wafer Bow (Chapter 2)

```
I = π d⁴ / 64;  EI at d = 23 nm, E = 300 GPa: 4.12×10⁻²¹ N·m²

Uniform lateral load q:
  cantilever      δ = q L⁴ / (8 EI)
  clamped–clamped δ = q L⁴ / (384 EI)

  q = 2×10⁻³ N/m: L = 1140 nm clamped → 2.1 nm; L = 2000 nm clamped → 20 nm
  Collapse when δ ≥ (p − CD)/2 = 7 nm

Scaling: δ ∝ (L/d)⁴ → 91:1 vs 57:1 = 6.5×

Stoney: κ = 6 σ_f t_f / (M_s t_s²); bow b = κ r²/2
  B-ACL −250 MPa, 1.5 µm on 775 µm Si: κ = 0.0208 m⁻¹ → b = 234 µm

Capillary (Chapter 16): ΔP = 2γ cos θ / g → IPA, 14 nm: 3.1 MPa
```

---

## E.4 Ions: Flux, Angle, Acceptance, Transmission (Chapter 3)

```
Removal flux = ER × n_SiO₂ → 2.65×10¹⁶ cm⁻² s⁻¹ at 700 nm/min
Ion flux = removal / Y; Y(E) ≈ Y₀ √(E/E₀) → Y(4.5 keV) ≈ 3.7
J_i ≈ 1.15 mA/cm²; ion power 5.2 W/cm² → 3.7 kW per wafer

Angular spread:
  collisionless   θ ≈ √(T_i⊥ / E_i) → 0.19° at 4.5 keV
  λ_cx = 1/(n σ_cx) → 6.9 mm at 15 mTorr; collisionless fraction exp(−s/λ)
  → 0.55 at s = 4 mm

Acceptance (edge to edge): θ_acc = arctan(w / h_tot), h_tot = h_mask + h
  end of R1: arctan(23/2930) = 0.45°

Monte Carlo transmission (illustrative model):
  launch uniformly over the opening; Gaussian angles σ per axis;
  specular reflection with probability R(θ) = 0.97 exp(−θ/2°);
  97% energy retained per reflection

  Mixed bottom ion fraction = 0.55 f_narrow(σ 0.2°) + 0.45 f_broad(σ 2°)
  A_tot 83: 0.56; 104: 0.54; 128: 0.52; 155: 0.50

Isotropic electron transmission to the bottom ≈ (w / 2h)²
```

---

## E.5 Charging and Deflection (Chapters 3, 6)

```
θ_defl ≈ E⊥ L / (2 E_i),  E⊥ = ΔV / w
  2 V across 23 nm, L = 200 nm, 4.5 keV: θ = 0.11°; shift over 1000 nm
  = 1.9 nm

Droop under a pulse-shaped bias: dV/dt = J_i / (C/A)
  C/A = ε₀ ε_r / t (alumina 0.5 mm: 1.74×10⁻¹¹ F/cm²) → 66 V/µs

Sinusoidal IED: P(E < E*) = 1/2 + arcsin(E*/V_rf − 1)/π
  V_rf 4.5 kV: P(E < 2 keV) = 0.31

Collisional ions in a Child sheath: E = V₀ [1 − (x/s)^(4/3)];
  mean 0.57 V₀ for uniform births
```

---

## E.6 Neutral Transport and ARDE (Chapter 4)

```
Clausing (long tube):   K ≈ 4d / (3L)  (or 1/(1 + 3L/4d))
Coburn–Winters:         Γ_b/Γ_t = K / (K + β (1 − K))
Wall-loss decay:        A_w = 1/√(2 s_w)

Series model → linear ARDE:
  1/ER = 1/ER₀ + (3/4) ν A / Γ_n0
  ER = ER₀ / (1 + k A),  k = (3/4) χ,  χ = ν ER₀ / Γ_n0
  R1: k 0.016 → χ 0.021; R2: k 0.010 → χ 0.013

Extended: ER = ER₀ / (1 + k A + k₂ A²); R1 k₂ ≈ 2×10⁻⁵

Time to depth: t(h) = G(h)/ER₀, G(h) = h + k h²/(2w) (+ k₂ h³/(3w²))
Step time in a layer of rate ratio r: Δt = [G(h₂) − G(h₁)] / (r ER₀)
Depth at fixed time (linear): h = (w/k)[√(1 + 2k ER₀ t / w) − 1]

CD sensitivity: ∂h/∂w = (k h² / (2 w²)) / (1 + k h / w)
  R1 at 2100: 27.1 nm/nm; R2: 21.8; Book #29 at 1600 (w 28): 15.2

Arrival delay at the stop (R1 layered): ≈ 5.2 s per nm of CD_avg deficit
```

---

## E.7 Maximum Depth (Chapter 4)

```
Mask erosion rate r_m; facet factor f ≈ 1.6; margin M (flat) or
M_f (facet to 150 nm above mold top)

Solve G(h_max) = ER₀ t_main, with t_main from the mask:
  flat:  t_total = (h_mask0 − 500) / r_m;  t_main = t_total − t_BO
  facet: t_main = t_main,ref + margin_facet

R1: flat 3.03 µm (A 132); facet 2.51 µm (A 109)
R2: flat 3.95 µm (A 172); facet 3.25 µm (A 141)
```

---

## E.8 Cryogenic Adsorption (Chapter 7)

```
θ = K p / (1 + K p),  K ∝ exp(E_ads / k_B T)
K(−60 °C)/K(+10 °C) at 0.4 eV = exp(4640 × 1.161×10⁻³) ≈ 220

Chuck heat balance: ΔT_total = q (1/h_He + R_dielectric + R_coolant)
  7.1 W/cm²: 18 + 5 + 5 ≈ 28 K → coolant ≈ −88 °C for a −60 °C wafer
```

---

## E.9 Recipe Arithmetic (Chapter 8)

```
Residence time: τ = pV / Q; 15 mTorr × 10 L / 4.8 Torr·L/s = 31 ms

2×2 edge tuning: solve S x = Δ
  S = [[0.20, 0.04], [0.10, 0.13]] (nm per % edge O₂, nm per K)
  Δ = [+0.8, −0.3] → x = +5.3%, y = −6.4 K
```

---

## E.10 Bow (Chapter 10)

```
Reflection from a neck inclined by φ: Δz ≈ w / tan(2φ)
  w 25 nm, φ 1.7° → 420 nm below the reflection point

Bow growth after formation: CD_bow(t) = CD_form + 2 r_b (t − t_form),
  r_b ≈ 0.22 nm/min per side (R1)

Wall between holes: t = p − (b₁ + b₂)/2 − δ; σ_t ≈ 0.46 nm
Gap-fill limit: wall ≥ 2 × dielectric physical thickness (≈ 9 nm)
```

---

## E.11 Twist, Tilt, and Placement (Chapter 11)

```
Random walk in angle beyond onset h_on:
  ⟨θ²⟩ = D_θ (h − h_on);  ⟨x²⟩ = D_θ (h − h_on)³ / 3
  R1: h_on 690 nm, D_θ 2.4×10⁻⁹ rad²/nm → 3σ 4.5 nm at 2.1 µm
  R1 shorthand: 3σ = 8.5×10⁻⁵ (h − 690)^1.5 nm
  R2: h_on 800 nm, D_θ 1.4×10⁻⁹ → 3σ 3.0 nm

Edge tilt: θ(r) = θ_edge exp(−(R_w − r)/λ_e), λ_e ≈ 5 mm
Displacement: Δ = H tan θ
Ring: 0.08° per 100 µm of wear

Contact overlap: (pad + CD_bot)/2 − |Δ| → |Δ| ≤ 7 nm for 13 nm overlap
Budget: RSS of overlay, mask open, tilt residual, twist
  no pre-comp 6.7 nm; with pre-comp 5.7 nm (R1), 4.4 nm (R2)
```

---

## E.12 Not-Open Statistics (Chapter 12)

```
Budget per hole = allowed per die / holes per die = 5 / 2.58×10¹⁰ ≈ 2×10⁻¹⁰

Mask CD tail (illustrative): P(Δw > x) = 3×10⁻⁶ exp(−(x − 1)/0.35)
Late-arrival rate = Σ_regions (area share) × P(Δw > Δw_max(region))
  OE 40 s: edge Δw_max 4.2 → ≈ 1.5 per die; OE 50 s: 5.5 → 0.04 per die

Stop consumption: SiN rate × time on stop; gouge = W rate × time on W
VC sample: holes per cm² = 10¹⁴ / 1186 = 8.4×10¹⁰
```

---

## E.13 Endpoint and APC (Chapter 15)

```
Bottom-area fraction of the wafer: (π/4) CD_bot² / A_site × array eff.
  = 0.24 × 0.55 = 0.13
EWMA: offset_{n+1} = offset_n + λ (target − measured) / gain, λ ≈ 0.3
Feed-forward: Δt = ΔCD_avg × 5.2 s/nm + Δmold / ER_bottom
```

---

**Appendix E Version:** 1.0
