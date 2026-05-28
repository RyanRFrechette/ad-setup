# Ticket 03 — Account Locked Out

**Status:** Resolved  
**Priority:** High  
**Category:** Account Management  
**Environment:** Windows Server 2022 domain controller · Windows 10 client · AD DS lab domain

---

## Problem

User cannot log into their workstation. The login screen shows "Your account has been locked. Please contact your administrator." The user did not intentionally enter incorrect passwords repeatedly.

---

## Environment

- Domain controller: Windows Server 2022 running AD DS
- Client machine: Windows 10, domain-joined
- Account Lockout Policy: 5 failed attempts triggers lockout (configured via Default Domain Policy)

---

## Checks Performed

1. Opened ADUC, located the user account — lock icon confirmed the account was locked
2. Checked the Account tab: "Unlock account" checkbox was available, confirming lockout state
3. Opened Event Viewer on the domain controller, filtered Security log for Event ID 4740 (account lockout)
4. Event ID 4740 identified the source machine causing repeated failed authentications
5. Investigated the source machine — found a mapped network drive still using the user's old cached credentials

---

## Resolution

Unlocked the account in ADUC by checking "Unlock account" on the Account tab and clicking Apply. Remotely assisted the user in removing the stale saved credential from Windows Credential Manager on the source machine to prevent immediate re-lockout.

```powershell
# Equivalent PowerShell approach
Unlock-ADAccount -Identity jdoe
Get-ADUser jdoe -Properties LockedOut, BadLogonCount | Select LockedOut, BadLogonCount
```

---

## Verification

Confirmed `LockedOut` returned `False` in PowerShell. User logged in successfully. Monitored for re-lockout over the next 10 minutes — account remained unlocked.

---

## What This Proves

- Can identify and unlock a locked domain account in ADUC and PowerShell
- Knows how to use Event ID 4740 to trace lockout source machines
- Understands stale cached credentials as a common re-lockout cause
- Goes beyond the immediate fix to prevent recurrence
