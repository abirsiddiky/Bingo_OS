# 🎯 Bingo OS

**Lightweight • Fast • Simple**

Bingo OS is a custom Linux distribution based on Debian 13 (Trixie) featuring the IceWM window manager. It's designed to be lightweight, fast, and easy to use.

## ✨ Features

- 🪶 **Extremely Lightweight**: IceWM window manager
- ⚡ **Fast Performance**: Low resource usage
- 🎨 **Simple Interface**: User-friendly design
- 💿 **Live Boot**: Run from USB without installation
- 🔧 **Easy Installation**: Calamares installer included
- 🌐 **Full Network Support**: NetworkManager built-in

## 📦 Included Software

### Desktop Environment
- **IceWM** - Lightweight window manager
- **LightDM** - Display manager with auto-login
- **Thunar** - File manager with volume management
- **Xfce4 Terminal** - Terminal emulator

### Applications
- **Firefox ESR** - Web browser
- **Gedit** - Text editor
- **Mousepad** - Lightweight text editor
- **File Roller** - Archive manager
- **LXAppearance** - Theme customization
- **Synaptic** - Package manager GUI

### Multimedia
- **PulseAudio** - Sound server
- **Pavucontrol** - Volume control

### Utilities
- **NetworkManager** - Network management
- **htop** - System monitor
- **Git** - Version control
- **wget/curl** - Download tools

## 💻 System Requirements

### Minimum
- **CPU**: 1 GHz processor
- **RAM**: 512 MB
- **Storage**: 5 GB free space
- **Display**: 800x600 resolution

### Recommended
- **CPU**: 2 GHz dual-core processor
- **RAM**: 2 GB or more
- **Storage**: 10 GB free space
- **Display**: 1024x768 or higher

## 🚀 Getting Started

### Create Bootable USB

#### Using Ventoy (Recommended)
1. Download [Ventoy](https://www.ventoy.net/)
2. Install Ventoy to your USB drive
3. Copy `Bingo-OS-1.0.iso` to the USB drive

#### Using Rufus (Windows)
1. Download [Rufus](https://rufus.ie/)
2. Select your USB drive
3. Select `Bingo-OS-1.0.iso`
4. Click Start

#### Using dd (Linux)
```bash
sudo dd if=Bingo-OS-1.0.iso of=/dev/sdX bs=4M status=progress
sudo sync
```
*Replace `/dev/sdX` with your USB device*

### Boot Options

When booting, you'll see these options:
- **Start Bingo OS (Live)** - Default live session
- **Start Bingo OS (Safe Mode)** - Boot with nomodeset
- **Start Bingo OS (Persistence)** - Save changes to USB

## 📥 Installation

1. Boot Bingo OS from USB
2. On the desktop, double-click **Install Bingo OS**
3. Follow the Calamares installer prompts:
   - Select language
   - Choose timezone
   - Configure keyboard
   - Partition disk
   - Create user account
4. Reboot after installation completes

## 🔑 Default Credentials

### Live Session
- **Username**: `bingo`
- **Password**: `live`

### Root User
- **Username**: `root`
- **Password**: `toor`

*Change these passwords after installation!*

## 🛠️ Building from Source

### Prerequisites (Rocky Linux 10)
```bash
sudo dnf install -y podman squashfs-tools xorriso
```

### Build Process
```bash
# Create workspace
mkdir -p ~/bingo-os
cd ~/bingo-os

# Start Debian container
podman run -it --privileged \
  -v ~/bingo-os:/work:Z \
  --name bingo-builder \
  debian:trixie /bin/bash

# Inside container
cd /work
apt update
apt install -y debootstrap squashfs-tools xorriso \
  isolinux syslinux-common grub-pc-bin grub-efi-amd64-bin mtools

# Create base system
debootstrap --arch=amd64 trixie chroot http://deb.debian.org/debian/

# Mount and enter chroot
mount --bind /dev chroot/dev
mount --bind /proc chroot/proc
mount --bind /sys chroot/sys
mount --bind /dev/pts chroot/dev/pts
chroot chroot /bin/bash

# Configure system (see full build script)
# ... install packages and configure ...

# Exit chroot
exit

# Build ISO
# ... create ISO structure and generate ISO ...

# Copy ISO to host
exit
podman cp bingo-builder:/work/Bingo-OS-1.0.iso ~/
```

## 🎨 Customization

### Change Theme
```bash
lxappearance
```

### Configure IceWM
Edit `~/.icewm/preferences` for window manager settings

### Add Startup Applications
Edit `~/.icewm/startup` and add your commands

### Install Additional Software
```bash
sudo apt update
sudo apt install package-name
```

Or use Synaptic Package Manager from the menu

## 🐛 Troubleshooting

### No WiFi Connection
```bash
sudo systemctl restart NetworkManager
```

### Black Screen After Boot
Boot in Safe Mode (nomodeset option)

### Sound Not Working
```bash
pulseaudio --kill
pulseaudio --start
```

### Display Resolution Issues
```bash
xrandr --output HDMI-1 --mode 1920x1080
```

## 📚 Documentation

- [Debian Documentation](https://www.debian.org/doc/)
- [IceWM Manual](https://ice-wm.org/manual/)
- [Arch Wiki](https://wiki.archlinux.org/) - Great resource for Linux

## 🤝 Contributing

Contributions are welcome! If you'd like to improve Bingo OS:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## 📄 License

Bingo OS is based on Debian GNU/Linux and inherits its free software licenses. 

Individual components maintain their respective licenses:
- Debian: [DFSG](https://www.debian.org/social_contract#guidelines)
- IceWM: LGPL
- Linux Kernel: GPLv2

## 🙏 Acknowledgments

- Debian Project for the solid base
- IceWM developers for the lightweight window manager
- Calamares team for the installer
- All open-source contributors

## 📞 Support

For issues and questions:
- Report bugs on the issue tracker
- Join community discussions
- Check the documentation

---

**Bingo OS** - Made with ❤️ for the Linux community

*Version 1.0 • Based on Debian 13 (Trixie)*