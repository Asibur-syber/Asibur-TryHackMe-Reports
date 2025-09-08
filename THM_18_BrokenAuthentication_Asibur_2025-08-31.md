# 🛡 Web Application Penetration Test Report  

<p align="center">
  <img src="https://i.imgur.com/do3UY0q.jpeg" alt="Cybersecurity Portfolio Banner" width="100%">
</p>  

*Client:* TryHackMe – Room #18 (Broken Authentication) – Educational  
*Project:* Authentication & Logic Flaw Vulnerability Assessment  
*Date:* August 31, 2025  
*Version:* Final Premium Edition  
*Prepared by:* Asibur Rahaman  
*Title:* Ethical Hacker & Cybersecurity Specialist  
*Contact:* 📧 asib51639@gmail.com | 🌐 GitHub | 🔗 LinkedIn  

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
A penetration test on the target application (10.201.90.135:8888) identified a *Broken Authentication vulnerability* due to a *re-registration logic flaw*.  

- 🚨 *Severity:* Medium (CVSS 6.5 – CWE-287)  
- *CVSS Vector:* AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:L/A:N  
- Attackers can bypass duplicate username validation by adding leading spaces (e.g., " darren") and gain unauthorized access.  

This weakness indicates *improper input sanitization* in authentication workflows, leading to *account takeover risk*.  

---

## 📅 Assessment Timeline
| Activity                | Date        | Notes                         |
|--------------------------|------------|-------------------------------|
| Project Kickoff          | Aug 28, 2025 | Scope confirmed with client   |
| Recon & Input Testing    | Aug 29, 2025 | Registration logic reviewed   |
| Vulnerability Identified | Aug 30, 2025 | Broken Authentication flaw found |
| Report Preparation       | Aug 31, 2025 | Final Premium Edition drafted |

---

## 📜 Scope & Engagement Details
*In-Scope:*  
- IP: 10.201.90.135  
- Endpoints: /register, /login  

*Out-of-Scope:*  
- SQL Injection  
- Cross-Site Scripting (XSS)  
- Denial of Service (DoS)  

*Methodology:*  
Reconnaissance → Registration Input Testing → Exploitation → Documentation  

*Frameworks Referenced:*  
- OWASP Top 10 – A07: Identification & Authentication Failures  
- NIST SP 800-115  

---

## 📊 Findings Overview
| ID | Vulnerability | CVSS | Risk | CWE | Status | Evidence |
|----|---------------|------|------|-----|--------|----------|
| 01 | Broken Authentication / Re-Registration Logic Flaw | 6.5 | 🟨 Medium | CWE-287 | Confirmed | SS01–SS04 |

---

## 🔍 Detailed Vulnerability Analysis
*Vulnerability:* Broken Authentication / Re-Registration Logic Flaw  
*CWE ID:* 287 – Improper Authentication  
*CVSS:* 6.5 (Medium)  
*CVSS Vector:* AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:L/A:N  

*Attack Scenario:*  
- Malicious user registers " darren" (leading space).  
- Duplicate check bypassed → session created.  
- Unauthorized access to *Darren’s account* (flag captured).  

*Steps to Reproduce:*  
1. Navigate to http://10.201.90.135:8888/register  
2. Attempt to register darren → error: user exists  
3. Register " darren" → account successfully created  
4. Access dashboard → Darren’s account compromised  
5. Repeat with " arthur"  

---

## 💡 Business Impact
- 🔓 *Account Takeover* – Unauthorized access to existing user accounts  
- ⚠ *Data Exposure* – Sensitive information/flags leaked  
- 💸 *Financial & Reputational Damage* – Loss of customer trust  
- 🛑 *Compliance Risk* – OWASP/NIST standards violated  

---

## 🧾 Technical Evidence
*Burp Suite – Intercepted Request*  

📤 *HTTP Request:*  
```http
POST /register HTTP/1.1
Host: 10.201.90.135:8888
Content-Type: application/x-www-form-urlencoded
Content-Length: 32

username=%20darren&password=test123

### Server Response

⚠ *Impact:* Session cookie grants unauthorized access to Darren’s account.

---

## 🛠 Tools & Methodology

| Tool / Method     | Purpose                     |
|-------------------|-----------------------------|
| Web Browser       | Manual registration exploit |
| Burp Suite        | HTTP interception & replay  |
| Screenshot Utility| Visual documentation        |
| OWASP/NIST Guides | Reference for remediation   |

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


(Screenshots to be attached in final version before GitHub/Fiverr upload)

---

## 🩹 Remediation Roadmap

*Authentication Fixes:*
- Normalize usernames (trim whitespace, enforce lowercase)  
- Enforce strict uniqueness checks at registration  
- Isolate sessions per account securely  

*Technical Enhancements:*
- Implement email verification  
- Apply rate-limiting on registration attempts  
- Regular audit of user accounts  

*Governance:*
- Schedule periodic penetration testing  
- Train developers on secure authentication  
- Adopt OWASP-compliant secure coding practices  

---

## 🔍 Verification Steps

1. Attempt to register " darren" → must be rejected  
2. Ensure duplicate checks are case-insensitive & trimmed  
3. Validate original users (e.g., Darren, Arthur) remain intact  
4. Monitor logs for suspicious registration attempts  

---

## ⚠ Risk Matrix

| Likelihood / Impact | Low | Medium | High |
|----------------------|-----|--------|------|
| Low                 | 🟩  | 🟨     | 🟨   |
| Medium              | 🟨  | 🟧     | 🟥   |
| High                | 🟧  | 🟥     | 🟥   |

*Overall Risk: 🟧 Medium → Immediate fix recommended.*

---

## 📚 References

- OWASP Top 10 – A07: Identification & Authentication Failures  
- CWE-287 – Improper Authentication  
- NIST SP 800-115 – Technical Guide to Security Testing  
- TryHackMe – Broken Authentication  

---

## 📎 Appendix

*Tools & Versions:*
- Burp Suite Community 2025.8  
- Firefox 129.0  
- Kali Linux Rolling 2025  

*Notes:*
- Performed in controlled educational lab  
- No destructive payloads used  

---

## 📑 Delivery Note

Hello 👋,  

This *Premium Report* is crafted to serve both audiences:  

📌 *Freelancer/Fiverr Clients* → Clean, polished, easy-to-read, visual-ready.  
📌 *Bug Bounty / Security Teams* → CVSS/CWE mapping, HTTP request/response, technical PoC.  

It ensures you present yourself as a *premium cybersecurity professional* across all platforms (GitHub, Fiverr, Bugcrowd, HackerOne).  

Best regards,  
*Asibur Rahaman*  
🛡 Ethical Hacker & Cybersecurity Specialist
