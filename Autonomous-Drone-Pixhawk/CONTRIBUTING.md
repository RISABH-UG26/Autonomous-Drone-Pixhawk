# Contributing to Flight Controller

Thank you for your interest in contributing to the Flight Controller project! 🚁

## How to Contribute

### Reporting Bugs

If you find a bug, please create an issue with the following information:

- **Clear title**: Describe the issue briefly
- **Description**: Detailed explanation of the problem
- **Steps to reproduce**: How to recreate the bug
- **Expected behavior**: What should happen
- **Actual behavior**: What actually happens
- **Hardware setup**: Arduino version, gyroscope type, ESCs used
- **Software version**: Which version
- **Serial output**: Any relevant error messages or logs

### Suggesting Enhancements

We welcome suggestions for improvements! Please include:

- **Use case**: Why this enhancement would be useful
- **Description**: Detailed explanation of the feature
- **Implementation ideas**: How it might work (optional)
- **Alternatives considered**: Other approaches you've thought about

### Submitting Code Changes

#### Before You Start

1. Check existing issues and pull requests to avoid duplicates
2. For major changes, open an issue first to discuss
3. Make sure you can test your changes safely
4. Keep safety as the top priority

#### Code Guidelines

**Safety First:**
- Never compromise safety features
- Add warnings for potentially dangerous changes
- Test thoroughly without propellers first

**Code Style:**
- Follow existing code formatting
- Use descriptive variable names
- Add comments for complex logic
- Keep functions focused and small

**Arduino Specific:**
- Maintain 250Hz loop timing
- Be mindful of memory usage (Arduino Uno has limited RAM)
- Use appropriate data types
- Avoid floating-point operations where possible
- Test on actual hardware

#### Pull Request Process

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Make your changes**
   - Write clear, commented code
   - Test thoroughly on hardware
   - Update documentation if needed

4. **Commit your changes**
   ```bash
   git commit -m "Add: Brief description of changes"
   ```
   Use prefixes:
   - `Add:` for new features
   - `Fix:` for bug fixes
   - `Update:` for improvements
   - `Refactor:` for code restructuring
   - `Docs:` for documentation changes

5. **Push to your fork**
   ```bash
   git push origin feature/your-feature-name
   ```

6. **Create a Pull Request**
   - Describe what changes you made and why
   - Reference any related issues
   - Include test results
   - Add photos/videos of testing if relevant

### Testing Guidelines

**Essential Tests:**
- [ ] Code compiles without warnings
- [ ] Setup program completes successfully
- [ ] ESC calibration works correctly
- [ ] Motors respond properly (without props!)
- [ ] PID loops remain stable
- [ ] Loop timing stays at 4000μs
- [ ] All safety features work

**Flight Tests (if applicable):**
- [ ] Stable hover
- [ ] Responds correctly to all stick inputs
- [ ] Auto-level works properly
- [ ] Arming/disarming functions correctly
- [ ] No unexpected behavior

## Development Setup

### Required Hardware
- Arduino Uno (16MHz)
- MPU-6050 gyroscope (or compatible)
- RC receiver (4+ channels)
- 4x ESCs
- 4x motors
- Power supply/battery

### Software Requirements
- Arduino IDE 1.8.0 or newer
- Wire library (included)
- EEPROM library (included)

### Project Structure
```
Flight_Controller/
├── setup/                      # Initial configuration
├── esc_calibrate/              # ESC calibration
├── Flight_controller/          # Main flight controller
├── README.md                   # Project documentation
├── QUICKSTART.md               # Quick setup guide
├── CHANGELOG.md                # Version history
├── LICENSE                     # MIT License
└── CONTRIBUTING.md             # This file
```

## Code Review Process

Pull requests will be reviewed for:

1. **Safety**: Does it maintain or improve safety?
2. **Functionality**: Does it work as intended?
3. **Code quality**: Is it well-written and documented?
4. **Testing**: Has it been tested thoroughly?
5. **Documentation**: Are docs updated if needed?

## Areas for Contribution

### High Priority
- Bug fixes
- Documentation improvements
- Test result sharing
- Hardware compatibility testing

### Medium Priority
- Code optimization
- Additional safety features
- Better error handling
- Performance improvements

### Future Features
- GPS integration
- Altitude hold
- Position hold
- Telemetry support
- Flight data logging

## Communication

- **Issues**: For bugs and feature requests
- **Pull Requests**: For code contributions
- **Discussions**: For questions and general chat
- **Original Source**: www.brokking.net for foundational questions

## Recognition

Contributors will be acknowledged in:
- CHANGELOG.md for significant contributions
- Code comments for specific implementations
- Project documentation where appropriate

## Questions?

If you have questions about contributing:
1. Check existing documentation
2. Search closed issues
3. Open a new issue with the "question" label
4. Visit www.brokking.net for original project support

## Code of Conduct

### Our Standards

- Be respectful and professional
- Welcome newcomers
- Focus on constructive feedback
- Share knowledge freely
- Prioritize safety above all

### Unacceptable Behavior

- Harassment or discrimination
- Trolling or insulting comments
- Publishing others' private information
- Encouraging unsafe practices

## Thank You!

Your contributions help make quadcopter flight controllers more accessible and safer for everyone. Every bug report, documentation improvement, and code contribution matters!

**Happy coding and safe flying!** 🚁

---

**Project Maintainer:** Risabh  
**Original Creator:** Joop Brokking (www.brokking.net)
