# ⚔️ Week 3 — Password Cracking & Attacking

> **NetworkWalks Academy | Batch B082 | August 2026**
>
> **Track:** Offensive (Red Team) — Phase 3 (Gaining Access)
>
> **Submission Deadline:** 23:00H, Friday 28-August-2026

---

## 📋 Project Overview

Week 3 focuses on **Phase 3 of the ethical hacking lifecycle — Gaining Access** through controlled password cracking and dictionary attacks. Using **John the Ripper (JTR Jumbo)**, **Johnny GUI**, and **NetworkWalks Online Cracking Tools & Wordlist Generators**, we extract cryptographic hashes from password-protected document targets (`$pdf$` format) and successfully crack the plaintext credentials using targeted dictionary and mutation attacks.

```
+----------------------------------------------------------------------------------+
|                          5 PHASES OF HACKING — WEEK 3 FOCUS                     |
+----------------------------------------------------------------------------------+
|  [01. FOOTPRINTING] -> [02. SCANNING] -> [03. GAINING ACCESS]  <== WEEK 3       |
|  (Week 2 Complete)    (Week 2 Complete)   Password Cracking / Hash Recovery      |
|                                                                                  |
|                                       -> [04. MAINTAINING ACCESS]  (Week 3/4)   |
|                                           Backdoors & Persistence                |
|                                                                                  |
|                                       -> [05. CLEARING LOGS]       (Week 4)     |
|                                           Anti-forensics & Log Removal           |
|                                                                                  |
|  [06. REPORTING] ===> Comprehensive Penetration Testing Documentation            |
+----------------------------------------------------------------------------------+
```

---

## 📦 Project Modules & Status

| Module ID | Module Name | Category | Scope | Status | Deliverables |
|---|---|:---:|---|:---:|---|
| **W3-PM1** | **Password Cracking with JTR** | **Essential** | Cracking locked PDF targets using John the Ripper (Jumbo) & Johnny GUI | ✅ Completed | [View Section](#-w3-pm1-password-cracking-with-john-the-ripper-jtr--johnny-gui) \| [📥 JTR Report](../Reports/Week3_Password_Cracking_JTR_Report.docx) |
| **W3-PM2** | **Password Cracking with NW Tools** | **Essential** | Hash calculation, dictionary attacks & custom wordlist generation | ✅ Completed | [View Section](#-w3-pm2-password-cracking-with-networkwalks-tools) \| [📥 NW Tools Report](../Reports/Week3_Password_Cracking_NetworkWalks_Tools_Report.docx) |
| **W3-OPTIONAL1** | AI-Assisted JTR Lab (Claude & Hexstrike MCP) | Optional | AI-augmented password cracking with Claude Desktop + MCP Server | ⬜ Documented | [View Section](#-w3-optional1-ai-assisted-jtr-lab-claude--hexstrike-mcp) |
| **W3-OPTIONAL2** | Mediroza Hospital Portal Hacking | Optional | Authorized patient portal CTF-style credential attack simulation | ⬜ Documented | [View Section](#-w3-optional2-mediroza-hospital-patient-portal-hacking) |

---

## 🎯 Cracking Targets & Recovered Credentials Summary

| Target File | Format / Encryption | Hash Prefix | Attack Method | Recovered Plaintext Password | Verification Status |
|---|---|---|---|:---:|:---:|
| **My Locked PDF1.pdf** | PDF 1.4 / 128-bit RC4 (R4/V4) | `$pdf$4*4*128*...` | JTR Default Dictionary / NW Cracker | **`good-luck`** | ✅ Unlocked (Flag Captured) |
| **My Locked PDF2.pdf** | PDF 1.4 / 128-bit RC4 (R4/V4) | `$pdf$4*4*128*...` | Custom Generated Wordlist | **`password1`** | ✅ Unlocked (Flag Captured) |
| **My Locked PDF3.pdf** | PDF 1.4 / 128-bit RC4 (R4/V4) | `$pdf$4*4*128*...` | 1,987-Word Target List | **`1qaz2wsx`** | ✅ Unlocked (Flag Captured) |

---

## 🔓 W3-PM1: Password Cracking with John the Ripper (JTR) & Johnny GUI

> **Tools Used:** John the Ripper v1.9.0-jumbo-1 (Cygwin 64-bit, x86_64 AVX2) + Johnny GUI v2.2

### Task 1: Cracking "My Locked PDF1"

1. **Hash Extraction:** Generated the `$pdf$` hash string from `My Locked PDF1.pdf` and saved it to `My Locked PDF1-Hash Value.txt`.
2. **Johnny Configuration:** Loaded JTR engine path and imported the hash into Johnny.
3. **Attack Execution:** Launched dictionary attack — JTR cracked the hash in seconds.
4. **Validation:** Opened PDF with recovered password `good-luck` to reveal the secret flag.

![Figure 1 — PDF Hash Extractor tool generating the hash](screenshots/jtr_figure1.png)
*Figure 1: PDF Hash Extractor tool generating the $pdf$ hash string for My Locked PDF1.*

![Figure 2 — Extracted hash saved locally as a .txt file](screenshots/jtr_figure2.png)
*Figure 2: Extracted hash saved locally as a .txt file for input into John the Ripper.*

![Figure 3 — Johnny main interface](screenshots/jtr_figure3.png)
*Figure 3: Johnny graphical interface configured with the target hash.*

![Figure 4 — Johnny Settings tab](screenshots/jtr_figure4.png)
*Figure 4: Johnny Settings tab confirming the John the Ripper executable path and detected version.*

![Figure 5 — Starting the attack in Johnny](screenshots/jtr_figure5.png)
*Figure 5: Hash loaded into Johnny, ready to begin the dictionary attack.*

![Figure 6 — Password cracked: good-luck](screenshots/jtr_figure6.png)
*Figure 6: Johnny displaying the successfully cracked password **`good-luck`** for PDF1.*

![Figure 7 — Entering recovered password into PDF prompt](screenshots/jtr_figure7.png)
*Figure 7: Entering the recovered password into the Adobe PDF password prompt.*

![Figure 8 — PDF successfully unlocked](screenshots/jtr_figure8.png)
*Figure 8: My Locked PDF1 successfully unlocked, revealing the captured flag.*

---

### Task 2: Cracking "My Locked PDF2"

1. **Hash Extraction:** Extracted `$pdf$` hash from `My Locked PDF2.pdf` and saved as `My Locked PDF2-Hash Value.txt`.
2. **Attack:** Executed JTR attack against the extracted hash string.
3. **Result:** Recovered plaintext password **`password1`**.
4. **Flag Captured:** Unlocked `My Locked PDF2.pdf` and confirmed document content.

![Figure 9 — Hash extracted and saved for PDF2](screenshots/jtr_figure9.png)
*Figure 9: Hash extracted and saved for My Locked PDF2.*

![Figure 10 — Password verification in PDF prompt](screenshots/jtr_figure10.png)
*Figure 10: Recovered password **`password1`** entered into the PDF password prompt.*

![Figure 11 — PDF2 unlocked and flag captured](screenshots/jtr_figure11.png)
*Figure 11: PDF2 successfully unlocked, confirming the recovered password.*

---

### Task 3: Cracking "My Locked PDF3"

1. **Hash Extraction:** Extracted `$pdf$` hash for `My Locked PDF3.pdf`.
2. **Attack:** Loaded `My Locked PDF3-Hash Value.txt` into Johnny and executed dictionary attack.
3. **Result:** Recovered keyboard-pattern plaintext password **`1qaz2wsx`** (100% complete, 1 cracked).
4. **Flag Captured:** Unlocked `My Locked PDF3.pdf` and verified document flag.

![Figure 12 — Hash extracted for PDF3](screenshots/jtr_figure12.png)
*Figure 12: Hash extracted and saved for My Locked PDF3.*

![Figure 13 — Selecting hash file in Johnny](screenshots/jtr_figure13.png)
*Figure 13: Selecting the My Locked PDF3 hash file inside Johnny's file picker.*

![Figure 14 — Starting attack in Johnny](screenshots/jtr_figure14.png)
*Figure 14: Starting attack in Johnny against the loaded PDF3 hash.*

![Figure 15 — Password cracked: 1qaz2wsx](screenshots/jtr_figure15.png)
*Figure 15: Johnny displaying the cracked password **`1qaz2wsx`** for My Locked PDF3.*

![Figure 16 — Verifying password in PDF prompt](screenshots/jtr_figure16.png)
*Figure 16: Recovered password entered into My Locked PDF3 prompt.*

![Figure 17 — PDF3 unlocked and third flag captured](screenshots/jtr_figure17.png)
*Figure 17: PDF3 successfully unlocked, revealing the third captured flag.*

---

## 🔧 W3-PM2: Password Cracking with NetworkWalks Tools

> **Platform:** NetworkWalks Password Cracker Lab & Hash Calculator (`networkwalks.com/password-cracker`)

### Task 1: Cracking PDF1 via NetworkWalks Online Tools

1. **Hash Extraction:** Uploaded `My Locked PDF1.pdf` to the NetworkWalks Hash Calculator to generate `$pdf$` hash.
2. **Initial Attempt:** Pasted hash into the Online Password Cracker with standard 100-word list → returned **ACCESS DENIED**.
3. **Wordlist Escalation:** Switched to the comprehensive `JTR_default_password.txt` (3,556 words).
4. **Result:** Cracked successfully → **`good-luck`**.

![Figure 18 — NW Hash Calculator landing page](screenshots/nw_figure1.png)
*Figure 18: NetworkWalks Hash Calculator landing page with PDF tab selected.*

![Figure 19 — Hash Calculator output](screenshots/nw_figure2.png)
*Figure 19: Hash Calculator output showing crackable $pdf$ hash string.*

![Figure 20 — NW Password Cracker landing page](screenshots/nw_figure3.png)
*Figure 20: NetworkWalks Password Cracker (Dictionary Attack Lab).*

![Figure 21 — Hash pasted with 100-word list](screenshots/nw_figure4.png)
*Figure 21: PDF1 hash pasted into Password Cracker with 100-word list selected.*

![Figure 22 — Access Denied result](screenshots/nw_figure5.png)
*Figure 22: First attack attempt failed (password not in top 100 list).*

![Figure 23 — Attack using JTR default wordlist](screenshots/nw_figure6.png)
*Figure 23: Second attack in progress using the 3,556-word JTR dictionary.*

![Figure 24 — Password Cracked: good-luck](screenshots/nw_figure7.png)
*Figure 24: PASSWORD CRACKED SUCCESSFULLY: **`good-luck`** recovered.*

![Figure 25 — Password prompt verification](screenshots/nw_figure8.png)
*Figure 25: Recovered password entered into PDF1 prompt.*

![Figure 26 — PDF1 unlocked](screenshots/nw_figure9.png)
*Figure 26: PDF1 unlocked and flag verified.*

---

### Task 2: Custom Wordlist Generation & Cracking PDF2

1. **Wordlist Mutation:** Used the NetworkWalks Wordlist Generator to create target-tailored passwords with suffix/prefix rules and leetspeak substitutions.
2. **Attack:** Executed attack against `My Locked PDF2` hash using generated custom list.
3. **Result:** Password recovered → **`password1`**.

![Figure 27 — Wordlist Generator tool](screenshots/nw_figure10.png)
*Figure 27: Wordlist Generator configuring base words, mutations, and append options.*

![Figure 28 — PDF2 Hash extraction](screenshots/nw_figure12.png)
*Figure 28: Hash Calculator extracting $pdf$ hash for My Locked PDF2.*

![Figure 29 — PDF2 Password Cracked: password1](screenshots/nw_figure13.png)
*Figure 29: PASSWORD CRACKED: **`password1`** recovered using the mutated wordlist.*

---

### Task 3: Cracking PDF3 with Custom Wordlist

1. **Hash Extraction:** Extracted `$pdf$` hash for PDF3 (313.5 KB, R4/V4 128-bit).
2. **Attack:** Executed dictionary attack using custom 1,987-word list.
3. **Result:** Password cracked → **`1qaz2wsx`**.
4. **Validation:** PDF3 unlocked and third flag captured.

![Figure 30 — PDF3 Hash extraction](screenshots/nw_figure14.png)
*Figure 30: Hash Calculator extracting $pdf$ hash for My Locked PDF3.*

![Figure 31 — Attack in progress](screenshots/nw_figure15.png)
*Figure 31: Attack in progress against PDF3 using the 1,987-word custom dictionary.*

![Figure 32 — PDF3 Password Cracked: 1qaz2wsx](screenshots/nw_figure16.png)
*Figure 32: PASSWORD CRACKED: **`1qaz2wsx`** recovered.*

![Figure 33 — Verification in PDF prompt](screenshots/nw_figure17.png)
*Figure 33: Password prompt verification for PDF3.*

![Figure 34 — PDF3 unlocked and flag captured](screenshots/nw_figure18.png)
*Figure 34: PDF3 unlocked, revealing the third captured flag.*

---

<details>
<summary><strong>📖 Linux CLI Password Cracking Cheatsheet (JTR, Hashcat & Hydra)</strong> — click to expand</summary>

### 1. John the Ripper (JTR) CLI Syntax
```bash
# Extract /etc/shadow hashes for cracking
sudo unshadow /etc/passwd /etc/shadow > hashes.txt

# Extract PDF password hash on Linux CLI
pdf2john.pl sample.pdf > pdf_hash.txt

# Dictionary attack with rockyou.txt
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt

# Apply rule mangling
john --wordlist=/usr/share/wordlists/rockyou.txt --rules=Jumbo hashes.txt

# Incremental brute-force mode
john --incremental hashes.txt

# Show cracked credentials
john --show hashes.txt
```

### 2. Hashcat GPU Cracking
```bash
# Identify hash format
hashid <hash_string>

# Dictionary attack (Mode 1800 = SHA-512 crypt, Mode 10500 = PDF 1.4-1.6)
hashcat -m 10500 -a 0 pdf_hash.txt /usr/share/wordlists/rockyou.txt

# Rule-based attack
hashcat -m 10500 -a 0 pdf_hash.txt /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best64.rule

# Display results
hashcat -m 10500 pdf_hash.txt --show
```

### 3. Online Authentication Attacks with Hydra
```bash
# SSH Login Brute-Force
hydra -l root -P /usr/share/wordlists/rockyou.txt 10.0.2.x ssh

# FTP Login Brute-Force
hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.0.2.x ftp

# Web Form Login Brute-Force
hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.0.2.x http-post-form "/login:user=^USER^&pass=^PASS^:Invalid"
```

</details>

---

## 🤖 W3-OPTIONAL1: AI-Assisted JTR Lab (Claude & Hexstrike MCP)

> **Prerequisites:** Claude Desktop installed + Hexstrike MCP Server configured.

- **Objective:** AI-augmented password cracking where Claude (via Hexstrike MCP v1) analyzes hash formats, recommends cracking strategies, and automates target-specific wordlist generation.

---

## 🏥 W3-OPTIONAL2: Mediroza Hospital Patient Portal Hacking

> **Target:** Authorized CTF Web Lab — Mediroza Hospital Portal

- **Objective:** Controlled web application penetration testing against healthcare authentication portals (testing for credential stuffing, missing rate limiting, and broken access controls).

---

## 📄 W3-PM-FINAL: Password Cracking Reports

The formal deliverables for Week 3 are available in the [`Reports/`](../Reports/) directory:

- 📥 **[Week 3 JTR Password Cracking Report (DOCX)](../Reports/Week3_Password_Cracking_JTR_Report.docx)** — W3-PM1
- 📥 **[Week 3 NW Tools Password Cracking Report (DOCX)](../Reports/Week3_Password_Cracking_NetworkWalks_Tools_Report.docx)** — W3-PM2

---

## 💡 What I Learned

1. **Hash Identification & Extraction:** Transforming encrypted documents and hashes into format-compatible syntax (`$pdf$`, `$6$`, `$y$`) is the critical starting phase of any cracking workflow.
2. **Wordlist Sizing & Escalation Strategy:** Starting with small, rapid wordlists before escalating to larger dictionaries (`rockyou.txt`, JTR default) or applying rule-based mutations optimizes cracking time.
3. **Pattern-Based Passwords Vulnerability:** Passwords following common keyboard walks (e.g., `1qaz2wsx`) or base word + single digit (e.g., `password1`) are trivially broken by dictionary mutation rules within seconds.
4. **Defensive Remediations:** Organizations must enforce strong password entropy, multi-factor authentication (MFA), and modern key derivation functions (Argon2, bcrypt, PBKDF2) to resist offline brute-forcing.

---

## ⚖️ Ethical Statement

> All password cracking activities were performed exclusively against **authorized lab targets** and files provided within the NetworkWalks Academy training curriculum. No unauthorized systems or third-party networks were targeted.

---

> 📂 [Back to Main README](../README.md) | 📋 [Reports](../Reports/) | 🔗 [Resources](../Resources/README.md)
