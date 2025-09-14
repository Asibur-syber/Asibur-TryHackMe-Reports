
# 🛡 Web Application Penetration Test Report — Room #18 (Broken Authentication) — Premium (Improved)

<p align="center">  
  <img src="https://i.imgur.com/do3UY0q.jpeg" alt="Cybersecurity Portfolio Banner" width="100%">  
</p>

**Client:** TryHackMe – Room #18 (Broken Authentication) — Educational  
**Project:** Authentication & Logic Flaw Vulnerability Assessment  
**Date:** August 31, 2025  
**Version:** Premium — Improved  
**Prepared by:** Asibur Rahaman — Ethical Hacker & Cybersecurity Specialist  
**Contact:** 📧 asib51639@gmail.com | 🌐 GitHub | 🔗 LinkedIn  

---

## TL;DR (HackerOne / Executive 2–3 lines)

- **Vulnerability:** Broken Authentication via re-registration logic. Registering usernames with leading whitespace (e.g., `" darren"`) bypasses uniqueness checks and allows session creation for an existing account.  
- **Impact:** Account takeover → session issued for victim account (sensitive data / flags exposure).  
- **Fix (short):** Trim and normalize usernames server-side (e.g., `LOWER(TRIM(username)))`, enforce DB uniqueness on normalized value, and verify session issuance logic.  

---

## 1. Executive Summary

A targeted test of the application at `10.201.90.135:8888` revealed a Broken Authentication vulnerability (**CWE-287**). The registration endpoint accepts usernames with leading whitespace and treats them as distinct, allowing an attacker to create accounts that effectively map to existing users and obtain session tokens granting access to those accounts.

- **Severity:** Medium — CVSS 6.5  
- **CVSS Vector:** `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:L/A:N`  
- **Recommendation:** Apply username normalization (trim + lowercase), add DB-level uniqueness on normalized username, and verify session creation logic does not authenticate unverified identities.  

---

## 2. Scope & Engagement

- **In-Scope:**  
  - IP: `10.201.90.135`  
  - Endpoints: `/register`, `/login`  

- **Out-of-Scope:** SQLi, XSS, DoS  

- **Methodology:** Recon → Input testing → Exploitation (non-destructive) → Documentation (OWASP/NIST referencing)  

---

## 3. Findings Summary

| ID  | Vulnerability                                | CVSS | CWE     | Status    |
|-----|----------------------------------------------|------|---------|-----------|
| 01  | Broken Authentication — Re-registration flaw | 6.5  | CWE-287 | Confirmed |

---

## 4. Detailed Vulnerability Analysis

**Vulnerability:** Re-registration bypass due to insufficient input normalization.  
**CWE:** 287 — Improper Authentication  

**Attack Flow:**  
1. Attacker attempts to register existing username `darren` → server rejects (user exists).  
2. Attacker registers ` username=%20darren` (leading space) → registration succeeds.  
3. Server issues session cookie for the new account which maps to Darren’s dashboard (account takeover).  

**PoC (Concise):**  
1. Navigate: `http://10.201.90.135:8888/register`  
2. Register `darren` → error.  
3. Register `" darren"` (leading space) → success.  
4. Access dashboard → victim’s data visible.  

---

## 5. Technical Evidence (Raw & Masked)

> **Note:** Attach full Burp `.txt` export in `evidence/` folder.  

**HTTP Request (captured via Burp):**
```http
POST /register HTTP/1.1
Host: 10.201.90.135:8888
Content-Type: application/x-www-form-urlencoded
Content-Length: 32

username=%20darren&password=test123

Server Response (truncated):

HTTP/1.1 302 Found
Set-Cookie: session=REDACTED; HttpOnly; Path=/
Location: /dashboard

Proof: Session cookie granted → /dashboard → victim’s data shown.


---

6. Reproduction (Exact commands)

cURL PoC:

curl -i -X POST 'http://10.201.90.135:8888/register' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  --data-urlencode 'username= darren' \
  --data 'password=test123'

Burp PoC: Intercept registration → replace username=darren with username=%20darren.


---

7. Root Cause Analysis

Input not normalized (whitespace preserved).

DB uniqueness uses raw username → "darren" ≠ " darren".

Session issued without additional verification (no email check).



---

8. Remediation (Technical)

Short-term Fix:

Normalize usernames:

LOWER(TRIM(input_username))

Enforce uniqueness at DB level.


PostgreSQL Example:

ALTER TABLE users ADD COLUMN username_norm TEXT;
UPDATE users SET username_norm = LOWER(TRIM(username));
CREATE UNIQUE INDEX ux_users_username_norm ON users (username_norm);

MySQL Example:

ALTER TABLE users ADD COLUMN username_norm VARCHAR(255) GENERATED ALWAYS AS (LOWER(TRIM(username))) STORED;
CREATE UNIQUE INDEX ux_users_username_norm ON users (username_norm);

App-side (Node.js/Express):

const normalized = req.body.username.trim().toLowerCase();

Additional Controls:

Require email verification.

Rate-limit registration.

Log & monitor suspicious registrations.



---

9. Verification Steps (Post-fix)

1. Register " darren" → rejected.


2. Ensure LOWER(TRIM(username)) uniqueness enforced.


3. Session only for verified accounts.



Automated Verification Script:

for u in "darren" " darren" "Darren" "darren  "; do
  curl -s -o /dev/null -w "%{http_code} $u\n" \
  -X POST 'http://10.201.90.135:8888/register' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  --data-urlencode "username=$u" --data "password=test123"
done


---

10. Proof & Screenshots (Placeholders)

SS01_login_page.png — Login page

SS02_rereg_attempt.png — Registration attempt blocked

SS03_burp_intercept.png — Burp intercept showing %20darren

SS04_exploit_outcome.png — Dashboard access


![SS01 – Login Page](screenshots/SS01_login_page.png)  
![SS02 – Re-Registration Attempt](screenshots/SS02_rereg_attempt.png)  
![SS03 – Burp Intercept](screenshots/SS03_burp_intercept.png)  
![SS04 – Exploit Outcome](screenshots/SS04_exploit_outcome.png)


---

11. Business Impact

Account Takeover → attacker hijacks victim account.

Data Exposure → sensitive info/flags leaked.

Reputation Risk → compliance & trust violations.



---

12. Risk Matrix & Prioritization

Likelihood: Medium

Impact: High

Overall Risk: 🔴 High Priority Patch Required



---

13. Appendix — Additional Artifacts

evidence/burp_export.txt — Burp raw logs

evidence/registration_tests.csv — test results

Example patch PR (showing .trim().toLowerCase() fix)



---

14. Delivery Note (Client-facing)

This report is produced for educational purposes (TryHackMe lab). Options:

Convert to HackerOne disclosure (TL;DR + PoC + Impact).

Export to PDF package (cover, TOC, screenshots).

Create Fiverr gig package (3 tiers + delivery templates).



---

15. Fiverr / Marketplace Ready

Gig Title: Premium Web App Vulnerability Report & PoC — Authentication Logic

Basic ($15): One-page TL;DR + 1 screenshot + remediation summary

Standard ($45): Full PDF + 4 screenshots + remediation steps

Premium ($120): Full report + raw evidence + 1-week support


Proposal Example:

> Hello — I reviewed your application and produced a premium, action-ready report showing an authentication logic flaw. I can deliver a full PDF with PoC and remediation within 48 hours and help verify the fix. Price: $45 (Standard). Shall I proceed?




---

16. Next Steps

1. Embed real screenshots → export PDF.


2. Generate HackerOne-ready short disclosure.


3. Create Fiverr gig descriptions & proposals.




---

Prepared by:
Asibur Rahaman — Ethical Hacker & Cybersecurity Specialist
Version: Premium (Improved) — 2025-08-31

End of document.

---
