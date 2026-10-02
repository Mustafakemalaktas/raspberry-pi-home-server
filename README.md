# Raspberry Pi 5 Home Server

A self-hosted Linux home server that I have been running and using daily for about a year, housed in a 3D-printed case. It handles file storage, personal finance tracking and remote media streaming.

![3D-printed case](case.jpg)
![Server inside the case](case1.jpeg)
![Server running](case2.jpeg)

## Hardware
- Raspberry Pi 5 (8 GB RAM)
- 512 GB SSD [NVMe HAT / USB 3.0 yaz]
- 3D-printed enclosure: model by [yapımcı adı] from Bambu Lab MakerWorld ([link]), printed by me
- cooler fon on the top of the case

## What it does
- **File storage:** Central place for documents and backups, accessible from all my devices
- **Finance tracking:** Monthly income and expense tracking with spreadsheets
- **Media streaming:** Video, music, movies, series and lecture videos, streamed remotely when I am away from home

## Software
- OS: [Raspberry Pi OS / Ubuntu Server / ...]
- Media server: [Jellyfin / Plex / ...]
- File sharing: [Samba / Nextcloud / ...]
- Remote access: [Tailscale / WireGuard / port forwarding]

## What I learned
- Setting up and maintaining a headless Linux server
- Basics of networking and remote access
- Running a system 24/7 and keeping it stable over a year
- 3D printing the enclosure and fitting the hardware into it

## Troubleshooting

### Server does not boot back after a power outage
**Problem:** After a short power cut or flicker, the Pi stayed off and I had to restart it manually.

**Fix I tried:** Checked the bootloader (EEPROM) configuration and made sure the board powers on automatically when power returns.

```bash
# Check the current bootloader config and update the firmware
sudo rpi-eeprom-update -a
sudo rpi-eeprom-config

# Edit the config
sudo -E rpi-eeprom-config --edit
```

Settings:

```
POWER_OFF_ON_HALT=0
WAKE_ON_GPIO=1
```

Then reboot with `sudo reboot`.

**Status:** [Tested by unplugging and replugging power: it boots by itself now / Still testing / Still not working, checking SSD detection and power supply]

**Next step:** A UPS (uninterruptible power supply) so the server shuts down cleanly or keeps running during outages, which also protects the filesystem from corruption.

## Future improvements
-Trading bots
