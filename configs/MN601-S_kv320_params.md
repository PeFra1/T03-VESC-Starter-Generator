# T-Motors AT4130 KV230 Motor Parameters

## Basic Specifications
- **Model**: T-Motors AT4130 KV230
- **KV Rating**: 230 RPM/V
- **Application**: Drone starter-generator
- **Protection**: (check label)
- **Poles**: (check datasheet - likely 14 or 28)
- **Windings**: (check datasheet)

## Recommended VESC Settings (Initial Estimate)

### Motor Configuration
```
si-motor-poles: 14 or 28   ;; Verify from datasheet
si-gear-ratio: 1.0
si-wheel-diameter: (depends on propeller)
```

### Current Limits (Start conservative)
```
l-current-max: 30.0    ;; 30A continuous (verify from motor rating)
l-current-min: -30.0   ;; Regen current
l-max-erpm: 50000      ;; Max electrical RPM
l-min-erpm: -50000     ;; Min electrical RPM
l-max-duty: 0.95       ;; 95% max duty cycle
l-min-duty: -0.95      ;; -95% min duty cycle
```

### Battery Settings (2-channel 24V supply)
```
si-battery-cells: 6      ;; 6S LiPo ~22.2V nominal
l-battery-cut-start: 20.4V
l-battery-cut-end: 18.0V
```

### FOC Settings (if using FOC)
```
foc-motor-r: (from motor resistance measurement)
foc-motor-l: (from motor inductance measurement)
foc-motor-flux-linkage: (from motor flux measurement)
foc-sensor-mode: sensorless
```

### Testing Settings
```
foc-openloop-rpm: 1000   ;; Low openloop RPM for testing
foc-sl-openloop-time: 0.05
```

## Test Commands via VESC Tool Console
```
(get-rpm)                    ;; Read RPM
(get-current)                ;; Read current (mA)
(get-duty)                   ;; Read duty cycle
(get-batt)                   ;; Battery voltage
(get-fault)                  ;; Fault codes
(conf-get 'l-current-max)    ;; Read current limit
(conf-get 'si-motor-poles)   ;; Read motor poles
```

## Notes
- **VERIFY** actual current rating on motor label
- **TEST** at low duty cycle first (5-10%)
- **MONITOR** temperature during extended runs
- **MEASURE** motor resistance, inductance, flux linkage for accurate FOC tuning
- For **starter mode** (<30% PWM): Use RPM mode at ~3150 RPM (low cranking speed)
- For **power mode** (≥30% PWM): Use Duty Cycle mode for direct control

## Comparison with MN601-S KV320 (T02)
| Parameter | MN601-S KV320 | AT4130 KV230 |
|-----------|---------------|--------------|
| KV | 320 RPM/V | 230 RPM/V |
| Max Power | 1200W | ~700W (estimated) |
| Max Current | 50A | ~30A (estimated) |
| Poles | 14 (7 pairs) | ~14 (verify) |
| Voltage | 6S (22.2V) | 6S (22.2V) |
