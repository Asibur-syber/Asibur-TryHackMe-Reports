# 🛡 Web Application Penetration Test Report

*Client:* TryHackMe – Room #17 (Brute Force) – Educational  
*Project:* Authentication & Brute Force Vulnerability Assessment  
*Date:* August 26, 2025  
*Version:* 2.0 (HackerOne-Ready Edition)  
*Prepared by:* Asibur Rahaman  
*Title:* Ethical Hacker & Cybersecurity Specialist  
*Contact:* 📧 asib51639@gmail.com | 🌐 [GitHub](https://github.com/Asibur-syber) | 🔗 [LinkedIn](https://www.linkedin.com/)  

---

## 📖 Table of Contents

1. [Executive Summary](#-executive-summary)  
2. [Scope & Engagement Details](#-scope--engagement-details)  
3. [Findings Overview](#-findings-overview)  
4. [Detailed Vulnerability Analysis](#-detailed-vulnerability-analysis)  
   - Brute Force Attack (High)  
5. [Business Impact](#-business-impact)  
6. [Tools & Methodology](#-tools--methodology)  
7. [Proof & Screenshots](#-proof--screenshots)  
8. [Remediation Roadmap](#-remediation-roadmap)  
9. [Risk Matrix](#-risk-matrix)  
10. [References](#-references)  
11. [Delivery Note](#-delivery-note)  

---

## ✨ Executive Summary

The penetration test conducted on the target web application (`10.201.56.109`) identified **critical brute force authentication vulnerabilities**.  
Exploitation of this weakness allowed bypassing authentication and accessing restricted areas.  

**Key Findings:**  
- 🚨 *Brute Force Attack (High)* – CVSS 8.5, CWE-307  
  Weak login security without rate-limiting, account lockout, or CAPTCHA.  

This issue demonstrates how attackers can systematically guess credentials using automated tools such as Hydra, Burp Intruder, and Patator.  

---

## 📜 Scope & Engagement Details

*Target in Scope:*  
- IP: `10.201.56.109`  
- Web login form (`/login`)  

*Out-of-Scope:*  
- DoS attacks, third-party integrations  

*Testing Methodology:*  
Reconnaissance → Enumeration → Exploitation (Brute Force) → Proof of Concept → Documentation  

*Frameworks Used:*  
- [OWASP WSTG v4.2](https://owasp.org/www-project-web-security-testing-guide/)  
- [NIST SP 800-115](https://csrc.nist.gov/publications/detail/sp/800-115/final)  

*Limitations:*  
- Non-destructive educational assessment only  

---

## 📊 Findings Overview

| ID  | Vulnerability         | CVSS Score | Risk Level | CWE ID | Status    | Evidence |
|-----|-----------------------|------------|------------|--------|-----------|----------|
| 01  | Brute Force Login     | 8.5        | 🟧 High    | CWE-307| Confirmed | SS03, SS04 |

---

## 🔍 Detailed Vulnerability Analysis

### 1️⃣ Brute Force Authentication – High

- *CWE ID:* [CWE-307](https://cwe.mitre.org/data/definitions/307.html) – Improper Restriction of Excessive Authentication Attempts  
- *CVSS Vector:* AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:L → Score: 8.5 (High)  

**Attack Scenario:**  
The login endpoint failed to implement brute force protections. By using a password list, an attacker could discover valid credentials.  

**Steps to Reproduce:**  
1. Access login page (`http://10.201.56.109/login`).  
2. Intercept login request with Burp Suite (SS02).  
3. Send request to **Burp Intruder** → configure payload positions for password field.  
4. Load password list: `/home/kali/Downloads/passwords_clean.txt`.  
5. Observe success response (different length/redirect) in Intruder results (SS04).  
6. Validate with **Hydra**: hydra -l admin -P /home/kali/Downloads/passwords_clean.txt 10.201.56.109 http-post-form "/login:username=^USER^&password=^PASS^:Invalid"
7. Confirm with Patator and ZAP fuzzing module for alternative validation.
8. Successfully logged into restricted area with discovered password.

---

## 💡 Business Impact

The identified brute force vulnerability poses **serious security implications** for the target application and its stakeholders:

- 🔓 **Unauthorized Access**  
  Attackers can systematically guess valid credentials, leading to full compromise of administrative accounts.  

- ⚠ **Sensitive Data Exposure**  
  Once authenticated, attackers can access confidential data, customer records, or system configurations.  

- 💸 **Financial & Reputational Loss**  
  Compromise of the application may result in brand damage, customer distrust, legal disputes, and monetary losses.  

- 🛑 **Regulatory & Compliance Risks**  
  Non-compliance with **GDPR**, **PCI-DSS**, **HIPAA**, and **OWASP ASVS** may result in fines, litigation, and sanctions.  

- 🚨 **Attack Surface Expansion**  
  Compromised accounts may act as a pivot point for **lateral movement**, enabling further exploitation (SQL injection, privilege escalation, or data exfiltration).  

---

## 🛠 Tools & Methodology

The following tools and frameworks were utilized to validate and confirm the brute force vulnerability:

| Tool             | Purpose                                    | Role in Testing |
|------------------|--------------------------------------------|-----------------|
| **Burp Suite Intruder** | Automated brute forcing on login form | Configured payload positions & validated successful responses |
| **Hydra**        | High-speed CLI brute forcing               | Confirmed credentials via HTTP POST requests |
| **Patator**      | Modular brute forcing framework            | Secondary validation of login endpoints |
| **OWASP ZAP**    | Web application security testing & fuzzing | Analyzed response differences and login behavior |
| **Firefox Browser** | Manual interaction and validation        | Verified discovered credentials in a real login scenario |

**Password List Used:**  
`/home/kali/Downloads/passwords_clean.txt`

---

## 🖼 Proof & Screenshots

1. *Target Login Page Opened in Browser*  
   ![Screenshot 1 – Target Login Page](https://i.imgur.com/V4wrbcN.jpeg)  

2. *Burp Suite Intercepted Login Request*  
   ![Screenshot 2 – Burp Suite Intercepted Request](https://i.imgur.com/wKdeeUC.jpeg)  

3. *Burp Intruder Payload Setup (Password Field Selected & Wordlist Loaded)*  
   ![Screenshot 3 – Burp Intruder Payload Setup](https://i.imgur.com/WfJMi9J.jpeg)  

4. *Hydra CLI Execution – Valid Credential Found*  
   ![Screenshot 4 – Hydra CLI Valid Credential](https://i.imgur.com/BgXZmue.jpeg)  

5. *Patator Execution – Brute Force Output*  
   ![Screenshot 5 – Patator Brute Force Result](https://i.imgur.com/bjd9ag4.jpeg)  

6. *Burp Intruder Attack Result Table (Status/Length Difference)*  
   ![Screenshot 6 – Burp Intruder Attack Results](https://i.imgur.com/rckgWPS.jpeg)  

7. *Successful Login to Admin Dashboard (Post Brute Force)*  
   ![Screenshot 7 – Successful Login Dashboard](https://i.imgur.com/dPtB9YY.jpeg)  

8. *Password List File Preview (Wordlist Used for Attack)*  
   ![Screenshot 8 – Password List Preview](https://i.imgur.com/zTgz76Z.jpeg)

> 🎨 Visual badge / summary:  
> ![Badge](https://i.imgur.com/GUgUmCK.jpeg)

---

## 🩹 Remediation Roadmap

### 🔐 Authentication Hardening
- Implement **account lockout** after 5–10 failed login attempts.  
- Add **CAPTCHA/reCAPTCHA** to mitigate automated login attempts.  
- Enforce **Multi-Factor Authentication (MFA)** for sensitive accounts.  

### 📊 Technical Fixes
- Enforce **minimum password complexity** (12+ characters, symbols, mixed case).  
- Configure **rate limiting** (e.g., 5 requests/minute per IP).  
- Enable **IP reputation-based blocking** for brute force traffic.  
- Ensure **audit logging** of failed login attempts and unusual login behavior.  

### 🛡 Governance
- Conduct **periodic penetration testing** and red team exercises.  
- Provide **developer security training** on authentication & session management.  
- Deploy a **Web Application Firewall (WAF)** with brute force protection rules.  
- Establish an **incident response playbook** for brute force attacks.  

---

## ⚠ Risk Matrix

| Likelihood ↓ / Impact → | Low | Medium | High |
|--------------------------|-----|--------|------|
| **Low**                 | 🟩 Insignificant | 🟨 Minor | 🟧 Noticeable |
| **Medium**              | 🟨 Acceptable | 🟧 Serious | 🟥 Major |
| **High**                | 🟧 Significant | 🟥 Critical | 🟥 Catastrophic |

**Overall Risk: 🟥 High**  
The vulnerability must be addressed **immediately** to prevent account compromise and unauthorized system access.  

---

## 📚 References

- [OWASP Top 10 – A07: Identification and Authentication Failures](https://owasp.org/Top10/A07_Identification_and_Authentication_Failures/)  
- [CWE-307: Improper Restriction of Excessive Authentication Attempts](https://cwe.mitre.org/data/definitions/307.html)  
- [Hydra GitHub Repository](https://github.com/vanhauser-thc/thc-hydra)  
- [Patator GitHub Repository](https://github.com/lanjelot/patator)  
- [OWASP ZAP Project](https://www.zaproxy.org/)  
- [NIST SP 800-115 – Technical Guide to Information Security Testing](https://csrc.nist.gov/publications/detail/sp/800-115/final)  
- [CVSS v3.1 Calculator](https://www.first.org/cvss/calculator/3.1)  

---

## 📑 Delivery Note (Freelance + Bug Bounty)

Hello 👋,  

This report provides a **comprehensive brute force penetration test assessment**, aligned with industry standards and HackerOne-ready formatting.  

🚀 **Deliverables Included:**  
- ✅ Executive summary for decision-makers  
- ✅ CVSS & CWE-mapped technical findings for engineers  
- ✅ Proof-of-Concept with screenshots & password list evidence  
- ✅ Detailed remediation roadmap & risk matrix  
- ✅ Documentation suitable for **Freelance delivery, GitHub portfolio, and Bug Bounty submissions**  

Best regards,  
**Asibur Rahaman**  
🛡 Ethical Hacker & Cybersecurity Specialist  

---
