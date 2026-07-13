# maintenance.md

# System Maintenance Guide

A centralized maintenance guide for my Windows development machine and WSL Ubuntu environment.

---

# Table of Contents

1. Update Everything
2. Manually Installed Software
3. System Cleanup
4. System Health
5. Diagnostics & Information
6. Maintenance Schedule

---

# 1. Update Everything

## 1.1 Preview Available Updates

### Windows (Winget)

```powershell
winget upgrade
```

### Scoop

```powershell
scoop status
```

### Ubuntu

```bash
apt list --upgradable
```

### WSL Version

```powershell
wsl --version
```

---

## 1.2 Windows

### Windows Update

Updates Windows security patches, cumulative updates, built-in applications, and many hardware drivers.

```powershell
Start-Process "ms-settings:windowsupdate"
```

Or manually:

```
Settings
→ Windows Update
→ Check for updates
```

---

### Windows Drivers

Windows Update installs many official drivers automatically.

Always check Windows Update first before downloading drivers manually.

---

### Dell BIOS & Firmware

Check Dell Support periodically for:

- BIOS
- Firmware
- Chipset
- Recommended drivers

Install only recommended updates.

---

### Intel Graphics Driver

Update only if Intel releases a newer stable driver or you need a bug fix.

---

## 1.3 Windows Applications

### Winget Packages

Updates every application installed through Winget.

```powershell
winget upgrade --all
```

---

### Scoop Packages

Update Scoop itself.

```powershell
scoop update
```

Update every installed application.

```powershell
scoop update *
```

Remove old package versions.

```powershell
scoop cleanup *
```

Clear Scoop download cache.

```powershell
scoop cache rm *
```

---

### Microsoft Store Applications

1. Open Microsoft Store
2. Library
3. Get updates

---

### Microsoft Edge

Open:

```
edge://settings/help
```

---

### Visual Studio Code Extensions

Open Command Palette:

```
Ctrl + Shift + P
```

Run:

```
Extensions: Update All Extensions
```

---

## 1.4 WSL

### Update WSL

```powershell
wsl --update
```

Verify:

```powershell
wsl --version
```

---

### Ubuntu Packages

```bash
sudo apt update
sudo apt upgrade -y
sudo apt autoremove -y
sudo apt autoclean
```

Optional:

```bash
sudo apt clean
```

---

## 1.5 Development Environment

### Oh My Zsh

```bash
omz update
```

---

### Python

Upgrade pip.

```bash
python3 -m pip install --upgrade pip
```

List outdated packages.

```bash
pip list --outdated
```

---

### npm

Check outdated packages.

```bash
npm outdated -g
```

Update global packages.

```bash
npm update -g
```

---

# 2. Manually Installed Software

Software installed manually from release pages or standalone installers must be maintained manually.

---

## Fastfetch

### Install

Download the latest **amd64** `.deb` package from the official GitHub Releases page.

Install it:

```bash
sudo apt install ./fastfetch-linux-amd64.deb
```

---

### Update

When a new version is released:

1. Download the latest `.deb`.
2. Install it again using:

```bash
sudo apt install ./fastfetch-linux-amd64.deb
```

APT automatically replaces the previous version while preserving your configuration.

---

### Remove

Remove Fastfetch:

```bash
sudo apt remove fastfetch
```

Remove the configuration files:

```bash
rm -rf ~/.config/fastfetch
```

---

### Notes

- Always download Fastfetch from the official GitHub Releases page.
- Use the **amd64** build on this machine.
- Because Fastfetch was installed manually from a local `.deb`, `apt upgrade` **will not** install future releases automatically.
- Check for new Fastfetch releases periodically.

---

## Future Manual Software

Examples:

- AppImages
- Standalone binaries
- Software installed from GitHub Releases
- Custom CLI tools

---

# 3. System Cleanup

## Windows Disk Cleanup

Run:

```powershell
cleanmgr
```

Click:

```
Clean up system files
```

Recommended:

- Windows Update Cleanup
- Temporary Files
- Delivery Optimization Files
- DirectX Shader Cache
- Temporary Internet Files
- Downloaded Program Files
- Windows Error Reports
- Thumbnails

Avoid deleting unless intended:

- Downloads
- Previous Windows Installation
- Recycle Bin

---

## Ubuntu Cleanup

Remove unused packages.

```bash
sudo apt autoremove -y
```

Remove obsolete package cache.

```bash
sudo apt autoclean
```

Optional:

```bash
sudo apt clean
```

---

## Scoop Cleanup

Remove old versions.

```powershell
scoop cleanup *
```

Remove download cache.

```powershell
scoop cache rm *
```

---

# 4. System Health

## Windows File Integrity

Check protected Windows files.

```powershell
sfc /scannow
```

Repair the Windows component store.

```powershell
DISM /Online /Cleanup-Image /RestoreHealth
```

---

## Disk Health

Quick filesystem scan.

```powershell
chkdsk C: /scan
```

---

## SSD Health

Basic information:

```powershell
Get-PhysicalDisk
```

Detailed reliability:

```powershell
Get-StorageReliabilityCounter -PhysicalDisk (Get-PhysicalDisk)
```

---

## Battery Health

Generate a battery report.

```powershell
powercfg /batteryreport
```

---

## Energy Report

Generate an energy efficiency report.

```powershell
powercfg /energy
```

---

# 5. Diagnostics & Information

## Windows Information

```powershell
systeminfo
```

---

## Ubuntu Information

```bash
fastfetch
```

---

## WSL Information

```powershell
wsl --version
```

---

## Installed Windows Packages

```powershell
winget list
```

---

## Installed Scoop Packages

```powershell
scoop list
```

---

## Installed Ubuntu Packages

```bash
apt list --installed
```

---

# 6. Maintenance Schedule

## Weekly

- Windows Update
- Winget packages
- Scoop packages
- Microsoft Store apps
- Microsoft Edge
- WSL
- Ubuntu packages
- Oh My Zsh

---

## Monthly

- Disk Cleanup
- Ubuntu cleanup
- Scoop cleanup
- Check Dell drivers
- Check Intel graphics driver
- Generate battery report
- Check SSD health
- Check Fastfetch releases

---

## Every 3 Months

- Run SFC
- Run DISM
- Review installed software
- Remove unused applications
- Review manually installed software

---

## Every 6 Months

- Check BIOS updates
- Check firmware updates
- Review development tools
- Review startup applications
- Review storage usage

---

# Notes

- Prefer official package managers whenever possible.
- Install software manually only when no package manager provides a suitable version.
- Always download manually installed software from its official release page.
- Keep this document updated whenever a new development tool is installed or removed.