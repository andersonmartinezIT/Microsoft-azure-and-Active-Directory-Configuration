
Using Microsoft Azure and installing Active Directory and Creating Administrative and User Accounts 
<p align="center">

</p>

<h1>Microsoft Azure and Active Directory Configuration</h1>

<h2>Video Demonstration</h2>

-<h3>Check out <a href="https://youtu.be/lfbgLHDZXio" target="_blank">YouTube: How to install Active Directory and configure accounts</a>.</h3>

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<p><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Setup Resources in Azure</span></span></span></p>

<p style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Create the Domain Controller VM (Windows Server 2022) named &ldquo;DC-1&rdquo;</span></span></span></p>

<p style="list-style-type:lower-alpha"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Take note of the Resource Group and Virtual Network (Vnet) that get created at this time</span></span></span></p>

<p style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Set Domain Controller&rsquo;s NIC Private IP address to be static</span></span></span></p>

<p style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Create the Client VM (Windows 10) named &ldquo;Client-1&rdquo;. Use the same Resource Group and Vnet that was created in Step 1.a (make sure that Client-1 is on the same network as the DC-1 windows server computer. You might have to wait a while until Azure is done creating the network for DC-1.)</span></span></span></p>

<p style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Ensure that both VMs are in the same Vnet (You can check by clicking on the virtual machine you then looking at the overview information)</span></span></span></p>

<p>&nbsp;</p>

<p><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Ensure Connectivity between the client and Domain Controller</span></span></span></p>

<ol start="5">
	<li style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Login to Client-1 with Remote Desktop (make sure to get the IP address of Client-1 to control it with the remove desktop software) and ping DC-1&rsquo;s private IP address with </span></span></span><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000"><em>ping -t &lt;ip address&gt;</em></span></span></span><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000"> (perpetual ping)</span></span></span></li>
	<li style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Login to the Domain Controller (make sure to get the IP address of DC-1 to control it with the remove desktop software) and enable ICMPv4 in on the local windows Firewall (You can also look it up by the name &quot;Windows Defender Firewall with Advance Security&quot;). Click on inbound. Then enable the options related to ICMPv4 protocols.&nbsp;</span></span></span></li>
	<li style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Check back at Client-1 to see the ping succeed. You will see that the ping is finally getting a reply.</span></span></span></li>
</ol>

<p>&nbsp;</p>

<p><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Install Active Directory</span></span></span></p>

<ol start="8">
	<li style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Login to DC-1 and install Active Directory Domain Services. Select &quot;Add roles and features&quot;. The installation type should be &quot;Role Based and Feature Based.&quot; On the select destination server it should be the private IP of the DC-1 virtual computer you created on Azure, which you can find by clicking on the virtual machine name in Azure then looking at the IP address in the overwview information.&nbsp;</span></span></span></li>
	<li style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">On Server Roles make sure to select &quot;Active directory domain service&quot; then keep clicking next until you see the &quot;install&quot; button. It will take a few minutes to download.</span></span></span></li>
	<li style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Once is done installing, on the server manager dashboard click on the flag icon at the top right. Promote as a DC: Setup a new forest as </span></span></span><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000"><u>mydomain.com</u></span></span></span><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000"> (can be anything, just remember what it is)</span></span></span></li>
	<li style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Restart and then log back into DC-1 as user: </span></span></span><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000"><u>mydomain.com\labuser</u></span></span></span></li>
</ol>

<p>&nbsp;</p>

<p><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Create an Admin and Normal User Account in AD</span></span></span></p>

<ol start="11">
	<li style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">In Active Directory Users and Computers (ADUC), right click on the domain and create an Organizational Unit (OU) called &ldquo;_EMPLOYEES&rdquo;</span></span></span></li>
	<li style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Create another&nbsp;Organizational Unit named &ldquo;_ADMINS&rdquo;</span></span></span></li>
	<li style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Create a new employee named &ldquo;Jane Doe&rdquo; (same password) with the username of &ldquo;jane_admin&rdquo;</span></span></span></li>
	<li style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Add jane_admin to the &ldquo;Domain Admins&rdquo; Security Group</span></span></span></li>
	<li style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Log out/close the Remote Desktop connection to DC-1 and log back in as &ldquo;mydomain.com\jane_admin&rdquo;</span></span></span></li>
	<li style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">User jane_admin as your admin account from now on</span></span></span></li>
</ol>

<p><br />
&nbsp;</p>

<p><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Join Client-1 to your domain (mydomain.com)</span></span></span></p>

<ol start="17">
	<li style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">From the Azure Portal, set Client-1&rsquo;s DNS settings to the DC&rsquo;s Private IP address</span></span></span></li>
	<li style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">From the Azure Portal, restart Client-1</span></span></span></li>
	<li style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart)</span></span></span></li>
	<li style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the &ldquo;Computers&rdquo; container on the root of the domain</span></span></span></li>
	<li style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Create a new Organizational Unit named &ldquo;_CLIENTS&rdquo; and drag Client-1 into there (Step is not really necessary, just for organizational purposes.&nbsp;</span></span></span></li>
</ol>

<p><br />
&nbsp;</p>

<p><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Setup Remote Desktop for non-administrative users on Client-1</span></span></span></p>

<ol start="22">
	<li style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Log into Client-1 as mydomain.com\jane_admin and open system properties</span></span></span></li>
	<li style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Click &ldquo;Remote Desktop&rdquo;</span></span></span></li>
	<li style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Allow &ldquo;domain users&rdquo; access to remote desktop</span></span></span></li>
	<li style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">You can now log into Client-1 as a normal, non-administrative user now</span></span></span></li>
	<li style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Normally you&rsquo;d want to do this with Group Policy that allows you to change MANY systems at once&nbsp;</span></span></span></li>
</ol>

<p>&nbsp;</p>

<p><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Create&nbsp; some additional users and attempt to log into client-1 with one of the users</span></span></span></p>

<p>&nbsp;</p>

<ol start="27">
	<li style="list-style-type:decimal"><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">attempt to log into Client-1 with one of the accounts (take note of the password in the script)</span></span></span></li>
</ol>

<p>&nbsp;</p>

<p><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Finish.&nbsp;</span></span></span></p>

<p><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">For a better understand please see the Youtube video link above.&nbsp;</span></span></span></p>

<p>&nbsp;</p>


<p><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">Finish.&nbsp;</span></span></span></p>

<p><span style="font-size:12pt"><span style="font-family:Arial,sans-serif"><span style="color:#000000">For a better understand please see the Youtube video link above.&nbsp;</span></span></span></p>

<p>&nbsp;</p>
