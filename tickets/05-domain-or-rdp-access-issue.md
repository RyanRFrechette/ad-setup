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
2. Reviewed Azure NSG inbound rules for port 3389 — in this scenario, a missing or overly restrictive rule is the first thing to check
3. Confirmed Remote Desktop was enabled on the target VM (System Properties → Remote)
4. Confirmed the connecting user was a member of the Remote Desktop Users group in ADUC

**Domain join issue:**
1. On the client VM, ran `nslookup lab.local` to test DNS resolution — a failed result points to incorrect DNS server configuration
2. Checked the client VM's DNS server setting — in this scenario, it would be pointing to a public resolver instead of the domain controller's private IP
3. Updated the DNS server address to the domain controller's private IP and re-ran `nslookup lab.local` to confirm resolution
4. Reattempted domain join via System Properties → Change

---

## Resolution

**RDP:** In this scenario, adding an inbound NSG rule for port 3389 scoped to the admin IP resolves the timeout. The documented resolution path is: Azure portal → NSG → Inbound security rules → Add rule for port 3389.

**Domain join:** The documented resolution is to correct the client VM's DNS server from a public resolver to the domain controller's private IP. Once DNS resolves `lab.local` correctly, the domain join completes through System Properties → Change.

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

Expected verification steps:
- RDP: After adding the NSG rule, open Remote Desktop Connection and connect using the VM's public IP — a successful desktop session confirms the fix
- Domain join: After correcting DNS and rejoining, Windows displays a "Welcome to the lab.local domain" confirmation dialog; verify by logging in with domain credentials (`LAB\username`) on the next boot

---

## What This Proves

- Can diagnose and fix Azure NSG rules blocking RDP without touching the VM
- Understands that DNS misconfiguration is the root cause of most domain join failures
- Knows how to verify DNS resolution, secure channel, and group membership from the command line
- Can resolve two distinct connectivity issues using a structured diagnostic approach
