# T3 VESC HP Application Configuration Export

## Original Export from VESC Tool

### App Settings (Critical)
| Parameter | Value | Notes |
|-----------|-------|-------|
| `app_to_use` | 4 | PPM app (perfect for PWM input) |
| `app_ppm_conf.ctrl_type` | 0 | Duty cycle control (ok za našu skriptu) |
| `app_ppm_conf.pid_max_erpm` | 15000 | Max RPM |
| `app_ppm_conf.safe_start` | 1 | Safe start enabled |
| `can_status_rate_1` | 50 | 50Hz status updates (dobar za VESC Tool) |

### Setup Instructions

1. **Connect VESC HP to VESC Tool**
2. Go to **Application** tab
3. Verify/adjust settings:
   - App: PPM
   - Ctrl Type: Duty Cycle
   - PID Max ERPM: 15000 (ili više ako treba)
4. Click **Write**
5. CAN status rate je 50Hz → VESC Tool će vidjeti parametre u real-time

### For T03 Starter-Generator

This configuration is **already correct** for:
- PPM input from Pixhawk
- Duty cycle control (skripta koristi `set-duty`)
- CAN monitoring (VESC Express)

No changes needed for application settings.

## Notes
- `app_ppm_conf.ctrl_type: 0` = Duty cycle (0-100%)
- `app_ppm_conf.ctrl_type: 1` = RPM mode (koristio bi `set-rpm`)
- Current export koristi **Duty Cycle** mode → kompatibilno s našom skriptom
