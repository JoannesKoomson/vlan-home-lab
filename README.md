# VLAN Home Lab

## Overview

This project demonstrates the design, configuration, and troubleshooting of a small VLAN-based network using Cisco Packet Tracer.

The lab was built to strengthen understanding of:
- VLAN segmentation
- DHCP configuration
- Router and switch configuration
- IP addressing and subnetting
- OSI troubleshooting
- Inter-device communication
- Cisco CLI navigation

The network was intentionally broken and troubleshot to better understand how VLANs affect communication between devices.

---

# Network Topology

## Devices Used

- Cisco 2911 Router
- Cisco 2960 Switch
- Laptop
- PC

## Connections

- Laptop → Switch Fa0/1
- PC → Switch Fa0/2
- Router g0/0 → Switch Fa0/24

---

# Objectives

- Configure router interfaces
- Configure DHCP
- Assign IP addresses dynamically
- Verify connectivity with ping
- Create VLANs
- Assign switch ports to VLANs
- Understand why communication fails between VLANs
- Troubleshoot Layer 1, Layer 2, and Layer 3 issues

---

# Initial Flat Network Configuration

Initially, all devices were placed in the default VLAN (VLAN 1).

This allowed:
- Successful DHCP assignment
- Successful device communication
- End-to-end ping testing

---

# Router Configuration

## Router Interface Configuration

```bash
enable
configure terminal

interface g0/0
ip address 192.168.10.1 255.255.255.0
no shutdown
exit
```

## DHCP Configuration

```bash
ip dhcp excluded-address 192.168.10.1

ip dhcp pool HOME
network 192.168.10.0 255.255.255.0
default-router 192.168.10.1
dns-server 8.8.8.8
exit
```

---

# Switch VLAN Configuration

## Create VLANs

```bash
enable
configure terminal

vlan 10
name LAPTOPS

vlan 20
name PCS
```

## Assign Ports to VLANs

```bash
interface fa0/1
switchport mode access
switchport access vlan 10

interface fa0/2
switchport mode access
switchport access vlan 20
```

---

# Results

## Before VLANs

- Laptop and PC communicated successfully
- Ping tests were successful
- Devices received DHCP addresses correctly

## After VLANs

- Laptop and PC could no longer communicate
- Ping requests timed out
- VLAN segmentation successfully separated network traffic

This demonstrated that:
> Devices in different VLANs cannot communicate without routing.

---

# Troubleshooting Process

## Problems Experienced

| Problem | Cause | Resolution |
|---|---|---|
| Red router link | Interface shutdown | Used `no shutdown` |
| 169.254.x.x address | DHCP failure | Verified DHCP configuration |
| Invalid input detected | Wrong CLI mode | Used `enable` and `configure terminal` |
| Ping failure after VLANs | VLAN separation | Expected VLAN behavior |
| Command typos | Syntax mistakes | Corrected CLI commands |

---

# OSI Model Mapping

## Layer 1 – Physical
- Ethernet cables
- Interface status
- Link lights

## Layer 2 – Data Link
- Switch configuration
- MAC addressing
- VLAN separation

## Layer 3 – Network
- Router configuration
- IP addressing
- DHCP
- Default gateway

---

# Key Lessons Learned

- VLANs logically separate devices on the same switch
- Switches separate VLAN traffic
- Routers connect networks
- DHCP failures often result in APIPA addresses (169.254.x.x)
- Cisco routers require `no shutdown` to activate interfaces
- Troubleshooting should follow the OSI model

---

# Important Networking Concepts

- VLAN Segmentation
- DHCP
- APIPA
- Default Gateway
- OSI Model
- ICMP Ping Testing
- Router & Switch Configuration
- Access Ports
- IP Addressing & Subnetting

---

# Rule of Thumb

> “Switches separate VLANs. Routers connect VLANs.”

---

# Future Improvements

- Inter-VLAN Routing
- Trunk Ports
- Wireless VLAN Segmentation
- ACL Security Rules
- Multiple DHCP Pools
- Network Monitoring Integration

---

# Files Included

- Packet Tracer topology (.pkt)
- Configuration screenshots
- VLAN tables
- Troubleshooting documentation
- Study recap notes

---

# Author

Joannes Koomson

Computer Networking | Infrastructure | Python Automation | Cloud Networking
