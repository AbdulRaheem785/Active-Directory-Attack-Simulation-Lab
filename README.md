<div align="justify">

# Active Directory Attack Simulation Lab

<p align="center">
  <img src="banner.png" alt="Active Directory Attack Simulation Lab" width="100%">
</p>

## 📌 Overview
This repository documents the deployment and offensive security assessment of an enterprise-grade Active Directory (AD) lab. The project objective was to build a realistic corporate environment, introduce common structural misconfigurations, and execute an end-to-end attack lifecycle from unauthenticated reconnaissance to full Domain Admin compromise.
</div>

---

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
  <img src="watermarked_img_15900776283458645334.png" alt="Active Directory Attack Flow" width="100%">
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

**Author:** AbdulRaheem | **Status:** Completed | **Environment:** Lab Simulation  
</div>
