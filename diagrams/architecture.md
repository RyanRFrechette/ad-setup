# Lab Architecture — Active Directory User Support Lab

## Overview
Two Azure virtual machines simulating a small Windows domain: one Windows Server domain controller and one Windows client joined to the domain.

## Components

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

## Access Methods
- **RDP** — remote desktop into domain controller and client VMs via Azure public IP
- **Active Directory Users and Computers (ADUC)** — GUI-based user and group management on the DC
- **PowerShell** — scripted account operations (create, unlock, reset, query)
- **DNS Manager** — verify DNS records that support domain join and authentication

## Authentication Flow
User logs into Windows client → client contacts DC on port 88 (Kerberos) → DC authenticates against AD DS → Group Policy applied → Desktop session started
