# 🛡 Web Application Penetration Test Report

*Client:* TryHackMe – Injection (SQLi/XSS) Room (Educational)  
*Project:* XSS Vulnerabilities Assessment  
*Date:* August 20, 2025  
*Version:* 3.0 (HackerOne-Ready Edition)  
*Prepared by:* Asibur Rahaman  
*Title:* Ethical Hacker & Cybersecurity Specialist  
*Contact:* 📧 asib51639@gmail.com | 🌐 [GitHub](https://github.com/Asibur-syber) | 🔗 [LinkedIn](https://www.linkedin.com/)

---

## 📖 Table of Contents

1. [Executive Summary](#1-executive-summary)  
2. [Scope & Engagement Details](#2-scope--engagement-details)  
3. [Findings Overview](#3-findings-overview)  
4. [Detailed Vulnerability Analysis](#4-detailed-vulnerability-analysis)  
   - [Cross-Site Scripting (High)](#cross-site-scripting-high)  
5. [Business Impact](#5-business-impact)  
6. [Tools & Methodology](#6-tools--methodology)  
7. [Proof & Screenshots](#7-proof--screenshots)  
8. [Remediation Roadmap](#8-remediation-roadmap)  
9. [Risk Matrix](#9-risk-matrix)  
10. [References](#10-references)  
11. [Delivery Note](#11-delivery-note)

---

## ✨ Executive Summary

The penetration test conducted on the target web application at IP 10.201.72.172 identified *high-risk Cross-Site Scripting (XSS) vulnerabilities*.  
Exploitation could allow attackers to *execute arbitrary JavaScript in victim browsers*, leading to session hijacking, phishing, or malware distribution.

*Key Findings:*

- ⚡ *Cross-Site Scripting (XSS) – High* – CVSS 7.5, CWE-79  
  Execution of unauthorized JavaScript code in client browsers.

---

## 📜 Scope & Engagement Details

*Target in Scope:*  
- IP: 10.201.72.172  
- Web-based HTTP application

*Out-of-Scope:*  
- DoS attacks, brute-force attacks, third-party services

*Testing Methodology:*  
Reconnaissance → Vulnerability Discovery → Exploitation → Proof of Concept → Documentation

*Frameworks Used:*  
- [OWASP WSTG v4.2](https://owasp.org/www-project-web-security-testing-guide/)  
- [NIST SP 800-115](https://csrc.nist.gov/publications/detail/sp/800-115/final)

*Limitations:*  
- Non-destructive testing only

---

## 📊 Findings Overview

| ID  | Vulnerability           | CVSS Score | Risk Level | CWE ID | Status    | Evidence         |
|-----|------------------------|------------|------------|--------|-----------|-----------------|
| 01  | Cross-Site Scripting     | 7.5        | 🟧 High    | CWE-79 | Confirmed | SS01, SS02, SS03|

---

## 🔍 Detailed Vulnerability Analysis

### 1️⃣ Cross-Site Scripting (High)

- *CWE ID:* [CWE-79](https://cwe.mitre.org/data/definitions/79.html) – Improper Neutralization of Input During Web Page Generation  
- *CVSS Vector:* AV:N/AC:L/PR:N/UI:R/S:C/C:L/I:L/A:N → Score: 7.5 (High)

*Attack Scenario:*  
Payload <script>alert('XSS')</script> executes in victim browsers, allowing attackers to *steal session cookies, perform phishing, or inject malware*.

*Steps to Reproduce:*  
1. Enter <script>alert('XSS')</script> in vulnerable input fields (SS01)  
2. Observe the JavaScript alert popup (SS02)  
3. Inspect the DOM for unsafe innerHTML sinks (SS03)

*Technical Insights:*  
- Application fails to *sanitize or encode user input*  
- DOM-based sinks allow *arbitrary script execution*  
- Can escalate to *session hijacking or client-side phishing*  

---

## 💡 Business Impact

- 🕵 *XSS* → Session hijacking, credential theft, phishing campaigns  
- ⚠ *Regulatory Risk* → GDPR, HIPAA, PCI-DSS violations  
- 💸 *Reputation & Financial Loss* → Customer trust erosion, incident response costs  

---

## 🛠 Tools & Methodology

- *Burp Suite* → Manual payload injection  
- *Firefox DevTools* → DOM inspection  
- *Manual JavaScript Payloads* → Alert popups & session testing  
- *Browser testing on multiple clients* → Verification

---

## 🖼 Proof & Screenshots

1. XSS Vulnerable Input Field  
   ![Screenshot 1 – XSS Vulnerable Input Field](https://i.imgur.com/Lkooeyq.jpeg)  
   **Caption:** The input field on the target page before payload injection, showing form context and URL.

2. JavaScript Alert Popup (Proof of Execution)  
   ![Screenshot 2 – JavaScript Alert Proof](https://i.imgur.com/yZ3zVZk.jpeg)  
   **Caption:** Successful execution of the injected payload, demonstrated by the JavaScript `alert()` popup.

> 🎨 Visual badge / summary:  
> ![Badge](https://i.imgur.com/8JnJMss.jpeg)

---

## 🩹 Strategic Remediation Roadmap

### 🛡 XSS Fixes
- Apply *context-aware output encoding*  
- Implement *Content Security Policy (CSP)* headers  
- Validate and sanitize *all user inputs*  
- Avoid unsafe DOM manipulation with innerHTML

### 📊 Governance
- Conduct *regular penetration tests & code reviews*  
- Provide *secure coding training* for developers  
- Deploy *WAF & continuous monitoring*

---

## ⚠ Risk Matrix

| Likelihood ↓ \ Impact → | Low | Medium | High |
|-------------------------|-----|--------|------|
| Low                     | 🟩   | 🟨      | 🟧    |
| Medium                  | 🟨   | 🟧      | 🟥    |
| High                    | 🟧   | 🟥      | 🟥    |

*Overall Rating:* 🟧 High

---

## 📚 References

- [OWASP Web Security Testing Guide (WSTG)](https://owasp.org/www-project-web-security-testing-guide/)  
- [OWASP Top 10 – XSS](https://owasp.org/Top10/A07_2021-Cross_Site_Scripting/)  
- [MITRE CWE-79: Cross-Site Scripting](https://cwe.mitre.org/data/definitions/79.html)  
- [NIST SP 800-115](https://csrc.nist.gov/publications/detail/sp/800-115/final)  
- [CVSS v3.1 Calculator](https://www.first.org/cvss/calculator/3.1)

---

## 📑 Delivery Note (Freelance + Bug Bounty)

Hello 👋,  

This report provides a *comprehensive XSS assessment* with CWE references, CVSS scoring, exploit scenarios, and remediation steps.

*🚀 Included:*  
- ✅ Executive summary for business stakeholders  
- ✅ CWE-mapped technical findings for security teams  
- ✅ Screenshots & reproduction steps  
- ✅ CVSS scoring & risk justification  
- ✅ Strategic remediation roadmap  

💡 Suitable for *Fiverr/Upwork freelance delivery, LinkedIn portfolio showcase, and HackerOne/Bugcrowd submissions*

Best regards,  
*Asibur Rahaman*  
🛡 Ethical Hacker & Cybersecurity Specialist
