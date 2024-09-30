<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- MacBook Pro
- Microsoft Azure (Virtual Machines/Compute)
- Microsoft Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup Domain Controller in Azure
- Setup Client-1 in Azure
- Install Active Directory
- Create a Domain Admin user within the domain
- Join Client-1 to your domain (mydomain.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create a bunch of additional users and attempt to log into client-1 with one of the users


<h2>Deployment and Configuration Steps</h2>

<p>
  
![CreateADResourceGroup](https://github.com/user-attachments/assets/563714d2-2fe1-4ef6-b771-7ffa9bb55c44)
![Screen Shot 2024-09-06 at 1 11 16 PM](https://github.com/user-attachments/assets/6c3481e1-d51c-4d07-8f5d-e7ba0c84861b)
![CreateVmDC-1](https://github.com/user-attachments/assets/3c4bc155-bc33-4932-a92f-834c16aba7ea)
![SetIPtoStatic](https://github.com/user-attachments/assets/bbb6b788-46ba-4923-aaeb-74da63724b71)

</p>
<p>
Setup Domain Controller in Azure<p/>
1) Create a Resource Group
Create a Virtual Network and Subnet
Create the Domain Controller VM (Windows Server 2022) named “DC-1”
Username: labuser
Password: Cyberlab123! <p/>
After VM is created, set Domain Controller’s NIC Private IP address to be static

</p>
<br />

![CreateVmClient-1](https://github.com/user-attachments/assets/65c23991-df08-4a10-870d-70cba9bfcc0e)

<p>

</p>
<p>
Setup Client-1 in Azure<p/>
  
<p> 2) Create the Client VM (Windows 10) named “Client-1”
Username: labuser
Password: Cyberlab123! <p/>
<p> Attach it to the same region and Virtual Network as DC-1<p/>

<p>
  
![CopyDC-1PrivateIPaddress](https://github.com/user-attachments/assets/0633b9d9-4dea-4b05-b15c-934decbca628)
![Screen Shot 2024-09-06 at 2 35 23 PM](https://github.com/user-attachments/assets/24e04ddc-f7a7-4967-aadb-94d10910d808)
![Screen Shot 2024-09-06 at 2 36 54 PM](https://github.com/user-attachments/assets/195c64ab-499e-4072-b4f5-c5388d6d9f05)
![Screen Shot 2024-09-06 at 2 41 05 PM](https://github.com/user-attachments/assets/4537fbeb-bf1f-4710-8041-aceb3f734d4d)

</p>
<p>
After VM is created, set Client-1’s DNS settings to DC-1’s Private IP address. <p/>
<p> 3) Go to the VM DC-1 and you copy DC-1 private IP address. <p/> 
Next, go to VM Client-1 and go to "Network settings" and click on "Network Interface / IP configuration". On the left panel click on "DNS server". Under DNS server click on "Custom" and copy paste DC-1 private IP address and click save. <p/> 
From the Azure Portal, restart Client-1 <p/>
</p>
<br />

</p>
<br />

![LogIntoVmDC-1](https://github.com/user-attachments/assets/b3a92607-ba27-4196-8824-52b04cae60e4)
![Typewf msc](https://github.com/user-attachments/assets/dc022618-f60d-40ac-8aa7-a5ba25e11256)
![Screen Shot 2024-09-06 at 2 01 22 PM](https://github.com/user-attachments/assets/763b7de3-80ca-4f3a-8040-5a1b89591872)
![Screen Shot 2024-09-06 at 2 02 40 PM](https://github.com/user-attachments/assets/17ca1a8d-c6e2-4ee8-8d30-5ac35ea95972)
![Screen Shot 2024-09-06 at 2 02 47 PM](https://github.com/user-attachments/assets/59c126ad-66a5-43e8-a008-94966350c838)

<p>

</p>
<p>
4) Log into the VM DC-1 using Microsoft Remote Desktop. <p> 
  <p> Continue to disable the Windows Firewall (for testing connectivity) <p/>
  On the bottom left type wf.msc to open up Windows firewall. Double click on "Windows Defender Firewall Properties". On "Domain Profile" "Private Profile" an "Public Profile" click off on their Firewall state. Click "Apply" and "OK". The Firewall is off! </p>
</p>
<br />

<p>
  
![LogginToClient-1](https://github.com/user-attachments/assets/4f5a590b-7ae9-4158-9dfb-250169df2ace)
![Screen Shot 2024-09-06 at 2 48 23 PM](https://github.com/user-attachments/assets/14d947f1-3a02-4931-bc29-6831a55c873b)
![Screen Shot 2024-09-06 at 2 49 15 PM](https://github.com/user-attachments/assets/93830f10-f85f-464b-a60c-5417cf494c4a)
![Screen Shot 2024-09-06 at 2 55 37 PM](https://github.com/user-attachments/assets/6f006500-47fb-474a-8e4a-5414c851fe6e)
![Screen Shot 2024-09-06 at 3 00 18 PM](https://github.com/user-attachments/assets/a6acbf73-0789-4cb7-8592-a5987b6067a1)

</p>
<p>
Login to Client-1 <p/>
Click no for all the private settings ane click yes for the "Network". 
<p> 5) Attempt to ping DC-1’s private IP address. On the bottowm left type "Powershell" and type ping and DC-1 private IP address. example: ping 10.0.0.4 <p/>
<p> Ensure the ping succeeded. </p>
From Client-1, open PowerShell and run ipconfig /all
The output for the DNS settings should show DC-1’s private IP Address
</p>
<br />

<p>
  
![GoToServerManager](https://github.com/user-attachments/assets/dc2237a0-f063-4b1b-ac3a-2befd3b8b7cd)
![ActivateDomainServices](https://github.com/user-attachments/assets/92f4bccb-5b8d-4a55-8443-97c56f9e71c3)
![Install](https://github.com/user-attachments/assets/3ec62d08-02c4-4615-877c-c650dd6dc732)

</p>
<p>
6) Login to DC-1 and install Active Directory Domain Services
</p>
<br />

<p>
  
![ConfigureDomainController](https://github.com/user-attachments/assets/ddb30fcd-22ef-4931-a1ed-e4ab8f0ea208)
![AddNewForest](https://github.com/user-attachments/assets/aa7704fd-4cbc-47bb-a03c-aa463ede2774)
![Unclick](https://github.com/user-attachments/assets/6abf0369-ddf6-41a1-b778-3aa0b185d985)
![Install](https://github.com/user-attachments/assets/089c3283-cec4-4477-a848-921d465abbd7)
![SignOut](https://github.com/user-attachments/assets/a8e2b56d-b75d-42a1-9a21-893d7d4b24c6)
![Screen Shot 2024-09-09 at 7 54 15 PM](https://github.com/user-attachments/assets/87d26557-bdd8-40af-a800-0d2bdcfe4846)

</p>
<p>
On the top right corner there will be a flag with a yellow exclamation point. Click on it and then click on "Promote this server as a domain controller". 
<p> 7) Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is) </p>
Restart and then log back into DC-1 as user: Domain\labuser
</p>
<br />

<p>

![Screen Shot 2024-09-10 at 5 10 53 PM](https://github.com/user-attachments/assets/739afd26-b1d3-4280-828b-f3c3fd114989)
![Screen Shot 2024-09-10 at 5 14 00 PM](https://github.com/user-attachments/assets/b510575d-232a-4bf4-a7a9-7d4ea7f408dc)
![Screen Shot 2024-09-10 at 5 14 41 PM](https://github.com/user-attachments/assets/c36c1baf-d980-45a9-b2c2-8ed4b32497b4)
![Screen Shot 2024-09-10 at 5 16 51 PM](https://github.com/user-attachments/assets/a83ea5ff-604e-4c58-81d4-4ea07c3792fb)
![Create_ADMINS](https://github.com/user-attachments/assets/b7817ce7-2be5-41fd-8a7b-21c54bf56cf7)

</p>
<p>
8) Create a Domain Admin user within the domain
<p> In DC-1 cick the bottom left start button and click on "Windows Administrative Tools" and scroll down to select "Active Directory Users and Computers". <p/>
In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”
Create a new OU named “_ADMINS”
</p>
<br />

<p>
  
![Screen Shot 2024-09-10 at 5 22 42 PM](https://github.com/user-attachments/assets/e00cb0cf-d329-4ecc-9c13-a1f8155eac24)
![Screen Shot 2024-09-27 at 3 31 09 PM](https://github.com/user-attachments/assets/ab9a6177-8f23-4dcf-bc86-f1403f72b524)
![Screen Shot 2024-09-27 at 3 32 28 PM](https://github.com/user-attachments/assets/2ad7e767-b50c-4f30-a036-59d1709e9f37)


</p>
<p>
 9) Create a new employee named “edgar castrejon” (same password) with the username of “edgar_admin” / Cyberlab123!
</p>
<br />

<p>
  
![Screen Shot 2024-09-27 at 3 33 56 PM](https://github.com/user-attachments/assets/0b5acfc9-fb05-41b9-9a64-47b7e4b3a84d)
![Screen Shot 2024-09-10 at 5 33 50 PM](https://github.com/user-attachments/assets/10712462-15dd-435c-be87-07347ebde024)
![Screen Shot 2024-09-10 at 5 34 16 PM](https://github.com/user-attachments/assets/02c8e1bf-0418-4294-b0a1-2b456dea4409)
![Screen Shot 2024-09-27 at 3 43 06 PM](https://github.com/user-attachments/assets/7946d593-3560-44a4-93ec-ce80fa403f2d)
![Screen Shot 2024-09-27 at 3 46 32 PM](https://github.com/user-attachments/assets/6a73e9b8-77c2-4d5e-a601-8874224800a1)

</p>
<p>
10) Add edgar castrejon to the “Domain Admins” Security Group <p/>
Log out / close the connection to DC-1 and log back in as “Domain\edgar_admin”
User edgar_admin as your admin account from now on
</p>
<br />

<p>
  
![Screen Shot 2024-09-10 at 5 49 10 PM](https://github.com/user-attachments/assets/41245c05-f95a-44a3-8d9c-79ec705200c5)
![Screen Shot 2024-09-10 at 5 49 23 PM](https://github.com/user-attachments/assets/01f8bc08-11a8-431d-a9de-e6079571f1c6)
![Screen Shot 2024-09-10 at 5 52 46 PM](https://github.com/user-attachments/assets/1017e3b8-da99-4cb8-a025-397cf8f7e288)
![Screen Shot 2024-09-10 at 5 59 50 PM](https://github.com/user-attachments/assets/71ccd112-f081-42ac-8e2e-8ca307331614)
![Screen Shot 2024-09-10 at 6 03 27 PM](https://github.com/user-attachments/assets/235df2ea-2e3e-48bd-a8a9-17a36cb1b1b5)

</p>
<p>
11) Join Client-1 to your domain (mydomain.com) <p/> 
<p> Right click the start menue and go to "Systems". Next click "Rename this PC (advanced)". Under the "Computer Name" tab click on "Change" and Clcik on "Domian". 
<p/> After joining your domian restart your computer

</p>
<br />

<p>

![Screen Shot 2024-09-10 at 6 10 33 PM](https://github.com/user-attachments/assets/6d748730-974f-41f7-a2f6-bd404659ab33)
![Screen Shot 2024-09-10 at 6 11 40 PM](https://github.com/user-attachments/assets/0c82d58a-d8d0-47bb-a75b-833f199fc4c0)
![Screen Shot 2024-09-10 at 6 13 29 PM](https://github.com/user-attachments/assets/376c1bd3-6f7b-4cf5-ac9a-567f816a8097)
![Screen Shot 2024-09-10 at 6 14 19 PM](https://github.com/user-attachments/assets/ee0a852a-c60a-4fa0-bebf-10c822949308)
![Screen Shot 2024-09-10 at 6 14 23 PM](https://github.com/user-attachments/assets/e2e00a57-4513-43a5-ad6a-15608717bfd6)

</p>
<p>
Login to the Domain Controller and verify Client-1 shows up in ADUC
12) Create a new OU named “_CLIENTS” and drag and drop Client-1 into there
</p>
<br />

<p>

![Screen Shot 2024-09-10 at 6 35 46 PM](https://github.com/user-attachments/assets/add87c40-b19c-4698-8999-36fa75ef4f9b)
![Screen Shot 2024-09-10 at 6 36 56 PM](https://github.com/user-attachments/assets/00af795e-41dc-40a9-9205-74bb3f01dc5e)
![Screen Shot 2024-09-10 at 6 38 23 PM](https://github.com/user-attachments/assets/6e7717f2-cbb3-4b49-8d9b-dbcd4a625424)

</p>
<p>
13) Log into Client-1 as mydomain.com\edgar_admin <p/>
Open system properties
<p> Click “Remote Desktop” <p/>
Allow “domain users” access to remote desktop
You can now log into Client-1 as a normal, non-administrative user now
</p>
<br />

<p>

![Screen Shot 2024-09-10 at 6 49 03 PM](https://github.com/user-attachments/assets/749a3af9-f761-4434-9b90-40cfd48b33a1)
![Screen Shot 2024-09-10 at 6 51 20 PM](https://github.com/user-attachments/assets/b8d9b0fb-9914-46ef-be30-1b14f557e00e)
![Screen Shot 2024-09-10 at 6 55 12 PM](https://github.com/user-attachments/assets/d617d935-a31d-432d-97d6-e57a0b7aa1ff)
![Screen Shot 2024-09-10 at 7 10 31 PM](https://github.com/user-attachments/assets/05673dc1-5cd5-40e3-9db3-e6d6d1e9b61c)
![Screen Shot 2024-09-10 at 7 09 18 PM](https://github.com/user-attachments/assets/afc3070c-a8af-4cfa-b596-dd8eec561666)
![Screen Shot 2024-09-10 at 7 07 43 PM](https://github.com/user-attachments/assets/73cdc778-b4d2-477e-89d1-7761f9017a0e)

</p>
<p>
14) Create a bunch of additional users and attempt to log into client-1 with one of the users <p/>
  
<p> Login to DC-1 as edgar_admin (if you're not already) <p/>
Open PowerShell_ise as an administrator
<p> Create a new File and paste the contents of the script into it <p/>
Run the script and observe the accounts being created
<p> When finished, open ADUC and observe the accounts in the appropriate OU　(_EMPLOYEES) Then, refresh to see new employees <p/>
attempt to log into Client-1 with one of the accounts (take note of the password in the script = Password1)

</p>
<br />
