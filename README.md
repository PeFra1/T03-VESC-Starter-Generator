# T03 - VESC Starter Generator

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

## Next Steps

1. [ ] Verify VESC HP firmware version
2. [ ] Export current VESC config (XML)
3. [ ] Document PWM input mapping
4. [ ] Test basic motor rotation
5. [ ] **Upload setStarter.lbm to VESC HP via WiFi (Express)**
6. [ ] **SAFETY: Add timeout-reset to prevent runaway motor**
7. [ ] Implement debounce for PWM input
8. [ ] Add RPM limits (min/max safe operating range)
9. [ ] Test PWM threshold switching (30%)
10. [ ] Validate VESC Tool WLAN connection
11. [ ] Engine test: full start sequence
