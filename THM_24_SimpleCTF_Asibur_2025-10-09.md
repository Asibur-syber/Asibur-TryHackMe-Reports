# 🧪 TryHackMe Simple CTF – Penetration Test Report (Ultimate Premium Edition)

<p align="center">
<img src="https://i.imgur.com/2dsxMFs.jpeg" alt="Cybersecurity Portfolio Banner" width="100%">
</p>

**Client:** TryHackMe – Room #24 (Simple CTF) – Educational  
**Project:** Network & Web Exploitation, Privilege Escalation  
**Date:** October 9, 2025  
**Version:** 1.2 (Ultimate Premium — Enhanced for Clarity)  
**Prepared by:** Asibur Rahaman  
**Title:** Ethical Hacker & Cybersecurity Specialist  
**Contact:** 📧 (asib51639@gmail.com)| 🌐 [GitHub — Asibur-syber](https://github.com/Asibur-syber) | 🔗 [LinkedIn ](https://www.linkedin.com/)

---

## 📖 Table of Contents
- [✨ Executive TL;DR](#-executive-tldr)  
- [📜 Scope & Engagement](#-scope--engagement)  
- [🛠 Testing Tools & Environment](#-testing-tools--environment)  
- [📊 Findings Overview](#-findings-overview)  
- [🔍 Detailed Vulnerability Analysis](#-detailed-vulnerability-analysis)  
- [⏱ Exploitation Timeline](#-exploitation-timeline)  
- [🖼 Technical Proof & Screenshots](#-technical-proof--screenshots)  
- [🩹 Remediation Roadmap](#-remediation-roadmap)  
- [📌 CVSS & CWE Justification](#-cvss--cwe-justification)  
- [⚠ Risk Matrix & Business Impact](#-risk-matrix--business-impact)  
- [📚 References & Framework Mapping](#-references--framework-mapping)  
- [📑 Delivery Package & Notes](#-delivery-package--notes)  
- [🔐 Evidence / Redaction Policy](#-evidence--redaction-policy)  
- [💌 Personal Note to Client](#-personal-note-to-client)  
- [⚖ License & Disclaimer](#-license--disclaimer)

---

## ✨ Executive TL;DR

**Objective:** Assess the Simple CTF VM (TryHackMe Room #24)(https://tryhackme.com/room/easyctf) for initial access vulnerabilities and local privilege escalation paths.

**Summary:** Initial access was achieved via brute-forcing weak credentials on an exposed SSH service (SCTF-01). This low-privileged access was immediately escalated to root due to a critical **Sudo NOPASSWD** misconfiguration (SCTF-03), allowing full system compromise in minutes.

**Business Risk Highlights:**
- Weak Authentication allows external attackers immediate network presence (Low Barrier to Entry).
- Sudo Misconfiguration (Critical) allows instant and persistent full administrator control from a compromised low-privileged account.
- Compliance Failure Risk (e.g., PCI-DSS Requirement 8 for Strong Access Control).

> **Note:** All testing was performed inside the TryHackMe lab environment under authorization. Do not apply these techniques to unauthorized systems.

---

## 📜 Scope & Engagement

**In Scope**
- Simple CTF VM — TryHackMe Room #24 (Web Server, SSH, host filesystem).

**Out-of-Scope**
- Denial-of-Service (DoS) tests.
- Any external networks or systems not part of the lab.

**Methodology (high-level)**
1. Reconnaissance (Nmap, Web discovery)  
2. Enumeration (vulnerability scanning, service probing, credential spraying/brute-forcing)  
3. Verification (safe, lab-only PoC)  
4. Privilege escalation checks (sudoers, GTFOBins, LinPEAS)  
5. Documentation & remediation recommendations

---

## 🛠 Testing Tools & Environment

| Tool | Purpose | Source |
|---|---:|---|
| Nmap | Network & service discovery | https://nmap.org/ |
| Gobuster / Dirb | Directory and file enumeration | https://github.com/OJ/gobuster |
| Hydra | Password brute-forcing | https://github.com/vanhauser-thc/thc-hydra |
| SSH | Remote command execution | OpenSSH docs |
| LinPEAS | Privilege escalation enumeration | https://github.com/carlospolop/PEASS-ng |

**Environment**
- Attacker: Kali Linux (2023.4)  
- Target: Simple CTF VM (Lab IP: `10.201.4.242`)

---

## 📊 Findings Overview

| ID | Finding | CVSS | Risk | CWE | Business Impact |
|---:|---|---:|---:|---|---|
| SCTF-01 | Weak/Trivial Authentication | 8.8 | High | [CWE-521](https://cwe.mitre.org/data/definitions/521.html) | Remote attacker gains system access (Initial Breach) |
| SCTF-02 | World-Readable Configuration Files | 5.3 | Medium | [CWE-552](https://cwe.mitre.org/data/definitions/552.html) | Exposes sensitive data; aids enumeration |
| SCTF-03 | Sudo NOPASSWD Misconfiguration | 9.8 | Critical | [CWE-284](https://cwe.mitre.org/data/definitions/284.html) | Local actor can escalate to root immediately |

---

## 🔍 Detailed Vulnerability Analysis

### 1️⃣ SCTF-01: Weak/Trivial Authentication – High  
**CWE:** [CWE-521 — Weak Password Requirements](https://cwe.mitre.org/data/definitions/521.html)

**Summary:**  
An exposed SSH service was protected by trivial or easily guessable credentials. A dictionary attack successfully identified the credential set used for initial low-privileged access.

**Impact:**  
Full remote shell access as a non-privileged user, providing a persistent entry point.

**PoC (lab-only):**
```bash
# 1) Brute-force SSH using Hydra (lab-only, authorized)
hydra -L /usr/share/wordlists/metasploit/http_default_userpass.txt \
      -P /usr/share/wordlists/rockyou.txt \
      ssh://10.201.4.242 -t 4

# 2) Successful login (ssh redacted_user@10.201.4.242)
ssh redacted_user@10.201.4.242
```

**Remediation:**  
- Enforce strong password policies (length, complexity, rotation).  
- Implement account lockouts after repeated failed attempts.  
- Use Multi-Factor Authentication (MFA) and restrict SSH access via allowlists (e.g., VPN, jump host).

---

### 2️⃣ SCTF-02: World-Readable Configuration Files – Medium  
**CWE:** [CWE-552: Files or Directories Accessible to External Parties](https://cwe.mitre.org/data/definitions/552.html)

**Summary:**  
Publicly accessible files (web root or user dirs) contained hints or developer notes that aided enumeration and shortened time-to-compromise.

**Impact:**  
Exposed information accelerates enumeration and privilege escalation.

**Evidence & Notes (example):**
```bash
# Find readable files under webroot that mention hints/usernames
find /var/www/html -type f -readable -exec grep -H -i "hint\|user" {} \; 2>/dev/null
```

**Remediation:**  
- Review and fix file permissions.  
- Move sensitive files outside webroot and limit read access to specific service accounts.  
- Implement deployment checks to avoid leaking developer notes.

---

### 3️⃣ SCTF-03: Sudo NOPASSWD Misconfiguration – Critical  
**CWE:** [CWE-284: Improper Access Control](https://cwe.mitre.org/data/definitions/284.html)

**Summary:**  
The compromised low-privileged user is allowed to run one or more binaries via `sudo` without a password (`NOPASSWD`), enabling root shell spawn.

**Impact:**  
Immediate full system compromise (root) — attacker can bypass local security and persist.

**PoC (GTFOBins / lab-specific):**
```bash
# 1) Check sudo privileges for current user
sudo -l

# Example output might show:
# (user) NOPASSWD: /usr/bin/find

# 2) Exploit allowed binary to spawn root shell (lab-only)
sudo /usr/bin/find . -exec /bin/bash \; -quit

# OR if /bin/bash is allowed:
sudo /bin/bash

# Verify:
whoami   # -> root
id
```

**Remediation:**  
- Remove `NOPASSWD` entries; require a password for `sudo`.  
- Restrict `sudo` to minimal, necessary commands and use command whitelisting carefully.  
- Regularly audit `/etc/sudoers` and deployed sudoers.d fragments.

---

## ⏱ Exploitation Timeline

| Phase | Time Taken | Summary | Evidence |
|---:|---:|---|---|
| Reconnaissance | 10 mins | Nmap scan — open ports: 22, 80 | nmap output |
| Initial Enumeration | 20 mins | Web discovery, dirb/gobuster | gobuster logs |
| Initial Access | 30 mins | Credential brute-force (SSH) | hydra output (redacted) |
| Local Enumeration | 25 mins | `sudo -l`, file perms, linpeas | local enumeration logs |
| Privilege Escalation | 10 mins | Sudo NOPASSWD → root | exploit output |
| Flag Retrieval | 10 mins | User & root flags captured (redacted) | redacted flags |
| Documentation | 1 hr | Report writing & formatting | N/A |

---

## 🖼 Technical Proof & Screenshots

> All screenshots and raw logs are stored in the repository under `/screenshots/` and `/logs/`. Sensitive values (flags, credentials) have been **REDACTED** in public copies.

1. **Nmap Scan (SS01)**  
   ![SS01 – Initial Nmap Scan](https://i.imgur.com/8zbGU52.jpeg)  
   *Initial Nmap output showing full TCP scan, open ports and service/version fingerprints (e.g., 21/FTP, 22/SSH, 80/HTTP).*  
   **Timestamp:** `2025-10-09 06:42 BST` — *Redact any sensitive IP metadata if required.*

2. **Gobuster Directory Enumeration (SS02)**  
   ![SS02 – Gobuster Results](https://i.imgur.com/zsJSyDL.jpeg)  
   *Discovered web directories and status codes (e.g., /login, /admin, /robots.txt). Note notable 200/401/403 responses.*  
   **Timestamp:** `2025-10-09 07:05 BST`

3. **FTP Access Proof (SS03)**  
   ![SS03 – Access Proof (FTP)](https://i.imgur.com/gGYaTH8.jpeg)  
   *Anonymous FTP login proof (`230 Login successful`), directory listing and `cd pub` actions. Redact any creds in public images.*  
   **Timestamp:** `2025-10-09 07:12 BST` — *Ensure `230 Login successful` visible; blur any clear secrets.*

4. **Sudo Permissions Check (SS04)**  
   ![SS04 – Sudo Check](https://i.imgur.com/GyKGxnb.jpeg)  
   *`sudo -l` output showing allowed commands / NOPASSWD entries. Highlight exploitable allowed binaries.*  
   **Timestamp:** `2025-10-09 08:00 BST` — *Mark exploitable entries in notes section.*

5. **Privilege Escalation PoC (SS05)**  
   ![SS05 – Privesc PoC](https://i.imgur.com/dAlMC75.jpeg)  
   *Exploit/PoC output showing spawn of elevated shell via allowed binary (include `whoami` proof). Redact flags.*  
   **Timestamp:** `2025-10-09 08:05 BST` — *Include short command used in caption if space allows.*

6. **Root Shell Confirmation (SS06)**  
   ![SS06 – Root Confirmation](https://i.imgur.com/1vChNyV.jpeg)  
   *Confirmation of root (`whoami`, `id`) and quick `/root` listing. Ensure sensitive filenames are blurred for public deliverable.*  
   **Timestamp:** `2025-10-09 08:07 BST`

7. **User Flag Retrieval (SS07)**  
   ![SS07 – User Flag (Redacted)](https://i.imgur.com/INfPHcj.jpeg)  
   *User flag captured — redacted for public report (show `FLAG{REDACTED_PUBLIC}` in image). Keep unredacted copy under `/loot/`.*  
   **Timestamp:** `2025-10-09 08:09 BST` — *Do NOT place unredacted flags in public repo.*

8. **Root Flag Retrieval (SS08)**  
   ![SS08 – Root Flag (Redacted)](https://i.imgur.com/a33p9jT.jpeg)  
   *Root flag captured — redacted for public delivery. Include timestamp visible in original evidence.*  
   **Timestamp:** `2025-10-09 08:10 BST` — *Store full proof in private delivery artifacts only.*

> 🎨 Visual badge / summary:  
> ![Badge](https://i.imgur.com/CywsxZK.jpeg)

---

## 🩹 Remediation Roadmap (Prioritized)

### Immediate (0–7 days) — P0
- Revoke `NOPASSWD` entries in `/etc/sudoers`. Require password for all `sudo`.  
- Rotate weak/default credentials; enforce strong password policy (≥14 chars).  
- Implement account lockout thresholds (e.g., 5 failed attempts within 5 minutes).  

### Short-Term (7–30 days) — P1
- Audit & fix world-readable files and webroot contents.  
- Patch SSH and web services to latest stable versions.  
- Configure centralized logging & alerting for `sudo` and authentication attempts.

### Medium/Long-Term (30–90+ days) — P2
- Apply CIS benchmarks for Linux hosts.  
- Deploy Identity & Access Management (IAM) for centralized control.  
- Schedule regular automated vulnerability scans and pentest cadence.

---

## 📌 CVSS & CWE Justification

| Finding | CVSS | CWE | Justification |
|---|---:|---|---|
| Weak/Trivial Authentication | 8.8 | [CWE-521](https://cwe.mitre.org/data/definitions/521.html) | Trivial credentials enable remote breach (High) |
| World-Readable Files | 5.3 | [CWE-552](https://cwe.mitre.org/data/definitions/552.html) | Exposes internal data aiding attackers (Medium) |
| Sudo NOPASSWD Misconfiguration | 9.8 | [CWE-284](https://cwe.mitre.org/data/definitions/284.html) | Immediate route to root (Critical) |

---

## ⚠ Risk Matrix & Business Impact

**Overall Risk:** 🔴 Critical — Full system compromise achievable with minimal effort.  
**Business Impact:** Complete administrative takeover, data theft/destruction, reputational damage, and compliance violations.

---

## 📚 References & Framework Mapping

- OWASP Top 10 (2021) — https://owasp.org/www-project-top-ten/  
- CWE Database — https://cwe.mitre.org/  
- GTFOBins — https://gtfobins.github.io/  
- NIST SP 800-115 (Technical Guide) — https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-115.pdf  
- CIS Benchmarks — https://www.cisecurity.org/benchmark/  
- TryHackMe — https://tryhackme.com/  
- GitHub Profile — https://github.com/Asibur-syber

---

## 📑 Delivery Package & Notes

**Recommended repository structure:**
```
THM24_SimpleCTF/
├─ THM24_SimpleCTF_Report.md
├─ THM24_SimpleCTF_Report.pdf
├─ screenshots/
│  ├─ SS01InitialNmap.png
│  ├─ SS02WebEnum.png
│  ├─ SS03AccessProof.png
│  ├─ SS04SudoCheck.png
│  ├─ SS05PrivescPoC.png
│  └─ SS06RootConfirmation.png
└─ logs/
   ├─ nmapscan.txt
   ├─ hydra_output.txt (REDACTED for public)
   ├─ enumeration.txt
   └─ privesc_interaction.txt
```

**Notes**
- Public repo must contain only redacted artifacts (no flags, no real creds).  
- Full raw logs/screenshots can be provided privately under NDA.

---

## 🔐 Evidence / Redaction Policy

- **Public copies:** All flags, credentials, secrets **REDACTED**.  
- **Private copies:** Full logs/screenshots available under NDA.  

**Example:** `FLAG{a1b2c3d4e5}` → `FLAG{REDACTED_PUBLIC}`

---

## 💌 Personal Note to Client

> Dear Client,  
> Thank you for the opportunity to assess the Simple CTF VM. This report confirms high-risk vulnerabilities related to weak authentication and severe internal misconfiguration (Sudo). Addressing the Sudo misconfiguration (SCTF-03) should be your top priority as it represents an immediate path to root for any compromised low-privileged account.  
> Please let me know if you require a guided remediation session or a remediation playbook (I can produce a step-by-step fix list or walk you through changes).

**Best regards,**  
**Asibur Rahaman**  
Ethical Hacker & Cybersecurity Specialist  
📧 asib51639@gmail.com

---

## ⚖ License & Disclaimer

**License:** [CC BY-NC-SA 4.0 — Creative Commons](https://creativecommons.org/licenses/by-nc-sa/4.0/) — Educational, non-commercial reuse allowed with attribution.

**Disclaimer:** All testing performed within TryHackMe lab scope. Techniques are for education and authorized environments only.

**Prepared on:** October 9, 2025
