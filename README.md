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

  <p><img width="857" alt="Screenshot 2025-01-10 at 3 17 24 PM" src="https://github.com/user-attachments/assets/6e457ff1-b50a-4e47-aeca-39a4e8b02190" /></p>

<p>In PowerShell if we ping "mothership" we will notice the IP address that it pings.</p>
<br>

<img width="1241" alt="Screenshot 2025-01-10 at 3 18 03 PM" src="https://github.com/user-attachments/assets/d611b6f4-a122-405e-870f-2d4b1ca61e83" />
<p>Back within DNS manager, change the IP address to 8.8.8.8</p>

<br>

<img width="856" alt="Screenshot 2025-01-10 at 3 19 02 PM" src="https://github.com/user-attachments/assets/1fc2d923-64be-4af6-93d5-3eeef83544a7" />
</p>
<p>Ping "mothership" again in PowerShell and notice that it still pings 10.0.0.4</p>
<p>
  This is due to the DNS cache still having mothership as 10.0.0.4
</p>
<br>

   <p>  <img width="823" alt="Screenshot 2025-01-10 at 3 21 32 PM" src="https://github.com/user-attachments/assets/0957a59b-6f8d-40b9-b568-a047f70b5756" /></p>
 <p>In PowerShell type "ipconfig /displaydns" to see the DNS cache still has 10.0.0.4 for mothership.</p>
<br>
<p><img width="857" alt="Screenshot 2025-01-10 at 3 22 44 PM" src="https://github.com/user-attachments/assets/2d8148bc-bdaf-4d0d-aa82-dd5c72be2e09" /></p>

<p>Type "ipconfig /flushdns" and then "ipconfig /dnsdisplay". This will let us see the emptied DNS cache.</p>
  <br>
  <h3>
    CNAME
  </h3>
<table>
  <tr>
    <td>
      <img width="966" alt="Screenshot 2025-01-10 at 3 23 29 PM" src="https://github.com/user-attachments/assets/106444bf-da12-4fec-9bf6-d392c20886f8" />
    </td>
    <td>
      <img width="400" alt="Screenshot 2025-01-10 at 3 24 46 PM" src="https://github.com/user-attachments/assets/d88162d7-57d7-4624-88d4-9b94ddca43ab" />
    </td>
  </tr>
</table>

<p>Within DNS manager add a new CNAME. Use "search" and link it to google.com</p>
<br>
<p><img width="858" alt="Screenshot 2025-01-10 at 3 25 55 PM" src="https://github.com/user-attachments/assets/8cdc347e-77f9-4963-a012-be776125692c" />
</p>
<p>Within PowerShell enter "nslookup search" and notice that it looks up google.com's IP address. </p>





