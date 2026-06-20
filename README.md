<p align="center">
<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=24&pause=1000&color=00FF00&center=true&vCenter=true&width=700&lines=Active+Directory+Attack+Simulation+Lab;Domain+Enumeration+%7C+SMB+%7C+LDAP;BloodHound+Attack+Path+Analysis;Privilege+Escalation+to+Domain+Admin;Cybersecurity+Portfolio+Project" />
</p>
<p align="center">

![Windows Server](https://img.shields.io/badge/Windows_Server-2022-0078D6?style=for-the-badge&logo=windows)
![Kali Linux](https://img.shields.io/badge/Kali-Linux-557C94?style=for-the-badge&logo=kalilinux)
![Active Directory](https://img.shields.io/badge/Active_Directory-Lab-0A66C2?style=for-the-badge)
![Nmap](https://img.shields.io/badge/Nmap-Network_Enumeration-4682B4?style=for-the-badge)
![NetExec](https://img.shields.io/badge/NetExec-SMB_&_LDAP-darkgreen?style=for-the-badge)
![BloodHound](https://img.shields.io/badge/BloodHound-Attack_Path_Analysis-red?style=for-the-badge)
![Privilege Escalation](https://img.shields.io/badge/Privilege_Escalation-Domain_Admin-success?style=for-the-badge)
![MITRE ATT&CK](https://img.shields.io/badge/MITRE-ATT%26CK-red?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)

</p>
<div align="justify">

<p align="center">
  <img src="banner.png" alt="Active Directory Attack Simulation Lab" width="100%">
</p>

## 📌 Overview
This repository documents the deployment and offensive security assessment of an enterprise-grade Active Directory (AD) lab. The project objective was to build a realistic corporate environment, introduce common structural misconfigurations, and execute an end-to-end attack lifecycle from unauthenticated reconnaissance to full Domain Admin compromise.
</div>

---
<p align="center">
<img src="https://media.giphy.com/media/f3iwJFOVOwuy7K6FFw/giphy.gif" width="500">
</p>
<div align="justify">

## 🛠️ Lab Specifications & Environment
The deployment architecture utilizes virtualized isolation to replicate an enterprise environment, mapping a complete attack path from unauthenticated access up to Tier 0 assets.

<p align="center">
  <img src="Topology.png" alt="Active Directory Lab Topology & Scope" width="100%">
</p>

* **Target Domain Controller:** Windows Server 2022 (`corp.local`)
* **Attacker Platform:** Kali Linux VM (Isolated Subnet)
* **Scope Constraints:** Network Mapping, AD Structure Misconfigurations, Credential Testing, and Graph Path Analysis.
</div>

---

<div align="justify">

### Weaponry & Utilities Used
The following key offensive testing utilities were leveraged across the assessment to discover, exploit, and track privilege escalation paths.

<p align="center">
  <img src="Toolset_Matrix.png" alt="Attack Toolset Matrix" width="100%">
</p>

* **Recon & Discovery:** `Nmap` for network enumeration and `Kerbrute` for user enumeration.
* **AD Exploitation:** `NetExec`.
* **Path Analysis & Post-Ex:** `BloodHound` for relationship mapping and `CrackMapExec` for post-exploitation validation.
</div>

---

<div align="justify">

## 🛑 Attack Lifecycle & Findings
The assessment followed a structured, 6-stage offensive security timeline to progress from network footprinting to domain-wide takeover.

<p align="center">
  <img src="lifecycle.png" alt="Active Directory Attack Flow" width="100%">
</p>

* **1. Reconnaissance (Nmap):** Identified open target ports and core infrastructure services (`88/Kerberos`, `389/LDAP`, `445/SMB`).
* **2. SMB Enumeration:** Discovered active null session permissions to harvest baseline password policies and system shares anonymously.
* **3. LDAP Enumeration:** Queried directory services unauthenticated to extract structural user accounts and group schemas.
* **4. Credential Attacks:** Executed horizontal password spraying to isolate weak accounts across the user directory.
* **5 & 6. Path Analysis & Takeover:** Ingested domain metadata into BloodHound to map hidden permission chains, allowing direct escalation to **Domain Admin**.
</div>

---

<div align="justify">

## 🛡️ Defensible Remediation
1. **Disable SMB Null Sessions:** Enforce explicit restrictions on anonymous network logons via Group Policy Objects (GPO).
2. **Mandate LDAP Signing:** Turn on strict LDAP signing constraints and Channel Binding requirements to neutralize cleartext queries.
3. **Deploy Fine-Grained Password Policies (FGPP):** Apply unique complexity rules and aggressive lockout settings to mitigate automated dictionary spraying.
4. **Audit AD ACLs:** Routinely analyze directory configurations using BloodHound to spot and eliminate unintended privilege delegation paths.
</div>

---

<div align="justify">

**Author:** AbdulRaheem
