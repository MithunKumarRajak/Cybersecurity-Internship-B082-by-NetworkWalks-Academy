# 🔍 Week 2 — Footprinting, Scanning & Report Writing

> **NetworkWalks Academy | Batch B082 | August 2026**
>
> **Track:** Offensive (Red Team) — Phase 1 (Reconnaissance) & Phase 2 (Scanning)
>
> **Submission Deadline:** 23:00H, Friday 28-August-2026

---

## 📋 Project Overview

Week 2 focuses on the foundational phases of ethical hacking and penetration testing: **Footprinting (Reconnaissance)** and **Network Scanning**. Using Kali Linux tools and Zenmap/Nmap, we systematically gather open-source intelligence (OSINT), fingerprint web infrastructures, discover live hosts on our network, map active services, and compile a client-ready **Penetration Testing Report (W2-PM-FINAL)**.

```
+---------------------------------------------------------------------------------------+
|                                5 PHASES OF HACKING                                    |
+---------------------------------------------------------------------------------------+
|  [01. FOOTPRINTING]  ->  [02. SCANNING]  ->  [03. GAINING ACCESS]                     |
|  Gather OSINT & Data     Find Open Ports     Password Cracking / Exploitation         |
|                                                                                       |
|                                          ->  [04. MAINTAINING ACCESS]                 |
|                                              Backdoors & Persistence                  |
|                                                                                       |
|                                          ->  [05. CLEARING LOGS]                      |
|                                              Anti-forensics & Log Removal             |
|                                                                                       |
|  [06. REPORTING] ===> Comprehensive Penetration Testing Documentation (W2-PM-FINAL)   |
+---------------------------------------------------------------------------------------+
```

---

## 📦 Project Modules & Status

| Module ID | Module Name | Category | Scope | Status | Deliverable Link |
|---|---|:---:|---|:---:|---|
| **W2-PM1** | Multi-Tool Kali Footprinting | **Elective** | 6 Kali tools (`whois`, `whatweb`, `nslookup`, `curl`, `wafw00f`, `dnsrecon`) | ✅ Completed | [View Section](#-w2-pm1-footprinting-with-multiple-kali-tools) |
| **W2-PM2** | Google Hacking Database (GHDB) | Elective | Google Dorks & search operator reconnaissance | 📚 Documented | [View Section](#-w2-pm2-ghdb-based-footprinting-attacks) |
| **W2-PM3** | Maltego Reconnaissance | Elective | Graph-based entity link analysis & transforms | 📚 Documented | [View Section](#-w2-pm3-maltego-based-footprinting-attacks) |
| **W2-PM4** | theHarvester OSINT | Elective | Email, domain, subdomain & IP enumeration | 📚 Documented | [View Section](#-w2-pm4-theharvester-based-footprinting-attacks) |
| **W2-PM5** | **Zenmap / Nmap Scanning** | **Essential** | Host discovery, port scanning, OS/service detection, topology | ✅ Completed | [View Section](#-w2-pm5-zenmap--nmap-network-scanning-essential) |
| **W2-PM-FINAL** | **Formal Pentest Report** | **Essential** | Professional client-ready vulnerability assessment report | ✅ Completed | [📄 Pentest Report](../Reports/Week2_Pentest_Report.md) |

---

## 🔬 W2-PM1: Footprinting with Multiple Kali Tools

Target: Authorized domain **`networkwalks.com`**

```
+-----------------------------------------------------------------------------------+
|                        W2-PM1: 6 KALI RECONNAISSANCE TASKS                        |
+-----------------------------------------------------------------------------------+
| 1. whois      -> Domain Ownership, Registrar & Nameservers                        |
| 2. whatweb    -> CMS (WordPress 7.0.4) & Plugins (WP Download Manager 3.3.58)     |
| 3. nslookup   -> Public IP Resolution (192.232.216.135)                           |
| 4. curl -I    -> HTTP Response Headers & WordPress REST API (/wp-json/)           |
| 5. wafw00f    -> Web Application Firewall Detection (ModSecurity SpiderLabs)      |
| 6. dnsrecon   -> Comprehensive DNS Records (NS, MX, SPF/TXT, SRV Records)         |
+-----------------------------------------------------------------------------------+
```

### Task 1: Domain Registration Enumeration (`whois`)
- **Objective:** Find domain registration details (owner, registrar, creation/expiration dates, name servers).
- **Command:**
  ```bash
  whois networkwalks.com
  ```
- **Key Findings:** Registrar identity, status codes, creation & renewal timeline, authoritative nameservers.
- **Attacker Insight:** Reveals contact channels, infrastructure providers, and contract lifecycles for social engineering or domain hijacking monitoring.

### Task 2: Web Technology Fingerprinting (`whatweb`)
- **Objective:** Fingerprint web technologies, CMS engine, and plugins.
- **Command:**
  ```bash
  whatweb -v -a 3 https://www.networkwalks.com
  ```
- **Key Findings:** Web server software, **WordPress 7.0.4**, and **WP Download Manager (v3.3.58)** plugin.
- **Attacker Insight:** Exposes specific CMS/plugin version identifiers that can be correlated with public exploit databases (NVD, Exploit-DB).

### Task 3: Domain Name Resolution (`nslookup`)
- **Objective:** Resolve domain name to its public IP address via DNS.
- **Command:**
  ```bash
  nslookup networkwalks.com
  ```
- **Key Findings:** Resolved IP address: **`192.232.216.135`**.
- **Attacker Insight:** Pinpoints the host IP address for scope boundary validation, geolocation analysis, and network-level targeting.

### Task 4: HTTP Header & Endpoint Inspection (`curl -I`)
- **Objective:** Read raw HTTP response headers without loading page body.
- **Command:**
  ```bash
  curl -I https://www.networkwalks.com
  ```
- **Key Findings:** Server response headers, Content-Type, and exposed WordPress REST API Link: `<https://networkwalks.com/wp-json/>; rel="https://api.w.org/"`.
- **Attacker Insight:** Header inspection reveals backend technologies and REST API endpoints that may permit unauthenticated user and post enumeration.

### Task 5: Web Application Firewall Detection (`wafw00f`)
- **Objective:** Detect whether a Web Application Firewall protects the web server.
- **Command:**
  ```bash
  wafw00f https://www.networkwalks.com
  ```
- **Key Findings:** WAF Identified: **ModSecurity (SpiderLabs)**.
- **Attacker Insight:** Alerts the tester to active web inspection rules, preventing naive attack attempts and highlighting the need for encoding/obfuscation.

### Task 6: DNS Infrastructure Enumeration (`dnsrecon`)
- **Objective:** Enumerate all DNS records (NS, MX, SPF, TXT, SRV).
- **Command:**
  ```bash
  dnsrecon -d networkwalks.com -t std
  ```
- **Key Findings:** Authoritative Name Servers, Mail Exchangers (MX), SPF verification records, and service records.
- **Attacker Insight:** Maps organization mail servers, cloud tenants, and potential subdomains.

---

## 🔎 W2-PM2: GHDB-based Footprinting Attacks

> **Resource:** [Google Hacking Database (GHDB) on Exploit-DB](https://www.exploit-db.com/google-hacking-database)

Google Dorking utilizes advanced search operators to uncover sensitive data indexed by Google search engines:

| Category | Dork Syntax | Security Significance |
|---|---|---|
| **Subdomain Discovery** | `site:networkwalks.com -www` | Finds forgotten staging/dev subdomains |
| **Exposed Documents** | `site:networkwalks.com filetype:pdf OR filetype:docx` | Identifies public manuals, invoices, or briefs |
| **Config / Backup Files** | `site:networkwalks.com ext:env OR ext:sql OR ext:bak` | Locates database dumps, environment secrets |
| **Admin Login Portals** | `site:networkwalks.com inurl:login OR inurl:admin` | Maps entry points for credential attacks |
| **Directory Indexing** | `site:networkwalks.com intitle:"index of /"` | Uncovers unprotected file directory listings |

---

## 🌐 W2-PM3: Maltego-based Footprinting Attacks

- **Overview:** Graph-based Open Source Intelligence (OSINT) and link analysis tool.
- **Workflow:**
  1. Initialize new graph and drag **Domain** entity (`networkwalks.com`).
  2. Run standard transforms: `To DNS Name`, `To IP Address`, `To Nameserver`, `To Mail Server`.
  3. Expand infrastructure graph to identify shared IP blocks, ASN ownership, and affiliated entities.

---

## 🌾 W2-PM4: theHarvester-based Footprinting Attacks

- **Command Syntax:**
  ```bash
  theHarvester -d networkwalks.com -b all -l 100
  ```
- **OSINT Harvested:**
  - Public corporate email addresses.
  - Subdomains and virtual hosts across public search engines.
  - Employee names, LinkedIn associations, and public IP ranges.

---

## 📡 W2-PM5: Zenmap & Nmap Network Scanning (Essential)

> **Resources:**
> - [Download Nmap / Zenmap Official](https://nmap.org/download.html)
> - [Lab Practice — Zenmap Network Scanning Guide](https://networkwalks.com/lab-practice-network-scanning-with-zenmap/)
> - [Authorized Practice Target: scanme.nmap.org](http://scanme.nmap.org/)

### 📖 Nmap Cheatsheet (NetworkWalks Reference)

#### 1. Target Selection
| Switch / Syntax | Example | Description |
|---|---|---|
| `nmap [IP]` | `nmap 10.0.0.1` | Scan a single IP |
| `nmap [Host]` | `nmap www.networkwalks.com` | Scan a domain / hostname |
| `nmap [Range]` | `nmap 10.0.0.1-99` | Scan a range of IP addresses |
| `nmap [Multiple]` | `nmap 10.0.0.1,10.0.0.2` | Scan multiple distinct IPs |
| `nmap [Subnet]` | `nmap 10.0.0.0/24` | Scan an entire CIDR subnet |
| `nmap -iL [File]` | `nmap -iL LIST1.txt` | Scan targets from a text file |
| `nmap --exclude` | `nmap 10.0.0.0/24 --exclude 10.0.0.1` | Exclude specific targets from scan |

#### 2. Target Scan Options
| Switch | Example | Description |
|---|---|---|
| `-sS` | `nmap 10.0.0.1 -sS` | **SYN Scan** (TCP Half-Open / Stealth Scan, default with root) |
| `-sT` | `nmap 10.0.0.1 -sT` | **TCP Connect Scan** (Full 3-way handshake, no root needed) |
| `-sA` | `nmap 10.0.0.1 -sA` | **ACK Scan** (Maps firewall rulesets and filtered ports) |
| `-sF` | `nmap 10.0.0.1 -sF` | **FIN Scan** (Sends FIN packet to elicit RST from closed ports) |
| `-sU` | `nmap 10.0.0.1 -sU` | **UDP Scan** (DNS, DHCP, SNMP, NTP service discovery) |
| `-sX` | `nmap 10.0.0.1 -sX` | **Xmas Scan** (Sets FIN, URG, and PUSH flags) |
| `-sL` | `nmap 10.0.0.1 -sL` | **List Scan** (Lists targets without sending packets to hosts) |
| `-sP` / `-sn` | `nmap -sn 10.0.0.0/24` | **Ping Scan** (Host discovery only, no port scan) |
| `--traceroute` | `nmap --traceroute 10.0.0.1` | Trace network hop path to target host |
| `-A` | `nmap 10.0.0.1 -A` | **Aggressive Scan** (OS detection, version detection, scripts, traceroute) |
| `-6` | `nmap -6 [IPv6-Address]` | IPv6 network scan |
| `-F` | `nmap 10.0.0.1 -F` | **Fast Scan** (Scans the top 100 most common ports) |

#### 3. Selection of Ports to Scan
| Switch | Example | Description |
|---|---|---|
| `-p [port]` | `nmap 10.0.0.1 -p 21` | Scan a single port (FTP) |
| `-p [p1,p2]` | `nmap 10.0.0.1 -p 21,22` | Scan specific individual ports |
| `-p [p1-p2]` | `nmap 10.0.0.1 -p 1-1000` | Scan a custom port range |
| `-p [service]` | `nmap 10.0.0.1 -p ssh,http` | Scan ports by service name |
| `-p-` | `nmap 10.0.0.1 -p-` | **Scan all 65,535 TCP ports** |

#### 4. Target Version & OS Fingerprinting
| Switch | Example | Description |
|---|---|---|
| `-O` | `nmap 10.0.0.1 -O` | **Remote Operating System Detection** |
| `-sV` | `nmap 10.0.0.1 -sV` | **Service Version Detection** (Queries open ports for version banners) |
| `--version-intensity` | `nmap -sV --version-intensity 9 10.0.0.1` | Set probing intensity level (0 to 9) |

#### 5. Scan Speed & Timing Options
| Switch | Speed Profile | Description |
|---|---|---|
| `-T0` | Paranoid | Extremely slow, serial probing for IDS/IPS evasion |
| `-T1` | Sneaky | Slow scan for stealthy network reconnaissance |
| `-T2` | Polite | Slows scan down to consume less bandwidth on target |
| `-T3` | Normal | Default Nmap timing template |
| `-T4` | Aggressive | Faster speed, recommended for reliable lab networks |
| `-T5` | Insane | Maximum speed, less accurate, easily detectable |

#### 6. Miscellaneous & Output Options
| Switch | Example | Description |
|---|---|---|
| `-oN [file]` | `nmap -oN output.txt 10.0.0.1` | Save output in human-readable normal format |
| `-oX [file]` | `nmap -oX output.xml 10.0.0.1` | Save scan output in XML format |
| `-oA [basename]`| `nmap -oA lab_scan 10.0.0.1` | Save in all three major formats (Nmap, XML, Grepable) |
| `-S [IP]` | `nmap -S 10.0.0.99 10.0.0.1` | Spoof source IP address |
| `-e [interface]`| `nmap -e eth0 10.0.0.1` | Specify network interface |
| `--spoof-mac` | `nmap --spoof-mac 00:11:22:33:44:55 10.0.0.1` | Spoof MAC address |
| `--script` | `nmap --script vuln 10.0.0.1` | Execute Nmap Scripting Engine (NSE) scripts |

---

### 🖥️ Local Network Scanning Steps with Zenmap

1. **Identify Local Network Configuration:**
   ```cmd
   ipconfig /all
   ```
2. **Execute Ping Discovery Sweep in Zenmap:**
   - Command: `nmap -sn 10.0.0.0/24` (or `10.0.2.0/24` in lab VM)
   - Live Hosts Discovered: `10.0.0.1`, `10.0.0.4`, `10.0.0.5`, `10.0.0.19`.
3. **Generate & Save Topology Diagram:**
   - Navigated to the **Topology** tab in Zenmap.
   - Enabled interactive Legend and exported the graphical network map in PDF/graphic format.

---

## 📄 W2-PM-FINAL: Penetration Testing Report

The formal penetration testing deliverable has been compiled and saved:

👉 **[Read the Full Penetration Testing Report](../Reports/Week2_Pentest_Report.md)**

### Report Highlights:
- **Liability Disclaimer:** Clear ethical boundaries and authorized testing statement.
- **Structured Findings Matrix:** 6 categorized findings with risk ratings (Medium / Low).
- **Remediation Roadmap:** Actionable steps covering banner suppression, REST API protection, WAF tuning, and VLAN segmentation.

---

## 💡 What I Learned

1. **The Attacker Mindset in Reconnaissance:** High-value data (CMS versions, WAF presence, REST endpoints) can be uncovered purely through passive and low-profile queries.
2. **Precision Port Scanning:** Understanding when to use stealth SYN scans (`-sS`), UDP scans (`-sU`), and timing profiles (`-T4`) depending on the environment.
3. **Professional Reporting Standards:** How to translate technical command outputs into executive-level risk assessments and actionable remediation guidance.

---

## ⚖️ Ethical Statement

> All activities were performed strictly within **authorized educational boundaries** (`networkwalks.com` with permission, and personal private subnet `10.0.0.0/24` / `10.0.2.0/24`). Unauthorized reconnaissance or scanning against third-party systems is strictly prohibited.

---

> 📂 [Back to Main README](../README.md)
