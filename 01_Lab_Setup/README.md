Part 1 LAB SETUP

1.1 INTRODUCTION

The laboratory environment was prepared to perform active reconnaissance against an intentionally vulnerable web application. 
The setup consists of two separate environments: Windows, which acts as the victim machine hosting Damn Vulnerable Web Application (DVWA), and Kali Linux, which acts as the attacker machine.

Oracle VirtualBox was used to run Kali Linux, while XAMPP was used to host the DVWA web application on Windows. 
Both machines were connected through a VirtualBox Host-only network to allow communication within an isolated laboratory environment.

1.2 LABORATORY ENVINRONMENT

| Component | Description |
|---|---|
| Attacker Machine | Kali Linux |
| Victim Machine | Windows |
| Virtualization Software | Oracle VirtualBox |
| Web Server | Apache (XAMPP) |
| Database Server | MySQL (XAMPP) |
| Vulnerable Application | DVWA |
| Reconnaissance Tool | Nmap |
| Network Mode | Host-only Adapter |

1.3 VICTIM MACHINE SETUP ( WINDOWS )

The victim environment was prepared using XAMPP to host the Damn Vulnerable Web Application (DVWA).

The following steps were performed:

1. Opened the XAMPP Control Panel on Windows and started the Apache service to enable the web server.

   <img width="663" height="426" alt="Screenshot 2026-11-19 212935" src="https://github.com/user-attachments/assets/4cad4099-d9b2-40b9-b4f6-2b5f5d3bc2d6" />

2. Opened a web browser and accessed the DVWA application through http://localhost/DVWA/ and logged in to the DVWA application using the default administrator credentials.

   <img width="1516" height="821" alt="Screenshot 2026-11-19 221915" src="https://github.com/user-attachments/assets/66245687-b597-4afe-b1e1-38e941539207" />

The DVWA application was successfully launched and used as the target for the active reconnaissance activity.

Victim Machine Network Configuration:

| Configuration | Value |
|---|---|
| Operating System | Windows |
| IPv4 Address | 192.168.56.1 |
| Subnet Mask | 255.255.255.0 |
| Application | DVWA |
| Web Server | Apache |
| Database Server | MySQL |

1.4 MACHINE SETUP KALI LINUX

Kali Linux was configured as the attacker machine using Oracle VirtualBox.

The following steps were performed:

1. Opened Oracle VirtualBox and selected the Kali Linux virtual machine.

2. Accessed the virtual machine network settings.

3. Configured a Host-only Adapter to establish communication between Kali Linux and the Windows victim machine.

4. Enabled the virtual network adapter and connected it to the VirtualBox Host-only Ethernet Adapter.

5. Started the Kali Linux virtual machine.

6. Opened the terminal and executed the ip -br addr command to identify the network interfaces and assigned IP addresses.

7. Executed the ip route command to examine the routing configuration.

<img width="1920" height="983" alt="Screenshot_2026-11-19_21_57_44" src="https://github.com/user-attachments/assets/c3528cf7-e209-4115-b6ec-04534f958ac2" />

| Configuration | Value |
|---|---|
| Operating System | Kali Linux |
| Network Interface | eth1 |
| IPv4 Address | 192.168.56.102 |
| Network CIDR | 192.168.56.0/24 |
| Network Mode | Host-only Adapter |
| Reconnaissance Tool | Nmap |

1.5 NETWORK CONNECTIVITY VERIFICATION

After configuring both environments, network connectivity was tested to ensure that the attacker machine could communicate with the victim machine.
The following command was executed in Kali Linux:

ping -c 4 192.168.56.1

The ping test was successful, indicating that the Windows victim machine was reachable from Kali Linux through the Host-only network.

The DVWA application was also accessed from the Kali Linux Firefox browser using the following address:
http://192.168.56.1/DVWA/

<img width="1920" height="983" alt="Screenshot_2026-11-19_21_56_26" src="https://github.com/user-attachments/assets/17196d6c-765d-4de7-bd0b-9f1452c70c11" />

The DVWA dashboard was successfully displayed, confirming that the web application was accessible from the attacker environment.

1.6 ASSIGNED NETWORK CONFIGURATION

| Device | IP Address | Role |
|---|---|---|
| Windows | 192.168.56.1 | Victim / DVWA |
| Kali Linux | 192.168.56.102 | Attacker |
| Laboratory Network | 192.168.56.0/24 | Host-only Network |

<img width="1920" height="983" alt="Screenshot_2026-11-19_21_57_44" src="https://github.com/user-attachments/assets/17065c1a-a640-4121-ade1-689824604f97" />

<img width="510" height="128" alt="Screenshot 2026-11-19 215311" src="https://github.com/user-attachments/assets/d414f288-1aa0-46a1-a715-68300d94af65" />

The /24 CIDR notation represents a subnet mask of 255.255.255.0, providing 256 total IPv4 addresses in the subnet.

| Test | Command / Method | Result |
|---|---|---|
| Windows IP Check | ipconfig | Successful |
| Kali IP Check | ip -br addr | Successful |
| Routing Check | ip route | Successful |
| Connectivity Test | ping -c 4 192.168.56.1 | Successful |
| DVWA Access | http://192.168.56.1/DVWA/ | Successful |


