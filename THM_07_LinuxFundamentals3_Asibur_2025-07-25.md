# 🛡️ **PENETRATION TEST REPORT**  
## 🔐 TryHackMe Room – #07: Linux Fundamentals 3

---

# 🧑‍💻 **ASIBUR RAHAMAN**  
*Ethical Hacker | Cybersecurity Learner | Web Recon & Auth Testing Enthusiast*  
🔗 GitHub: [github.com/Asibur-syber](https://github.com/Asibur-syber)  
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Risk](https://img.shields.io/badge/Overall_Risk-Low-green)
![Last Updated](https://img.shields.io/badge/Last_Update-July_28,_2025-blue)

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
- [🛠️ Tools, Commands & Payloads](#-tools-commands--payloads)
- [🖼️ Proof & Screenshots](#-proof--screenshots)
- [✅ Conclusion](#-conclusion)
- [⚠️ Risk Matrix](#️-risk-matrix)
- [📚 References](#-references)
- [📎 Appendix](#-appendix)
- [✍️ Signature & Contact](#-signature--contact)

---

## 🧠 **EXECUTIVE SUMMARY**
> Covers TryHackMe’s “Linux Fundamentals 3” room:
> - Wildcards, symbolic & hard links, and advanced file search
> - Commands like `find`, `grep`, `ln` and text processing utilities
> - Educational lab only; no vulnerability scanning or exploitation conducted

---

## 📜 **SCOPE & LIMITATIONS**
- Scope limited strictly to TryHackMe “Linux Fundamentals 3” room
- No vulnerability scanning, exploitation, or external enumeration performed
- Focused solely on quizzes and hands-on command line tasks

---

## 💡 **BUSINESS IMPACT**
- Enhances team’s advanced Linux proficiency
- Reduces risk of operational errors and misconfigurations
- Supports infrastructure hardening and security compliance

---

## 🔍 **METHODOLOGY**
| Step | Goal |
|--:|--:|
| Study | Learn advanced Linux commands, linking, and file search techniques |
| Practice | Complete lab tasks and challenges in TryHackMe |
| Document | Summarize key findings and lessons into a professional report |

Aligned with [OWASP Testing Guide](https://owasp.org/www-project-web-security-testing-guide/).

---

## 📊 **DETAILED FINDINGS TABLE**
| # | Vulnerability | Impact | Proof / Screenshot | Recommendation |
|--:|--:|--:|--:|--:|
| – | N/A | N/A | – | – |

---

## 🔒 **INDIVIDUAL FINDINGS & RISK RATINGS**
✅ *No vulnerabilities identified* — purely educational lab; no exploitation performed.

---

## 🛠️ **TOOLS, COMMANDS & PAYLOADS**
| Tool / Command | Purpose |
|--:|--:|
| `find`, `grep` | File searching and content filtering |
| `ln -s`, `ln` | Create symbolic and hard links |
| `wc`, `sort`, `head`, `tail` | File processing and text analysis |
| `passwd`, `sudo` | User and privilege management |
| TryHackMe platform | Virtual lab environment |

---

## 🖼️ **PROOF & SCREENSHOTS**

> 🟢 **Figure 1: Created symbolic link**
>
> ```
> ln -s /etc/passwd symlink_passwd
> ls -l
> ```
> ![Figure1](https://i.imgur.com/kg9JJ9q.jpeg)

> 🟢 **Figure 2: Created hard link**
>
> ```
> ln /etc/passwd hardlink_passwd
> ls -l
> ```
> ![Figure2](https://i.imgur.com/b7tbcHH.jpeg)

> 🟢 **Figure 3: Wildcard usage listing *.conf files**
>
> ```
> ls *.conf
> ```
> ![Figure3](https://i.imgur.com/uLMf7UL.jpeg)

> 🟢 **Figure 4: Find command searching for .conf files**
>
> ```
> find /etc -name "*.conf"
> ```
> ![Figure4](https://i.imgur.com/o5LOCWU.jpeg)

> 🟢 **Figure 5: Grep command filtering lines containing "root"**
>
> ```
> grep "root" /etc/passwd
> ```
> ![Figure5](https://i.imgur.com/O1IdYEh.jpeg)

> 🟢 **Figure 6: Counting lines in /etc/passwd**
>
> ```
> wc -l /etc/passwd
> ```
> ![Figure6](https://i.imgur.com/YMjbbeA.jpeg)

> 🟢 **Figure 7: Sorting and showing first 5 lines**
>
> ```
> sort /etc/passwd | head -n 5
> ```
> ![Figure7](https://i.imgur.com/bS8Geym.jpeg)

> 🟢 **Figure 8: Showing current user context**
>
> ```
> whoami
> ```
> ![Figure8](https://i.imgur.com/nxbUYTX.jpeg)

> 🟢 **Figure 9: Showing sudo privileges**
>
> ```
> sudo -l
> ```
> ![Figure9](https://i.imgur.com/7fqTM7f.jpeg)

> 🟢 **Figure 10: Combined command example (find + grep)**
>
> ```
> find . -type f | grep ".sh"
> ```
> ![Figure10](https://i.imgur.com/kYB9S5t.jpeg)

> 🎨 **Visual badge / summary:**  
> ![Badge](https://i.imgur.com/YHmN3uf.jpeg)

---

## ✅ **CONCLUSION**
- Successfully completed “Linux Fundamentals 3” focusing on linking, wildcards, and advanced search
- Enhanced practical Linux command line skills
- No real-world vulnerabilities tested; purely educational environment
- Next step: move toward Linux privilege escalation and enumeration techniques

---

## ⚠️ **RISK MATRIX**
| Risk | Findings |
|--:|--:|
| N/A | Educational lab only; no vulnerabilities assessed |

---

## 📚 **REFERENCES**
- [Linux Wildcards – GNU Manual](https://www.gnu.org/software/bash/manual/html_node/Wildcards.html)
- [Hard vs. Symbolic Links – Wikipedia](https://en.wikipedia.org/wiki/Hard_link)
- [OWASP Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
- [TryHackMe Room](https://tryhackme.com/room/linuxfundamentals3)

---

## 📎 **APPENDIX**
- Practice notes and task answers
- Advanced Linux commands cheat sheet

---

## ✍️ **SIGNATURE & CONTACT**
*Prepared by:*  
**Asibur Rahaman** – Ethical Hacker | Cybersecurity Learner | Web Recon & Auth Testing Enthusiast  
📅 Report generated on: July 25, 2025  
🔗 GitHub: [github.com/Asibur-syber](https://github.com/Asibur-syber)  
🔗 LinkedIn: [linkedin.com](https://www.linkedin.com/)  
📧 Email: asib51639@gmail.com

> _"Security is a journey, not a destination."_

---
