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
| VESC 2 | VESC Express (CAN connected, WLAN to PC) |
| Flight Controller | Pixhawk (generates PWM based on RC input) |
| Calibration Tool | CCPM Servo Consistency Master |
| Wiring | PWM from VESC to CCPM, CAN from VESC to VESC Express |

### Firmware/Software Requirements

#### VESC HP Script (T-Motor AT4130 KV230)

The script must implement hybrid PWM-based control with two modes:

**Threshold: 30% PWM**

**Mode 1 (PWM < 30%):**
- Motor runs at fixed RPM (*fixed-rpm* parameter, e.g., 3150 RPM)
- RPM mode active
- Used for engine cranking at low throttle

**Mode 2 (PWM ≥ 30%):**
- Motor runs at duty cycle read from PWM input
- Duty cycle mapped 0-100% from PWM pulse width
- Duty Cycle mode active
- Used for direct power control at high throttle

**Additional Requirements:**
- VESC Express connected via CAN bus
- WLAN connection to PC for VESC Tool monitoring
- Parameters must be visible in VESC Tool (PC)

#### VESC Express Role
- CAN interface to main system
- WLAN hotspot/STA for VESC Tool connection
- No custom script required (default VESC Express firmware)

### Tasks

#### Hardware
- [ ] Connect VESC HP 6MKvi to T-Motor AT4130 KV230
- [ ] Connect Pixhawk PWM output to VESC PWM input
- [ ] Connect VESC to VESC Express via CAN bus
- [ ] Set up CCPM Servo Consistency Master for signal validation
- [ ] Configure VESC Express WLAN (hotspot or STA)

#### Firmware/Software
- [ ] Configure VESC HP for starter mode
- [ ] Write LBM script with PWM threshold logic (30%)
- [ ] Implement fixed duty cycle parameter (Mode 1)
- [ ] Implement PWM-read duty cycle (Mode 2)
- [ ] Ensure both modes use RPM control
- [ ] Configure CAN settings for VESC Express
- [ ] Enable VESC Tool monitoring via WLAN

#### Testing
- [ ] Bench test: verify PWM threshold switching
- [ ] Bench test: fixed duty cycle mode (<30% PWM)
- [ ] Bench test: PWM-read duty cycle mode (≥30% PWM)
- [ ] Validate VESC Tool WLAN connection
- [ ] Engine test: full start sequence with gasoline engine
- [ ] Validation: CCPM signal consistency

### Notes

- 2026-09-04: Lost 2 hours on unrelated online meeting (not StratoWAVE-related)
