# Winstaller Prerelease

A lightweight Windows software installer built with **Rust** and **egui**.

Winstaller provides a simple graphical interface for discovering, checking, and installing common Windows applications using either **Windows Package Manager (`winget`)** or **Chocolatey**.

> ⚠️ **Winstaller is currently a prerelease.**  
> Some features are still being developed and Windows security software may occasionally flag early builds as potentially unwanted or suspicious software.

---

## ✨ Features

- 📦 Supports **Windows Package Manager (`winget`)**
- 🍫 Supports **Chocolatey**
- 🔍 Search applications by name or description
- ☑️ Select multiple applications
- 🚫 Automatically detects already-installed applications
- ⚡ Installs multiple applications in parallel
- 🔄 Refresh application installation status
- 📊 Overall installation/status progress bar
- 📝 Automatic logging to `logs.txt`
- 🌙 Dark-themed graphical interface
- 🚀 Background threads keep the UI responsive
- 🪟 Package-manager console windows are hidden
- 💾 Application definitions are compiled directly into the executable
- 🔧 Automatically checks whether `winget` and Chocolatey are available

---

## 🖥️ Requirements

Winstaller is currently intended for **Windows 10 and Windows 11**.

Winstaller uses one of the following package managers:

- Windows Package Manager (`winget`)
- Chocolatey

You can check whether they are installed with:

### Winget

```powershell
winget --version
```

### Chocolatey

```powershell
choco --version
```

---

## 📦 Package Managers

### Winget

Windows Package Manager is normally included with modern Windows 10 and Windows 11 installations through Microsoft's **App Installer** package.

If Winget is unavailable, Winstaller can direct you to the official Microsoft App Installer page so it can be installed.

### Chocolatey

If Chocolatey is not installed, Winstaller can attempt to install it using Chocolatey's official installation bootstrap script.

Installing Chocolatey may require **Administrator privileges**.

---

## 🔎 Application Detection

Before installing an application, Winstaller checks whether it is already installed.

### Winget

Winstaller uses:

```powershell
winget list --id <id> -e
```

### Chocolatey

Winstaller uses:

```powershell
choco list --local-only --exact <id>
```

Installation-status checks are performed in background threads so the graphical interface remains responsive.

---

## ⚡ Installation

Applications can be selected using the checkboxes and installed together.

### Winget

```powershell
winget install --id <id> -e --silent --accept-package-agreements --accept-source-agreements
```

### Chocolatey

```powershell
choco install <id> -y
```

Each application is installed in its own background task.

The application status changes between:

```text
Not installed
     ↓
Installing...
     ↓
Done / Failed
```

---

## 📊 Progress

Winstaller displays an overall progress indicator while applications are being checked or installed.

The current progress bar represents **completed application operations**.

It does **not** currently represent the actual download percentage reported by Winget or Chocolatey.

For example:

```text
[████████████░░░░░░░░] 60%
```

means approximately 60% of the tracked application operations have completed.

Real download/install percentage tracking may be added in a future release.

---

## 📝 Logging

Winstaller automatically writes application activity to:

```text
logs.txt
```

The log can contain information such as:

```text
Winstaller starting...
Loaded 50 applications.
Winget available: true
Chocolatey available: true
Checking installation status: Visual Studio Code
Installation started: Git
Installation successful: Git
Installation failed: Example App - exit code 1
```

The log file is useful when troubleshooting failed installations.

---

## 🛡️ Windows Defender / Virus Detection

Because Winstaller is a **new, unsigned prerelease application**, Windows Defender or another antivirus product may occasionally flag a build as suspicious.

This does **not automatically mean that Winstaller contains malware**.

Winstaller performs actions that can resemble installer or deployment software, including:

- Launching `winget`
- Launching Chocolatey
- Installing applications
- Starting PowerShell when setting up Chocolatey
- Running package-manager commands in the background
- Hiding package-manager console windows

These behaviors can sometimes trigger heuristic antivirus detections, particularly for new executables with little or no reputation.

### If Windows Defender detects Winstaller

First, check the exact detection name instead of assuming that every warning is a confirmed infection.

You can inspect Defender detections with:

```powershell
Get-MpThreatDetection |
    Select-Object ThreatName, InitialDetectionTime, Resources
```

You can also scan the executable with a multi-engine service such as VirusTotal.

> **Do not disable Windows Defender simply to run Winstaller.**
>
> If a release is incorrectly detected, the preferred solution is to investigate the detection, verify the source code/build, and submit a false-positive report to the relevant antivirus vendor.

### Code Signing

Official releases should eventually be **digitally signed** with an Authenticode certificate.

Code signing can help Windows establish the publisher's identity and improve application reputation.

Prerelease development builds may remain unsigned.

---

## 🔐 Security

Winstaller is designed to use the official package managers rather than downloading application installers directly.

Applications are installed through:

```text
Winstaller
    │
    ├── Winget
    │     └── Application package
    │
    └── Chocolatey
          └── Application package
```

Application definitions are stored directly in the Rust source code rather than loaded from an external JSON configuration file.

---

## 🛠️ Source Code

Winstaller is built using:

- **Rust**

---

## 🚧 Prerelease Status

Winstaller is still under active development.

Planned improvements include:

- 🖼️ Application icons
- 📈 Real download/install progress
- 🔐 Code-signed releases
- 📦 More applications
- 🔄 Improved package-manager setup
- ❌ Better error handling
- 📋 More detailed installation logs
- 🎨 UI improvements
- 🪟 Windows installer/package distribution

---
