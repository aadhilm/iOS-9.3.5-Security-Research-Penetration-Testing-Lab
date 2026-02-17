# iOS 9.3.5 Legacy Device CTF Lab

This lab is designed for beginners to understand and study iOS 9.3.5 devices in a structured, hands-on environment.

**Target:** iOS 9.3.5  
**Attacker Machine:** Kali Linux / Parrot OS

---

## Mission Objectives
- Identify exposed network services  
- Gain authorized SSH access  
- Locate the encrypted flag  
- Decrypt the file  
- Capture the flag  

---

## Instructor Setup Guide

### Lab Preparation (On iOS 9.3.5 Device)

#### 1️⃣ Create the Flag
```bash
echo "FLAG{ios9_legacy_recon_success}" > /var/mobile/flag.txt
```

#### 2️⃣ Encrypt the Flag (AES-256-CBC + Base64)
```bash
openssl enc -aes-256-cbc -salt -a \
  -in /var/mobile/flag.txt \
  -out /var/mobile/flag.enc
```

You will be prompted to enter a password (example: `ios935`).

#### 3️⃣ Hide the Flag
```bash
rm /var/mobile/flag.txt
mv /var/mobile/flag.enc /var/mobile/Documents/.hidden_flag.enc
```

#### 4️⃣ (Optional) Move SSH to Non-Standard Port
Edit:
```text
/etc/ssh/sshd_config
```

Change:
```text
Port 22
```

To:
```text
Port 2222
```

Restart SSH:
```bash
launchctl unload /Library/LaunchDaemons/com.openssh.sshd.plist
launchctl load /Library/LaunchDaemons/com.openssh.sshd.plist
```

---

## Attack Phases (Kali / Parrot OS)

### 🔎 Phase 1 – Discovery (Reconnaissance)

**Objective:**  
Identify open ports and exposed services on the iOS device.

#### 🔍 Basic TCP Scan
```bash
nmap -n -sT -PN TARGET_IP
```

- `-sT` → TCP Connect scan (required for iOS restrictions)  
- `-PN` → Skip host discovery (treat host as online)  
- `-n` → No DNS resolution  

#### 🔍 Full Port Scan (If Nothing Appears)
```bash
nmap -p- -sT -PN TARGET_IP
```

This scans all 65535 TCP ports.

**Expected Result**

Students should identify:
- SSH service  

Possibly running on:
- Port 22 (Beginner)  
- Port 2222 (Intermediate)  
- High random port (Advanced)  

---

### Phase 2 – Authorized Access

Students use provided credentials.

**Default SSH (Port 22)**
```bash
ssh -oHostKeyAlgorithms=+ssh-rsa mobile@TARGET_IP
```

**Non-Standard Port**
```bash
ssh -p PORT -oHostKeyAlgorithms=+ssh-rsa mobile@TARGET_IP
```

**Example**
```bash
ssh -p 2222 -oHostKeyAlgorithms=+ssh-rsa mobile@192.168.1.25
```

iOS 9 uses older SSH algorithms — `+ssh-rsa` may be required.

---

### Phase 3 – Enumeration

**Objective:**  
Find encrypted files on the system.

**Search for Encrypted Files**
```bash
find / -type f -name "*.enc" 2>/dev/null
```

**Check Mobile Documents Directory**
```bash
ls -la /var/mobile/Documents
```

Look for hidden files:
```text
.hidden_flag.enc
```

Hidden files start with a dot (`.`).

---

### Phase 4 – Decryption

Once `.hidden_flag.enc` is found:
```bash
openssl enc -aes-256-cbc -a -d \
  -in .hidden_flag.enc \
  -out flag.txt
```

Enter the lab password (example: `ios935`).

**View the Flag**
```bash
cat flag.txt
```

**Expected Output**
```text
FLAG{ios9_legacy_recon_success}
```

---

## Progressive Hint System

**Hint 1**  
Legacy iOS devices often expose remote administration services.

**Hint 2**  
Try scanning all ports.

**Hint 3**  
Hidden files begin with a dot (`.`).

**Hint 4**  
The encryption used AES-256-CBC with base64 encoding.

---

## Advanced Variations

### 1️⃣ Add a Decoy File
```bash
echo "FAKE FLAG" > /var/mobile/Documents/fake.enc
```

### 2️⃣ Password Hint Example

**Password**
```text
ios935
```

**Hint for Students**  
“The key relates to the device OS version.”

---

## Difficulty Levels

### 🟢 Beginner
- SSH on port 22  
- Password given directly  
- File in visible directory  

### 🟡 Intermediate
- SSH on port 2222  
- Hidden file (`.hidden_flag.enc`)  
- Password hint only  

### 🔴 Advanced
- SSH on high random port (49152+)  
- Add decoy encrypted file  
- Password clue hidden in system file  
- Students must exfiltrate file and decrypt locally

### 📈 Future Lab Expansion Roadmap
This CTF series will continuously evolve to simulate real-world legacy iOS attack and defense scenarios. Upcoming labs will progressively increase in technical depth, realism, and defensive awareness to better prepare students for structured security assessments and controlled research environments.

🔎 CVE Coverage (Coming Soon)

At this stage, specific CVE-based vulnerabilities are not yet integrated into the lab environment.

Future updates are planned to incorporate selected historical vulnerabilities that impacted legacy systems, including:

CVE-2016-4655 — Kernel Information Disclosure (affecting iOS 9)

CVE-2016-4657 — WebKit Remote Code Execution (Safari / WebKit component)

These vulnerabilities are historically associated with the iOS 9.x era and are relevant for educational analysis in legacy security research.

🛡 Implementation Policy

CVE scenarios will only be introduced after proper validation and controlled lab testing.

All simulations will remain strictly within an isolated and safe environment.

No live exploitation of real-world systems is involved.

The lab will be updated periodically to maintain technical accuracy and educational relevance.

📌 Integration Status

CVE-based lab modules are currently under review and development.
Selected historical vulnerabilities affecting legacy iOS environments will be incorporated in upcoming updates as soon as validation is complete.
