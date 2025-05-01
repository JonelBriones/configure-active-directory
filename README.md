<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Deployment and Configuration Steps</h2>
<ol>
  <li>Create a Resource Group named "Active-Directory-Lab"</li>
  <li>Create a Virtual Network named "Active-Directory-VNet"</li>
  <li>Create a Domain Controller VM named "dc-1" running windows server 2022</li>
  <li>Configure dc-1 private ip address from dynamic to static

![configure-ad-47](https://github.com/user-attachments/assets/b78fb7fb-fd18-446d-9d97-5b2a51258924)
  </li>
  <li>To test connectivity, disable dc-1's windows firewall
  </li>
</ol>

<h2>Setup Client-1</h2>
<ol>
  <li>Create a virtual machine named "client-1"</li>
  <li>Update client-1's dns server to dc-1's private ip address
    
   ![configure-ad-1](https://github.com/user-attachments/assets/f1431541-f4de-43c7-867e-343bf132ac9b)
  ![configure-ad-2](https://github.com/user-attachments/assets/59e477ba-ee1f-4473-8575-29f34055921f)
  </li>
  <li>Validate ping dc-1 from client-1</li>
  <li>Validate client-1 private ip matches dc-1</li>
</ol>

<h2>Install Active Directory</h2>
<ol>
  <li>Install Active Directory Domain Services on dc-1
    
  ![configure-ad-4](https://github.com/user-attachments/assets/1c671527-292b-4cd4-88f3-cf1493ea785d)
  </li>
  <li>Promote as a domain controller
    
![configure-ad-6](https://github.com/user-attachments/assets/740ad678-a9db-4d8a-b863-3584d8336e08)
  </li>
  <li>Add a new forest, our root domain name will be "mydomain.com"
    
  ![configure-ad-7](https://github.com/user-attachments/assets/b910c15e-08d7-465d-b9fa-b27d815acf4b)
  </li>
  <li>Open Active Directory Users and Computers and right click mydomain.com and create new Organizational Units:
  <ul>
    <li>_EMPLOYEES</li>
    <li>_ADMIN</li>
    <li>_ADMIN</li>
  </ul>
    
  ![configure-ad-10](https://github.com/user-attachments/assets/7a8aae16-8b4d-4eaf-845a-73ef48f1d551)
  </li>
  <li>Create a new employee
  <ul>
    <li>Username: jane_admin</li>    
    <li>Password: Password1</li>    
  </ul>
    
  ![configure-ad-11](https://github.com/user-attachments/assets/c450bc8a-82b0-41f3-8384-c137e5a8ef4a)
  ![configure-ad-12](https://github.com/user-attachments/assets/558f1fda-0b87-414c-a5ca-928f0ef1ae55)
  ![configure-ad-13](https://github.com/user-attachments/assets/43313c34-9220-4cf8-8edf-ace367186f41)
  </li>
  <li>Add jane_doe as a member of Domain Admins
  
  ![configure-ad-14](https://github.com/user-attachments/assets/a158f8bb-3320-459d-af0d-3fc093c8a5c6)
  </li>
  <li>Re-log into dc-1 using mydomain.com\jane_admin</li>
  <li>Log into client-1, and go to system settings > rename this PC (advanced) > toggle Member of Domain: mydomain.com</li>
  <li>Log in as mydomain.com\jane_admin to enable client-1 to join the domain
  
  ![configure-ad-17](https://github.com/user-attachments/assets/8ce34647-edfb-4827-b9fb-bbed0f25e316)
  </li>
  <li>In dc-1, verify client-1 is listed in the Computers folder in Active Directory Users and Computers. Drag client-1 into _CLIENTS
    
  ![configure-ad-18](https://github.com/user-attachments/assets/550ed021-dfb3-475a-9431-5363c0f27f97)
  ![configure-ad-19](https://github.com/user-attachments/assets/ade6ab89-e4e3-4560-9da7-5402dad9637c)
  </li>
</ol>

<h2>Setup Remote Desktop for non-administrative users on client-1</h2>
<ol>
  <li>Open system settings > Remote desktop > Select users that can remotely access this PC > enter Domain Users
    
![configure-ad-20](https://github.com/user-attachments/assets/96111507-55a2-4a8d-a0bd-ea672fd958bc)
![configure-ad-21](https://github.com/user-attachments/assets/7e6e3285-8ba4-4675-97c3-7199031ce271)
![configure-ad-22](https://github.com/user-attachments/assets/84a16f9e-e6b4-46b6-a17c-be2b94018310)
  </li>
</ol>

<p>Summary: This will allow any user from dc-1 active directory to log into client-1</p>

<h2>Create additional users</h2>
<ol>
  <li>Login to dc-1 as jane_admini</li>
  <li>Open PowerShell_ise as an administrator</li>
  <li>Create a new file and paste the <a href="https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1">script</a>
  </li>
  <li>Running the script will generate new users
    
![configure-ad-23](https://github.com/user-attachments/assets/d4a7bdad-f00c-4475-91d4-15c2429c3d2c)
https://github.com/user-attachments/assets/c60222a7-dde9-4aa6-a394-72202d08f418
  </li>
  <li>Select a random user from dc-1 Active Directory to log into client-1
  
![configure-ad-24](https://github.com/user-attachments/assets/416f5653-2a73-4a8f-a906-158ea0f22351)
![configure-ad-26](https://github.com/user-attachments/assets/a6215049-5975-42f6-a093-d0189298b2d6)
![configure-ad-27](https://github.com/user-attachments/assets/be9fd835-6ac3-4b0b-bd99-3b3367d1aea3)
  </li>
</ol>
<p>Summary: We generated random users to simulate a real work place environment. We can now manage user's password, ability to disable/enable accounts, etc.</p>

<h2>Manage user password lockout with Group Policy Management</h2>
<ol>
  <li>Open Group Policy Management, Forest: mydomain.com > mydomain.com > right click Default Domain Policy and select edit</li>
<li>Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy > Account lockout threshhold

![configure-ad-30](https://github.com/user-attachments/assets/1bfff9c3-9a74-4c97-b9cd-5257bdbdc541)
![configure-ad-31](https://github.com/user-attachments/assets/46ae407e-96de-4a1c-adff-04495ac01530)
</li>
<li>Login into client-1 as jane_admin</li>
<li>Open PowerShell and run "gpupdate /force"
  
![configure-ad-33](https://github.com/user-attachments/assets/d4e6fc23-f864-4d68-8688-6cee03c1edba)
![configure-ad-34](https://github.com/user-attachments/assets/c956368f-5a69-463b-85b9-08645a142c29)

</li>
<li>We can unlock by selecting user properties Account tab or right click user account and reset password & unlock account
  
![configure-ad-36](https://github.com/user-attachments/assets/7d6f4e37-c183-40df-8ea8-5892814673a4)
![configure-ad-38](https://github.com/user-attachments/assets/374e65fd-57c1-4e99-af67-c2eafa5c6cd2)
![configure-ad-39](https://github.com/user-attachments/assets/726dfc75-57ab-452a-8a3b-e00efff12cc8)
</li>

<p>Summary: This will enable a password lockouts when the number of failed attempts reaches the threshold value</p>
</ol>

<h2>Observing Logs</h2>
<li>Open Event Viewer in client-1 as jane_admin or run as administrator using jane_admin</li>
<li>Windows Logs > Security, we can view all user login activity
  
![configure-ad-46](https://github.com/user-attachments/assets/1d1b4574-7663-4409-a8b0-cc879c77daa4)
</li>
