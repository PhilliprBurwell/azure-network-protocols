<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups by configuring a Firewall. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

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

- Step 1
- Step 2
- Step 3
- Step 4

<h2> Part 1 Inspecting Traffic Between Azure Virtual Machines</h2>

<p>
(Image #1) 
  
![image](https://github.com/user-attachments/assets/e3ae8b61-29a9-4ef7-9df3-f26acf4661cf)

(Image #2)
![image](https://github.com/user-attachments/assets/8363fe5d-c006-4d78-8543-3718094d6d5c)


</p>
<p>
#1 Create Resourse Group & Virtual Network
Create a Resource Group While creating the VM, select the previously created Resource Group
While creating the VM, allow it to create a new Virtual Network (Vnet) and Subnet

</p>
<br />

<p>
(Image #1) 
  
![image](https://github.com/user-attachments/assets/d3260ebb-ac08-470f-b390-3cdb34334da3)
(Image #2) 

![image](https://github.com/user-attachments/assets/33a93015-29ad-4c5d-8dbe-127a5b1029b9)


</p>
<p>
#2 Create 2 VM's Create a Windows 10 Virtual Machine (VM) Create a Linux (Ubuntu) VM
While creating the VM, select the previously created Resource Group and Virtual Network—the Virtual Network MUST BE THE SAME.
Authentication type: Username/Password
Ensure both VMs are in the same Virtual Network / Subnet

</p>
<br />

<p>
(Image #1) 
  
![image](https://github.com/user-attachments/assets/4c816892-1ade-43e5-ad18-d935d9df5369)
(Image #2) 

![image](https://github.com/user-attachments/assets/37d8aa9a-ff16-4123-a524-0b4b64048bb6)

</p>
<p>
#3 Examine traffic to and from Azure Virtual Machines with Wireshark If using Mac, install Microsoft Remote Desktop Use Remote Desktop to connect to your Windows 10 Virtual Machine Within your Windows 10 Virtual Machine, Install WiresharkOpen Wireshark and start packet capture Within Wireshark, filter for ICMP traffic only Retrieve the private IP address of the Ubuntu VM (linux-vm) and attempt to ping it from within the Windows 10 VM Observe ping requests and replies within WireShark From The Windows 10 VM, open command line or PowerShell and attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark
</p>
<br />

<h2> Part 2 Configuring a Firewall [Network Security Group]</h2>

<p>

(Image #1) 
  ![image](https://github.com/user-attachments/assets/a887ab50-e0be-4957-a0fd-a30e6679b906)
(Image #2) 
![image](https://github.com/user-attachments/assets/0ffadf59-4dc3-497c-a815-78b3a5d6417a)


</p>
<p>
#1 Disable imcoming IMCP Traffic Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM
Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic. Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity. Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is. Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working). Stop the ping activity

<br />

<p>
   <h2> Examination of All Traffic to and from Azure Virtual Machines</h2> 


![image](https://github.com/user-attachments/assets/2f2bc158-bb98-42fb-8126-d9326c6891bb)
 
#2 Observing IMCP Traffic

ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.

![image](https://github.com/user-attachments/assets/aa0c0475-079a-431d-9fa9-59403c766e76)

#3 Observing SSH Traffic
Log back into the windows-vm
Back in Wireshark, start a packet capture up
Filter for SSH traffic only
From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address)
Open PowerShell, and type: ssh labuser@<private IP address>
Type commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark
Exit the SSH connection by typing ‘exit’ and pressing [Enter]

![image](https://github.com/user-attachments/assets/d9a242d4-a3c5-4e28-ba44-e5a4d20bf0b3)


#4 Observing DHCP Traffic
Back in Wireshark, filter for DHCP traffic only
From your Windows 10 VM, attempt to issue your VM a new IP address from the command line
Open PowerShell as admin and run: ipconfig /renew
Observe the DHCP traffic appearing in WireShark

![image](https://github.com/user-attachments/assets/c4c292cd-bb12-4ded-b270-33264f28f94f)


#5 Observing DNS Traffic
Back in Wireshark, filter for DNS traffic only
From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are
Observe the DNS traffic being show in WireShark


![image](https://github.com/user-attachments/assets/1b4d767e-5f83-472b-addc-80a1132baad5)


#6 Observing RDP Traffic
Back in Wireshark, filter for RDP traffic only (tcp.port == 3389)
Observe the immediate non-stop spam of traffic? Why do you think it’s non-stop spamming vs only showing traffic when you do an activity?
Answer: because the RDP (protocol) is constantly showing you a live stream from one computer to another, therefor traffic is always being transmitted


