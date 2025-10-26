# Flight Controller

An Arduino-based multicopter flight controller system with auto-leveling capabilities, designed for DIY quadcopter enthusiasts.

> **⚠️ LEGACY VERSION NOTICE**
> 
> This repository contains the **previous version** of the flight controller system that used **Arduino Uno** as the flight controller. 
> 
> **Current Version (New):**
> - **Flight Controller**: Pixhawk 2.4.8
> - **Flight Computer**: Raspberry Pi Zero 2W
> - **Firmware**: Mission Planner (ArduPilot)
> - **Communication**: MAVLink protocol
> 
> This Arduino-based code is maintained for reference, learning purposes, and those who prefer the simpler Arduino platform.

## 📋 Project Overview

This is a complete flight control system that transforms an Arduino into a capable quadcopter flight controller. It features PID-based stabilization, gyroscope/accelerometer fusion, and support for standard RC receivers and ESCs.

## ✨ Features

- **Auto-Level Mode**: Automatic stabilization using gyroscope and accelerometer data fusion
- **PID Control**: Tunable PID controllers for roll, pitch, and yaw axes
- **Multiple Gyro Support**: Compatible with MPU-6050, L3G4200D, and L3GD20H
- **ESC Calibration**: Built-in ESC calibration routine
- **Receiver Configuration**: Flexible receiver channel mapping
- **Battery Monitoring**: Real-time battery voltage monitoring with compensation
- **Safety Features**: Motor arming/disarming sequences and failsafe mechanisms

## 🛠️ Hardware Requirements

### Essential Components
- **Microcontroller**: Arduino Uno (ATmega328P @ 16MHz)
- **Gyroscope/Accelerometer**: MPU-6050 (recommended), L3G4200D, or L3GD20H
- **RC Receiver**: Any 4+ channel receiver (PWM output)
- **ESCs**: 4x brushless ESCs (compatible with standard PWM signals)
- **Motors**: 4x brushless motors
- **Battery**: LiPo battery (3S recommended)
- **Frame**: Quadcopter frame (any X-configuration)

### Pin Connections
- **Digital Pin 4-7**: ESC control signals (Motor 1-4)
- **Digital Pin 8-11**: RC receiver inputs (Roll, Pitch, Throttle, Yaw)
- **Digital Pin 12**: Status LED
- **Analog Pin 0**: Battery voltage monitor
- **I2C Pins (A4/A5)**: Gyroscope/Accelerometer communication

## 📦 Software Components

### 1. Setup
Initial configuration program that:
- Detects and configures the gyroscope
- Maps RC receiver channels
- Calibrates gyroscope offsets
- Verifies hardware connections
- Stores configuration to EEPROM

### 2. ESC Calibrate
ESC calibration utility that:
- Calibrates all ESCs simultaneously
- Tests individual motor vibrations
- Displays receiver signals
- Shows quadcopter angles

### 3. Flight Controller
Main flight control program featuring:
- 250Hz refresh rate for precise control
- Complementary filter for angle estimation
- PID control loops for stabilization
- Auto-level and manual (rate) mode
- Battery voltage compensation

## 🚀 Getting Started

### Installation Steps

1. **Hardware Assembly**
   - Assemble your quadcopter frame
   - Mount the Arduino and connect all components according to pin configuration
   - Ensure proper motor rotation (CW/CCW pattern)

2. **Upload Setup Program**
   ```
   Open setup/setup.ino in Arduino IDE
   Upload to Arduino
   Open Serial Monitor (57600 baud)
   Follow on-screen instructions
   ```

3. **Calibrate ESCs**
   ```
   Open esc_calibrate/esc_calibrate.ino
   Upload to Arduino
   Follow ESC calibration procedure
   Test each motor individually
   ```

4. **Upload Flight Controller**
   ```
   Open Flight_controller/Flight_controller.ino
   Adjust PID values if needed (see Configuration section)
   Upload to Arduino
   ```

### First Flight Checklist
- [ ] All setup steps completed successfully
- [ ] ESCs calibrated and motors spinning correctly
- [ ] Propellers removed for testing
- [ ] Battery fully charged
- [ ] Open area for flight testing
- [ ] Gyroscope calibrated (don't move quad during startup)
- [ ] Transmitter properly bound to receiver

## ⚙️ Configuration

### PID Tuning (in Flight_controller.ino)

```cpp
// Roll/Pitch PID Settings
float pid_p_gain_roll = 1.3;    // Proportional gain
float pid_i_gain_roll = 0.04;   // Integral gain
float pid_d_gain_roll = 18.0;   // Derivative gain
int pid_max_roll = 400;         // Maximum output

// Yaw PID Settings
float pid_p_gain_yaw = 4.0;
float pid_i_gain_yaw = 0.02;
float pid_d_gain_yaw = 0.0;
int pid_max_yaw = 400;

// Auto-level Mode
boolean auto_level = true;      // Set to false for rate mode
```

### Motor Configuration

Motors must be connected in the following pattern:
```
    Front
  1 ▲ ▲ 4
   CCW CW
     X
   CW CCW
  2     3
    Rear
```

### Arming/Disarming
- **Arm Motors**: Throttle low + Yaw left, then center yaw
- **Disarm Motors**: Throttle low + Yaw right

## 📊 Technical Specifications

- **Control Loop Frequency**: 250Hz (4ms)
- **Gyroscope Range**: ±500°/s
- **Accelerometer Range**: ±8g
- **PWM Output Range**: 1000-2000μs
- **Minimum Throttle**: 1100μs (motors running)
- **I2C Clock Speed**: 400kHz

## 🔧 Troubleshooting

### LED Status Indicators
- **Solid ON during startup**: Waiting for valid receiver signals
- **Blinking**: Gyroscope calibration in progress
- **ON after startup**: Loop time exceeded 4050μs (check code modifications)
- **Blinking fast**: Low battery voltage detected

### Common Issues

1. **Motors won't arm**
   - Ensure throttle is at minimum
   - Check receiver signal quality
   - Verify EEPROM configuration (run setup again)

2. **Unstable flight**
   - Recalibrate gyroscope
   - Adjust PID values
   - Check motor directions and propeller orientation
   - Verify CG (center of gravity)

3. **Drift in one direction**
   - Recalibrate accelerometer offsets
   - Ensure quadcopter is level during gyro calibration
   - Check motor/propeller balance

## 📈 Version History

### Version 1.4 (April 30, 2017)
- Fixed ESC calibration sketch serial buffer handling
- Improved compatibility with Arduino IDE 1.6.x+

### Version 1.3 (October 30, 2016)
- Fixed compiler optimization issues with Arduino IDE 1.6.x+
- Reduced starting motor speed to 1100μs
- Added new PDF schematic

### Version 1.2 (July 12, 2016)
- Enhanced NaN prevention in angle calculations
- Improved asin function bounds checking

### Version 1.1 (July 11, 2016)
- Fixed NaN error during aggressive flight maneuvers
- Added boundary checks for accelerometer values

### Version 1.0 (July 3, 2016)
- Initial release

## ⚠️ Safety Warning

**IMPORTANT**: Always remove propellers when:
- Testing on the bench
- Calibrating ESCs
- Uploading new code
- Making adjustments
- Unless you are absolutely certain of what you're doing

Quadcopters can cause serious injury. Fly responsibly and follow local regulations.

## 🤝 Contributing

This is a modified version of the original project. Feel free to:
- Report bugs and issues
- Suggest improvements
- Submit pull requests
- Share your build experiences

## 📄 License

This software is provided "AS IS", without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose and noninfringement.

## 🔗 Resources

- **Original Project**: www.brokking.net
- **Video Tutorials**: Available on YouTube
- **Support Forums**: Q&A section at www.brokking.net

## 👤 Author

Modified and maintained by **Risabh**

---

**Happy Flying! 🚁**

*Remember: Safety first, remove props for testing, and always fly in open areas away from people and property.*
