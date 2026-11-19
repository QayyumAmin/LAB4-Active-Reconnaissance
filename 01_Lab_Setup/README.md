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


PART 2 - OWN HOST AND DISCOVERY HOST

2.1 INTRODUCTION

This section describes the identification of the attacker machine and the discovery of active hosts within the assigned laboratory network. Nmap was used to perform host discovery to identify devices that were active and responding within the network range.

The purpose of this activity was to identify the available hosts before proceeding with network service detection.


2.2 ATTACKER HOST IDENTIFICATION 

The attacker machine used in this activity was Kali Linux. The network configuration was examined using Linux networking commands to identify the machine's hostname, network interface and assigned IP address.

<img width="1920" height="983" alt="Screenshot_2026-11-19_21_59_25" src="https://github.com/user-attachments/assets/b1ed3f6f-ba10-40da-8786-d0d80777e942" />

| Configuration | Result |
|---|---|
| Operating System | Kali Linux |
| Network Interface | eth1 |
| Attacker IP Address | 192.168.56.102 |
| Network CIDR | 192.168.56.0/24 |
| Network Mode | Host-only Adapter |
| Role | Attacker |


2.3 NMAP HOST DISCOVERY

Command used

sudo nmap -sn 192.168.56.0/24

<img width="1920" height="983" alt="Screenshot_2026-11-19_22_00_32" src="https://github.com/user-attachments/assets/93055b74-b37a-4e9c-8c51-c7c88854b31b" />


2.4 DISCOVERY HOST

| No. | IP Address | Status | Identification |
|---|---|---|---|
| 1 | 192.168.56.1 | Up | Windows Victim / DVWA |
| 2 | 192.168.56.100 | Up | VirtualBox network device (role unconfirmed) |
| 3 | 192.168.56.102 | Up | Kali Linux Attacker |

Scan Summary :

| Item | Result |
|---|---|
| Scanning Tool | Nmap |
| Scan Type | Host Discovery |
| Target Network | 192.168.56.0/24 |
| Total IP Addresses | 256 |
| Active Hosts Discovered | 3 |
| Scan Duration | Approximately 1.9 seconds |
| Scan Status | Successful |


2.5 INTERPRETATION OF FINDING

The Nmap host discovery scan successfully identified three active hosts within the laboratory network.

The host at 192.168.56.1 was identified as the Windows victim machine hosting the Damn Vulnerable Web Application (DVWA). The host at 192.168.56.102 represents the Kali Linux attacker machine used to perform reconnaissance activities.
These findings demonstrate that Nmap can identify active devices within the configured network and provide information for further reconnaissance activities.

The host discovery activity was completed successfully using Nmap. Three active hosts were identified within the 192.168.56.0/24 network.

The discovery results provided an initial understanding of the laboratory network and confirmed the presence of the target Windows machine. The identified target IP address, 192.168.56.1, will be used in the next stage to identify available network services and open ports.

PART 3 - SERVICES AND INTERPRETATION

3.1 INTRODUCTION

This section focuses on identifying the network services and open TCP ports available on the target machine. Nmap service version detection was used to examine the services running on the Windows victim machine hosting the Damn Vulnerable Web Application (DVWA).


3.2 PERFORM NMAP SERVICE DETECTION

Step 1 - Scan HTTP and HTTPS ports
Step 2 - Save the scan result
Step 3 - View the save result

<img width="1920" height="983" alt="Screenshot_2026-11-19_22_01_11" src="https://github.com/user-attachments/assets/62600906-90de-4365-986c-936046b68fd7" />

<img width="1920" height="983" alt="Screenshot_2026-11-19_23_13_40" src="https://github.com/user-attachments/assets/98b74172-304a-424c-8ad5-2b87b5a9f8c6" />


3.3 FINDINGS TABLE

| Port | State | Service | Version |
|---|---|---|---|
| 80/tcp | Open | HTTP | Apache httpd 2.4.65 |
| 443/tcp | Open | SSL/HTTP | Apache httpd 2.4.65 |

**Additional Detected Information**

| Information | Result |
|---|---|
| Target IP | 192.168.56.1 |
| Operating Platform | Windows (Win64) |
| OpenSSL Version | 3.5.1 |
| PHP Version | 8.5.12 |

PART 4 : LIMITATIONS AND RISK

4.1 Limitations

There are several limitations during the active reconnaissance activity:

1. **Limited Network Scope:** The scanning activity was conducted only within the assigned Host-only network (192.168.56.0/24).

2. **Limited Port Scanning:** The service detection activity focused only on ports 80 and 443. Other open ports may not have been identified.

3. **Firewall Restrictions:** Firewall configurations may block or filter certain network scan requests, which can affect scan results.

4. **Service Version Accuracy:** Nmap service detection provides estimated software and version information. The results may require further verification.


4.2 Risks

Active reconnaissance involves sending packets and requests directly to the target machine. The following risks should be considered:

1. **System Performance:** Excessive scanning may consume network or system resources.

2. **Service Disruption:** Aggressive scanning may affect the availability or performance of running services.

3. **Security Monitoring Alerts:** Active scanning activities may trigger firewall alerts or intrusion detection systems.

4. **Unauthorized Access:** Scanning systems without permission may violate organisational policies or legal requirements.


4.3 Mitigation Measures

The following measures were applied to reduce potential risks:

- Conducted scanning within an isolated VirtualBox Host-only network.
- Used a personally configured Windows machine hosting DVWA as the target.
- Limited the scan to the required IP address and ports.
- Avoided exploitation, brute-force attacks, and destructive testing.
- Performed the activity for educational purposes only.

