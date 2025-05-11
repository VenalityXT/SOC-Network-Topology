# VLAN Breakdown

This document provides a detailed breakdown of each VLAN in the network topology, including their specific configuration, access control policies, and use cases. Each VLAN serves a unique purpose and is essential for maintaining the security, functionality, and isolation of network traffic in the lab environment.

---

## 1. **VLAN 1: Internal Network**

- **Purpose**: Admin devices and core infrastructure
- **IP Range**: 192.168.1.0/24
- **Security**: Restricted access with ACLs and WPA3
- **Devices**: Admin workstations, network management systems, and critical infrastructure
- **Access Control**: 
  - Only trusted administrative devices are allowed.
  - Only management protocols (e.g., SSH, RDP) are permitted.
  - Access to other VLANs is strictly controlled and limited to authorized IPs.
- **Notes**: This VLAN is highly secured and isolated from other user-facing VLANs to protect sensitive systems.

---

## 2. **VLAN 2: IoT Network**

- **Purpose**: Smart home and embedded devices
- **IP Range**: 192.168.2.0/24
- **Security**: Internet access only, with ACLs and WPA2
- **Devices**: Smart TVs, IoT sensors, smart thermostats, cameras, and other embedded devices
- **Access Control**:
  - Strict ingress and egress filtering to limit traffic to the internet.
  - No inter-VLAN communication allowed to prevent lateral movement from IoT devices.
  - Limited access to only the necessary services required for IoT devices to function.
- **Notes**: This VLAN is designed to minimize risk from vulnerable IoT devices and prevent them from affecting other network segments.

---

## 3. **VLAN 3: Guest Network**

- **Purpose**: Temporary user devices
- **IP Range**: 192.168.3.0/24
- **Security**: Segmented and rate-limited access
- **Devices**: Laptops, mobile phones, and other guest devices
- **Access Control**:
  - Guest devices are limited to external internet access and cannot communicate with internal network resources.
  - Rate-limiting is implemented to manage bandwidth usage.
  - Captive portal is used for authentication and network access control.
- **Notes**: This VLAN ensures that guest devices do not impact the performance or security of the internal network.

---

## 4. **VLAN 4: SOC Network**

- **Purpose**: Security monitoring and response tools
- **IP Range**: 192.168.4.0/24
- **Security**: Connected to logging systems, SIEM stack, and other monitoring tools
- **Devices**: Security operations center (SOC) devices, monitoring systems, log aggregation tools (e.g., Splunk), IDS/IPS systems
- **Access Control**:
  - This VLAN has access to security-related data across other VLANs.
  - Devices in this VLAN are restricted from accessing user or admin networks to prevent manipulation of logs and data.
  - Direct access to SIEM and other security tools is allowed.
- **Notes**: The SOC Network is critical for real-time security monitoring and incident response. It is connected to all other relevant networks to ensure visibility across the environment.

---

## 5. **VLAN 5: HoneyNet**

- **Purpose**: Deceptive honeypot systems
- **IP Range**: 192.168.5.0/24
- **Security**: High logging, captive portal for entrapment
- **Devices**: Honeypot systems designed to simulate vulnerable services and trap malicious actors
- **Access Control**:
  - The HoneyNet is isolated from other networks to prevent attackers from using it as a springboard to attack other segments.
  - All traffic to and from the HoneyNet is logged and monitored for suspicious activity.
  - This VLAN is designed to entice attackers and gather intelligence.
- **Notes**: The HoneyNet serves as a decoy and can be used for threat intelligence collection and forensics.

---

## 6. **VLAN 6: SAN (Storage Area Network)**

- **Purpose**: Storage and backup infrastructure
- **IP Range**: 192.168.6.0/24
- **Security**: Limited lateral access, no internet
- **Devices**: Storage servers, backup systems, and other critical data storage devices
- **Access Control**:
  - Only authorized devices within trusted networks can access the storage and backup systems.
  - Lateral movement from other VLANs to the SAN is restricted.
  - Internet access is disallowed to prevent potential attacks from reaching sensitive data storage.
- **Notes**: The SAN is used for securely storing data, backups, and critical assets. It is isolated to ensure its integrity and confidentiality.

---

## Future Considerations

- **Additional Segmentation**: Future VLANs may be added for specific lab use cases such as database servers, web application testing environments, or research purposes.
- **VLAN Expansion**: Larger VLANs with broader use cases may be incorporated, such as dedicated networks for development, staging, and production environments.
- **Advanced Security Features**: Future iterations may include advanced security measures such as dynamic VLAN assignment, tighter ACLs, and threat intelligence integration.

