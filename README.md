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
  <li>Create a Resource Group named "Active-Directory-Lab".</li>
  <li>Create a Virtaul Network named "Active-Directory-VNet".</li>
  <li>Create a Domain Controller VM named "dc-1" running windows server 2022.</li>
  <li>Configure dc-1 private ip address from dynamic to static.
    
 

  </li>
  <li>To test connectivity, disable dc-1's windows firewall
  
    add pic
  </li>
</ol>

<h2>Setup Client-1</h2>
<ol>
  <li>Create a virtual machine named "client-1".</li>
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

![configure-ad-21](https://github.com/user-attachments/assets/7e6e3285-8ba4-4675-97c3-7199031ce271)
![configure-ad-22](https://github.com/user-attachments/assets/84a16f9e-e6b4-46b6-a17c-be2b94018310)


  </li>
</ol>
<br />
