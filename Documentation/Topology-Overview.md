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

The network is logically segmented into multiple VLANs, each serving a specific purpose to enhance security and operational efficiency. Each VLAN is configured with specific access control policies to simulate real-world segmentation.

| VLAN ID | Name             | Purpose                              | IP Range         | Notes                                                         |
|---------|------------------|---------------------------------------|------------------|---------------------------------------------------------------|
| 1       | Internal Network | Admin devices and core infrastructure | 192.168.1.0/24   | Restricted access, ACLs/WPA3                                  |
| 2       | IoT Network      | Smart home and embedded devices       | 192.168.2.0/24   | Internet only, ACLs/WPA2                                      |
| 3       | Guest Network    | Temporary user devices                | 192.168.3.0/24   | Segmented, rate-limited                                       |
| 4       | SOC Network      | Security monitoring and response tools| 192.168.4.0/24   | Connected to logging and SIEM stack                           |
| 5       | HoneyNet         | Deceptive honeypot systems            | 192.168.5.0/24   | Captive portal, aggressive logging                            |
| 6       | SAN              | Storage and backup infrastructure     | 192.168.6.0/24   | Limited lateral access, no internet                           |

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

