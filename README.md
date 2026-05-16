<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

# Active Directory Lab: Domain Controller and User Management in Azure

## Recruiter TL;DR

This repo demonstrates foundational Windows administration by building an Active Directory domain lab on Azure VMs. It proves hands-on practice with domain controller setup, DNS, domain joining, organizational units, user/admin accounts, Remote Desktop access, and common account support tasks like password resets, unlocks, disabling, and enabling users.

## Project Summary

This lab demonstrates a working Windows domain environment built on Microsoft Azure virtual machines. I configured a Windows Server domain controller, joined a Windows client to the domain, created organizational units and users, configured DNS/domain connectivity, enabled remote access, and practiced common account administration tasks.

This is a portfolio project for help desk, desktop support, cloud support, and junior systems administrator roles. It shows that I understand how business users, domain accounts, client machines, DNS, Remote Desktop, and Active Directory all connect in a real support environment.

## Hiring Manager Snapshot

| Area | What this lab demonstrates |
|---|---|
| Windows Server | Installed and configured a domain controller in a lab environment |
| Active Directory | Created OUs, users, admin accounts, and domain access structure |
| DNS / Domain Join | Configured client DNS so a Windows machine could join the domain |
| Remote Support | Used RDP to manage cloud-hosted Windows machines |
| User Administration | Practiced account unlocks, password resets, enabling/disabling users |
| PowerShell | Used scripting concepts to support user/account management |
| Cloud Fundamentals | Built the lab using Azure virtual machines and networking |

## Business Scenario

A small organization needs a basic Windows domain where employees can sign into domain-joined computers, admins can manage users centrally, and support staff can troubleshoot account access issues.

This lab simulates that environment by creating:

- A Windows Server domain controller
- A Windows client machine
- A domain structure with users and administrative accounts
- Remote Desktop access for management
- Basic account support workflows

## Tools and Technologies

- Microsoft Azure Virtual Machines
- Windows Server 2022
- Windows 10
- Active Directory Domain Services
- Active Directory Users and Computers
- DNS configuration
- Remote Desktop Protocol
- PowerShell / PowerShell ISE

## What I Built

- Deployed Windows Server and Windows client VMs in Azure
- Configured network connectivity between server and client
- Enabled ICMP testing for connectivity validation
- Promoted the server into a domain controller
- Created a new Active Directory forest/domain
- Created organizational units for employees and admins
- Created an admin user and assigned domain admin rights
- Joined the Windows client machine to the domain
- Configured Remote Desktop access for domain users
- Practiced user management tasks such as password resets, unlocks, disabling, and enabling accounts

## Skills Demonstrated

- Building a Windows domain lab from scratch
- Understanding how DNS affects domain joins
- Managing users and organizational units in Active Directory
- Supporting common help desk account issues
- Verifying network connectivity between machines
- Using Remote Desktop for administration
- Documenting technical work clearly with screenshots
- Connecting Azure infrastructure concepts to Windows administration

## Lab Evidence and Walkthrough

### 1. Domain Controller Preparation

<p>
<img src="https://i.imgur.com/UZliaOP.png" height="80%" width="80%" alt="Active Directory setup steps"/>
</p>

I prepared the Windows Server VM for domain controller duties and verified basic network communication. This included configuring Windows Defender Firewall rules to allow ICMP testing so connectivity between machines could be confirmed before deeper domain configuration.

### 2. Active Directory Structure and Admin User

<p>
<img src="https://i.imgur.com/QpTonRy.png" height="80%" width="80%" alt="Active Directory users and computers"/>
</p>

I created organizational units for employees and admins, then created a domain admin account. This demonstrates the basic identity structure used in many Windows business environments.

### 3. Client Domain Join and Remote Access

<p>
<img src="https://i.imgur.com/o5pLdr6.png" height="80%" width="80%" alt="Domain join and remote desktop settings"/>
</p>

I joined the Windows client machine to the domain and configured Remote Desktop access for domain users. This is a common real-world support task when setting up or troubleshooting company workstations.

### 4. PowerShell User Creation and Verification

<p>
<img src="https://i.imgur.com/MfT0bdg.png" height="80%" width="80%" alt="PowerShell user administration"/>
</p>

I used PowerShell ISE to work with account creation concepts and verified the results inside Active Directory Users and Computers. This shows comfort with both GUI-based and script-assisted administration.

### 5. Account Administration Practice

<p>
<img src="https://i.imgur.com/6VfpU4E.png" height="80%" width="80%" alt="Active Directory account management"/>
</p>

I practiced common support actions such as unlocking accounts, resetting passwords, disabling accounts, and enabling accounts. These are directly relevant to entry-level help desk and support roles.

## Real-World Support Relevance

This lab maps to common tickets such as:

- “User cannot log into their workstation”
- “New employee needs a domain account”
- “User account is locked”
- “Password reset request”
- “Computer cannot join the domain”
- “Remote Desktop access is not working”
- “DNS/domain connectivity issue”

## What I Learned

- Active Directory depends heavily on correct DNS configuration
- Domain-joined clients need to point to the domain controller for name resolution
- Account access issues are often solved through structured checks: user status, password, group membership, machine domain status, and network connectivity
- Azure VMs can be used to safely practice Windows administration without physical hardware
- Clear documentation makes troubleshooting repeatable and easier to hand off

## Status

Completed portfolio lab. Future improvements could include Group Policy, shared folders, mapped drives, account lockout policy testing, and a deeper troubleshooting scenario set.
