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

## 🛠️ Lab Specifications & Utilities
The architecture utilizes virtualized isolation to safely replicate a corporate subnet layout.

<p align="center">
  <img src="Screenshot 2026-06-19 205703.png" alt="Lab Metadata Specifications" width="100%">
</p>

* **Target:** Windows Server 2022 (`corp.local`)
* **Attacker Platform:** Kali Linux
* **Key Frameworks:** Reconnaissance, Credential Testing, Graph-Theory Path Analysis.

<p align="center">
  <img src="watermarked_img_4266735515220668041.png" alt="Attack Toolset Matrix" width="100%">
</p>

* **Recon & Mapping:** `Nmap` for deep port probing and service verification.
* **AD Exploitation:** `NetExec`, `SMBClient`, and `Impacket` for protocol interaction.
* **Path Analysis & Post-Ex:** `BloodHound` (Neo4j backend) and `CrackMapExec`.
</div>

---

<div align="justify">

## 🛑 Attack Lifecycle & Findings
The simulation followed a structured pipeline to systematically elevate privileges.

<p align="center">
  <img src="Topology.png" alt="Refined Active Directory Attack Flow" width="100%">
</p>

* **1. Reconnaissance:** Discovered exposed critical services (`88/Kerberos`, `389/LDAP`, `445/SMB`).
* **2. SMB Null Sessions:** Exploited anonymous IPC$ connections to harvest password policies and domain metadata.
* **3. LDAP Enumeration:** Dumped complete AD user tables and group mappings unauthenticated.
* **4. Credential Attacks:** Executed horizontal password spraying to isolate weak, low-entropy accounts.
* **5 & 6. Path Analysis & Takeover:** Ingested domain data into BloodHound to uncover transitive permission chains (e.g., identity misconfigurations), granting direct escalation to **Domain Admin**.
</div>

---

<div align="justify">

## 🛡️ Remediation Strategies
1. **Disable SMB Null Sessions:** Restrict anonymous network logons via Group Policy Objects (GPO).
2. **Mandate LDAP Signing:** Enforce LDAP signing and Channel Binding to terminate cleartext queries.
3. **Deploy Fine-Grained Password Policies (FGPP):** Enforce strict complexity requirements and lockout thresholds to mitigate password spraying.
4. **Audit AD ACLs:** Perform regular defensive graph analysis with BloodHound to eliminate accidental or high-risk privilege delegations.
</div>

---

<div align="justify">

**Author:** AbdulRaheem | **Status:** Completed | **Environment:** Lab Simulation  
</div>
