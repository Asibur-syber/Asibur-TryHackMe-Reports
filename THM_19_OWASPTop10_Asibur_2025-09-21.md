# 🛡 TryHackMe Web Application Penetration Test Report (Ultimate Premium)

<p align="center">
  <img src="https://i.imgur.com/QYVip77.jpeg" alt="Cybersecurity Portfolio Banner" width="100%">
</p>  

**Client:** TryHackMe – Room #19 (OWASP Top 10) – Educational  
**Project:** Web Application Security Assessment (OWASP Framework)  
**Date:** September 21, 2025  
**Version:** 4.2 (Ultimate Premium HackerOne-Ready Edition)  
**Prepared by:** Asibur Rahaman  
**Title:** Ethical Hacker & Cybersecurity Specialist  
**Contact:** 📧 asib51639@gmail.com | 🌐 [GitHub](https://github.com/Asibur-syber) | 🔗 [LinkedIn](https://www.linkedin.com/)  

---

## 📖 Table of Contents

1. [Executive TL;DR](#-executive-tldr)  
2. [Scope & Engagement](#-scope--engagement)  
3. [Testing Tools & Environment](#-testing-tools--environment)  
4. [Findings Overview](#-findings-overview)  
5. [Detailed Vulnerability Analysis](#-detailed-vulnerability-analysis)  
6. [Technical Proof & Screenshots](#-technical-proof--screenshots)  
7. [Remediation Roadmap](#-remediation-roadmap)  
8. [CVSS & CWE Justification](#-cvss--cwe-justification)  
9. [Risk Matrix & Business Impact](#-risk-matrix--business-impact)  
10. [References & Framework Mapping](#-references--framework-mapping)  
11. [Delivery Package & Notes](#-delivery-package--notes)  

---

## ✨ Executive TL;DR (Decision Maker Ready)

**Objective:** Identify, exploit, and remediate OWASP Top 10 vulnerabilities in TryHackMe Lab Room #19.  

**Outcome:** Client-ready, actionable report suitable for freelance delivery, bug bounty submission, and portfolio showcase.

| Vulnerability | Risk | Impact | Quick Fix | Target IP |
|---------------|------|--------|-----------|-----------|
| SQL Injection | Critical | Database compromise / RCE | Parameterized queries, ORM | 10.201.4.206 |
| Broken Auth | High | Account takeover | MFA, secure sessions | 10.201.77.228 |
| Sensitive Data Exposure | High | Credential theft | TLS, encryption at rest | 10.201.120.119 |
| XXE | High | File disclosure / SSRF | Disable external XML entities | 10.201.29.198 |
| IDOR / Broken Access Control | Critical | Unauthorized access | Server-side access checks | 10.201.30.140 |
| Security Misconfig | Medium | System compromise | Configuration hardening | 10.201.125.250 |
| XSS | Medium | Session hijack / Credential theft | Output encoding, CSP headers | 10.201.62.56 |
| Insecure Deserialization | High | RCE / PrivEsc | Avoid untrusted deserialization | 10.201.69.226 |
| Known Vulnerable Components | High | Exploits | Regular patch management | 10.201.106.190 |
| Insufficient Logging & Monitoring | Low | Detection delay | Centralized SIEM, audit logs | N/A |

**Key Takeaways:**  
- Immediate mitigation required for SQLi, IDOR, XXE  
- Implement MFA, encryption, secure session management  
- Continuous patching, monitoring, and DevSecOps recommended  
- Ready for delivery to clients, HackerOne/Bugcrowd submissions  

---

## 📜 Scope & Engagement

**In Scope:**  
- TryHackMe Lab Room #19 (OWASP Top 10)  
- Simulated vulnerable web applications for educational purposes  

**Out-of-Scope:**  
- DoS attacks  
- Physical security assessments  

**Methodology:**  
1. Reconnaissance  
2. Vulnerability Identification  
3. Exploitation (PoC)  
4. Documentation & Reporting  
5. Remediation Guidance  

**Frameworks Used:**  
- [OWASP Top 10 – 2021](https://owasp.org/Top10/)  
- [NIST SP 800-115](https://csrc.nist.gov/publications/detail/sp/800-115/final)  

---

## 🛠 Testing Tools & Environment

**Tools Used:**  
- Burp Suite Professional / ZAP Proxy  
- SQLMap & Manual SQLi Testing  
- OWASP ZAP Active Scanning  
- Nikto & Nmap for web & network discovery  
- Postman for API testing  
- OpenSSL & TLS inspection tools  
- DevTools (Browser Developer Tools — Network / Console / Elements / Sources)

**Environment:**  
- Lab IPs provided for each vulnerability  
- Local Kali Linux VM (2025)  
- Proxy and VPN isolation for safe exploitation  
- Screenshots & PoC stored for report delivery  

---

## 📊 Findings Overview

| ID | Vulnerability | CVSS | Risk | CWE | Status | Target IP |
|----|---------------|------|------|-----|--------|-----------|
| 01 | SQL Injection | 9.8  | Critical | CWE-89 | Confirmed | 10.201.4.206 |
| 02 | Broken Auth | 8.1 | High | CWE-287 | Confirmed | 10.201.77.228 |
| 03 | Sensitive Data Exposure | 7.5 | High | CWE-200 | Confirmed | 10.201.120.119 |
| 04 | XXE | 7.4 | High | CWE-611 | Confirmed | 10.201.29.198 |
| 05 | Broken Access Control | 9.0 | Critical | CWE-639 | Confirmed | 10.201.30.140 |
| 06 | Security Misconfiguration | 6.5 | Medium | CWE-16 | Confirmed | 10.201.125.250 |
| 07 | XSS | 6.1 | Medium | CWE-79 | Confirmed | 10.201.62.56 |
| 08 | Insecure Deserialization | 8.2 | High | CWE-502 | Confirmed | 10.201.69.226 |
| 09 | Vulnerable Components | 7.2 | High | CWE-937 | Confirmed | 10.201.106.190 |
| 10 | Insufficient Logging & Monitoring | 5.5 | Low | CWE-778 | Confirmed | N/A |

---

## 🔍 Detailed Vulnerability Analysis

### 1️⃣ SQL Injection – Critical
- **CWE-89**  
- **Target IP:** 10.201.4.206  
- Example: `http://target/login.php?user=admin' OR '1'='1`  
- **Impact:** Full database disclosure / RCE  
- **Remediation:** Parameterized queries, ORM frameworks, input validation  

### 2️⃣ Broken Authentication – High
- **CWE-287**  
- **Target IP:** 10.201.77.228  
- Weak session tokens, re-registration flaws  
- **Impact:** Account takeover  
- **Remediation:** MFA, secure session handling, strong password policies  

### 3️⃣ Sensitive Data Exposure – High
- **CWE-200**  
- **Target IP:** 10.201.120.119  
- Plaintext passwords, unencrypted traffic  
- **Remediation:** TLS for all communication, encrypt sensitive data at rest  

*(Remaining vulnerabilities formatted similarly with Target IPs; Insufficient Logging & Monitoring = N/A)*

---

## 🖼 Technical Proof & Screenshots

1. **SQL Injection – Login/Search Form (SS01)**  
   ![SS01 – SQL Injection](https://i.imgur.com/ZdrZJza.jpeg)  
   *Bypassed authentication using `' OR '1'='1`. Demonstrates DB query manipulation.*

2. **Broken Authentication: Weak Password / Re-registration (SS02)**  
   ![SS02 – Broken Authentication](https://i.imgur.com/6DKvnPL.jpeg)  
   *Weak password/re-registration allowed unauthorized account access.*

3. **Sensitive Data Exposure (SS03)**  
   ![SS03 – Sensitive Data Exposure](https://i.imgur.com/k8meblo.jpeg)  
   *Credentials sent via HTTP, no encryption.*

4. **XXE Attack Proof (SS04)**  
   - **Web Form (XXE Attack Example):** [View Screenshot](https://i.imgur.com/d8ZRgnW.jpeg)
   - **Burp Repeater:** ![SS04 – XXE Burp](https://i.imgur.com/bvAFFKv.jpeg)  
   *XML payload disclosed `/etc/passwd`.*

5. **Broken Access Control (IDOR) (SS05)**  
   - **Browser:** ![SS05 – IDOR Browser](https://i.imgur.com/Xhg3AHG.jpeg)  
   - **Burp Suite:** ![SS05 – IDOR Burp](https://i.imgur.com/Z8ekxJe.jpeg)  
   *Direct access to `note.php?note=0` revealed sensitive flag.*

6. **Security Misconfiguration: Default Credentials & Flag Disclosure (SS06)**  
   ![SS06 – Security Misconfiguration](https://i.imgur.com/ziMoPKp.jpeg)  
   *Exposed flag `thm{4b591366fd5648a7b28aa1f9667217}` due to insecure defaults.*

7. **Cross-Site Scripting (XSS) (SS07)**  
   ![SS07 – XSS](https://i.imgur.com/Jp4tGiD.jpeg)  
   *Injected `<script>alert(1)</script>` executed successfully.*

8. **Insecure Deserialization (SS08)**  
   - **Burp Suite:** ![SS08 – Deserialization Burp](https://i.imgur.com/iraeEbO.jpeg)  
   - **Terminal:** ![SS08 – Deserialization Terminal](https://i.imgur.com/bIn4yXr.jpeg)  
   *Serialized payload accepted, potential remote code execution.*

9. **Using Components with Known Vulnerabilities (SS09)**  
   - **Outdated jQuery v1.4.2:** ![SS09 – jQuery 1.4.2](https://i.imgur.com/YEfYkby.jpeg)  
   - **jQuery v2.1.4 & Bootstrap:** ![SS09 – jQuery 2.1.4](https://i.imgur.com/RknqYvZ.jpeg)  
   *Outdated libraries exposed to known CVEs.*

10. **Insufficient Logging & Monitoring (SS10)**  
   ![SS10 – Failed Login Attempts](https://i.imgur.com/Kqq2mSI.jpeg)  
   *Multiple failed logins detected, no proper alerts.*

> 🎨 Visual badge / summary:  
> ![Badge](https://i.imgur.com/FviV7Bd.jpeg)

**PoC Commands & Scripts:** See `commands.txt`  

---

## 🩹 Remediation Roadmap

### ⏱ Immediate (0–7 Days)
- Block SQLi, IDOR, XXE via WAF rules  
- Remove default accounts & sensitive files  
- Enforce HTTPS with valid TLS certificates  
- Patch all critical components  

### 📅 Short-Term (30 Days)
- Refactor code with secure practices  
- Implement MFA & secure session handling  
- Encrypt sensitive data at rest & in transit  
- Developer training & configuration audits  

### 📆 Long-Term (90 Days)
- DevSecOps pipeline with automated SAST/DAST  
- OWASP ASVS Level 2 adoption  
- Centralized SIEM & anomaly detection  
- Regular pentest & red-team exercises  
- Continuous third-party patch management  

---

## 📌 CVSS & CWE Justification

| Vulnerability | CVSS | CWE | Justification |
|---------------|------|-----|---------------|
| SQL Injection | 9.8 | CWE-89 | Full DB compromise possible |
| Broken Auth | 8.1 | CWE-287 | Account takeover risk |
| Sensitive Data Exposure | 7.5 | CWE-200 | Credentials exposed, compliance risk |
| … | … | … | … |

---

## ⚠ Risk Matrix & Business Impact

| Likelihood ↓ / Impact → | Low | Medium | High |
|--------------------------|-----|--------|------|
| Low | 🟩 Insignificant | 🟨 Minor | 🟨 Noticeable |
| Medium | 🟨 Acceptable | 🟧 Serious | 🟥 Major |
| High | 🟧 Significant | 🟥 Critical | 🟥 Catastrophic |

**Overall Risk:** 🟥 High  
**Business Impact:**  
- Data breach, financial & reputational loss  
- Compliance violations: GDPR / PCI / HIPAA  
- Priority remediation recommended  

---

## 📚 References & Framework Mapping

- [OWASP Top 10 (2021)](https://owasp.org/Top10/)  
- [CWE Database](https://cwe.mitre.org/)  
- [NIST SP 800-115](https://csrc.nist.gov/publications/detail/sp/800-115/final)  
- [GitHub](https://github.com/Asibur-syber)  
- [LinkedIn](https://www.linkedin.com/)  
- [TryHackMe – OWASP Top 10 Room](https://tryhackme.com/room/owasptop10)  

---

## 📑 Delivery Package

- `THM_19_OWASP_Ultimate_Premium_Report.pdf`  
- `screenshots/` folder (SS01–SS10)  
- `commands.txt` (copy-paste ready)  
- Optional Burp/ZAP project  
- TL;DR Executive Summary (1-page PDF)  
- README.md explaining structure & usage  

**Use Cases:**  
- Fiverr / Upwork freelance delivery  
- Bug bounty submissions (HackerOne / Bugcrowd)  
- GitHub portfolio showcase  

---

*Prepared by Asibur Rahaman – Ethical Hacker & Cybersecurity Specialist – Ultimate Premium HackerOne-Ready Edition*
