# Ticket 02 — Password Reset Request

**Status:** Resolved  
**Priority:** Medium  
**Category:** Account Management

## Issue Description
User has forgotten their domain password and is unable to sign into their workstation or domain resources. Requests a manual password reset by the administrator.

## Steps Taken
1. Verified caller identity (employee ID, manager confirmation, or in-person verification)
2. Located user account in Active Directory Users and Computers (ADUC)
3. Reset password to a temporary value meeting domain password policy requirements
4. Checked "User must change password at next logon" in ADUC
5. Communicated temporary password to user via secure channel

## Resolution
<!-- Document what fixed the issue -->
_Placeholder: describe resolution here._

## Notes
- Never share passwords over email in plain text; deliver in person or via secure method
- Confirm domain password policy (minimum length, complexity, history) before resetting
- PowerShell: `Set-ADAccountPassword -Identity username -Reset -NewPassword (Read-Host -AsSecureString)`
