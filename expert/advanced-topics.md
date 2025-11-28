# Expert Level Advanced Topics

**This section is part of the [Networking Principles Guide](../Networking-Principles.md)**

---

## Expert Level Advanced Topics

### 3.1 Advanced Routing Protocols

**OSPF Advanced Features:**

- **Area Types**:
  - Standard Area: Connects to area 0 (backbone)
  - Backbone Area (Area 0): Central area, all other areas connect to it
  - Stub Area: No external routes, default route advertised
  - Totally Stubby Area: No external or inter-area routes
  - NSSA (Not-So-Stubby Area): Allows ASBR within area
  - Totally NSSA: Combination of totally stubby and NSSA

- **LSA Types**:
  - Type 1: Router LSA (within area)
  - Type 2: Network LSA (within area)
  - Type 3: Summary LSA (inter-area)
  - Type 4: ASBR Summary LSA
  - Type 5: External LSA (from ASBR)
  - Type 7: NSSA External LSA

- **OSPFv3 (IPv6)**:
  - Link-local addresses for adjacencies
  - Multiple instances per interface
  - Address-family separation
  - For IPv6 configuration examples, see [IPv6 Workshop Guide](../docs/IPv6-Workshop-Guide.md)

**BGP Advanced Topics:**

- **Path Attributes**:
  - Well-known Mandatory: ORIGIN, AS_PATH, NEXT_HOP
  - Well-known Discretionary: LOCAL_PREF, ATOMIC_AGGREGATE
  - Optional Transitive: COMMUNITY, AGGREGATOR
  - Optional Non-transitive: MED (Multi-Exit Discriminator)

- **BGP Route Selection Process**:
  1. Highest Weight (Cisco)
  2. Highest Local Preference
  3. Prefer locally originated
  4. Shortest AS_PATH
  5. Lowest Origin code (IGP < EGP < Incomplete)
  6. Lowest MED
  7. Prefer eBGP over iBGP
  8. Lowest IGP metric to next hop
  9. Prefer oldest route (eBGP)
  10. Lowest router ID
  11. Shortest cluster list
  12. Lowest neighbor IP address

- **Route Reflectors and Confederations**:
  - **Route Reflectors**: Reduces full mesh requirement for iBGP
    - Client/Non-client relationships
    - Cluster ID for loop prevention
  - **Confederations**: Divides AS into sub-ASes
    - External and internal confederation peers

- **BGP Communities**:
  - Tags applied to routes for policy control
  - Well-known communities: NO_EXPORT, NO_ADVERTISE, LOCAL_AS
  - Custom communities for traffic engineering

- **Multihoming Strategies**:
  - Provider-dependent: Single or multiple ISPs
  - Provider-independent: Own ASN and IP space
  - Load balancing and redundancy considerations

### 3.2 MPLS (Multiprotocol Label Switching)

**MPLS Fundamentals:**

- **Purpose**: Fast packet forwarding using labels instead of IP lookup
- **Components**:
  - **Label Edge Router (LER)**: Adds/removes labels (Ingress/Egress)
  - **Label Switch Router (LSR)**: Forwards based on labels
  - **Label Distribution Protocol (LDP)**: Distributes labels

- **Label Structure**:
  - 20-bit label value
  - 3-bit traffic class (QoS)
  - 1-bit bottom of stack
  - 8-bit TTL

**MPLS Applications:**

1. **MPLS VPN (L3VPN)**:
   - Provider maintains separate routing tables (VRF) per customer
   - BGP distributes VPN routes
   - Label stack: Outer (transport) + Inner (VPN)
   - Full mesh connectivity with route reflectors

2. **MPLS Traffic Engineering (TE)**:
   - Explicit paths for traffic
   - RSVP-TE for label distribution
   - Constraint-based routing
   - Fast Reroute (FRR) for protection

3. **MPLS L2VPN**:
   - Layer 2 service emulation
   - Types: VPWS (Virtual Private Wire Service), VPLS (Virtual Private LAN Service)
   - Transparent Layer 2 connectivity

4. **Segment Routing (SR)**:
   - Source-routed tunnels
   - No signaling protocol needed
   - IPv6 extension (SRv6)
   - Simplified operations

**MPLS Advantages:**

- Fast forwarding (label swap vs IP lookup)
- Traffic engineering capabilities
- VPN services
- Scalability
- Unified infrastructure

### 3.3 Software-Defined Networking (SDN)

**SDN Architecture:**

- **Separation of Control and Data Planes**:
  - Control Plane: Routing decisions, policy
  - Data Plane: Packet forwarding
  - Centralized control, distributed forwarding

- **Components**:
  - **SDN Controller**: Centralized control logic
  - **Southbound APIs**: Communication with switches (OpenFlow)
  - **Northbound APIs**: Applications and services
  - **Network Operating System (NOS)**: Abstraction layer

**SDN Benefits:**

- Centralized management and control
- Programmability and automation
- Vendor independence
- Rapid innovation and deployment
- Improved resource utilization

**SDN Controllers:**

- OpenDaylight
- ONOS (Open Network Operating System)
- Cisco ACI
- VMware NSX
- Juniper Contrail

**OpenFlow Protocol:**

- Communication protocol between controller and switches
- Flow tables with match/action rules
- Versions: 1.0 through 1.5, evolving

**SDN Use Cases:**

- Data center networks
- WAN optimization (SD-WAN)
- Network virtualization
- Traffic engineering
- Security policy enforcement

### 3.4 Network Function Virtualization (NFV)

**NFV Concepts:**

- Decouples network functions from dedicated hardware
- Runs network functions as software on commodity hardware
- Virtualized network appliances (vFirewall, vRouter, vLoad Balancer)

**NFV Architecture:**

- **Virtualized Network Functions (VNFs)**: Software implementations of network functions
- **NFV Infrastructure (NFVI)**: Compute, storage, network resources
- **Management and Orchestration (MANO)**:
  - NFV Orchestrator (NFVO)
  - VNF Manager (VNFM)
  - Virtual Infrastructure Manager (VIM)

**NFV Benefits:**

- Reduced CAPEX and OPEX
- Faster service deployment
- Scalability and elasticity
- Vendor independence
- Innovation acceleration

**NFV vs SDN:**

- **NFV**: Virtualizes network functions
- **SDN**: Separates control and data planes
- Complementary technologies

### 3.5 Network Virtualization

**VRF (Virtual Routing and Forwarding):**

- Multiple routing tables on single router
- Isolation between routing instances
- Used in MPLS VPNs and network segmentation
- Separate routing table per VRF

**VXLAN (Virtual eXtensible LAN):**

- Layer 2 overlay over Layer 3 network
- 24-bit VNI (VXLAN Network Identifier)
- UDP encapsulation (port 4789)
- MAC-in-UDP tunneling
- Used in data centers and cloud environments

**EVPN (Ethernet VPN):**

- BGP-based control plane for Layer 2/3 VPNs
- Combines benefits of L2 and L3 VPNs
- Supports multihoming and load balancing
- Uses MPLS or VXLAN encapsulation

**Overlay Networks:**

- Logical network built on top of physical network
- Decouples logical topology from physical topology
- Examples: VXLAN, NVGRE, STT
- Enables network virtualization and multi-tenancy

---