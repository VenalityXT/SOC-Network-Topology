# Network Topology Overview

This document provides an in-depth explanation of the home lab network topology, including the physical and logical layout, device roles, and interconnectivity between VLANs and network services. The lab is designed to simulate a secure, segmented enterprise environment for cybersecurity learning and experimentation.

---

## 1. Physical Topology

The physical layout consists of:

- **Modem** → Connects to the public internet.
- **Firewall Router (pfSense)** → Provides routing, firewalling, VPN services, and VLAN segmentation.
- **Main Switch** → Distributes traffic to connected VLANs via trunk and access ports.
- **Devices** → Connected to VLANs through the switch (e.g., laptops, servers, IoT devices).

```
Internet → Modem → pfSense (WAN) → pfSense (LAN) → Main Switch → VLAN Devices
```
![Network Topology](https://github.com/user-attachments/assets/ef415833-3132-4b92-ad66-df87a1a7a5af)

---

## 2. Logical Topology

The network is logically segmented into multiple VLANs, each assigned a specific trust level and function:

| VLAN ID | Name         | Purpose                         | IP Range         | Notes                           |
|---------|--------------|----------------------------------|------------------|----------------------------------|
| 1       | Management    | Admin devices and services       | 192.168.1.0/24   | Restricted access, WPA2         |
| 2       | Trusted LAN   | Workstations and secure clients  | 192.168.2.0/24   | ACL-controlled, high trust      |
| 3       | Server Zone   | Internal servers and backups     | 192.168.3.0/24   | Inter-zone access enabled       |
| 4       | IoT Zone      | Smart home/embedded devices      | 192.168.4.0/24   | Internet access only            |
| 5       | HoneyNet      | Honeypot systems and traps       | 192.168.5.0/24   | Captive portal, high logging    |
| 10      | Client Zone   | Guest laptops, desktops          | 192.168.10.0/24  | Limited lateral access          |
| 30      | Lab Devices   | Test equipment and labs          | 192.168.30.0/24  | No outbound by default          |
| 40      | DMZ           | Public-facing services           | 192.168.40.0/24  | Isolated disk, external-facing  |

[Insert Image: logical-topology.png]

---

## 3. Inter-VLAN Routing and Security

- **pfSense** acts as the central point for inter-VLAN routing and enforces firewall rules.
- VLANs are isolated by default, with explicit rules allowing only necessary communication (e.g., Server Zone <→ Trusted LAN).
- Internet access is filtered per VLAN. IoT and Guest VLANs have strict egress-only policies.
- The DMZ is physically and logically isolated, with its own logging and security controls.

---

## 4. Key Design Principles

- **Segmentation**: Reduce lateral movement risk through strict VLAN separation.
- **Principle of Least Privilege**: Firewall rules enforce minimal access between zones.
- **Monitoring**: HoneyNet and DMZ zones are heavily logged to simulate real-world detection scenarios.
- **Scalability**: Modular VLAN design allows for future additions and reconfigurations.

---

## 5. Future Considerations

- Expand topology with additional WAPs for segregated wireless access.
- Integrate a SIEM (e.g., Splunk) into the Server Zone or DMZ for real-time monitoring.
- Implement redundant switch/firewall paths for high availability simulation.
- Add outbound firewall rules using alias lists and threat intelligence feeds.

