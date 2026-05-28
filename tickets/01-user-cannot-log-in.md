# Ticket 01 — User Cannot Log In

**Status:** Resolved  
**Priority:** High  
**Category:** Authentication  
**Environment:** Windows Server 2022 domain controller · Windows 10 client · AD DS lab domain

---

## Problem

User reports they cannot log into their domain-joined Windows 10 workstation. The Windows login screen rejects their credentials with "The user name or password is incorrect" even though the user believes the password is correct.

---

## Environment

- Domain controller: Windows Server 2022 running AD DS and DNS
- Client machine: Windows 10, domain-joined
- User account managed in Active Directory Users and Computers (ADUC)

---

## Checks Performed

1. Opened ADUC on the domain controller and located the user account
2. Confirmed account was not disabled — checked Account tab for disabled flag
3. Confirmed password was not expired — checked "Password never expires" and last set date
4. Checked account logon hours restrictions — no restrictions applied
5. On the client, ran `nltest /sc_verify:lab.local` to confirm the secure channel to the DC was intact
6. Ran `nslookup lab.local` on the client to verify DNS was resolving the domain controller
7. Reviewed Security event log on the domain controller for Event ID 4625 (failed logon)

---

## Resolution

In this scenario, Event ID 4625 reveals the failure reason (wrong password, account restriction, or logon type mismatch). The documented resolution path is to reset the domain password via ADUC (right-click user → Reset Password) with "User must change password at next logon" checked, then deliver the temporary password to the user securely.

---

## Verification

Expected verification: user logs into the domain-joined workstation with the temporary password, is immediately prompted to set a new password, and can confirm domain authentication by running `whoami` — expected output: `LAB\username`.

---

## What This Proves

- Can navigate ADUC to inspect and manage a domain user account
- Understands the structured login failure diagnostic process (account status → password → DNS → secure channel → event logs)
- Can perform a password reset in Active Directory and communicate it securely
