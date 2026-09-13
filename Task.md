# T03 - VESC Starter Generator

## Task (from Ivan Salajster, 2026-09-04)

### System Overview (User Story)

**Goal:** Implement a starter-generator system for a drone with a gasoline engine.

**Operation:**
1. Operator presses button on RC controller
2. PWM signal is sent to VESC via Pixhawk flight controller
3. Generators motor (T-Motor AT4130 KV230) acts as starter motor, cranking the gasoline engine from standstill
4. As engine starts producing thrust, it takes over from the generator motor
5. Operator releases button → PWM stops
6. Generator motor switches to normal generation mode (powers electrical systems)

### Hardware Setup

| Item | Description |
|------|-------------|
| Battery/Power | 2-channel lab power supply (24V/1A per channel) |
| Motor 1 | T-Motor AT4130 KV230 (generator/starter) |
| Engine | Gasoline engine (unspecified) |
| VESC 1 | VESC HP 6MKvi (controls generator motor) |
| VESC 2 | VESC Express (unspecified role) |
| Flight Controller | Pixhawk (generates PWM based on RC input) |
| Calibration Tool | CCPM Servo Consistency Master |
| Wiring | PWM from VESC to CCPM, CAN from VESC to VESC Express |

### Tasks

#### Hardware
- [ ] Connect VESC HP 6MKvi to T-Motor AT4130 KV230
- [ ] Connect Pixhawk PWM output to VESC PWM input
- [ ] Connect VESC to VESC Express via CAN bus
- [ ] Set up CCPM Servo Consistency Master for signal validation

#### Firmware/Software
- [ ] Configure VESC HP for starter mode
- [ ] Implement PWM-to-RPM mapping
- [ ] Configure auto-switch to generation mode after engine starts
- [ ] Test start sequence (crank → engine fires → switch to gen mode)
- [ ] Test manual cancel (button release during cranking)

#### Testing
- [ ] Bench test: cranking sequence with dummy load
- [ ] Engine test: full start sequence with gasoline engine
- [ ] Validation: CCPM signal consistency

### Notes

- 2026-09-04: Lost 2 hours on unrelated online meeting (not StratoWAVE-related)
