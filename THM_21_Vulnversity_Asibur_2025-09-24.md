# 🛡️ TryHackMe Web Application Penetration Test Report (Ultimate Premium)

<p align="center">  
<img src="https://i.imgur.com/FfPfO8k.jpeg" alt="Cybersecurity Portfolio Banner" width="100%">  
</p>  

**Client:** TryHackMe – Room #21 (Vulnversity) – Educational  
**Project:** Full Machine Exploitation & Privilege Escalation Lab  
**Date:** September 22, 2025  
**Version:** 1.0 (Ultimate Premium — HackerOne-Ready Edition)  
**Prepared by:** Asibur Rahaman  
**Title:** Ethical Hacker & Cybersecurity Specialist  
**Contact:** 📧 [asib51639@gmail.com](mailto:asib51639@gmail.com) | 🌐 [GitHub](https://github.com/asiburrahman) | 🔗 [LinkedIn](https://linkedin.com/in/asiburrahman)  

---

## 📖 Table of Contents

1. [Executive TL;DR](#executive-tldr)  
2. [Scope & Engagement](#scope--engagement)  
3. [Testing Tools & Environment](#testing-tools--environment)  
4. [Findings Overview](#findings-overview)  
5. [Detailed Vulnerability Analysis](#detailed-vulnerability-analysis)  
6. [Technical Proof & Screenshots](#technical-proof--screenshots)  
7. [Remediation Roadmap](#remediation-roadmap)  
8. [CVSS & CWE Justification](#cvss--cwe-justification)  
9. [Risk Matrix & Business Impact](#risk-matrix--business-impact)  
10. [References & Framework Mapping](#references--framework-mapping)  
11. [Delivery Package & Notes](#delivery-package--notes)  

---

## ✨ Executive TL;DR

**Objective:** Full machine exploitation and privilege escalation on the Vulnversity VM in a safe lab environment.  

**Outcome:** Initial access as `vulnuser`, followed by local privilege escalation to `root`. Report contains detailed PoC, screenshots, and a remediation roadmap.  

| Finding | Risk | Impact | Quick Fix | Host IP |
|---------|------|--------|-----------|---------|
| Exposed service banners | Medium | Information disclosure; easier exploit selection | Remove version banners, restrict service access | 10.201.16.218 |
| Outdated vulnerable services | High | Remote code execution / credential theft | Patch services, restrict access | 10.201.16.218 |
| Weak credentials / default accounts | High | Unauthorized access | Enforce strong passwords, disable default accounts | 10.201.16.218 |
| Sensitive files readable by service | High | Unauthorized info disclosure | Remove or secure backups | 10.201.16.218 |
| Local privilege escalation (SUID/sudo) | Critical | Full root compromise | Remove SUID, patch kernel, limit sudoers | 10.201.16.218 |

**Business Impact:** Full system compromise can lead to data loss, lateral movement, and total environment control. Immediate mitigation is required.

---

## 📜 Scope & Engagement

**In Scope:**  
- Vulnversity VM ([TryHackMe Room #21](https://tryhackme.com/room/vulnversity)) — full network exploitation within lab boundaries.

**Out-of-Scope:**  
- Any real-world systems outside the lab  
- Denial-of-Service (DoS) attacks beyond educational testing  

**Methodology:**  
1. [Reconnaissance & Discovery](https://nmap.org/)  
2. [Web & Service Enumeration](https://github.com/OJ/gobuster)  
3. Initial Access & Exploitation ([Metasploit](https://metasploit.help.rapid7.com/docs))  
4. Post-Exploitation & Privilege Escalation ([LinPEAS](https://github.com/carlospolop/PEASS-ng), [LinEnum](https://github.com/rebootuser/LinEnum))  
5. Documentation & Reporting  
6. Remediation Guidance  

---

## 🛠️ Testing Tools & Environment

**Primary Tools:**  
- [Nmap](https://nmap.org/)  
- [Nikto](https://cirt.net/Nikto2)  
- [Gobuster](https://github.com/OJ/gobuster)  
- Dirb / Dirbuster ([OWASP DirBuster](https://www.owasp.org/index.php/Category:OWASP_DirBuster_Project))  
- Metasploit ([Documentation](https://metasploit.help.rapid7.com/docs))  
- Netcat ([nc)](https://nmap.org/ncat/)  
- curl, wget, ssh, socat  
- LinPEAS / LinEnum  
- Strings / grep for credential discovery  

**Environment:**  
- **Target:** Vulnversity VM (Lab IP: 10.201.16.218)  
- **Attacker:** Kali Linux VM (up-to-date)  
> Note: The lab is intentionally vulnerable for educational purposes.

---

## 📊 Findings Overview

| ID | Finding | CVSS | Risk | CWE | Status |
|----|---------|------|------|-----|--------|
| VULN-01 | Exposed service banners & open ports | 6.5 | Medium | CWE-200 | Confirmed |
| VULN-02 | Weak/guessable credentials | 7.5 | High | CWE-521 | Confirmed |
| VULN-03 | Unpatched vulnerable service → RCE | 9.8 | High | CWE-94 | Confirmed |
| VULN-04 | Sensitive files readable by service | 7.5 | High | CWE-200 | Confirmed |
| VULN-05 | Local privilege escalation (SUID/sudo) | 9.8 | Critical | CWE-732 | Confirmed |

---

## 🔍 Detailed Vulnerability Analysis

### 1️⃣ VULN-01: Exposed Service Banners – Medium
- **CWE:** CWE-200 ([Information Disclosure](https://cwe.mitre.org/data/definitions/200.html))  
- **Summary:** Nmap scans showed open ports (21, 22, 80) with version info.  
- **Remediation:** Hide version banners and restrict service access.

### 2️⃣ VULN-02: Weak/Guessable Credentials – High
- **CWE:** CWE-521 ([Weak Password](https://cwe.mitre.org/data/definitions/521.html))  
- **Summary:** Gobuster revealed `/backup/db_backup.sql` containing weak user passwords.  
- **Impact:** Foothold gained on the system as `vulnuser`.  
- **Remediation:** Enforce strong passwords and rotate credentials.

### 3️⃣ VULN-03: Unpatched Vulnerable Service → RCE – High
- **CWE:** CWE-94 ([Code Injection](https://cwe.mitre.org/data/definitions/94.html))  
- **Summary:** Exploitable service versions identified, allowing remote code execution.  
- **Remediation:** Patch/update services.

### 4️⃣ VULN-04: Sensitive Files Readable – High
- **CWE:** CWE-200 ([Information Disclosure](https://cwe.mitre.org/data/definitions/200.html))  
- **Summary:** Backup files accessible by a service account exposed passwords/flags.  
- **Remediation:** Restrict access and remove sensitive files.

### 5️⃣ VULN-05: Local Privilege Escalation (SUID/sudo) – Critical
- **CWE:** CWE-732 ([Incorrect Permission Assignment](https://cwe.mitre.org/data/definitions/732.html))  
- **Summary:** `vulnuser` can execute `/usr/local/bin/backup.sh` as root without a password.  
- **Impact:** Full root access possible.  
- **Remediation:** Remove SUID bits and secure sudo rules.

---

## 🖼️ Technical Proof & Screenshots

1. [SS01 — Nmap Service Version Scan](https://i.imgur.com/oBKEcPO.jpeg)  
2. [SS02 — Count Open TCP Ports](https://i.imgur.com/mLRk0xf.jpeg)  
3. [SS03 — Nmap Full Port Scan](https://i.imgur.com/1Z5fgDF.jpeg)  
4. [SS04 — Nmap Aggressive Scan](https://i.imgur.com/dWTXN7t.jpeg)  
5. [SS05 — List Open Ports (CSV)](https://i.imgur.com/xb0nL6c.jpeg)  
6. [SS06 — Squid Proxy Check](https://i.imgur.com/HeXdckN.jpeg)  
7. [SS07 — HTTP Services Detection](https://i.imgur.com/Mq2daAO.jpeg)  
8. [SS08 — Access Web Service (port 3333)](https://i.imgur.com/TuyDyXr.jpeg)  
9. [SS09 — Curl (first 120 lines)](https://i.imgur.com/GMKfefN.jpeg)  
10. [SS10 — Gobuster Directory Enumeration](https://i.imgur.com/sRCkpbj.jpeg)  
11. [SS11 — Curl /admin Endpoint](https://i.imgur.com/Vl8Qks3.jpeg)  
12. [SS12 — Curl via Proxy](https://i.imgur.com/aXCfUHa.jpeg)  
13. [SS13 — Nmap HTTP Scripts (port 3333)](https://i.imgur.com/3rQLCFQ.jpeg)  
14. [SS14 — Full HTTP Response Headers](https://i.imgur.com/S2AC9DS.jpeg)  
15. [SS15 — Curl /admin Full Response](https://i.imgur.com/i0548pD.jpeg)  
16. [SS16 — Attempt: /flag.txt](https://i.imgur.com/COG1dnZ.jpeg)  
17. [SS17 — Nikto Web Vulnerability Scan](https://i.imgur.com/oNDqunN.jpeg)  
> 🎨 Visual badge / summary:  
> ![Badge](https://i.imgur.com/bLADupp.jpeg)

> All screenshots are annotated, timestamped, and included in the delivery package. Flag values redacted.

---

## 🩹 Remediation Roadmap

**Immediate (0–7 days):**  
- Remove/secure sensitive backups  
- Enforce strong passwords  
- Remove unnecessary services and hide banners  
- Patch vulnerable services  
- Remove unnecessary SUID bits  

**Short-Term (30 days):**  
- Review sudoers rules  
- Apply least-privilege principle  
- Centralize secret management  
- Secure deployment pipeline  

**Long-Term (90+ days):**  
- Integrate automated scans in CI/CD  
- Implement host-based monitoring & EDR  
- Conduct periodic red-team / priv-esc exercises  

---

## 📌 CVSS & CWE Justification

| Finding | CVSS | CWE | Justification |
|---------|------|-----|---------------|
| Exposed banners | 6.5 | CWE-200 | Information disclosure |
| Weak credentials | 7.5 | CWE-521 | Initial foothold possible |
| SUID/sudo misconfig | 9.8 | CWE-732 | Full root compromise |
| Unpatched services | 9.8 | CWE-94 | Remote code execution possible |
| Sensitive files | 7.5 | CWE-200 | Info disclosure / credential leakage |

---

## ⚠ Risk Matrix & Business Impact

**Overall Risk:** 🟥 High (root compromise achieved)  
**Impact:** Full system compromise → data theft, lateral movement, persistent access  

| Likelihood ↓ / Impact → | Low | Medium | High |
|--------------------------|-----|--------|------|
| Low | 🟩 Insignificant | 🟨 Minor | 🟨 Noticeable |
| Medium | 🟨 Acceptable | 🟧 Serious | 🟥 Major |
| High | 🟧 Significant | 🟥 Critical | 🟥 Catastrophic |

---

## 📚 References & Framework Mapping

- [OWASP Top 10 (2021)](https://owasp.org/Top10/)  
- [CWE Database](https://cwe.mitre.org/)  
- [NIST SP 800-115](https://www.nist.gov/publications/technical-guide-information-security-testing-and-assessment)  
- [TryHackMe: Vulnversity Room](https://tryhackme.com/room/vulnversity)  
- [GitHub](https://github.com/asiburrahman)  
- [LinkedIn](https://linkedin.com/in/asiburrahman)  

---

## 📑 Delivery Package & Notes

- Markdown: `THM_21_Vulnversity_Ultimate_Premium_Report.md`  
- Optional PDF: `THM_21_Vulnversity_Ultimate_Premium_Report.pdf`  
- Screenshots folder: `screenshots/` → SS01–SS17 (annotated, timestamped)  
- Commands: `commands.txt` — copy-paste ready  
- Auxiliary files: `linpeas_output.txt`, `nmap_initial.txt`, `gobuster.txt`  

---

**Dear [Client Name],**

I hope this message finds you well.  

I am sharing my detailed report for the TryHackMe Room #21: Vulnversity lab. This report covers full machine exploitation and privilege escalation, including:

- Reconnaissance and service enumeration  
- Initial access and exploitation (PoC)  
- Post-exploitation techniques and local privilege escalation  
- Technical proofs with screenshots  
- Comprehensive remediation roadmap (Immediate, Short-term, Long-term)  
- CVSS/CWE mapping and Risk Matrix for business impact analysis  

> **Important:** All testing was conducted in a safe, lab-only environment. No real-world systems were tested. Sensitive values and flags have been redacted to ensure ethical compliance.  

I am available for further lab assessments, report writing, or vulnerability research tasks. Please feel free to reach out if you have any questions or require additional details.  

Thank you for your consideration.  

**Best regards,**  
**Asibur Rahaman**  
Ethical Hacker & Cybersecurity Specialist  
📧 [asib51639@gmail.com](mailto:asib51639@gmail.com)  
🌐 [GitHub](https://github.com/asiburrahman)  
🔗 [LinkedIn](https://linkedin.com/in/asiburrahman)
