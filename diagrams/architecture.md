# Lab Architecture — Azure Active Directory User Support Lab

## Overview
Single-tenant Azure environment simulating a small enterprise IT setup for help desk practice.

## Components

```
┌─────────────────────────────────────────────┐
│           Azure Active Directory             │
│  (Entra ID Tenant)                          │
│                                             │
│  Users / Groups / Licenses / Policies       │
└────────────────┬────────────────────────────┘
                 │
    ┌────────────▼────────────┐
    │   Azure Virtual Network  │
    │                          │
    │  ┌────────────────────┐  │
    │  │  Windows Server VM │  │
    │  │  (Domain-joined)   │  │
    │  │  RDP port 3389     │  │
    │  └────────────────────┘  │
    │                          │
    │  Network Security Group  │
    │  (Inbound: RDP, HTTPS)   │
    └──────────────────────────┘
```

## Access Methods
- **Azure Portal** — user and group management, license assignment
- **RDP** — remote desktop into Azure VMs
- **PowerShell** — scripted account operations (unlock, reset, provision)
- **Azure Bastion** *(optional)* — browser-based RDP without open port 3389

## Identity Flow
User sign-in → Azure AD authentication → Conditional Access evaluation → Session granted or denied
