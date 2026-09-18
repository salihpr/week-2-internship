<div align="center">

# 🔐 Cybersecurity Internship – Week 02

### OSINT Footprinting (Maltego) & Network Scanning (Zenmap)

![Program](https://img.shields.io/badge/program-Networkwalks%20B083-blue)
![Scope](https://img.shields.io/badge/scope-authorized%20only-important)
![OS](https://img.shields.io/badge/OS-Kali%20Linux-557C94?logo=kalilinux&logoColor=white)
![Tool](https://img.shields.io/badge/tool-Maltego-6C2EB9?logo=maltego&logoColor=white)
![Tool](https://img.shields.io/badge/tool-Nmap%20%2F%20Zenmap-0B7285)
![LinkedIn](https://img.shields.io/badge/LinkedIn-Muhammed%20Salih%20CV-0A66C2?logo=linkedin&logoColor=white)

A hands-on penetration testing practical combining **OSINT footprinting** with Maltego against a live authorized domain and **active network scanning** with Nmap/Zenmap on my own local network, performed on industry-standard Kali Linux tooling.

</div>

---

## 📌 Project Overview

| | |
|---|---|
| **Intern** | Muhammed Salih CV |
| **Program / Batch** | B083 – Networkwalks |
| **Report Date** | 18 September 2026 |
| **Targets** | 1. `networkwalks.com` (written permission secured) <br> 2. My own local LAN network (own IP addresses) |
| **Phases Covered** | Phase 1: Reconnaissance & Footprinting<br>Phase 2: Scanning & Network Discovery |

> ⚠️ **Authorization Notice:** All activities were performed only against systems I have explicit written permission to test, or on my own network/IP addresses, strictly for educational purposes. No exploitation, intrusion, or unauthorized access was performed at any stage.

---

## 🎯 Objectives

- 🕵️ Map the target website as an entity in Maltego and pivot outward using OSINT transforms
- 📧 Discover email addresses linked to the target domain via the Mirror transform
- 🖥️ Run all footprinting activity from a Kali Linux environment
- 🛰️ Identify live hosts on the local network using Zenmap (Nmap GUI)
- 🗺️ Visualize the discovered hosts as a network topology graph
- 🔎 Run an Nmap Intense Scan for host, port and OS discovery
- 📝 Document the risk arising from exposed email addresses and discoverable network hosts

---

## 🧰 Tools Used

| Tool | Phase | Purpose |
|---|---|---|
| 🖥️ Kali Linux | Footprinting & Scanning | Operating system used to run Maltego and the scanning tools |
| 🕵️ Maltego (Community Edition) | Footprinting | OSINT graphing tool — maps a domain to related infrastructure and email addresses |
| 🔁 Mirror Transform (Utilities) | Footprinting | Maltego transform used to pivot from a Website entity to linked email addresses |
| 📡 Nmap | Scanning | Core scan engine — host discovery, port scanning, OS fingerprinting |
| 🛰️ Zenmap (Nmap GUI) | Scanning | Graphical front-end for Nmap — scan configuration, output and topology view |

---

## 🧪 Methodology

### Part A — 🕵️ Footprinting with Maltego (`networkwalks.com`)

1. **Added a Website entity** for `https://networkwalks.com/` to a new Maltego graph on Kali Linux

   <img width="1024" alt="maltego-add-entity" src="https://raw.githubusercontent.com/salihpr/week-2-internship/main/screenshorts/Screenshot%202026-09-16%20080918.png" />

---

2. **Reviewed the entity details** in the Details panel to confirm the Website entity resolved correctly

   <img width="1024" alt="maltego-entity-details" src="https://raw.githubusercontent.com/salihpr/week-2-internship/main/screenshorts/Screenshot%202026-09-16%20081945.png" />

---

3. **Ran the "Email addresses found [Mirror]" transform** against the Website entity — 3 linked email entities were returned in just over a minute, using 0 of 200 available Unified Credits

   <img width="1024" alt="maltego-mirror-transform-results" src="https://raw.githubusercontent.com/salihpr/week-2-internship/main/screenshorts/Screenshot%202026-09-16%20082150.png" />

---

### Part B — 🛰️ Network Scanning with Zenmap (Own Local LAN)

1. **Ran an Intense Scan** (`nmap -T4 -A -v 10.0.0.2/24`) from Zenmap against my own subnet to discover live hosts, open ports and attempt OS detection

   <img width="1024" alt="zenmap-intense-scan-output" src="https://raw.githubusercontent.com/salihpr/week-2-internship/main/screenshorts/VirtualBox_kali%20linux_18_09_2026_06_12_56.png" />

---

2. **Reviewed the Topology tab**, which plotted `localhost` at the centre with the scanning host and the discovered live hosts around it

   <img width="1024" alt="zenmap-topology-view" src="https://raw.githubusercontent.com/salihpr/week-2-internship/main/screenshorts/VirtualBox_kali%20linux_18_09_2026_06_12_40.png" />

---

## 🔍 Key Findings

### 🕵️ Footprinting — Maltego (Email Exposure)

| Attribute | Value |
|---|---|
| Target Entity | `https://networkwalks.com/` (Website) |
| Transform Used | Email addresses found [Mirror] (Utilities set) |
| Emails Discovered | `available@akismet.com`, `info@atechacademy.com`, `info@networkwalks.com` |
| Entities Returned | 3 |
| Credits Consumed | 0 / 200 |
| Run Time | ≈ 1 min 4 s |

### 🛰️ Network Scanning — Zenmap (Own Local Network)

| Attribute | Value |
|---|---|
| Target Subnet | `10.0.0.2/24` |
| Scan Profile / Command | Intense scan — `nmap -T4 -A -v 10.0.0.2/24` |
| Live Hosts Found | `10.0.0.1`, `10.0.0.2`, `10.0.0.4` |
| Port State | All 1000 scanned TCP ports filtered (no-response) on `.2` and `.4` |
| OS Detection | Inconclusive — too many fingerprints matched |
| Scan Coverage | 256 IP addresses scanned in 265.37 seconds |

---

## ⚠️ Risk Analysis Summary

| Finding | Evidence | Risk Level |
|---|---|---|
| Email address exposure | Maltego Mirror transform identified 3 emails linked to `networkwalks.com` | 🟠 Medium |
| Multiple live hosts visible on local network | Zenmap intense scan identified 3 live hosts on `10.0.0.2/24` | 🟠 Medium |

> These are discovery-stage observations from the Maltego and Zenmap exercises only, not confirmed vulnerabilities. No exploitation or vulnerability validation was performed.

---

## ✅ Recommendations

1. **Limit publicly harvestable email addresses** — prefer role-based addresses (e.g. `info@`) over individual staff emails
2. **Monitor your own OSINT footprint** — periodically run Maltego-style transforms against your own domain
3. **Train staff on phishing awareness** — harvested emails are common phishing targets
4. **Maintain a network asset inventory** — verify every host a Zenmap/Nmap scan turns up
5. **Perform regular internal network scans** — catch unauthorized or rogue devices early
6. **Keep firewall/filtering rules consistent** — maintain the "no-response" filtering observed during scanning
7. **Perform security testing with authorization** — only scan systems and networks with explicit permission

---

## 📁 Repository Structure

```
├── Report/
│   └── Pentest_Report_Muhammed_Salih_CV.docx   # Full report — Maltego footprinting & Zenmap scanning
├── screenshorts/
│   ├── Screenshot 2026-09-16 080918.png        # Maltego — Website entity added to graph
│   ├── Screenshot 2026-09-16 081945.png        # Maltego — Website entity details
│   ├── Screenshot 2026-09-16 082150.png        # Maltego — Mirror transform results (emails)
│   ├── VirtualBox_kali linux_18_09_2026_06_12_56.png   # Zenmap — Intense scan output
│   └── VirtualBox_kali linux_18_09_2026_06_12_40.png   # Zenmap — Network topology view
└── README.md
```

🔗 **Full Report:** [Pentest_Report_Muhammed_Salih_CV.docx](https://github.com/salihpr/week-2-internship/blob/main/Report/Pentest_Report_Muhammed_Salih_CV.docx)

---

## 🧠 Key Takeaway

OSINT footprinting and active network scanning are complementary discovery techniques that form the foundation of every real-world security assessment. A single domain name fed into Maltego can reveal email addresses useful for social engineering, while a simple Zenmap scan of a local network can reveal live hosts even when their ports are filtered. Reducing unnecessary public exposure — combined with regular self-reconnaissance — directly shrinks an organization's attack surface.

---

## ⚖️ Disclaimer

This material is for education and authorized research purposes only. Unauthorized access to computer systems is illegal in most jurisdictions, even when no damage occurs. All activities documented here were performed only against systems I own, have explicit written permission to test, or on my own network/IP addresses.

---

<div align="center">

### 👤 Author

**Muhammed Salih CV**
Cybersecurity Intern — Batch B083

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?logo=linkedin&logoColor=white)](https://linkedin.com/in/muhammed-salih-cv-9a292433a)
[![GitHub](https://img.shields.io/badge/GitHub-salihpr-181717?logo=github&logoColor=white)](https://github.com/salihpr/week-2-internship)

LinkedIn: [https://linkedin.com/in/muhammed-salih-cv-9a292433a](https://linkedin.com/in/muhammed-salih-cv-9a292433a)

</div>
