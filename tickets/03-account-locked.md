# Ticket 03 — Account Locked Out

**Status:** Resolved  
**Priority:** High  
**Category:** Account Management

## Issue Description
User's domain account has been locked after multiple failed sign-in attempts. User cannot authenticate until the account is unlocked by an administrator.

## Steps Taken
1. Confirmed lockout in Active Directory Users and Computers (ADUC) — lock icon on account
2. Reviewed Security event logs on the domain controller (Event ID 4740) to identify the source machine
3. Checked for stale cached credentials on the user's devices (mapped drives, saved passwords)
4. Unlocked the account in ADUC (Account tab → Unlock account)
5. Advised user to update saved credentials on all devices

## Resolution
<!-- Document what fixed the issue -->
_Placeholder: describe resolution here._

## Notes
- PowerShell: `Unlock-ADAccount -Identity username`
- Use `Get-ADUser username -Properties LockedOut,BadLogonCount` to inspect account state
- Repeated lockouts often point to a device with stale cached credentials, not a user error
- Review domain Account Lockout Policy via Group Policy (gpmc.msc) for threshold settings
