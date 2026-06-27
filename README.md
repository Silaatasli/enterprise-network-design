# Enterprise Network Infrastructure Design & Simulation

A secure, multi-layered, and high-availability corporate network infrastructure designed and simulated using **Cisco Packet Tracer**. This project demonstrates a complete enterprise network lifecycle, including advanced routing, switching, security policies, and redundancy mechanisms.

##  Architecture Overview
The topology is designed following Cisco's hierarchical network design model, divided into Core, Distribution, and Access layers to ensure scalability, ease of management, and fault tolerance.

### Key Technical Features

* **High Availability & Edge Redundancy:** 
  * Features a Dual-ISP implementation (MAIN and BACKUP links).
  * Configured with **Floating Static Routing** to ensure automatic, seamless failover and maximum uptime if the primary link goes down.
* **Core & Distribution Layers:** 
  * Multi-layer switches (MLS) handle high-speed Inter-VLAN routing via Switched Virtual Interfaces (SVIs).
  * Redundant cross-links between switches prevent single points of failure within the local backbone.
* **Dynamic IP Management (VLSM & DHCP):** 
  * Structural IP addressing using the **Variable Length Subnet Masking (VLSM)** method based on the `10.10.0.0/16` private IP range.
  * Local networks are divided into precise `/24` subnets to guarantee strict Layer 3 isolation between specific departments (Servers, Accounting, regular Users, and Guests).
  * Centralized IP allocation managed dynamically via a dedicated **DHCP Server** configured with dedicated scopes and exclusion pools.
* **Network Security & Access Control:**
  * Network boundary security is hardened with standard and **Extended Access Control Lists (ACLs)**.
  * Implemented strict traffic control policies to isolate sensitive departments (e.g., Accounting) and restrict Guest network capabilities (internet access only, zero internal LAN access).
  * Integrated **Network Address Translation (NAT)** on the edge router to mask internal local IPs and enable secure external internet access.

---

| Department / VLAN | Subnet Block | Subnet Mask | Gateway | Assignment Type |
| --- | --- | --- | --- | --- |
| **Server Farm (VLAN 10)** | `10.10.10.0/24` | `255.255.255.0` | `10.10.10.1` | Static & DHCP |
| **Accounting (VLAN 20)** | `10.10.20.0/24` | `255.255.255.0` | `10.10.20.1` | Dynamic (DHCP) |
| **Regular Users (VLAN 30)**| `10.10.30.0/24` | `255.255.255.0` | `10.10.30.1` | Dynamic (DHCP) |
| **Guests (VLAN 40)** | `10.10.40.0/24` | `255.255.255.0` | `10.10.40.1` | Dynamic (DHCP) |

---   

## 🛠️ How to Run the Simulation
1. Download and install **Cisco Packet Tracer**.
2. Clone this repository or download the `.pkt` file directly.
3. Due to Packet Tracer's file path association quirks, **do not double-click the file directly from a zipped folder**.
4. Extract the file to your desktop, open Cisco Packet Tracer, and navigate to **`File -> Open`** to load the topology correctly.
5. Switch to *Simulation* or *Realtime* mode to test connection pings, DHCP assignments, and ACL rules.
