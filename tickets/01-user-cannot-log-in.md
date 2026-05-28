# Ticket 01 — User Cannot Log In

**Status:** Resolved  
**Priority:** High  
**Category:** Authentication

## Issue Description
User reports they cannot log into their domain-joined Windows workstation. Login fails with an error or credentials are rejected at the Windows login screen.

## Steps Taken
1. Verified user account exists in Active Directory Users and Computers (ADUC)
2. Confirmed account is not disabled or expired
3. Checked account logon hours and workstation restrictions
4. Verified the workstation is still domain-joined and can reach the domain controller
5. Confirmed DNS is resolving the domain controller correctly on the client

## Resolution
<!-- Document what fixed the issue -->
_Placeholder: describe resolution here._

## Notes
- Common causes: disabled account, expired password, domain trust issue, DNS failure, workstation dropped from domain
- Check Event Viewer on the client (Security log, Event ID 4625) for detailed failure reasons
- Use `nltest /sc_verify:domain.local` to verify the secure channel to the DC
