# Intermediate Level Concepts

**This section is part of the [Networking Principles Guide](../Networking-Principles.md)**

---

## Intermediate Level Concepts

### 2.1 Ethernet and Switching

**Ethernet Fundamentals:**

- **CSMA/CD (Carrier Sense Multiple Access with Collision Detection)**:
  - Legacy access method for shared Ethernet
  - Devices listen before transmitting
  - Detects collisions and retransmits
  - Not needed in full-duplex switched networks

- **Ethernet Frame Structure**:
  - Preamble (7 bytes) + Start Frame Delimiter (1 byte)
  - Destination MAC Address (6 bytes)
  - Source MAC Address (6 bytes)
  - EtherType/Length (2 bytes)
  - Payload (46-1500 bytes)
  - Frame Check Sequence (4 bytes)
  - Total: 64-1518 bytes

- **Ethernet Standards**:
  - 10BASE-T: 10 Mbps over twisted pair
  - 100BASE-TX: 100 Mbps (Fast Ethernet)
  - 1000BASE-T: 1 Gbps (Gigabit Ethernet)
  - 10GBASE-T: 10 Gbps over twisted pair
  - Fiber standards: 1000BASE-SX/LX, 10GBASE-SR/LR, etc.

**Switch Operation:**

- **MAC Address Learning**:
  - Switches build MAC address tables by examining source addresses
  - Dynamic learning from incoming frames
  - Aging timer removes stale entries

- **Frame Forwarding Methods**:
  - **Store-and-Forward**: Receives entire frame, checks for errors, then forwards
    - Highest latency but error checking
  - **Cut-Through**: Forwards as soon as destination address is read
    - Lowest latency but no error checking
  - **Fragment-Free**: Receives first 64 bytes (collision window), then forwards
    - Balance between latency and error checking

- **VLANs (Virtual LANs)**:
  - Logical segmentation of a physical network
  - Benefits: Security, broadcast domain reduction, flexibility
  - Types: Port-based, MAC-based, protocol-based, policy-based
  - VLAN Trunking: Carries multiple VLANs over single link (802.1Q)

**Detailed VLAN Concepts:**

**VLAN Benefits:**
- **Broadcast Domain Segmentation**: Reduces broadcast traffic
- **Security**: Isolates sensitive departments
- **Flexibility**: Logical grouping independent of physical location
- **Cost Efficiency**: Reduces need for additional hardware

**VLAN ID Ranges:**
- **Normal Range**: 1-1005 (stored in VLAN database)
- **Extended Range**: 1006-4094 (VTP v3 only, stored in running config)
- **Reserved VLANs**: 
  - VLAN 1: Default VLAN (cannot be deleted)
  - VLAN 1002-1005: FDDI/Token Ring (legacy)

**802.1Q Trunking Protocol:**

**802.1Q Frame Structure:**

```
Original Ethernet Frame:
| Dst MAC | Src MAC | Type | Data | FCS |

802.1Q Tagged Frame:
| Dst MAC | Src MAC | 0x8100 | PRI | CFI | VLAN ID | Type | Data | FCS |
                            (4 bytes tag inserted here)
```

**802.1Q Tag Fields:**
- **TPID (Tag Protocol Identifier)**: 0x8100 (identifies 802.1Q frame)
- **PRI (Priority)**: 3 bits for QoS (0-7)
- **CFI (Canonical Format Indicator)**: 1 bit (always 0 for Ethernet)
- **VID (VLAN ID)**: 12 bits (1-4094)

**Native VLAN:**
- Untagged traffic on trunk links
- Default: VLAN 1
- **Important**: Native VLAN must match on both ends

**VLAN Configuration Example (Cisco):**

```cisco
! Create VLAN
vlan 10
  name SALES

vlan 20
  name ENGINEERING

! Assign access port to VLAN
interface GigabitEthernet0/1
  switchport mode access
  switchport access vlan 10

! Configure trunk port
interface GigabitEthernet0/24
  switchport mode trunk
  switchport trunk native vlan 100
  switchport trunk allowed vlan 10,20,100
  ! OR allow all VLANs:
  ! switchport trunk allowed vlan all

! Configure trunk encapsulation (older switches)
interface GigabitEthernet0/24
  switchport trunk encapsulation dot1q
  switchport mode trunk

! Verify VLAN configuration
show vlan brief
show vlan id 10
show interfaces trunk
show interfaces Gi0/24 switchport
```

**Inter-VLAN Routing:**

To enable communication between VLANs, a router or Layer 3 switch is required:

**Router-on-a-Stick Configuration:**

```cisco
! Router Configuration
interface GigabitEthernet0/0.10
  encapsulation dot1Q 10
  ip address 192.168.10.1 255.255.255.0

interface GigabitEthernet0/0.20
  encapsulation dot1Q 20
  ip address 192.168.20.1 255.255.255.0

! Switch Configuration
interface GigabitEthernet0/24
  switchport mode trunk
```

**Layer 3 Switch (SVI - Switched Virtual Interface):**

```cisco
! Enable IP routing
ip routing

! Configure SVI for each VLAN
interface vlan 10
  ip address 192.168.10.1 255.255.255.0
  no shutdown

interface vlan 20
  ip address 192.168.20.1 255.255.255.0
  no shutdown
```

**VLAN Trunking Protocol (VTP):**

**VTP Modes:**
- **Server**: Can create, modify, delete VLANs (propagates to all)
- **Client**: Receives VLAN updates, cannot modify locally
- **Transparent**: Forwards VTP messages but doesn't participate

**VTP Configuration:**

```cisco
! Configure VTP domain
vtp domain COMPANY
vtp mode server
vtp version 2

! Verify VTP status
show vtp status
show vtp password
```

- **Spanning Tree Protocol (STP)**: 
  - Prevents loops in switched networks
  - Protocol: IEEE 802.1D
  - States: Blocking, Listening, Learning, Forwarding, Disabled
  - Enhanced versions: RSTP (Rapid STP), MSTP (Multiple STP)

**Detailed STP Operation (IEEE 802.1D):**

**STP Algorithm Steps:**

1. **Elect Root Bridge**:
   - Lowest Bridge ID wins (Priority + MAC Address)
   - Default priority: 32768
   - Example: Priority 4096 = 4096.0000.0000.0001

2. **Select Root Ports**:
   - One root port per non-root bridge
   - Lowest cost path to root bridge

3. **Select Designated Ports**:
   - One designated port per segment
   - Lowest cost path to root bridge

4. **Block Remaining Ports**:
   - All other ports become blocking
   - Prevents loops

**STP Port States:**

- **Blocking**: 
  - Receives BPDUs, does not forward frames
  - Duration: 20 seconds (max age timer)
  - Can transition to listening state

- **Listening**: 
  - Receives and sends BPDUs
  - No MAC address learning
  - Duration: 15 seconds (forward delay timer)
  - Elects root/designated ports

- **Learning**: 
  - Receives and sends BPDUs
  - Builds MAC address table
  - Duration: 15 seconds (forward delay timer)

- **Forwarding**: 
  - Normal operation
  - Forwards frames and learns MAC addresses
  - Only root and designated ports reach this state

- **Disabled**: 
  - Administratively shut down
  - Does not participate in STP

**STP Timers:**
- **Hello Timer**: 2 seconds (BPDU interval)
- **Max Age**: 20 seconds (maximum BPDU age)
- **Forward Delay**: 15 seconds (listening + learning)

**STP Port Costs (Legacy):**

| Link Speed | Cost |
|------------|------|
| 10 Mbps | 100 |
| 100 Mbps | 19 |
| 1 Gbps | 4 |
| 10 Gbps | 2 |

**Rapid STP (RSTP) - IEEE 802.1w:**

**RSTP Improvements:**
- Faster convergence (1-3 seconds vs 30-50 seconds)
- New port roles and states
- Backup port role for redundancy
- Proposal/Agreement mechanism

**RSTP Port Roles:**
- **Root Port**: Best path to root (same as STP)
- **Designated Port**: Best path on a segment
- **Alternate Port**: Backup root port
- **Backup Port**: Backup designated port
- **Disabled**: Not participating

**RSTP Port States:**
- **Discarding**: Replaces blocking/listening (no forwarding, no learning)
- **Learning**: Builds MAC table, no forwarding
- **Forwarding**: Normal operation

**RSTP Configuration Example (Cisco):**

```cisco
! Enable RSTP globally
spanning-tree mode rapid-pvst

! Configure priority for root bridge
spanning-tree vlan 10 priority 4096

! Configure port cost
interface GigabitEthernet0/1
  spanning-tree cost 2000

! Configure port priority
interface GigabitEthernet0/1
  spanning-tree port-priority 128

! View STP status
show spanning-tree
show spanning-tree root
show spanning-tree interface Gi0/1 detail
```

**STP Troubleshooting Commands:**

```cisco
! View STP topology
show spanning-tree summary
show spanning-tree vlan 10
show spanning-tree root detail

! Verify BPDUs
debug spanning-tree events
show spanning-tree inconsistentports

! Force recalculation
clear spanning-tree detected-protocols
```

**Link Aggregation:**

- **EtherChannel / Link Aggregation**:
  - Combines multiple physical links into one logical link
  - Standards: LACP (802.3ad), PAgP (Cisco proprietary)
  - Benefits: Increased bandwidth, redundancy, load balancing

### 2.2 Routing Fundamentals

**Routing Concepts:**

- **Routing vs. Switching**:
  - Switches forward within same network (Layer 2)
  - Routers forward between networks (Layer 3)

- **Routing Table**:
  - Contains network destinations and next-hop information
  - Includes: Network, Subnet Mask, Next Hop, Interface, Metric

- **Static Routing**:
  - Manually configured routes
  - Advantages: Simple, predictable, low overhead
  - Disadvantages: No automatic updates, manual maintenance

- **Dynamic Routing**:
  - Routes learned automatically via routing protocols
  - Advantages: Automatic updates, adapts to changes
  - Disadvantages: Requires processing, potential instability

**Distance Vector Protocols:**

- **RIP (Routing Information Protocol)**:
  - Hop count metric (max 15 hops)
  - Periodic updates every 30 seconds
  - Versions: RIPv1 (classful), RIPv2 (classless)
  - Slow convergence

- **EIGRP (Enhanced Interior Gateway Routing Protocol)**:
  - Cisco proprietary (now partially open)
  - Composite metric (bandwidth, delay, reliability, load)
  - DUAL (Diffusing Update Algorithm)
  - Fast convergence, supports multiple protocols

**Link State Protocols:**

- **OSPF (Open Shortest Path First)**:
  - Dijkstra's shortest path algorithm
  - Hierarchical design with areas
  - Link State Advertisements (LSAs)
  - Supports VLSM and route summarization
  - Version 2 (IPv4) and Version 3 (IPv6)

- **IS-IS (Intermediate System to Intermediate System)**:
  - OSI protocol adapted for IP
  - Similar to OSPF but more scalable
  - Used in large service provider networks
  - For detailed IS-IS configuration examples, see [IPv6 Workshop Guide](../docs/IPv6-Workshop-Guide.md)
  - For router commands, see [Configuration Cheatsheet](../docs/Configuration-Cheatsheet.md)

**Path Vector Protocol:**

- **BGP (Border Gateway Protocol)**:
  - Exterior Gateway Protocol (EGP) for the Internet
  - Path vector algorithm
  - AS (Autonomous System) based routing
  - Policy-based routing decisions
  - Versions: BGP-4 (IPv4), MP-BGP (multiprotocol, includes IPv6)

### 2.3 WAN Technologies

**Traditional WAN Technologies:**

1. **Leased Lines**:
   - Point-to-point dedicated connections
   - T1 (1.544 Mbps), T3 (44.736 Mbps)
   - E1 (2.048 Mbps), E3 (34.368 Mbps)
   - Predictable bandwidth, high cost

2. **Frame Relay**:
   - Packet-switched WAN technology
   - PVCs (Permanent Virtual Circuits)
   - Shared bandwidth, lower cost than leased lines
   - Largely replaced by MPLS

3. **ATM (Asynchronous Transfer Mode)**:
   - Cell-based switching (53-byte cells)
   - Supports voice, video, data
   - Used in some core networks
   - Complex, largely replaced by Ethernet

**Modern WAN Technologies:**

1. **MPLS (Multiprotocol Label Switching)**:
   - Label-based forwarding (covered in Expert section)
   - Combines benefits of layer 2 and layer 3
   - Used by service providers

2. **VPN (Virtual Private Network)**:
   - Encrypted tunnel over public network
   - Types:
     - **Site-to-Site VPN**: Connects networks
     - **Remote Access VPN**: Connects individual users
   - Protocols: IPsec, SSL/TLS, GRE

3. **SD-WAN (Software-Defined WAN)**:
   - Centralized management and control
   - Multiple transport options (MPLS, Internet, LTE)
   - Dynamic path selection
   - Application-aware routing

4. **Cellular Networks (4G/5G)**:
   - Mobile broadband connectivity
   - Backup or primary WAN link
   - Always-on connectivity

### 2.4 Wireless Networking

**Wi-Fi Standards:**

- **802.11a**: 5 GHz, up to 54 Mbps
- **802.11b**: 2.4 GHz, up to 11 Mbps
- **802.11g**: 2.4 GHz, up to 54 Mbps
- **802.11n (Wi-Fi 4)**: 2.4/5 GHz, up to 600 Mbps, MIMO
- **802.11ac (Wi-Fi 5)**: 5 GHz, up to 6.77 Gbps, MU-MIMO
- **802.11ax (Wi-Fi 6)**: 2.4/5/6 GHz, up to 9.6 Gbps, OFDMA, improved efficiency

**Wireless Security:**

- **WEP (Wired Equivalent Privacy)**: Insecure, deprecated
- **WPA (Wi-Fi Protected Access)**: Interim solution, uses TKIP
- **WPA2**: Uses AES encryption, widely deployed
- **WPA3**: Latest standard, improved security
  - Individual Data Encryption
  - Protection against brute-force attacks
  - Simplified IoT device security

**Wireless Architecture:**

- **Infrastructure Mode**: Devices connect through access point
- **Ad-Hoc Mode**: Direct device-to-device communication
- **Wireless Controller**: Centralized management of access points
- **Lightweight Access Points**: Managed by controller (CAPWAP protocol)

**Wireless Considerations:**

- Signal strength and coverage
- Interference (other Wi-Fi, Bluetooth, microwaves)
- Channel planning and selection
- Band steering (2.4 GHz vs 5 GHz)
- Power management (for mobile devices)

### 2.5 Quality of Service (QoS)

**QoS Concepts:**

- **Purpose**: Prioritize and manage network traffic to ensure performance
- **Key Metrics**:
  - **Bandwidth**: Available data rate
  - **Delay**: Time for packet to travel from source to destination
  - **Jitter**: Variation in delay
  - **Packet Loss**: Percentage of packets that don't reach destination

**QoS Models:**

1. **Best Effort**: No QoS, first-come-first-served
2. **Integrated Services (IntServ)**:
   - Per-flow resource reservation (RSVP)
   - Guaranteed service levels
   - Scalability limitations

3. **Differentiated Services (DiffServ)**:
   - Class-based service differentiation
   - DSCP (Differentiated Services Code Point) marking
   - Scalable and practical

**QoS Mechanisms:**

- **Classification**: Identify traffic types (ACLs, NBAR)
- **Marking**: Set priority (DSCP, CoS, IP precedence)
- **Policing**: Limit traffic rate, drop excess
- **Shaping**: Buffer and smooth traffic bursts
- **Congestion Management**: Queuing (FIFO, Priority, Weighted Fair, CBWFQ, LLQ)
- **Congestion Avoidance**: WRED (Weighted Random Early Detection)

**Application Priorities:**

- **Voice**: Highest priority, low latency/jitter requirements
- **Video**: High priority, bandwidth and jitter sensitive
- **Interactive Data**: Medium-high priority
- **Best Effort Data**: Medium priority
- **Scavenger**: Lowest priority

### 2.6 Network Address Translation (NAT)

**NAT Types:**

1. **Static NAT**: One-to-one mapping (private IP → public IP)
2. **Dynamic NAT**: Pool of public IPs, allocated on demand
3. **PAT (Port Address Translation) / NAT Overload**:
   - Multiple private IPs to single public IP
   - Uses port numbers to differentiate connections
   - Most common in home/SOHO networks

**NAT Terminology:**

- **Inside Local**: Private IP on internal network
- **Inside Global**: Public IP representing inside host
- **Outside Local**: IP of external host as seen from inside
- **Outside Global**: Public IP of external host

**NAT Benefits and Limitations:**

- Benefits: Conserves public IP addresses, hides internal network structure
- Limitations: Breaks some protocols, complicates troubleshooting, can cause performance issues

### 2.7 First Hop Redundancy Protocols

**Purpose**: Provide default gateway redundancy without manual configuration

**HSRP (Hot Standby Router Protocol)**:
- Cisco proprietary
- Virtual IP and MAC address
- Active/Standby routers
- Priority-based election
- Preemption enabled by default

**VRRP (Virtual Router Redundancy Protocol)**:
- Standards-based (RFC 3768)
- Similar to HSRP
- Master/Backup routers
- Can use real IP of master router

**GLBP (Gateway Load Balancing Protocol)**:
- Cisco proprietary
- Load balancing across multiple gateways
- Single virtual IP, multiple virtual MACs
- Active Virtual Forwarder (AVF) concept

---