# T03 - VESC Starter Generator

## LBM Scripting References

### GitHub Examples
- **VESC Tool Examples (LispBM):** https://github.com/vedderb/vesc_tool/tree/master/res/LispBM/Examples
- **VESC Express Examples (Lisp):** https://github.com/vedderb/vesc_express/tree/main/lbm_examples

### Documentation
- **VESC LispBM Examples:** https://vedderb-bldc.mintlify.app/lispbm/examples
- **VESC Extensions:** https://vedderb-bldc.mintlify.app/lispbm/vesc-extensions

### Key Notes
- **VESC LBM** (VESC HP) doesn't have built-in `min`/`max` - use `if` statements (see T02 scripts)
- **VESC Express** uses standard Scheme/Lisp with `min`/`max`
- PWM input is read via `get-PPM` (returns -1.0 to +1.0)
- **Always use `timeout-reset`** in motor control loops to prevent faults
- `limit` function doesn't exist - implement with conditional logic
- Use multiple `print` args instead of `str`/`format`/`concat`

### Notable Examples from vesc_tool
| Example | Purpose | Relevance to T03 |
|---------|---------|------------------|
| `ppm_read.lbm` | Read PPM input and set duty | Direct reference for PWM reading |
| `can_pos_follow.lbm` | CAN communication + `timeout-reset` | CAN monitoring pattern |
| `duty_ramp_imperative.lbm` | Motor control with state | Motor control loop pattern |
| `balance.lbm` | Complex motor control | Full example with `timeout-reset` |
| `log_can.lbm` | CAN logging | Monitoring via VESC Express |

## Setup Notes

### Hardware Connection Diagram

```
[RC Controller] 
       │
       ▼
   [Pixhawk]
   (PWM out)
       │
       ▼
  [VESC HP 6MKvi]  ← Local script control (set-rpm / set-duty)
   (PWM in, CAN)       Motor: T-Motor AT4130 KV230
       │
       ▼
   [VESC Express]
   (CAN, WLAN to PC)
       │
       ▼
  [PC - VESC Tool]
  (monitoring via WiFi)
```

### CAN Bus Configuration
- **VESC HP:** CAN ID **100** (controls motor locally)
- **VESC Express:** CAN ID **6** (gateway to PC)
- **Function:** Monitoring only (script runs locally on VESC HP)

### Motor: T-Motor AT4130 KV230

**Datasheet:** [TMotor AT4130 Long Shaft Motor](https://store.tmotor.com/product/at4130-long-shaft-fixed-wing-motor.html?srsltid=AfmBOor3jltLm7XQg7X0c8YeBHvvAZ2COdoFQoErVvohIMKbULhLAjmh)

| Parameter | Value | Notes |
|-----------|-------|-------|
| Model | AT4130 KV230 | Brushless DC motor |
| KV rating | 230 RPM/V | Speed constant |
| Poles | 14 (7 pole pairs) | From datasheet: 12N14P |
| Flux linkage | ~0.0065 Wb | Calculated from KV |
| Resistance | 0.06 Ω | From datasheet |
| Inductance | ~0.02 mH | Estimated (use autodetect) |
| Max current | 60A (180s) | From datasheet |
| Max voltage | 12S LiPo (50.4V) | From datasheet |

**VESC FOC Setup:** See `specification/MOTOR_SETUP.md` for detailed parameters.

**Datasheet search:** TMotor AT4130 KV230 documentation

### How It Works
1. Script (`setStarter.lbm`) is uploaded to **VESC HP** via VESC Tool over WiFi
2. Script runs **locally** on VESC HP, controlling motor with `set-rpm`/`set-duty`
3. VESC Express forwards status data via CAN for real-time monitoring
4. User monitors RPM, current, duty cycle, temperature via VESC Tool on PC

### Power Supply Settings
- 24V / 1A lab power supply (6S LiPo equivalent)

### CCPM Servo Consistency Master
- Connect to VESC PWM output
- Verify signal consistency during operation

## Firmware Update Checklist

### VESC HP 6MKvi
| Item | Status |
|------|--------|
| Firmware version | Check in VESC Tool → Info tab |
| Required FW version | Latest stable (check VESC docs) |
| Backup config | Export XML before update |
| Update method | USB → VESC Tool → Firmware tab |

### VESC Express
| Item | Status |
|------|--------|
| Firmware version | Check in VESC Tool → Info tab |
| Required FW version | Compatible with VESC HP |
| Backup config | Export XML before update |
| Update method | WiFi → VESC Tool → Firmware tab |

### Post-Update Verification
- [ ] Verify CAN communication between HP and Express
- [ ] Test script upload via WiFi gateway
- [ ] Verify monitoring in VESC Tool
- [ ] Test PWM input threshold switching

## Next Steps

1. [ ] **Update VESC HP firmware** (backup config first)
2. [ ] **Update VESC Express firmware** (backup config first)
3. [ ] Verify VESC Tool WiFi connection to Express
4. [ ] Verify CAN communication (HP ID 100 ↔ Express ID 6)
5. [ ] Export current VESC config (XML)
6. [ ] Document PWM input mapping
7. [ ] Test basic motor rotation
8. [ ] Upload setStarter.lbm to VESC HP via WiFi (Express)
9. [ ] **SAFETY: Add timeout-reset to prevent runaway motor**
10. [ ] Implement debounce for PWM input
11. [ ] Add RPM limits (min/max safe operating range)
12. [ ] Test PWM threshold switching (20%)
13. [ ] Validate VESC Tool WLAN connection
14. [ ] Engine test: full start sequence
15. [ ] **Find T-Motor AT4130 KV230 documentation and create VESC motor setup**
