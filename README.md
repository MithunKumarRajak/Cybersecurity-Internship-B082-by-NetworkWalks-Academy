# ðŸ›¡ï¸ Cybersecurity & Ethical Hacking â€” Internship B082

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Mithun_Kumar_Rajak-0077b5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/mithun-kumar-rajak/)
[![Program](https://img.shields.io/badge/NetworkWalks-B082_Internship-0a66c2?style=for-the-badge&logo=shield&logoColor=white)](https://www.networkwalks.com)
[![Week](https://img.shields.io/badge/Current-Week_3-0a66c2?style=for-the-badge)](Week-3-Cracking-Attacking/)
[![Status](https://img.shields.io/badge/Status-Week_3_Completed-28a745?style=for-the-badge)](Week-3-Cracking-Attacking/)

> A 4-week remote cybersecurity internship by **[NetworkWalks Academy](https://www.networkwalks.com)**, guided by CCIE-certified industry experts. This repository documents my hands-on work â€” from lab setup to full penetration testing.

---

## ðŸ“Œ Program at a Glance

| Field | Detail |
|---|---|
| **Intern** | [Mithun Kumar Rajak](https://www.linkedin.com/in/mithun-kumar-rajak/) |
| **Batch** | B082 â€” August 2026 |
| **Duration** | 4 Weeks |
| **Mode** | 100% Remote + Weekly LIVE Zoom Sessions |
| **Instructor** | Waqas Karim (CCIE) |
| **Focus** | Penetration Testing, VAPT, Network Security, SOC Analysis |

---

## ðŸ“‚ Repository Structure

```
.
â”œâ”€â”€ README.md                      <- Root repository overview & progress tracker
â”œâ”€â”€ Reports/
â”‚   â”œâ”€â”€ README.md                                      <- Report index & templates
â”‚   â”œâ”€â”€ Week1_Lab_Setup_Report.pdf                     <- Submitted Week 1 Lab Setup Report (PDF)
â”‚   â”œâ”€â”€ Week2_Footprinting_Reconnaissance_Report.docx <- Submitted Week 2 Footprinting Report (DOCX)
â”‚   â”œâ”€â”€ Week2_Zenmap_Report.docx                       <- Submitted Week 2 Zenmap Scanning Report (DOCX)
â”‚   â””â”€â”€ Week2_Pentest_Report.md                        <- Week 2 Pentest Report (Markdown)
â”œâ”€â”€ Resources/
â”‚   â””â”€â”€ README.md                                      <- References, downloads & cheat sheets
â”œâ”€â”€ Week-1-Lab-Setup/
â”‚   â””â”€â”€ README.md                                      <- Week 1: Kali Linux 2026.2 + VirtualBox setup
â””â”€â”€ Week-2-Footprinting-Scanning/
    â””â”€â”€ README.md                                      <- Week 2: Reconnaissance, scanning & VAPT
```

> *Note: Week 4 modules will be added upon completion.*

---

## ðŸ“† Progress Tracker

| Week | Project | Track | Status | Report / Deliverable |
|:---:|---|:---:|:---:|---|
| **1** | [Lab Setup â€” Kali Linux 2026.2 + VirtualBox](Week-1-Lab-Setup/) | ðŸ”§ Essentials | âœ… Completed | [ðŸ“„ Week 1 PDF Report](Reports/Week1_Lab_Setup_Report.pdf) |
| **2** | [Footprinting, Scanning & Report Writing](Week-2-Footprinting-Scanning/) | ðŸ”´ Red Team | âœ… Completed | [ðŸ“„ Week 2 Pentest Report](Reports/Week2_Pentest_Report.md) |
| **3** | [Cracking & Attacking — JTR & NW Tools](Week-3-Cracking-Attacking/) | 🔴 Red Team | ✅ Completed | [📥 JTR Report](Reports/Week3_Password_Cracking_JTR_Report.docx) \| [📥 NW Tools Report](Reports/Week3_Password_Cracking_NetworkWalks_Tools_Report.docx) |
| **4** | [Full Pentest + Wireshark SOC Analysis](Week-4-Full-Pentest-Project/) | ðŸ”´ðŸ”µ Red + Blue | â¬œ Upcoming | â¬œ Upcoming |

---

## ðŸ–¥ï¸ Lab Architecture & Network Topology

```
+-----------------------------------------------------------------------+
|                           HOST: Windows 11                            |
|                    Oracle VirtualBox Hypervisor                       |
|                                                                       |
|   +---------------------------------------------------------------+   |
|   |         Isolated Virtual Subnet: NatNetwork (10.0.2.0/24)     |   |
|   |                     DHCP: Enabled | IPv6: Off                 |   |
|   |                                                               |   |
|   |   +--------------------------+     +----------------------+   |   |
|   |   |   Kali Linux 2026.2      |     |  Target VM (Planned) |   |   |
|   |   |   Role: Attacker         |     |  Role: Victim        |   |   |
|   |   |   IP:   10.0.2.15 (eth0) | <-> |  IP:   10.0.2.x      |   |   |
|   |   |   RAM:  4096 MB | 3 vCPU |     |  OS:   Metasploitable|   |   |
|   |   |   Disk: 80.09 GB VDI     |     |        / Windows     |   |   |
|   |   |   Mode: Promisc AllowAll |     |                      |   |   |
|   |   +--------------------------+     +----------------------+   |   |
|   +---------------------------------------------------------------+   |
|                                  |                                    |
|                                  v (NAT Outbound Access)              |
|                    +---------------------------+                      |
|                    |      Internet / WAN       |                      |
|                    +---------------------------+                      |
+-----------------------------------------------------------------------+
```

### Lab Nodes & IP Addressing

| Node / Virtual Machine | Operating System | IP Address | Subnet | Role | Status |
|---|---|---|---|---|:---:|
| **Host Machine** | Windows 11 | Host Network | Host LAN | Hypervisor Host | Active |
| **Virtual Gateway** | VirtualBox NAT | `10.0.2.1` | `10.0.2.0/24` | Default Gateway | Active |
| **Kali Linux (Attacker)** | Kali 2026.2 (x64) | `10.0.2.15` | `10.0.2.0/24` | Primary Pentest Machine | âœ… Ready |
| **Metasploitable 2** | Linux (Vulnerable) | `10.0.2.x` | `10.0.2.0/24` | Red Team Target | âœ… Ready (Week 3) |
| **Windows Target** | Windows OS | `10.0.2.x` | `10.0.2.0/24` | Red Team Target | âœ… Ready (Week 3) |

---

## ðŸ› ï¸ Tools & Technologies

| Category | Tools | Applied In |
|---|---|---|
| **Pentesting OS** | Kali Linux 2026.2 | Week 1, 2, 3, 4 |
| **Hypervisor** | Oracle VirtualBox 7.x | Week 1, 2, 3, 4 |
| **Scanning & Recon** | Nmap, Zenmap, Nessus, Nikto | Week 2, 4 |
| **OSINT & Footprinting** | Maltego, theHarvester, GHDB (Google Dorks) | Week 2, 4 |
| **Exploitation Frameworks** | Metasploit Framework, Burp Suite | Week 3, 4 |
| **Password Attacks** | John The Ripper (JTR), Hydra, Hashcat | Week 3, 4 |
| **Packet & SOC Analysis** | Wireshark, tcpdump | Week 1, 4 |

---

## âš–ï¸ Disclaimer

> **All work in this repository is strictly for educational and authorized security testing purposes.**
> Testing is performed exclusively on **owned lab machines** within an isolated virtual environment (`10.0.2.0/24`).
> Unauthorized access to any system outside this lab is illegal and strictly against professional ethics.

---

## ðŸ”— Quick Links

| Resource | Link |
|---|---|
| **LinkedIn Profile** | [Mithun Kumar Rajak](https://www.linkedin.com/in/mithun-kumar-rajak/) |
| **NetworkWalks Website** | [networkwalks.com](https://www.networkwalks.com) |
| **Instructor LinkedIn** | [Waqas Karim CCIE](https://linkedin.com/in/waqaskarim/) |
| **NetworkWalks LinkedIn** | [Follow Company](https://linkedin.com/company/networkwalks/) |

---

<p align="center">
  <strong>NetworkWalks Academy</strong> Â· Batch B082 Â· August 2026<br>
  <em>Instructor: Waqas Karim â€” CCIE</em>
</p>



