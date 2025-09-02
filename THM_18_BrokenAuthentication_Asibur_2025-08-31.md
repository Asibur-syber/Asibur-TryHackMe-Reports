# 🛡 Web Application Penetration Test Report

Client: TryHackMe – Room #18 (Broken Authentication) – Educational  
Project: Authentication & Logic Flaw Vulnerability Assessment  
Date: August 31, 2025  
Version: 2.0 (HackerOne-Ready Edition)  
Prepared by: Asibur Rahaman  
Title: Ethical Hacker & Cybersecurity Specialist  
Contact: 📧 asib51639@gmail.com | 🌐 [GitHub](https://github.com/Asibur-syber) | 🔗 [LinkedIn](https://www.linkedin.com/)  

---

## 📖 Table of Contents

1. [Executive Summary](#-executive-summary)  
2. [Scope & Engagement Details](#-scope--engagement-details)  
3. [Findings Overview](#-findings-overview)  
4. [Detailed Vulnerability Analysis](#-detailed-vulnerability-analysis)  
   - Broken Authentication / Re-Registration Logic Flaw (Severity 2)  
5. [Business Impact](#-business-impact)  
6. [Tools & Methodology](#-tools--methodology)  
7. [Proof & Screenshots](#-proof--screenshots)  
8. [Remediation Roadmap](#-remediation-roadmap)  
9. [Risk Matrix](#-risk-matrix)  
10. [References](#-references)  
11. [Delivery Note](#-delivery-note)  

---

## ✨ Executive Summary

The penetration test conducted on the target web application (10.201.90.135:8888) identified a *broken authentication vulnerability due to re-registration logic flaw*.  
Exploitation of this flaw allowed unauthorized access to existing user accounts (darren and optionally arthur) without valid credentials.  

*Key Findings:*  
- 🚨 Broken Authentication / Logic Flaw (Severity 2) – CVSS 6.5, CWE-287  
  Application fails to properly sanitize user input for usernames, allowing a malicious user to gain access via slight modification of existing usernames.  

This issue demonstrates how attackers can exploit minor developer mistakes to access privileged accounts.  

---

## 📜 Scope & Engagement Details

Target in Scope:  
- IP: 10.201.90.135  
- Web registration & login forms (/register, /login)  

Out-of-Scope:  
- SQL Injection, XSS, DoS attacks  

Testing Methodology:  
Reconnaissance → Registration Input Testing → Exploit Logic Flaw → Capture Flag → Documentation  

Frameworks Used:  
- [OWASP Top 10 – A07: Identification and Authentication Failures](https://owasp.org/Top10/A07_Identification_and_Authentication_Failures/)  
- [NIST SP 800-115](https://csrc.nist.gov/publications/detail/sp/800-115/final)  

Limitations:  
- Non-destructive educational assessment only  

---

## 📊 Findings Overview

| ID  | Vulnerability                        | CVSS Score | Risk Level | CWE ID | Status    | Evidence |
|-----|--------------------------------------|------------|------------|--------|-----------|----------|
| 01  | Broken Authentication / Re-Registration Logic Flaw | 6.5        | 🟨 Medium | CWE-287 | Confirmed | SS01, SS02, SS03, SS04 |

---

## 🔍 Detailed Vulnerability Analysis

### 1️⃣ Broken Authentication / Re-Registration Logic Flaw – Medium

- CWE ID: [CWE-287](https://cwe.mitre.org/data/definitions/287.html) – Improper Authentication  
- CVSS Vector: AV:N/AC:L/PR:N/UI:R/S:U/C:L/I:L/A:N → Score: 6.5 (Medium)  

*Attack Scenario:*  
The registration mechanism allows creating a new user with a slight modification (leading space) of an existing username.  
This results in a new user session having the *same privileges as the original user*, exposing all user-specific content including flags.  

*Steps to Reproduce:*  

1. Access registration page: http://10.201.90.135:8888/register  
2. Attempt to register existing user: darren → observe “user already exists”  
3. Re-register user with *leading space*: " darren" → submit form  
4. Session created → access darren’s account content  
5. Capture the flag → store screenshot (SS04)  
6. Optional: Repeat with " arthur" to capture Arthur’s flag  

*No CLI or Hydra commands required*; purely browser-based logic flaw exploit.  

---

## 💡 Business Impact

Broken authentication via re-registration exposes:

- 🔓 *Unauthorized Access*: Attackers gain access to other user accounts  
- ⚠ *Sensitive Data Exposure*: All user-specific content visible  
- 💸 *Potential Reputational Damage*: Demonstrates poor authentication hygiene  
- 🛑 *Compliance Risks*: Violates secure authentication standards (OWASP A07, CWE-287)  

---

## 🛠 Tools & Methodology

| Tool / Method      | Purpose                                        | Role in Testing |
|-------------------|-----------------------------------------------|----------------|
| **Web Browser**    | Manual interaction with registration/login   | Exploit re-registration logic |
| **Burp Suite**     | Intercept & inspect HTTP requests/responses | Capture request data, verify logic flaw |
| **Screenshot Tool**| Document evidence                             | Windows: `PrtSc` / Linux: `gnome-screenshot -a` / Mac: `Cmd+Shift+4` |
| **OWASP Guidance** | Reference for authentication best practices | Remediation suggestions |

**No external attack tools (Hydra/Patator) needed**

---

## 🖼 Proof & Screenshots

1. *Login Page – Initial Access*  
   ![SS01 – Login Page](https://i.imgur.com/cOETJaN.jpeg)  

2. *Re-Registration Attempt with Leading Space*  
   ![SS02 – Re-Registration Attempt](https://i.imgur.com/OP9UwSN.jpeg)  

3. *Burp Suite Intercept – Request Captured*  
   ![SS03 – Burp Suite Intercept](https://i.imgur.com/Mbv3j8h.jpeg)  

4. *Exploit Outcome / Attempt Proof*  
   ![SS04 – Exploit Outcome](https://i.imgur.com/mW0tASV.jpeg)

> 🎨 Visual badge / summary:  
> ![Badge](https://i.imgur.com/B5Nkey5.jpeg)

---

## 🩹 Remediation Roadmap

### 🔐 Authentication Hardening
- Validate & sanitize username input; strip leading/trailing spaces  
- Prevent duplicate accounts via normalization checks  
- Enforce strict session management & account verification  

### 📊 Technical Fixes
- Implement *email verification* before account creation  
- Limit registration attempts from same IP per hour  
- Regular audit for existing account anomalies  

### 🛡 Governance
- Conduct periodic penetration tests  
- Developer security training focused on authentication & session management  
- Implement *OWASP-compliant authentication* controls  

---

## ⚠ Risk Matrix

| Likelihood ↓ / Impact → | Low | Medium | High |
|--------------------------|-----|--------|------|
| *Low*                 | 🟩 Insignificant | 🟨 Minor | 🟨 Noticeable |
| *Medium*              | 🟨 Acceptable | 🟧 Serious | 🟥 Major |
| *High*                | 🟧 Significant | 🟥 Critical | 🟥 Catastrophic |

*Overall Risk: 🟧 Medium*  
Immediate remediation recommended to prevent account compromise.  

---

## 📚 References

- [OWASP Top 10 – A07: Identification and Authentication Failures](https://owasp.org/Top10/A07_Identification_and_Authentication_Failures/)  
- [CWE-287: Improper Authentication](https://cwe.mitre.org/data/definitions/287.html)  
- [TryHackMe – Broken Authentication Room](https://tryhackme.com/room/brokenauth)  
- [NIST SP 800-115 – Technical Guide to Information Security Testing](https://csrc.nist.gov/publications/detail/sp/800-115/final)  

---

## 📑 Delivery Note (Freelance + Bug Bounty)

Hello 👋,  

This report provides a *comprehensive Broken Authentication practical assessment, fully **HackerOne-ready*, aligned with industry standards and formatted for professional delivery.  

🚀 *Deliverables Included:*  
- ✅ Executive summary for decision-makers  
- ✅ CVSS & CWE-mapped technical findings for engineers  
- ✅ Proof-of-Concept with screenshots & flag evidence  
- ✅ Detailed remediation roadmap & risk matrix  
- ✅ Documentation suitable for *Freelance delivery, GitHub portfolio, and Bug Bounty submissions*  

Best regards,  
*Asibur Rahaman*  
🛡 Ethical Hacker & Cybersecurity Specialist
