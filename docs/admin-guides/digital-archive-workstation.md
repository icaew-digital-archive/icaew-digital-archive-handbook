# Digital Archive Workstation

## Overview

> **Purpose:** This document provides comprehensive information about the digital archiving workstation setup, including system configuration, installed software, and maintenance procedures.

The workstation runs Ubuntu/BitCurator as the primary operating system.

---

## Installation Guide

### Installing Ubuntu/BitCurator
Follow these steps to set up a new laptop:

1. **Download Ubuntu**  
   - Obtain the Ubuntu image from [ubuntu.com](https://ubuntu.com/tutorials/install-ubuntu-desktop)

2. **Create Bootable USB**  
   - Use Ubuntu's "Startup Disk Creator" or [balenaEtcher](https://www.balena.io/etcher/)
   - Follow the tool's instructions to create a bootable USB

3. **Install Ubuntu**  
   - Restart and press `F12` (or appropriate boot menu key) to boot from USB
   - Select "Erase disk and install Ubuntu" or "Install Ubuntu" depending on your needs
   - Follow the installation wizard
   - **Default naming conventions:**
     - Username: `digital-archivist`
     - Computer name: `digital-archive`

4. **Install BitCurator**  
   - Use the [SaltStack repository](https://github.com/bitcurator/bitcurator-salt)
   - Follow the installation instructions provided

5. **Post-Installation**  
   ```bash
   sudo apt update && sudo apt upgrade
   ```

---

## Software Installation

### Pre-Installed Software
The following tools come pre-installed with BitCurator:

- **[Ubuntu](https://ubuntu.com/download/desktop)** - Core operating system
- **[BitCurator](https://bitcurator.net/)** - Digital archiving suite
- **[Python](https://www.python.org/downloads/)** - Programming language
- **[Git](https://git-scm.com/download/linux)** - Version control
- **[Docker](https://docs.docker.com/engine/install/ubuntu/)** - Container platform

---

### Additional Software to Install

#### Development Tools

**Python Virtual Environment Support:**
```bash
sudo apt install python3.10-venv
```

**Git Configuration:**
```bash
git config --global user.name "FIRST_NAME LAST_NAME"
git config --global user.email "MY_NAME@example.com"
```

**Visual Studio Code:**
Install via Ubuntu Software app, or via command line:
```bash
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -o root -g root -m 644 packages.microsoft.gpg /etc/apt/trusted.gpg.d/
sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/trusted.gpg.d/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'
sudo apt update
sudo apt install code
```

Recommended extensions:
- Python
- Prettier
- Markdown All in One

---

#### Web Archiving Tools

**Google Chrome/Chromium:**
Required for browsertrix-crawler
```bash
# Install Google Chrome
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo apt install ./google-chrome-stable_current_amd64.deb

# Or install Chromium
sudo apt install chromium-browser
```

**AWS CLI:**
For large file ingestion into Preservica
```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

**Get cookies.txt:**
Chrome extension for cookie export - [Install from Chrome Web Store](https://chrome.google.com/webstore/detail/get-cookiestxt-locally/cclelndahbckbenkjhflpdbgdldlbecc)

**Thunar:**
Bulk file rename utility
```bash
sudo apt install thunar
```

---

#### Digital Archiving Tools

**archiveweb.page:**
Chrome extension for web archiving - [Install from Chrome Web Store](https://github.com/webrecorder/archiveweb.page)

**replayweb.page:**
Web archive replay tool - [Available online](https://github.com/webrecorder/replayweb.page)

**OCRmyPDF:**
PDF OCR tool
```bash
sudo apt install ocrmypdf
```

**ExifTool:**
Metadata management tool
```bash
sudo apt install libimage-exiftool-perl
```

**yt-dlp:**
Enhanced fork of youtube-dl with additional features
```bash
pip install yt-dlp
```

**py-wacz:**
WACZ format handler
```bash
pip install py-wacz
```

**py-wasapi-client:**
WARC file download client
```bash
pip install py-wasapi-client
```

---

#### Documentation Tools

**MkDocs:**
Documentation generator
```bash
pip install mkdocs
```

**Material:**
MkDocs theme
```bash
pip install mkdocs-material
```

---

#### VDI Access

**Citrix Workspace:**
Version 23.3.0.32 (tested working) for VDI access via:
- [MKPortal](https://www.mkportal.icaew.com)
- [LonPortal](https://www.lonportal.icaew.com/)

---

## Additional Resources

- [BitCurator Documentation](https://wiki.bitcurator.net/)
- [Ubuntu Documentation](https://help.ubuntu.com/)
- [Docker Documentation](https://docs.docker.com/)
- [Python Documentation](https://docs.python.org/)
- [Git Documentation](https://git-scm.com/doc)
