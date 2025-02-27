<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<!--<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)
-->
<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Step 1 Start Your Virtual Machines
- Step 2 Create Sample File Shares with Various Permissions
- Step 3 Test File Share Access as a Normal User
- Step 4 Create an "ACCOUNTANTS" Security Group & Assign Permissions
- Step 5 Grant User Access & Test Again
- Step 6 Clean Up or Continue Practicing

<h2>Actions and Observations</h2>

<p>
  <details>
        <summary><strong>Step 1: Start Your Virtual Machines</strong></summary>
        <p>Ensure that <strong>DC-1</strong> and <strong>Client-1</strong> are turned on in the <strong>Azure Portal</strong>.</p>
    </details>
</p>

<p>
  <details>
        <summary><strong>Step 2: Create Sample File Shares with Various Permissions</strong></summary>
        <ol>
            <li>Log into <strong>DC-1</strong> as your domain admin account: <code>mydomain.com\jane_admin</code></li>
            <li>Log into <strong>Client-1</strong> as a normal user: <code>mydomain\&lt;someuser&gt;</code></li>
            <li>On <strong>DC-1</strong>, create the following folders in <code>C:\</code>:
                <ul>
                    <li>read-access</li>
                    <li>write-access</li>
                    <li>no-access</li>
                    <li>accounting</li>
                </ul>
            </li>
                <p>
    <img src="https://github.com/Drew-Stokes/azure-network-protocols/blob/520d20d2ff0618b56f85feaf391c866cb1aeec74/create_4_folders.png" height="30%"width="30%" alt="Disk Sanitization Steps"/>
    </p>
            <li>Set permissions and share folders:
                <ul>
                    <li><strong>read-access:</strong> Domain Users → Read</li>
                  <p>
<img src="https://github.com/Drew-Stokes/azure-network-protocols/blob/520d20d2ff0618b56f85feaf391c866cb1aeec74/readAccess_domain_users.png" height="30%" width ="30%" alt="Disk Sanitization Steps"/>
</p>
                    <li><strong>write-access:</strong> Domain Users → Read/Write</li>
                  <p>
<img src="https://github.com/Drew-Stokes/azure-network-protocols/blob/520d20d2ff0618b56f85feaf391c866cb1aeec74/writeAccess_DomainUsers.png" height="30%" width="30%" alt="Disk Sanitization Steps"/>
</p>
                    <li><strong>no-access:</strong> Domain Admins → Read/Write</li>
                  <p>
<img src="https://github.com/Drew-Stokes/azure-network-protocols/blob/520d20d2ff0618b56f85feaf391c866cb1aeec74/no_access_readwrite.png" height="30%" width="30%" alt="Disk Sanitization Steps"/>
</p>
                    <li>(Skip accounting for now)</li>
                </ul>
            </li>
        </ol>
    </details>
</p>
<p>
  <details>
        <summary><strong>Step 3: Test File Share Access as a Normal User</strong></summary>
        <ol>
            <li>On <strong>Client-1</strong>, open the Run window (<code>Win + R</code>) and type: <code>\\dc-1</code></li>
            <li>Test access to the folders:
                <ul>
                    <li>Which folders can you <strong>open</strong>?</li>
                    <li>Which folders can you <strong>write to</strong>?</li>
                    <li>Do the results make sense?</li>
                </ul>
            </li>
        </ol>
    </details>
</p>
<p>
  <details>
        <summary><strong>Step 4: Create an "ACCOUNTANTS" Security Group & Assign Permissions</strong></summary>
        <ol>
            <li>On <strong>DC-1</strong>, open <strong>Active Directory Users and Computers (ADUC)</strong>.</li>
            <li>Create a security group:
                <ul>
                    <li>Name: <strong>ACCOUNTANTS</strong></li>
                    <li>Type: <strong>Security Group</strong></li>
                  <p>
<img src="https://github.com/Drew-Stokes/azure-network-protocols/blob/2db2dcec3cfa878f21f20c9e7377f1a05d1751e9/accountants_security_group.png" height="30%" width="30%" alt="Disk Sanitization Steps"/>
</p>
                </ul>
            <li>On <strong>Client-1</strong>, as <code>&lt;someuser&gt;</code>, try to access <code>\\DC-1\accounting</code>. It should fail.</li>
          <p>
<img src="https://github.com/Drew-Stokes/azure-network-protocols/blob/2db2dcec3cfa878f21f20c9e7377f1a05d1751e9/No_access_accounting.png" height="30%" width="30%" alt="Disk Sanitization Steps"/>
</p>
        </ol>
    </details>
</p>
<p>
  <details>
        <summary><strong>Step 5: Grant User Access & Test Again</strong></summary>
        <ol>
            <li>On <strong>DC-1</strong>, add <code>&lt;someuser&gt;</code> to the <strong>ACCOUNTANTS</strong> group.</li>
          <p>
<img src="https://github.com/Drew-Stokes/azure-network-protocols/blob/2db2dcec3cfa878f21f20c9e7377f1a05d1751e9/add_user_to_accounts_group.png" height="30%" width="30%" alt="Disk Sanitization Steps"/>
</p>
            <li>Log out of <strong>Client-1</strong> as <code>&lt;someuser&gt;</code>.</li>
            <li>Log back in as <code>&lt;someuser&gt;</code>.</li>
            <li>Test access again to <code>\\DC-1\accounting</code>. Does it work now?</li>
          <p>
<img src="https://github.com/Drew-Stokes/azure-network-protocols/blob/8be28b51fdbfaf83108ea408aad3cd882cff5614/Sign_back_in-check_accountant_folder.png" height="30%" width="30%" alt="Disk Sanitization Steps"/>
</p>
        </ol>
    </details>
</p>

