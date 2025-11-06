# Lab 4: Inter-VLAN Communication with Router-on-a-Stick

## Objective
Create two VLANs on a switch and configure a router to allow communication between them using router-on-a-stick. Test connectivity to verify the network is functioning correctly.

This lab demonstrates:
- VLAN segmentation
- Access port configuration
- Trunk configuration
- Router subinterfaces for inter-VLAN routing
- Basic network connectivity testing

---

## Network Topology


---

## VLAN & IP Addressing Plan

| VLAN | Purpose | Subnet | Default Gateway (Router) |
|------|---------|--------|--------------------------|
| **10** | Workstation Group A | **10.10.10.0/24** | **10.10.10.1** |
| **20** | Workstation Group B | **10.10.20.0/24** | **10.10.20.1** |

| Device | VLAN | Interface | IP Address |
|--------|------|-----------|------------|
| PC-A | 10 | NIC | 10.10.10.10 |
| PC-B | 20 | NIC | 10.10.20.10 |
| Router | — | G0/0.10 | 10.10.10.1 |
| Router | — | G0/0.20 | 10.10.20.1 |

---

## Configuration Steps (Summary — Commands Added Later)

### 1. Create VLANs on the switch
- VLAN 10 = "Clients10"
- VLAN 20 = "Clients20"

### 2. Assign switch ports to VLANs
- Port for PC-A → VLAN 10
- Port for PC-B → VLAN 20

### 3. Configure the switch uplink as a **trunk**
- Allows VLAN traffic to travel between switch & router

### 4. Configure router subinterfaces
- One subinterface per VLAN
- Each gets its own IP → becomes the **default gateway**

### 5. Test and verify
- Ping default gateways
- Ping across VLANs (PC-A ↔ PC-B)
- Confirm which connectivity works and why

---

## Verification and Testing Commands

| Test | Command | Expected Result |
|------|---------|----------------|
| Check PC IPs | `ipconfig` (Windows) | Correct IP, subnet, gateway |
| Check VLAN assignment | `show vlan brief` | Ports assigned correctly |
| Check trunk status | `show interfaces trunk` | Switch uplink listed as trunk |
| Test LAN connectivity | `ping 10.10.10.1` (from PC-A) | Success |
| Test inter-VLAN connectivity | `ping 10.10.20.10` (PC-A → PC-B) | Success |

---

## What This Lab Demonstrates (Interview Talking Points)
- Understanding of VLAN segmentation and why networks use VLANs
- Ability to configure inter-VLAN routing using subinterfaces
- Comfort using structured IP addressing plans
- Logical connectivity testing process
- Awareness of the OSI model during troubleshooting

---

## Next Step After This Lab
Add **DHCP relay (ip helper-address)** so each VLAN can receive DHCP IPs from a single DHCP server.
