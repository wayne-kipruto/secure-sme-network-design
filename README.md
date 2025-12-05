#SME Secure Network Infrastructure Design 🛡️

### Project Overview
This project documents the design and simulation of a secure, segmented network infrastructure for **Rorizzi Digital Services**, a tech consultancy and cyber hub. The goal was to replace a flat network architecture with an enterprise-grade solution that isolates sensitive business operations from public guest traffic while ensuring high availability.

**Tools Used:** Cisco Packet Tracer v9.0, Cisco IOS.

---

## 🏗️ Network Topology
> *Architecture Diagram showing the Hub-and-Spoke topology with VLAN segmentation.*

![Network Topology](Rorizzi-Network-Topology.png)


---

## ⚙️ Key Features & Configuration

### 1. VLAN Segmentation (Security)
To prevent unauthorized access to financial data, the network is divided into two distinct broadcast domains using **802.1Q tagging**:
- **VLAN 10 (Management):** Dedicated to Admin PCs and the Network Printer. Restricted access.
- **VLAN 20 (Guest/Public):** Dedicated to Client PCs and Wi-Fi users. Isolated from the Admin network.

### 2. Inter-VLAN Routing (Router-on-a-Stick)
Implemented **Sub-Interfaces** on the Edge Router to allow controlled communication between VLANs (e.g., for printing) while maintaining logical separation.

**Configuration Snippet (Router):**
```cisco
interface GigabitEthernet0/0.10
 description Admin_Gateway
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0

interface GigabitEthernet0/0.20
 description Guest_Gateway
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
```
### 3. Dynamic Addressing (DHCP)
Configured a DHCP pool on Rorizzi-Router to automatically assign IP addresses to Guest devices (Mobile/Laptops), significantly reducing administrative overhead.

Pool Name: GUEST_POOL

Gateway: 192.168.20.1

DNS: 8.8.8.8

### 4.Wireless Security
Deployed a Wireless Access Point (WAP) secured with WPA2-PSK (AES) encryption to protect guest traffic from interception.
