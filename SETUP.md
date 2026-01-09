# Setup Guide

This guide will help you set up the xemu Docker container with all required files.

## Quick Start

1. **Clone this repository**
   ```bash
   git clone https://github.com/YOUR-USERNAME/docker-xemu-linuxserver.git
   cd docker-xemu-linuxserver
   ```

2. **Download required files** (see below)

3. **Build and run**
   ```bash
   docker-compose up --build
   ```

4. **Access xemu**
   - HTTP: http://localhost:3000
   - HTTPS: https://localhost:3001

---

## Required Files

### Files Included in Repository

These files are already included and ready to use:
- ✅ `mcpx_1.0.bin` - Xbox MCPX boot ROM (512B)
- ✅ `complex_4627.bin` - Xbox flash ROM (~1MB)
- ✅ `halo2-server-eeprom.bin` - Xbox EEPROM (256B)
- ✅ `xemu.toml` - Xemu configuration

### Files You Need to Provide

Due to size, these files are **not included** and must be downloaded separately:

| File | Size | Required | Description |
|------|------|----------|-------------|
| `xbox_hdd.qcow2` | ~3.6GB | **Yes** | Xbox hard disk image with your custom setup |
| `*.iso` | Varies | Optional | Game ISOs (if you want to run games from disc) |

### Where to Get the Disk Image

**Option 1: Download the pre-configured image**
- Google Drive: [Your link here]
- MEGA: [Your link here]
- Dropbox: [Your link here]
- Place downloaded file in `config/emulator/xbox_hdd.qcow2`

**Option 2: Use your own disk image**
- If you have an existing Xbox disk image, place it in `config/emulator/`
- Update paths in `config/emulator/xemu.toml` if needed

**Option 3: Create a new disk image**
- Follow the [official xemu setup guide](https://xemu.app/docs/required-files/)
- Create a blank or formatted disk image
- Place in `config/emulator/xbox_hdd.qcow2`

---

## Directory Structure

After setup, your directory should look like this:

```
docker-xemu-linuxserver/
├── config/
│   ├── emulator/
│   │   ├── xbox_hdd.qcow2          # Your disk image (3.6GB)
│   │   ├── mcpx_1.0.bin            # Boot ROM
│   │   ├── complex_4627.bin        # Flash ROM
│   │   ├── halo2-server-eeprom.bin # EEPROM
│   │   └── xemu.toml               # Config (tracked in git)
│   └── ... (runtime files, auto-generated)
├── Dockerfile
├── docker-compose.yml
└── SETUP.md (this file)
```

---

## First Run Checklist

- [ ] All required `.bin` files are in `config/emulator/`
- [ ] `xbox_hdd.qcow2` is in `config/emulator/`
- [ ] `config/emulator/xemu.toml` paths match your files
- [ ] Docker and docker-compose are installed
- [ ] Ports 3000-3001 are available

---

## Configuration

The main configuration file is `config/emulator/xemu.toml`. Key settings:

```toml
[sys.files]
bootrom_path = '/config/emulator/mcpx_1.0.bin'
flashrom_path = '/config/emulator/complex_4627.bin'
eeprom_path = '/config/emulator/halo2-server-eeprom.bin'
hdd_path = '/config/emulator/xbox_hdd.qcow2'
```

All paths are automatically managed via symlink (see [CHANGELOG.md](CHANGELOG.md) for details).

---

## Troubleshooting

### "Could not open file" errors
- Verify all files are in `config/emulator/`
- Check file permissions: `chmod 644 config/emulator/*`
- Verify paths in `config/emulator/xemu.toml`

### Container won't start
- Check Docker logs: `docker-compose logs`
- Ensure ports 3000-3001 aren't in use
- Try rebuilding: `docker-compose up --build --force-recreate`

### Files not persisting
- Make sure you're using the volume mount in docker-compose.yml
- Check that `./config` directory exists and has correct permissions

---

## Updating

### Update xemu version
```bash
# Rebuild the container to pull latest xemu
docker-compose down
docker-compose up --build
```

### Update your disk image
- Simply replace `config/emulator/xbox_hdd.qcow2`
- Changes are persistent and survive container restarts

### Update configuration
- Edit `config/emulator/xemu.toml`
- Restart container: `docker-compose restart`

---

## Notes

- Your modifications to the Xbox disk image are preserved in `xbox_hdd.qcow2`
- The `.qcow2` format is efficient and supports snapshots
- Regular backups of `config/emulator/` are recommended
- See [CHANGELOG.md](CHANGELOG.md) for details on customizations vs upstream

---

## Support

For issues specific to this fork, check:
- [CHANGELOG.md](CHANGELOG.md) - What's different from upstream
- [Issues](https://github.com/YOUR-USERNAME/docker-xemu-linuxserver/issues)

For general xemu help:
- [xemu Documentation](https://xemu.app/docs/)
- [xemu Discord](https://discord.gg/ayoHRuH)
