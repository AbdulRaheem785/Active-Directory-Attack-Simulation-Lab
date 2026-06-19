<div align="justify">

# Active Directory Attack Simulation Lab

<p align="center">
  <img src="banner.png" alt="Active Directory Attack Simulation Lab" width="100%">
</p>

## 📌 Overview
Built and analyzed an enterprise-grade Active Directory environment to simulate real-world corporate attack paths. The core purpose of this project was to construct an active playground mirroring modern corporate networks, intentionally introduce common default misconfigurations, and systematically execute an end-to-end cyber attack lifecycle—ranging from unauthenticated network reconnaissance to full Domain Admin takeover.
</div>

---

<div align="justify">

## 🛠️ Lab Specifications & Environment
The deployment mimics an isolated corporate infrastructure segment utilizing localized virtualization to safeguard offensive testing procedures.

<p align="center">
  <img src="Screenshot 2026-06-19 205703.png" alt="Lab Metadata" width="100%">
</p>

* **Target Domain Controller:** Windows Server 2022 (`corp.local`)
* **Attacker Platform:** Kali Linux
* **License:** MIT License
* **Core Domains:** Network Mapping, Active Directory Structure Misconfigurations, Credential Testing, Graph-Based Transitive Attack Path Analysis.
</div>

---

<div align="justify">

### Weaponry & Defensive Utilities Used
The following industry-standard penetration testing tools were leveraged across the simulation lifecycle to discover, map, and exploit flaws.

<p align="center">
  <img src="Screenshot 2026-06-19 205725.png" alt="Tools Used" width="100%">
</p>

* **Nmap:** Deployed for network discovery and target service fingerprinting.
* **NetExec / CrackMapExec:** Multi-protocol assessment tool used to automate massive SMB/LDAP enumeration and post-exploitation workflows.
* **BloodHound:** Graph-theory-based Active Directory attack path mapping powered by a Neo4j backend database.
* **Impacket Suite:** Python classes for working with network protocols, allowing targeted interaction with SMB, Kerberos, and RPC services.
* **SMBClient:** Utilized for rapid manual share interaction and unauthenticated null-session identification tasks.
* **Kerbrute:** Employed for rapid, stealthy Kerberos pre-authentication user enumeration without triggering typical defensive alerts.
</div>

---

<div align="justify">

## 🛑 Attack Flow Lifecycle
The assessment followed a structured, highly systematic offensive security methodology to progress through the network architecture.

<p align="center">
  <img src="Screenshot 2026-06-19 205812.png" alt="Attack Flow" width="100%">
</p>

1. **Reconnaissance (Nmap):** Formulated an explicit footprint map by locating exposed services such as LDAP, SMB, Kerberos, and RPC.
2. **SMB Enumeration:** Discovered and exploited null session vulnerabilities to pull baseline domain details, password policies, and available shares.
3. **LDAP Enumeration:** Queried the Active Directory engine anonymously or via low-level credentials to dump structural user accounts, security groups, and object relationships.
4. **Credential Attacks:** Conducted precision password spraying and automated user validation to locate systemic credential vulnerabilities across the target list.
5. **BloodHound Analysis:** Ingested the collected directory data into an offline database instance to isolate structural permission flaws.
6. **Privilege Escalation:** Traced and executed explicit logical links to safely step up permissions from a zero-privilege account directly to full Domain Admin control.
</div>

---

<div align="justify">

## 🔍 Key Findings & Vulnerability Assessment
* **Exposed Directory Services:** Publicly accessible domain ports allowed unauthenticated threat entities to interact directly with infrastructure components (`389/LDAP`, `445/SMB`, `88/Kerberos`).
* **SMB Null Sessions Enabled:** Legacy configurations permitted completely unauthenticated null connections, exposing core directory layout elements to initial threat vectors.
* **Weak Password Policy Enforcement:** Missing lock-out rules or dynamic thresholds allowed password spraying toolsets to compromise target profiles without setting off security barriers.
* **Hidden Transitive Privilege Paths:** BloodHound mappings brought to light structural directory access control flaws (e.g., `GenericAll`, `WriteDacl`) that allowed standard user tokens to alter or take ownership of high-value administrative roles.
</div>

---

<div align="justify">

## 📸 Technical Evidence & Execution
The images below serve as forensic and operational evidence confirming execution parameters across different testing phases.

<p align="center">
  <img src="Screenshot 2026-06-19 205751.png" alt="Evidence Screenshots" width="100%">
</p>

* **Nmap Enumeration (Phase 1):** Validated active listening configurations across the target IP layout, pinpointing the signature Active Directory platform footprint.
* **SMB Null Session (Phase 2):** Established an anonymous IPC pipe handle to read local configuration guidelines, security rules, and network identities.
* **LDAP Enumeration (Phase 3):** Dumped data records, organizational units, and directory structural data sets straight out of the active domain controller catalog.
* **Password Spraying (Phase 4):** Completed horizontal security checks utilizing standard corporate baselines, safely validating low-entropy account credentials.
* **BloodHound Attack Path (Phase 5 & 6):** Derived structural permission links across the network environment, confirming an exploitation path right up into the Domain Admins ecosystem.
</div>

---

<div align="justify">

## 🛡️ Defensible Remediation Strategies
To harden the target environment and eliminate the vectors exploited during this simulation, implement the following changes:
1. **Block SMB Null Sessions:** Adjust relevant Registry configurations and local Group Policy Objects (GPO) to deny unauthenticated guest or anonymous network logons.
2. **Mandate LDAP Signing:** Turn on mandatory LDAP signing requirements alongside LDAP Channel Binding to terminate cleartext traffic vulnerabilities entirely.
3. **Deploy Fine-Grained Password Policies (FGPP):** Configure unique, restrictive security policies across human and system service objects to render standard automated dictionary attacks ineffective.
4. **Regularly Audit Active Directory ACLs:** Introduce routine defensive graph analysis using BloodHound to audit, track, and eliminate accidental structural privilege delegations.
</div>

---

<div align="justify">

**Author:** AbdulRaheem  
**Status:** Completed  
**Environment:** Lab Simulation  
</div>
