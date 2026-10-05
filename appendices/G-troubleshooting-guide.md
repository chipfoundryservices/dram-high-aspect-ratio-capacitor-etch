# Appendix G: Troubleshooting Guide

Symptom-driven guide for extreme-aspect-ratio capacitor etch excursions. For each symptom: likely causes ranked from most to least common, checks to separate them, and corrective actions. Chapter references point to the underlying physics.

---

## G.1 Not-Open Rate Up, Concentrated at the Wafer Edge

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Edge lag grown (ring wear, edge gas     Depth series at 147 mm; ring RF     Recalibrate ring; edge
   split drift) (Ch. 9.2.3)                hours; edge O₂ split readback        O₂ APC; extend edge OE
2. Edge mask CD small (litho/mask open     CD-SEM radial map before etch        Feed-forward; fix mask
   radial signature) (Ch. 13)                                                   open edge tuning
3. Thick mold at the edge (Ch. 2.1.3)      Film radial map                      Feed-forward time
4. Edge temperature high → bottom CD       Chuck zone temps; He flow by zone    Restore zone setpoint
   small (Ch. 8.5)
```

## G.2 Not-Open Rate Up, Whole Wafer

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Π drift up: electrode late in life,     Electrode RF hours; CF₂/Ar up;      Verify O₂ age offset;
   O₂ low (Ch. 9.1)                        bottom CD down                      change electrode
2. Mask CD tail grown (EUV dose, resist    Sensitized monitor up on all        Litho dose / resist
   lot) (Ch. 13.5)                         chambers at once                    lot action
3. Overetch shortened by APC error         APC log; CO knee timing             Fix APC input
   (Ch. 15.4)
4. Pulsing or DC superposition fault       Generator and DC supply logs         Repair; requalify
   (Ch. 6)
5. Bottom-open step degraded (CHF₃ MFC,    BO time; gouge low on TEM           Fix flow/bias
   bias low)
```

## G.3 Not-Opens or Damage in Clusters

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Flakes from walls or rings (Ch. 9.5)    SEM review at cluster centre;       Wet clean; check WAC
                                           particle wafer adders                endpoint; confinement
2. Arc (helium hole pattern, edge)         Arc log; crater pattern vs chuck     Chuck inspection;
   (Ch. 5.4, 6.5)                          He-hole map                          replace if repeat
3. Mask defects (litho field repeat)       Cluster position vs litho fields    Litho/mask-open action
```

## G.4 Bow Too Large (Wall < 9 nm)

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Low-energy ion fraction up (waveform    Generator waveform readback;        Repair generator;
   fault, pressure high) (Ch. 6.2)         pressure, valve position            recalibrate
2. Wafer warm (He leak, zone fault)        Zone temps; He leak per zone        Chuck service
   (Ch. 8.5)
3. Π low in ME1 (new electrode, C₄F₆ low)  OES CF₂/Ar; MFC readback            Flow; age offset reset
   (Ch. 4, 9)
4. Mask thin or low selectivity → facet    Mask remaining; facet on TEM        Mask spec; feed-forward
   down early (Ch. 13.1)                                                        mask check
5. Etch time extended by APC beyond        APC log                             Limit extensions;
   design (Ch. 10.3.3)                                                          investigate cause
```

## G.5 Twist Increased (Array Interior)

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Charge relief degraded: pulse duty,     Generator logs; DC current          Restore settings
   DC superposition off (Ch. 6.3–6.4)
2. Pressure high (fewer narrow ions)       Pressure, throttle valve            Recalibrate
   (Ch. 3.2)
3. Mask ellipticity up (litho focus,       CD-SEM ellipticity distribution     Litho/mask-open action
   mask-open) (Ch. 11.2.4, 13.4)
4. Π up → more polymer asymmetry           OES; bottom CD down                 O₂ offset
5. V_pp low (generator calibration)        V_pp probe vs readback              Recalibrate
```

## G.6 Edge Tilt Out of Spec

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Ring lift not tracking erosion          Ring RF hours vs lift position      Recalibrate (App. C.3)
   (Ch. 9.2)
2. New ring, not calibrated                PM log                              Lift calibration
3. Mask-open tilt changed (Ch. 11.3.2)     HV-SEM of mask openings             Fix mask-open chamber
4. Litho pre-compensation table out of     Overlay recipe vs ring-age model    Update pre-comp
   date (Ch. 11.3.3)
5. Wafer bow high (Ch. 2.4)                Incoming bow                        Stress balance
```

## G.7 Bottom CD Small (Not Yet Not-Open)

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Π drift (electrode, walls)              See G.2                             O₂ offset
2. Wafer cold                              Zone temps                          Restore
3. NF₃ ramp missing in ME2 (Ch. 8.1.3)     Recipe log                          Restore ramp
4. Mask CD small, not fed forward          APC log                             Fix feed-forward
```

## G.8 Pad Gouge or Side Punch Too Large

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Overetch selectivity to SiN low (O₂     Stop thickness left on TEM; OES     Restore OE chemistry
   high, NF₃ left on in OE) (Ch. 12.3)     CN in OE
2. Bottom-open step too long or bias high  BO time; V_pp in BO                 Restore; consider BO
                                                                                endpoint
3. Early holes much earlier than mean      CD distribution wider; centre-fast  Narrow radial lag;
   (Ch. 12.3.1)                            radial pattern                      APC edge
4. Placement worse → more overhang         HV-SEM placement                    See G.5, G.6
   (side punch width) (Ch. 12.3.4)
```

## G.9 Mask Remaining Low

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. B-ACL thin or low B content             Incoming film metrology; XPS        Mask spec; feed-forward
2. V_pp high (calibration) → sputter       V_pp probe                          Recalibrate
3. O₂ high in ME2 (APC over-correction)    APC log                             Bound O₂ offsets
4. Etch time extended (APC)                APC log                             Investigate driver
```

## G.10 Cryogenic (R2) Specific

```
Symptom                         Likely causes                         Actions
──────────────────────────────────────────────────────────────────────────────────────────
Rate low, radial pattern        Zone temperature high (He loss,       He leak check; zone
                                worn chuck surface) (Ch. 7.3)          service
Rate falls wafer to wafer       Coolant temperature drifting up;       Chiller service
                                chiller capacity
Contact resistance high,        Salt residue; warm-up short or         Restore warm-up; XPS
not open                        temperature low (Ch. 7.2.4)            monitor
Bow broad and large             Water accumulation; HF too high;       Pumping; HF flow; C₄F₈
                                C₄F₈ low (chemical bow) (Ch. 7.2.2)
Dechuck slow / wafer sticks     Residual charge at low T (Ch. 7.3.3)   Dechuck sequence; chuck
                                                                       check
Particles after PM              Condensation during cool-down          Dry purge before cooling
```

## G.11 Pillar Collapse or Twin-Bit Fails Up

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Drying non-uniform (IPA exchange)       Wet-tool logs; pattern on wafer      Wet process fix
   (Ch. 16.3)
2. Bow or twist up → smaller gaps          CD-SAXS bow; HV-SEM twist           See G.4, G.5
   (Ch. 2.2.5)
3. Support opening off-target              Support-open CD and overlay          Support-open process
4. Electrode void opened (re-entrant       TEM of pillars; neck/bow ratio      Reduce neck pinch
   profile) (Ch. 16.2.2)
```

---

**Appendix G Version:** 1.0
