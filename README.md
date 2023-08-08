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

- Create a Windows Server VM and a Windows-10 VM in Microsft Azure
- Ensure Connectivity between the client and Domain Controller
- Install Active Directory
- Create an Admin and normal user account in AD
- Join Client-1 to your Domain
- Setup Remote Desktop for non-administrative users on Client-1

<h2>Deployment and Configuration Steps</h2>

<p>
  
  **PART 1**
  
  **1.) Creating a Windows server VM and Windows 10 VM in Microsoft Azure**
  
  ![image](https://github.com/akingsley22/configure-ad/assets/138138839/a9df99df-095a-4c03-9397-77794af8edbe)

  ![image](https://github.com/akingsley22/configure-ad/assets/138138839/98b61b19-4ea8-42b8-b4b9-5c5027a902cf)


</p>
<p>
Once Windows Server VM is created, it is going to act as the domain controller where AD (Active Directory) is going to be installed. 
  
Next step, create another VM on a windows 10 server that is going to act as a client. Make sure both VM are in the same virtual network and the ip address of the domain controller is turned to static.
</p>
<br />

<p>

  **2.) Ensuring Connectivity between the client and Domain Controller**
![image](https://github.com/akingsley22/configure-ad/assets/138138839/5f2db3c5-eefd-46ee-987d-1fce9b0b355c)

![image](https://github.com/akingsley22/configure-ad/assets/138138839/3f98dd48-fab5-41bc-9767-52d292e4305a)



Login to the Domain controller with Remote Desktop and enable ICMPv4 on the local windows firewall 

Login to Client-1 on Windows 10 and try to ping the Domain controller with ping -t <ipaddress>. If it goes through, connectivity is ensured.
</p>
<p>

**3.) Install Active Directory**
</p>
<br />

<p>
  
  ![image](https://github.com/akingsley22/configure-ad/assets/138138839/23bd2d87-a3a3-476e-8224-600ff932fa2c)

  ![image](https://github.com/akingsley22/configure-ad/assets/138138839/1f481b58-73b2-4839-9e9d-b9ca0cfb329e)

</p>
<p>
-Login to DC and Install active directory from Server Manager. 
-Promote as a DC: Set up a new forest e.g. "mydomain.com" and a password.
-Your VM is automatically going to restart once you install AD. 
-Log back into DC-1 as user: "mydomain.com\labuser".

 **PART 2**
 
 **Creating Organizational Units and End Users**

 - Open Active Directory Users and Computers.
 - Right click on "mydomain.com" and create new organization unit.

 ![image](https://github.com/akingsley22/configure-ad/assets/138138839/81e9d14d-c956-4d7b-8502-19cc83293686)

 -To create Users within organization units, right click on already created organizational unit and create new Users.
    
     -If you wish, you can add user to domain admins group by rights clicking on user, click add to group, enter object names (domain), check names and select domain admin.

 ![image](https://github.com/akingsley22/configure-ad/assets/138138839/87711012-a702-4d36-a957-601c5c23d213)

 -  Now you can connect back into VM as The Domain controller

  **PART 3**

  **Join Client-1 to the Domain**

  - Set Client-1's DNS settings to DC's Private IP address

  - Restart Client-1

![image](https://github.com/akingsley22/configure-ad/assets/138138839/c98e73fc-b2b6-420b-820d-411164af003e)

  -Log back into Client-1 as labuser and join it to the domain (computer will restart). 

  ![image](https://github.com/akingsley22/configure-ad/assets/138138839/55645b37-7d94-43cc-af09-32b94565826d)

  -Now you can log into Client-1 with your domain admin account.

  


     

 
 
</p>
<br />
