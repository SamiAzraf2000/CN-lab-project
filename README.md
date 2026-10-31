# CN Lab Project: Zero Trust Enterprise Network

Computer Networks Lab Project implemented in **Cisco Packet Tracer**.

---

## 📌 Project Overview
This project models a **Zero Trust Enterprise Network Architecture** demonstrating micro-segmentation, centralized authentication, role-based access control (RBAC), and strict perimeter/internal security.

### 🏢 Network Topology & Devices
- **Perimeter & Security**:
  - Router: Cisco 2911 (ISP)
  - Firewall: Cisco ASA 5506-X (Edge & Inspection)
- **Switching Infrastructure**:
  - Core Multilayer Switch: Cisco Catalyst 3560-24PS
  - Access Switches: Cisco Catalyst 2960 (`ACC1`, `ACC2`, `ACC3`, `Outside-SW`)
- **Central Servers**:
  - AAA/RADIUS Server (Centralized Authentication & 802.1X)
  - Web-Internal (Internal Corporate Portal)
  - DMZ-Web (Public / Demilitarized Zone Services)
- **Departmental Endpoints**:
  - General Users (`User-PC1` – `User-PC9`)
  - Finance (`Fin-PC1` – `Fin-PC3`)
  - Human Resources (`HR1` – `HR4`)
  - Engineering (`ENG1` – `ENG2`)
  - Management / IT Admin (`Admin-PC1` – `Admin-PC2`)
  - External / Untrusted (`OUT1` – `OUT3`)

---

## 📂 Repository Contents
- **`cn lab project.pkt`**: Cisco Packet Tracer topology and lab configuration file.
- **`Network_Architecture_Pitch-1.pptx`**: Architecture pitch presentation.
- **`Zero_Trust_CPT_Build_Guide.pdf`**: Detailed build and step-by-step implementation guide.
- **`I'm building a Computer Network Lab.txt`**: Lab project specifications, roadmap, and device notes.
