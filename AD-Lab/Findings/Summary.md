# Security Findings

## 1. AD Reconnaissance
Exposed domain services detected (LDAP, SMB, Kerberos).

- Risk: Medium
- Impact: Attack surface exposed for enumeration

---

## 2. SMB Null Session
Anonymous SMB access partially allowed.

- Risk: High
- Impact: Domain info exposed without authentication

---

## 3. LDAP Exposure
LDAP service accessible for directory queries.

- Risk: Medium
- Impact: User/group enumeration possible