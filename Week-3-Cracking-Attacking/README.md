# ⚔️ Week 3 — Password Cracking & Attacking

> **NetworkWalks Academy | Batch B082 | August 2026**
>
> **Track:** Offensive (Red Team) — Phase 3 (Gaining Access)
>
> **Submission Deadline:** 23:00H, Friday 28-August-2026

---

## 📋 Project Overview

Week 3 focuses on **Phase 3 of the ethical hacking lifecycle — Gaining Access** through controlled password cracking and authentication attacks. Using industry-standard tools (John The Ripper, Hashcat, Hydra) against authorized lab targets, we learn to crack password hashes, perform dictionary/brute-force attacks, and understand how weak credential policies are exploited in real-world penetration tests.

```
+----------------------------------------------------------------------------------+
|                          5 PHASES OF HACKING — WEEK 3 FOCUS                     |
+----------------------------------------------------------------------------------+
|  [01. FOOTPRINTING] -> [02. SCANNING] -> [03. GAINING ACCESS]  <== WEEK 3       |
|  (Week 2 Complete)    (Week 2 Complete)   Password Cracking / Exploitation       |
|                                                                                  |
|                                       -> [04. MAINTAINING ACCESS]  (Week 3/4)   |
|                                           Backdoors & Persistence                |
|                                                                                  |
|                                       -> [05. CLEARING LOGS]       (Week 4)     |
|                                           Anti-forensics & Log Removal           |
|                                                                                  |
|  [06. REPORTING] ===> Penetration Testing Documentation                          |
+----------------------------------------------------------------------------------+
```

---

## 📦 Project Modules & Status

| Module ID | Module Name | Category | Scope | Status | Deliverables |
|---|---|:---:|---|:---:|---|
| **W3-PM1** | **Password Cracking with JTR** | **Essential** | Hash cracking using John The Ripper (`/etc/shadow`, wordlists, rules) | 🔄 In Progress | [View Section](#-w3-pm1-password-cracking-with-john-the-ripper-jtr) |
| **W3-PM2** | **Password Cracking with NW Tools** | **Essential** | NetworkWalks-guided cracking methodology & custom toolchain | 🔄 In Progress | [View Section](#-w3-pm2-password-cracking-with-nw-tools) |
| **W3-OPTIONAL1** | AI-Assisted JTR Lab (Claude & Hexstrike MCP) | Optional | AI-augmented password cracking with Claude Desktop + MCP Server | ⬜ Optional | [View Section](#-w3-optional1-ai-assisted-jtr-lab-claude--hexstrike-mcp) |
| **W3-OPTIONAL2** | Mediroza Hospital Portal Hacking | Optional | Authorized patient portal CTF-style credential attack simulation | ⬜ Optional | [View Section](#-w3-optional2-mediroza-hospital-patient-portal-hacking) |

> ⚠️ **Note:** Both Essential modules (W3-PM1 & W3-PM2) must be completed. Optional modules are bonus challenges.

---

## 🛠️ Tools & Frameworks

| Tool | Purpose | Primary Use Case |
|---|---|---|
| 🔓 **John The Ripper (JTR)** | Offline Hash Cracking | Dictionary, brute-force & rule-based attacks on `/etc/shadow` |
| 🧠 **Hashcat** | GPU-Accelerated Hash Cracking | High-speed offline password recovery |
| 🔑 **Hydra** | Online Authentication Attacks | Network service login cracking (SSH, FTP, HTTP, RDP) |
| 📖 **rockyou.txt** | Wordlist | Industry-standard 14M+ password dictionary |
| 🤖 **Claude Desktop + Hexstrike MCP** | AI-Assisted Lab (Optional) | AI-guided attack workflow automation |

---

## 🎯 Lab Targets

> ⚠️ **All activities performed strictly against authorized lab targets within `10.0.2.0/24`.**

| Target | IP | OS | Vulnerable Services |
|---|---|---|---|
| **Kali Linux (Local)** | `10.0.2.15` | Kali 2026.2 | Local `/etc/shadow` hash extraction |
| **Metasploitable 2** | `10.0.2.x` | Ubuntu Linux (Vulnerable) | FTP, SSH, Telnet, SMB, HTTP |
| **Mediroza Hospital Portal** | Web App (CTF) | Authorized Lab Target | Patient Portal login (Optional) |

---

## 🔓 W3-PM1: Password Cracking with John The Ripper (JTR)

> **Resource:** [John The Ripper Official](https://www.openwall.com/john/)

### Step 1: Extract & Unshadow Password Hashes

```bash
# View the shadow file (requires root)
sudo cat /etc/shadow

# Combine /etc/passwd and /etc/shadow into a crackable format
sudo unshadow /etc/passwd /etc/shadow > hashes.txt

# Verify the combined output
cat hashes.txt
```

### Step 2: Identify Hash Type

```bash
# Inspect the hash format ($y$ = yescrypt, $6$ = SHA-512, $1$ = MD5)
head -5 hashes.txt
```

| Hash Prefix | Algorithm | Cracking Difficulty |
|---|---|---|
| `$y$` | yescrypt | Very High (modern default) |
| `$6$` | SHA-512 | High |
| `$5$` | SHA-256 | Medium-High |
| `$1$` | MD5-crypt | Low-Medium |
| `$2y$` | bcrypt | Very High |

### Step 3: Dictionary Attack with rockyou.txt

```bash
# Run dictionary attack against extracted hashes
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt

# Show cracked passwords
john --show hashes.txt

# Check John's cracking session status
john --status
```

### Step 4: Rule-Based Attack

```bash
# Apply built-in word mangling rules (capitalisation, l33t substitution, etc.)
john --wordlist=/usr/share/wordlists/rockyou.txt --rules hashes.txt

# Use a specific rule set
john --wordlist=/usr/share/wordlists/rockyou.txt --rules=Jumbo hashes.txt
```

### Step 5: Brute-Force Attack (Incremental Mode)

```bash
# Full incremental brute-force (time-intensive)
john --incremental hashes.txt

# Target a specific character set
john --incremental=Digits hashes.txt
```

### Key JTR Flags Reference

| Flag | Example | Description |
|---|---|---|
| `--wordlist` | `--wordlist=rockyou.txt` | Dictionary / wordlist attack |
| `--rules` | `--rules` | Apply word mangling rules |
| `--incremental` | `--incremental` | Brute-force all combinations |
| `--format` | `--format=sha512crypt` | Specify exact hash format |
| `--show` | `--show hashes.txt` | Display all cracked credentials |
| `--restore` | `--restore` | Resume an interrupted session |

---

## 🔧 W3-PM2: Password Cracking with NW Tools

> **Resource:** NetworkWalks Academy — Week 3 NW Tools Module
>
> **Lab Guide:** [networkwalks.com](https://www.networkwalks.com)

### Step 1: Hash Identification

```bash
# Identify unknown hash type
hashid <hash_value>

# Example
hashid '$6$rounds=5000$salt$hash...'
```

### Step 2: Hashcat GPU-Accelerated Cracking

```bash
# Dictionary attack with Hashcat (SHA-512 = mode 1800)
hashcat -m 1800 hashes.txt /usr/share/wordlists/rockyou.txt

# With rules for better coverage
hashcat -m 1800 hashes.txt /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best64.rule

# Show cracked results
hashcat -m 1800 hashes.txt --show
```

### Step 3: Online Service Attack with Hydra

```bash
# SSH brute-force
hydra -l root -P /usr/share/wordlists/rockyou.txt 10.0.2.x ssh

# FTP brute-force
hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.0.2.x ftp

# HTTP POST form attack
hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.0.2.x http-post-form "/login:username=^USER^&password=^PASS^:Invalid"

# Limit threads to avoid lockout (default 16)
hydra -l admin -P rockyou.txt -t 4 10.0.2.x ssh
```

### Hashcat Attack Mode Reference

| Mode | Flag | Description |
|---|---|---|
| Dictionary | `-a 0` | Wordlist attack (default) |
| Combination | `-a 1` | Combine two wordlists |
| Brute-Force | `-a 3` | Mask-based character set attack |
| Rule-Based | `-a 0 -r rule` | Dictionary + transformation rules |

---

## 🤖 W3-OPTIONAL1: AI-Assisted JTR Lab (Claude & Hexstrike MCP)

> ⚠️ **Prerequisites:** Claude Desktop installed + Hexstrike MCP Server configured.
>
> **Note:** This optional lab requires MCP Server setup with Claude Desktop before starting.

### Overview

An AI-augmented password cracking workflow where Claude (via Hexstrike MCP v1) assists in:
- Analyzing hash formats and recommending optimal cracking strategies
- Generating targeted wordlists based on target OSINT (names, dates, company)
- Automating JTR command generation and interpreting results

### Setup (Required First)
1. Install **Claude Desktop** from [claude.ai/download](https://claude.ai/download)
2. Configure **Hexstrike MCP Server** per NetworkWalks Academy instructions
3. Connect MCP to Claude Desktop via `claude_desktop_config.json`

<!-- Add screenshots and MCP configuration output when completed -->

---

## 🏥 W3-OPTIONAL2: Mediroza Hospital Patient Portal Hacking

> ⚠️ **Authorized lab target only.** This is a controlled CTF-style simulation.

### Overview

A guided web application credential attack against the **Mediroza Hospital patient portal** — an authorized NetworkWalks Academy lab target simulating real-world healthcare portal vulnerabilities.

### Attack Workflow
1. **Reconnaissance** — Identify login endpoints, form parameters, error messages
2. **Credential Stuffing** — Test common default credentials
3. **Brute-Force / Dictionary Attack** — Use Hydra or Burp Suite Intruder
4. **Privilege Escalation** — Test for horizontal/vertical access control flaws

<!-- Add screenshots, captured flags, and findings when completed -->

---

## 🐞 Troubleshooting Log

| Issue Encountered | Root Cause | Resolution |
|---|---|---|
| | | |

---

## 💡 What I Learned

1. **Hash Identification is Critical:** The cracking strategy depends entirely on the algorithm — always identify the hash type first.
2. **Wordlist Quality > Brute Force:** `rockyou.txt` + rules recovers more passwords faster than pure incremental brute-force.
3. **Online vs Offline Attacks:** Offline cracking (JTR/Hashcat) has no lockout risk; online attacks (Hydra) must throttle threads to avoid account lockouts and IDS alerts.
4. **Password Policy Awareness:** Short, predictable passwords fall within seconds — strong policies and salted hashing are essential defenses.

---

## ⚖️ Ethical Statement

> All password cracking activities were performed exclusively against **authorized lab targets** (`10.0.2.0/24` and authorized NetworkWalks Academy web targets). No unauthorized systems were accessed. All work is strictly for educational penetration testing practice.

---

> 📂 [Back to Main README](../README.md) | 📋 [Reports](../Reports/) | 🔗 [Resources](../Resources/README.md)


