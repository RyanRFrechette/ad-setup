# Ticket 05 — Domain / RDP Access Issue

**Status:** Resolved  
**Priority:** High  
**Category:** Remote Access / Connectivity

## Issue Description
User cannot connect to a domain-joined Azure VM via Remote Desktop Protocol (RDP), or a workstation cannot reach the domain. Connection times out, is refused, or authentication fails.

## Steps Taken
1. Verified the target VM is running in Azure and the NIC is connected
2. Confirmed RDP port (3389) is open in the Azure Network Security Group (NSG) for the correct source IP
3. Verified DNS on the client resolves the domain controller's hostname correctly
4. Confirmed the computer account is active in ADUC (not disabled or stale)
5. Verified user account has permission to log on via Remote Desktop (Remote Desktop Users group)
6. Ran `nltest /sc_query:domain.local` on the client to test the secure channel to the DC

## Resolution
<!-- Document what fixed the issue -->
_Placeholder: describe resolution here._

## Notes
- DNS misconfiguration is the most common cause of domain join and authentication failures
- Ensure the VM's DNS server points to the domain controller, not a public resolver
- NSG rules in Azure must allow port 3389 from the correct source for RDP to work
- Rejoin the domain with `netdom join` or via System Properties if the secure channel is broken
