# Ticket 05 — Domain / RDP Access Issue

**Status:** Resolved  
**Priority:** High  
**Category:** Remote Access / Connectivity  
**Environment:** Windows Server 2022 domain controller · Windows 10 client · Azure virtual network

---

## Problem

User cannot connect to a domain-joined Azure VM via Remote Desktop Protocol (RDP). The RDP client either times out or returns "Remote Desktop can't connect to the remote computer." A second user reports their workstation cannot join the domain.

---

## Environment

- Domain controller: Windows Server 2022 on Azure VM, private IP on the virtual network
- Client VM: Windows 10 on Azure VM, same virtual network
- Azure Network Security Group (NSG) controls inbound traffic
- DNS on the client VM must point to the domain controller for domain join to work

---

## Checks Performed

**RDP issue:**
1. Confirmed the target VM was running in the Azure portal
2. Checked the Azure NSG inbound rules — port 3389 was missing a rule for the admin's IP
3. Confirmed Remote Desktop was enabled on the target VM (System Properties → Remote)
4. Confirmed the connecting user was a member of the Remote Desktop Users group in ADUC

**Domain join issue:**
1. On the client VM, ran `nslookup lab.local` — returned no results (DNS pointed to 8.8.8.8 instead of the DC)
2. Updated the client VM's DNS server address to the domain controller's private IP
3. Re-ran `nslookup lab.local` — resolved correctly to the DC
4. Attempted domain join again via System Properties → Change

---

## Resolution

**RDP:** Added an inbound NSG rule for port 3389 from the admin IP. RDP connection succeeded immediately after the rule was saved.

**Domain join:** Correcting the DNS server from `8.8.8.8` to the domain controller's private IP resolved the join failure. The workstation joined the domain on the next attempt without any other changes.

```powershell
# Verify DNS resolution on the client
Resolve-DnsName lab.local

# Check secure channel after domain join
Test-ComputerSecureChannel -Verbose

# Verify RDP group membership
Get-ADGroupMember -Identity "Remote Desktop Users"
```

---

## Verification

- RDP: Connected successfully to the domain-joined VM via Remote Desktop after NSG rule update
- Domain join: Received "Welcome to the lab.local domain" confirmation dialog. User logged in with domain credentials on first boot after join.

---

## What This Proves

- Can diagnose and fix Azure NSG rules blocking RDP without touching the VM
- Understands that DNS misconfiguration is the root cause of most domain join failures
- Knows how to verify DNS resolution, secure channel, and group membership from the command line
- Can resolve two distinct connectivity issues using a structured diagnostic approach
