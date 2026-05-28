# Screenshot Audit — Active Directory User Support Lab

> **Do not capture screenshots yet — screenshot time comes after review.**

---

## Existing Evidence (Already in README)

These 5 screenshots are already embedded in `README.md` via Imgur and cover the lab build phase:

| # | Description | URL |
|---|---|---|
| 1 | Domain Controller Preparation — Windows Server VM setup and ICMP connectivity test | https://i.imgur.com/UZliaOP.png |
| 2 | Active Directory Structure — ADUC showing OUs and admin account | https://i.imgur.com/QpTonRy.png |
| 3 | Client Domain Join and Remote Access — domain join dialog and RDP settings | https://i.imgur.com/o5pLdr6.png |
| 4 | PowerShell User Creation — PowerShell ISE script and ADUC verification | https://i.imgur.com/MfT0bdg.png |
| 5 | Account Administration — ADUC showing account unlock/reset/disable/enable actions | https://i.imgur.com/6VfpU4E.png |

---

## Optional Screenshots That Would Strengthen the Repo

These are missing but would add ticket-level evidence. Capture these when returning to the lab environment.

### Ticket 01 — User Cannot Log In
- [ ] Event Viewer on DC filtered to Event ID 4625 showing a failed logon with the source workstation
- [ ] ADUC account properties tab showing account status (enabled, not locked)
- [ ] Successful domain login (`whoami` output in Command Prompt showing `LAB\username`)

### Ticket 02 — Password Reset
- [ ] ADUC Reset Password dialog with "User must change password at next logon" checked
- [ ] Windows login screen prompting the user to set a new password after first login with temp password

### Ticket 03 — Account Locked Out
- [ ] ADUC account showing the lock icon before unlock
- [ ] Event Viewer on DC filtered to Event ID 4740 showing lockout source machine name
- [ ] PowerShell output of `Get-ADUser` confirming `LockedOut: False` after unlock

### Ticket 04 — New Employee Account Setup
- [ ] ADUC showing the new user account inside the `_EMPLOYEES` OU
- [ ] Group membership tab in ADUC showing the user added to the correct security group
- [ ] `gpresult /r` output on the client showing Group Policy applied from the correct OU

### Ticket 05 — Domain / RDP Access Issue
- [ ] Azure portal showing the NSG inbound rules before and after adding the RDP rule
- [ ] `nslookup lab.local` output showing DNS failure (pointing to 8.8.8.8) then success (pointing to DC)
- [ ] "Welcome to the lab.local domain" confirmation dialog after successful domain join
- [ ] Successful RDP session connected to the domain-joined VM

---

## Priority Order for Capture

If time is limited, prioritize in this order:
1. Event ID 4740 lockout source (Ticket 03) — shows investigative depth
2. NSG rule fix (Ticket 05) — shows Azure + AD together
3. New user in ADUC OU (Ticket 04) — shows provisioning workflow
4. `whoami` domain login proof (Ticket 01) — simple but concrete
5. Password reset dialog (Ticket 02) — straightforward to capture
