# SOC-Network-Topology & Firewall Architecture

This repository documents the design and implementation of a segmented, security-focused home network using pfSense, VLANs, and managed switches. It demonstrates enterprise-level network architecture practices with detailed configuration and zone isolation to simulate secure real-world environments.

## Table of Contents
- [Project Overview](#project-overview)
- [Technologies Used](#technologies-used)
- [Objectives](#objectives)
- [Key Achievements](#key-achievements)
- [Skills Demonstrated](#skills-demonstrated)
- [Setup and Configuration Guide](#setup-and-configuration-guide)
- [Repository Structure](#repository-structure)
- [Recommendations for Future Enhancements](#recommendations-for-future-enhancements)
- [License](#license)


## Project Overview

This lab simulates a secure home network using pfSense to manage six isolated VLANs (Client, IoT, Server, DMZ, Admin, and HoneyNet), configured with strict firewall rules, service zoning, and access control. The project replicates core enterprise network principles for training, experimentation, and practical demonstration of security architecture.

[Network Topology](https://raw.githubusercontent.com/VenalityXT/SOC-Network-Topology/main/Network.drawio.svg)

## Technologies Used

- pfSense – Firewall, VLAN routing, OpenVPN, Captive Portal  
- Kea DHCP – IP address management and host reservations  
- Unmanaged/Managed Switch – VLAN tagging and traffic segmentation  
- Ubuntu – OS for connected services, log processing, and lab operations  
- OpenVPN – Secure remote access  
- Wireshark – Network traffic analysis  

## Objectives

- Design and document a secure, scalable home network topology  
- Segment the network using VLANs and enforce inter-zone firewall policies  
- Deploy core services including DHCP, DNS, VPN, and a captive portal  
- Simulate a DMZ and HoneyNet for threat modeling and response testing  
- Provide professional-grade documentation for review and reproducibility  

## Key Achievements

- **Implemented a fully segmented VLAN-based network**  
  *Created six VLANs aligned with security roles and enforced routing rules via pfSense to isolate traffic and restrict access.*

- **Built modular service zones for lab and simulation use**  
  *Configured isolated zones including a Captive Portal (HoneyNet), OpenVPN-enabled Admin VLAN, and dedicated IoT VLAN.*

- **Developed comprehensive documentation and diagrams**  
  *Included logical/physical diagrams, detailed service breakdowns, and configuration notes for each network component.*

- **Secured internal traffic and access flows**  
  *Applied firewall rules and DHCP static mappings to prevent unauthorized lateral movement or service misuse.*

- **Established groundwork for logging and security automation**  
  *Designed the layout for centralized monitoring, allowing future Splunk or syslog integration.*

[Insert Logical Topology Diagram or Firewall Rule Chart Here]

## Skills Demonstrated

- **Secure Network Design**  
  Built a robust, layered topology emphasizing defense-in-depth and role-based segmentation.

- **Firewall Configuration and Policy Enforcement**  
  Created strict allowlist-based rules between VLANs, simulating zero-trust principles.

- **Service Deployment and Zoning**  
  Deployed and documented OpenVPN, Captive Portal, DNS, and DHCP in isolated zones.

- **Access Control and Remote Access**  
  Enabled remote access via VPN while maintaining strict zone boundaries internally.

- **Professional Documentation and Diagramming**  
  Maintained readable configuration guides, service maps, and architectural diagrams.

## Setup and Configuration Guide

1. **Network Topology Design**
   - Designed physical and logical layouts with six VLANs
   - Mapped VLANs to physical switch ports and pfSense interfaces

2. **pfSense Configuration**
   - Created VLAN interfaces for each zone
   - Configured DHCP (via Kea) for each subnet with static host mapping
   - Defined firewall rules to control inter-zone traffic and outbound access

3. **Service Deployment**
   - OpenVPN configured for secure Admin access
   - Captive Portal assigned to HoneyNet for unauthorized device sinkhole
   - DNS and DHCP integrated across zones

4. **Device Assignment**
   - Defined static IPs for laptops, servers, and IoT devices
   - Used MAC-based reservations for critical hosts

5. **Testing and Validation**
   - Verified isolation between VLANs (e.g., IoT can’t reach Admin)
   - Tested remote VPN access and captive portal behavior

## Repository Structure
```
## Repository Structure

SOC-Network-Topology/

├── diagrams/
│   ├── physical-topology.png
│   ├── logical-topology.png
│   └── vlan-overview.png

├── docs/
│   ├── topology-overview.md
│   ├── vlan-breakdown.md
│   ├── firewall-rules.md
│   ├── services-config.md
│   ├── remote-access.md
│   └── recommendations.md

├── configs/
│   ├── pfSense/
│   │   ├── interfaces.conf.txt
│   │   ├── vlans.conf.txt
│   │   ├── dhcp-kea.conf.txt
│   │   ├── openvpn.conf.txt
│   │   └── firewall-rules.conf.txt
│   ├── switch/
│   │   └── vlan-ports-config.txt
│   └── dns-dhcp/
│       └── host-reservations.yaml

├── scripts/
│   └── pfSense-backup.sh

├── README.md  
├── LICENSE

```
## Recommendations for Future Enhancements

- Deploy a centralized syslog or SIEM solution (e.g., Splunk or Graylog)
- Integrate Snort or Suricata for IDS/IPS functionality
- Automate configuration backups and version control using Git
- Introduce IPv6 support and dual-stack compatibility
- Expand HoneyNet with honeypots and alerting mechanisms
- Implement high availability (HA) using pfSense CARP or VRRP

## License

This project is licensed under the MIT License – see the LICENSE file for details.
