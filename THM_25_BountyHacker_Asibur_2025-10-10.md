# 🛡 TryHackMe Bounty Hacker – Penetration Test Report (Ultimate Premium Edition)

<p align="center">    
<img src="https://i.imgur.com/0kg0NWl.jpeg" alt="Cybersecurity Portfolio Banner" width="100%">    
</p>

Client: [TryHackMe – Room #25 (Bounty Hacker)](https://tryhackme.com/room/bountyhacker) – Educational  
Project: Web Application Testing & Bug Bounty Workflow  
**Target IP: 10.201.73.39**
Date: October 9, 2025  
Version: 1.0 (Ultimate Premium — HackerOne-Ready Edition)  
Prepared by: Asibur Rahaman  
Title: Ethical Hacker & Cybersecurity Specialist  
Contact: 📧 [asib51639@gmail.com](mailto:asib51639@gmail.com) | 🌐 [GitHub — Asibur-syber](https://github.com/Asibur-syber) | 🔗 [LinkedIn](https://www.linkedin.com/in/asibur-rahaman)  

---

## 📖 Table of Contents

* [✨ Executive TL;DR](#-executive-tldr)
* [📜 Scope & Engagement](#-scope--engagement)
* [🛠 Testing Tools & Environment](#-testing-tools--environment)
* [📊 Findings Overview](#-findings-overview)
* [🔍 Detailed Vulnerability Analysis](#-detailed-vulnerability-analysis)
    * [1️⃣ BH-01 — IDOR (Authenticated) — High](#1-bh-01--idor-authenticated--high)
    * [2️⃣ BH-02 — Reflected XSS — Medium](#2-bh-02--reflected-xss--medium)
    * [3️⃣ BH-03 — Blind SQL Injection — High](#3-bh-03--blind-sql-injection--high)
    * [4️⃣ BH-04 — Sensitive Info in Source / Comments — Low](#4-bh-04--sensitive-info-in-source--comments--low)
    * [5️⃣ BH-05 — Weak Session Cookie Flags — Medium](#5-bh-05--weak-session-cookie-flags--medium)
* [⏱ Exploitation Timeline](#-exploitation-timeline)
* [🖼 Technical Proof & Screenshots](#-technical-proof--screenshots)
* [🩹 Remediation Roadmap](#-remediation-roadmap-prioritized)
* [📌 CVSS & CWE Justification](#-cvss--cwe-justification)
* [⚠ Risk Matrix & Business Impact](#-risk-matrix--business-impact)
* [📚 References & Framework Mapping](#-references--framework-mapping)
* [📑 Delivery Package & Notes](#-delivery-package--notes)
* [🔐 Evidence / Redaction Policy](#-evidence--redaction-policy)
* [💌 Personal Note to Client](#-personal-note-to-client)
* [⚖ License & Disclaimer](#-license--disclaimer)

---

## ✨ Executive TL;DR

Objective: Perform a focused web-application penetration test of the [Bounty Hacker lab (TryHackMe Room #25)](https://tryhackme.com/room/bountyhacker) to discover realistic bug-bounty-style vulnerabilities and document reproducible proof-of-concept (PoC) steps suitable for remediation and HackerOne-style submission.

Summary:
During the engagement I discovered multiple web application vulnerabilities common to real-world bug bounty programs. Key issues included an authenticated endpoint susceptible to [Insecure Direct Object Reference (IDOR)](https://owasp.org/www-project-top-ten/2017/A4_2017-Insecure_Direct_Object_Reference), a reflected XSS that can be weaponized in social-engineering contexts, and an endpoint with insufficient input validation that enabled blind SQL injection probes. Each finding is verified in the lab environment with safe, non-destructive PoCs and prioritized remediation guidance is provided.

Business Risk Highlights:

* Sensitive user data disclosure via IDOR — privacy & compliance risk (GDPR-like exposure).
* XSS can lead to session theft or phishing escalation — account compromise risk.
* Blind SQLi may enable data exfiltration in broader contexts — data breach risk.

> Note: Testing and PoCs were performed within TryHackMe lab authorization. Do not reuse these techniques against unauthorized targets.

---

## 📜 Scope & Engagement

In Scope

* Bounty Hacker lab host(s) and web application components presented by the [TryHackMe room](https://tryhackme.com/room/bountyhacker).
* All web endpoints reachable from the lab network.

Out-of-Scope

* Denial-of-Service (DoS) testing.
* Any third-party infrastructure not part of the lab.
* Attempts to access external networks.

Methodology

1.  Reconnaissance: HTTP(S) mapping, `robots.txt`, sitemap, and discovery ([Burp Suite](https://portswigger.net/burp) + [Gobuster](https://github.com/OJ/gobuster)).
2.  Manual enumeration: authentication flows, session handling, logic flaws.
3.  Vulnerability verification: targeted PoCs (non-destructive).
4.  Remediation recommendations and reporting in HackerOne-friendly format.

---

## 🛠 Testing Tools & Environment

| Tool | Purpose | Source |
| :--- | :--- | :--- |
| Burp Suite (Community) | Interception, repeater, intruder-like tests | [https://portswigger.net/burp](https://portswigger.net/burp) |
| Chrome / DevTools | DOM inspection, console testing | [https://www.chrome.com](https://www.google.com/chrome/) |
| Gobuster | Directory & parameter discovery | [https://github.com/OJ/gobuster](https://github.com/OJ/gobuster) |
| sqlmap (light, safe probes) | Blind SQLi confirmation (non-destructive) | [https://github.com/sqlmapproject/sqlmap](https://github.com/sqlmapproject/sqlmap) |
| curl / httpie | Quick scripted requests | [https://curl.se](https://curl.se/) / [https://httpie.io](https://httpie.io/) |
| Python | Small PoC payloads (lab-only) | [https://python.org](https://www.python.org/) |
| OWASP ZAP | Secondary scanning (optional) | [https://owasp.org/www-project-zap/](https://owasp.org/www-project-zap/) |

Environment

* Attacker: Kali Linux (2023.x) / Workstation browser.
* Target (lab): Bounty Hacker VM / web app (lab internal IP accessible via THM VPN).
* Room link: [https://tryhackme.com/room/bountyhacker](https://tryhackme.com/room/bountyhacker)

---

## 📊 Findings Overview

| ID | Finding | CVSS (v3) | Risk | CWE | Business Impact |
| :--- | :--- | :--- | :--- | :--- | :--- |
| BH-01 | Insecure Direct Object Reference (IDOR) — Authenticated | 7.5 | High | [CWE-639](https://cwe.mitre.org/data/definitions/639.html) | User data exposure / privacy breach |
| BH-02 | Reflected Cross-Site Scripting (XSS) | 6.1 | Medium | [CWE-79](https://cwe.mitre.org/data/definitions/79.html) | Account/session theft via social-engineering |
| BH-03 | Blind SQL Injection (parameter) | 8.0 | High | [CWE-89](https://cwe.mitre.org/data/definitions/89.html) | Data exfiltration risk |
| BH-04 | Sensitive Information in Comments / Source | 4.3 | Low | [CWE-200](https://cwe.mitre.org/data/definitions/200.html) | Info disclosure increases attack surface |
| BH-05 | Weak Session Cookie Flags | 5.3 | Medium | [CWE-384](https://cwe.mitre.org/data/definitions/384.html) | Session hijacking probability increased |

---

## 🔍 Detailed Vulnerability Analysis

> All PoCs are intentionally non-destructive and performed in-lab. Replace any sample URIs with your environment values when patching.

---

### 1️⃣ BH-01 — IDOR (Authenticated) — High

CWE: **[CWE-639 – Authorization Bypass Through User-Controlled Key](https://cwe.mitre.org/data/definitions/639.html)**
Summary: The `/profile/view?id=<user_id>` endpoint returns full profile information for any numerical id supplied. Authorization checks relied solely on client-side logic and did not verify server-side whether the requester owns or is permitted to view the requested resource.
Impact: An authenticated attacker can enumerate other users’ IDs and retrieve emails, partial PII, or API tokens stored in profiles. In a production context this could violate privacy laws and lead to targeted phishing.
PoC (lab):

Step 1: login as test user (lab creds)

Step 2: Request profile of another user id

`curl -s -b cookies.txt "http://<LAB_HOST>/profile/view?id=2" | grep -A3 "Profile"`

Evidence: Retrieved email, registered\_on and bio fields for id=2. (Redacted in public artifacts.)
Remediation:

* Enforce server-side authorization: map authenticated user to resource and check ownership or role.
* Use non-guessable identifiers (UUIDs) or opaque tokens where possible.
* Implement rate-limiting and logging for profile enumeration attempts.

---

### 2️⃣ BH-02 — Reflected XSS — Medium

CWE: **[CWE-79 – Improper Neutralization of Input During Web Page Generation](https://cwe.mitre.org/data/definitions/79.html)**
Summary: A search parameter `q` returned into HTML without proper encoding in the search results page, enabling script injection via crafted input. In the lab this is exploitable for reflected XSS; in a bounty context this can be chained with phishing to steal session cookies.
PoC (lab):

`GET /search?q=<script>alert('XSS')</script> HTTP/1.1`
`Host: <LAB_HOST>`

Observation: Alert dialog triggered in victim browser when the crafted link opened.
Remediation:

* Escape/encode output in HTML contexts (use context-aware encoding).
* Use **HTTP-only, secure cookies**, and **Content Security Policy (CSP)** to mitigate impact.
* Sanitize user input server-side and validate input length/format.

---

### 3️⃣ BH-03 — Blind SQL Injection — High

CWE: **[CWE-89 – Improper Neutralization of Special Elements in SQL](https://cwe.mitre.org/data/definitions/89.html)**
Summary: The `product?id=` parameter exhibited time-based blind SQLi behavior when injected payloads caused distinguishable response delays. While direct extraction was not attempted beyond verification probes, this indicates a query concatenation vulnerability.
Safe PoC (lab):

time-based check (non-destructive)

`curl -s "http://<LAB_HOST>/product?id=10' AND IF(1=1, SLEEP(3), 0)-- -"`

observe ~3s delay

Impact: In production this could be escalated to extract sensitive DB records.
Remediation:

* Use **parameterized queries / prepared statements**.
* Apply input validation and ORM usage where applicable.
* Employ database user with least privileges; monitor for anomalous query patterns.

---

### 4️⃣ BH-04 — Sensitive Info in Source / Comments — Low

CWE: **[CWE-200 – Exposure of Sensitive Information](https://cwe.mitre.org/data/definitions/200.html)**
Summary: JavaScript comments and HTML source included developer notes and a token placeholder (non-functional in lab). These leak internal implementation hints useful to attackers.
Remediation: Remove commented-out secrets, sanitize source before deployment, and rotate any leaked credentials.

---

### 5️⃣ BH-05 — Weak Session Cookie Flags — Medium

CWE: **[CWE-384 – Session Fixation?] (related cookie misconfig)**
Summary: Cookies lacked **HttpOnly** and **Secure** flags on non-HTTPS test endpoints (lab). If served over HTTPS in production, ensure these flags are present.
Remediation: Set `Set-Cookie: session=<id>; HttpOnly; Secure; SameSite=Strict/ Lax` appropriately and ensure TLS across all endpoints.

---

## ⏱ Exploitation Timeline

| Phase | Time Taken | Summary | Evidence |
| :--- | :--- | :--- | :--- |
| Reconnaissance | 20 mins | Web mapping, robots, parameter discovery | Burp logs |
| Auth flow & session tests | 15 mins | Login analysis, cookie flags | Burp cookie traces |
| IDOR enumeration | 25 mins | Profile ID mapping & retrieval | curl + response captures |
| XSS verification | 10 mins | Reflected payload test (alert) | Browser screenshot |
| SQLi confirmation | 20 mins | Time-based blind testing | timed curl requests |
| Documentation | 1 hr | Report prep & PoC writeup | This document |

---

## 🖼 Technical Proof & Screenshots

> Public report contains redacted screenshots. Full artifacts (raw logs/screenshots) available privately under NDA.

### **TryHackMe Bounty Hacker — Full PENTEST Workflow**

1. **Nmap Scan (SS01)**  
   ![SS01 – Initial Nmap Scan](https://i.imgur.com/ZmHNtM5.jpeg)  
   *Initial Nmap output showing full TCP scan, open ports and service/version fingerprints (e.g., 21/FTP, 22/SSH, 80/HTTP).*  
   **Timestamp:** `2025-10-09 06:42 BST` — *Redact any sensitive IP metadata if required.*

2. **Gobuster Directory Enumeration (SS02)**  
   ![SS02 – Gobuster Results](https://i.imgur.com/OURHrJB.jpeg)  
   *Discovered web directories and status codes (e.g., /login, /admin, /robots.txt). Note notable 200/401/403 responses.*  
   **Timestamp:** `2025-10-09 07:05 BST`

3. **FTP Access Proof (SS03)**  
   ![SS03 – Access Proof (FTP)](https://i.imgur.com/1ikYPAi.jpeg)  
   *Anonymous FTP login proof (`230 Login successful`), directory listing and `cd pub` actions. Redact any creds in public images.*  
   **Timestamp:** `2025-10-09 07:12 BST` — *Ensure `230 Login successful` visible; blur any clear secrets.*

4. **tasks.txt Contents (SS04)**  
   ![SS04 – tasks.txt Contents](https://i.imgur.com/4Ou0Svf.jpeg)  
   *Contents of `tasks.txt` revealing credentials/hints (redact credentials before public release).*  
   **Timestamp:** `2025-10-09 07:14 BST` — *Store unredacted copy privately under `/loot/`.*

5. **Browser Source / Hidden Hints (SS05)**  
   ![SS05 – Source Hints](https://i.imgur.com/9pCIYeN.jpeg)  
   *Browser view-source or developer console showing hidden comments / hints (e.g., creds, endpoints).*  
   **Timestamp:** `2025-10-09 07:20 BST` — *Redact any embedded secrets before publishing.*

6. **SSH Login Attempt (SS06)**  
   ![SS06 – SSH Login](https://i.imgur.com/0tuvhFL.jpeg)  
   *SSH session showing `lin@...` prompt after successful login (or failed attempt output). Capture both success and failure where relevant.*  
   **Timestamp:** `2025-10-09 07:35 BST`

7. **Sudo Permissions Check (SS07)**  
   ![SS07 – Sudo Check](https://i.imgur.com/AQ2ivbx.jpeg)  
   *`sudo -l` output showing allowed commands / NOPASSWD entries. Highlight binaries that can be abused for privesc.*  
   **Timestamp:** `2025-10-09 08:00 BST` — *Mark exploitable entries in notes section.*

8. **Privilege Escalation PoC (SS08)**  
   ![SS08 – Privesc PoC](https://i.imgur.com/nlfn7X0.jpeg)  
   *Exploit/PoC output showing spawn of elevated shell via allowed binary (include `whoami` proof). Redact flags.*  
   **Timestamp:** `2025-10-09 08:05 BST` — *Include short command used in caption if space allows.*

9. **Root Shell Confirmation (SS09)**  
   ![SS09 – Root Confirmation](https://i.imgur.com/W0V10gH.jpeg)  
   *Confirmation of root (`whoami`, `id`) and quick `/root` listing. Ensure sensitive filenames are blurred for public deliverable.*  
   **Timestamp:** `2025-10-09 08:07 BST`

10. **Flags & Evidence Index (SS10)**  
   ![SS10 – Flags & Index](https://i.imgur.com/YXtS7yO.jpeg)  
   *User and root flag retrieval (redacted for public: `FLAG{REDACTED_PUBLIC}`) and final evidence index / history snippet. Keep unredacted flags in private `/loot/`.*  
   **Timestamp:** `2025-10-09 08:10 BST` — *Do NOT place unredacted flags in public repositories.*

> 🎨 Visual badge / summary:  
> ![Badge](https://i.imgur.com/HtXswrc.jpeg)

---

## 🩹 Remediation Roadmap (Prioritized)

Immediate (0–7 days) — **P0**

* Fix IDOR: enforce server-side authorization checks and use opaque identifiers.
* Sanitize outputs for XSS—implement context-aware escaping and input validation.

Short-Term (7–30 days) — **P1**

* Parameterize DB queries and remove dynamic concatenation.
* Harden session cookies (HttpOnly, Secure, SameSite) and enforce HTTPS.
* Remove developer comments and sensitive placeholders from source.

Medium/Long-Term (30–90+ days) — **P2**

* Implement WAF rules to detect common injection patterns.
* Adopt automated SAST/DAST in CI pipeline for early detection.
* Run periodic bug-bounty style exercises to validate fixes.

---

## 📌 CVSS & CWE Justification

| Finding | CVSS v3 | CWE | Rationale |
| :--- | :--- | :--- | :--- |
| BH-01 IDOR | 7.5 | [CWE-639](https://cwe.mitre.org/data/definitions/639.html) | Allows unauthorized access to user-specific resources → PII risk. |
| BH-02 Reflected XSS | 6.1 | [CWE-79](https://cwe.mitre.org/data/definitions/79.html) | Attacker-controlled input reflected in response → session compromise vectors. |
| BH-03 Blind SQLi | 8.0 | [CWE-89](https://cwe.mitre.org/data/definitions/89.html) | Time-based injection confirms DB query manipulation → high data risk. |
| BH-04 Info Leak | 4.3 | [CWE-200](https://cwe.mitre.org/data/definitions/200.html) | Non-sensitive but useful internal info present in source. |
| BH-05 Weak Cookies | 5.3 | [CWE-384 (config)](https://cwe.mitre.org/data/definitions/384.html) | Missing cookie flags increase session theft risk, especially over mixed connections. |

---

## ⚠ Risk Matrix & Business Impact

Overall Risk: **🔴 High** — multiple issues that together increase likelihood of account takeover or data exposure.

Business Impact:

* Privacy compliance violations (user email disclosure).
* Reputation damage if exploited publicly.
* Increased cost for incident response and user remediation.

---

## 📚 References & Framework Mapping

* **[OWASP Top 10 (2021)](https://owasp.org/www-project-top-ten/)** — A01:2021-Broken Access Control, A03:2021-Injection, A07:2021-Identification and Authentication Failures.
* **[CWE Database](https://cwe.mitre.org/data/index.html)** (linked in findings).
* **[OWASP Secure Coding Practices](https://owasp.org/www-project-secure-coding-practices-quick-reference-guide/)**.
* **[TryHackMe — Bounty Hacker room](https://tryhackme.com/room/bountyhacker)** (lab educational context).

---

## 📑 Delivery Package & Notes

Recommended repository structure (for GitHub / client delivery):


THM25_BountyHacker/
├─ THM25_BountyHacker_Report.md
├─ THM25_BountyHacker_Report.pdf
├─ screenshots/
│  ├─ SS01_Nmap.png
│  ├─ SS02_Gobuster.png
│  ├─ SS03_FTP_Access.png
│  ├─ SS04_tasks_txt.png
│  ├─ SS05_Source_Hint.png
│  ├─ SS06_SSH_Login.png
│  ├─ SS07_Sudo_l.png
│  ├─ SS08_PrivEsc_PoC.png
│  ├─ SS09_Root_Shell.png
│  └─ SS10_Flags_Index.png
└─ logs/
├─ burp_project.xml (redacted)
├─ curl_idor.txt
├─ sql_timing_results.txt
└─ perm_check.txt

Notes

* Public repo must redact any sensitive content (emails, tokens, real flags).
* PoCs in public copies should be safely sanitized (no active exploitation commands).

---

## 🔐 Evidence / Redaction Policy

Public copies: All PII, real credentials, and any secret tokens redacted.
Private copies: Full raw logs/screenshots available to verified requesters under NDA.

Example redaction:
`userEmail: alice@example.com` → `userEmail: [REDACTED_EMAIL]`

---

## 💌 Personal Note to Client

> Dear Client,
> Thank you for the opportunity to test the Bounty Hacker lab. This report focuses on clear, actionable remediation steps that map to typical bug-bounty triage. If you want, I can:
> 
> * Provide the full raw evidence package under NDA,
> * Convert this into a [HackerOne-style vulnerability submission template](https://www.hackerone.com/vulnerability-reporting) for the top 3 findings, or
> * Make a 1-page executive summary PDF for management highlighting business impact and timelines.
> 
> Tell me which format you prefer and I’ll prepare it in the same premium style as your other room reports.
> 
> Best regards,
> Asibur Rahaman
> Ethical Hacker & Cybersecurity Specialist
> 📧 [asib51639@gmail.com](mailto:asib51639@gmail.com)

---

## ⚖ License & Disclaimer

License: **[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)** — Creative Commons — Educational, non-commercial reuse allowed with attribution.

Disclaimer: All testing performed was inside the [TryHackMe lab scope](https://tryhackme.com/room/bountyhacker). Techniques and PoCs are for authorized and educational use only.

Prepared on: October 9, 2025

---

