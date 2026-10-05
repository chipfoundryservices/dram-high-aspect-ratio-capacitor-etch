# Appendix C: Standard Operating Procedures

Representative procedures for qualifying and monitoring extreme-aspect-ratio capacitor etch. Adapt sample sizes and limits to local practice and to the product specification.

---

## C.1 Full-Depth Depth Series (ARDE Calibration)

**Purpose:** Fit ER₀, k, and k₂ over the full depth (Chapter 4). A series that stops short of full depth under-predicts the time to the stop.

```
1. Wafers: 6 product-pattern wafers with measured mask CD and mold thickness
2. Etch times (R1): 60, 120, 180, 240, 300 s, and full recipe (359 s)
   (stop each partial wafer at the end of the step in progress, then run
   a 10 s low-bias passivation step to freeze the front)
3. Cross-section (FIB/TEM) 5 holes at centre, mid-radius (100 mm), and
   147 mm on each wafer; record depth, top/bow/bottom CD
4. Convert times to TEOS-equivalent using the layer rate ratios
5. Fit t/h = (1/ER₀)(1 + (k/2w) h + (k₂/3w²) h²) by least squares
6. Accept if: ER₀ within ±3% of reference; k within ±0.001;
   k₂ ≤ 3×10⁻⁵; residuals < 15 nm
```

---

## C.2 Chamber Qualification After PM

```
1. Season: 25 wafers with the production recipe (Chapter 9)
2. Particle wafer: bare Si, full recipe without bias in the final 30 s;
   adders ≥ 45 nm ≤ 14 per wafer; no flakes > 1 µm
3. Edge-tilt monitor: product wafer; HV-SEM at 147, 145, 140 mm, 8 azimuths
   → mean tilt within ±0.03° of fleet target; adjust ring lift (C.3)
4. Golden wafer: depth, bottom CD, bow CD (CD-SAXS), mask remaining
   → within chamber-matching limits (Chapter 5): bottom CD ±0.4 nm,
     bow ±0.4 nm, time to stop ±3 s, mask ±30 nm
5. Sensitized not-open monitor (C.6): rate within ±50% of fleet baseline
6. Release with updated chamber constants
```

---

## C.3 Ring-Lift Calibration

```
1. Etch three tilt monitors at lift positions −25, 0, +25 µm from the
   expected setting
2. Measure mean tilt at 147 mm by HV-SEM (≥ 2000 holes per azimuth, 8
   azimuths)
3. Fit tilt vs lift (expected slope ≈ 0.08° per 100 µm)
4. Set lift to zero mean tilt minus the litho pre-compensation target
   (Chapter 11); record slope for the lift schedule
5. Re-check every 100 RF hours; recalibrate if |Δtilt| > 0.02°
```

---

## C.4 HV-SEM Twist and Placement Measurement

```
1. Image after strip and clean (or after bottom open with mask, if the
   HV-SEM contrast permits)
2. Beam: 30–60 keV; detect backscattered electrons from the hole bottoms
   through the mold
3. For each hole: top centre (SE image) and bottom centre (BSE image);
   displacement d = bottom − top
4. Per site (≥ 10⁵ holes): tilt = mean(d); twist = 3σ of (d − mean(d))
   in each axis; report the larger
5. Also report the bottom-angle proxy: d / H for the 1% largest |d|
6. Flag subpopulations: fit a two-component Gaussian mixture to |d|;
   report the weight of the broad component (Chapter 11 tail model)
```

---

## C.5 CD-SAXS Profile Measurement

```
1. Site in the array interior, beam spot ≥ 50 µm × 50 µm
2. Collect transmission scattering at ≥ 30 tilt angles (±30°)
3. Fit a stacked-trapezoid profile model: ≥ 12 segments over 2.1 µm, plus
   ellipticity and tilt
4. Report: top, neck, bow (and its depth), CD at 900 nm, bottom CD,
   CD_avg, tilt, ellipticity
5. Cross-check against FIB/TEM weekly; bias-correct
```

---

## C.6 Sensitized Not-Open Monitor

```
1. Product wafer with standard incoming metrology
2. Run R1 with the overetch shortened from 40 to 5 s (centre sites) —
   the bottom-open step unchanged
3. Strip and clean as production
4. VC inspection: ≥ 10⁷ holes at centre and 10⁷ at 147 mm
5. Report not-open rates; expected ≈ 3×10⁻⁶ at the centre (Chapter 12)
6. Trend weekly per chamber; a doubling indicates a change in the mask CD
   tail or the edge lag; investigate before product is affected
```

---

## C.7 Waferless Autoclean (WAC) Verification

```
1. Run WAC with OES logging (O 777 nm, F 704 nm, CO 483 nm)
2. Endpoint when CO falls to within 5% of the clean-wall baseline and F
   rises to within 5% of its plateau
3. If endpoint not reached within the time limit (60 s), extend by 30 s
   once; if still not reached, hold the chamber
4. Weekly: compare first-wafer and fifth-wafer bottom CD on a monitor;
   difference ≤ 0.2 nm
```

---

## C.8 Cryogenic Chuck Checks (R2)

```
1. Daily: helium flow and leak rate per zone at −60 °C; leak < 1 sccm
   per zone
2. Daily: wafer temperature by monitor wafer (or temperature-sensing
   wafer) at four radii → within ±1.2 K
3. Weekly: clamp force vs voltage at −60 °C; dechuck time < 5 s
4. After any warm-up of the chuck (PM): dry purge 2 h before cooling;
   no condensation on cold surfaces
5. Post-etch warm-up verification: XPS or TOF-SIMS on a monitor for
   (NH₄)₂SiF₆ residue; none detectable
```

---

**Appendix C Version:** 1.0
