# Raspberry Pi 4 Dual HDMI Setup with Ansible

This Ansible playbook configures a Raspberry Pi 4 running Raspios Bookworm ARM64 Lite with dual HDMI output for different purposes.

## Setup Overview

- **HDMI Port 0**: Console/desktop access
- **HDMI Port 1**: Dedicated pygame display output
- **WiFi**: Disabled
- **SSH**: Enabled for remote management

## Prerequisites

1. Fresh installation of 2025-05-13-raspios-bookworm-arm64-lite
2. Pi connected to network via Ethernet
3. SSH keys set up for passwordless access
4. Ansible installed on control machine

## Initial Pi Setup

Before running the playbook, enable SSH on the Pi:

```bash
# On the Pi console:
sudo systemctl enable ssh
sudo systemctl start ssh

# Change default password
passwd
```

## Usage

1. Update the IP address in `inventory/hosts.yml`
2. Run the playbook:

```bash
ansible-playbook site.yml
```

3. Reboot the Pi after completion for boot config changes to take effect

## Testing Dual HDMI

After setup, test the pygame display on HDMI port 2:

```bash
# SSH into the Pi
ssh pi@<pi-ip>

# Run the sample pygame script
cd ~/scripts
python3 hdmi2_display.py
```

## Files Created

- `/home/pi/scripts/hdmi2_display.py`: Sample pygame script for HDMI port 2
- `/etc/X11/xorg.conf.d/99-dual-hdmi.conf`: X11 dual display configuration
- `/boot/firmware/config.txt`: Boot configuration with dual HDMI settings