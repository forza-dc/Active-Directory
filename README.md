# 👨🏻‍💻 🌎 🔐 Unboxing Active Directory with Group Policy Magic 👨🏻‍💻 🌎 🔐
![image](https://github.com/forza-dc/Active-Directory/blob/main/Microsoft%20Image%20Front.png)  

## Lab Overview  
Embarking on the journey of network administration using VirtualBox and Windows Server 2019 brings an exciting opportunity to delve into the world of Active Directory. In this step-by-step guide, we've navigated through the initial setup stages, from installing VirtualBox and Windows Server 2019 to configuring Active Directory Directory Services. Not only have we created a domain and configured the domain controller, but we've also taken the extra step of implementing a crucial aspect of network management - Group Policy. In this article, I'll walk you through the process I followed to set up a Group Policy restricting control panel access for a user group. Let's explore how these foundational steps lay the groundwork for a secure, well-organized network environment.

## Network Layout

![image](https://github.com/forza-dc/Active-Directory/blob/main/Network%20Diagram.jpg)  

## Setting Up VirtualBox and Virtual Machine
The initial step in my project involved configuring VirtualBox to create a seamless environment for a Windows 19 Server dedicated to Active Directory. Alongside, I set up a Windows 10 virtual machine as a client, enabling the seamless enforcement of policies from the server to the client's end.
![image](https://github.com/forza-dc/Active-Directory/blob/main/Setting%20Up%20VirtualBox%20and%20Virtual%20Machine.png) 

## Installing Windows Server 2019
Step 1- Follow the onscreen prompt to install windows server.

![image](https://github.com/forza-dc/Active-Directory/blob/main/Installing%20Win%2019%20Srv.jpg)  

Step 2 -  Ensure to choose 'Windows Server 2019 Standard Evaluation(Desktop Experience)".

![image](https://github.com/forza-dc/Active-Directory/blob/main/Windows%20Server%202019%20Standard%202.png) 

Step 3 -  Now you can log on to Windows. The Server Manager Dashboard opens up as shown below.

![image](https://github.com/forza-dc/Active-Directory/blob/main/Server%20Manager%20Screen.jpg) 


## Setting Up Windows 10 Machine (End User)

Step 1- Window is getting ready.

![image](https://github.com/forza-dc/Active-Directory/blob/main/Setting%20up%20windows%2010.png) 

Step 1- Now you can see the windows 10 dektop, we will be joining this machine to domain.

![image](https://github.com/forza-dc/Active-Directory/blob/main/Windows%2010%20main%20page.png) 

## Configuring the Active Directory Directory Services(AD DS)
Now we would set up this computer as a domain controller. We do this by installing the AD DS role to the server.

Step 1 - Click on Add Role and Features in the Dashboard. This opens the Add Roles and Features Wizard.
![image](https://github.com/forza-dc/Active-Directory/blob/main/AD%20DC%20Services.png) 

Step 2 - Click on Next > Next until you have a list of Features. In the list, check Active Directory Directory Services as shown below:
![image](https://github.com/forza-dc/Active-Directory/blob/main/AD%20DC%20Step%202.png) 

## Create a Domain and Configure the Domain Controller

Step 1 - Click on the yellow triangle at the upper right and click 'Promote this server to domain controller'. The 'Active Directory Domain Services Configuration Wizard will open.

![image](https://github.com/forza-dc/Active-Directory/blob/main/Create%20DC%20Step%201.png) 

Step 2 - Click on 'Add a new forest' and enter a name for the domain and add .local suffix. For me, it's soran.local.
![image](https://github.com/forza-dc/Active-Directory/blob/main/Create%20DC%20step%202.png) 

Step 3 - Click on next and then enter a password. Click Next. As you can see I can login with SORAN\Adminstrator. Enter the password you set.
![image](https://github.com/forza-dc/Active-Directory/blob/main/Create%20DC%20step%202.png) 

As I'm using Virtualbox Bridged Network on both the Client machine and AD Server, you just need to use the AD Server's IP in the IPV4 DNS settings on the client side. After that, verify the connectivity using 'ping pong' on both sides. Please refer to the snapshot below while verifying the connection from the client side towards the end user:

![image](https://github.com/forza-dc/Active-Directory/blob/main/Ping%20Pong.jpg) 

## Joining Client Machines to the Domain

          a) Right-click on "This PC" or "My Computer" and select "Properties."
          b) In System Properties, go to the "Computer Name" tab.
          c) Remove WORKGROUP, select domain and restart.
          d) Select the "Domain" option and enter the domain name "soran.local", 
          
![image](https://github.com/forza-dc/Active-Directory/blob/main/Joining%20domain.jpg) 

Step 5 - Provide domain admin credentials and machine will be restarted. A welcome message will appear: 
![image](https://github.com/forza-dc/Active-Directory/blob/main/Joining%20domain.jpg)

## New Domain User Creation
I intend to create a new user within the 'soran.local' domain to implement targeted group policies. 

          a) Access 'Active Directory Users and Computers.'
          b) Within the Active Directory Users and Computers console, navigate to the 'soran.local' domain. Right-click and select 'New User.'
          c) A new window for creating a user object will appear. Fill in the required user information, including the password, and proceed by clicking Next.

![image](https://github.com/forza-dc/Active-Directory/blob/main/Joining%20domain.jpg) 

Now, I'm able to login with the newly created user.
![image](https://github.com/forza-dc/Active-Directory/blob/main/New%20user%20login.jpg) 

## Group Policy Creation and Enforcement

Step 1 - Our first step is to create a new group to add newly created user. Follow below steps to create a new grouo:

          a) Open 'Active Directory Users and Computers.'
          b) Right-click on the domain, select 'New,' then 'Group.'
          c) Enter the group details and confirm.

As I created a group named "DevSecOps Team". 

Step 2 - Adding newly created user (forza.taye) to the group(DevSecOps Team).
![image](https://github.com/forza-dc/Active-Directory/blob/main/Group%20joining%20to%20user.jpg) 

Step 3 - Creating Group Policy Object

          a) Open Group Policy Management Console.
          b) Right-click on the domain or OU and choose "Create a GPO in this domain".
          c) Enter a name for the GPO (DevSecOps GPO-1) and click "OK".
![image](https://github.com/forza-dc/Active-Directory/blob/main/New%20Gpo.jpg) 

Step 3 - Crearting Policy on GPO

I intend to enforce a policy that prevents any user belonging to the 'DevSecOps Team' group from adding or removing programs. Whenever a user from this group attempts to install or reinstall a program, it will prompt for administrator credentials.

          a) Open Group Policy Management Console.
          b) Navigate to the desired GPO, as my GPO is "DevSecOps GPO-1".
          c) Right-click on the chosen GPO and select "Edit."
          d) Under "User Configuration," go to "Policies" > "Administrative Tempplate: Policy Defination" > "Control Panel" > "Add or Remove Programs". Add or Remove tab will open.
          e) On Add or Remove Programs tab, double click on "Remove Add or Remove Programs". A new tab for Remove Add or Remove Programs will open.
          f) Click "Enabled" and click "Apply".
![image](https://github.com/forza-dc/Active-Directory/blob/main/Policy%20Creation%20for%20Add%20or%20remove%20programs.jpg) 

Step 4 - Policy Enforcement

Once you done with the policy creation, Navigate to the desired GPO, as my GPO is "DevSecOps GPO-1". Right click on policy and elect Enforce.
![image](https://github.com/forza-dc/Active-Directory/blob/main/Policy%20Enforcement.png) 


## Policy Testing on User End

After implementing the policy, I logged in using a user (forza.taye) who is in the group (DevSecOps Team). Upon attempting to download WinRAR software, the system prompted for admin credentials, affirming the policy's restriction on software installation without elevated access.

![image](https://github.com/forza-dc/Active-Directory/blob/main/Winrar%20software%20installation%20attempt.jpg) 

Let's put the administrator credentials to verify if the system allows the software installation.

![image](https://github.com/forza-dc/Active-Directory/blob/main/Administrator%20password%20to%20install%20the%20program.jpg) 

Upon entering the admin credentials, WinRAR installed successfully. Our policy implementation appears to be effective. 🚀🚀🚀🚀

![image](https://github.com/forza-dc/Active-Directory/blob/main/Winrar%20Successfully%20Installed..jpg) 

👨🏻‍💻 🚀 Active Directory setup, policy creation, and enforcement have been successfully completed and tested. The project concludes with a demonstrated implementation of user restrictions on software installation, validating the effectiveness of the policies established. 👨🏻‍💻 🚀

