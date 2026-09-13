# T03 - VESC Starter Generator

## LBM Scripting References

### GitHub Examples
- **VESC Tool Examples:** https://github.com/vedderb/vesc_tool/tree/master/res/LispBM/Examples
- **VESC Express Examples:** https://github.com/vedderb/vesc_express/tree/main/lbm_examples

### Documentation
- **VESC LispBM Examples:** https://vedderb-bldc.mintlify.app/lispbm/examples
- **VESC Extensions:** https://vedderb-bldc.mintlify.app/lispbm/vesc-extensions

### Key Notes
- VESC LBM doesn't have built-in `min`/`max` - use `if` statements (see T02 scripts)
- PWM input is read via `get-PPM` (returns -1.0 to +1.0)
- Always use `timeout-reset` in motor control loops
- `limit` function doesn't exist - implement with conditional logic

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
12. [ ] Test PWM threshold switching (30%)
13. [ ] Validate VESC Tool WLAN connection
14. [ ] Engine test: full start sequence
