# Learning Notes — Active Directory User Support Lab

## AD DS Fundamentals
- Active Directory Domain Services (AD DS) is Microsoft's on-premises directory service running on Windows Server
- Stores user accounts, computer accounts, groups, and Group Policy in a centralized directory
- Domain controllers (DCs) handle authentication via Kerberos (port 88) and LDAP (port 389)

## Key Concepts

### Organizational Units (OUs)
- Containers within a domain used to organize users, computers, and groups
- Group Policy Objects (GPOs) are linked to OUs to apply settings to their members
- Place new users in the correct OU so they inherit the right policies

### Account Lifecycle
- Create in ADUC → assign to OUs and groups → enable → maintain → disable on offboard → delete after retention period
- Always disable before deleting to allow recovery

### Account Lockout Policy
- Configured via Group Policy (Default Domain Policy → Account Lockout Policy)
- Typical settings: threshold 5–10 attempts, 30-minute observation window, 30-minute lockout duration
- Event ID 4740 on the DC identifies the source machine that triggered the lockout

### DNS in a Windows Domain
- DNS is critical — clients must resolve the domain controller's hostname to authenticate
- The DC should be its own primary DNS server; clients should point to the DC for DNS
- Broken DNS is the most common cause of domain join failure and login errors

## PowerShell Snippets

```powershell
# Unlock a user account
Unlock-ADAccount -Identity username

# Reset password and force change at next login
Set-ADAccountPassword -Identity username -Reset -NewPassword (Read-Host -AsSecureString)
Set-ADUser -Identity username -ChangePasswordAtLogon $true

# Check account status
Get-ADUser username -Properties LockedOut, BadLogonCount, Enabled, PasswordExpired

# Create a new domain user
New-ADUser -Name "Jane Doe" -SamAccountName jdoe -UserPrincipalName jdoe@lab.local `
  -AccountPassword (Read-Host -AsSecureString) -Enabled $true -Path "OU=Staff,DC=lab,DC=local"

# Verify domain secure channel on a client
Test-ComputerSecureChannel -Verbose
```

## Things to Explore Next
- [ ] Group Policy Object (GPO) creation and linking
- [ ] Fine-Grained Password Policies
- [ ] FSMO roles on the domain controller
- [ ] Read-only domain controllers (RODC)
- [ ] Active Directory replication concepts
