# Azure-Network-Protocols-
<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark and experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTPS, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Step 1: Create a resource group with a virtual network and add two VMs into the resource group and the same virtual network. One should be Windows 10 and the other should be Ubuntu 
- Step 2: Log into the Windows VM with RDP and download wireshark to observe network traffic. 
- Step 3: On the command line, send a ping to your Ubuntu VM and observe the Wireshark traffic.
- Step 4: Use network security groups to ignore inbound ICMP traffic and observe in wireshark.
- Step 5: Use Wireshark to examine different ports and see the traffic moving in and out with protocols such as DHCP, DNS, SSH, and RDP.

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
- Create your Windows and Ubuntu VMs in Azure, and ensure they are in the same resource group and a part of the same virtual network. I found it easier to create the virtual network first, so you don't have to wait for it to complete its creation before making the next VM. 
</p>
<p>
- Once both VMs are running, use RDP to log to the Windows 10 VM and install Wireshark.
</p>
<p>
- Wireshark will then be used to observe ICMP traffic. Open the command line and send a ping to the Ubuntu VM you used by typing ping and then the private IP of the Ubuntu VM. 
</p>
<p>
- Send pings from the Windows VM to the Ubuntu VM perpetually by typing "ping (Ubuntu private IP) -t." In Azure, open the network security group of the Ubuntu VM, create a new rule denying inbound ICMP traffic, and observe in Wireshark and on the command line. Ensure the new rule has the lowest number, indicating it has the highest priority so another rule doesn't overrule it.
</p>
<p>
- Then delete the rule and observe as the pings start to receive replies again. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, we are going to observe SSH traffic with Wireshark. Look at SSH traffic in Wireshark in the same Windows VM and open up PowerShell. Please remember your login for the Ubuntu VM. 
</p>
<p>
Once PowerShell is open, type "ssh (your login)@(the Ubuntu private IP)." It will prompt you to type in the password, which will be invisible. Type it and hit enter. 
</p>
<p>
- Then, watch in Wireshark as the SSH traffic appears when connecting to the server. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In Wireshark, change the traffic you are observing to DHCP traffic. Then, in Powershell, type "ipconfig /renew." This will get you a new IP address, and you should witness some DHCP traffic. 
</p>
<p>
- Next, we will observe DNS traffic in Wireshark, then open a web browser and browse any website. You should see DNS traffic in Wireshark. 
</p>
<p>
- Lastly, we will look at RDP traffic; simply observe that traffic in Wireshark should be a continuous stream since we are connecting to the Windows 10 VM using RDP. If you are having trouble and cannot observe by typing RDP, try "tcp.port == 3389."
</p>
<p>
- Once complete, delete the VMs and the resource group in Azure. 
</p>
<br />
