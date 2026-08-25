# ðŸ”— Resources & Lab Reference Guide

> **NetworkWalks Academy | Batch B082 | August 2026**

---

## ðŸ“‹ Overview

A practical reference guide containing verified software download sources, official documentation, web security databases, and command cheat sheets directly practiced in the **Cybersecurity & Ethical Hacking Internship**.

---

## ðŸ› ï¸ Lab Software & Downloads

### Hypervisor & Utilities

| Software | Version / Purpose | Official Source |
|---|---|---|
| ðŸ§° **Oracle VirtualBox** | Type-2 Hypervisor for isolated lab environment | [VirtualBox Downloads](https://virtualbox.org/wiki/Downloads) |
| ðŸ“¦ **7-Zip** | Archive utility for `.7z` VM image extraction | [7-Zip Official](https://7-zip.org/download.html) |

### Operating System & Security Tools

| System / Tool | Role | Official Source |
|---|---|---|
| ðŸ‰ **Kali Linux 2026.2** | Attacker VM (Pre-built VirtualBox Image) | [Kali Linux Get-Kali](https://kali.org/get-kali) |
| ðŸ‘ï¸ **Nmap & Zenmap** | Free Security Scanner & Network Exploration Tool | [Nmap Official Downloads](https://nmap.org/download.html) |
| ðŸŒ **ScanMe (Nmap)** | Authorized Public Practice Target for Port Scanning | [scanme.nmap.org](http://scanme.nmap.org/) |
| ðŸ” **Google Hacking Database** | OSINT Dorking & Google Reconnaissance Repository | [GHDB on Exploit-DB](https://www.exploit-db.com/google-hacking-database) |
| ðŸ“š **Zenmap Lab Tutorial** | NetworkWalks Academy Zenmap Scanning Practical | [NetworkWalks Zenmap Guide](https://networkwalks.com/lab-practice-network-scanning-with-zenmap/) |

---

## ðŸ“– Nmap Cheatsheet & Command Reference (NetworkWalks Series)

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

## ðŸ”Ž Footprinting & OSINT Quick Reference

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

## ðŸ“š Official Documentation & Manuals

| Resource | Scope | Link |
|---|---|---|
| **Kali Linux Official Documentation** | OS configuration, package management & tool usage | [kali.org/docs](https://www.kali.org/docs/) |
| **Nmap Reference Guide** | Official command-line flags, scan types & NSE scripts | [nmap.org/book/man.html](https://nmap.org/book/man.html) |
| **Exploit-DB GHDB** | Verified Google Dorks and OSINT patterns | [exploit-db.com/ghdb](https://www.exploit-db.com/google-hacking-database) |
| **Oracle VirtualBox User Manual** | Networking modes (NAT vs NAT Network), snapshot management | [virtualbox.org/manual](https://www.virtualbox.org/manual/) |

---

## ðŸ›ï¸ Program References

- ðŸŒ **NetworkWalks Academy:** [networkwalks.com](https://www.networkwalks.com)
- ðŸ¢ **NetworkWalks LinkedIn:** [Company Page](https://linkedin.com/company/networkwalks/)
- ðŸ‘¨â€ðŸ« **Lead Instructor:** [Waqas Karim (CCIE)](https://linkedin.com/in/waqaskarim/)

---

## ðŸ”— Week Quick Links

| Week | Module | Direct Link |
|:---:|---|---|
| **1** | Lab Setup â€” Kali Linux + VirtualBox | [Week-1 README](../Week-1-Lab-Setup/README.md) |
| **2** | Footprinting, Scanning & Report Writing | [Week-2 README](../Week-2-Footprinting-Scanning/README.md) |
| **2** | Pentest Report (Markdown) | [Week2_Pentest_Report.md](../Reports/Week2_Pentest_Report.md) |
| **2** | Footprinting Report (DOCX) | [Week2_Footprinting_Reconnaissance_Report.docx](../Reports/Week2_Footprinting_Reconnaissance_Report.docx) |
| **2** | Zenmap Report (DOCX) | [Week2_Zenmap_Report.docx](../Reports/Week2_Zenmap_Report.docx) |
| **3** | Cracking & Attacking — JTR & NW Tools (In Progress) | [Week-3 README](../Week-3-Cracking-Attacking/README.md) |
| **4** | Full Pentest + SOC Analysis (Upcoming) | [Week-4 README](../Week-4-Full-Pentest-Project/README.md) |

---

> ðŸ“‚ [Back to Main README](../README.md)

