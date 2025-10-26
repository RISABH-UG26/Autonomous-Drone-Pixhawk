# MAVLink Setup for Raspberry Pi Zero 2W

A complete guide for installing and configuring MAVLink communication on Raspberry Pi Zero 2W for drone/flight controller interfacing.

## 📋 Overview

This guide walks you through setting up MAVLink (Micro Air Vehicle Link) communication protocol on a Raspberry Pi Zero 2W. MAVLink enables communication between ground control stations, drones, and other autonomous vehicles.

## 🎯 What is MAVLink?

MAVLink is a lightweight messaging protocol for communicating with drones and between onboard drone components. It's used by popular flight controllers like:
- ArduPilot
- PX4
- PIXHAWK
- And many others

## 🛠️ Hardware Requirements

- **Raspberry Pi Zero 2W** (or compatible Pi models)
- **Flight Controller** with UART/Serial output (e.g., Pixhawk, ArduPilot)
- **MicroSD Card** (8GB+ recommended)
- **Power Supply** (5V, 2.5A recommended)
- **Serial Connection Cable** (UART to flight controller)

### Pin Connections

| Raspberry Pi Zero 2W | Flight Controller |
|----------------------|-------------------|
| GPIO14 (TXD) - Pin 8 | RX (TELEM port) |
| GPIO15 (RXD) - Pin 10 | TX (TELEM port) |
| GND - Pin 6 | GND |

> ⚠️ **Warning**: Do NOT connect 5V pins between devices unless voltage levels are compatible!

## 🚀 Installation Steps

### Step 1: Install Python PIP

First, ensure Python 3 and pip are installed:

```bash
sudo apt install python3-pip
```

**What this does:**
- Installs the Python package manager (pip3)
- Required for installing Python-based MAVLink tools
- Updates system package lists

**Expected output:**
```
Reading package lists... Done
Building dependency tree... Done
python3-pip is already the newest version (x.x.x)
```

---

### Step 2: Install MAVProxy

Install MAVProxy, a powerful MAVLink ground control station:

```bash
pip3 install MAVProxy
```

**What this does:**
- Downloads and installs MAVProxy and its dependencies
- Installs MAVLink Python libraries
- Sets up command-line tools for drone communication

**Expected output:**
```
Collecting MAVProxy
  Downloading MAVProxy-x.x.x.tar.gz
Successfully installed MAVProxy-x.x.x pymavlink-x.x.x
```

**Installation location:** `~/.local/bin/mavproxy.py`

---

### Step 3: Test MAVProxy (First Attempt)

Try running MAVProxy with the default path:

```bash
mavproxy.py --master=/dev/serial0 --baudrate 921600
```

**Parameters explained:**
- `--master=/dev/serial0` - Serial port on Raspberry Pi GPIO
- `--baudrate 921600` - Communication speed (bits per second)

**If this fails with "command not found"**, proceed to Step 4.

---

### Step 4: Run MAVProxy with Full Path

If the command isn't in your PATH, use the full path:

```bash
~/.local/bin/mavproxy.py --master=/dev/serial0 --baudrate 921600
```

**What this does:**
- Runs MAVProxy directly from installation directory
- Connects to flight controller via serial port
- Establishes MAVLink communication at 921600 baud

**Expected output (if successful):**
```
Connect /dev/serial0 source_system=255
Loaded module console
Loaded module map
MAV> 
```

---

### Step 5: Add MAVProxy to PATH (Permanent Fix)

To run `mavproxy.py` from anywhere, add it to your system PATH:

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
```

**What this does:**
- Adds `~/.local/bin` to your PATH environment variable
- Appends the export command to `.bashrc` (runs on every terminal start)
- Makes MAVProxy accessible from any directory

**Verification:**
```bash
cat ~/.bashrc | grep "local/bin"
```

You should see:
```bash
export PATH="$HOME/.local/bin:$PATH"
```

---

### Step 6: Reload Configuration

Apply the PATH changes to your current session:

```bash
source ~/.bashrc
```

**What this does:**
- Reloads the `.bashrc` configuration file
- Applies PATH changes immediately
- No need to logout/login or reboot

**Alternative:** Close and reopen your terminal

---

### Step 7: Run MAVProxy (Final Test)

Now you should be able to run MAVProxy from anywhere:

```bash
mavproxy.py --master=/dev/serial0 --baudrate 921600
```

**Success indicators:**
- MAVProxy console appears
- Connection to flight controller established
- Receiving heartbeat messages
- Can send commands

---

## 🔧 Configuration Options

### Common Baud Rates

| Baud Rate | Use Case | Notes |
|-----------|----------|-------|
| 57600 | Standard telemetry | Most common, reliable |
| 115200 | Fast telemetry | Good balance |
| 921600 | High-speed | Best for short cables |

**Change baud rate:**
```bash
mavproxy.py --master=/dev/serial0 --baudrate 57600
```

### Serial Port Options

| Port | Description |
|------|-------------|
| `/dev/serial0` | GPIO serial (default) |
| `/dev/ttyAMA0` | Primary UART |
| `/dev/ttyUSB0` | USB serial adapter |

### Advanced MAVProxy Options

```bash
# Add secondary output (e.g., for GCS)
mavproxy.py --master=/dev/serial0 --baudrate 921600 --out=udp:192.168.1.100:14550

# Enable specific modules
mavproxy.py --master=/dev/serial0 --baudrate 921600 --load-module=terrain,rally

# Set aircraft type
mavproxy.py --master=/dev/serial0 --baudrate 921600 --aircraft=MyDrone
```

---

## 📊 Complete Setup Script

Run all commands in sequence:

```bash
#!/bin/bash
# MAVLink Setup Script for Raspberry Pi Zero 2W
# Modified by: Risabh

echo "Installing Python pip..."
sudo apt install python3-pip -y

echo "Installing MAVProxy..."
pip3 install MAVProxy

echo "Adding MAVProxy to PATH..."
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc

echo "Reloading configuration..."
source ~/.bashrc

echo "Testing MAVProxy connection..."
echo "Starting MAVProxy with 921600 baud rate..."
mavproxy.py --master=/dev/serial0 --baudrate 921600
```

**Save as:** `mavlink_setup.sh`

**Make executable:**
```bash
chmod +x mavlink_setup.sh
```

**Run:**
```bash
./mavlink_setup.sh
```

---

## ⚙️ Raspberry Pi Configuration

### Enable Serial Port

1. **Open Raspberry Pi Configuration:**
   ```bash
   sudo raspi-config
   ```

2. **Navigate to:**
   - `3 Interface Options`
   - `I6 Serial Port`

3. **Configure:**
   - "Would you like a login shell accessible over serial?" → **No**
   - "Would you like the serial port hardware enabled?" → **Yes**

4. **Reboot:**
   ```bash
   sudo reboot
   ```

### Disable Serial Console (Important!)

Edit boot configuration:
```bash
sudo nano /boot/cmdline.txt
```

**Remove** this text if present:
```
console=serial0,115200
```

**Save:** `Ctrl+O`, `Enter`, `Ctrl+X`

### Verify Serial Port

Check if serial port is available:
```bash
ls -l /dev/serial0
```

**Expected output:**
```
lrwxrwxrwx 1 root root 5 Oct 25 12:00 /dev/serial0 -> ttyAMA0
```

---

## 🧪 Testing & Troubleshooting

### Test 1: Check MAVProxy Installation

```bash
pip3 show MAVProxy
```

**Expected output:**
```
Name: MAVProxy
Version: x.x.x
Location: /home/pi/.local/lib/python3.x/site-packages
```

### Test 2: Check Serial Port

```bash
# Test if port is accessible
sudo cat /dev/serial0
```

Press `Ctrl+C` to stop. If no errors, port is working.

### Test 3: Monitor Serial Traffic

```bash
# Install screen
sudo apt install screen

# Monitor serial port
screen /dev/serial0 921600
```

You should see MAVLink binary data if the flight controller is transmitting.

### Test 4: Verify PATH

```bash
echo $PATH | grep ".local/bin"
```

Should show `.local/bin` in the path.

---

## 🐛 Common Issues & Solutions

### Issue 1: "mavproxy.py: command not found"

**Solution:**
```bash
# Use full path
~/.local/bin/mavproxy.py --master=/dev/serial0 --baudrate 921600

# OR add to PATH
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

### Issue 2: "Permission denied: /dev/serial0"

**Solution:**
```bash
# Add user to dialout group
sudo usermod -a -G dialout $USER

# Logout and login again, or:
sudo reboot
```

### Issue 3: "No heartbeat packets received"

**Possible causes:**
- Wrong baud rate (try 57600 or 115200)
- Incorrect wiring (swap TX/RX)
- Flight controller not powered
- Serial console not disabled

**Solution:**
```bash
# Try different baud rates
mavproxy.py --master=/dev/serial0 --baudrate 57600
mavproxy.py --master=/dev/serial0 --baudrate 115200
```

### Issue 4: "Port already in use"

**Solution:**
```bash
# Check what's using the port
sudo lsof /dev/serial0

# Kill the process (replace PID)
sudo kill -9 [PID]
```

### Issue 5: ImportError or Module Not Found

**Solution:**
```bash
# Reinstall MAVProxy
pip3 uninstall MAVProxy
pip3 install MAVProxy --upgrade

# Check Python version (needs 3.7+)
python3 --version
```

---

## 📡 MAVProxy Basic Commands

Once connected, you can use these commands in the MAVProxy console:

### Essential Commands

```bash
# Check mode
mode

# Arm motors (DANGEROUS - props off!)
arm throttle

# Disarm motors
disarm

# Change flight mode
mode STABILIZE
mode LOITER
mode AUTO

# View parameters
param show *

# Set parameter
param set PARAM_NAME value

# Reboot flight controller
reboot

# Exit MAVProxy
exit
```

### Information Commands

```bash
# Show status
status

# Show GPS info
gps

# Show battery info
battery

# Show all modules
module list

# Load a module
module load terrain
```

---

## 🌐 Remote GCS Connection

Forward MAVLink to a Ground Control Station (GCS) over network:

```bash
mavproxy.py --master=/dev/serial0 --baudrate 921600 \
  --out=udpout:192.168.1.100:14550
```

**Parameters:**
- `--out=udpout:IP:PORT` - Send data to this address
- Default GCS port: 14550 (Mission Planner, QGroundControl)

### Connect Multiple GCS

```bash
mavproxy.py --master=/dev/serial0 --baudrate 921600 \
  --out=udpout:192.168.1.100:14550 \
  --out=udpout:192.168.1.101:14550
```

---

## 🔒 Security Considerations

- **Never expose MAVLink directly to the internet** without encryption
- Use VPN for remote access
- Change default parameters on production systems
- Implement authentication if available
- Monitor for unauthorized connections

---

## 📚 Additional Resources

### Documentation
- [MAVLink Official Documentation](https://mavlink.io/)
- [MAVProxy Documentation](https://ardupilot.org/mavproxy/)
- [ArduPilot Documentation](https://ardupilot.org/)
- [PX4 Documentation](https://docs.px4.io/)

### Ground Control Stations
- **Mission Planner** (Windows)
- **QGroundControl** (Cross-platform)
- **APM Planner 2** (Cross-platform)
- **MAVProxy** (Command-line, all platforms)

### Community
- [ArduPilot Forum](https://discuss.ardupilot.org/)
- [DIY Drones Community](https://diydrones.com/)
- [PX4 Slack Channel](https://px4.io/community/)

---

## 🔄 Auto-Start on Boot (Optional)

Create a systemd service to start MAVProxy automatically:

### Create Service File

```bash
sudo nano /etc/systemd/system/mavproxy.service
```

### Add Configuration

```ini
[Unit]
Description=MAVProxy MAVLink Gateway
After=network.target

[Service]
Type=simple
User=pi
ExecStart=/home/pi/.local/bin/mavproxy.py --master=/dev/serial0 --baudrate 921600
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
```

### Enable Service

```bash
# Reload systemd
sudo systemctl daemon-reload

# Enable service
sudo systemctl enable mavproxy.service

# Start service
sudo systemctl start mavproxy.service

# Check status
sudo systemctl status mavproxy.service
```

### View Logs

```bash
# Real-time logs
sudo journalctl -u mavproxy.service -f

# Recent logs
sudo journalctl -u mavproxy.service -n 50
```

---

## 📈 Performance Tips

### Optimize for Raspberry Pi Zero 2W

1. **Reduce CPU load:**
   ```bash
   # Disable unnecessary services
   sudo systemctl disable bluetooth
   sudo systemctl disable wifi
   ```

2. **Use lower baud rates for stability:**
   - 57600 or 115200 for long-term reliability

3. **Monitor system resources:**
   ```bash
   top
   htop  # Install with: sudo apt install htop
   ```

4. **Keep system updated:**
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

---

## ✅ Quick Reference

### Command Summary

| Command | Purpose |
|---------|---------|
| `sudo apt install python3-pip` | Install Python package manager |
| `pip3 install MAVProxy` | Install MAVProxy |
| `~/.local/bin/mavproxy.py --master=/dev/serial0 --baudrate 921600` | Run MAVProxy (full path) |
| `echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc` | Add to PATH permanently |
| `source ~/.bashrc` | Reload configuration |
| `mavproxy.py --master=/dev/serial0 --baudrate 921600` | Run MAVProxy (after PATH setup) |

### Baud Rate Quick Switch

```bash
# 57600 baud
mavproxy.py --master=/dev/serial0 --baudrate 57600

# 115200 baud
mavproxy.py --master=/dev/serial0 --baudrate 115200

# 921600 baud (high-speed)
mavproxy.py --master=/dev/serial0 --baudrate 921600
```

---

## 🎯 Next Steps

After successful setup:

1. ✅ Test basic MAVLink communication
2. ✅ Configure flight controller parameters
3. ✅ Set up telemetry forwarding to GCS
4. ✅ Implement auto-start (optional)
5. ✅ Configure WiFi for wireless operation
6. ✅ Test all flight modes safely
7. ✅ Document your specific configuration

---

## ⚠️ Safety Reminders

- **Always remove propellers** when testing
- Test MAVLink commands with motors disarmed
- Verify all connections before powering flight controller
- Keep emergency stop procedures ready
- Follow local aviation regulations
- Never fly over people or property without permission

---

## 📝 Version History

| Date | Version | Changes |
|------|---------|---------|
| Oct 25, 2025 | 1.0 | Initial documentation by Risabh |

---

## 👤 Author

**Modified and documented by:** Risabh  
**Date:** October 25, 2025

---

## 📄 License

This documentation is provided as-is for educational and personal use.

**Disclaimer:** Working with flight controllers and drones carries risks. Always follow safety guidelines, local regulations, and manufacturer instructions. The author is not responsible for any damage, injury, or loss resulting from the use of this information.

---

**Happy Flying! 🚁**

*Remember: Safety first, test thoroughly, and always fly responsibly.*
