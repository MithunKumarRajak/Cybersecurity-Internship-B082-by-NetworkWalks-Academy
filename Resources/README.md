# 📚 Resources, References & Cheat Sheets

> **NetworkWalks Academy | Batch B082 | August 2026**

---

## 📋 Overview

A practical reference guide containing verified software download sources, official documentation, web security databases, and command cheat sheets directly practiced in the **Cybersecurity & Ethical Hacking Internship**.

---

## 🛠️ Lab Software & Downloads

### Hypervisor & Utilities

| Software | Version / Purpose | Official Source |
|---|---|---|
| 🧰 **Oracle VirtualBox** | Type-2 Hypervisor for isolated lab environment | [VirtualBox Downloads](https://virtualbox.org/wiki/Downloads) |
| 📦 **7-Zip** | Archive utility for `.7z` VM image extraction | [7-Zip Official](https://7-zip.org/download.html) |

### Operating System & Security Tools

| System / Tool | Role | Official Source |
|---|---|---|
| 🐉 **Kali Linux 2026.2** | Attacker VM (Pre-built VirtualBox Image) | [Kali Linux Get-Kali](https://kali.org/get-kali) |
| 👁️ **Nmap & Zenmap** | Free Security Scanner & Network Exploration Tool | [Nmap Official Downloads](https://nmap.org/download.html) |
| 🌐 **ScanMe (Nmap)** | Authorized Public Practice Target for Port Scanning | [scanme.nmap.org](http://scanme.nmap.org/) |
| 🔍 **Google Hacking Database** | OSINT Dorking & Google Reconnaissance Repository | [GHDB on Exploit-DB](https://www.exploit-db.com/google-hacking-database) |
| 📚 **Zenmap Lab Tutorial** | NetworkWalks Academy Zenmap Scanning Practical | [NetworkWalks Zenmap Guide](https://networkwalks.com/lab-practice-network-scanning-with-zenmap/) |

---

## 📖 Nmap Cheatsheet & Command Reference (NetworkWalks Series)

### 1. Target Selection Syntax
```bash
# Scan a single IP address
nmap 10.0.0.1

# Scan a domain or hostname
nmap www.networkwalks.com

# Scan a range of IP addresses
nmap 10.0.0.1-99

# Scan multiple distinct IPs
nmap 10.0.0.1,10.0.0.2

# Scan an entire CIDR subnet
nmap 10.0.0.0/24

# Scan targets listed in a text file
nmap -iL LIST1.txt

# Exclude specific targets from a subnet scan
nmap 10.0.0.0/24 --exclude 10.0.0.1
```

### 2. Target Scan Types
```bash
# TCP SYN / Stealth Scan (default with root privileges)
nmap 10.0.0.1 -sS

# TCP Connect Scan (completes 3-way handshake, no root needed)
nmap 10.0.0.1 -sT

# TCP ACK Scan (maps firewall rule sets and filters)
nmap 10.0.0.1 -sA

# TCP FIN Scan (probes for RFC 793 compliance)
nmap 10.0.0.1 -sF

# UDP Port Scan (identifies DNS, SNMP, DHCP services)
nmap 10.0.0.1 -sU

# TCP Xmas Scan (sets FIN, URG, and PSH flags)
nmap 10.0.0.1 -sX

# List Scan (simply enumerates targets without sending probes)
nmap 10.0.0.0/24 -sL

# Ping Sweep (Host discovery only, no port scanning)
nmap -sn 10.0.0.0/24

# Aggressive Scan (OS detection, service versions, script scanning, traceroute)
nmap 10.0.0.1 -A

# Fast Scan (probes top 100 most common ports)
nmap 10.0.0.1 -F

# Scan over IPv6
nmap -6 [2001:db8::1]
```

### 3. Port Selection Options
```bash
# Scan a single port
nmap 10.0.0.1 -p 21

# Scan multiple specific ports
nmap 10.0.0.1 -p 21,22,80,443

# Scan a custom port range
nmap 10.0.0.1 -p 1-1000

# Scan by service name
nmap 10.0.0.1 -p ssh,http,https

# Scan all 65,535 TCP ports
nmap 10.0.0.1 -p-
```

### 4. Version & OS Detection
```bash
# Remote Operating System detection
nmap 10.0.0.1 -O

# Service version detection on open ports
nmap 10.0.0.1 -sV

# Maximum version probing intensity (0 to 9)
nmap 10.0.0.1 -sV --version-intensity 9
```

### 5. Scan Speed & Timing Templates
- `-T0` (Paranoid) / `-T1` (Sneaky): Slow scans for IDS/IPS evasion
- `-T2` (Polite): Bandwidth-friendly scanning
- `-T3` (Normal): Default timing template
- `-T4` (Aggressive): Recommended for fast, reliable local lab scanning
- `-T5` (Insane): Maximum speed (may drop packets on congested networks)

### 6. Miscellaneous, Evasion & Output Flags
```bash
# Save output in standard human-readable text format
nmap -oN scan_output.txt 10.0.0.1

# Save output in XML format (for importing to tools/frameworks)
nmap -oX scan_output.xml 10.0.0.1

# Save in all three major formats (Nmap, XML, Grepable)
nmap -oA pentest_results 10.0.0.1

# Spoof source IP address
nmap -S 10.0.0.99 10.0.0.1

# Specify source network interface
nmap -e eth0 10.0.0.1

# Spoof MAC address
nmap --spoof-mac 00:11:22:33:44:55 10.0.0.1

# Run Nmap Scripting Engine (NSE) vulnerability checks
nmap --script vuln 10.0.0.1
```

---

## 🔎 Footprinting & OSINT Quick Reference

```bash
# Query domain registration details
whois networkwalks.com

# Web application technology fingerprinting
whatweb -v -a 3 https://www.networkwalks.com

# DNS resolution
nslookup networkwalks.com

# HTTP Header inspection
curl -I https://www.networkwalks.com

# Web Application Firewall (WAF) detection
wafw00f https://www.networkwalks.com

# Comprehensive DNS enumeration
dnsrecon -d networkwalks.com -t std

# OSINT email and subdomain harvesting
theHarvester -d networkwalks.com -b all -l 100
```

---

## 🔐 Password Cracking & PDF Extraction Quick Reference

```bash
# Extract hash from encrypted PDF document
pdf2john patient_report.pdf > pdf.hash

# Crack PDF hash with John the Ripper using wordlist
john --wordlist=/usr/share/wordlists/rockyou.txt pdf.hash

# Crack PDF hash using wordlist rules
john --wordlist=/usr/share/wordlists/rockyou.txt --rules=Jumbo pdf.hash

# Display cracked passwords from John database
john --show pdf.hash

# GPU-accelerated PDF hash cracking with Hashcat
# Mode 10500: PDF 1.4 - 1.6 (Acrobat 5 - 8)
# Mode 10600: PDF 1.7 Level 3 (Acrobat 9)
# Mode 10700: PDF 1.7 Level 8 (Acrobat X - XI)
hashcat -m 10500 -a 0 pdf.hash /usr/share/wordlists/rockyou.txt
```

---

## 📚 Official Documentation & Manuals

| Resource | Scope | Link |
|---|---|---|
| **Kali Linux Official Documentation** | OS configuration, package management & tool usage | [kali.org/docs](https://www.kali.org/docs/) |
| **Nmap Reference Guide** | Official command-line flags, scan types & NSE scripts | [nmap.org/book/man.html](https://nmap.org/book/man.html) |
| **Exploit-DB GHDB** | Verified Google Dorks and OSINT patterns | [exploit-db.com/ghdb](https://www.exploit-db.com/google-hacking-database) |
| **Oracle VirtualBox User Manual** | Networking modes (NAT vs NAT Network), snapshot management | [virtualbox.org/manual](https://www.virtualbox.org/manual/) |
| **OWASP Top 10 Web Security Risks** | Standard awareness document for developers and security professionals | [owasp.org/Top10](https://owasp.org/www-project-top-ten/) |
| **HIPAA Security Rule Standards** | National standards for the protection of Electronic Protected Health Information (ePHI) | [hhs.gov/hipaa](https://www.hhs.gov/hipaa/for-professionals/security/index.html) |

---

## 🏛️ Program References

- 🌐 **NetworkWalks Academy:** [networkwalks.com](https://www.networkwalks.com)
- 🏢 **NetworkWalks LinkedIn:** [Company Page](https://linkedin.com/company/networkwalks/)
- 👨‍🏫 **Lead Instructor:** [Waqas Karim (CCIE)](https://linkedin.com/in/waqaskarim/)

---

## 🔗 Week Quick Links

| Week | Module | Direct Link | Status |
|:---:|---|---|:---:|
| **1** | Lab Setup — Kali Linux + VirtualBox | [Week-1 README](../Week-1-Lab-Setup/README.md) | ✅ Completed |
| **2** | Footprinting, Scanning & Report Writing | [Week-2 README](../Week-2-Footprinting-Scanning/README.md) | ✅ Completed |
| **3** | Cracking & Attacking — JTR & NW Tools | [Week-3 README](../Week-3-Cracking-Attacking/README.md) | ✅ Completed |
| **4** | Capstone Pentest: Mediroza General Hospital | [Week-4 README](../Week-4-Full-Pentest-Project/README.md) | 🔄 In Progress |

---

> 📂 [Back to Main README](../README.md)
