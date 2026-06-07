## Screenshots

### Switch System Information
![Switch System Info](screenshots/Screenshot%202026-06-06%20194344.png)
*TP-Link TL-SG108E management interface showing device info, MAC address, IP address and firmware version*

### Port Mirroring — Before Configuration
![Port Mirror Disabled](screenshots/Screenshot%202026-06-06%20195655.png)
*Port mirroring disabled by default — no traffic copying occurring*

### Port Mirroring — Configured and Enabled
![Port Mirror Enabled](screenshots/Screenshot%202026-06-06%20195812.png)
*Port mirroring enabled — Port 3 set as destination, Ports 1 and 2 mirrored with Ingress and Egress enabled*

### Wireshark Live Capture
![Wireshark Capture](screenshots/Screenshot%202026-06-06%20195948.png)
*Wireshark capturing live packets via port mirroring*

### DNS Queries
![DNS Packets](screenshots/Screenshot%202026-06-06%20200600.png)
*DNS standard queries captured in real time showing website lookups*

### SMB Traffic
![SMB Packets](screenshots/Screenshot%202026-06-06%20201633.png)
*SMB packets captured from Windows Server VM*

### ARP Traffic
![ARP Packets](screenshots/Screenshot%202026-06-06%20201806.png)
*ARP packets showing IP to MAC resolution — foundation of man-in-the-middle attacks*

### HTTP Traffic — Unencrypted
![HTTP Packets](screenshots/Screenshot%202026-06-06%20202002.png)
*HTTP traffic captured in plain text — headers and data fully readable*

### TLS Traffic — Encrypted
![TLS Packets](screenshots/Screenshot%202026-06-06%20202346.png)
*TLS 1.3 encrypted traffic — payload completely unreadable*
*ARP packets showing "Who has 10.0.0.80? Tell 10.0.0.1" — no 
authentication in ARP makes this the foundation of man-in-the-middle attacks*

### HTTP Traffic — Unencrypted
(screenshots/Screenshot_2026-06-06_202002.png)
*HTTP traffic captured in plain text — GET requests, browser user 
agent, and full headers readable by anyone on the network*

### TLS Traffic — Encrypted
![TLS Packets](screenshots/Screenshot_2026-06-06_202346.png)
*TLS 1.3 encrypted traffic — payload completely unreadable compared 
to HTTP. Cipher suites confirm encryption is active.*
