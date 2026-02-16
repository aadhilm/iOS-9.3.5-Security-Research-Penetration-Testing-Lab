# 📱 iOS 9.3.5 Security Research Lab

> **Verified & Tested Commands**  
> All commands below were executed and validated on a **jailbroken iPad 2 running iOS 9.3.5**.  
> Functionality is constrained by Apple’s XNU kernel and iOS security model. Many tools originate from **Cydia**, not the base OS.

---

## Target audience: 
> Linux beginners, developers, system and network administrators, security analysts, penetration testers, blue/red team trainees, cybersecurity students, forensics and CTF practitioners, mobile and embedded security researchers, educators, and trainers.
---

## 🔍 Nmap – Working Commands

> Only **TCP connect scans** work reliably. ICMP and raw sockets are blocked on iOS.

```bash
nmap -n -sT TARGET
nmap -n -sT -PN TARGET
nmap -n -sT --max-retries=0 TARGET
nmap -n -sT -PN -p 22,80,443 SUBNET
nmap -n -sT -PN --max-retries=0 -p 80 SUBNET
```

### ⚡ Fast & Focused Scans

```bash
nmap -n -PN -sT -F TARGET
nmap -n -PN -sT -p 80 TARGET
nmap -n -PN -sT -T1 -p 80 TARGET
```

---

## 🌐 Network Information & Diagnostics

### 📡 Interface & DHCP Overview

```bash
ipconfig ifcount
ipconfig waitall
ipconfig setverbose 1
```

### 📶 IPv4 Configuration (Wi‑Fi – en0)

```bash
ipconfig getifaddr en0
ipconfig getoption en0 router
ipconfig getoption en0 subnet_mask
ipconfig getoption en0 domain_name_server
```

### 📦 DHCP Packet Inspection

```bash
ipconfig getpacket en0
ipconfig getv6packet en0
```

### 🌍 Connectivity Testing (HTTP)

```bash
curl http://TARGET
curl -I http://TARGET
```

---

## 🧠 System Information

```bash
uname -a
sw_vers
date
getconf
pagesize
```

### 🧩 Kernel & Hardware

```bash
sysctl kern.version
sysctl kern.osversion
sysctl kern.uuid
sysctl hw.machine
sysctl hw.cputype
sysctl hw.cpusubtype
sysctl -a | head
```

---

## 💾 Memory & Storage Inspection

```bash
df -h
df -h /
du
vm_stat
zprint
```

### 🗂 Disk & Filesystem Health

```bash
mount
mount | grep /
ls /var
ls /private/var
```

---

## ⚙️ Process Management

```bash
ps
ps aux
ps aux | grep -i springboard
ps aux | grep /var/mobile/Applications/
taskinfo
```

---

## 🚀 Service & Daemon Awareness

```bash
launchctl
launchctl list
launchctl list | head
launchctl list | grep ssh
launchctl load
launchctl unload
launchctl start
launchctl stop
```

---

## 📁 Filesystem Enumeration

```bash
ls
ls -la
stat FILE
```

```bash
find . -type d | sed -e "s/[^-][^\/]*\// |/g" -e "s/|\([^ ]\)/|-\1/"
```

```bash
ls -R | grep ":$" | sed -e 's/:$//' \
  -e 's/[^-][^\/]*\//--/g' \
  -e 's/^/ /' \
  -e 's/-/|/'
```

---

## 🔎 File Search & Content Discovery

```bash
grep -R "password" .
grep -R "FLAG{" /
strings FILE | grep FLAG
```

---

## 🔐 File Permissions & Identity

```bash
ls -la
stat FILE
whoami
id
groups
```

---

## ✍️ File I/O Testing

```bash
dd if=/dev/zero of=/tmp/test bs=1M count=100
```

---

## 🔓 Jailbreak & UI Maintenance

```bash
ldrestart
uicache
PS1='[root@ios9 ~]# '
clear
```

---

## 📊 Live System Monitoring

```bash
while true; do
  date
  df -h /
  vm_stat | head -5
  sleep 2
done
```

---

## 🔑 Cryptography Basics

### Encrypt

```bash
echo "FLAG{example}" > secret.txt
openssl enc -aes-256-cbc -salt -a \
  -in secret.txt -out secret.txt.enc
rm secret.txt
```

### Decrypt

```bash
openssl enc -aes-256-cbc -a -d \
  -in secret.txt.enc -out secret.txt
```

---

## 📦 Compression & Archiving

```bash
tar -czvf file.tar.gz DIR
tar -xzvf file.tar.gz
zip -r archive.zip DIR
unzip archive.zip
```

---

## 📤 File Transfer (OpenSSH)

```bash
scp file user@HOST:/path
scp user@HOST:/path/file .
```

---

## 🧭 DNS & Network State

```bash
scutil
scutil --dns
scutil --nwi
```

---

## 🪵 Logs & Debugging

```bash
dmesg
spindump
ls /var/mobile/Library/Logs/CrashReporter
```

---

## 🔋 Power & System Control ⚠️

```bash
nvram
halt
reboot
shutdown
```

---

## 🎭 Demo & Terminal Effects

```bash
for i in 5 4 3 2 1; do echo $i; sleep 1; done
yes YOURNAME | head -n 20
echo "Your jailbreak will survive… maybe."
echo "iOS 9.3.5 > iOS 17 (fight me)"
```

---

## 🕶 Fake Hack Demo (Cosmetic Only)

```bash
echo "Connecting to NSA server..."
sleep 2
echo "Bypassing firewall..."
sleep 2
echo "Access granted ■"
```

---

## 🎲 Random Data Generation

```bash
cat /dev/urandom
cat /dev/urandom | tr -dc '01' | fold -w 80
```

---

🧪 **Educational & Research Use Only**  
Legacy platforms like iOS 9.3.5 remain valuable for learning OS internals, security constraints, and historical exploitation techniques.
