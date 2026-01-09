# Changelog

All notable changes to this fork of the LinuxServer.io xemu container are documented in this file.

This project follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [Unreleased]

### Added
- **Additional System Packages** ([Dockerfile](Dockerfile#L23-L26), [Dockerfile.aarch64](Dockerfile.aarch64#L24-L26))
  - `libusb-1.0-0` - USB device support for Xbox controller passthrough
  - `wmctrl` - Window manager control for automation and window management
  - `xdotool` - X11 automation tool for programmatic input simulation
  - These packages enable better hardware support and automation capabilities
  - Added to both x86_64 and aarch64 (ARM64) builds for cross-platform consistency

- **Xemu Configuration Symlink Management** ([root/defaults/autostart](root/defaults/autostart))
  - Implemented automatic symlinking of xemu's default config location to `/config/emulator/xemu.toml`
  - This enables a single, clean, version-controlled configuration file location
  - Allows xemu auto-save functionality to work properly while maintaining config in a distributable location
  - See comments in `root/defaults/autostart` for detailed technical explanation

- **Setup Documentation** ([SETUP.md](SETUP.md))
  - Comprehensive setup guide for users
  - Documents required files and where to obtain them
  - Troubleshooting and configuration instructions

- **Gameplay Automation** ([config/emulator/passleader_v3.sh](config/emulator/passleader_v3.sh))
  - Automated input script for xemu gameplay
  - Launches in separate terminal window on container start
  - Waits for xemu, loads snapshot (F6), then automates B/A button presses
  - Can be stopped with Ctrl+C in the automation terminal
  - Optional - only runs if script is present in config/emulator/

- **XLink Kai Integration** ([docker-compose.yml](docker-compose.yml#L41-L58))
  - Added XLink Kai service for system link gaming over internet
  - Connects to xemu via UDP tunneling (ports 9968/34523)
  - Web interface accessible on port 34522
  - Enables LAN multiplayer games over the internet
  - Uses ich777/xlinkkaievolution Docker image

### Changed
- **Dockerfile** - Added additional runtime dependencies for USB and automation support
- **Startup Script** - Modified to manage xemu configuration via symlink instead of relying on default location
- **Startup Script** - Added automatic file ownership fix for xemu.toml to ensure write permissions

### Fixed
- **Configuration Saving** - Fixed circular symlink issue that prevented xemu from saving settings
- **File Permissions** - Automatically set correct ownership on xemu.toml at container startup

### Technical Details

#### Configuration Management
- **Managed Config Location**: `/config/emulator/xemu.toml` (version controlled, distributable)
- **Xemu Default Location**: `/config/.local/share/xemu/xemu/xemu.toml` (symlinked to managed location)
- **Benefit**: Single source of truth for configuration, no custom xemu binary required

---

## About This Fork

This is a modified version of the [LinuxServer.io xemu container](https://github.com/linuxserver/docker-xemu).

### Upstream Repository
- **Original**: https://github.com/linuxserver/docker-xemu
- **Base Image**: `ghcr.io/linuxserver/baseimage-selkies:ubuntunoble`

### Key Differences from Upstream
1. **Additional Packages**: Added `libusb-1.0-0`, `wmctrl`, and `xdotool` for USB support and automation
2. **Custom Configuration Management**: Xemu config managed via symlinks for clean, distributable setup
3. **Organized Storage**: User-level modifications stored in `/config/emulator/` for easy distribution
4. **Enhanced Documentation**: Additional inline documentation and changelog for configuration persistence

### Distribution Strategy

**Repository Contents:**
- Docker configuration and build files (Dockerfiles, docker-compose.yml)
- Startup scripts and xemu configuration management
- Small configuration files (`xemu.toml`)
- Documentation (CHANGELOG.md, SETUP.md)

**Separate Distribution (Not in Git):**
- Large disk images (~3.6GB):
  - Xbox disk image (`xbox_hdd.qcow2`)
  - Game ISOs (`*.iso`)
- BIOS files (`*.bin`) **ARE included** in the repository (total ~1MB)
- See [SETUP.md](SETUP.md) for download instructions

**Benefits:**
- **Small repo size**: ~10MB instead of ~3.6GB
- **Flexible hosting**: Large disk images can be hosted on Google Drive, MEGA, etc.
- **Easy updates**: Update disk image without git history bloat
- **Simple setup**: Most files included, only large disk image needs downloading

---

## Versioning Notes

This changelog tracks changes specific to this fork. For upstream LinuxServer.io xemu changes, see:
- https://github.com/linuxserver/docker-xemu/commits/master
