# Enterprise High-Availability Architecture | Cytonn Innovation Ltd 🌐

![Main Architecture Topology](./Enterprise_Network_Design.png)

## 📋 Project Overview
This project involved the end-to-end design and implementation of a secure, 3-floor hierarchical network for **Cytonn Innovation Ltd**, supporting a workforce of **600 staff**. The architecture focuses on the "Three Pillars of Networking": **Redundancy, Scalability, and Security**.

### 🛠️ Key Technical Specifications
* **Capacity:** Scalable infrastructure for 600+ users across 6 distinct departments.
* **Topology:** 3-Floor Hierarchical Model (Core, Distribution, Access).
* **Hardware:** Catalyst 3850 (Core), Catalyst 2960 (Access), and dual Cisco ASA 5500-X Firewalls.

---

## ⚙️ Advanced Implementations

### 1. High Availability & Redundancy 🛡️
To eliminate single points of failure, I implemented:
* **HSRP (Hot Standby Router Protocol):** Configured for gateway redundancy across the Catalyst 3850s, successfully establishing **ACTIVE/STANDBY** states.
* **EtherChannel (LACP):** Bundled physical links between core switches to increase bandwidth and provide link-level redundancy.
* **ISP Redundancy:** Dual-homed WAN connections routing traffic through SEACOM and SAFARICOM.

### 2. Security & Firewall Architecture 🔐
A multi-zone security strategy was deployed using **Cisco ASA Firewalls**:
* **DMZ (Demilitarized Zone):** Isolated public-facing servers (Web, FTP, Email, APP, NAS) from the internal network.
* **Inside Zone:** Secured critical internal identity and management resources (DHCP, DNS, RADIUS) on a dedicated server VLAN.
* **STP Optimization:** Tuned Spanning Tree Protocol with PortFast and BPDUguard on access layers to prevent Layer 2 loops.

### 3. Dynamic Routing & Segmenting 🛣️
* **OSPF (Open Shortest Path First):** Utilized as the primary Interior Gateway Protocol (IGP) for fast convergence.
* **Centralized Wireless & Voice:** Deployed a Cisco WLC for corporate/guest WiFi and a Cisco Voice Gateway for IP Telephony.

---

## 🔢 IP Addressing & VLAN Scheme

| Network Segment | VLAN ID | IP Network Range | Subnet Mask | Description |
| :--- | :--- | :--- | :--- | :--- |
| **Management** | 10 | `192.168.10.0` | `255.255.255.0` | Network device management (SSH/VTY) |
| **LAN (Data)** | 20 | `172.16.0.0` | `255.255.0.0` | Wired employee workstations across floors |
| **WLAN** | 50 | `10.20.0.0` | `255.255.0.0` | Corporate WiFi via Cisco WLC |
| **VoIP** | 70 | `172.30.0.0` | `255.255.0.0` | IP Telephony (Voice Gateway) |
| **Inside Servers**| 90 | `10.11.11.32` | `255.255.255.224` | AD, DHCP, DNS, and RADIUS Servers |
| **DMZ** | N/A | `10.11.11.0` | `255.255.255.224` | Fortified zone for WEB/FTP/Email servers |
| **ISP 1 (SEACOM)**| N/A | `105.100.50.0` | `255.255.255.252` | Public WAN Link (Primary) |
| **ISP 2 (Safaricom)**| N/A| `197.200.100.0` | `255.255.255.252` | Public WAN Link (Redundant) |
| **Blackhole** | 199 | N/A | N/A | Security sinkhole for all unused switch ports |

---

## ✅ Verification & Evidence

### 1. HSRP Redundancy Verification
Executing `show standby brief` on the Core Switches verifies that one switch is actively routing traffic while the other is in standby mode, ensuring zero downtime if the primary switch fails.
![HSRP Verification](./HSRP_EVIDENCE.png)

### 2. EtherChannel (LACP) Link Aggregation
Running `show etherchannel summary` confirms that the links between the Core switches are successfully bundled using LACP, maximizing throughput and preventing STP blocking.
![EtherChannel Evidence](./LACP_EVIDENCE.png)

### 3. End-to-End Connectivity (Inside to DMZ)
A successful ping from an internal employee workstation to the DMZ Web Server verifies that Inter-VLAN routing, OSPF, and ASA Firewall inspection rules are operating correctly.
![Ping Evidence](./PING_EVIDENCE.png)

---

## 📂 Project Files
* 📂 **[Download Packet Tracer Lab (.pkt)](./Cytonn_Innovation_Network.pkt)**
