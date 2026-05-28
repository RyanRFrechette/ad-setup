# Learning Notes — Active Directory User Support Lab

## Azure AD Fundamentals
- Azure Active Directory (now Entra ID) is Microsoft's cloud-based identity and access management service
- UPN (User Principal Name) is the login format: `user@domain.onmicrosoft.com`
- Accounts can be cloud-only or synced from on-premises AD via Azure AD Connect

## Key Concepts

### Account Lifecycle
- Create → assign groups → assign licenses → enable → offboard (disable → delete)
- Always disable before deleting to allow recovery window

### Smart Lockout
- Azure AD automatically locks accounts after repeated failed sign-ins
- Default threshold: 10 attempts; lockout duration starts at 1 minute
- Admins can unlock immediately via Portal or PowerShell

### Conditional Access
- Policies that enforce access rules (require MFA, block risky sign-ins, restrict by location)
- Can block users even with correct credentials — always check CA policies when troubleshooting

### SSPR (Self-Service Password Reset)
- Allows users to reset their own passwords without admin help
- Reduces help desk ticket volume significantly
- Requires users to register authentication methods in advance

## PowerShell Snippets

```powershell
# Unlock a user account (MSOnline module)
Set-MsolUser -UserPrincipalName user@domain.com -BlockCredential $false

# Reset password and force change at next login
Set-MsolUserPassword -UserPrincipalName user@domain.com -NewPassword "TempPass123!" -ForceChangePassword $true

# Check user account status
Get-MsolUser -UserPrincipalName user@domain.com | Select DisplayName, BlockCredential, IsLicensed
```

## Things to Explore Next
- [ ] Azure AD audit logs and sign-in logs
- [ ] MFA registration and Authenticator app setup
- [ ] Role-Based Access Control (RBAC) in Azure
- [ ] Azure AD joined vs. hybrid joined devices
