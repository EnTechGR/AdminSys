Phase 1: Accessing the Launchpad (Laptop VM) Before scanning the target, you must establish a presence on the local network.

Establish **SSH** Connection: Connect from your physical machine to the laptop VM using the designated port forward.

Command: ssh user@localhost -p **10122**

Authentication: When prompted for the password, use the single space as instructed in the project brief.

Identify the Interface: Determine your local IP and the name of the network interface.

Command: ip a

Note: Look for enp0s8 (VirtualBox) or enp0s1 (**UTM**).

Phase 2: Network Reconnaissance (Link Layer) Now, find the hidden server on the local network using **ARP**. Since **ARP** operates at the Link Layer, it is the most reliable way to find hosts that might be *stealthy* to higher-layer pings.

Perform **ARP** Scan:

Bash sudo nmap -sn -PR **192**.**168**.x.0/24 (Replace with the subnet found in Phase 1).

Identify the Target: Look for an IP address in the results that is not your own laptop's IP. This is your target: 01_scan_RRF-**CONTROL**.

Phase 3: Port Discovery (Transport Layer) Once you have the target IP, you need to find where the door is open.

Full Port Scan: Because standard services might be moved to non-standard ports, scan all 65,**535** ports.

Bash nmap -p- -T4 <TARGET_IP> Analyze Results: Identify the open port (e.g., **4223**).

Service Verification: Confirm that the service running on that port is indeed **SSH**.

Bash nmap -p **4223** -sV <TARGET_IP> Phase 4: Exploitation (Application Layer) With the IP and Port in hand, you must now provide the credentials hidden within the *Subject* of the project.

Initiate Connection: Use **SSH** to connect to the target port.

Bash ssh root@<TARGET_IP> -p **4223** Provide Credentials: Enter the password discovered by carefully analyzing the images and clues provided in the project description (referencing The Matrix Reloaded).

### Success Criteria

You have completed the task once your terminal prompt transitions from the laptop user to the control server:

Plaintext root@**192**.**168**.x.x's password: **RRF**-**CONTROL**> █ Mission Accomplished. You have successfully navigated the Link, Network, and Transport layers to gain Application-level access to the grid.