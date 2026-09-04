# 🛡️ Cybersecurity & Ethical Hacking — Internship B082

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Mithun_Kumar_Rajak-0077b5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/mithun-kumar-rajak/)
[![Program](https://img.shields.io/badge/NetworkWalks-B082_Internship-0a66c2?style=for-the-badge&logo=shield&logoColor=white)](https://www.networkwalks.com)
[![Week](https://img.shields.io/badge/Current-Week_4_(Capstone)-0a66c2?style=for-the-badge)](Week-4-Full-Pentest-Project/)
[![Status](https://img.shields.io/badge/Status-Week_4_In_Progress-f39c12?style=for-the-badge)](Week-4-Full-Pentest-Project/)

> A 4-week remote cybersecurity internship by **[NetworkWalks Academy](https://www.networkwalks.com)**, guided by CCIE-certified industry experts. This repository documents my hands-on work — from initial lab setup to full black-box penetration testing of enterprise and healthcare web targets.

---

## 📌 Program at a Glance

| Field | Detail |
|---|---|
| **Intern** | [Mithun Kumar Rajak](https://www.linkedin.com/in/mithun-kumar-rajak/) |
| **Batch** | B082 — August 2026 |
| **Duration** | 4 Weeks |
| **Mode** | 100% Remote + Weekly LIVE Zoom Sessions |
| **Instructor** | Waqas Karim (CCIE) |
| **Focus** | Penetration Testing, VAPT, Network Security, SOC Analysis, Healthcare ePHI Security |

---

## 📂 Repository Structure

```
.
├── README.md                                          <- Root repository overview & progress tracker
├── Reports/
│   ├── README.md                                      <- Report index & submission registry
│   ├── Week1_Lab_Setup_Report.pdf                     <- Submitted Week 1 Lab Setup Report (PDF)
│   ├── Week2_Footprinting_Reconnaissance_Report.docx <- Submitted Week 2 Footprinting Report (DOCX)
│   ├── Week2_Zenmap_Report.docx                       <- Submitted Week 2 Zenmap Scanning Report (DOCX)
│   ├── Week2_Pentest_Report.md                        <- Week 2 Pentest Report (Markdown)
│   ├── Week3_Password_Cracking_JTR_Report.docx        <- Submitted Week 3 JTR Cracking Report (DOCX)
│   └── Week3_Password_Cracking_NetworkWalks_Tools_Report.docx <- Submitted Week 3 NW Tools Report (DOCX)
├── Resources/
│   └── README.md                                      <- References, downloads & cheat sheets
├── Week-1-Lab-Setup/
│   └── README.md                                      <- Week 1: Kali Linux 2026.2 + VirtualBox setup
├── Week-2-Footprinting-Scanning/
│   ├── README.md                                      <- Week 2: Reconnaissance, scanning & VAPT
│   └── screenshots/                                   <- 8 Evidentiary terminal captures
├── Week-3-Cracking-Attacking/
│   ├── README.md                                      <- Week 3: Password cracking with JTR & NW Tools
│   └── screenshots/                                   <- 35 Evidentiary cracking captures
└── Week-4-Full-Pentest-Project/
    └── README.md                                      <- Week 4: Capstone Pentest (Mediroza General Hospital)
```

---

## 📆 Progress Tracker

| Week | Project | Track | Status | Report / Deliverable |
|:---:|---|:---:|:---:|---|
| **1** | [Lab Setup — Kali Linux 2026.2 + VirtualBox](Week-1-Lab-Setup/) | 🔧 Essentials | ✅ Completed | [📄 Week 1 PDF Report](Reports/Week1_Lab_Setup_Report.pdf) |
| **2** | [Footprinting, Scanning & Report Writing](Week-2-Footprinting-Scanning/) | 🔴 Red Team | ✅ Completed | [📄 Week 2 Pentest Report](Reports/Week2_Pentest_Report.md) |
| **3** | [Cracking & Attacking — JTR & NW Tools](Week-3-Cracking-Attacking/) | 🔴 Red Team | ✅ Completed | [📥 JTR Report](Reports/Week3_Password_Cracking_JTR_Report.docx) \| [📥 NW Tools Report](Reports/Week3_Password_Cracking_NetworkWalks_Tools_Report.docx) |
| **4** | [Capstone Pentest — Mediroza General Hospital](Week-4-Full-Pentest-Project/) | 🔴🔵 Red + Blue | 🔄 In Progress | [🎯 Week 4 Capstone Project](Week-4-Full-Pentest-Project/) \| [Reports](Reports/) |

---

## 🖥️ Lab Architecture & Network Topology

```
+---------------------------------------------------------------------------------------+
|                           HOST: Windows 11 Hypervisor Host                            |
|                                                                                       |
|   +---------------------------------------------------------------+                   |
|   |         Isolated Virtual Subnet: NatNetwork (10.0.2.0/24)     |                   |
|   |                     DHCP: Enabled | IPv6: Off                 |                   |
|   |                                                               |                   |
|   |   +--------------------------+     +----------------------+   |                   |
|   |   |   Kali Linux 2026.2      |     |  Metasploitable 2    |   |                   |
|   |   |   Role: Attacker         |     |  Role: Lab Target    |   |                   |
|   |   |   IP:   10.0.2.15 (eth0) | <-> |  IP:   10.0.2.x      |   |                   |
|   |   |   RAM:  4096 MB | 3 vCPU |     |  OS:   Linux VAPT    |   |                   |
|   |   |   Disk: 80.09 GB VDI     |     +----------------------+   |                   |
|   |   |   Mode: Promisc AllowAll |                                |                   |
|   |   +--------------------------+                                |                   |
|   +---------------------------------------------------------------+                   |
|                                  |                                                    |
|                                  v (Authorized External Testing)                      |
|                    +------------------------------------------+                       |
|                    |     AUTHORIZED CLIENT TARGET SYSTEM      |                       |
|                    |        Mediroza General Hospital         |                       |
|                    |     https://medirozahospital.com         |                       |
|                    |    (Black-Box Pentest — 3 Days)          |                       |
|                    +------------------------------------------+                       |
+---------------------------------------------------------------------------------------+
```

### Lab Nodes & Target Systems

| Node / System | Type / OS | Network Location | Role / Target | Status |
|---|---|---|---|:---:|
| **Host Machine** | Windows 11 | Host Network | Hypervisor Host | Active |
| **Virtual Gateway** | VirtualBox NAT | `10.0.2.1` (`10.0.2.0/24`) | Default Gateway | Active |
| **Kali Linux (Attacker)** | Kali 2026.2 (x64) | `10.0.2.15` (`10.0.2.0/24`) | Primary Pentest Machine | ✅ Ready |
| **Metasploitable 2** | Linux (Vulnerable) | `10.0.2.x` (`10.0.2.0/24`) | Local Subnet Target | ✅ Ready |
| **Windows Target** | Windows OS | `10.0.2.x` (`10.0.2.0/24`) | Local Subnet Target | ✅ Ready |
| **Mediroza General Hospital** | Healthcare Web App | `https://medirozahospital.com` | **Capstone Black-Box Target (Week 4)** | 🎯 Active Scope |

---

## 🏥 Week 4 Capstone: Mediroza General Hospital Pentest

| Detail | Specification |
|---|---|
| **Client** | **Mediroza General Hospital** |
| **Project Type** | Full Black-Box Penetration Testing & Vulnerability Assessment |
| **Target URL** | `https://medirozahospital.com` |
| **Scope & Rules** | Testing strictly limited to target domain. No DoS. No social engineering. Written authorization provided. |
| **Timeline** | **3 Days** (Independent work under confidentiality policy) |
| **Milestone 1 (M1)** | **Initial Access:** Attack the website and retrieve 3 confidential patient PDF lab reports. |
| **Milestone 2 (M2)** | **Data Extraction:** Crack the encryption on all 3 retrieved PDF files using `pdf2john` & JTR/Hashcat. |
| **Milestone 3 (M3)** | **Attack (Cracking):** Discover hospital staff salary records and shareholder registry details. |
| **Milestone 4 (M4)** | **Pentest Report:** Author a formal, client-ready Penetration Testing & Remediation Report. |

---

## 🛠️ Tools & Technologies

| Category | Tools | Applied In |
|---|---|---|
| **Pentesting OS** | Kali Linux 2026.2 | Week 1, 2, 3, 4 |
| **Hypervisor** | Oracle VirtualBox 7.x | Week 1, 2, 3, 4 |
| **Scanning & Recon** | Nmap, Zenmap, Nikto, wafw00f, whatweb, dnsrecon | Week 2, 4 |
| **OSINT & Footprinting** | WHOIS, nslookup, theHarvester, GHDB (Google Dorks) | Week 2, 4 |
| **Exploitation & Web** | Burp Suite, cURL, Metasploit Framework | Week 3, 4 |
| **Password Attacks** | John The Ripper (JTR), pdf2john, Hashcat, Hydra, hashid | Week 3, 4 |
| **Packet & SOC Analysis** | Wireshark, tcpdump, Snort/Suricata rules | Week 1, 4 |

---

## ⚖️ Rules of Engagement & Ethical Statement

> **CONFIDENTIAL — AUTHORISED PERSONNEL ONLY**  
> All security testing documented in this repository is conducted in a strictly controlled environment for educational and professional validation purposes.  
> 
> * **Written Authorization:** Explicit written permission was granted by **Mediroza General Hospital** and **NetworkWalks Academy**.
> * **Target Boundaries:** Testing is strictly limited to authorized domains and private subnets (`10.0.2.0/24`).
> * **Strict Prohibitions:** No Denial of Service (DoS), no social engineering against personnel or patients, and no disruption to hospital healthcare operations.
> * Unauthorized testing against any infrastructure without prior written authorization is illegal.

---

## 🔗 Quick Links

| Resource | Link |
|---|---|
| **LinkedIn Profile** | [Mithun Kumar Rajak](https://www.linkedin.com/in/mithun-kumar-rajak/) |
| **NetworkWalks Website** | [networkwalks.com](https://www.networkwalks.com) |
| **Instructor LinkedIn** | [Waqas Karim CCIE](https://linkedin.com/in/waqaskarim/) |
| **NetworkWalks LinkedIn** | [Follow Company](https://linkedin.com/company/networkwalks/) |

---

<p align="center">
  <strong>NetworkWalks Academy</strong> · Batch B082 · August 2026<br>
  <em>Instructor: Waqas Karim — CCIE</em>
</p>
