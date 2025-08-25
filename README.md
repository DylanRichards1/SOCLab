# SOCLab
This project documents a personal SOC (Security Operations Center) lab project using VirtualBox. The lab demonstrates endpoint log forwarding, SIEM ingestion, and detection of network scanning activity.

## Overview

### Components
- Kali Linux VM - Used as the attacker machine to perform reconnaissance (Nmap).
- Windows 10 VM (Victim) - Configured with the Wazuh agent to forward logs to Wazuh Manager.
- Wazuh Manager - Collects and analyzes logs from endpoints.

### Lab Flow
- Configure VirtualBox with Kali Linux and two Windows 10 VMs.
- Install and configure the Wazuh agent on the Windows 10 Victim VM.
- Forward logs from Windows to Wazuh Manager.
- Run Nmap scans from Kali Linux targeting the Windows 10 Victim.
- Observe forwarded logs and create detections in Wazuh.

### Setup Instructions
1. VirtualBox Networking
- Adapter 1 (NAT) - Internet access.
- Adapter 2 (Host-Only) - Internal lab network (isolated).

- Example IP scheme:
  - Wazuh Manager - 192.168.56.10
  - Windows 10 Victim - 192.168.56.20
  - Kali Linux - 192.168.56.30

2. Windows 10 Victim
- Install Windows 10 VM.
- Configure Host-Only IP (static: 192.168.56.20).
- Install Wazuh Agent:
  - Set Manager IP = 192.168.56.10.
  - Verify agent shows active on Wazuh Manager.

3. Kali Linux Attacker
- Install Kali Linux VM.
- Configure Host-Only IP (static: 192.168.56.30).

4. Nmap Scanning (Attack Simulation)
- Run from Kali against the Windows 10 Victim: sudo nmap 192.168.56.20

### Detection in Wazuh
- Monitor Windows Security Events 5156 / 5158 (connections allowed/blocked).
