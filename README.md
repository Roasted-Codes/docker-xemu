# docker-xemu (Enhanced Fork)

Xbox emulator (xemu) with XLink Kai multiplayer and Passleader automation.

## Features

- **XLink Kai Integration** - Online multiplayer for system link games
- **Passleader Automation** - Scripted gameplay with automated inputs
- **CPU Rendering** - Works without GPU passthrough
- **Web Interface** - Browser-based access via KasmVNC
- Based on [LinuxServer.io docker-xemu](https://github.com/linuxserver/docker-xemu)

## Quick Start

### 1. Download Required Files
- **Xbox HDD Image** (3.6GB): [Google Drive](https://drive.google.com/drive/folders/10KqAo_bU0cdI_nOkcUG2paMmZ4phiBaY?usp=drive_link)
- Place in `config/emulator/xbox_hdd.qcow2`

### 2. Run Container
```bash
docker compose up -d
```

### 3. Access
- **Xemu Interface**: https://localhost:3001
- **XLink Kai**: http://localhost:34522

## Documentation

- **[SETUP.md](SETUP.md)** - Complete setup guide with detailed instructions
- **[CHANGELOG.md](CHANGELOG.md)** - Fork modifications and differences from upstream

## Configuration

Default ports:
- `3000/3001` - Xemu web interface (HTTP/HTTPS)
- `34522` - XLink Kai web interface
- `34523/UDP` - XLink Kai game traffic

See [SETUP.md](SETUP.md) for environment variables and advanced configuration.

## What's Different?

This fork adds:
- XLink Kai container for online multiplayer
- Passleader automation script (`passleader_v3.sh`)
- Additional packages: `libusb-1.0`, `wmctrl`, `xdotool`
- Improved configuration management
- Setup documentation and troubleshooting

See [CHANGELOG.md](CHANGELOG.md) for complete list of modifications.

## Support

- **Issues**: [GitHub Issues](https://github.com/Roasted-Codes/docker-xemu/issues)
- **Upstream**: [linuxserver/docker-xemu](https://github.com/linuxserver/docker-xemu)
- **xemu Docs**: [xemu.app/docs](https://xemu.app/docs/)

## License

Same as upstream LinuxServer.io docker-xemu project.
