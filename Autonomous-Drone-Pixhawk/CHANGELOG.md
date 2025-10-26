# Changelog

All notable changes to the Flight Controller project will be documented in this file.

## [Modified Version] - 2025-10-25

### Changed by Risabh
- Complete project documentation overhaul
- Added comprehensive GitHub README with detailed features and specifications
- Enhanced code header comments with clear descriptions
- Created Quick Start Guide for faster setup
- Improved code documentation and inline comments
- Updated safety warnings throughout all files

### Maintained
- All core flight control functionality
- PID control algorithms
- Gyroscope/accelerometer fusion
- Motor control and ESC interface
- Safety features and arming sequences

---

## [1.4] - 2017-04-30

### Fixed
- ESC calibration sketch now properly handles serial buffer
- Fixed issue where program stops when multiple characters are sent via serial monitor
- Added delay and buffer clearing to handle line feed characters from various Arduino IDE versions

### Changed
- Serial read implementation in ESC calibration program
```cpp
data = Serial.read();
delay(100);
while(Serial.available() > 0)loop_counter = Serial.read();
```

---

## [1.3] - 2016-10-30

### Fixed
- Setup program hanging with newer Arduino IDE versions (1.6.x and up)
- Fixed compiler optimization issues

### Changed
- Reduced starting speed of motors to 1100μs (from higher value)
- Better compatibility with modern Arduino IDE

### Added
- New PDF schematic for hardware connections

---

## [1.2] - 2016-07-12

### Fixed
- Complete NaN problem resolution in angle calculations
- Enhanced bounds checking for accelerometer values
- Prevented division by zero in angle calculations

### Changed
- Improved asin function input validation:
```cpp
if(abs(acc_y) < acc_total_vector){
  angle_pitch_acc = asin((float)acc_y/acc_total_vector)* 57.296;
}
if(abs(acc_x) < acc_total_vector){
  angle_roll_acc = asin((float)acc_x/acc_total_vector)* -57.296;
}
```

---

## [1.1] - 2016-07-11

### Fixed
- NaN (Not a Number) error during aggressive flight maneuvers
- Quadcopter becoming uncontrollable during fast descents
- Issue where asin function received values greater than 1

### Changed
- Added boundary checks for accelerometer calculations
```cpp
if(acc_y > acc_total_vector){
  angle_pitch_acc = asin((float)acc_y/acc_total_vector)* 57.296;
}
if(acc_x > acc_total_vector){
  angle_roll_acc = asin((float)acc_x/acc_total_vector)* -57.296;
}
```

### Known Issues at Release
- Boundary check logic was incomplete (fixed in v1.2)

---

## [1.0] - 2016-07-03

### Added - Initial Release
- Complete flight controller implementation
- PID control for roll, pitch, and yaw axes
- Auto-level mode using complementary filter
- Support for MPU-6050, L3G4200D, and L3GD20H gyroscopes
- RC receiver channel mapping and calibration
- ESC control and calibration routines
- Battery voltage monitoring
- Motor arming/disarming sequences
- 250Hz control loop frequency
- EEPROM configuration storage
- Interactive setup program
- LED status indicators
- Safety features and failsafes

### Technical Specifications
- Control frequency: 250Hz (4ms loop time)
- Gyroscope range: ±500°/s
- Accelerometer range: ±8g
- PWM output: 1000-2000μs
- I2C clock: 400kHz
- Complementary filter for angle estimation
- PID controller with anti-windup

---

## Version Comparison

| Version | Key Feature | Status |
|---------|-------------|--------|
| 1.0 | Initial release | Stable |
| 1.1 | Basic NaN fix | Superseded |
| 1.2 | Complete NaN fix | Stable |
| 1.3 | IDE compatibility | Stable |
| 1.4 | Serial buffer fix | Current Release |
| Modified | Enhanced documentation | Current |

---

## Future Improvements (Planned)

Potential enhancements for future versions:
- [ ] GPS hold functionality
- [ ] Return to home feature
- [ ] Telemetry support
- [ ] Altitude hold mode
- [ ] Position hold mode
- [ ] Headless mode
- [ ] Multiple flight modes
- [ ] Real-time PID tuning via serial
- [ ] Flight data logging
- [ ] Improved failsafe mechanisms

---

## Notes

- This project is community-driven and open for contributions
- Always test thoroughly with propellers removed
- Report bugs and issues through the project repository
- For support, visit www.brokking.net

---

**Maintained by:** Risabh  
**Original Creator:** Joop Brokking (www.brokking.net)
