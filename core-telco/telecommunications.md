# Core Telecommunications Networking

**This section is part of the [Networking Principles Guide](../Networking-Principles.md)**

---

## Core Telecommunications Networking

### 4.1 Telecom Network Architecture

**Network Hierarchy:**

- **Access Network (RAN)**: Connects end users to network
- **Transport Network**: Backhaul and aggregation
- **Core Network**: Central switching and routing
- **Service Layer**: Applications and services

**Radio Access Network (RAN):**

- **Cellular Networks**:
  - 2G: GSM, CDMA
  - 3G: UMTS, CDMA2000
  - 4G LTE: OFDMA, MIMO
  - 5G NR: mmWave, massive MIMO, network slicing

- **Cell Types**:
  - Macrocell: Large coverage area (1-30 km)
  - Microcell: Urban coverage (0.2-2 km)
  - Picocell: Indoor/small area (0.1-0.2 km)
  - Femtocell: Home/office (10-50 m)

- **Base Station Components**:
  - Antennas and transceivers
  - Baseband processing
  - Backhaul connectivity

**Core Network Evolution:**

- **Circuit-Switched (CS) Core**: Voice networks (2G/3G)
- **Packet-Switched (PS) Core**: Data networks
  - 3G: SGSN, GGSN
  - 4G: EPC (Evolved Packet Core)
    - MME (Mobility Management Entity)
    - S-GW (Serving Gateway)
    - P-GW (Packet Data Network Gateway)
    - HSS (Home Subscriber Server)
  - 5G: 5GC (5G Core)
    - AMF (Access and Mobility Management)
    - SMF (Session Management Function)
    - UPF (User Plane Function)
    - NRF (Network Repository Function)

**Transport Network:**

- **Backhaul**: From base stations to core
  - Microwave links
  - Fiber optic
  - Ethernet/IP transport

- **Backbone**: Between core network elements
  - High-capacity fiber networks
  - DWDM (Dense Wavelength Division Multiplexing)
  - OTN (Optical Transport Network)

### 4.2 Telecom Protocols and Technologies

**Signaling Protocols:**

- **SS7 (Signaling System 7)**: Circuit-switched signaling
  - MTP (Message Transfer Part)
  - SCCP (Signaling Connection Control Part)
  - ISUP (ISDN User Part)
  - TCAP (Transaction Capabilities Application Part)

- **Diameter**: Authentication, authorization, accounting
  - Used in 4G/5G networks
  - Evolved from RADIUS

- **SIP (Session Initiation Protocol)**: VoIP signaling
  - IMS (IP Multimedia Subsystem) component
  - Call setup, modification, teardown

**Transport Technologies:**

- **DWDM (Dense Wavelength Division Multiplexing)**:
  - Multiple wavelengths on single fiber
  - 40+ channels, up to 160+
  - Long-haul transmission

- **SONET/SDH (Synchronous Optical Network / Synchronous Digital Hierarchy)**:
  - TDM-based optical transmission
  - Ring topologies for protection
  - Legacy technology, being replaced by packet-based transport

- **Ethernet in Transport**:
  - Carrier Ethernet
  - E-Line, E-LAN, E-Tree services
  - MEF (Metro Ethernet Forum) standards

**5G Technologies:**

- **Network Slicing**: Virtual networks for different use cases
- **Edge Computing**: Processing at network edge
- **Massive MIMO**: Large antenna arrays
- **Beamforming**: Directional signal transmission
- **mmWave**: High-frequency bands for capacity
- **URLLC**: Ultra-reliable low-latency communication

### 4.3 Service Provider Architectures

**ISP Network Architecture:**

- **Points of Presence (PoPs)**: Network interconnection points
- **Internet Exchange Points (IXPs)**: Peering locations
- **Autonomous Systems (AS)**: Networks under single administrative control
- **BGP Peering**: eBGP connections between ASes
  - Transit: Paid connectivity
  - Peering: Free mutual exchange

**Content Delivery Networks (CDNs):**

- Distributed servers for content delivery
- Reduces latency and bandwidth usage
- Edge servers closer to users
- Examples: Akamai, Cloudflare, AWS CloudFront

**Network Operations:**

- **Network Operations Center (NOC)**: 24/7 monitoring
- **Fault Management**: Detection, isolation, resolution
- **Performance Management**: Monitoring, optimization
- **Configuration Management**: Change control
- **Security Management**: Threat detection, response

---