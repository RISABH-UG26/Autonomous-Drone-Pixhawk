# Flight Controller Quick Start Guide

> **⚠️ SAFETY FIRST: Remove all propellers before powering up your quadcopter for the first time!**

## Quick Setup (30 minutes)

### Step 1: Hardware Connections (5 min)

Connect components to your Arduino Uno:

| Component | Arduino Pin | Notes |
|-----------|-------------|-------|
| ESC 1 (Front Right) | Digital 4 | CCW rotation |
| ESC 2 (Rear Right) | Digital 5 | CW rotation |
| ESC 3 (Rear Left) | Digital 6 | CCW rotation |
| ESC 4 (Front Left) | Digital 7 | CW rotation |
| Receiver Ch1 (Roll) | Digital 8 | Signal wire only |
| Receiver Ch2 (Pitch) | Digital 9 | Signal wire only |
| Receiver Ch3 (Throttle) | Digital 10 | Signal wire only |
| Receiver Ch4 (Yaw) | Digital 11 | Signal wire only |
| Status LED | Digital 12 | Through 220Ω resistor |
| Gyro SDA | A4 (SDA) | I2C data |
| Gyro SCL | A5 (SCL) | I2C clock |
| Battery Monitor | A0 | Through voltage divider |

### Step 2: Run Setup Program (10 min)

1. Open `setup/setup.ino` in Arduino IDE
2. Upload to Arduino
3. Open Serial Monitor (57600 baud)
4. Follow the interactive setup wizard:
   - It will detect your gyroscope automatically
   - Move sticks as instructed to map channels
   - Lift and rotate quadcopter as prompted
   - Keep quadcopter level during gyro calibration

**Expected Output:** "Setup is finished" message

### Step 3: Calibrate ESCs (10 min)

1. **Disconnect battery from ESCs**
2. Open `esc_calibrate/esc_calibrate.ino`
3. Upload to Arduino
4. Follow calibration procedure:
   - Set throttle to maximum
   - Connect battery
   - Wait for ESC beeps
   - Lower throttle to minimum
   - ESCs will beep to confirm

**Test Motors:** Send `1`, `2`, `3`, or `4` via Serial Monitor to test each motor

### Step 4: Upload Flight Controller (5 min)

1. Open `Flight_controller/Flight_controller.ino`
2. **Optional:** Adjust PID values (default values work for most builds)
3. Upload to Arduino
4. Wait for LED to stop blinking (gyro calibration complete)

### Step 5: First Test Flight

1. **Arm motors:**
   - Throttle stick: minimum
   - Yaw stick: full left
   - Wait for motors to spin slowly
   - Center yaw stick

2. **Test hover:**
   - Slowly increase throttle
   - Make small adjustments
   - Keep quadcopter in sight

3. **Disarm motors:**
   - Lower throttle to minimum
   - Yaw stick: full right
   - Motors will stop

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Setup fails | Check I2C connections, ensure 16MHz Arduino |
| Motors won't arm | Verify throttle at minimum, run setup again |
| Drifts to one side | Recalibrate gyro, keep level during startup |
| Unstable hover | Reduce P gain by 0.1, test again |
| Motors spin at different speeds | Balance propellers, calibrate ESCs again |

## Quick Reference

### Serial Commands (ESC Calibrate Mode)
- `r` - Show receiver signals
- `a` - Show angles
- `1`-`4` - Test individual motors
- `5` - Test all motors

### PID Tuning Workflow
1. Start with default values
2. If oscillates: reduce P gain
3. If slow response: increase P gain
4. If drift over time: increase I gain
5. If overshoots: increase D gain

### LED Indicators
- **Solid on startup** - Waiting for receiver
- **Blinking** - Calibrating gyro
- **Off** - Ready to fly
- **On during flight** - Loop time error

## Default PID Values

```cpp
Roll/Pitch:  P=1.3  I=0.04  D=18.0
Yaw:         P=4.0  I=0.02  D=0.0
```

## Next Steps

- Read full [README.md](README.md) for detailed information
- Visit www.brokking.net for video tutorials
- Join online communities for support
- Practice in safe, open areas

---

**Remember:** 
- ✅ Always test without propellers first
- ✅ Keep quadcopter level during gyro calibration
- ✅ Fly in open areas away from people
- ✅ Start with low throttle
- ✅ Have fun and fly safe!

Modified by: **Risabh**
