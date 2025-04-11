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

- Create two Virtual Machine for Dc-1 (Domain controller) and client-1 
- Configure Dc-1 private IP address to static, set CLient-1 DnS setting to DC-1 Private IP address
- Install and configure Active Directory and promote Dc-1 to Domain Controller
- Join Client-1 to domain and setup Remote Desktop for non-admin users

<h2>Overall Picture</h2>
<P>
  <img width="548" alt="image" src="https://github.com/user-attachments/assets/9653c620-73bd-4805-be60-734e519b9a65" />
</P>

<h2>Deployment and Configuration Steps</h2>

![image](https://github.com/user-attachments/assets/006201de-e564-46b6-9277-982703b60379)
![6B30B4E4-0704-4924-AC9B-A3BBC783E646_1_201_a](https://github.com/user-attachments/assets/a0a525ff-6c8d-4f62-8468-16e06a28a51b)
![2A9C16CC-400C-48E1-8BB1-29D9FCD036C3_1_201_a](https://github.com/user-attachments/assets/f1447111-d95c-489a-b6fc-e803ff1d1fe2)
<img width="1728" alt="6168ACFB-45AB-42D4-A325-84B997DD5923" src="https://github.com/user-attachments/assets/6424aea4-d2d7-417e-a49f-ac13cabe5ec3" />


<p>
Setting Up a Domain Controller in Azure
Create a Resource Group
Set up a new resource group to organize and manage related resources in Azure.
Create a Virtual Network and Subnet
Deploy a Virtual Network (VNet) and configure a subnet where your domain controller will reside.
Deploy the Domain Controller Virtual Machine
Create a Windows Server 2022 VM named “DC-1”.
Use the following credentials:
Username: labuser
Password: Cyberlab123!
Initial Configuration of the VM
Log in to the VM after deployment.
Temporarily disable the Windows Firewall to allow for easier connectivity testing during setup.
Deploying and Configuring the Client VM in Azure
Create the Client Virtual Machine
Deploy a Windows 10 VM named “Client-1”.
Use the following credentials:
Username: labuser
Password: Cyberlab123!
Ensure the VM is created in the same region and attached to the same Virtual Network and subnet as DC-1.
Configure DNS Settings
After deployment, update Client-1’s DNS server settings to use the private IP address of DC-1.
Restart the Client VM
Use the Azure Portal to restart Client-1 so the new DNS settings take effect.
Verify Connectivity
Log into Client-1.
Open a Command Prompt or PowerShell window and attempt to ping the private IP address of DC-1.
Confirm that the ping is successful.
Verify DNS Configuration
On Client-1, open PowerShell and run the command ipconfig /all


</p>
<br />

<p><img width="1728" alt="3E8FE8B3-56C8-4140-BC10-CD84261CC110" src="https://github.com/user-attachments/assets/fb2c8e7e-30ac-48c8-97bc-082d4465127a" />

</p>
<p>
Configure DC-1 as a Domain Controller
Install Active Directory Domain Services (AD DS)
Log into DC-1 and install the Active Directory Domain Services role via Server Manager.
Promote the Server to a Domain Controller
After installation, promote DC-1 to a domain controller by creating a new forest.
Use a domain name such as mydomain.com (you can choose any name, just be sure to remember it).
Restart and Reauthenticate
Once the promotion process is complete, the system will prompt a restart.
After the restart, log back into DC-1 using the domain credentials:
Username: mydomain.com\labuser

</p>
<br />

<p>
<img width="1728" alt="6DEF0A3F-DAF7-4F03-805F-4893D5C051F6" src="https://github.com/user-attachments/assets/c896b002-1acc-4a0b-98f5-86362c8a08fe" />
  <img width="1728" alt="B63B5D74-A8D3-4C07-BB02-BC8100425D42" src="https://github.com/user-attachments/assets/e9e8a023-3d12-445e-8bfb-8a909f5799e7" />

<img width="1728" alt="39320886-5E11-48FE-8037-B2210BA534A7" src="https://github.com/user-attachments/assets/9c3c2546-11b2-41ee-8941-91d46a2f2f74" />
<img width="1728" alt="BC2C8C15-61DC-470A-A9FC-DC52B3228F72" src="https://github.com/user-attachments/assets/1b9317eb-a12e-4798-bd21-c16413b6919b" />

</p>
<p>
Create a Domain Administrator User Account
Open Active Directory Users and Computers (ADUC)
On DC-1, launch Active Directory Users and Computers.
Create Organizational Units (OUs)
In the domain, create a new Organizational Unit (OU) named _EMPLOYEES.
Create another OU named _ADMINS.
Create a New Domain User
Within the _ADMINS OU, create a new user with the following details:
Full Name: Jane Doe
Username: jane_admin
Password: Cyberlab123!
Ensure the option to require a password change at next login is disabled (for testing purposes).
Assign Administrative Privileges
Add the jane_admin user to the Domain Admins security group to grant administrative rights.
Switch to the New Admin Account
Log out or close the session on DC-1.
Log back in using the new admin account:
Username: mydomain.com\jane_admin
From this point forward, use jane_admin as your primary domain administrator account.
</p>
<img width="1728" alt="BC2C8C15-61DC-470A-A9FC-DC52B3228F72" src="https://github.com/user-attachments/assets/1b9317eb-a12e-4798-bd21-c16413b6919b" />

<img width="1728" alt="AED7D8FA-A990-4A6A-86C4-B537535F3E38" src="https://github.com/user-attachments/assets/73969bb9-870b-4b79-8572-f9dcc2aa0e40" />
Enable Remote Desktop Access for Domain Users on Client-1
Log into Client-1
Use the domain admin account: mydomain.com\jane_admin.
Enable Remote Desktop for Non-Administrators
Open System Properties.
Navigate to the Remote Desktop tab.
Enable Remote Desktop access and add the Domain Users group to the list of allowed remote users.
Test Access
You should now be able to remotely log into Client-1 using any standard domain user account.
(Note: In a real-world environment, this would typically be configured via Group Policy to apply settings across multiple systems efficiently—something to consider for a future lab.)
Create Multiple Standard Users and Test Access
Log into DC-1
Sign in as mydomain.com\jane_admin.
Open PowerShell ISE with Admin Privileges
Right-click PowerShell ISE and select “Run as Administrator”.
Create and Run the Script
In PowerShell ISE, create a new script file.
Paste the provided user creation script into the file.
Run the script and observe the user accounts being created.
Verify User Creation
Open Active Directory Users and Computers (ADUC).
Navigate to the _EMPLOYEES OU and confirm the new accounts have been created.
Test User Login on Client-1
Use one of the newly created user accounts to log into Client-1.
Be sure to use the correct domain and the password specified in the script.



