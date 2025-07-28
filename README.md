<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory Deployed in the Cloud (Azure)</h1>
This project outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (22H2)

<h2>Walkthrough</h2>

<h3> Section 1: Installing Active Directory</h3>

<p>
<img src="https://github.com/user-attachments/assets/ff640680-a9aa-48a6-bb6e-66d9aacb9951" width=800/>
</p>
<p>

  - To begin the project, I logged into the DC-1 Virtual Machine and selected "Add Roles and Features" in Server Manager.
  - Next, I navigated to the Server Roles tab and selected "Active Directory Domain Services".

</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/b10ce9f2-e22b-4330-9269-ff71ccc55b80" width=800 />
</p>
<p>

  - After the installation was complete, I promoted the server to a domain controller.
  - Under "Deployment Operation", I selected "Add a new forest" and named the root domain "mydomain.com".

</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/c3d7f8a5-d5c3-4364-8d5d-e4261e39acd2" width=400 />
</p>
<p>

  - Once the forest was created, I restarted DC-1 and I logged back in as the user "mydomaincom\jrskanes".

</p>
<br />

<h3> Section 2: Creating a Domain Admin user within the domain </h3>
<table>
  <tr>
    <td>
      <img src="https://github.com/user-attachments/assets/6873e276-648d-4e2e-ab47-193b36bf5c14" />
    </td>
    <td>
      <img src="https://github.com/user-attachments/assets/3521ce4a-0e5e-43ba-b76e-3ef1823a82f6" />
 </td>
  </tr>
</table>

  - After logging back into DC-1, I navigated to the start menu and opened "Acitive Directory Users and Computers".
  - Once there, I right clicked "mydomain.com" to create a new Organizational Unit (OU).
  - I named the Organizational Unit "_EMPLOYEES".

</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/0ab2b38b-c7b4-49ba-9be1-e0eda465afeb" />
</p>
<p>

  - Next, I created another Organizational Unit (OU) named "_ADMINS".

</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/1f87466b-eebc-41c1-8f79-319dfe8c521a" />
</p>
<p>

  - Next, I right clicked the "_ADMINS" OU to create a new user.
  - I named the new user "Jane Doe" with the username of "jane_admin".

</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/685637c0-925f-4bdd-bfee-70363bcb143b" />
</p>
<p>

  - After that, I went into the _ADMINS folder and opened the Properties for Jane Doe.
  - I selected "Member Of" and added Jane Doe to the "Domain Admins" Security Group.
  - Next, I closed the the connection to DC-1 and logged back in as "mydoamin.com\jane_admin".

</p>
<br />

<h3> Section 3: Joining Client-1 to the domain (mydomain.com) </h3>
<p>
<img src="https://github.com/user-attachments/assets/03e86815-a1be-4cb7-bcf4-bc1fc81708bb" width=800 />
</p>
<p>

  - After logging into DC-1 as Jane Doe, I connected to Client-1 as the original local admin (jrskanes).
  - I navigated to the settings and clicked on "Rename this PC (Advanced).
  - In the "Computer Name" tab, I clicked "Change".
  - Under "Member Of", I selected "Domain" and entered "mydomain.com".

</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/00a735ff-d4ab-4590-989f-ba196c91ba5d" />
</p>
<p>
  - To join the domain, I used the jane_admin account login.

</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/830f5a24-f016-4267-a382-9c5f5b6c9cf7" />
</p>
<p>

  - Next, I logged back into DC-1 as jane_admin and navigated to Active Directory Users and Computers.
  - I expanded mydomain.com to ensure that client-1 was there.
  - I created a new Organizational Unit (OU) named "_CLIENTS".
  - I dragged client-1 into the "_CLIENTS" Organizational Unit.

</p>
<br />

<h3> Section 4: Setting up Remote Desktop for non-administrative users on Client-1 </h3>
<p>
<img src="https://github.com/user-attachments/assets/275401d9-1095-4ca5-ae66-a4fd6f950122" width=800 />
</p>
<p>

  - I logged into Client-1 as mydomain.com\jane_admin.
  - In the start menu, I opened system properties and selected "Remote Desktop".
  - Under "Remote Desktop Users", I added the "Domain Users" group which will allow all users in the group access to remote desktop.

</p>
<br />

<h3> Section 5: Creating Users </h3>
<p>
<img src="https://github.com/user-attachments/assets/0f40c26a-4dfc-4d7f-80da-5e7a87a6f103" width=800 />
</p>
<p>

  - I logged back into DC-1 as jane_admin
  - I opened Powershell_ISE as an administrator and ran a script that automatically generated multiple employee user accounts in the _EMPLOYEES Organizational Unit (OU).

</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/f599663b-1fd3-4947-87fd-5d2d09b17b7f" width=800 />
</p>
<p>

  - After running the script, I navigated to Active Directory Users & Computers to ensure that all of the user accounts were correctly listed in the _EMPLOYEES Organization Unit (OU).

</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/966ab955-6d25-427d-b903-dd1beaa69588" />
</p>
<p>

  - To finish the project, I chose a random employee user account (bib.tel) and successfully logged into Client-1.


