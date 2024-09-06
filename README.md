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
Create a Resource Group
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
  
<p> Create the Client VM (Windows 10) named “Client-1”
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
After VM is created, set Client-1’s DNS settings to DC-1’s Private IP address. <p> First, go to the VM DC-1 and you copy DC-1 private IP address. Next, go to VM Client-1 and go to "Network settings" and click on "Network Interface / IP configuration". On the left panel click on "DNS server". Under DNS server click on "Custom" and copy paste DC-1 private IP address and click save. <p/> 
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
Log into the VM DC-1 using Microsoft Remote Desktop. When asked on the Network to enable other computers from your network to find you, click "Yes". <p> Then continue to disable the Windows Firewall (for testing connectivity) On the bottom left type wf.msc to open up Windows firewall. Double click on "Windows Defender Firewall Properties". On "Domain Profile" "Private Profile" an "Public Profile" click off on their Firewall state. Click "Apply" and "OK". The Firewall is off! </p>
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
<p> Attempt to ping DC-1’s private IP address. On the bottowm left type "Powershell" and type ping and DC-1 private IP address. example: ping 10.0.0.4 <p/>
<p> Ensure the ping succeeded. </p>
From Client-1, open PowerShell and run ipconfig /all
The output for the DNS settings should show DC-1’s private IP Address
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

