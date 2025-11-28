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

**Detailed 5G Core Network Functions:**

**5G Core (5GC) Network Functions:**

1. **AMF (Access and Mobility Management Function)**:
   - Manages connection and mobility
   - Handles registration, connection management
   - Interacts with UE (User Equipment) and RAN

2. **SMF (Session Management Function)**:
   - Manages PDU sessions
   - IP address allocation
   - QoS policy enforcement

3. **UPF (User Plane Function)**:
   - Packet routing and forwarding
   - Anchor point for mobility
   - Traffic measurement and reporting

4. **UDM (Unified Data Management)**:
   - Subscriber data management
   - Authentication credentials
   - Service authorization

5. **AUSF (Authentication Server Function)**:
   - Authentication services
   - 5G authentication key generation

6. **NRF (Network Repository Function)**:
   - Service discovery
   - NF registration and discovery

**Service-Based Architecture (SBA):**
- All NFs communicate via HTTP/2 REST APIs
- Stateless design for scalability
- Network slicing support

**Transport Network Details:**

**DWDM Systems:**
- **Channels**: 40, 80, 160+ channels
- **Channel Spacing**: 50 GHz, 100 GHz
- **Speeds**: 10G, 40G, 100G, 400G per wavelength
- **Range**: Long-haul (1000+ km), metro (80 km)
- **Amplification**: EDFA (Erbium-Doped Fiber Amplifier)

**Optical Transport Network (OTN) - ITU-T G.709:**
- Wrapper technology for transparent transport
- ODU (Optical Data Unit) hierarchy:
  - ODU0: 1.25 Gbps
  - ODU1: 2.5 Gbps
  - ODU2: 10 Gbps
  - ODU3: 40 Gbps
  - ODU4: 100 Gbps
  - ODUflex: Flexible rate

**Carrier Ethernet Services (MEF Standards):**

- **E-Line**: Point-to-point service
  - EPL (Ethernet Private Line)
  - EVPL (Ethernet Virtual Private Line)

- **E-LAN**: Multipoint-to-multipoint service
  - EPLAN (Ethernet Private LAN)
  - EVPLAN (Ethernet Virtual Private LAN)

- **E-Tree**: Rooted multipoint service
  - EP-Tree (Ethernet Private Tree)
  - EVP-Tree (Ethernet Virtual Private Tree)

---

## References

**Telecommunications Standards:**
- **3GPP Specifications**: https://www.3gpp.org/specifications
- **ITU-T Recommendations**: https://www.itu.int/itu-t/recommendations/
- **IEEE 802 Standards**: https://standards.ieee.org/standard/

**5G Standards:**
- **3GPP TS 23.501**: System Architecture for 5G System
- **3GPP TS 23.502**: Procedures for 5G System
- **3GPP TS 29.500**: 5G System; Technical Realization of Service Based Architecture

**Transport Technologies:**
- **ITU-T G.709**: Interfaces for Optical Transport Network (OTN)
- **ITU-T G.872**: Architecture of Optical Transport Networks
- **MEF Standards**: https://www.mef.net/standards-technical-specifications/

**Signaling Protocols:**
- **RFC 3261**: SIP: Session Initiation Protocol
- **RFC 6733**: Diameter Base Protocol
- **ITU-T Q.700**: Introduction to CCITT Signaling System No. 7

**Trusted Resources:**
- **3GPP**: https://www.3gpp.org/
- **ITU-T**: https://www.itu.int/en/ITU-T/Pages/default.aspx
- **IEEE Standards Association**: https://standards.ieee.org/
- **MEF (Metro Ethernet Forum)**: https://www.mef.net/

---