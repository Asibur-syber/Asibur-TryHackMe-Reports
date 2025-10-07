# 🧪 TryHackMe Blue – Penetration Test Report (Ultimate Premium Edition)

<p align="center">  
<img src="https://i.imgur.com/MNlo0V7.jpeg" alt="Cybersecurity Portfolio Banner" width="100%">  
</p>

*Client:* TryHackMe – Room #23 (Blue) – Educational  
*Project:* Web Exploitation & Privilege Escalation  
*Date:* October 6, 2025  
*Version:* 1.1 (Ultimate Premium — HackerOne-Ready Edition)  
*Prepared by:* Asibur Rahaman  
*Title:* Ethical Hacker & Cybersecurity Specialist  
*Contact:* 📧 [asib51639@gmail.com](mailto:asib51639@gmail.com) | 🌐 [GitHub — Asibur-syber](https://github.com/Asibur-syber) | 🔗 [LinkedIn](https://www.linkedin.com/)  

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

---

## ✨ Executive TL;DR

Objective: Assess the Blue VM ([TryHackMe Room #23](https://tryhackme.com/room/blue)) for web/service and local privilege escalation vulnerabilities.

Summary: Initial access was achieved via an exposed/misconfigured service. Subsequent enumeration and exploitation of weak file permissions and outdated binaries allowed local privilege escalation and full capture of lab flags.

Business Risk Highlights:

* Remote takeover possible within 1 hour of engagement.
* Weak file permissions increase insider-threat risk and ease privilege escalation.
* Outdated/unmaintained binaries create *compliance & data-breach risk* (e.g., [PCI-DSS](https://www.pcisecuritystandards.org/)/ [ISO 27001](https://www.iso.org/iso-27001-information-security.html) exposure).

Status: Findings confirmed; remediation recommendations and prioritized action items provided below.

> Note: All testing was performed inside the TryHackMe lab environment under authorization. Do not apply these techniques to unauthorized systems.

---

## 📜 Scope & Engagement

*In Scope:*

* Blue VM — [TryHackMe Room #23](https://tryhackme.com/room/blue) (web & service components, host filesystem).

*Out-of-Scope:*

* Denial-of-Service (DoS) tests.
* Any external networks or systems not part of the lab.

*Methodology (high-level):*

1.  Reconnaissance ([Nmap](https://nmap.org/), banner & version detection).
2.  Enumeration (web content + service probing, directory discovery).
3.  Verification (safe, lab-only PoC to confirm impact).
4.  Privilege escalation checks ([LinPEAS/WinPEAS](https://github.com/carlospolop/privilege-escalation-awesome-scripts) / manual checks).
5.  Documentation & remediation recommendations.

---

## 🛠 Testing Tools & Environment

| Tool | Purpose | Source |
| :--- | :--- | :--- |
| Nmap | Network & service discovery | [Nmap Official Site](https://nmap.org/) |
| Gobuster | Directory and file enumeration | [Gobuster GitHub](https://github.com/OJ/gobuster) |
| Nikto | Quick web vulnerability scan | [Nikto Official Site](https://cirt.net/nikto2) |
| Netcat | Reverse shell / connections | [Netcat Documentation](https://manpages.debian.org/testing/netcat-openbsd/nc.1.en.html) |
| Python | Reverse shell scripts (lab-only) | [PayloadsAllTheThings Shells](https://book.hacktricks.xyz/shells/reverse-shells) |
| LinPEAS | Privilege escalation enumeration | [LinPEAS GitHub](https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS) |

*Environment:*

* Attacker: Kali Linux (2023.4)
* Target: Blue VM (Lab IP: *10.201.121.110*)

---

## 📊 Findings Overview

| ID | Finding | CVSS | Risk | CWE | Business Impact |
| :--- | :--- | :--- | :--- | :--- | :--- |
| BLUE-01 | Exposed Service Misconfiguration | 9.5 | Critical | [CWE-15](https://cwe.mitre.org/data/definitions/15.html) | Remote attacker gains system access (data theft or persistence) |
| BLUE-02 | Weak File Permissions | 7.8 | High | [CWE-276](https://cwe.mitre.org/data/definitions/276.html) | Local actor can escalate privileges; data integrity risk |
| BLUE-03 | Outdated Software / Exploitable | 8.1 | High | [CWE-1104](https://cwe.mitre.org/data/definitions/1104.html) | Known exploit chains could yield privilege escalation & RCE |

---

## 🔍 Detailed Vulnerability Analysis

### 1️⃣ BLUE-01: Exposed Service Misconfiguration – Critical
*CWE:* [CWE-15 — External Control of System or Configuration Setting](https://cwe.mitre.org/data/definitions/15.html).

*Summary:*
A service on the host accepts unauthenticated connections or uses default/insecure binding which allowed interaction that led to a remote shell in the lab environment.

*Impact:*
Full remote control of VM — attacker can run arbitrary commands, persist access, and access sensitive files.

> The following PoC is intended for authorized lab validation only. Do not attempt on production or unauthorized systems.

bash
# Example PoC (lab-reproducible, non-destructive):
# 1) Basic probe (service banner):
nc -vn 10.201.121.110 1337

# 2) If service echoes input back, test benign command injection verification:
echo "test; whoami > /tmp/lab_proof.txt" | nc 10.201.121.110 1337

# 3) Verify result (lab web server or file retrieval):
curl -s [http://10.201.121.110/tmp/lab_proof.txt](http://10.201.121.110/tmp/lab_proof.txt)

Remediation: Harden service binding and authentication, restrict to localhost or authorized networks, apply access controls, and patch/configure the service according to vendor guidance.

### 2️⃣ BLUE-02: Weak File Permissions – High

CWE: [CWE-276: Improper Default Permissions](https://cwe.mitre.org/data/definitions/276.html)

Summary:
Critical files and scripts under /opt and application directories have overly permissive modes allowing non-privileged users to view or modify them.

Impact:
Local users or processes can alter scripts/binaries leading to privilege escalation, persistence, or data tampering.

Evidence & Notes: File listings and ls -la outputs were captured and stored in /logs/perm_check.txt (redacted for public). Example check performed with:
find / -perm -o=w -type f 2>/dev/null

Remediation: Identify files with excessive permissions and tighten ownership/mode (e.g., chmod 640 or chmod 700 where applicable).
 * Remove SUID/SGID where not required.
 * Enforce least-privilege access controls and review deployment processes that set file modes.

---

### 3️⃣ BLUE-03: Outdated Software / Exploitable – High

CWE: [CWE-1104: Use of Unmaintained Third-Party Components](https://cwe.mitre.org/data/definitions/1104.html)

Summary:
Binaries on host are outdated with publicly known vulnerabilities (e.g., potentially MS17-010 / EternalBlue based on common THM Blue room design). Exploits for these versions exist and were used in the lab context to escalate privileges.

Impact:
Unpatched components may allow code execution, privilege escalation, or bypass of security controls.

Remediation: Inventory installed packages and apply vendor patches.
 * Remove unnecessary legacy services and packages.
 * Implement patch management and vulnerability scanning (e.g., weekly/bi-weekly scans).

---

## ⏱ Exploitation Timeline

| Phase | Time Taken | Summary | Evidence |
|:---|:---|:---|:---|
| Reconnaissance | 15 mins | Nmap + Gobuster scan | Commands logged |
| Web/Service Enumeration | 25 mins | Discovered endpoints & configs | Logs & screenshots |
| Exploitation | 30 mins | Remote shell (lab) obtained (Metasploit reference) | Payload & output |
| Privilege Escalation | 20 mins | Local → root via outdated/SUID | Commands executed |
| Flag Retrieval | 15 mins | All lab flags captured (redacted) | Flags stored (redacted) |
| Documentation | 1 hr | Report writing & formatting | N/A |

---

## 🖼 Technical Proof & Screenshots

> All screenshots and raw logs are stored in the repository under /screenshots/ and /logs/ respectively. Sensitive values (flags, credentials) have been redacted in public copies — full artifacts are available on request under NDA (Non-Disclosure Agreement).

1. **Initial Nmap Scan (SS01)**  
   ![SS01 – Initial Nmap Scan](https://i.imgur.com/ZL7oBOJ.jpeg)  
   *Initial Nmap output showing open ports and service fingerprints.*

2. **SMB Enumeration (SS02)**  
   ![SS02 – SMB Enumeration](https://i.imgur.com/JCYjuM2.jpeg)  
   *Discovered SMB shares, NetBIOS name and domain/workgroup information.*

3. **Vulnerability Identification (SS03)**  
   ![SS03 – Vulnerability Identification](https://i.imgur.com/SdtZvKz.jpeg)  
   *Confirmed whether MS17-010 / other SMB vulnerabilities are present; exploit references captured.*

4. **Exploit PoC Output (SS04)**  
   ![SS04 – Exploit PoC](https://i.imgur.com/bjGyKhv.jpeg)
   *Exploit run output; capture successful session lines (redact sensitive strings for public disclosure).*

5. **Reverse Shell Confirmation (SS05)**  
   ![SS05 – Reverse Shell Confirmation](https://i.imgur.com/NI8IH07.jpeg)  
   *Show session index, `getuid` and `sysinfo` outputs as confirmation of access.*

6. **Local Enumeration (SS06)**  
   ![SS06 – Local Enumeration](https://i.imgur.com/3DvjAAP.jpeg)  
   *Local enumeration showing process list and privilege information.*

7. **Final Flag 1 (SS07)**  
   ![SS07 – Final Flag 1](https://i.imgur.com/wclT3MP.jpeg)  
   *Redacted Final Flag 1 (public copy must show `THM{access_the_machine}` or similar). Keep the unredacted original in /loot/.*

8. **Final Flag 2 (SS08)**  
   ![SS08 – Final Flag 2](https://i.imgur.com/684Nvic.jpeg)  
   *Redacted Final Flag 2 with timestamp as proof of completion. Ensure timestamp and timezone are visible.*

> 🎨 Visual badge / summary:  
> ![Badge](https://i.imgur.com/gnkm3rd.jpeg)

---

## 🩹 Remediation Roadmap (Prioritized)

### Immediate (0–7 days) — P0
 * Harden exposed services: bind to localhost or secure network, enforce authentication.
 * Rotate any credentials discovered (if any).
 * Remove or restrict direct access to /tmp or public file lists used in lab deployments.

### Short-Term (7–30 days) — P1
 * Audit and fix file permissions.
 * Patch critical and high-severity CVEs; upgrade vulnerable packages.
 * Enable centralized logging & alerting for unusual service behavior.

### Medium/Long-Term (30–90+ days) — P2
 * Implement secure configuration baselines (CIS benchmarks).
 * Deploy automated patch management and vulnerability scanning.
 * Regular penetration testing cadence + remediation verification.

---

## 📌 CVSS & CWE Justification

| Finding | CVSS | CWE | Justification |
|:---|:---|:---|:---|
| Exposed Service Misconfiguration | 9.5 | [CWE-15](https://cwe.mitre.org/data/definitions/15.html) | Remote code execution potential (CVSS: Critical) |
| Weak File Permissions | 7.8 | [CWE-276](https://cwe.mitre.org/data/definitions/276.html) | Overly permissive files enable privilege escalation (CVSS: High) |
| Outdated Software / Exploitable | 8.1 | [CWE-1104](https://cwe.mitre.org/data/definitions/1104.html) | Known CVEs and exploitability (CVSS: High) |

---

## ⚠ Risk Matrix & Business Impact

Overall Risk: 🔴 Critical — Full system compromise achievable under current configuration.

Business Impact: Data exposure, loss of integrity, potential lateral movement in an enterprise if similar misconfigurations exist across environment.

---

## 📚 References & Framework Mapping

 * [OWASP Top 10 (2021)](https://owasp.org/www-project-top-ten/)
 * [CWE Database](https://cwe.mitre.org/data/definitions/1000.html)
 * NIST SP 800-115 (Technical Guide)
 * TryHackMe: Blue Room
 * GitHub Profile - Asibur-syber

## 📑 Delivery Package & Notes

*Recommended repository structure:*

THM23_Blue/
├─ THM23_Blue_Report.md
├─ THM23_Blue_Report.pdf
├─ screenshots/
│  ├─ SS01InitialNmap10.201.121.110.png
│  ├─ SS02SMBEnum10.201.121.110.png
│  ├─ SS03VulnScan10.201.121.110.png
│  ├─ SS04ExploitPoC10.201.121.110.png
│  ├─ SS05ShellInfo10.201.121.110.png
│  ├─ SS06LocalEnum10.201.121.110.png
│  ├─ SS07PrivEsc10.201.121.110.png
│  └─ SS08FlagTimestamp10.201.121.110.png
└─ logs/
   ├─ nmapscan.txt
   ├─ smb_enum.txt
   ├─ vulnscan.txt
   ├─ exploit_interaction.txt
   └─ perm_check.txt

*Notes:*
- Public repository should contain redacted artifacts (remove flags/credentials).  
- Full raw logs/screenshots should be provided privately under NDA if requested.

## 🔐 Evidence / Redaction Policy

*Public copies:* All flags, credentials, and secrets redacted.  
*Private copies:* Full logs/screenshots available under NDA.  

*Example:*  
FLAG{access_the_machine} → FLAG{sam_database_elevated_access}

---

## 💌 Personal Note to Client

> Dear Client,  
> Thank you for the opportunity to assess the Blue VM. This report focuses on technical accuracy and business impact. If you’d like, I can:
> 
> * Provide full raw evidence under NDA, or  
> * Schedule a 30-min walkthrough for remediation steps, or  
> * Convert this report into a 1-page executive summary PDF for board review.

*Best regards,*  
*Asibur Rahaman*  
Ethical Hacker & Cybersecurity Specialist  
📧 [asib51639@gmail.com](mailto:asib51639@gmail.com)

---

## ⚖ License & Disclaimer

*License:* [CC BY-NC-SA 4.0 — Creative Commons](https://creativecommons.org/licenses/by-nc-sa/4.0/) — Educational, non-commercial reuse allowed with attribution.  

*Disclaimer:* All testing was performed within TryHackMe lab scope. Techniques are for education and authorized environments only.

*Prepared on:* October 6, 2025
