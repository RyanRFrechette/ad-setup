# Ticket 03 — Account Locked Out

**Status:** Resolved  
**Priority:** High  
**Category:** Account Management

## Issue Description
User account has been locked after multiple failed sign-in attempts. User is unable to authenticate until the account is unlocked.

## Steps Taken
1. Confirmed lockout in Azure AD via user account status
2. Reviewed Azure AD Sign-in logs to identify source of failed attempts
3. Checked for signs of unauthorized access or credential stuffing
4. Unlocked the account in Azure Portal (or via PowerShell)
5. Advised user to update any saved passwords on devices or apps

## Resolution
<!-- Document what fixed the issue -->
_Placeholder: describe resolution here._

## Notes
- PowerShell: `Set-MsolUser -UserPrincipalName user@domain.com -BlockCredential $false`
- Investigate repeated lockouts — may indicate a compromised credential
- Review Smart Lockout settings in Azure AD for threshold tuning
