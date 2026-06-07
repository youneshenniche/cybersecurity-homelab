## Screenshots

### Switch System Information
![Switch System Info](screenshots/Screenshot_2026-06-06_194344.png)
*TP-Link TL-SG108E management interface showing device info, MAC address, 
IP address and firmware version*

### Port Mirroring — Before Configuration
![Port Mirror Disabled](screenshots/Screenshot_2026-06-06_195655.png)
*Port mirroring disabled by default — no traffic copying occurring*

### Port Mirroring — Configured and Enabled
![Port Mirror Enabled](screenshots/Screenshot_2026-06-06_195812.png)
*Port mirroring enabled — Port 3 set as destination, Ports 1 and 2 
mirrored with Ingress and Egress enabled. ZBook now sees all network traffic.*

### Wireshark Live Capture
![Wireshark Capture](screenshots/Screenshot_2026-06-06_195948.png)
*Wireshark capturing live packets via port mirroring — MDNS, UDP, 
and ICMPv6 traffic visible in real time*

### DNS Queries — Domain Name Resolution
![DNS Packets](screenshots/Screenshot_2026-06-06_200600.png)
*DNS standard queries captured in real time — login.microsoftonline.com, 
manage.microsoft.com and other domains visible*

### SMB Traffic — Windows Network Browsing
![SMB Packets](screenshots/Screenshot_2026-06-06_201633.png)
*SMB packets captured from Windows Server VM — Host Announcements 
visible showing YOUNES workstation and domain controller*

### ARP Traffic — IP to MAC Resolution
![ARP Packets](screenshots/Screenshot_2026-06-06_201806.png)
*ARP packets showing "Who has 10.0.0.80? Tell 10.0.0.1" — no 
authentication in ARP makes this the foundation of man-in-the-middle attacks*

### HTTP Traffic — Unencrypted
![HTTP Packets](screenshots/Screenshot_2026-06-06_202002.png)
*HTTP traffic captured in plain text — GET requests, browser user 
agent, and full headers readable by anyone on the network*

### TLS Traffic — Encrypted
![TLS Packets](screenshots/Screenshot_2026-06-06_202346.png)
*TLS 1.3 encrypted traffic — payload completely unreadable compared 
to HTTP. Cipher suites confirm encryption is active.*
