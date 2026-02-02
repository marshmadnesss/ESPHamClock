# ESPHamClock (Community Mirror)

ESPHamClock is an ESP-based implementation of **HamClock**, a widely used amateur radio clock and situational awareness display.

This repository is a **community-maintained mirror** of the ESPHamClock source code, preserved under the original MIT license to ensure continued availability, transparency, and community contribution.

---

## 🕊 In Memoriam

This project is dedicated to the memory of  
**Elwood Downey, WB0OEW**

Elwood was the creator of HamClock and a tremendous contributor to the amateur radio community.  
His work helped thousands of operators better understand propagation, timing, and global radio conditions.

This repository exists to **preserve his work**, honor his contributions, and ensure the community can continue to learn from and build upon what he created.

---

## 📡 About ESPHamClock

ESPHamClock is a **client application**. It aggregates and visualizes information from multiple **independent, public, and community-run data sources**, including:

- DX Cluster nodes (ham-run, distributed)
- NTP servers for accurate timekeeping
- NOAA / NASA space weather feeds
- Public amateur radio reference services
- Optional GPS hardware (via gpsd)

> **There is no single central backend server required for ESPHamClock to operate.**

If any individual external data source becomes unavailable, only the related feature may degrade; the application itself continues to function.

---

## 🧠 Clarifying a Common Misconception

Some users have expressed concern that ESPHamClock depends on a single author-operated backend server.

**This is not the case.**

- ESPHamClock does **not** require a proprietary server to run
- It does **not** authenticate, license, or “phone home”
- DX Cluster data comes from **independent, volunteer-run cluster nodes**
- Time synchronization uses standard **NTP pools**
- Solar and propagation data comes from **public scientific institutions**

The original author hosted **distribution and support infrastructure** (such as downloads and documentation), but the runtime operation of ESPHamClock does **not** depend on that infrastructure.

---

## 📦 What This Repository Is

- A preserved, open-source copy of ESPHamClock
- A place for community review and contribution
- A neutral, factual reference for how the software works
- A long-term download source for users

## ❌ What This Repository Is Not

- It is not a fork claiming authorship
- It is not a replacement for Elwood’s contributions
- It is not a commercial or centralized service

---

## 🛠 Building & Flashing

> (Existing build instructions remain unchanged from the original source.)

Please refer to the original documentation within this repository for:
- Supported ESP hardware
- Display compatibility
- Arduino IDE configuration
- Flashing instructions

Community improvements to documentation are welcome.

---

## 📥 Installation (Debian / Ubuntu / Raspberry Pi OS)

### Update system:
`sudo apt update`

### Install dependencies:

`sudo apt install -y git build-essential g++ make libx11-dev gpsd gpsd-clients`

### Download ESPHamClock:
`git clone https://github.com/marshmadnesss/ESPHamClock.git`

### Go to ESPHamClock directory:
`cd ESPHamClock`

### If the system has a desktop (X11):
`make hamclock-800x480
./hamclock-800x480`

### If the system is Raspberry Pi OS headless / Lite:
`make hamclock-fb0-800x480
./hamclock-fb0-800x480`

## *OPTIONAL* Run on boot
### Create a systemd service file:
`sudo nano /etc/systemd/system/hamclock.service`

### Paste THIS exactly (headless / fb0):
```bash
[Unit]
Description=HamClock
After=network-online.target
Wants=network-online.target

[Service]
Type=simple
User=pi
WorkingDirectory=/home/pi/ESPHamClock
ExecStart=/home/pi/ESPHamClock/hamclock-fb0-800x480
Restart=always
RestartSec=5
StandardOutput=journal
StandardError=journal

[Install]
WantedBy=multi-user.target
```

### Important Notes

`User=pi` → change if you use a different user

Path assumes:`=
`/home/pi/ESPHamClock/hamclock-fb0-800x480`

No X11, no desktop, no login required

Ctrl+O, Enter
Ctrl+X

### Enable the service:
`sudo systemctl daemon-reexec`
`sudo systemctl daemon-reload`
`sudo systemctl enable hamclock`

### Start it now (no reboot needed):
`sudo systemctl start hamclock`

### Test reboot behavior (recommended):
`sudo reboot`

After reboot:
Pi boots
HamClock launches automatically
No login
No commands needed

## Useful management commands

### Check Status:
`systemctl status hamclock`



