# Edit as of 2/18/2026

Plans to have this repository work off of a new backend server is slotted to be live by 2/20/2026
That means this repository will not work off of Clear Sky Institutes backend and will be entirely dependent on a new and maintained backend. 
The backend for this repostiry is nearly a 1:1 working clone of Elwoods backened. There will be a PayPal contributions button added shortly if you would like to donate
to keep the server maintained and as we work to re-write Ham Clock to work independently. 

---

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

## 🧠 Clarifying 

### Some users have expressed concern that ESPHamClock depends on a single author-operated backend server.

This is sadly true

After the unfortunate incident occured from the author and creator of ESP Ham Clock, many in facebook groups and on reddit have been trying to skim the code (heavily C++ written) to see what exactly is being served on a backend that points to clearskyinstitute.com. 
This sadly is what serves as a centeralized node that takes all incoming live information that all ESP Ham Clock EUD's (End User Devices) take in. We are actively trying to build a new backbone infrustrstucture to make ESPHamClock more "open source"
and reduce reliance on a single node serving live time information to EUD's.
Currently, all live information served via clearskyinstitute.com will continue to run until June 2026. This currentl release of ESP HAM Clock (date 02/03/2026) will serve live information from clearskyinstitute.com until a new node is created to serve live info.
We are actively trying to rewrite all of ESPHamClock to not rely on a centeralized node for this information and that all information that was pushed to the centeral backend node will soon be opened to all Ham Clock EUD's. 

### DATE 2/10/2026
Live Spots for PSK reports is now working on the new backend server we are creating. We are still beta testing to make sure all data displayed is true, live, and accurate as time drifts can cause discrepencies. Please keep coming back to this github for more updates.

Again, it is on the drawing board to re-write this version of HAM Clock to not rely on a backend server for this information but after rebuilding one myself, I can see why it worked this way. As live PSK reports would come in, that data is ALOT...BUT...Its because my backend server is currently pulling GLOBAL PSK reports, and then HAM Clock is just filtering for your grid. So you are obviously only displayed PSK reports Live for your grid only, so - we will be writing it that based on the Grid you input on set up, it will only grab PSK reports for your grid only to write to your device and self purge and live reports older than 24hrs + 1m. 
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

## 📥 Installation (Debian12 / Ubuntu / Raspberry Pi (bookworm) OS)

### Update system:
`sudo apt update`

### Install dependencies:

`sudo apt install -y git build-essential g++ make libx11-dev gpsd gpsd-clients`

### Download ESPHamClock:
`git clone https://github.com/marshmadnesss/ESPHamClock.git`

### Go to ESPHamClock directory:
`cd ESPHamClock`

### If the system has a desktop (X11):
`make clean`

`make -j 4 hamclock-800x480`

`sudo make install`

### Run HamClock
`hamclock &`

### If the system is Debian12/Ubuntu/PiOS(bookworm) *headless* / *Lite* (CLI Only):
`make clean`

`make -j 4 FB_DEPTH=16 hamclock-fb0-800x480`

Note:
Supported fb0 build sizes:

`hamclock-fb0-800x480`

`hamclock-fb0-1600x960`

`hamclock-fb0-2400x1440`

`hamclock-fb0-3200x1920`

### Install the built binary
`sudo cp ./hamclock-fb0-800x480 /usr/local/bin/hamclock`

`sudo chown root:root /usr/local/bin/hamclock`

`sudo chmod 4755 /usr/local/bin/hamclock`

### Run HamClock
`hamclock`

## *OPTIONAL* Run on boot for headless/lite OS
### Create a systemd service file:
`sudo nano /etc/systemd/system/hamclock.service`

### Paste THIS exactly (headless / fb0):
```bash
[Unit]
Description=HamClock framebuffer display
After=multi-user.target

[Service]
ExecStart=/usr/local/bin/hamclock
Restart=always
User=root
Environment=HOME=/root

[Install]
WantedBy=multi-user.target
```


No X11, no desktop, no login required

Ctrl+O, Enter
Ctrl+X

### Enable the service:
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

## 📥 Installation for MacOS

### To install HamClock on macOS:

### Using macports:
1. `sudo port install hamclock xorg-server`

2. log out and back in to reinitialize launchd then just type hamclock and it should come right up.

### Otherwise you can build from source using the scenic route:

Install XQuartz and Xcode.

Start Xcode then open More developer tools and install the command line tools. You may also need to run the following command line in Terminal: `xcode-select --install.`

## Now follow the instructions for any UNIX system, above.

If you want a launch icon for the Dock or Desktop, I recommend using the free program Platypus to wrap HamClock into a proper application bundle. The script it will run is just one line to give the full path to the hamclock executable (/opt/local/bin/hamclock if using macports or /usr/local/bin/hamclock otherwise). For an icon use the file hamclock.png found in the ESPHamCLock directory.



