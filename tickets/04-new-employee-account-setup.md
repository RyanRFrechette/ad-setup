# Ticket 04 — New Employee Account Setup

**Status:** Resolved  
**Priority:** Medium  
**Category:** Onboarding / Provisioning

## Issue Description
New employee is starting and requires a domain user account, correct OU placement, group memberships, and a domain-joined workstation before their first day.

## Steps Taken
1. Collected required info: full name, job title, department, manager, start date
2. Created domain user account in Active Directory Users and Computers (ADUC)
3. Placed account in the correct Organizational Unit (OU) for the department
4. Set a temporary password with "User must change password at next logon"
5. Added user to appropriate security groups (e.g., domain users, department share access)
6. Confirmed workstation is domain-joined and user can log in successfully

## Resolution
<!-- Document what was provisioned -->
_Placeholder: list OU placement, groups assigned, and any special access granted._

## Notes
- Follow least-privilege: assign only the group memberships the role requires on day one
- PowerShell: `New-ADUser -Name "First Last" -SamAccountName flast -AccountPassword (...) -Enabled $true`
- Verify Group Policy applies correctly on first login with `gpresult /r`
