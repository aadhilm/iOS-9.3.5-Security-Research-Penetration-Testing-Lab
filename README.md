# 📱 Jailbroken iOS Security & Penetration Testing Lab
[![Platform](https://img.shields.io/badge/Platform-iOS%209.3.5%20%7C%20Jailbroken-blue)](#)
[![Devices](https://img.shields.io/badge/Devices-iPhone%20%7C%20iPad-lightgrey)](#)
[![Purpose](https://img.shields.io/badge/Purpose-Educational%20Only-success)](#)
[![Ethical Hacking](https://img.shields.io/badge/Ethical-Hacking-brightgreen)](#)
[![Security Lab](https://img.shields.io/badge/Security-Lab-red)](#)
[![Requires Jailbreak](https://img.shields.io/badge/Requires-Jailbreak-orange)](#)
[![Legacy iOS](https://img.shields.io/badge/iOS-Legacy%209.3.5-yellow)](#)
[![CTF Practice](https://img.shields.io/badge/CTF-Practice-purple)](#)
[![CLI Tools](https://img.shields.io/badge/CLI-Tools-5391FE?logo=terminal)](https://github.com/topics/command-line-tool)
[![System Utilities](https://img.shields.io/badge/System-Utilities-FF6E00?logo=linux)](https://github.com/topics/system-tools)
[![Open Source Love](https://badges.frapsoft.com/os/v2/open-source.svg?v=103)](#)

> **A hands-on security lab for networking, hardening, and CTF-style penetration testing on legacy jailbroken iOS devices**

This repository documents a **controlled, educational security lab** built on **old jailbroken iPhones and iPads** running **iOS 9.3.5**. The lab focuses on understanding real-world limitations of legacy iOS, practicing basic penetration testing techniques, and learning how to harden fragile systems without breaking them.

🚫 **Not for illegal hacking.** This lab is intended **only** for devices you own and environments you are explicitly authorized to test.

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

---

## 🎯 Learning Objectives

* Network discovery and enumeration on restricted systems
* SSH hardening and recovery on jailbroken iOS
* Understanding legacy crypto and protocol constraints
* Practicing CTF-style thinking in a safe, local lab
* Learning how systems fail — and how to recover them

---

## ⚠️ Legal & Ethical Notice

* Jailbreak **only devices you own**
* Scan **only networks and systems you are authorized to test**
* Jailbroken devices are **fragile** and can bootloop or brick

> Always define a recovery plan *before* modifying system services.

---

## 1️⃣ Immediate Post-Jailbreak Security (DO FIRST)

### Default SSH Credentials (High Risk)

```
root   : alpine
mobile : alpine
```

### Change Passwords Immediately

```
passwd root
passwd mobile
```

### Legacy SSH Compatibility (iOS 9.3.5)

Modern SSH clients may fail unless legacy algorithms are explicitly enabled:

```
ssh -o HostKeyAlgorithms=+ssh-rsa \
    -o PubkeyAcceptedAlgorithms=+ssh-rsa root@TARGET
```

⚠️ Do **not** expose SSH to the public internet.

---

## 2️⃣ SSH Hardening (Safe Method)

CLI editors are unreliable on jailbroken iOS.

✅ **Recommended:** *Filza File Manager* (Cydia)

### SSH Config Path

```
/etc/ssh/sshd_config
```

> Filza may show `/` as `root/` — they refer to the same location.

### Change SSH Port

From:

```
#Port 22
```

To:

```
Port 2222
```

Save the file and restart SSH or reboot.

> **Rule:** If CLI tools misbehave, trust Filza.

---

## 🔄 SSH Recovery (Critical)

If you lock yourself out:

1. Open **Filza**

2. Edit:

   ```
   /etc/ssh/sshd_config
   ```

3. Revert to:

   ```
   Port 22
   ```

4. Save and reboot

❌ **Never** delete `/etc/ssh` or remove OpenSSH.

---

## 3️⃣ Fixing Cydia / dpkg / apt

Common issues include broken installs and dpkg locks.

```
apt-get update
apt-get -f install
dpkg --configure -a
apt-get clean
```

💡 SSH from another device is significantly more stable than on-device terminals.

---

## 4️⃣ Known Terminal Bug (iOS 9.3.5)

### Symptoms

* Invisible input while typing
* Terminal freezes after long sessions

### Workarounds

* Restart terminal app
* ✅ Use SSH instead
* Keep local sessions short

This is a **UI bug**, not a shell failure.

---

## 5️⃣ Minimal Tooling Philosophy

### Core

* OpenSSH
* Filza File Manager
* iCleaner Pro

### Optional (Media / Remote)

* VLC
* ThinStuff
* xDisplay
* iRDP

⚠️ Keep repositories minimal and trusted.

---

## 6️⃣ Crypto Basics (CTF-Oriented)

### Encrypt a Flag

```
echo "FLAG{example}" > secret.txt
openssl enc -aes-256-cbc -salt -a \
  -in secret.txt -out secret.txt.enc
rm secret.txt
```

### Decrypt

```
openssl enc -aes-256-cbc -a -d \
  -in secret.txt.enc -out secret.txt
```

---

## 7️⃣ Nmap on Legacy iOS (Important Limitations)

On iOS 9.3.5:

* ICMP is blocked
* Raw sockets are restricted

✅ **Only TCP connect scans work reliably**.

### Safe Commands

```
nmap -n -sT TARGET
nmap -n -sT -PN TARGET
nmap -n -sT --max-retries=0 TARGET
```

❌ Avoid:

* SYN scans (`-sS`)
* UDP scans (`-sU`)
* OS detection (`-O`)
* NSE scripts

---

## 8️⃣ TCP-Based Network Sweep

```
nmap -n -sT -PN -p 22,80,443 SUBNET
```

Fast sweep:

```
nmap -n -sT -PN --max-retries=0 -p 80 SUBNET
```

---

## 9️⃣ CTF-Style Lab Workflow

### Phase 1: Discovery

```
nmap -n -sT -PN TARGET
```

### Phase 2: Authorized Access

```
ssh user@TARGET
```

### Phase 3: Enumeration

```
find / -name "*.enc" 2>/dev/null
```

### Phase 4: Decryption

```
openssl enc -aes-256-cbc -a -d -in flag.enc -out flag.txt
```

🚩 Flag captured

---

## 🔥 Progressive CTF Scenarios

* Hidden SSH ports
* Fake flags and misdirection
* Password reuse logic
* Permission barriers (root-only flags)
* Noise-heavy environments

Each level emphasizes **analysis over exploitation**.

---

## ❌ Things That Will Break Your Device

* Deleting system files
* Random scripts from forums
* Pirated tweaks
* Repo hoarding
* Public SSH exposure
* Leaving default passwords

---

## ✅ Final Notes

> Jailbroken iOS devices are **powerful, constrained, and unforgiving**.
>
> Move slowly. Document changes. Always preserve SSH access.
> The goal is learning — not speed.
