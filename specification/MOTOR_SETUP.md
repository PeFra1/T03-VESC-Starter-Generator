# T-Motor AT4130 KV230 - VESC FOC Setup

**Datasheet:** [TMotor AT4130 Long Shaft Motor](https://store.tmotor.com/product/at4130-long-shaft-fixed-wing-motor.html?srsltid=AfmBOor3jltLm7XQg7X0c8YeBHvvAZ2COdoFQoErVvohIMKbULhLAjmh)

## Motor Specifications

| Parameter | Value |
|-----------|-------|
| Model | AT4130 Long Shaft |
| KV Rating | 230 RPM/V |
| Configuration | 12N14P |
| Pole Pairs | **7** |
| Stator Resistance (R) | **0.06 Ω** |
| Idle Current @ 10V | 1.4A |
| Peak Current (180s) | 60A |
| Max Power (180s) | 2500W |
| Rated Voltage | 12S LiPo |
| Dimensions | Φ50×79mm |
| Weight | 408g (incl. cable) |
| Shaft Diameter | 6mm |

## VESC FOC Parameters

### Required for Manual Setup

| Parameter | Value | Notes |
|-----------|-------|-------|
| **Number of Pole Pairs** | 7 | From 12N14P configuration |
| **Resistance (R)** | 0.06 Ω | Measured or from datasheet |
| **Flux Linkage (λ)** | ~0.0065 Wb | Calculated from KV = 230 RPM/V |
| **Ld (d-axis inductance)** | ~0.02 mH | Estimated (can use autodetect) |
| **Lq (q-axis inductance)** | ~0.02 mH | Estimated (can use autodetect) |

### Flux Linkage Calculation

```
KV = 230 RPM/V
ω = 230 × 2π/60 = 24.1 rad/s per volt

Flux linkage λ = √2 / (2 × KV × π/30)
λ ≈ 0.0065 Wb (milliWebers)
```

## Recommended VESC Settings

### Motor Detection
- Use **Auto-detect** in VESC Tool if possible
- If auto-detect fails, use manual entry with values above

### Current Limits
- **Max Current:** 60A (continuous), 75A (peak 180s)
- **Max Input Current:** 60A
- **Max Negative Current:** -15A (braking)

### FOC Parameters
- **Motor Inductance:** Use autodetect or estimate ~0.02 mH
- **Motor Resistance:** 0.06 Ω
- **Pole Pairs:** 7

### RPM Limits
- **Max RPM:** 5000 (script limit)
- **Safe Operating Range:** 0-5000 RPM

## Test Data Reference

### APC 16×8 Propeller @ 44.4V

| Throttle | Current (A) | Power (W) | RPM | Torque (N·m) | Thrust (g) |
|----------|-------------|-----------|-----|--------------|------------|
| 40% | 2.87 | 127.6 | 3701 | 0.226 | 1087 |
| 50% | 5.18 | 230.9 | 4664 | 0.366 | 1744 |
| 60% | 8.56 | 379.9 | 5546 | 0.531 | 2513 |
| 70% | 13.10 | 579.1 | 6363 | 0.719 | 3366 |
| 80% | 19.63 | 865.5 | 7215 | 0.958 | 4407 |
| 90% | 27.66 | 1216 | 7875 | 1.174 | 5293 |
| 100% | 38.25 | 1674 | 8646 | 1.521 | 6395 |

### APC 17×10 Propeller @ 44.4V

| Throttle | Current (A) | Power (W) | RPM | Torque (N·m) | Thrust (g) |
|----------|-------------|-----------|-----|--------------|------------|
| 40% | 3.84 | 171.1 | 3512 | 0.349 | 1459 |
| 50% | 6.96 | 309.4 | 4395 | 0.547 | 2285 |
| 60% | 13.34 | 591.6 | 5359 | 0.835 | 3459 |
| 70% | 19.07 | 843.6 | 6038 | 1.087 | 4428 |
| 80% | 28.30 | 1248 | 6806 | 1.410 | 5650 |
| 90% | 39.96 | 1754 | 7468 | 1.780 | 6939 |
| 100% | 55.63 | 2427 | 7891 | 2.101 | 7630 |

## Setup Steps

1. **Motor Detection:** Connect motor and use VESC Tool → Motor Parameters → Auto-detect
2. **Manual Entry (if needed):** 
   - Pole pairs: 7
   - Resistance: 0.06 Ω
   - Flux linkage: 0.0065 Wb
   - Inductance: ~0.02 mH
3. **Current Limits:** Set max current to 60A
4. **RPM Limits:** Set max RPM to 5000 (script limit)

## Notes

- Use 12S LiPo battery (44.4V nominal)
- Motor has 14 poles (7 pole pairs)
- Resistance is low (0.06Ω), ensure proper current sensing
- Test with small throttle first to verify rotation direction
