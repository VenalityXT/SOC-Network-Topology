# Firewall Rules

This document outlines the firewall configurations in the network, ensuring proper security policies are applied between VLANs and the associated devices. It covers the router firewall, inter-VLAN firewalls, and segmentation for specific VLANs.

---

## 1. **Router Firewall Rules**

The router firewall serves as the primary security control between the LAN and WAN, ensuring that only legitimate traffic enters or leaves the network. It applies filtering rules based on the network topology and security policies.

### General Rules:
- **Allow outbound traffic** for devices in VLANs 1, 2, 3, and 6 (Admin, IoT, Guest, SAN).
- **Deny inbound traffic** from the WAN unless it is explicitly permitted (e.g., VPN or specific service).
- **Allow established connections** (related and incoming traffic for active sessions).
- **Block traffic** from external networks attempting to reach internal services.
  
---

## 2. **Firewall between VLAN 2 (IoT) and Switch**

This firewall enforces rules to control traffic between the IoT devices and the main network switch. The goal is to ensure that IoT devices do not have unrestricted access to the broader network and can only access the internet if needed.

### General Rules:
- **Allow outbound traffic to the internet** (to access cloud services, etc.).
- **Deny inter-VLAN communication** between IoT devices and other VLANs, except for necessary services like DHCP and DNS.
- **Block inbound traffic** from VLANs 1 (Internal Network) and 4 (SOC Network) to the IoT VLAN.
- **Allow DNS, NTP, and other service-based traffic** from VLAN 2 to the appropriate servers.
  
**Note**: The firewall rules here are particularly strict because IoT devices often have weak security and need to be isolated from other internal resources.

---

## 3. **Firewall between VLAN 3 (Guest) and Switch**

The firewall between the Guest network and the main switch ensures that devices in the Guest VLAN (such as laptops and mobile phones) are isolated from critical internal resources while still being able to access the internet.

### General Rules:
- **Allow outbound traffic** to the internet for guest devices.
- **Block inbound traffic** from VLAN 3 (Guest) to any internal networks (e.g., VLAN 1, 2, 4, 5, 6).
- **Block direct access** from Guest devices to sensitive network resources.
- **Rate-limit traffic** to prevent abuse and ensure fair usage of available bandwidth for guest devices.
  
---

## 4. **Firewall between VLAN 5 (HoneyNet) and Switch**

The firewall between the HoneyNet and the main switch ensures that the deceptive systems in VLAN 5 are isolated from the internal network while still capturing and logging malicious activity.

### General Rules:
- **Allow inbound traffic** to VLAN 5 from the internet to simulate attack scenarios.
- **Block all inbound traffic** from VLAN 5 to VLANs 1 (Internal Network), 2 (IoT), and 3 (Guest).
- **Log all traffic** to and from VLAN 5 for later analysis.
- **Block all inter-VLAN communication** except to the SOC Network (VLAN 4), as the SOC is responsible for monitoring and analyzing the HoneyNet.
- **Implement captive portal** to entrap attackers and collect data.

---

## 5. **Firewall between Secure Catalyst Switches and Other VLANs**

There are three **Secure Catalyst Switches** in the network. These switches are critical for ensuring that traffic between different VLANs is managed securely.

### General Rules for Secure Catalyst Switches:
- **Block unauthorized access** to and from the switches, ensuring that only authorized network devices can manage the switches.
- **Allow management access** to the switches from the Internal Network (VLAN 1) but block access from other VLANs (except SOC VLAN).
- **Apply role-based access controls** (RBAC) to restrict access to the switches based on device type and trust level.
- **Enable VLAN segmentation** and **network ACLs** to further isolate traffic between VLANs.
- **Allow network management protocols** (e.g., SSH, SNMP) from trusted devices and only over secure channels.
  
**Note**: The configuration of these switches can be critical for enforcing segmentation, ensuring that VLAN policies are applied consistently across the network.

---

## 6. **Firewall Rules Summary Table**

| Rule ID | Source VLAN | Destination VLAN | Action    | Description                                             |
|---------|-------------|------------------|-----------|---------------------------------------------------------|
| 1       | VLAN 1      | WAN              | Allow     | Outbound traffic to the internet from admin devices.    |
| 2       | VLAN 2      | WAN              | Allow     | Internet access for IoT devices.                       |
| 3       | VLAN 2      | VLAN 1, VLAN 4   | Deny      | Block IoT devices from accessing internal resources.    |
| 4       | VLAN 3      | VLAN 1, 2, 4, 5  | Deny      | Guest devices cannot access internal resources.         |
| 5       | VLAN 3      | WAN              | Allow     | Outbound traffic to the internet for guest devices.     |
| 6       | VLAN 5      | VLAN 1, 2, 3     | Deny      | HoneyNet is isolated from other internal VLANs.          |
| 7       | VLAN 5      | VLAN 4           | Allow     | SOC can access HoneyNet for monitoring purposes.        |
| 8       | Catalyst    | VLAN 1           | Allow     | Management access for secure switches from VLAN 1.      |
| 9       | Catalyst    | VLAN 2, 3, 5     | Deny      | Block access to switches from non-admin VLANs.          |

---

## 7. **Future Considerations for Firewall Rules**

- **Dynamic Segmentation**: Implement policies to automatically segment new devices based on their behavior or attributes.
- **Advanced Threat Detection**: Integrate firewall logging with a SIEM solution (e.g., Splunk) for real-time alerting on suspicious traffic patterns.
- **Application Layer Filtering**: Add deep packet inspection (DPI) for advanced filtering on services such as HTTP, DNS, and FTP.
- **Automated Incident Response**: Use Ansible to automate firewall changes in response to specific threat indicators.

---

## 8. **Firewall Logging and Monitoring**

- **Enable logging** on all firewalls for detailed traffic analysis and forensic purposes.
- **Integrate firewall logs** with a centralized logging system (e.g., Splunk) for visibility and alerting on potential security incidents.
- **Regularly review firewall logs** to ensure that the rules are working as expected and that no unauthorized changes have been made.

---

This document should serve as a guide for understanding and configuring the firewall rules in your network, ensuring proper security, segmentation, and monitoring across the lab environment.
