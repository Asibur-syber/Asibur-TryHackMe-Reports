# 🛡 PENETRATION TEST REPORT

## 🔐 TryHackMe Room – #13: Burp Suite Repeater (🟨 Medium Risk)

---

### 🧑‍💻 ASIBUR RAHAMAN  
Ethical Hacker | Web App Pentester | Burp Suite & OWASP Enthusiast  
🔗 GitHub: [github.com/Asibur-syber](https://github.com/Asibur-syber)  
🔗 LinkedIn: [linkedin.com/feed](https://linkedin.com/feed)

> “Beginner to advanced TryHackMe walkthrough reports documenting my practical cybersecurity learning journey.”

---

## 📌 SUMMARY

| Target IP        | Scope Type       | Total Findings | Risk Level      |
|------------------|------------------|----------------|-----------------|
| 10.201.6.12    | Educational Lab  | 1              | 🟨 Medium Risk   |

---

## 📚 TABLE OF CONTENTS  
  
- [🧠 Executive Summary](#-executive-summary)  
- [📜 Scope & Limitations](#-scope--limitations)  
- [💡 Business Impact](#-business-impact)  
- [🔍 Methodology](#-methodology)  
- [📊 Findings Table](#-findings-table)  
- [🔒 Analysis & Risk Ratings](#-analysis--risk-ratings)  
- [🛠 Tools & Techniques](#-tools--techniques)  
- [🖼 Proof & Screenshots](#-proof--screenshots)  
- [🧪 MCQ Solutions](#-mcq-solutions)  
- [📈 Next Steps](#-next-steps)  
- [✅ Conclusion](#-conclusion)  
- [⚠ Visual Risk Matrix](#-visual-risk-matrix)  
- [📎 Appendix](#-appendix)  
- [📚 References](#-references)  
- [✍ Signature](#-signature)
 
---

## 🧠 EXECUTIVE SUMMARY

This report details the penetration testing steps performed in TryHackMe Room #13: *Burp Suite Repeater*. The room focuses on capturing and modifying HTTP requests using the Burp Suite Repeater tool to bypass client-side restrictions and retrieve sensitive information like flags.

*Key Focus:*
- Capturing HTTP traffic with Burp Proxy  
- Sending and modifying requests in Burp Repeater  
- Understanding Inspector panel functionality  
- Bypassing headers to reveal hidden data

---

## 📜 SCOPE & LIMITATIONS

- ✅ Scope limited to TryHackMe Room 10.201.6.12 only  
- ❌ No attack on real-world or production systems  
- ✅ Testing limited to web-based HTTP request manipulation  
- ❌ No brute-force or fuzzing performed  

---

## 💡 BUSINESS IMPACT

| Impact Area              | Description                                                                 |
|--------------------------|-----------------------------------------------------------------------------|
| Authentication Testing   | Demonstrates how client-side restrictions can be bypassed using intercepts |
| Defensive Awareness      | Helps identify weaknesses in relying solely on frontend validation         |
| Secure Headers Practice  | Encourages implementation of server-side authorization logic               |

---

## 🔍 METHODOLOGY

| Step            | Description                                             |
|-----------------|---------------------------------------------------------|
| Recon           | Visited target http://10.201.6.12 in browser          |
| Interception    | Used Burp Suite Proxy to capture HTTP request           |
| Repeater Use    | Forwarded request to Repeater for modification/testing  |
| Inspector Panel | Used Inspector to add new header (e.g., FlagAuthorised) |
| Response Review | Observed output with flag data in response body         |

---

## 📊 FINDINGS TABLE

| ID  | Finding                        | Risk     | Evidence                        | Recommendation                       |
|-----|--------------------------------|----------|----------------------------------|--------------------------------------|
| 01  | Header-based flag bypass       | 🟨 Medium | Burp Repeater & response content | Enforce server-side authentication   |

---

## 🔒 ANALYSIS & RISK RATINGS

| Scenario                              | Potential Impact |
|---------------------------------------|------------------|
| Missing server-side validation        | 🟥 High           |
| Reliance on client-side logic only    | 🟧 Medium         |
| Unauthorized flag disclosure via header | 🟨 Medium         |

➡ Final Lab Risk Level: 🟨 Medium

---

## 🛠 TOOLS & TECHNIQUES

| Tool             | Purpose                                          |
|------------------|--------------------------------------------------|
| Burp Suite Proxy | Intercept HTTP traffic from browser              |
| Burp Suite Repeater | Modify & resend captured requests             |
| Burp Inspector   | Modify headers, params, and view request layers  |
| Firefox Browser  | Access lab environment (http://10.201.6.12)      |

---

## 🖼 PROOF & SCREENSHOTS

### 📷 Screenshot Gallery

1. *Target Website Opened in Browser*  
   ![Screenshot 1 – Accessing Target IP](https://i.imgur.com/rHzDLar.jpeg)

2. *HTTP Request Captured in Burp Proxy*  
   ![Screenshot 2 – Burp Proxy Request](https://i.imgur.com/Lf37GO4.jpeg)

3. *Request Sent to Repeater (Unmodified)*  
   ![Screenshot 3 – Repeater Original Request](https://i.imgur.com/2ruMhe7.jpeg)

4. *Inspector Panel Showing Added Header*  
   ![Screenshot 4 – Inspector with FlagAuthorised: True](https://i.imgur.com/6sWlTR8.jpeg)

5. *Flag Shown in Repeater Response*  
   ![Screenshot 5 – Flag in Response Body](https://i.imgur.com/tP244C7.jpeg)

6. *Response View Switched to Pretty / Hex*  
   ![Screenshot 6 – Pretty View Enabled](https://i.imgur.com/RvwwEeo.jpeg)

7. *Final Flag Highlighted for Submission*  
   ![Screenshot 7 – Flag Highlighted](https://i.imgur.com/Ktafuyj.jpeg)

> 🎨 **Visual badge / summary:**  
> ![Badge](https://i.imgur.com/UMZ0HRD.jpeg)

---

## 🧪 MCQ SOLUTIONS

| Question                                        | Correct Answer        |
|-------------------------------------------------|------------------------|
| Repeater is used to...                          | ✅ Modify & resend requests |
| Add headers easily in Repeater using...         | ✅ Inspector panel     |
| Which section is specific to POST requests?     | ✅ Body                |
| Which panel lets you see request layers easily? | ✅ Inspector           |
| How to bypass flag restriction in lab?          | ✅ Add FlagAuthorised: True header |

---

## 📈 NEXT STEPS

- Learn Burp Intruder and advanced automation  
- Explore Auth bypass using tokens/cookies  
- Start hands-on testing with real bug bounty targets  
- Practice POST-based attacks with complex headers  

---

## ✅ CONCLUSION

The lab demonstrated how an attacker can *modify headers* using Burp Suite Repeater to bypass superficial client-side restrictions and extract sensitive content. This reinforces the need for *server-side validation* of all inputs and headers.

---

## ⚠ VISUAL RISK MATRIX

| Likelihood ↓ \ Impact → | Low  | Medium | High  |
|--------------------------|------|--------|-------|
| Low                      | 🟩   | 🟨     | 🟧    |
| Medium                   | 🟨   | 🟧     | 🟥    |
| High                     | 🟧   | 🟥     | 🟥    |

🟨 *Overall Risk Level: Medium*

---

## 📎 APPENDIX

### 🛠 Commands & Headers Used
- Header: FlagAuthorised: True  
- Repeater modifications via Inspector  

---

## 📚 REFERENCES

- [TryHackMe Room – Burp Suite Repeater](https://tryhackme.com/room)
- [Burp Suite Official Documentation](https://portswigger.net)
- [OWASP Web Security Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)

---

## ✍ SIGNATURE

*Prepared by:*  
🧑‍💻 Asibur Rahaman  
Web App Pentester & Burp Suite Enthusiast  
📅 Report Date: August 5, 2025  
📧 Email: asib51639@gmail.com  
🔗 GitHub: [github.com/Asibur-syber](https://github.com/Asibur-syber)  
🔗 LinkedIn: [linkedin.com/feed](https://linkedin.com/feed)

> "Test every assumption. Trust no header without validation."
