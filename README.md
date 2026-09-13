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
  [VESC HP 6MKvi]
   (PWM in, CAN)
       │          │
       │          ▼
       │     [VESC Express]
       │
       ▼
[T-Motor AT4130 KV230]
 (generator/starter)
```

### Power Supply Settings
- Channel 1: 24V / 1A (main VESC power)
- Channel 2: 24V / 1A (backup/starter辅助)

### CAN Configuration
- VESC HP: CAN ID ____
- VESC Express: CAN ID ____
- Baud rate: 500k

### CCPM Servo Consistency Master
- Connect to VESC PWM output
- Verify signal consistency during operation

## Next Steps

1. [ ] Verify VESC HP firmware version
2. [ ] Export current VESC config (XML)
3. [ ] Document PWM input mapping
4. [ ] Test basic motor rotation
5. [ ] Implement starter script
