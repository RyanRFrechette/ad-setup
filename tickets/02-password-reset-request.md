# Ticket 02 — Password Reset Request

**Status:** Resolved  
**Priority:** Medium  
**Category:** Account Management  
**Environment:** Windows Server 2022 domain controller · Windows 10 client · AD DS lab domain

---

## Problem

User has forgotten their domain password and cannot log into their workstation or any domain resources. Calls the help desk requesting a manual password reset.

---

## Environment

- Domain controller: Windows Server 2022 running AD DS
- Client machine: Windows 10, domain-joined
- User account managed in Active Directory Users and Computers (ADUC)

---

## Checks Performed

1. Verified caller identity — confirmed name, department, and manager before proceeding
2. Located the user account in ADUC and confirmed it was active and not locked
3. Reviewed domain password policy (minimum length, complexity, history) via Default Domain Policy in Group Policy Management
4. Confirmed the user had no active logon sessions that would be disrupted by the reset

---

## Resolution

Right-clicked the user in ADUC → Reset Password. Set a temporary password meeting domain complexity requirements (8+ characters, uppercase, lowercase, number, symbol). Checked "User must change password at next logon." Delivered the temporary password to the user verbally — not over email.

```powershell
# Equivalent PowerShell approach
Set-ADAccountPassword -Identity jdoe -Reset -NewPassword (ConvertTo-SecureString "TempPass1!" -AsPlainText -Force)
Set-ADUser -Identity jdoe -ChangePasswordAtLogon $true
```

---

## Verification

User logged in with the temporary password, was immediately prompted to set a new password, and confirmed access to their workstation and shared drives.

---

## What This Proves

- Understands identity verification before performing account actions
- Can reset a domain user password in both ADUC and PowerShell
- Knows domain password policy constraints and how to enforce them
- Follows secure credential delivery practices
