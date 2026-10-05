# Chapter 10: Bow, Neck & the 9 nm Wall

## Overview

The capacitor hole is not a cylinder. It narrows slightly just below the top, where polymer gathers under the mask, then widens into a bow a few hundred nanometres down, then tapers to the bottom. At 57:1 the bow was a few nanometres on a 13 nm wall. At 91:1 the wall is 11 nm at the top, and the bow must leave at least 9 nm of it standing. The bow has about 1 nm of room per side.

This chapter describes the reference profile, explains how the neck forms and how ions reflected from it cut the bow, shows why the bow grows with etch time and therefore with aspect ratio, explains why 9 nm is the limit, treats bridging on the honeycomb as a statistical problem, and sets out the knobs that reduce the bow without closing the bottom.

**Learning Objectives:**
- Describe the reference profile and compute the wall at each depth
- Explain neck formation and locate the bow from the neck taper
- Estimate the growth of the bow with etch time
- Explain the 9 nm wall limit from integration and mechanics
- Estimate bridging probability on the honeycomb and identify its real source
- Choose bow-control knobs and quantify the bow–bottom trade-off

---

## 10.1 The Reference Profile

### 10.1.1 Shape

```
R1 reference profile (illustrative, after strip and clean):

  Depth (nm)   CD (nm)   Wall p − CD (nm)   Feature
  ─────────────────────────────────────────────────────────────
     0          26.0        11.0             top of mold (top SiN)
   120          25.0        12.0             neck
   450          27.5         9.5             bow maximum
   900          26.2        10.8             middle support (small step)
  1500          23.5        13.5
  2080          19.4        17.6             top of bottom stop
  2100          19.0        18.0             bottom (on W pad)

  Area-weighted average CD (Chapter 1): 23.9 nm as etched
```

```
Schematic (not to scale; lateral exaggerated):

  mask   │  │      │  │
  ───────┤  ├──────┤  ├──── top SiN       26
         │  │      │  │
          \ /       \ /     neck           25  (120 nm)
          (  )      (  )    bow            27.5 (450 nm)
          |  |      |  |
          ┤  ├      ┤  ├    middle SiN     26.2 (900 nm)
          |  |      |  |
           \/        \/     taper
           ▔▔        ▔▔     bottom         19  (2100 nm)
```

### 10.1.2 Comparison with Book #29

```
                        1b (Book #29)     1d (R1)
  ─────────────────────────────────────────────────
  Top CD                  32               26
  Bow CD                  33.5             27.5
  Bow depth               350 nm           450 nm
  Bow / top               1.05             1.06
  Wall at bow             11.5 nm          9.5 nm
  Bottom CD               24               19
  Bottom / top            0.75             0.73
```

The profile has kept its proportions. That is the problem: the wall has not. A bow that is 6% wider than the top consumes 1.5 nm of an 11 nm wall, leaving 9.5 nm against a 9 nm limit.

---

## 10.2 The Neck

### 10.2.1 How It Forms

Just below the mask, the sidewall receives the most polymer precursors (the high-sticking species never get further, Chapter 4) and few ions, because the ions that strike the wall this high are mostly the broad, low-energy ones. Polymer builds up and narrows the hole. Below the neck, the polymer flux falls and the ion flux to the wall from reflection rises, so the wall begins to recede.

### 10.2.2 The Neck Taper

```
Neck: CD falls from 26.0 at the mold top to 25.0 at 120 nm
Average wall inclination of the oxide over that span:
  arctan(0.5 nm / 120 nm) ≈ 0.24° per side
The polymer surface inside the neck, where most reflections occur, is
  far steeper locally: φ ≈ 1.5–2° over its last few tens of nanometres
```

The neck matters less for its own CD than for what it does to ions. A wall inclined inward by φ reflects a vertical ion away from the vertical by 2φ.

---

## 10.3 Where the Bow Comes From

### 10.3.1 The Reflection Model

```
An ion reflecting from a neck wall inclined by φ leaves at 2φ from vertical
and crosses the hole (width w) to strike the opposite wall at a depth
  Δz ≈ w / tan(2φ) below the reflection point

R1: w ≈ 25 nm, φ ≈ 1.7° → 2φ = 3.4°, tan(3.4°) = 0.059
  Δz ≈ 25 / 0.059 ≈ 420 nm
Reflection points spread over ≈ 0–120 nm (mid ≈ 60 nm)
  → bow centred near 60 + 420 ≈ 480 nm (reference 450 nm)
```

```
Book #29 for comparison: w ≈ 31 nm at the neck, φ ≈ 2.2°:
  Δz = 31 / tan(4.4°) = 31 / 0.077 ≈ 400 nm → bow near 350–450 nm
```

The bow sits deeper in the narrower hole only if the neck taper is gentler. In practice R1's neck is gentler (more ion-driven polymer removal at higher energy), and the bow is at nearly the same depth.

### 10.3.2 The Other Contributors

```
Contributions to the bow at 450 nm (R1, illustrative share of lateral etch):

  Source                                          Share
  ────────────────────────────────────────────────────────
  Ions reflected from the neck taper              ≈ 40%
  Broad, low-energy collisional ions              ≈ 30%
  Ions deflected by wall charge                   ≈ 15%
  Ions reflected from the mask facet              ≈ 10%
  Spontaneous chemical etch (F, O)                ≈ 5%
```

Ions that arrive directly at the bow from the plasma at angles of 2–4° account for much of the "broad" share: Chapter 3 showed that most of the broad population is lost in the upper hole. The waveform and the pressure (Chapter 6) attack this share; the polymer and temperature attack the reflection share.

### 10.3.3 The Bow Grows with Time

The bow region, once formed, is exposed for the rest of the etch.

```
Bow forms when the front passes ≈ 450 nm: t ≈ 0.9 min (Chapter 8)
End of high-bias etch (end of overetch): t ≈ 5.4 min
Bow CD at formation (front passing): ≈ 25.5 nm
Bow CD at end: 27.5 nm
Mean lateral recession: (27.5 − 25.5)/2 / (5.4 − 0.9) ≈ 0.22 nm/min per side

Sensitivity: each 10% of extra high-bias time adds ≈ 0.1 nm to the bow CD
```

This is the first way the aspect ratio enters the bow: a deeper hole takes longer, and the upper hole is cut for longer. A 1e hole at 2.35 µm with R1 would take about 20% longer. With a top CD near 23.7 nm and the same 6% bow ratio, plus the extra growth, its bow would be about 25.3 nm on a 34 nm pitch, leaving 8.7 nm, below the 9 nm limit. **R1 cannot make the 1e bow without new bow control.**

---

## 10.4 The 9 nm Wall

### 10.4.1 Three Reasons

The minimum wall at the bow is set by what happens after the etch:

1. **Electrode and wet steps.** The thin oxide wall must survive the post-etch clean (which removes 0.5–1 nm of oxide), the TiN deposition, and the start of mold removal without breaking. Walls below about 6–7 nm crack.
2. **Gap fill after mold removal.** Once the mold is gone, the gap between two pillars at the bow equals the wall. The dielectric (physical thickness ≈ 4.5 nm at EOT 0.50 nm) coats both pillars. If the gap is less than 2 × 4.5 = 9 nm, the dielectric closes it before the plate can enter, leaving a seam with no plate and a weak spot for leakage.
3. **Mechanics.** A narrower gap reduces the collapse margin of the pillars (Chapter 2).

```
Wall budget at the bow (illustrative):
  Pitch                              37.0 nm
  Bow CD (mean)                     −27.5
  Wall (mean)                         9.5
  Post-etch clean (both sides)       −0.6
  Wall at mold removal                8.9
  Required for gap fill (2 × 4.5)     9.0
  Shortfall                          −0.1 → closed only because ALD
                                       dielectric grows ≈ 0.1–0.2 nm thinner
                                       in the re-entrant bow; the as-etched
                                       specification is therefore ≥ 9 nm
```

The specification is effectively met with no margin. Every tenth of a nanometre of bow matters.

---

## 10.5 Bridging on the Honeycomb

### 10.5.1 Pairs, Not Holes

```
Each hole has 6 neighbours; each pair is shared → 3 pairs per hole
24 Gb die: 3 × 2.58×10¹⁰ = 7.7×10¹⁰ pairs
Specification: ≤ 1×10⁻¹⁰ per pair → ≤ 8 bridged pairs per die
```

### 10.5.2 Gaussian Variation Is Not the Problem

```
Wall between two holes: t = p − (b₁ + b₂)/2 − δ
  b₁, b₂: bow CDs; δ: relative placement at the bow depth

  σ(b) = 0.5 nm per hole → σ of (b₁+b₂)/2 = 0.35 nm
  σ(δ) at 450 nm depth ≈ 0.3 nm
  σ(t) = √(0.35² + 0.3²) = 0.46 nm

Breaking threshold ≈ 4 nm (the wall fails in the clean or electrode step)
Z = (9.5 − 4.0) / 0.46 = 12 → Gaussian probability ≈ 10⁻³³ per pair
```

A Gaussian wall never bridges. Bridged pairs come from **outliers**: holes whose mask opening was abnormally large, mask defects that merge two openings, striations that cut into the wall, and particles that distort the mask. Their rate is set by patterning and mask-open defectivity, which Chapter 13 treats. The etch's role is to not amplify them: an outlier hole 3 nm wide at the mask grows to a bow 3–4 nm wider than normal, leaving a 5–6 nm wall, and survives; one 6 nm wide leaves 2–3 nm and bridges.

---

## 10.6 Controlling the Bow

### 10.6.1 Knobs

```
Bow-control knobs (R1, illustrative sensitivities on bow CD):

  Knob                                      Δ bow CD     Δ bottom CD   Cost
  ──────────────────────────────────────────────────────────────────────────────
  C₄F₆ +10% in ME1                          −0.4 nm      −0.5 nm        not-open risk
  Wafer temperature −5 K                    −0.65 nm     −0.3 nm        selectivity, rate
  Low-energy ion fraction −5 points         −0.5 nm      ≈ 0            generator
  (waveform, pressure)
  Pressure −2 mTorr                         −0.3 nm      +0.2 nm        lower rate
  Cyclic sub-steps in ME1                   −0.9 nm      ≈ 0            +7% time
  DC superposition +300 V                   −0.2 nm      +0.3 nm        electrode life
  (less wall charging)
  Thinner mask facet (more selective mask)  −0.3 nm      ≈ 0            mask cost
  R2 cryogenic chemistry                    −0.7 nm      +1.0 nm        hardware
```

### 10.6.2 The Bow–Bottom Trade

The easiest knobs, more polymer and lower temperature, narrow the bow and the bottom together. The polymer that protects the bow wall also tapers the lower hole and raises the not-open rate.

```
Polymer knob (C₄F₆ in ME1):  Δbottom/Δbow ≈ 1.25
  To recover 0.5 nm of bow: lose 0.6 nm of bottom CD
  Bottom CD 19.0 → 18.4, closer to the 16 nm limit; not-open rate ≈ ×2
```

The knobs that break the trade act on the ions rather than the polymer: the waveform, the pressure, cyclic sub-steps, and charge relief. At 91:1 they are no longer optional. **Bow control at extreme aspect ratio is ion control.**

---

## Summary and Key Takeaways

1. **The profile kept its shape; the wall did not.** A bow 6% wider than the top leaves 9.5 nm against a 9 nm limit.

2. **The neck makes the bow.** Ions reflected from a neck taper of about 1.7° cross the hole and strike the opposite wall about 420 nm lower.

3. **The bow grows with time.** About 0.22 nm/min per side after it forms; each extra 10% of etch time adds about 0.1 nm. A 1e hole with R1 would leave about 8.7 nm, below the 9 nm limit.

4. **The 9 nm limit is a gap-fill limit.** Two dielectric layers of about 4.5 nm must fit in the gap between pillars at the bow.

5. **Bridging is an outlier problem.** A Gaussian wall never bridges; mask and patterning outliers do.

6. **Bow control is ion control.** Polymer and temperature trade bow for bottom CD; waveform, pressure, cyclic etch, and charge relief do not.

---

## Study Questions

1. A neck taper of 1.3° forms instead of 1.7°. Where does the bow centre move, assuming reflections centred at 60 nm and w = 25 nm?

2. Using the lateral recession rate of Section 10.3.3, estimate the bow CD for a 2.35 µm hole etched with R1 (compute the extra time from G(h) with w = 21 nm and scale the recession for the narrower hole as you think appropriate).

3. The dielectric is changed to a material with physical thickness 4.0 nm at EOT 0.50 nm. What bow CD is then allowed on the 37 nm pitch?

4. Compute the per-pair bridging probability if 1 hole in 10⁸ has a mask CD 6 nm too large, assuming that such a hole always bridges with one of its six neighbours. Does this meet the specification?

5. Find a combination of two knobs from Section 10.6.1 that reduces the bow by 1.0 nm while keeping the bottom CD within 0.2 nm of its reference.

---

**Next Chapter:** [Chapter 11: Twist, Tilt & Bottom Placement at Extreme Depth](./11-twist-tilt-placement.md)

---

**Chapter 10 Development Status:** Complete  
**Version:** 1.0
