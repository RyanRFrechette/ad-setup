# Case Study: Active Directory User Support Lab on Azure

## Overview

A self-directed portfolio lab demonstrating the Windows Server Active Directory skills most commonly tested in help desk and IT support interviews. I built a two-VM Windows domain on Azure, practiced the administrative workflows that appear in real support queues, and documented five simulated support scenarios as structured tickets.

---

## Business Problem

Entry-level IT support roles expect candidates who have actually touched Active Directory — not just read about it. Most people without enterprise experience have no way to demonstrate that they can unlock an account, trace a lockout to its source, provision a new user, or fix a domain join failure. This lab closes that gap with a working domain environment and documented support workflows.

---

## Lab Environment

| Component | Details |
|---|---|
| Domain controller | Windows Server 2022 VM on Azure, running AD DS and DNS |
| Client machine | Windows 10 VM on Azure, domain-joined |
| Networking | Azure Virtual Network with NSG controlling RDP access |
| Administration | Active Directory Users and Computers (ADUC), DNS Manager, PowerShell |
| Domain | `lab.local` — single-domain forest |

---

## What I Built

Starting from two blank Azure VMs, I:

1. Configured a private virtual network and validated connectivity between machines
2. Promoted the Windows Server VM to a domain controller with AD DS and DNS
3. Created the `lab.local` domain forest
4. Built an OU structure for employees and administrators
5. Created a domain admin account and assigned domain admin rights
6. Configured the Windows 10 client's DNS to point to the domain controller
7. Joined the Windows 10 client to the domain
8. Enabled RDP access for domain users and managed NSG rules in Azure
9. Practiced account administration: password resets, account unlocks, disabling, enabling, and new user provisioning

All build steps are documented with screenshots in [README.md](README.md).

---

## Support Workflows Practiced

Five simulated help desk scenarios, each documented as a structured ticket with problem, checks performed, resolution path, and verification steps:

| Ticket | Scenario | Core Skill |
|---|---|---|
| [01](tickets/01-user-cannot-log-in.md) | User cannot log into domain workstation | Login failure diagnosis, password reset |
| [02](tickets/02-password-reset-request.md) | User forgot domain password | Secure credential reset in ADUC and PowerShell |
| [03](tickets/03-account-locked.md) | Account locked after repeated failures | Event ID 4740, lockout source tracing, unlock |
| [04](tickets/04-new-employee-account-setup.md) | New employee account setup | User provisioning, OU placement, group assignment |
| [05](tickets/05-domain-or-rdp-access-issue.md) | RDP timeout and domain join failure | NSG rules, DNS misconfiguration, secure channel |

---

## Troubleshooting Approach

Every ticket follows the same structured diagnostic pattern used in real support environments:

1. **Scope the problem** — is this one user, one machine, or a broader issue?
2. **Check the account** — status, lockout, expiry, group membership in ADUC
3. **Check the machine** — domain join status, DNS resolution, secure channel to DC
4. **Check the network** — NSG rules, connectivity between VMs, RDP access
5. **Check the logs** — Security event log on the DC (Event ID 4625, 4740) for root cause
6. **Fix and verify** — apply the resolution, then confirm the outcome before closing

---

## Outcome

The lab environment was successfully built and is documented with screenshot evidence. Five support scenarios were practiced and written up as realistic help desk tickets with documented resolution paths. The project demonstrates both the technical skills to build a Windows domain and the process discipline to work through support issues methodically.

---

## Skills Demonstrated

- Windows Server domain controller installation and configuration
- Active Directory Domain Services — users, groups, OUs, and Group Policy basics
- DNS configuration for domain name resolution and client domain join
- Remote Desktop Protocol access management (Azure NSG rules + AD group membership)
- Account support operations: password reset, account unlock, disable, enable, provision
- PowerShell account management (`New-ADUser`, `Unlock-ADAccount`, `Set-ADAccountPassword`, `Get-ADUser`)
- Structured troubleshooting documentation suitable for a help desk ticketing system
- Azure virtual machine and virtual network fundamentals
