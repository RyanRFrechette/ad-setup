<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Set up Active Directory and Users
- Configure DNS and Network Settings
- Manage Users and Remote Access
- Verify Setup and User Accounts

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/UZliaOP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In this post, we'll discuss the process of configuring and managing a domain controller and a client machine in a WindowsThe process begins by setting up and configuring the Windows Defender Firewall with Advanced Security on the server. This includes enabling the Core Networking Diagnostics - ICMP Echo Request (ICMPv4-In) inbound rules to allow for successful pinging between the server and clients. After completing these configurations, you can proceed to install Active Directory Certificate Services on the server through the Server Manager. This will enable the server to be promoted as a domain controller for a new forest, with the root domain name set as "mydomain.com" and a strong password.
</p>
<br />

<p>
<img src="https://i.imgur.com/QpTonRy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Once the domain controller is set up, you can create organizational units (_EMPLOYEES and _ADMINS) and user accounts within Active Directory Users and Computers. In this example, a user named "jane_admin" is created and added to the Domain Admins group. After creating the user accounts, you can connect to the domain controller and client machines using their respective public IP addresses through Microsoft Remote Desktop. This allows you to verify the user accounts and make any necessary changes, such as renaming the client machine, adding it to the domain, or updating its DNS settings.
</p>
<br />

<p>
<img src="https://i.imgur.com/o5pLdr6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After successfully joining the client machine to the domain, you can configure remote desktop settings to allow domain users to access the machine remotely. This can be done through the System Properties window on the client machine. You can then verify that the domain users are properly set up by checking their membership within Active Directory Users and Computers on the domain controller.
</p>
<br />

<p>
<img src="https://i.imgur.com/MfT0bdg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
PowerShell ISE can be used to run scripts on the domain controller, such as creating new user accounts or modifying existing ones. After running a script, you can refresh the Active Directory Users and Computers window to observe the changes. You can also test the functionality of the user accounts by logging into the client machine with various user credentials, verifying the account information through the command prompt, and observing the results.
</p>
<br />

<p>
<img src="https://i.imgur.com/6VfpU4E.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Finally, you can manage user accounts by performing actions such as unlocking, resetting passwords, disabling, or enabling accounts through Active Directory Users and Computers on the domain controller. This allows you to maintain control over account access and security. By following these steps, you will have successfully set up and configured a domain controller and client machine, created user accounts and organizational units, and managed user access and permissions within the domain.
</p>
<br />
