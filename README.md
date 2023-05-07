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
In this post, we'll discuss the process of configuring and managing a domain controller and a client machine in a Windows-based environment. This includes the essential tasks of setting up the Windows Defender Firewall with Advanced Security settings to ensure proper communication between the machines, and installing Active Directory Certificate Services on the domain controller to manage users, permissions, and other domain-related settings.
</p>
<br />

<p>
<img src="https://i.imgur.com/QpTonRy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Organizational units (OUs) play a crucial role in simplifying the management of user accounts and permissions within the domain. By creating OUs, you can organize your domain in a structured manner, making it easier to manage user accounts and their respective permissions.
</p>
<br />

<p>
<img src="https://i.imgur.com/o5pLdr6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Another key aspect of domain management is handling user properties such as resetting passwords and enabling or disabling user accounts. These tasks help maintain security and ensure that only authorized users have access to the domain and its resources.
</p>
<br />

<p>
<img src="https://i.imgur.com/MfT0bdg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Furthermore, it is important to understand how to monitor and manage network settings and connectivity. This includes ensuring proper DNS configuration and addressing any issues that may arise, such as IP address conflicts or connectivity problems between the domain controller and client machines.
</p>
<br />

<p>
<img src="https://i.imgur.com/6VfpU4E.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Overall, this post aims to provide a high-level overview of managing a domain controller and a client machine in a Windows environment. With a solid understanding of Active Directory, user accounts, and system configurations, you'll be well-equipped to handle various IT scenarios that involve managing domain resources.
</p>
<br />
