![image](https://github.com/user-attachments/assets/949dbcca-9433-46e0-aa42-27a4789dbc40)<p align="center">
<img src="https://i.imgur.com/Mf76DFC.jpeg" alt="Permissions Photo"/>
</p>

<h1>Understanding File Permissions</h1>
This lab centers around file permissions and shared resources within an Active Directory domain. In a business environment, managing file permissions and shares is crucial to ensuring that users have the correct access to the files they need. This lab builds upon a previous exercise, where I joined a client machine to my domain, ernestotest.com. I am logged in as Jane Doe (an administrator) on the domain controller VM and as a regular user on the client VM. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Active Directory Domain Services
- Remote Desktop

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 Pro (21H2)

<h2>File Permissions Configuration Steps</h2>
<p>
To set permissions for folders and files, we first need to create the folders we want to share. While logged in as an admin on the domain controller VM, I created four appropriately named folders on the C:\ drive. To share a folder and assign permissions, open the folder's Properties, and click on Share under the Sharing tab. From there, you can specify the users on the network to share with and assign the necessary permissions. I have set the following permissions for the folders (with the accounting folder's permissions to be changed later):

- Domain Users can Read the read-access folder and they have Read/Write permissions on the write-access folder
- Domain Admins have Read/Write access to the no-access folder
</p>
<br />

<p>
<img src="https://i.imgur.com/VTmGpJN.png" height="80%" width="80%" alt="Permissions Steps"/>
<img src="https://i.imgur.com/scZXP9r.png" height="80%" width="80%" alt="Permissions Steps"/>
</p>

<p>
On the client VM, navigate to the shared folders in File Explorer using the path: \dc-1. You'll notice that some folders only allow you to view files without adding new ones, while one folder doesn't allow access at all. This is because, as a Domain User, the permissions for each folder are linked to the relevant Security Group and the specific permissions set for users within that group.
</p>
<p>
<img src="https://i.imgur.com/CZ0yjst.png" height="80%" width="80%" alt="Permissions Steps"/>
</p>


<p>
Next, we'll create a new Security Group and assign the appropriate permissions to the accounting folder. On the domain controller, open the Active Directory Users and Computers panel and create a new Group named ACCOUNTANTS. After creating the group, go to the accounting folder and assign Read/Write permissions to the ACCOUNTANTS Group.
</p>
<br />

<p>
<img src="https://i.imgur.com/nVPVv6Z.png" height="80%" width="80%" alt="Permissions Steps"/>
<img src="https://i.imgur.com/BYHy7cb.png" height="80%" width="80%" alt="Permissions Steps"/>
<img src="https://i.imgur.com/A7qJoMe.png" height="80%" width="80%" alt="Permissions Steps"/>
<img src="https://i.imgur.com/ikqumCN.png" height="80%" width="80%" alt="Permissions Steps"/>
</p>


<p>
The user cannot access the accounting folder because they are not part of the ACCOUNTANTS Security Group. Log off the client so that the permissions are in place by the time the client is logged into again. On the domain controller, open the ACCOUNTANTS Properties on Active Directory Users and Computers. In the Members tab, add the respective user. In my case, it is bon.rovej. Upon logging into the client, bon.rovej is now able to open the accounting folder because they are part of ACCOUNTANTS.
<br />

<p>
<img src="https://i.imgur.com/xev1Svv.png" height="80%" width="80%" alt="Permissions Steps"/>
<img src="https://i.imgur.com/SHotVB2.png" height="80%" width="80%" alt="Permissions Steps"/>
</p>


<h2>Lessons Learned </h2>

This lab made me understand how file permissions work in the context of Windows/Active Directory. In a real setting, I might have to set permissions so that people can only access what they need to in order to complete their work. It is not necessary to give more permissions than what is needed.
