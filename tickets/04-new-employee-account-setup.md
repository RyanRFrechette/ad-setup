# Ticket 04 — New Employee Account Setup

**Status:** Resolved  
**Priority:** Medium  
**Category:** Onboarding / Provisioning  
**Environment:** Windows Server 2022 domain controller · Windows 10 client · AD DS lab domain

---

## Problem

A new employee is starting. HR submits an onboarding request: the employee needs a domain user account, correct OU placement, group memberships, and a working login on a domain-joined workstation before their first day.

---

## Environment

- Domain controller: Windows Server 2022 running AD DS
- Client machine: Windows 10, domain-joined
- Active Directory structure: OUs for `_EMPLOYEES` and `_ADMINS`; security group for department share access

---

## Checks Performed

1. Collected required info from HR: full name, job title, department, manager, start date
2. Confirmed no duplicate `SamAccountName` exists in ADUC before creating the account
3. Identified the correct OU for the department (`_EMPLOYEES`)
4. Identified the security groups the role requires on day one

---

## Resolution

Created the domain user account in ADUC: right-click OU → New → User. Filled in first name, last name, and logon name (`jdoe@lab.local`). Set a temporary password with "User must change password at next logon" checked.

Moved account to the correct OU and added to the department security group.

```powershell
# Equivalent PowerShell approach
New-ADUser -Name "Jane Doe" `
  -SamAccountName jdoe `
  -UserPrincipalName "jdoe@lab.local" `
  -Path "OU=_EMPLOYEES,DC=lab,DC=local" `
  -AccountPassword (ConvertTo-SecureString "TempPass1!" -AsPlainText -Force) `
  -ChangePasswordAtLogon $true `
  -Enabled $true

Add-ADGroupMember -Identity "SalesShare" -Members jdoe
```

---

## Verification

Logged into the domain-joined Windows 10 client as the new user. Confirmed:
- Prompted to change password on first logon
- `gpresult /r` showed correct Group Policy applied for the `_EMPLOYEES` OU
- User had access to expected shared resources, not beyond

---

## What This Proves

- Can provision a domain user account end-to-end in ADUC and PowerShell
- Understands OU structure and its role in Group Policy application
- Applies least-privilege by assigning only required group memberships on day one
- Verifies provisioning outcomes rather than assuming success
