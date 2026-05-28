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
3. Opened Event Viewer on the domain controller, filtered Security log for Event ID 4740 (account lockout) to identify the source machine
4. In this scenario, Event ID 4740 would name the Caller Computer Name — the device generating the failed attempts
5. Investigated the source machine for stale saved credentials (common cause: mapped drive or app still using an old password)

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

Expected verification: `Get-ADUser jdoe -Properties LockedOut` returns `LockedOut: False`. User logs in successfully. Monitor for re-lockout — if it recurs immediately, a device with stale credentials is still active and needs to be addressed.

---

## What This Proves

- Can identify and unlock a locked domain account in ADUC and PowerShell
- Knows how to use Event ID 4740 to trace lockout source machines
- Understands stale cached credentials as a common re-lockout cause
- Goes beyond the immediate fix to prevent recurrence
