# Ticket 02 — Password Reset Request

**Status:** Resolved  
**Priority:** Medium  
**Category:** Account Management

## Issue Description
User has forgotten their password and is unable to sign in. Requests a manual password reset by the administrator.

## Steps Taken
1. Verified caller identity (employee ID, manager confirmation, or alternate contact)
2. Located user account in Azure Active Directory
3. Generated a temporary password meeting complexity requirements
4. Set "Require password change at next sign-in" flag
5. Communicated temporary password to user via secure channel

## Resolution
<!-- Document what fixed the issue -->
_Placeholder: describe resolution here._

## Notes
- Never share passwords over email in plain text; use a secure method
- Encourage user to enable Self-Service Password Reset (SSPR) to reduce future tickets
- Log all password reset actions per security policy
