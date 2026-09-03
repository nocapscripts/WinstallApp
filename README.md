# Winstaller

A lightweight Windows software installer.

Winstaller provides a simple graphical interface for discovering, checking,
and installing common Windows applications using either **Windows Package
Manager (`winget`)** or **Chocolatey**.


---

## Features


- 📦 Supports `winget`
- 🍫 Supports Chocolatey
- 🔍 Search applications by name or description
- ☑️ Select multiple applications
- 🚫 Automatically detects already-installed applications
- ⚡ Installs multiple applications in parallel
- 🔄 Refresh installation status
- 📊 Overall installation/status progress bar
- 📝 Automatic logging to `logs.txt`
- 🌙 Dark-themed interface
- 🚀 Background threads keep the UI responsive
- 🪟 Installer console windows are hidden
- 💾 Application list is compiled directly into the executable

---

## Requirements

### Windows

Winstaller is currently intended for Windows.

You need at least one of the following package managers installed:

### Winget

Windows Package Manager is normally available through modern versions of
Windows 10 and Windows 11.

Check:

```powershell
winget --version
