# Project Information

## Flight Controller
**Arduino-based Multicopter Flight Controller**

### Project Stats

- **Language**: Arduino C/C++
- **Platform**: Arduino Uno (ATmega328P)
- **Version**: 1.4 (Modified)
- **License**: MIT
- **Status**: Active
- **Maintained by**: Risabh
- **Original Creator**: Joop Brokking

### Quick Links

📚 **Documentation**
- [Main README](README.md) - Complete project documentation
- [Quick Start Guide](QUICKSTART.md) - Get flying in 30 minutes
- [Changelog](CHANGELOG.md) - Version history
- [Contributing](CONTRIBUTING.md) - How to contribute

🛠️ **Code**
- [Setup Program](setup/) - Initial configuration
- [ESC Calibration](esc_calibrate/) - Calibrate your ESCs
- [Flight Controller](Flight_controller/) - Main flight code

⚙️ **Configuration**
- [License](LICENSE) - MIT License with safety disclaimer
- [.gitignore](.gitignore) - Git ignore rules

### Hardware Compatibility

| Component | Supported Models |
|-----------|------------------|
| **Microcontroller** | Arduino Uno (ATmega328P @ 16MHz) |
| **Gyroscope** | MPU-6050 (recommended), L3G4200D, L3GD20H |
| **RC Receiver** | Any PWM receiver (4+ channels) |
| **ESCs** | Standard PWM ESCs (1000-2000μs) |
| **Motors** | Brushless DC motors |

### Key Features

✅ **Flight Control**
- PID-based stabilization
- Auto-level mode
- Manual (rate) mode
- 250Hz control loop
- Battery compensation

✅ **Setup & Configuration**
- Interactive setup wizard
- Automatic gyroscope detection
- Channel mapping
- ESC calibration tools

✅ **Safety**
- Motor arming sequences
- Loop time monitoring
- Battery voltage alerts
- Comprehensive warnings

### Performance Specs

| Specification | Value |
|--------------|-------|
| Loop Frequency | 250 Hz (4ms) |
| Gyro Range | ±500°/s |
| Accelerometer Range | ±8g |
| PWM Resolution | 1μs |
| I2C Speed | 400 kHz |
| Response Time | ~16ms |

### PID Default Values

```cpp
Roll/Pitch:
  P = 1.3
  I = 0.04
  D = 18.0
  Max = ±400

Yaw:
  P = 4.0
  I = 0.02
  D = 0.0
  Max = ±400
```

### Repository Statistics

- **Files**: 3 main programs
- **Lines of Code**: ~2000+
- **Functions**: 20+
- **Supported Gyros**: 3 types
- **Languages**: C/C++ (Arduino)

### Development Timeline

```
July 2016    ► v1.0 - Initial Release
July 2016    ► v1.1 - NaN Error Fix
July 2016    ► v1.2 - Enhanced NaN Prevention
October 2016 ► v1.3 - IDE Compatibility
April 2017   ► v1.4 - Serial Buffer Fix
October 2025 ► Modified - Enhanced Documentation
```

### Community

🌐 **Resources**
- Original Project: [www.brokking.net](http://www.brokking.net)
- Video Tutorials: YouTube
- Support Forum: brokking.net Q&A

🤝 **Contributing**
We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### Project Structure

```
Flight_Controller/
│
├── 📁 setup/
│   └── 🔧 Initial configuration and gyro setup
│
├── 📁 esc_calibrate/
│   └── ⚡ ESC calibration and motor testing
│
├── 📁 Flight_controller/
│   └── 🚁 Main flight control program
│
├── 📄 README.md
│   └── Complete project documentation
│
├── 📄 QUICKSTART.md
│   └── 30-minute setup guide
│
├── 📄 CHANGELOG.md
│   └── Version history and updates
│
├── 📄 CONTRIBUTING.md
│   └── Contribution guidelines
│
├── 📄 LICENSE
│   └── MIT License + Safety disclaimer
│
└── 📄 .gitignore
    └── Git ignore configuration
```

### Safety Reminders

⚠️ **Always:**
- Remove propellers for testing
- Test in open areas
- Check battery voltage
- Calibrate before flight
- Follow local regulations

❌ **Never:**
- Fly near people
- Test indoors with props
- Ignore warnings
- Skip calibration
- Fly with low battery

### Getting Help

1. Check [README.md](README.md) for documentation
2. Review [QUICKSTART.md](QUICKSTART.md) for setup help
3. Search existing issues
4. Visit www.brokking.net for tutorials
5. Create a new issue if needed

---

**Made with ❤️ for the drone community**

*Fly safe, fly smart!* 🚁
