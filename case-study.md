# Case Study: Active Directory User Support Lab

## Overview
Simulated help desk environment built on Windows Server Active Directory Domain Services (AD DS), hosted on Azure virtual machines. Covers user account management, access troubleshooting, and onboarding workflows in a domain environment.

## Environment
- **Platform:** Azure virtual machines (Windows Server domain controller + Windows client)
- **Directory Service:** Active Directory Domain Services (AD DS)
- **Tools:** Active Directory Users and Computers (ADUC), PowerShell, Remote Desktop Protocol (RDP), DNS Manager
- **Scope:** 5 simulated support tickets across common help desk scenarios

## Problem Statement
Entry-level IT support roles require hands-on experience resolving authentication, access, and account issues in a Windows Server Active Directory environment. This lab bridges that gap.

## Tickets Resolved
| # | Issue | Resolution |
|---|-------|-----------|
| 01 | User cannot log in | Verified account status, reset credentials in ADUC |
| 02 | Password reset request | Performed secure password reset via Active Directory |
| 03 | Account locked out | Identified lockout source, unlocked account in ADUC |
| 04 | New employee account setup | Created domain user, assigned groups and OUs |
| 05 | Domain / RDP access issue | Diagnosed connectivity, DNS, and permission gaps |

## Key Skills Demonstrated
- Active Directory Domain Services user and group management
- Account lockout investigation and remediation
- Domain user onboarding and OU placement
- DNS troubleshooting and RDP access resolution

## Outcome
All five tickets resolved with documented steps, simulating a production Windows domain help desk workflow.
