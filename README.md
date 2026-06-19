# Active Directory Attack Simulation Lab

## Overview
Built and analyzed an Active Directory environment to simulate real-world enterprise attack paths including enumeration, credential attacks, and privilege escalation analysis.

## Environment
- Windows Server 2022 (Domain Controller)
- Kali Linux (Attacker)
- Domain: corp.local

## Objectives
- AD enumeration using Nmap, SMB, LDAP
- Password attack simulation
- Attack path mapping using BloodHound
- Identify misconfigurations

## Tools Used
- Nmap
- NetExec
- SMBClient
- BloodHound
- Impacket

## Key Findings
- Exposed AD services (LDAP, SMB, Kerberos)
- Null session SMB enumeration enabled
- Weak password policy simulation
- Attack paths identified via BloodHound

## Attack Flow
Recon → SMB Enumeration → LDAP Enumeration → Credential Testing → BloodHound Analysis

## Screenshots
See /screenshots folder

## Author
Cybersecurity Practitioner (VAPT / AD Security Lab)
