# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Ansible playbook for setting up Raspberry Pi 4 with dual HDMI configuration. HDMI port 0 serves console access while HDMI port 1 is dedicated for pygame display output.

## Key Commands

```bash
# Run the full playbook
ansible-playbook site.yml

# Run specific tags (if added later)
ansible-playbook site.yml --tags config

# Check inventory
ansible-inventory --list

# Test connectivity
ansible raspberrypis -m ping
```

## Architecture

- `site.yml`: Main playbook entry point
- `roles/raspberrypi/`: Complete Pi configuration role
  - `tasks/main.yml`: All setup tasks including packages, SSH, dual HDMI config
  - `templates/config.txt.j2`: Boot configuration template for dual HDMI
  - `handlers/main.yml`: Service restart handlers
- `inventory/hosts.yml`: Pi connection details

## Important Configuration

- Dual HDMI setup in `/boot/firmware/config.txt` with forced hotplug detection
- Direct framebuffer access for pygame on HDMI port 1 using `/dev/fb1`
- WiFi disabled via device tree overlay
- Sample pygame script targets HDMI port 1 using direct framebuffer (`SDL_FBDEV=/dev/fb1`)