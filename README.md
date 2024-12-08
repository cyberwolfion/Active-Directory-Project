# Active-Directory-Project
This project aims to set up a realistic Active Directory (AD) environment with logging and monitoring capabilities using Splunk. It also demonstrates attack simulation using Kali Linux and Atomic Red Team to generate detectable telemetry in Splunk, simulating real-world attacks on the AD environment.

## Environment Setup
Network Setup:
- Domain Name: HomeLab
- Network (NAT): 192.168.15.0/24

Virtual Machines and Roles:
- Splunk Server (Ubuntu 22.04): ``` 192.168.15.10 ```
- Active Directory (Windows Server): ``` 192.168.15.5 ```
- Windows 10 Client (Target-PC): DHCP IP (domain-joined)
- Kali Linux (Attacker): ```192.168.15.250```

## Step 1: Setting Up the Splunk Server (Ubuntu)
Objective: Install and configure Splunk on Ubuntu to act as the primary log aggregator and SIEM for the environment.

### Detailed Steps:
1. Install Ubuntu 22.04 on VirtualBox:
- Set the network adapter to NAT Network.
- Assign a static IP of ``` 192.168.15.10 ``` to ensure it remains accessible.

2. Set Static IP:
- Edit the Netplan configuration to set the static IP:
``` sudo nano /etc/netplan/00-installer-config.yaml ```

- Add the following configuration:
```
network:
  ethernets:
    enp0s3:
      dhcp4: no
      addresses: [192.168.15.10/24]
      nameservers:
          addresses: [8.8.8.8]
      routes:
          - to: default
            via: 192.168.15.1      
version: 2
```

- Apply changes:

```
sudo netplan apply
```

3. Download and Install Splunk:
- Download Splunk Enterprise for Linux from Splunk’s website.
- Transfer the .deb file to the server, then install it:
```
sudo dpkg -i splunk-installer.deb
```

4. Configure Splunk:
- Start Splunk and set admin credentials:
```
cd /opt/splunk/bin
sudo ./splunk start --accept-license
```

- Enable Splunk to start on boot:
```
sudo ./splunk enable boot-start
```

## Step 2: Install Splunk Universal Forwarder & Sysmon (Windows 10 & Windows Server)

### Objective: 
Set up the Splunk Universal Forwarder and Sysmon on Windows systems to forward security-related logs to the Splunk server for centralized monitoring and analysis.

### Prerequisites:
- Windows 10 (target-PC) IP: DHCP.
- Windows Server IP: 192.168.15.5.

### Steps (for both Windows 10 & Windows Server):
1. Install Splunk Universal Forwarder:
- Download and install Splunk Universal Forwarder.
- Configure inputs.conf to send system, security, application, and Sysmon logs to Splunk:



























