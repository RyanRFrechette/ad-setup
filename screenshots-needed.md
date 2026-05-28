# Screenshot Workflow — Active Directory User Support Lab

> **Do not capture screenshots yet. Work through one ticket section at a time. Save locally first, add to repo after each batch, update README only after screenshots are verified.**

---

## Capture Workflow

1. Open the lab environment (Azure portal → start both VMs)
2. Work through one section at a time in the order below
3. Save screenshots locally with the suggested filenames before adding them to the repo
4. After completing each ticket's screenshots, add the images to the repo and update the relevant ticket file with `![description](images/filename.png)`
5. Update README only after the images are committed and verified rendering on GitHub
6. Do not skip ahead — capture Setup proof first to confirm the environment is healthy before practicing support scenarios

---

## Section 1 — Setup / Build Proof

These 5 screenshots are **already complete** and embedded in `README.md` via Imgur.

| # | Screenshot Name | What It Shows | Status | Filename / URL |
|---|---|---|---|---|
| 1 | Domain Controller Preparation | Windows Server VM setup and ICMP connectivity test between VMs | ✅ Done | https://i.imgur.com/UZliaOP.png |
| 2 | Active Directory Structure | ADUC showing OU structure and admin account created | ✅ Done | https://i.imgur.com/QpTonRy.png |
| 3 | Client Domain Join and Remote Access | Domain join confirmation dialog and RDP settings | ✅ Done | https://i.imgur.com/o5pLdr6.png |
| 4 | PowerShell User Creation | PowerShell ISE script running and result visible in ADUC | ✅ Done | https://i.imgur.com/MfT0bdg.png |
| 5 | Account Administration | ADUC showing account unlock / reset / disable / enable actions | ✅ Done | https://i.imgur.com/6VfpU4E.png |

---

## Section 2 — Ticket 01 · User Cannot Log In

| # | Screenshot Name | What to Capture | What This Proves | Suggested Filename |
|---|---|---|---|---|
| 1 | Failed Logon Event | Event Viewer on DC — Security log filtered to Event ID 4625, showing failed logon with source workstation and failure reason | Knows how to read Windows Security event logs to diagnose login failures | `ticket01-event-4625.png` |
| 2 | Account Status in ADUC | User account properties → Account tab showing account is enabled and not locked | Can inspect account state in ADUC as a first diagnostic step | `ticket01-account-status.png` |
| 3 | Successful Domain Login | Command Prompt on the client running `whoami`, output showing `LAB\username` | Confirms the domain login issue was resolved and domain authentication is working | `ticket01-whoami.png` |

---

## Section 3 — Ticket 02 · Password Reset Request

| # | Screenshot Name | What to Capture | What This Proves | Suggested Filename |
|---|---|---|---|---|
| 1 | Reset Password Dialog | ADUC — right-click user → Reset Password dialog with "User must change password at next logon" checked | Knows the correct ADUC workflow for a secure domain password reset | `ticket02-reset-password-dialog.png` |
| 2 | Forced Password Change Prompt | Windows login screen on the client showing the "You must change your password" prompt on first login | Confirms the reset was applied correctly with the forced-change flag | `ticket02-password-change-prompt.png` |

---

## Section 4 — Ticket 03 · Account Locked Out

| # | Screenshot Name | What to Capture | What This Proves | Suggested Filename |
|---|---|---|---|---|
| 1 | Locked Account in ADUC | ADUC showing the lock icon on the user account before unlock | Recognizes the visual lockout indicator in ADUC | `ticket03-account-locked.png` |
| 2 | Lockout Source Event | Event Viewer on DC — Security log filtered to Event ID 4740, showing Caller Computer Name (the source machine) | Understands how to trace lockout origin using Windows event logs | `ticket03-event-4740.png` |
| 3 | Unlock Confirmation | PowerShell output of `Get-ADUser jdoe -Properties LockedOut` showing `LockedOut: False` after unlock | Verifies the account was unlocked using PowerShell, not just assumed | `ticket03-unlocked-confirm.png` |

---

## Section 5 — Ticket 04 · New Employee Account Setup

| # | Screenshot Name | What to Capture | What This Proves | Suggested Filename |
|---|---|---|---|---|
| 1 | New User in ADUC OU | ADUC showing the new user account sitting inside the `_EMPLOYEES` OU | Can provision a domain account with correct OU placement | `ticket04-user-in-ou.png` |
| 2 | Group Membership Tab | User properties → Member Of tab in ADUC showing the correct security group assigned | Understands group-based access control and applies least-privilege | `ticket04-group-membership.png` |
| 3 | Group Policy Applied | `gpresult /r` output on the client showing Group Policy from the `_EMPLOYEES` OU is applied | Confirms OU placement drives the correct policy and access scope | `ticket04-gpresult.png` |

---

## Section 6 — Ticket 05 · Domain / RDP Access Issue

| # | Screenshot Name | What to Capture | What This Proves | Suggested Filename |
|---|---|---|---|---|
| 1 | NSG Rules in Azure Portal | Azure portal → NSG inbound rules showing the RDP rule (port 3389) in place | Understands Azure NSG as the network-layer control for VM access | `ticket05-nsg-rdp-rule.png` |
| 2 | DNS Failure Then Success | Two `nslookup lab.local` results side by side or in sequence — one failing (wrong DNS), one succeeding (DC as DNS) | Demonstrates DNS as root cause of domain join failure and how to verify the fix | `ticket05-nslookup-fix.png` |
| 3 | Domain Join Confirmation | Windows dialog showing "Welcome to the lab.local domain" after a successful domain join | Confirms the domain join completed after correcting DNS | `ticket05-domain-join-confirm.png` |
| 4 | Active RDP Session | Remote Desktop session connected to the domain-joined VM showing the Windows desktop | Proves RDP access works end-to-end after NSG and permission fixes | `ticket05-rdp-connected.png` |
