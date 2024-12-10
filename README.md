# Cisco Packet Tracer Network Project

This project demonstrates the setup of a small, multi-subnet network using **Cisco Packet Tracer**. The network is designed with **five different subnets** connected through routers and switches, providing services like DHCP, DNS, FTP, and HTTP, along with wireless connectivity.

---
![image](https://github.com/user-attachments/assets/d248d1c5-cb09-410b-bb1a-531f1f94e5cd)


## Network Topology Overview

### **Network 1 (Blue)**
- **Purpose**: DHCP configuration for dynamic IP allocation.
- **Devices**:
  - DHCP Server
  - Two PCs (PC0 and PC1)
  - 2960-24TT Switch
- **Network Details**:
  - Network Address: `192.168.2.0/26`
  - Default Gateway: `192.168.2.1`

### **Network 2 (Orange)**
- **Purpose**: FTP service for file transfers.
- **Devices**:
  - FTP Server
  - Two PCs (PC6 and PC7)
  - 2960-24TT Switch
- **Network Details**:
  - Network Address: `192.168.2.64/27`
  - Default Gateway: `192.168.2.65`

### **Network 3 (Red)**
- **Purpose**: DNS service for resolving domain names.
- **Devices**:
  - DNS Server
  - Two PCs (PC4 and PC5)
  - 2960-24TT Switch
- **Network Details**:
  - Network Address: `192.168.2.96/27`
  - Default Gateway: `192.168.2.97`

### **Network 4 (Yellow)**
- **Purpose**: HTTP service for web hosting.
- **Devices**:
  - HTTP Server
  - Two PCs (PC8 and PC9)
  - 2960-24TT Switch
- **Network Details**:
  - Network Address: `192.168.2.128/28`
  - Default Gateway: `192.168.2.129`

### **Network 5 (Purple)**
- **Purpose**: Wireless connectivity with wired devices.
- **Devices**:
  - Access Point
  - Two PCs (PC2 and PC3)
  - One Smartphone
  - 2960-24TT Switch
- **Network Details**:
  - Network Address: `192.168.2.144/28`
  - Default Gateway: `192.168.2.145`

---

## Configuration Steps

### **1. Router Setup**
- Configure **GigaNet interfaces** for each router for all connected networks:
  ```bash
  Router(config)#int gig0/0
  Router(config-if)#ip address 192.168.2.1 255.255.255.192
  Router(config-if)#no shutdown


## Set up static routing for networks not directly connected to the router:

Router(config)#ip route 192.168.2.64 255.255.255.224 192.168.2.65

## 2. DHCP Server Configuration

Assign a static IP address to the DHCP server (e.g., 192.168.2.2).
Configure DHCP pools for each subnet on the DHCP server.
On the router, configure the IP Helper address for the DHCP server:

Router(config)#int gig0/1
Router(config-if)#ip helper-address 192.168.2.2
Router(config-if)#do wr

## 3. Dynamic IP Allocation
Test DHCP functionality by dynamically assigning IPs to devices connected to the network.

## 4. DNS Configuration
Set up a DNS server in any subnet (e.g., Network 3).
Configure a domain name (e.g., test.html or index.html) and assign the IP of the HTTP server.
Ensure the HTTP server hosts the specified sites. If not, create the sites manually.

## 5. Wireless Configuration
Replace the wired NIC in wireless devices (e.g., PCs or smartphones) with a WMP300N component.
Add an AP-TP Access Point to the subnet, configure it with:
SSID
Security: WPA2-PSK
Passphrase (e.g., a password or key)
Connect wireless devices to the network:

PC > Desktop > PC Wireless > Connect to SSID > Enter passphrase

## 6. Router as DHCP
If you want the router to act as a DHCP server, configure it as follows:

Router>en
Router#conf t
Router(config)#ip dhcp excluded-address 192.168.2.144 192.168.2.145
Router(config)#ip dhcp pool netone
Router(dhcp-config)#default-router 192.168.2.145
Router(dhcp-config)#network 192.168.2.144 255.255.255.240
Router(dhcp-config)#dns-server 192.168.2.146
Final Testing
Verify interconnectivity between all subnets.
Access DNS and HTTP servers from any PC.
Test FTP functionality by transferring files to and from the FTP server.
Confirm wireless devices can connect and access network resources.


## Summary
This project demonstrates the implementation of a small-scale, functional network using Cisco Packet Tracer, incorporating static routing, DHCP, DNS, HTTP, FTP, and wireless connectivity. 
The setup highlights practical use cases for server-client communication across multiple subnets.
