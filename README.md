<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create folders: "read-access", "write-access", "no-access", "accounting"
- Set permissions for the "Domain-Users" group
- Attempt to access file share as a normal User
- Create an "accountant' folder for Security Group and configure permissions

<h2>Actions and Observations</h2>

<p>

  ![Screenshot 2024-09-04 161442](https://github.com/user-attachments/assets/1c7a91d0-3ede-4a75-a484-d349a4c6c4d5)

![Screenshot 2024-09-04 161926](https://github.com/user-attachments/assets/94d49483-2896-411e-b329-48d368a3b4d7)

</p>
<p>
I first created sample file shares with various permissions:

  - Connect/log into DC-1 as my domain admin account (mydomain.com/jane_admin)
  - Connect/log into Client-1 as a normal user (mydomain<some.user>)
  - On DC-1, on the C:\drive, create 4 folders: "read-access", "write-access", "no-access", "accounting"
  - Set the following permissions (share the folder) for the "Domain Users" group:

        - Folder: "read-access", Group: "Domain Users", Permissions: "Read"
        - Folder: "write-access", Group: "Domain Users", Permissions: "Read/Write"
        - Folder: "no-access", Group: "Domain Admins", Permissions: "Read/Write" 
</p>
<br />

<p>

  ![Screenshot 2024-09-04 162441](https://github.com/user-attachments/assets/cef126b5-2fb0-4494-8504-dbd0beadff1a)

![Screenshot 2024-09-04 162547](https://github.com/user-attachments/assets/32018f63-936b-4904-8555-8cc3c174fc52)

</p>
<p>
In this section, I created an "ACCOUNTANTS" Security Group, assign permissions, and test access:

  - Back to DC-1, in Active Directory, and created "ACCOUNTANTS" security group
  - In the "accounting" folder created earlier, set the following permissions:

       - Folder: "accounting", Group: "ACCOUNTANTS", Permissions: "Read/Write"
  - On Client-1, try to access "accounting"folder, it should fail
  - Go back to DC-1, make user a member of the "ACCOUNTANTS" Security Group
  - Sign back into Client-1 and try to gain access to "accounting" folder, it should work
</p>

