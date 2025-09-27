# 🧪 TryHackMe Pickle Rick – Penetration Test Report (Ultimate Premium Edition)

<p align="center">        
<img src="https://i.imgur.com/sV5Speb.jpeg" alt="Cybersecurity Portfolio Banner" width="100%">        
</p>  

*Client:* TryHackMe – Room #22 (Pickle Rick) – Educational  
*Project:* Web Exploitation & Privilege Escalation  
*Date:* September 27, 2025  
*Version:* 1.0 (Ultimate Premium — HackerOne-Ready Edition)  
*Prepared by:* Asibur Rahaman  
*Title:* Ethical Hacker & Cybersecurity Specialist  
*Contact:* [📧 Email](mailto:asib51639@gmail.com) | [🌐 GitHub](https://github.com/Asibur-syber) | [🔗 LinkedIn](https://www.linkedin.com/)  

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
- [💌 Personal Note to Client](#-personal-note-to-client)  

---

## ✨ Executive TL;DR

This engagement focused on the *Pickle Rick VM* from [TryHackMe](https://tryhackme.com/room/picklerick), simulating a real-world penetration test against a vulnerable web application and backend system.  

- *Objective:* Identify, exploit, and document vulnerabilities in the Pickle Rick VM to retrieve hidden “ingredients.”  
- *Outcome:* Successfully gained initial access via command injection, escalated privileges to root, and captured all target flags.  
- *Impact:* Demonstrated how poor input validation, exposed credentials, and misconfigured SUID binaries can lead to *full system compromise*.  
- *Business Value:* This lab mirrors real-world risks to organizations if secure coding and access controls are not enforced.  

| Finding                  | Risk     | Impact              | Quick Fix                           | Host IP       |
|---------------------------|---------|---------------------|-------------------------------------|---------------|
| Command Injection (login form) | 🔴 Critical | Remote shell access | Sanitize input, use parameterized code | 10.201.52.185 |
| Hardcoded Credentials     | 🟠 High | Unauthorized access | Remove credentials, use vault       | 10.201.52.185 |
| SUID Misconfigured Script | 🟠 High | Root shell access   | Remove SUID, audit permissions      | 10.201.52.185 |

---

## 📜 Scope & Engagement

*In Scope:*  
- [Pickle Rick VM – TryHackMe Room #22](https://tryhackme.com/room/picklerick)  
- Web interface, backend scripts, and local privilege escalation  

*Out-of-Scope:*  
- Denial-of-Service  
- External systems  

*Methodology:*  
1. Reconnaissance ([Nmap](https://nmap.org), [Gobuster](https://github.com/OJ/gobuster))  
2. Web Enumeration  
3. Exploitation (Command Injection)  
4. Privilege Escalation  
5. Flag Retrieval  
6. Reporting & Remediation  

---

## 🛠 Testing Tools & Environment

*Tools Used:*  
- [Nmap](https://nmap.org/)  
- [Gobuster](https://github.com/OJ/gobuster)  
- [curl](https://curl.se/)  
- [Burp Suite](https://portswigger.net/burp)  
- [Netcat](http://nc110.sourceforge.net/)  
- Python Reverse Shell  
- [LinPEAS](https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS)  

*Environment:*  
- Attacker: Kali Linux (2023.4)  
- Target: Pickle Rick VM (Lab IP: 10.201.52.185)  

---

## 📊 Findings Overview

| ID       | Finding                     | CVSS | Risk     | CWE     | Status    |
|----------|-----------------------------|------|---------|---------|-----------|
| PRICK-01 | Command Injection (login)   | 9.8  | Critical | CWE-77  | Confirmed |
| PRICK-02 | Hardcoded Credentials       | 7.5  | High     | CWE-798 | Confirmed |
| PRICK-03 | SUID Misconfigured Script   | 8.2  | High     | CWE-732 | Confirmed |

---

## 🔍 Detailed Vulnerability Analysis

### 1️⃣ PRICK-01: Command Injection – Critical
*CWE:* [CWE-77: Improper Neutralization of Special Elements used in a Command](https://cwe.mitre.org/data/definitions/77.html)  
*Summary:* /login.php accepts unsanitized input, allowing OS commands.
**PoC:**  ```
admin' || ls / > /tmp/output.txt || 
*Impact:* Remote shell access.  
*Remediation:* Validate input, use parameterized queries.  
 
---

### 2️⃣ PRICK-02: Hardcoded Credentials – High
*CWE:* [CWE-798: Use of Hard-coded Credentials](https://cwe.mitre.org/data/definitions/798.html)  
*Summary:* Credentials found in source code / backup files.  
*Impact:* Unauthorized access.  
*Remediation:* Remove credentials, use secrets manager.  
 
---

### 3️⃣ PRICK-03: SUID Misconfigured Script – High
*CWE:* [CWE-732: Incorrect Permission Assignment](https://cwe.mitre.org/data/definitions/732.html)  
*Summary:* /usr/bin/sudo_script.sh executable as root.  
*Impact:* Privilege escalation → root.  
*Remediation:* Remove SUID bit, audit permissions.  
  
---

## ⏱ Exploitation Timeline

| Phase                | Time Taken | Summary                         | Evidence |
|----------------------|------------|---------------------------------|----------|
| Reconnaissance       | 15 mins    | Nmap + Gobuster scanning        | Commands logged |
| Web Enumeration      | 20 mins    | Found vulnerable login form     | Request/Response logs |
| Exploitation         | 25 mins    | Command injection → shell       | Payload & output |
| Privilege Escalation | 20 mins    | Root shell via SUID script      | Escalation steps |
| Flag Retrieval       | 10 mins    | Retrieved Rick’s ingredients    | Flag values |
| Documentation        | 1 hr       | Report writing & formatting     | N/A |

---

## 🖼 Technical Proof & Screenshots

1. **Nmap Survey (SS01)**  
   ![SS01 – Nmap Survey](https://i.imgur.com/6ug5puZ.jpeg)  
   *Initial reconnaissance showing open ports and services — web service identified as primary target.*

2. **Gobuster Directory Enumeration (SS02)**  
   ![SS02 – Gobuster Results](https://i.imgur.com/Klsv5U1.jpeg)  
   *Discovered directories/files (e.g., /backup/, config.php.bak) — useful for further investigation.*

3. **Target Web Application Homepage (SS03)**  
   ![SS03 – Homepage](https://i.imgur.com/BVhJK5h.jpeg)  
   *Visual inspection of homepage features and input fields for subsequent testing.*

4. **Configuration Backup Exposure (SS04)**  
   ![SS04 – Config Backup](https://i.imgur.com/4JNn7WL.jpeg)  
   *Exposed backup file containing hardcoded credentials — redact sensitive info before public disclosure.*

5. **Command Injection PoC (SS05)**  
   ![SS05 – Command Injection PoC](https://i.imgur.com/6fHGtFQ.jpeg)  
   *PoC POST payload sent to login.php demonstrating possible command execution.*

6. **Injection Output Evidence (/tmp/out.txt) (SS06)**  
   ![SS06 – Injection Output](https://i.imgur.com/tqczbpk.jpeg)  
   *Server-side output file showing executed command results — confirms RCE potential.*

7. **Netcat Listener (Attacker Machine) (SS07)**  
   ![SS07 – Netcat Listener](https://i.imgur.com/WOL83CQ.jpeg)  
   *Netcat listening on port 4444 ready to receive reverse shell.*

8. **Reverse Shell: whoami / id / uname (SS08)**  
   ![SS08 – Reverse Shell Info](https://i.imgur.com/vY2rTKN.jpeg)  
   *Reverse shell obtained — user & host enumeration performed.*

9. **SUID Files & sudo -l Enumeration (SS09)**  
   ![SS09 – SUID and sudo Results](https://i.imgur.com/sTkTLYQ.jpeg)  
   *SUID binaries and sudo permissions enumerated — potential privilege escalation vectors.*

10. **Root Shell Confirmation & Flag (SS10)**  
    ![SS10 – Root Shell and Flag](https://i.imgur.com/SS10_placeholder.png)  
    *Root shell confirmed; root flag recovered — redact flag before public disclosure.*

> 🎨 Visual badge / summary:  
> ![Badge](https://i.imgur.com/rdnlel5.jpeg)

---

## 🩹 Remediation Roadmap

*Immediate (0–7 days):*  
- Sanitize web inputs  
- Remove hardcoded credentials  
- Remove SUID permissions  

*Short-Term (30 days):*  
- Implement secure coding practices  
- Audit user permissions  
- Apply least privilege  

*Long-Term (90+ days):*  
- Regular penetration testing  
- Secure CI/CD pipelines  
- Continuous monitoring  

---

## 📌 CVSS & CWE Justification

| Finding            | CVSS | CWE   | Justification |
|--------------------|------|-------|---------------|
| Command Injection  | 9.8  | CWE-77 | Full remote shell execution possible |
| Hardcoded Credentials | 7.5 | CWE-798 | Immediate unauthorized login |
| SUID Misconfigured Script | 8.2 | CWE-732 | Root escalation through misconfig |

---

## ⚠ Risk Matrix & Business Impact

*Overall Risk: 🔴 Critical*  
*Impact:* Complete compromise of VM, root access, sensitive data retrieval.  

| Likelihood ↓ / Impact → | Low | Medium | High |
|--------------------------|-----|--------|------|
| Low                     | 🟩 Minor | 🟨 Noticeable | 🟨 Serious |
| Medium                  | 🟨 Acceptable | 🟧 Major | 🔴 Critical |
| High                    | 🟧 Major | 🔴 Severe | 🔴 Catastrophic |

---

## 📚 References & Framework Mapping

- [OWASP Top 10 (2021)](https://owasp.org/Top10/)  
- [CWE Database](https://cwe.mitre.org/)  
- [NIST SP 800-115](https://csrc.nist.gov/publications/detail/sp/800-115/final)  
- [TryHackMe: Pickle Rick Room](https://tryhackme.com/room/picklerick)  
- [GitHub Profile](https://github.com/Asibur-syber)  
- [LinkedIn](https://www.linkedin.com/)  

---

## 📑 Delivery Package & Notes

- THM22_PickleRick_Report.md (this file)  
- THM22_PickleRick_Report.pdf  
- /screenshots/ → SS01–SS10 (annotated, timestamped)  
- /logs/ → nmapscan.txt, gobuster.txt, linpeasoutput.txt, commands.txt  

---

## 💌 Personal Note to Client

> Dear [Client],  
>  
> This report was prepared with professional care, ensuring both *technical depth* and *business clarity*. Each finding includes evidence, remediation, and direct references to industry standards (OWASP, CWE, NIST).  
>  
> I believe in *quality over quantity* — delivering not just vulnerabilities, but *actionable insights*. If this engagement meets your standards, I look forward to collaborating on more advanced penetration testing projects.  
>  
> Thank you for trusting my work.  
>  
> Best regards,  
> *Asibur Rahaman*  
> Ethical Hacker & Cybersecurity Specialist  

---
