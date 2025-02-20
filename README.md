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
            <li>Set permissions and share folders:
                <ul>
                    <li><strong>read-access:</strong> Domain Users → Read</li>
                    <li><strong>write-access:</strong> Domain Users → Read/Write</li>
                    <li><strong>no-access:</strong> Domain Admins → Read/Write</li>
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
                </ul>
            </li>
            <li>Assign permissions to the <code>accounting</code> folder:
                <ul>
                    <li>Group: ACCOUNTANTS</li>
                    <li>Permissions: Read/Write</li>
                </ul>
            </li>
            <li>On <strong>Client-1</strong>, as <code>&lt;someuser&gt;</code>, try to access <code>\\DC-1\accounting</code>. It should fail.</li>
        </ol>
    </details>
</p>
<p>
  <details>
        <summary><strong>Step 5: Grant User Access & Test Again</strong></summary>
        <ol>
            <li>On <strong>DC-1</strong>, add <code>&lt;someuser&gt;</code> to the <strong>ACCOUNTANTS</strong> group.</li>
            <li>Log out of <strong>Client-1</strong> as <code>&lt;someuser&gt;</code>.</li>
            <li>Log back in as <code>&lt;someuser&gt;</code>.</li>
            <li>Test access again to <code>\\DC-1\accounting</code>. Does it work now?</li>
        </ol>
    </details>
</p>
<p>
  <details>
        <summary><strong>Step 6: Clean Up or Continue Practicing</strong></summary>
        <p>If you are <strong>done</strong>, you can <strong>delete the VMs</strong>.</p>
        <p>If you want to <strong>save money</strong> but keep practicing, <strong>stop the VMs</strong> in the <strong>Azure Portal</strong>.</p>
    </details>
</p>
