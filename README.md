# Zero Trust Enterprise Network

## Project overview

This Computer Network Lab project models a multi-department enterprise network with a headquarters site and two branches in Cisco Packet Tracer 9.0.1.0858.

The design uses VLANs to separate departments, VTP to distribute VLAN definitions among headquarters access switches, and DHCP so PCs can receive IP addresses automatically. The planned security layer includes centralized RADIUS authentication, 802.1X, inter-VLAN ACLs, and an ASA firewall separating internal, DMZ, and Outside networks.

Project guidance and conversation:
[Zero Trust project walkthrough](https://chatgpt.com/s/cx_6ae9e8758c508191a098378832a732a5)

## Planned network size

The current target is approximately **87 PCs**:

- 68 PCs across headquarters departments
- 3 Outside test PCs
- 8 PCs at Branch A
- 8 PCs at Branch B

The topology also includes three servers and the network infrastructure devices. Verify the final count in Packet Tracer before reporting it as the completed device count.

## VLAN and subnet plan

| Site or department | VLAN | Subnet | Gateway |
|---|---:|---|---|
| HQ Users | 10 | `10.10.10.0/24` | `10.10.10.1` |
| HQ Finance | 11 | `10.10.11.0/24` | `10.10.11.1` |
| HQ HR | 12 | `10.10.12.0/24` | `10.10.12.1` |
| HQ Engineering | 13 | `10.10.13.0/24` | `10.10.13.1` |
| HQ Research | 14 | `10.10.14.0/24` | `10.10.14.1` |
| HQ Operations | 15 | `10.10.15.0/24` | `10.10.15.1` |
| HQ Marketing | 16 | `10.10.16.0/24` | `10.10.16.1` |
| HQ Support | 17 | `10.10.17.0/24` | `10.10.17.1` |
| HQ Logistics | 18 | `10.10.18.0/24` | `10.10.18.1` |
| HQ Training | 19 | `10.10.19.0/24` | `10.10.19.1` |
| HQ Servers | 20 | `10.10.20.0/24` | `10.10.20.1` |
| HQ Management | 99 | `10.10.99.0/24` | `10.10.99.1` |
| Branch A | 30 | `10.10.30.0/24` | `10.10.30.1` |
| Branch B | 40 | `10.10.40.0/24` | `10.10.40.1` |
| Outside test network | Separate network | Planned: `198.51.100.0/24` | Planned: `198.51.100.1` |
| DMZ | Separate network | Planned: `172.16.50.0/24` | Planned: `172.16.50.1` |

PCs are intended to use DHCP. Server, router, firewall, and switch management addresses require planned configuration. DHCP operation and each PC's assigned subnet still need verification.

## Main devices

- `ISP`: Cisco 2911 router simulating the provider network
- `Internet-WAN`: Cloud-PT symbol for the simulated Internet/WAN
- `Provider-WAN-SW`: 2960 switch for the provider-side branch links
- `ASA1`: Cisco ASA 5506-X firewall
- `CORE`: Cisco 3560-24PS multilayer switch for HQ VLAN gateways and routing
- `ACC1`–`ACC9`: planned HQ department access switches
- `Outside-SW`: 2960 switch for the Outside test PCs
- Branch A: `Branch-A-RTR`, `Branch-A-SW`, and 8 PCs
- Branch B: `Branch-B-RTR`, `Branch-B-SW`, and 8 PCs
- `AAA-Server`: planned RADIUS/AAA server
- `Web-Internal`: planned internal web server
- `DMZ-Web`: planned DMZ web server

`Internet-WAN` is a visual cloud symbol. Routing is provided by the ISP router and provider-side network configuration.

## Intended network behavior

- Each department and branch uses a separate VLAN/subnet.
- PCs obtain addresses dynamically using DHCP.
- VTP distributes HQ VLAN definitions from CORE to HQ access switches over trunk links.
- Branch VLANs 30 and 40 are configured locally and remain outside the HQ VTP domain.
- The ASA separates Inside, Outside, and DMZ traffic.
- RADIUS and 802.1X authenticate selected users/devices.
- ACLs restrict inter-department movement and limit access to servers and management.
- Branch-to-HQ security and Internet access will be tested after the WAN routing design is configured.

## Team work split

### Member 1: network foundation

- Maintain the topology and address/VLAN plan.
- Configure VTP, VLANs, trunk links, and access ports.
- Configure HQ and branch gateway interfaces and routing.
- Configure DHCP and verify each client receives an address from the correct subnet.
- Configure baseline ISP/ASA/provider connectivity.
- Save a working handoff file and document port assignments.

### Member 2: security and demonstration

- Continue from the saved handoff file.
- Configure RADIUS/AAA and 802.1X.
- Configure the ASA security policy and NAT.
- Apply ACLs for department isolation and controlled server/management access.
- Configure or verify secure branch-to-HQ access as agreed.
- Run the allowed/denied traffic demonstrations and capture evidence.

## Progress and verification status

### Completed or reported complete

- HQ topology, department groups, VLAN labels, and colored visual areas have been placed.
- Branch A and Branch B routers and access switches have been added.
- Branches are planned for VLANs 30 and 40.
- CORE is in VTP server mode in domain `ZT-LAB`.
- HQ internal access switches were configured as VTP clients in domain `ZT-LAB`.
- CORE trunk interfaces `Fa0/4` and `Fa0/6` through `Fa0/12` are trunking.
- The Users access switch has `Fa0/1` trunking and `Fa0/2` through `Fa0/10` assigned to VLAN 10.
- VLANs 10–20 and 99 appear active across the configured trunks.
- PCs were reportedly set to obtain addresses through DHCP; the pools and results have not yet been verified.

### Still to do or verify

- Confirm that every intended HQ access switch has an uplink; CORE currently reports eight 2960 neighbors, while the plan has nine HQ access switches.
- Configure and verify trunks on the remaining HQ access switches.
- Assign each department's PC-facing ports to the correct VLAN.
- Configure and verify CORE VLAN gateway interfaces and inter-VLAN routing.
- Verify DHCP pools and test a PC in every VLAN.
- Configure branch switch VLANs, branch router gateways, branch DHCP, and ISP/WAN routing.
- Verify how `Provider-WAN-SW` and `Internet-WAN` are used in the final simulated WAN design.
- Configure ASA interfaces, routing, NAT, and firewall rules.
- Configure AAA/RADIUS, 802.1X, and ACLs.
- Run baseline and security tests, capture screenshots, and save the Member 1 handoff file.
