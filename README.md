<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>Objectives</h2>

- Get a better understanding for firewalls and network protocols

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/PDdWUFq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/vUHvDKn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 1: Creating the VMs and Downlaoding WireShark
  
- Create two VMs in Azure 
   - One VM running Windows 10 and the other running Linux(Ubuntu).
   - Make sure that the Linux computer is using the same Vnet as the Windows. 
- Log into the Windows computer and dowload [Wireshark](https://www.wireshark.org/download.html)
  
</p>
<br />

<p>
<img src="https://i.imgur.com/vUHvDKn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/lmWIdsc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/gYWcnCI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Observe ICMP Traffic
  
- Open Wireshark and filter to only ICMP traffic only. 
- Next, get the private IP address of the Linux computer and ping it from the Windows computer
- Once the pinging start there should be traffic starting to appear.
    - This is because ping uses the protocol ICMP(Internet Control Message Protocol). This protcol is used to communicate error or updates between two hosts. So when using ping the host is simply trying to connect to the other host.
- Back to Azure we will set up a firewall to block ICMP traffic and when we ping again it should not be able to connect again.
    - In Azure go to Network Securtiy Groups -> the Linux Computer -> Inbound Securtiy Rules -> Add -> Deny ICMP.
- Now if we go back to the Windows VM we should see request time out which means it is not able to connect. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Observe SSH Traffic
  
- In WireShark filter to only SSH Traffic only 
- From your Windows computer SSH into your Ubuntu VM.  
</p>
<br />
