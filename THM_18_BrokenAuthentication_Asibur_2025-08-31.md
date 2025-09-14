# 🛡 Web Application Penetration Test Report  

<p align="center">
  <img src="https://i.imgur.com/do3UY0q.jpeg" alt="Cybersecurity Portfolio Banner" width="100%">
</p>  

Client: TryHackMe – Room #18 (Broken Authentication) – Educational  
Project: Authentication & Logic Flaw Vulnerability Assessment  
Date: August 31, 2025  
Version: Final Premium Edition  
Prepared by: Asibur Rahaman  
Title: Ethical Hacker & Cybersecurity Specialist  
Contact: 📧 asib51639@gmail.com | 🌐 GitHub | 🔗 LinkedIn  

---

## 📖 Table of Contents
1. [Executive Summary](#-executive-summary)  
2. [Assessment Timeline](#-assessment-timeline)  
3. [Scope & Engagement Details](#-scope--engagement-details)  
4. [Findings Overview](#-findings-overview)  
5. [Detailed Vulnerability Analysis](#-detailed-vulnerability-analysis)  
6. [Business Impact](#-business-impact)  
7. [Technical Evidence](#-technical-evidence)  
8. [Tools & Methodology](#-tools--methodology)  
9. [Proof & Screenshots](#-proof--screenshots)  
10. [Remediation Roadmap](#-remediation-roadmap)  
11. [Verification Steps](#-verification-steps)  
12. [Risk Matrix](#-risk-matrix)  
13. [References](#-references)  
14. [Appendix](#-appendix)  
15. [Delivery Note](#-delivery-note)  

---

## ✨ Executive Summary

A thorough penetration test was conducted on the target application (`10.201.90.135:8888`).  

**Key Findings:**  
- **Vulnerability:** Broken Authentication / Re-Registration Logic Flaw  
- **Severity:** Medium – CVSS 6.5 (CWE-287)  
- **Impact:** An attacker can bypass duplicate username checks using leading spaces (e.g., `" darren"`), allowing unauthorized account access.  

**Strategic Summary:**  
- Indicates critical input validation flaws in authentication workflow  
- Poses **account takeover risk**, exposure of sensitive information  
- Immediate remediation recommended for production or real-world deployment  

---

## 📅 Assessment Timeline
| Phase | Date | Activity | Outcome |
|-------|------|----------|---------|
| Initiation | Aug 28, 2025 | Project Kickoff & Scope Finalization | Engagement defined |
| Recon | Aug 29, 2025 | Registration Workflow Testing | Input validation analyzed |
| Exploitation | Aug 30, 2025 | Vulnerability Identified | Broken Authentication confirmed |
| Reporting | Aug 31, 2025 | Markdown + PDF Draft | Premium Enterprise Report completed |

---

## 📜 Scope & Engagement Details
**In-Scope:**  
- IP: `10.201.90.135`  
- Endpoints: `/register`, `/login`  

**Out-of-Scope:**  
- SQL Injection, XSS, DoS  

**Methodology:**  
Reconnaissance → Input Testing → Exploitation → Documentation → Remediation Recommendations  

**Frameworks & Standards:**  
- [OWASP Top 10 – A07: Identification & Authentication Failures](https://owasp.org/Top10/A07_Identification_and_Authentication_Failures/)  
- [CWE-287 – Improper Authentication](https://cwe.mitre.org/data/definitions/287.html)  
- [NIST SP 800-115 – Technical Guide to Security Testing](https://csrc.nist.gov/publications/detail/sp/800-115/final)
```0

---

## 📊 Findings Overview
| ID | Vulnerability | CVSS | Risk | CWE | Status | Evidence |
|----|---------------|------|------|-----|--------|----------|
| 01 | Broken Authentication / Re-Registration Logic Flaw | 6.5 | 🟨 Medium | CWE-287 | Confirmed | SS01–SS04 |

> **Professional Highlight:** Findings prioritized by CVSS + business impact

---

## 🔍 Detailed Vulnerability Analysis
**Title:** Broken Authentication / Re-Registration Logic Flaw  
**CWE:** 287 – Improper Authentication  
**CVSS:** 6.5 (Medium)  

**Attack Scenario:**  
- Register `" darren"` → duplicate validation bypassed  
- Unauthorized session creation → account takeover  

**Steps to Reproduce:**  
1. Access `http://10.201.90.135:8888/register`  
2. Attempt `darren` → rejected  
3. Register `" darren"` → account created  
4. Dashboard shows Darren’s account → exploit verified  
5. Repeat with `" arthur"`  

---

## 💡 Business Impact
- 🔓 **Account Takeover**  
- ⚠ **Sensitive Data Exposure**  
- 💸 **Reputation & Financial Risk**  
- 🛑 **Compliance Violation (OWASP/NIST)**  

---

## 🧾 Technical Evidence
Burp Suite – Intercepted Request  

📤 HTTP Request:  
http
POST /register HTTP/1.1
Host: 10.201.90.135:8888
Content-Type: application/x-www-form-urlencoded
Content-Length: 32

username=%20darren&password=test123


### Server Response

⚠ Session cookie allows unauthorized access

---

## 🛠 Tools & Methodology

| Tool                   | Version  | Purpose                             |
|------------------------|----------|-------------------------------------|
| Burp Suite Community   | 2025.8   | Intercept, replay, analyze requests|
| Firefox                | 129.0    | Manual testing, PoC validation      |
| Screenshot Utility     | N/A      | Evidence capture                    |
| Kali Linux Rolling     | 2025     | Testing environment                 |
| OWASP / NIST Guides    | Latest   | Reference & remediation guidance    |

---

## 🖼 Proof & Screenshots

1. Login Page – Initial Access  
   ![SS01 – Login Page](https://i.imgur.com/cOETJaN.jpeg)  

2. Re-Registration Attempt with Leading Space  
   ![SS02 – Re-Registration Attempt](https://i.imgur.com/OP9UwSN.jpeg)  

3. Burp Suite Intercept – Request Captured  
   ![SS03 – Burp Suite Intercept](https://i.imgur.com/Mbv3j8h.jpeg)  

4. Exploit Outcome / Attempt Proof  
   ![SS04 – Exploit Outcome](https://i.imgur.com/mW0tASV.jpeg)

> 🎨 Visual badge / summary:  
> ![Badge](https://i.imgur.com/B5Nkey5.jpeg)

(Screenshots to be attached in final version before GitHub/Fiverr upload)

---

## 🩹 Remediation Roadmap

### Authentication Enhancements:
- Normalize usernames (trim + lowercase)
- Enforce strict uniqueness checks
- Isolate sessions securely

### Technical Measures:
- Email verification
- Rate-limiting registration attempts
- Periodic pentesting & audits

### Governance & Training:
- Developer training on secure coding
- OWASP-compliant authentication workflow

---

## 🔍 Verification Steps

. Attempt " darren" registration → should be rejected
2. Validate username uniqueness (case-insensitive, trimmed)
3. Confirm original users remain unaffected
4. Monitor logs for suspicious attempts

---

## ⚠ Risk Matrix

| Likelihood / Impact | Low | Medium | High |
|----------------------|-----|--------|------|
| Low                 | 🟩  | 🟨     | 🟨   |
| Medium              | 🟨  | 🟧     | 🟥   |
| High                | 🟧  | 🟥     | 🟥   |

Overall Risk: 🟧 Medium → Immediate fix recommended.

---

## 📚 References


---

## 📎 Appendix

**Tools & Versions:**

- Burp Suite 2025.8
- Firefox 129.0
- Kali Linux Rolling 2025

**Notes:**

- Controlled lab environment
- No destructive payloads used

---

## 📑 Delivery Note

Hello 👋,

This Enterprise Premium Report is crafted for:

- **Freelancer / Fiverr Clients:** Polished, visually professional, ready for submission
- **Bug Bounty / Security Teams:** Complete CVSS/CWE mapping, PoC, raw HTTP requests

> Ensures professional presentation across GitHub, Fiverr, Bugcrowd, HackerOne

**Prepared by:**  
Asibur Rahaman  
🛡 Ethical Hacker & Cybersecurity Specialist
