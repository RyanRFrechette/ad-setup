# Ticket 05 — Domain / RDP Access Issue

**Status:** Resolved  
**Priority:** High  
**Category:** Remote Access / Connectivity

## Issue Description
User cannot connect to a domain-joined Azure VM via Remote Desktop Protocol (RDP). Connection times out, is refused, or authentication fails at the RDP prompt.

## Steps Taken
1. Verified the VM is running in Azure Portal
2. Confirmed RDP port (3389) is open in the Network Security Group (NSG) for the user's IP
3. Verified user account has "Allow log on through Remote Desktop Services" permission
4. Checked if user is a member of the Remote Desktop Users group on the VM
5. Tested connectivity using the correct public IP or DNS name of the VM
6. Reviewed Azure Bastion as an alternative if direct RDP is blocked

## Resolution
<!-- Document what fixed the issue -->
_Placeholder: describe resolution here._

## Notes
- NSG rules are a common culprit — ensure inbound rule allows port 3389 from the correct source
- Prefer Azure Bastion over open RDP port for production environments
- Check Windows Firewall on the VM if NSG rules appear correct
