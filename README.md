<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

# Active Directory User Support Lab on Azure

## Recruiter TL;DR

This portfolio lab demonstrates foundational Windows administration and help desk account-support skills by building a Windows Server Active Directory Domain Services (AD DS) environment on Azure virtual machines. It proves hands-on practice with domain controller setup, DNS, domain joining, organizational units, user/admin accounts, Remote Desktop access, and common support tasks — password resets, account unlocks, disabling and enabling users.

> Full case study: [case-study.md](case-study.md) | Resume bullets: [resume-bullets.md](resume-bullets.md)

---

## Business Scenario

A small organization needs a Windows domain where employees sign into domain-joined computers, admins manage users centrally, and support staff resolve account access issues.

This lab simulates that environment:

- Windows Server 2022 domain controller with AD DS and DNS
- Windows 10 client machine joined to the domain
- Organizational units, user accounts, and a domain admin account
- Remote Desktop access for administration and user support
- Documented account support workflows

| Area | What this lab demonstrates |
|---|---|
| Windows Server | Installed and configured a domain controller on Azure VMs |
| Active Directory | Created OUs, users, admin accounts, and domain access structure |
| DNS / Domain Join | Configured client DNS so a Windows machine could join the domain |
| Remote Support | Used RDP to manage cloud-hosted Windows machines |
| User Administration | Account unlocks, password resets, enabling and disabling users |
| PowerShell | Scripted account management tasks alongside GUI administration |
| Cloud Fundamentals | Built the full lab using Azure virtual machines and networking |

---

## Lab Architecture

Two Azure virtual machines connected on a private virtual network — one Windows Server domain controller, one domain-joined Windows client.

See full diagram: [diagrams/architecture.md](diagrams/architecture.md)

```
┌──────────────────────────────────────────────────┐
│              Azure Virtual Network                │
│                                                  │
│  ┌──────────────────────┐  ┌──────────────────┐  │
│  │  Windows Server VM   │  │  Windows 10/11   │  │
│  │  Domain Controller   │  │  Client VM       │  │
│  │                      │  │                  │  │
│  │  - AD DS             │  │  - Domain-joined │  │
│  │  - DNS Server        │  │  - RDP access    │  │
│  │  - ADUC / GPMC       │  │  - User logins   │  │
│  └──────────────────────┘  └──────────────────┘  │
│                                                  │
│  Network Security Group (NSG)                    │
│  Inbound: RDP (3389) from admin IP               │
└──────────────────────────────────────────────────┘
```

**Authentication flow:** User logs in → Windows client contacts DC via Kerberos (port 88) → AD DS authenticates → Group Policy applies → Session starts

---

## Tools Used

| Tool | Purpose |
|---|---|
| Microsoft Azure Virtual Machines | Host Windows Server and Windows client |
| Windows Server 2022 | Domain controller OS |
| Windows 10 | Domain-joined client OS |
| Active Directory Domain Services (AD DS) | Directory and identity management |
| Active Directory Users and Computers (ADUC) | GUI user/group/OU administration |
| DNS Manager | Domain name resolution for domain join and auth |
| Remote Desktop Protocol (RDP) | Remote management of VMs |
| PowerShell / PowerShell ISE | Scripted account operations |

---

## Build Steps

1. Deployed Windows Server and Windows 10 VMs in Azure on a shared virtual network
2. Configured network connectivity and enabled ICMP for connectivity validation
3. Promoted the Windows Server VM to a domain controller with AD DS and DNS
4. Created a new Active Directory forest and domain
5. Created organizational units for employees and administrators
6. Created a domain admin account and assigned domain admin rights
7. Configured the Windows 10 client's DNS to point to the domain controller
8. Joined the Windows client to the domain
9. Configured Remote Desktop access for domain users
10. Practiced account administration: password resets, unlocks, disabling, enabling

---

## Support Tasks Practiced

These map directly to common help desk tickets:

- User cannot log into their workstation
- Password reset request
- Account locked out after failed login attempts
- New employee needs a domain account and OU placement
- Workstation cannot join the domain (DNS misconfiguration)
- Remote Desktop access not working (NSG rule or group membership)

---

## Ticket Evidence

Full ticket documentation: [tickets/](tickets/)

| Ticket | Issue | File |
|---|---|---|
| 01 | User cannot log in | [tickets/01-user-cannot-log-in.md](tickets/01-user-cannot-log-in.md) |
| 02 | Password reset request | [tickets/02-password-reset-request.md](tickets/02-password-reset-request.md) |
| 03 | Account locked out | [tickets/03-account-locked.md](tickets/03-account-locked.md) |
| 04 | New employee account setup | [tickets/04-new-employee-account-setup.md](tickets/04-new-employee-account-setup.md) |
| 05 | Domain / RDP access issue | [tickets/05-domain-or-rdp-access-issue.md](tickets/05-domain-or-rdp-access-issue.md) |

### 1. Domain Controller Preparation

<p>
<img src="https://i.imgur.com/UZliaOP.png" height="80%" width="80%" alt="Active Directory setup steps"/>
</p>

Prepared the Windows Server VM for domain controller duties and verified network communication between VMs. Configured Windows Defender Firewall rules to allow ICMP so connectivity could be confirmed before domain configuration.

### 2. Active Directory Structure and Admin User

<p>
<img src="https://i.imgur.com/QpTonRy.png" height="80%" width="80%" alt="Active Directory users and computers"/>
</p>

Created organizational units for employees and administrators, then created a domain admin account in ADUC. This is the identity structure used in most Windows business environments.

### 3. Client Domain Join and Remote Access

<p>
<img src="https://i.imgur.com/o5pLdr6.png" height="80%" width="80%" alt="Domain join and remote desktop settings"/>
</p>

Joined the Windows client to the domain and configured Remote Desktop access for domain users — a common task when setting up or troubleshooting company workstations.

### 4. PowerShell User Creation and Verification

<p>
<img src="https://i.imgur.com/MfT0bdg.png" height="80%" width="80%" alt="PowerShell user administration"/>
</p>

Used PowerShell ISE for account creation and verified results in ADUC. Demonstrates comfort with both GUI-based and script-assisted administration.

### 5. Account Administration Practice

<p>
<img src="https://i.imgur.com/6VfpU4E.png" height="80%" width="80%" alt="Active Directory account management"/>
</p>

Practiced common support actions: unlocking accounts, resetting passwords, disabling accounts, and enabling accounts — directly relevant to help desk and desktop support roles.

---

## Lessons Learned

- Active Directory depends heavily on correct DNS configuration — the client must point to the DC for name resolution, not a public resolver
- Domain join failures almost always trace back to DNS before anything else
- Account access issues follow a structured resolution path: user status → password → group membership → machine domain status → network connectivity
- Azure VMs are an effective and affordable way to practice Windows administration without physical hardware
- Clear documentation makes troubleshooting repeatable and easier to hand off to another technician

---

## Resume Value

See [resume-bullets.md](resume-bullets.md) for ready-to-use resume bullets and ATS keywords tailored to help desk, desktop support, and junior sysadmin roles.

**Core competencies this lab proves:**
- Windows Server domain controller configuration
- Active Directory user, group, and OU management
- DNS troubleshooting in a Windows domain environment
- RDP-based remote administration
- Common account support workflows (reset, unlock, disable, enable, provision)

---

## Related Training

This lab extends foundational IT support concepts from the Google IT Support Professional Certificate into identity management, Windows domain administration, and cloud-based lab practice.

---

## Project Documents

| Document | Description |
|---|---|
| [case-study.md](case-study.md) | Hiring-manager case study — environment, what I built, troubleshooting approach |
| [resume-bullets.md](resume-bullets.md) | Resume bullets, LinkedIn summary, GitHub summary, ATS keyword bank |
| [diagrams/architecture.md](diagrams/architecture.md) | Lab architecture diagram and authentication flow |
| [screenshots-needed.md](screenshots-needed.md) | Audit of existing screenshot evidence and optional captures to strengthen the repo |
| [tickets/](tickets/) | Five simulated help desk support scenarios with structured documentation |

> **Note:** The five support tickets are simulated scenarios practiced in the lab environment, not production incidents. Each is documented with the diagnostic process and resolution path that would apply to a real-world equivalent.

---

## Status

**Portfolio-ready.** Lab environment built and documented with screenshot evidence. Five help desk support scenarios documented as structured tickets. Case study and resume materials included.

Planned additions: Group Policy Object configuration, shared folder permissions, account lockout policy testing, and deeper multi-step troubleshooting scenarios.
