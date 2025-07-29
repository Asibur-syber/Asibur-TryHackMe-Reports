# 🛡️ **PENETRATION TEST REPORT**  
## 🔐 TryHackMe Room – #09: Windows Fundamentals 2

---

# 🧑‍💻 **ASIBUR RAHAMAN**  
*Ethical Hacker | Cybersecurity Learner | Web Recon & Auth Testing Enthusiast*  
🔗 GitHub: [github.com/Asibur-syber](https://github.com/Asibur-syber)  
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Risk](https://img.shields.io/badge/Overall_Risk-Low-green)
![Last Updated](https://img.shields.io/badge/Last_Update-July_29,_2025-blue)

> _"Beginner to advanced TryHackMe walkthrough reports documenting my practical cybersecurity learning journey."_

---

## 📌 **REPORT SUMMARY**
| Target IP | Overall Risk | Total Findings | High | Medium | Low |
|--:|--:|--:|--:|--:|--:|
| *N/A* | 🟩 Low | 0 | 0 | 0 | 0 |

---

## 📑 **TABLE OF CONTENTS**
- [🧠 Executive Summary](#-executive-summary)
- [📜 Scope & Limitations](#-scope--limitations)
- [💡 Business Impact](#-business-impact)
- [🔍 Methodology](#-methodology)
- [📊 Detailed Findings Table](#-detailed-findings-table)
- [🔒 Individual Findings & Risk Ratings](#-individual-findings--risk-ratings)
- [🛠️ Tools, Commands & Techniques](#-tools-commands--techniques)
- [🖼️ Proof & Screenshots](#-proof--screenshots)
- [🧪 MCQ Answers](#-mcq-answers)
- [✅ Conclusion](#-conclusion)
- [⚠️ Risk Matrix](#️-risk-matrix)
- [📚 References](#-references)
- [📎 Appendix](#-appendix)
- [✍️ Signature & Contact](#-signature--contact)

---

## 🧠 **EXECUTIVE SUMMARY**
> Covers TryHackMe’s “Windows Fundamentals 2” room:  
> - Windows user and group management  
> - Key tools: Local Users & Groups, lusrmgr.msc, net user command  
> - Focused on understanding permissions, user rights, and administrative groups  
> - No exploitation performed; purely educational

---

## 📜 **SCOPE & LIMITATIONS**
- Scope strictly limited to the **Windows Fundamentals 2** TryHackMe room
- Only local lab; no external scanning, enumeration, or privilege escalation
- Purpose purely educational

---

## 💡 **BUSINESS IMPACT**
- Strengthens IT team’s understanding of Windows access control
- Reduces risk of misconfigured permissions
- Supports secure user account management practices

---

## 🔍 **METHODOLOGY**
| Step | Goal |
|--:|--:|
| Study | Learn Windows user & group management |
| Hands-on | Complete TryHackMe tasks using built-in Windows tools |
| Document | Summarize commands, screenshots & MCQ answers |

---

## 📊 **DETAILED FINDINGS TABLE**
| # | Vulnerability | Impact | Proof / Screenshot | Recommendation |
|--:|--:|--:|--:|--:|
| – | N/A | N/A | – | – |

---

## 🔒 **INDIVIDUAL FINDINGS & RISK RATINGS**
✅ *No vulnerabilities identified* — purely educational lab focused on Windows management basics.

---

## 🛠️ **TOOLS, COMMANDS & TECHNIQUES**
| Tool / Command | Purpose |
|--:|--:|
| `lusrmgr.msc` | Manage local users & groups |
| `net user` | View user info, create/delete users |
| `net localgroup` | Manage group memberships |
| Windows GUI | Users, Groups, and Permissions configuration |

---

## 🖼️ **PROOF & SCREENSHOTS**

> 🟢 Figure 1: Opened Local Users & Groups (lusrmgr.msc)  
> ![Figure1](https://i.imgur.com/jiR8hM3.jpeg)

> 🟢 Figure 2: Listed all local users using net user command  
> ![Figure2](https://i.imgur.com/kiPxt4y.jpeg)

> 🟢 Figure 3: Listed all local groups using net localgroup command  
> ![Figure3](https://i.imgur.com/yQNTvYI.jpeg)

> 🟢 Figure 4: Viewed built-in Guest account properties window  
> ![Figure4](https://i.imgur.com/jUUNo3u.jpeg)

> 🟢 Figure 5: Viewed Administrator account properties window  
> ![Figure5](https://i.imgur.com/sMcMEnC.jpeg)

> 🟢 Figure 6: Viewed Backup Operators group properties  
> ![Figure6](https://i.imgur.com/TONpZR8.jpeg)

> 🎨 **Visual badge / summary:**  
> ![Badge](https://i.imgur.com/Kj1yxWY.jpeg)

---

## 🧪 **MCQ ANSWERS**
> ✅ _TryHackMe Windows Fundamentals 2 – Quiz section exact answers:_

1️⃣ **What built-in group has full control over the system?**  
✅ *Administrators*

2️⃣ **What is the name of the built-in guest account?**  
✅ *Guest*

3️⃣ **What command lists all local users?**  
✅ `net user`

4️⃣ **What command lists all local groups?**  
✅ `net localgroup`

5️⃣ **Which tool provides a GUI for managing local users and groups?**  
✅ *lusrmgr.msc*

6️⃣ **Which user account is disabled by default?**  
✅ *Guest*

7️⃣ **What group can back up and restore files?**  
✅ *Backup Operators*

8️⃣ **What command changes a user's password?**  
✅ `net user <username> *`

9️⃣ **Which account cannot be deleted?**  
✅ *Administrator*

🔟 **What is the primary purpose of groups?**  
✅ *Manage permissions efficiently*

---

## ✅ **CONCLUSION**
- Completed **Windows Fundamentals 2** with hands-on on users, groups & permissions
- Documented tools, key commands & MCQ answers
- No vulnerabilities tested; purely educational
- Next step: **Windows Fundamentals 3** to learn deeper OS internals

---

## ⚠️ **RISK MATRIX**
| Risk | Findings |
|--:|--:|
| N/A | Educational lab only; no vulnerabilities found |

---

## 📚 **REFERENCES**
- [Microsoft Docs – Manage Local Users](https://learn.microsoft.com/en-us/windows/security/identity-protection/access-control/local-accounts)
- [Net User Command Guide](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/net-user)
- [TryHackMe Room](https://tryhackme.com/room/windowsfundamentals2)

---

## 📎 **APPENDIX**
- Notes on user/group permissions
- Cheatsheet: `net user`, `net localgroup`, `lusrmgr.msc`

---

## ✍️ **SIGNATURE & CONTACT**
*Prepared by:*  
**Asibur Rahaman** – Ethical Hacker | Cybersecurity Learner | Web Recon & Auth Testing Enthusiast  
📅 Report generated on: July 29, 2025  
🔗 GitHub: [github.com/Asibur-syber](https://github.com/Asibur-syber)  
🔗 LinkedIn: [linkedin.com](https://www.linkedin.com/)  
📧 Email: asib51639@gmail.com

> _"Security is a journey, not a destination."_
