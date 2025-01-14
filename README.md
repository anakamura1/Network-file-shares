<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Understanding Network File Share Permissions</h1>
This tutorial will walk through how to configure network file share permissions and how they affect users in Active Directory. <br />

<h2>Prerequisites</h2>
See the links below to set up for this lab:
Creating Virtual Machines www.github.com/anakamura1/vm-creation
Active Directory Setup www.github.com/anakamura1/ad-configuration

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<table>
  <tr>
    <td>
      <img width="1126" alt="Screenshot 2025-01-10 at 3 30 54 PM" src="https://github.com/user-attachments/assets/f704348e-b224-437e-b5b1-91895317f64e" />
    </td>
    <td>
      <img width="1122" alt="Screenshot 2025-01-10 at 3 31 36 PM" src="https://github.com/user-attachments/assets/fc244a86-1fa2-4a3c-b349-989fd71ecdde" />
    </td>
  </tr>
</table>
<p>In DC-1, login as an admin and create four folders in the C-drive.</p>
<p>Right click on each folder and click properties. Within properties, click share and configure the share settings</p>
<p>Folder: “Read-access”, Group: “Domain Users”, Permission: “Read”
Folder: “Write-access”,  Group: “Domain Users”, Permissions: “Read/Write”
Folder: “No-access”, Group: “Domain Admins”, “Permissions: “Read/Write”
  We will skip the HR Only folder for now.
</p>
<br>

<table>
  <tr>
    <td>
<img width="399" alt="Screenshot 2025-01-10 at 3 33 40 PM" src="https://github.com/user-attachments/assets/7da2d858-a060-4e05-996c-ceeaf5ef59d2" />
    </td>
    <td>
<img width="1123" alt="Screenshot 2025-01-10 at 3 33 56 PM" src="https://github.com/user-attachments/assets/f4ccbac6-a754-4e6d-b111-0cb23d7c3c80" />
    </td>
  </tr>
</table>

<p>Within Client-1, log in as any user and go to Start -> Run -> \\dc-1</p>
<p>This will open the shared folders and notice that they the permissions are enforced.</p>
  <br>

<p><img width="751" alt="Screenshot 2025-01-10 at 3 35 46 PM" src="https://github.com/user-attachments/assets/73fdf9a6-592f-492e-a722-25cdf9b28483" />
</p>
<p>
  Back in DC-1, in Active Directory Users and Computers, create a new group named "HR"
</p>
<br>

<p><img width="752" alt="Screenshot 2025-01-10 at 3 36 17 PM" src="https://github.com/user-attachments/assets/1a7a038c-19e8-4d1f-bf5b-ebb6f750b1b2" /></p>
<p>In _EMPLOYEES, make a user a member of the group "HR"</p>
<br>



<table>
  <tr>
    <td>
<img width="1122" alt="Screenshot 2025-01-10 at 3 37 39 PM" src="https://github.com/user-attachments/assets/7b10a7ea-1955-4109-8a32-3b2f286abf73" />
    </td>
    <td>
<img width="1126" alt="Screenshot 2025-01-10 at 3 39 29 PM" src="https://github.com/user-attachments/assets/5f358992-1030-4817-9215-6d85b163b999" />
    </td>
  </tr>
</table>

<P>Back in DC-1, go to the HR only folder and change the share properties. Add the group HR in the share settings. </P>
  <p>Back in Client-1, log in as the user that was added to the HR group and access the HR only folder</p>
  <br>





