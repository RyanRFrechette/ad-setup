# Ticket 01 — User Cannot Log In

**Status:** Resolved  
**Priority:** High  
**Category:** Authentication

## Issue Description
User reports they cannot log into their workstation or Azure-joined device. Login fails with an error or the credentials are rejected.

## Steps Taken
1. Verified user account exists in Azure Active Directory
2. Confirmed account is not disabled or deleted
3. Checked for active sign-in restrictions or Conditional Access policies
4. Verified correct UPN (User Principal Name) format
5. Tested sign-in from Azure Portal to isolate the issue

## Resolution
<!-- Document what fixed the issue -->
_Placeholder: describe resolution here._

## Notes
- Common causes: incorrect UPN, expired password, MFA not configured, Conditional Access block
- Check Azure AD Sign-in logs for detailed error codes
