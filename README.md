# Zero Trust Enterprise Network

> **Computer Network Lab Project**  
> Simulation Environment: **Cisco Packet Tracer 9.0.1.0858**

---

## 📌 Project Overview

This Computer Network Lab project models a segmented enterprise network in Cisco Packet Tracer. Its goal is to demonstrate department-level network separation, automatic IP addressing, centralized identity services, and controlled access between internal, DMZ, and Outside networks.

The project uses VLANs to separate departments. VTP distributes VLAN definitions across internal switches, and DHCP assigns addresses to client PCs. Security controls and attack demonstrations will be added after the network foundation is working.

---

## 📊 Project Size and Departments

The target design accommodates **at least 70 PCs**: 68 internal PCs and 3 Outside test PCs.

| Department or Network | VLAN | Subnet | Default Gateway | Planned PCs / Endpoints |
|:---|:---:|:---|:---|:---:|
| **Users** | 10 | `10.10.10.0/24` | `10.10.10.1` | 9 |
| **Finance** | 11 | `10.10.11.0/24` | `10.10.11.1` | 3 |
| **HR** | 12 | `10.10.12.0/24` | `10.10.12.1` | 4 |
| **Engineering** | 13 | `10.10.13.0/24` | `10.10.13.1` | 2 |
| **Research** | 14 | `10.10.14.0/24` | `10.10.14.1` | 8 |
| **Operations** | 15 | `10.10.15.0/24` | `10.10.15.1` | 8 |
| **Marketing** | 16 | `10.10.16.0/24` | `10.10.16.1` | 8 |
| **Support** | 17 | `10.10.17.0/24` | `10.10.17.1` | 8 |
| **Logistics** | 18 | `10.10.18.0/24` | `10.10.18.1` | 8 |
| **Training** | 19 | `10.10.19.0/24` | `10.10.19.1` | 8 |
| **Servers** | 20 | `10.10.20.0/24` | `10.10.20.1` | 3 servers |
| **Management** | 99 | `10.10.99.0/24` | `10.10.99.1` | 2 |
| **Outside test network** | *Separate* | Planned: `198.51.100.0/24` | Planned: `198.51.100.1` | 3 |
| **DMZ** | *Separate* | Planned: `172.16.50.0/24` | Planned: `172.16.50.1` | 1 server |

> **Addressing Scheme:** PCs use DHCP. Network-device interfaces and servers use static addresses.

---

## 🛠️ Main Devices

- **`ISP`**: Cisco 2911 router simulating the Internet/Outside network
- **`ASA1`**: Cisco ASA 5506-X firewall
- **`CORE`**: Cisco Catalyst 3560-24PS multilayer switch providing internal VLAN gateways and inter-VLAN routing
- **`ACC1`–`ACC9`**: Cisco Catalyst 2960 internal access switches
- **`Outside-SW`**: Cisco Catalyst 2960 switch for the three Outside test PCs (kept separate from the internal VTP domain)
- **`AAA-Server`**: Planned RADIUS/AAA server for 802.1X authentication
- **`Web-Internal`**: Planned internal web server
- **`DMZ-Web`**: Planned DMZ web server

*Topology Structure:* Internal access switches connect to `CORE`. Department PCs connect to their assigned access switch. Outside PCs connect to `Outside-SW`. The ASA separates the Internal, DMZ, and Outside networks.

---

## 🔐 Planned Network Services & Security Controls

1. **VTP (VLAN Trunking Protocol):**  
   `CORE` acts as the VTP server; internal access switches (`ACC1`–`ACC9`) operate as VTP clients in domain `ZT-LAB` (Password: `ZTnet2026`). `Outside-SW` is excluded. Trunk links between `CORE` and access switches propagate VTP advertisements and VLAN traffic.
2. **DHCP:**  
   `CORE` provides a dedicated DHCP pool for each internal client VLAN. The `ISP` router provides a separate pool for the Outside test PCs.
3. **Inter-VLAN Routing:**  
   `CORE` provides default gateway Switched Virtual Interfaces (SVIs) for each internal VLAN.
4. **AAA/RADIUS & 802.1X:**  
   The AAA server authenticates selected endpoint users through the access switches.
5. **ACLs (Access Control Lists):**  
   Strict ACLs restrict lateral movement between departments and enforce least-privilege access to servers and management devices.
6. **ASA Firewall:**  
   Separates Inside, DMZ, and Outside security zones, inspecting traffic and allowing only explicitly authorized services to the DMZ.
7. **Security Demonstrations & Testing:**  
   Demonstrating successful authorized access vs. blocked unauthorized/prohibited access attempts.

---

## 📈 Current Progress

### ✅ Completed
- [x] Created Packet Tracer topology and saved project file (`cn lab project.pkt`).
- [x] Placed and named router (`ISP`), firewall (`ASA1`), core switch (`CORE`), access switches (`ACC1`–`ACC9`, `Outside-SW`), and servers (`AAA-Server`, `Web-Internal`, `DMZ-Web`).
- [x] Added departmental PCs and utilized colored boundaries/labels to distinguish network groups.
- [x] Connected devices with physical cabling.
- [x] Configured `CORE` as VTP server (domain: `ZT-LAB`, password: `ZTnet2026`).
- [x] Configured internal access switches as VTP clients using the same domain and credentials.

### ⏳ Pending Configuration
- [ ] Create VLANs on `CORE` (VLANs 10–20, 99).
- [ ] Configure and verify 802.1Q trunk links across all switch-to-switch links.
- [ ] Assign department access switch ports to their designated VLANs.
- [ ] Configure SVIs (VLAN gateway interfaces) and enable IP routing on `CORE`.
- [ ] Configure DHCP pools and exclusions on `CORE` and `ISP`.
- [ ] Set PCs to obtain IP addresses automatically and assign static IPs to servers.
- [ ] Configure ASA routing, NAT, and security zone access policies.
- [ ] Implement AAA/RADIUS, 802.1X authentication, and segmentation ACLs.
- [ ] Execute baseline connectivity and security validation tests.

---

## 👥 Team Work Split

### 👤 Member 1: Network Foundation
- Maintain topology, department/VLAN plan, and IP address allocation plan.
- Configure VTP and 802.1Q trunk links.
- Create VLANs and assign access ports.
- Configure `CORE` gateway interfaces (SVIs) and inter-VLAN routing.
- Configure DHCP pools and verify automatic IP assignment on client PCs.
- Configure baseline ISP/ASA connectivity and test basic network reachability.
- Save a verified working handoff Packet Tracer file and document all port assignments.

### 👤 Member 2: Security & Demonstration
- Continue implementation directly from the saved Part 1 handoff file.
- Configure AAA/RADIUS service and 802.1X port authentication.
- Configure ASA security policy, inspection, and NAT as required.
- Apply micro-segmentation ACLs to prevent lateral movement and isolate servers/management.
- Execute authorized access, denied access, and unauthorized lateral movement tests.
- Capture verification screenshots and prepare the security demonstration and report.

---

## 🧪 Validation Plan

### Phase 1: Pre-Handoff Verification (Foundation)
- [ ] Confirm VTP domain, version, and operating mode on `CORE` and each internal access switch.
- [ ] Verify that all VLANs (10–20, 99) propagate to all internal access switches over trunk links (`show vlan brief`).
- [ ] Confirm each PC receives an IP address from its designated department DHCP subnet.
- [ ] Test that each PC can ping its default gateway SVI on `CORE`.
- [ ] Verify basic server reachability and inter-VLAN routing paths prior to applying security restrictions.

### Phase 2: Post-Security Verification (Controls & Isolation)
- [ ] Verify authorized endpoint users successfully authenticate via 802.1X.
- [ ] Verify unauthorized devices or invalid credentials are systematically denied access.
- [ ] Confirm department-to-department lateral traffic is blocked by ACLs.
- [ ] Validate that only approved ports/services can reach internal servers and the DMZ.
- [ ] Confirm Outside endpoints (`OUT1`–`OUT3`) can only reach the published DMZ service and are blocked from the internal network.

---

## 📁 Repository Structure
- **`cn lab project.pkt`**: Cisco Packet Tracer topology and device configuration file.
- **`Network_Architecture_Pitch-1.pptx`**: Architecture pitch presentation.
- **`Zero_Trust_CPT_Build_Guide.pdf`**: Detailed step-by-step build guide.
- **`I'm building a Computer Network Lab.txt`**: Project specifications, device breakdown, and notes.
- **`README.md`**: Master documentation and lab execution roadmap.
