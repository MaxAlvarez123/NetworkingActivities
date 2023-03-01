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
    - This is because ping uses the internet protocol ICMP(Internet Control Message Protocol). This protcol is used to communicate error or updates between two hosts. So when using ping the host is simply trying to connect to the other host.
- Back to Azure we will set up a firewall to block ICMP traffic and when we ping again it should not be able to connect again.
    - In Azure go to Network Securtiy Groups -> the Linux Computer -> Inbound Securtiy Rules -> Add -> Deny ICMP.
- Now if we go back to the Windows VM we should see request time out which means it is not able to connect. 
</p>
<br />

<p>
<img src="https://i.imgur.com/2ARue7J.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Observe SSH Traffic
  
- In WireShark filter to only SSH Traffic only
    - You can also use tcp.port == 22 as port 22 is the port SSH uses.
- From your Windows computer SSH into your Ubuntu VM.  
- Once login you will start seeing traffic. 
- And notice that evertime you type into your Ubnuntu computer more traffic appears 
- This is becuause SSH or Secure Shell is a internet protcol that is used when connecting to another computer securely. Once login SSH really has no GUI besides the command line. So to navigate around the linux computer you will have to know linux commands. That is why you see traffic when navigating the Ubuntu computer as your Window's computer communicate over SSH. 
</p>
<br />
<br />

<p>
<img src="https://i.imgur.com/EwYpIZ0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Observe DHCP Traffic
  
- In Wireshark filter for DHCP traffic only.
- in Powershell type the command ipconfig /renew.
  - what this command does is that it issues you a new ip address.
- Once entered you should see some traffic comming in.
- This is because DHCP or Dyanmic Host Configuration Protocol is a internet protocol that is used when assigning a computer a new IP address. 
</p>
<br />
<br />

<p>
<img src="https://i.imgur.com/nkryvP5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Observe DNS Traffic
  
 - In Wireshark filter for DNS traffic and there will most likely already be traffic showing so to clear the traffic click the green Wireshark fin.
 - In Powershell use the command nslook www.google.com or any public wesbite.
    - What nslookup does is that it simply ask the computer what the IP address is of the website you are asking it. 
 - Once entered there should be traffic starting to come in
 - This is becuase DNS or Domain Name System is a internet protocol that converts readable wesbite domain name like google.com to computer readable IP addresses.
</p>
<br />
<br />

<p>
<img src="https://i.imgur.com/toQx0hK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Observe RDP Traffic
  
- In WireShark filter for only RDP/tcp.port==3389 traffic only.
- Once entered there should be a constant flow of traffic happening that is because your lcoal computer and the Window VM is using RDP(Remote Desktop Protocol). RDP is a internet protocol that is used when remotely accessing another another computer. 
    - Not to be confused with SSH as SSH only uses the command line and not a GUI. 
</p>
<br />
