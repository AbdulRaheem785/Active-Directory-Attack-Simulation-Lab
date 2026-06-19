# Active Directory Attack Simulation Lab

![Active Directory Attack Simulation Lab](banner.jpg)

## 📌 Overview
This repository documents the design, implementation, and analysis of an enterprise-grade **Active Directory (AD) Attack Simulation Lab**. The objective of this project was to construct a secure-by-default environment, intentionally introduce common misconfigurations, and execute an end-to-end cyber attack lifecycle—ranging from initial network reconnaissance to full Domain Admin compromise.

---

## 🛠️ Lab Specifications & Environment

The architecture mimics a modern corporate environment using localized virtualization to isolate offensive testing.

![Lab Metadata](Screenshot%202026-06-19%20205703.png)

* **Target Domain Controller:** Windows Server 2022 (`corp.local`)
* **Attacker Platform:** Kali Linux
* **License:** MIT
* **Focus Areas:** Network Enumeration, Active Directory Misconfigurations, Credential Testing, Graph-Based Attack Path Analysis.

### Weaponry & Defensive Utilities Used
The following industry-standard tools were leveraged throughout the simulation:

![Tools Used](Screenshot%202026-06-19%20205725.png)

* **Nmap:** Network discovery and service fingerprinting.
* **NetExec / CrackMapExec:** Multi-protocol automation for SMB/LDAP enumeration and post-exploitation.
* **BloodHound:** Graph-theory-based Active Directory attack path mapping.
* **Impacket Suite:** Interaction with Windows network protocols (SMB, Kerberos, RPC).
* **SMBClient:** Manual share interaction and null-session testing.
* **Kerbrute:** Stealthy Kerberos pre-authentication user enumeration.

---

## 🛑 Attack Flow Lifecycle

The simulation followed a structured, professional penetration testing methodology to compromise the `corp.local` domain.

![Attack Flow](Screenshot%202026-06-19%20205812.png)

1.  **Reconnaissance (Nmap):** Identified open ports and critical running services (LDAP, SMB, Kerberos, RPC).
2.  **SMB Enumeration:** Exploited null session vulnerabilities to enumerate open shares and local policies.
3.  **LDAP Enumeration:** Queried the Active Directory database anonymously/with low privileges to extract structural user, group, and domain data.
4.  **Credential Attacks:** Conducted targeted password spraying and validation against the discovered user roster.
5.  **BloodHound Analysis:** Ingested domain data into Neo4j to visualize transitive relationships and complex permission chains.
6.  **Privilege Escalation:** Executed precise attack vectors to escalate privileges from a standard user to full **Domain Admin**.

---

## 🔍 Key Findings & Vulnerability Assessment

* **Exposed Directory Services:** Unauthenticated access allowed initial interaction with core infrastructure components (`389/LDAP`, `445/SMB`, `88/Kerberos`).
* **SMB Null Sessions Enabled:** Misconfigured registry keys permitted anonymous IPC share enumeration, leaking domain configuration insights.
* **Weak Password Policy Enforcement:** Allowed successful horizontal movement via automated password spraying without triggering account lockouts.
* **Transitive Privilege Paths:** BloodHound uncovered hidden ACL/ACE paths (e.g., `GenericAll`, `WriteDacl`) that allowed standard service accounts to take control of administrative groups.

---

## 📸 Technical Evidence & Execution

Below are the cryptographic and terminal proofs demonstrating successful execution at each stage of the assessment lifecycle.

![Evidence Screenshots](Screenshot%202026-06-19%20205751.png)

### 1. Phase 1 & 2: Reconnaissance & SMB Exploitation
* **Nmap Enumeration:** Scanned the Target IP to map the attack surface, confirming Active Directory footprints (`88`, `389`, `445`, `3268`).
* **SMB Null Session:** Successfully authenticated with a blank username and password to read system configurations and pipe connections.

### 2. Phase 3 & 4: AD Harvesting & Credential Spraying
* **LDAP Enumeration:** Extracted the entire Active Directory user schema, structural organization units (OUs), and group memberships.
* **Password Spraying:** Executed low-and-slow password testing against the extracted user list to identify weak passwords while evading basic detection.

### 3. Phase 5 & 6: Path Graphing & Domain Takeover
* **BloodHound Attack Path:** Mapped out the precise layout of objects connecting the compromised user account to the high-value `Domain Admins` group, simplifying final privilege escalation.

---

## 🛡️ Remediation Strategies
To secure the `corp.local` infrastructure against these simulated vectors, the following hardening steps are recommended:
1.  **Disable SMB Null Sessions:** Restrict anonymous access to named pipes and shares via Group Policy Objects (GPO).
2.  **Enforce LDAP Signing and Channel Binding:** Prevent cleartext LDAP queries and enforce secure authentication.
3.  **Implement Fine-Grained Password Policies (FGPP):** Increase complexity and implement strict lockout thresholds to break password spraying efficacy.
4.  **Audit Active Directory ACLs:** Regularly run BloodHound defensively to identify and eliminate accidental privilege delegation (e.g., non-admin users with modification rights on administrative groups).

---
**Author:** AbdulRaheem
