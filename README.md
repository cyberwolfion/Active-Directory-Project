# Active-Directory-Project
The goal of this project is to set up an Active Directory environment, ingest and monitor logs with Splunk, and generate attack telemetry using Kali Linux and Atomic Red Team. 


# Step 1: Splunk Server Setup (Ubuntu)

### Prerequisites:
- Downloaded ISO files for Ubuntu, Windows 10, and Windows Server.
- Network setup with a NAT Network at 192.168.15.0/24.
- Ubuntu Server IP: 192.168.15.10.

### Steps:

1. Install Ubuntu and set static IP:

   Update the system:
```
sudo apt-get update && sudo apt-get upgrade -y
```
  
