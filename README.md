# Unboxing Active Directory with Group Policy Magic
![image](https://github.com/forza-dc/Active-Directory/blob/main/Microsoft%20Image%20Front.png)  
## Lab Overview  
Embarking on the journey of network administration using VirtualBox and Windows Server 2019 brings an exciting opportunity to delve into the world of Active Directory. In this step-by-step guide, we've navigated through the initial setup stages, from installing VirtualBox and Windows Server 2019 to configuring Active Directory Directory Services. Not only have we created a domain and configured the domain controller, but we've also taken the extra step of implementing a crucial aspect of network management - Group Policy. In this article, I'll walk you through the process I followed to set up a Group Policy restricting control panel access for a user group. Let's explore how these foundational steps lay the groundwork for a secure, well-organized network environment.
# Network Layout
![image](https://github.com/forza-dc/Active-Directory/blob/main/Network%20Diagram.jpg)  

# Setting Up VirtualBox and Virtual Machine
The initial step in my project involved configuring VirtualBox to create a seamless environment for a Windows 19 Server dedicated to Active Directory. Alongside, I set up a Windows 10 virtual machine as a client, enabling the seamless enforcement of policies from the server to the client's end.
![image](https://github.com/forza-dc/Active-Directory/blob/main/Setting%20Up%20VirtualBox%20and%20Virtual%20Machine.png) 

# Installing Windows Server 2019
Step 1- Follow the onscreen prompt to install windows server.

![image](https://github.com/forza-dc/Active-Directory/blob/main/Installing%20Win%2019%20Srv.jpg)  

Step 2 -  Ensure to choose 'Windows Server 2019 Standard Evaluation(Desktop Experience)".

![image](https://github.com/forza-dc/Active-Directory/blob/main/Windows%20Server%202019%20Standard%202.png) 

Step 3 -  Now you can log on to Windows. The Server Manager Dashboard opens up as shown below.

![image](https://github.com/forza-dc/Active-Directory/blob/main/Server%20Manager%20Screen.jpg) 

# Setting Up Windows 10 Machine (End User)

Step 1- Window is getting ready.

![image](https://github.com/forza-dc/Active-Directory/blob/main/Installing%20Win%2019%20Srv.jpg) 

Step 1- Now you can see the windows 10 dektop, we will be joining this machine to domain.

![image](https://github.com/forza-dc/Active-Directory/blob/main/Windows%2010%20main%20page.png) 



