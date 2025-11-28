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

- **Spanning Tree Protocol (STP)**:
  - Prevents loops in switched networks
  - Protocol: IEEE 802.1D
  - States: Blocking, Listening, Learning, Forwarding, Disabled
  - Enhanced versions: RSTP (Rapid STP), MSTP (Multiple STP)

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