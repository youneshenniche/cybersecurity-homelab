## Screenshots

### Switch System Information
![Switch System Info](https://raw.githubusercontent.com/youneshenniche/cybersecurity-homelab/main/Phase-2%20Networking-Wireshark/screenshots/Screenshot%202026-06-06%20194344.png)
*TP-Link TL-SG108E management interface showing device info, MAC address, IP address and firmware version*

### Port Mirroring — Before Configuration
![Port Mirror Disabled](https://raw.githubusercontent.com/youneshenniche/cybersecurity-homelab/main/Phase-2%20Networking-Wireshark/screenshots/Screenshot%202026-06-06%20195655.png)
*Port mirroring disabled by default — no traffic copying occurring*

### Port Mirroring — Configured and Enabled
![Port Mirror Enabled](https://raw.githubusercontent.com/youneshenniche/cybersecurity-homelab/main/Phase-2%20Networking-Wireshark/screenshots/Screenshot%202026-06-06%20195812.png)
*Port mirroring enabled — Port 3 set as destination, Ports 1 and 2 mirrored with Ingress and Egress enabled*

### Wireshark Live Capture
![Wireshark Capture](https://raw.githubusercontent.com/youneshenniche/cybersecurity-homelab/main/Phase-2%20Networking-Wireshark/screenshots/Screenshot%202026-06-06%20195948.png)
*Wireshark capturing live packets via port mirroring*

### DNS Queries
![DNS Packets](https://raw.githubusercontent.com/youneshenniche/cybersecurity-homelab/main/Phase-2%20Networking-Wireshark/screenshots/Screenshot%202026-06-06%20200600.png)
*DNS standard queries captured in real time showing website lookups*

### SMB Traffic
![SMB Packets](https://raw.githubusercontent.com/youneshenniche/cybersecurity-homelab/main/Phase-2%20Networking-Wireshark/screenshots/Screenshot%202026-06-06%20201633.png)
*SMB packets captured from Windows Server VM*

### ARP Traffic
![ARP Packets](https://raw.githubusercontent.com/youneshenniche/cybersecurity-homelab/main/Phase-2%20Networking-Wireshark/screenshots/Screenshot%202026-06-06%20201806.png)
*ARP packets showing IP to MAC resolution — foundation of man-in-the-middle attacks*

### HTTP Traffic — Unencrypted
![HTTP Packets](https://raw.githubusercontent.com/youneshenniche/cybersecurity-homelab/main/Phase-2%20Networking-Wireshark/screenshots/Screenshot%202026-06-06%20202002.png)
*HTTP traffic captured in plain text — headers and data fully readable*

### TLS Traffic — Encrypted
