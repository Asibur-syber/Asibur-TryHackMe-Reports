# 🛡️ **PENETRATION TEST REPORT**  
## 🔐 TryHackMe Room – #10: Windows Fundamentals 3 (🟩 Low Risk)

---

# 🧑‍💻 **ASIBUR RAHAMAN**  
*Ethical Hacker | Cybersecurity Learner | Web Recon & Auth Testing Enthusiast*  
🔗 GitHub: [github.com/Asibur-syber](https://github.com/Asibur-syber)  
🔗 LinkedIn: [linkedin.com/feed](https://www.linkedin.com/feed)  
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Risk](https://img.shields.io/badge/Overall_Risk-Low-green)
![Last Updated](https://img.shields.io/badge/Last_Update-July_29,_2025-blue)

> _"Beginner to advanced TryHackMe walkthrough reports documenting my practical cybersecurity learning journey."_

---

## 📌 **SUMMARY**
| Target Environment     | Scope Type      | Total Findings | Risk Level |
|----------------------|-----------------|----------------|-----------|
| Local VM (Windows)   | Educational Lab | 0              | 🟩 Low    |

---

## 📚 **TABLE OF CONTENTS**
- [🧠 Executive Summary](#-executive-summary)
- [📜 Scope & Limitations](#-scope--limitations)
- [💡 Business Impact](#-business-impact)
- [🔍 Methodology](#-methodology)
- [📊 Findings Table](#-findings-table)
- [🔒 Analysis & Risk Ratings](#-analysis--risk-ratings)
- [🛠️ Tools & Techniques](#-tools--techniques)
- [🖼️ Proof & Screenshots](#-proof--screenshots)
- [🧪 MCQ Solutions](#-mcq-solutions)
- [📈 Next Steps](#-next-steps)
- [✅ Conclusion](#-conclusion)
- [⚠️ Visual Risk Matrix](#-visual-risk-matrix)
- [📎 Appendix](#-appendix)
- [📚 References](#-references)
- [✍️ Signature](#-signature)

---

## 🧠 **EXECUTIVE SUMMARY**
This report documents the completion of **TryHackMe’s Windows Fundamentals 3** room, focusing on:

- Windows internal tools: `msinfo32`, `msconfig`, `Task Manager`, `Event Viewer`
- Windows Defender configuration & scanning
- System diagnostics and log monitoring

> **Purpose:** Gain practical familiarity with core Windows administrative tools to improve defensive awareness.

---

## 📜 **SCOPE & LIMITATIONS**
- Only the TryHackMe "Windows Fundamentals 3" lab
- No real-world systems or external enumeration
- Focus: Educational exploration of built-in tools, no exploitation performed

---

## 💡 **BUSINESS IMPACT**
- Strengthens administrator visibility into system health
- Helps identify & respond to anomalies using native tools
- Improves defense through better understanding of built-in security features

---

## 🔍 **METHODOLOGY**
| Step      | Purpose                                      |
|---------|-----------------------------------------------|
| Research | Learn built-in tools & defensive capabilities |
| Practice | Perform lab tasks & quizzes                   |
| Document | Capture screenshots, explain tools & answers  |

---

## 📊 **FINDINGS TABLE**
| ID  | Finding                   | Risk | Evidence                                       | Recommendation        |
|----|---------------------------|-----|-----------------------------------------------|----------------------|
| N/A | Educational lab only – no real vulnerability | N/A  | ![Proof](https://i.imgur.com/f2LnbD7.jpeg) | No action required   |

> ✅ All security features (Defender, logs, configurations) remained active.

---

## 🔒 **ANALYSIS & RISK RATINGS**
| Scenario                                | Potential Impact |
|----------------------------------------|-----------------|
| Disabled Defender real-time protection | 🟥 High         |
| Ignored event logs                     | 🟧 Medium       |
| Poor admin monitoring                  | 🟨 Low          |

🟩 In this lab: all defensive settings were correctly enabled → overall risk remains **Low**.

---

## 🛠️ **TOOLS & TECHNIQUES**
| Tool              | Use Case                                |
|------------------|-------------------------------------------|
| `msinfo32`       | View detailed system specs                |
| `msconfig`       | Manage startup configurations            |
| `Task Manager`   | Monitor processes, services & performance |
| `Event Viewer`   | Analyze system & application logs        |
| `Windows Defender` | Scan and protect the system              |
| `winver`         | Check OS version                         |

---

## 🖼️ **PROOF & SCREENSHOTS**

> 🖥️ Figure 1: OS Version (winver)  
> ![Figure1](https://i.imgur.com/2kIZfaZ.jpeg)

> 📋 Figure 2: System Information (msinfo32)  
> ![Figure2](https://i.imgur.com/X4jEb4P.jpeg)

> ⚙️ Figure 3: System Configuration (msconfig)  
> ![Figure3](https://i.imgur.com/mi7cS5M.jpeg)

> 🛡️ Figure 4: Windows Defender Settings  
> ![Figure4](https://i.imgur.com/6GxvylK.jpeg)

> 🔍 Figure 5: Defender Scan Result  
> ![Figure5](https://i.imgur.com/Egvm8Hb.jpeg)

> 📊 Figure 6: Task Manager Overview  
> ![Figure6](https://i.imgur.com/iHVXG1S.jpeg)

> 🧾 Figure 7: Event Viewer – System Logs  
> ![Figure7](https://i.imgur.com/qWzNjJv.jpeg)

> 🎨 **Visual badge / summary:**  
> ![Badge](https://i.imgur.com/ITtXwoA.jpeg)

---

## 🧪 **MCQ SOLUTIONS**

| Question                               | Answer              |
|---------------------------------------|--------------------|
| Detailed system info                  | ✅ msinfo32        |
| Control startup options               | ✅ msconfig        |
| Built-in antivirus                    | ✅ Windows Defender|
| Monitor memory/CPU                    | ✅ Task Manager    |
| View logs                              | ✅ Event Viewer    |
| OS version command                     | ✅ winver          |
| Task Manager tab for services          | ✅ Services        |
| Alerts about system issues              | ✅ Event Logs      |
| Defender scans using                    | ✅ Signatures      |
| Disable startup apps                    | ✅ Task Manager (Startup tab) |

> ✅ All answers verified & documented.

---

## 📈 **NEXT STEPS**
- Learn Windows privilege escalation techniques
- Explore real-world misconfigurations & exploit paths
- Practice Active Directory basics & local user enumeration

---

## ✅ **CONCLUSION**
- Successfully completed Windows Fundamentals 3 lab
- Understood critical Windows system & security tools
- No vulnerabilities; lab was purely educational

> 🔜 Next target: Move beyond fundamentals to real-world Windows security testing.

---

## ⚠️ **VISUAL RISK MATRIX**

| Likelihood ↓ \ Impact → | Low | Medium | High |
|------------------------|-----|--------|------|
| **Low**               | 🟩 | 🟨 | 🟨 |
| **Medium**            | 🟨 | 🟧 | 🟥 |
| **High**              | 🟨 | 🟥 | 🟥 |

🟩 Current Risk Level: **Low**

---

## 📎 **APPENDIX**
- 🛠️ Cheat tools: `msinfo32`, `msconfig`, `winver`, Event Viewer, Task Manager
- 📌 Key focus: defensive monitoring, system diagnostics, Windows Defender basics

---

## 📚 **REFERENCES**
- [TryHackMe Room – Windows Fundamentals 3](https://tryhackme.com/room/windowsfundamentals3)
- [Microsoft Defender Docs](https://learn.microsoft.com/en-us/microsoft-365/security/defender-endpoint/microsoft-defender-endpoint)
- [System Configuration Tool (msconfig)](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/msconfig)
- [Event Viewer Overview](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-viewer)

---

## ✍️ **SIGNATURE**

**Prepared by:**  
🧑‍💻 *Asibur Rahaman*  
Ethical Hacker | Cybersecurity Learner  
📅 Report Date: July 29, 2025  
📧 Email: asib51639@gmail.com  
🔗 GitHub: [github.com/Asibur-syber](https://github.com/Asibur-syber)  
🔗 LinkedIn: [linkedin.com/feed](https://www.linkedin.com/feed)

> _"Windows gives you visibility — security gives you control."_
