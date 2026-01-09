# Xemu Emulator Files

This directory contains all files needed for xemu to run.

## Files Included in Repository ✅

These are already here:
- `mcpx_1.0.bin` - Xbox MCPX boot ROM (512 bytes)
- `complex_4627.bin` - Xbox flash ROM (~1MB)
- `halo2-server-eeprom.bin` - Xbox EEPROM (256 bytes)
- `xemu.toml` - Xemu configuration
- `passleader_v3.sh` - **Gameplay automation script** (auto-runs on container start)
  - Waits for xemu, loads snapshot (F6), automates B/A button presses
  - Runs in separate terminal - stop with Ctrl+C
  - See [SETUP.md](../../SETUP.md#gameplay-automation-optional) for details

## Files You Must Add ⚠️

Download separately - see [SETUP.md](../../SETUP.md):

- `xbox_hdd.qcow2` - Xbox hard disk image (~3.6GB) **[REQUIRED]**
- `*.iso` - Game disc images (optional)

## Why is the disk image excluded?

The `.qcow2` disk image is excluded from git because:
1. It's 3.6GB - too large for git repositories
2. GitHub has a 100MB file size limit
3. Allows you to use your own custom Xbox setup
4. Can be updated independently without bloating git history

Place your `xbox_hdd.qcow2` file in this directory before running the container.

See [SETUP.md](../../SETUP.md) for download links and setup instructions.
