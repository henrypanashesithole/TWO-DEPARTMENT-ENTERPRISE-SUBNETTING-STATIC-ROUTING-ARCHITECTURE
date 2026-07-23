# Small Office / Departmental Router Configuration

## Project Overview & Rationale
This project demonstrates the design and step-by-step configuration of a departmental network routing architecture using Cisco Packet Tracer. 

**Why this project was created:**
* **Network Isolation & Organization:** To separate traffic between key business units (Accounts and Delivery) using distinct IP subnets for enhanced traffic management and security.
* **Gateway Implementation:** To set up an explicit routing mechanism (Layer 3 interfaces) that serves as default gateways for each department's local subnet.
* **Portfolio & Practical Hands-on:** To serve as a practical demonstration of IP addressing, CIDR subnetting (`/25`), and Cisco IOS CLI command execution.

---

## Network Topology
![Network Topology]

### Addressing Table
| Device | Interface | IP Address | Subnet Mask | Subnet Prefix | Assigned Department |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Router0 | Gi0/0 | 192.168.40.1 | 255.255.255.128 | /25 | Accounts Gateway |
| Router0 | Gi0/1 | 192.168.40.129 | 255.255.255.128 | /25 | Delivery Gateway |

---

## Router Configuration Commands

```cisco
! Router Interface Setup
Router> enable
Router# configure terminal
Router(config)# hostname Router0

! Configure Accounts Department Gateway Interface
Router0(config)# interface GigabitEthernet0/0
Router0(config-if)# ip address 192.168.40.1 255.255.255.128
Router0(config-if)# no shutdown
Router0(config-if)# exit

! Configure Delivery Department Gateway Interface
Router0(config)# interface GigabitEthernet0/1
Router0(config-if)# ip address 192.168.40.129 255.255.255.128
Router0(config-if)# no shutdown
Router0(config-if)# exit

Router0# copy running-config startup-config

## Verification & Testing
To confirm connectivity across subnets, ping tests were conducted from a host in the Accounts subnet (192.168.40.0/25) targeting the gateway and hosts in the Delivery subnet (192.168.40.128/25).
