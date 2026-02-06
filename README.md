
# iOS 9.3.5 Security Research & Penetration Testing Lab

![Status](https://img.shields.io/badge/status-research--only-blue)
[![Platform](https://img.shields.io/badge/Platform-iOS%209.3.5%20%7C%20Jailbroken-blue)](#)
[![Devices](https://img.shields.io/badge/Devices-iPhone%20%7C%20iPad-lightgrey)](#)
[![Legacy iOS](https://img.shields.io/badge/iOS-Legacy%209.3.5-yellow)](#)
[![Apple Unsupported](https://img.shields.io/badge/Apple-Unsupported-lightgrey)](#)
[![Purpose](https://img.shields.io/badge/Purpose-Educational%20Only-success)](#)
[![Ethical Hacking](https://img.shields.io/badge/Ethical-Hacking-brightgreen)](#)
[![⚠️ Authorized Only](https://img.shields.io/badge/⚠️-Authorized%20Use%20Only-red)](#)
[![Security Lab](https://img.shields.io/badge/Security-Lab-red)](#)
[![Security Research](https://img.shields.io/badge/Security-Research-critical)](#)
[![PenTest Lab](https://img.shields.io/badge/PenTest-Lab-darkred)](#)
[![Lab Status](https://img.shields.io/badge/Lab-Active-success)](#)
[![CTF Practice](https://img.shields.io/badge/CTF-Practice-purple)](#)
[![CTF Ready](https://img.shields.io/badge/CTF-Ready-purple)](#)
[![Hands On](https://img.shields.io/badge/Hands--On-Learning-blueviolet)](#)
[![CLI Tools](https://img.shields.io/badge/CLI-Tools-5391FE?logo=terminal)](https://github.com/topics/command-line-tool)
[![System Utilities](https://img.shields.io/badge/System-Utilities-FF6E00?logo=linux)](https://github.com/topics/system-tools)
[![Open Source Love](https://badges.frapsoft.com/os/v2/open-source.svg?v=103)](#)

---
## 🧪 Lab Scope

### Supported iOS Version

* **iOS 9.3.5 (legacy)**

### Supported / Tested Devices

* iPhone 4s
* iPhone 5
* iPhone 5c
* iPad 2
* iPad 3
* iPad 4
* Original iPad Mini
✅ **Primary test platform:** *iPad 2 (iOS 9.3.5)*
All quirks, limitations, and notes in this README are based on real testing, primarily on an iPad 2.

## 📌 Overview

According to my research on jailbreaking **iPad 2 (iOS 9.3.5)**, I have documented my hands-on experience.  
The **primary purpose of this jailbreak** is **ethical hacking and penetration testing**, not piracy or misuse.

This document covers:
- Pre‑jailbreak preparation
- Limitations of non‑jailbroken iOS 9.3.5
- Phoenix jailbreak behavior and Apple’s security model
- Cydia issues and recovery
- SSH, terminal bugs, and fixes
- Nmap usage on legacy iOS
- Practical commands and CTF-style workflows

---

## ⚠️ Pre‑Jailbreak Preparation

### During Jailbreak
- Turn **OFF Wi‑Fi & Cellular**
- **Do NOT power off** the device
- Ensure **at least 50% battery**

This helps avoid:
- iOS auto‑updates
- Certificate revokes during jailbreak
- Random background processes interfering

---

### Backup (DO NOT SKIP)
- Use **iTunes / Finder (computer backup)**
- Safer than iCloud for jailbreaking
- Ensure backup completes successfully

---

### Disable Security Features
- **Find My iPhone** → OFF  
- **Passcode / Touch ID / Face ID** → OFF  
- **iCloud** → Sign out (recommended)

---

### Confirm Compatibility
- Exact **iOS version**
- Exact **device model**
- Jailbreak tool explicitly supports both

❗ If not supported: **STOP**. Updating usually kills jailbreak chances.

---

### Storage & Updates
- Minimum **2–3 GB free space**
- Disable auto‑updates:
  - Settings → General → Software Update → Automatic Updates → OFF

---

### Stable Setup (Computer)
- Use a good USB cable
- Avoid USB hubs
- Don’t touch the device during the process

---

## 📱 Without Jailbreak (iOS 9.3.5 Capabilities)

Without jailbreak:
- App Store and modern external apps **do not work**

Still usable for:
- PDF & eBook reading via **iBooks**
- Very useful for students & researchers
- No distractions → better focus
- Web browsing
- Notes app (cross‑device sync)

### Notes Sync Trick
If signed in with the same Apple ID on:
- macOS
- Newer iOS
- Android / Windows / Linux (via browser)

You can:
- Paste links/text into Notes
- Access them on the old iOS device

Slow but easier than typing long URLs.

---

## 🔓 Jailbreak Behavior (Phoenix)

I jailbroke, reset, and restored the system **15+ times**.  
Each time resulted in different Cydia and system‑level issues.

### 7‑Day Phoenix Crash (Important)
- Phoenix crashes after ~7 days
- Cydia apps also stop opening

This is **not a bug**.  
It is part of **Apple’s Security Model**.

---

## 🍎 Apple’s Security Model Explained

- iOS runs only **cryptographically signed code**
- Phoenix cannot be on the App Store
- Free Apple IDs get **7‑day certificates**

### Developer Programs
- Apple Developer Program: **$99/year**
- Apple Developer Enterprise Program: **$299/year**
  - Not for individuals
  - Requires organization approval

---

## 🔁 Fixing Phoenix (No Restore Needed)

To fix expired certificates:
- Re‑install Phoenix with a **new certificate**
- No system restore required

If device was reset:
- Restore via iTunes backup

❌ Changing date & time **does NOT work**

---

## ⏱️ How the 7‑Day Limit Works

- Free Apple ID → temporary certificate
- Certificate expires in 7 days
- After expiry:
  - App opens then closes
  - “Unable to verify app”

Paid developer account:
- Certificate valid for **1 year**

---

## 🛠 Ways to Deal with This

### Option 1 (Common)
- Re‑sign Phoenix every 7 days
- Re‑jailbreak after reboot

### Option 2 (Paid)
- Use paid developer account
- Re‑sign once per year

⚠️ No untethered jailbreak exists for iOS 9.3.5.

---

## 💾 Cydia Issues & Fixes

### Common Problems
- Broken or incompatible repos
- Repeated jailbreaking corrupts apt/dpkg
- Cydia & its apps fail to open

### Fix Methods
- Use **Filza** or **Terminal**
- If Terminal fails → use **SSH**

### Repo File Paths
```
/etc/apt/source.list
/etc/apt/source.list.d/
```

Best practices:
- Remove unused or broken repos
- Always respring or reboot after changes
- If dpkg fully breaks → restore required

---

## 📦 Useful Applications

### Core
- OpenSSH
- Filza File Manager
- iCleaner Pro

### Optional
- VLC
- ThinStuff
- xDisplay
- iRDP

Installed & used:
- Terminal
- Filza
- iCleaner
- iTransmission
- ThinStuff

---

## 🖥️ xDisplay Notes

- Mirrors Windows screen only
- Extend mode does **not** work
- Requires constant interaction
- Does **not** work on Linux

---

## 🔐 SSH on iOS 9.3.5

Modern SSH disables `ssh-rsa` by default.

### Working Command (Linux)
```bash
ssh -o HostKeyAlgorithms=+ssh-rsa     -o PubkeyAcceptedAlgorithms=+ssh-rsa root@TARGET
```

### Default Credentials
```
root   : alpine
mobile : alpine
```

---

## 🔧 Changing SSH Port (Safely)

Config file:
```
/etc/ssh/sshd_config
```

⚠️ Rules:
- Backup before editing
- Restart SSH daemon
- Test connection
- THEN reboot

Recovery:
- Revert port to `22`
- Save & reboot

Never delete `/etc/ssh` or OpenSSH.

---

## 🐞 Terminal Bug (Observed)

- Input becomes invisible
- Terminal freezes after long sessions

Workarounds:
- Restart terminal
- Keep sessions short
- Use SSH (recommended)

UI bug, not shell failure.

---
## 🎥 Video Demonstrations (Real Device)

The following videos document real behavior on a jailbroken iOS 9.3.5 device and are included for transparency and troubleshooting reference.

### ▶️ Video 1 — Terminal App Auto-Closes After Jailbreak

Description:
After jailbreak, the on-device terminal application fails to stay open and closes immediately. To continue working, an SSH connection is established from another device and used successfully.

Commands shown (over SSH):

sw_vers
df -h
whoami
ls

🔗 Video link:
https://drive.google.com/file/d/1hAhupgXhBVFyhgPntPzcjyRKE8L0VE11/view

### ▶️ Video 2 — Nmap on Legacy iOS (Unprivileged Mode)

Description:
Demonstrates running nmap in unprivileged TCP connect mode on iOS 9.3.5, including:

Scanning a target host device

Scanning the localhost / self (the iOS device itself)

Fast-forwarded sections to save time

Command used:

nmap -unprivileged -n -sT TARGET

🔗 Video link:
https://drive.google.com/file/d/1K4UNADtX0v_I9rSHr3oDTWV5kkIuMqLp/view
## Nmap Scan Screenshot

![Nmap Scan on iOS 9.3.5](ipad.png)


These videos intentionally avoid SYN scans, UDP scans, and NSE scripts due to raw socket restrictions on iOS.

---

## 🧪 Nmap on Legacy iOS

### Limitations
- ICMP blocked
- Raw sockets restricted
- Only TCP connect scans work

### Working Commands
```bash
nmap -n -sT TARGET
nmap -n -sT -PN TARGET
nmap -n -sT --max-retries=0 TARGET
```

### Network Sweep
```bash
nmap -n -sT -PN -p 22,80,443 SUBNET
```

---

## 📊 Test Report (Localhost)

```
22/tcp     open  ssh
1053/tcp   filtered unknown
1080/tcp   open  socks
1083/tcp   open  ansoft-Im-1
8021/tcp   open  ftp-proxy
11111/tcp  open  unknown
62078/tcp  open  iphone-sync
```
---


# 🛠️ Tested & Working Commands (CTF / iOS / Network Lab)
> ⚠️ **Disclaimer**: All commands are intended for **educational and authorized testing only**.


---

## 🔍 Nmap – Working Commands

```bash
nmap -n -sT TARGET
nmap -n -sT -PN TARGET
nmap -n -sT --max-retries=0 TARGET
nmap -n -sT -PN -p 22,80,443 SUBNET
nmap -n -sT -PN --max-retries=0 -p 80 SUBNET
```

---

## 🖥️ System Info

```bash
uname -a
sw_vers
date
sysctl kern.version
sysctl kern.uuid
sysctl hw.machine
sysctl hw.cputype
sysctl hw.cpusubtype
sysctl -a | head
pagesize
```

---

## 💾 Memory & Storage

```bash
df -h
df -h /
du
vm_stat
zprint
```

---

## ⚙️ Process Management

```bash
ps aux
ps aux | grep -i springboard
ps aux | grep /var/mobile/Applications/
```

---

## 🌐 Network

```bash
ipconfig getifaddr en0
```

---

## 📁 Filesystem Exploration

```bash
find . -type d | sed -e "s/[^-][^\/]*\// |/g" -e "s/|\([^ ]\)/|-\1/"
find . -maxdepth 3 -type d | sort
ls -R | grep ":$" | sed -e 's/:$//' -e 's/[^-][^\/]*\//--/g' -e 's/^/ /' -e 's/-/|/'
```

---

## 🧪 File Test

```bash
dd if=/dev/zero of=/tmp/test bs=1M count=100
```

---

## 🔓 Jailbreak / UI (iOS)

```bash
ldrestart
uicache
PS1='[root@ios9 ~]# '
clear
```

---

## 🎉 Fun / Terminal Effects

```bash
for i in 5 4 3 2 1; do echo $i; sleep 1; done
yes YOURNAME | head -n 20
echo "Your jailbreak will survive… maybe."
echo "iOS 9.3.5 > iOS 17 (fight me)"
```

---

## 🕶️ Fake Hack Sequence

```bash
echo "Connecting to NSA server..."
sleep 2
echo "Bypassing firewall..."
sleep 2
echo "Access granted ■"
```

---

## 🔢 Random Data

```bash
cat /dev/urandom
cat /dev/urandom | tr -dc '01' | fold -w 80
```

---

## 📊 Monitor Loop

```bash
while true; do
  date
  df -h /
  vm_stat | head -5
  sleep 2
done
```

---

## 🔐 Crypto Basics (CTF-Oriented)

### Encrypt a Flag

```bash
echo "FLAG{example}" > secret.txt
openssl enc -aes-256-cbc -salt -a   -in secret.txt -out secret.txt.enc
rm secret.txt
```

### Decrypt

```bash
openssl enc -aes-256-cbc -a -d   -in secret.txt.enc -out secret.txt
```

---

## 🏁 CTF Lab Workflow

---

## ⚠️ Things That Will Break Your Device

- Deleting system files
- Pirated tweaks
- Random scripts
- Repo hoarding
- Public SSH exposure
- Default passwords

---

## 🔄 Phoenix Jailbreak Notes

- Semi‑tethered
- Reboot disables jailbreak
- Must re‑run Phoenix
- Tweaks load only after re‑jailbreak

---

## 📜 Disclaimer

This project is for **educational and research purposes only**.  
All testing was performed on personally owned hardware.

---
