# 🧠 Cybersecurity Homelab

![Status](https://img.shields.io/badge/project-active-brightgreen) ![Lab Type](https://img.shields.io/badge/type-home--lab-blue) ![License](https://img.shields.io/badge/license-MIT-lightgrey) ![Platform](https://img.shields.io/badge/platform-VirtualBox-orange) ![Focus](https://img.shields.io/badge/focus-Blue%20Team%20%2B%20OffSec-red)

Welcome to my **Cybersecurity Homelab** – a personal, hands-on project to build and simulate real-world network environments using open-source tools and virtual machines.

This lab is part of my career transition into cybersecurity, and serves as a portfolio project to demonstrate my practical knowledge in:

- Network segmentation and firewalling
- Active Directory (AD/DC) and domain infrastructure
- Proxy, content filtering and ACLs
- SIEM logging and threat visibility
- Offensive security and internal threat simulations

> 🎯 **Goal**: Create an enterprise-like lab from scratch, with focus on blue team strategies, threat detection, and infrastructure hardening.

---

## 🧱 Lab Overview

| Component         | Role                                                       |
| ----------------- | ---------------------------------------------------------- |
| `pfSense`         | Firewall, NAT, VLANs, DNS Forwarding, pfBlockerNG          |
| `Gondor-DC`       | Active Directory Domain Controller (lab.local)             |
| `Snape-Proxy`     | Replaced for pfBlockerNG no pfSense                     |
| `Oracle-SI`       | SIEM using Splunk Free, receiving logs from all components |
| `BlackMirror-Web` | Vulnerable webapp (DVWA, Juice Shop) in DMZ                |
| `Trinity-Pentest` | Offensive Kali machine: attacks, phishing, BloodHound      |
| `Neo-Client`      | User workstation (Windows 10), GPOs, domain logon          |
| `Borg-Victim`     | Metasploitable 2 – vulnerable target for exploits          |

---

## 📡 Network Design

Four segmented networks using VMware Host-Only adapters:

- `VMnet1 (LAN)` – 192.168.1.0/24
- `VMnet2 (DMZ)` – 192.168.10.0/24
- `VMnet3 (SERVERS)` – 192.168.20.0/24
- `VMnet9 (ADMIN)` – 192.168.99.0/24 (access from host)

*(to be added)*

---

## 🔧 Machines & Setup

### 🔐 Gondor-DC (192.168.20.10)
- OS: Debian 12
- Roles: Samba 4 (AD/DC, DNS, DHCP)
- Users & Groups: Created via CLI

### 🧠 Oracle-SI (192.168.20.30)
- OS: Ubuntu Server 22.04
- Splunk Free 9.x
- Receives logs from proxy, firewall, AD, etc.

### ☣️ BlackMirror-Web (192.168.10.120)
- OS: Ubuntu Server 22.04
- Tools: DVWA, OWASP Juice Shop
- Hosted in DMZ

### 🧨 Trinity-Pentest (IP via DHCP - LAN)
- OS: Kali Linux
- RAM: 3 GB | vCPU: 2 | Disk: 30 GB
- Network: VMnet1 (192.168.1.0/24)
- Tools: Phishing, LDAP enumeration, BloodHound, exploits

### 👩‍💼 Neo-Client (IP via DHCP - LAN)
- OS: Windows 10 Pro (Eval)
- RAM: 4 GB | vCPU: 2 | Disk: 40 GB
- Network: VMnet1 (192.168.1.0/24)
- Function: Domain logon, GPO behavior, normal user activity

### 🐑 Borg-Victim (IP via DHCP - LAN)
- OS: Metasploitable 2
- RAM: 768 MB | vCPU: 1 | Disk: 10 GB
- Network: VMnet1 (192.168.1.0/24)
- Function: Exploit target, vulnerable services, lateral movement testing

---

## 📁 Structure

```bash
/
├── docs/
│   ├── network-diagram.md
│   ├── ad-setup.md
│   ├── pfblockerng-config.md
│   ├── splunk-config.md
│   ├── kali-attacks.md
│   └── firewall-rules.md
├── configs/
│   ├── pfsense/
│   ├── samba/
│   └── splunk/
├── scripts/
│   ├── join-domain.sh
│   └── attack-scripts/
├── assets/
│   └── screenshots/
└── README.md
```

---

## 🧭 Roadmap

> A guided journey through enterprise-grade simulations, blue team strategy, and offensive testing.

### 🔹 Phase 1 – Core Infrastructure
- [x] Install and configure pfSense with 4 isolated networks (LAN, DMZ, SERVERS, ADMIN)
- [x] Enable pfBlockerNG for content and reputation control
- [x] Deploy Samba AD/DC (Gondor-DC) with DNS and DHCP
- [x] Join Neo-Client to the domain with basic Group Policy Objects (GPOs)

### 🔹 Phase 2 – Monitoring and Logging
- [x] Install and configure Splunk Free (Oracle-SI)
- [x] Ingest logs from pfSense, Samba, Kali, and Neo-Client
- [ ] Create dashboards for visibility and event correlation
- [ ] Generate custom alerts based on suspicious activity

### 🔹 Phase 3 – Attack Simulations
- [ ] Create and execute scenarios using Kali (Trinity-Pentest)
  - Phishing with SEToolkit
  - LDAP/AD enumeration with enum4linux and BloodHound
  - Exploitation against Borg-Victim
- [ ] Analyze logs and alerts generated in Splunk

### 🔹 Phase 4 – Expansions
- [ ] Integrate IDS (Suricata) for traffic analysis
- [ ] Create a GPO to map network drives with specific permissions
- [ ] Implement a “trash” folder in Samba for deletion auditing
- [ ] Simulate lateral movement and privilege escalation
- [ ] Automate startup and snapshots with bash scripts

---

## 📬 Contact

If you're a recruiter, security engineer, or curious mind – feel free to reach out. I'm open to feedback, collaboration or job opportunities.

**Leandro Uehara**

[LinkedIn](https://www.linkedin.com/in/leandro-stolfo-uehara-800499163) • [GitHub](https://github.com/leandrosu) 

`leadrosu@gmail.com`

---

> 🚀 *This project reflects my journey from Java developer to chef to aspiring cybersecurity analyst — built with hard work, persistence, and a hunger to grow.*
