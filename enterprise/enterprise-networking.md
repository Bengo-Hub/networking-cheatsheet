# Enterprise Networking

**This section is part of the [Networking Principles Guide](../Networking-Principles.md)**

---

## Enterprise Networking

### 5.1 Enterprise Network Design

**Hierarchical Design Model:**

- **Access Layer**: End device connectivity
  - Port security
  - VLAN assignment
  - Power over Ethernet (PoE)
  - Wireless access points

- **Distribution Layer**: Aggregation and policy
  - Route summarization
  - Security policies
  - QoS marking
  - Redundancy

- **Core Layer**: High-speed backbone
  - Fast switching
  - Redundancy and resiliency
  - Minimal processing (routing, not filtering)

**Modular Design:**

- **Campus Design**: Access, distribution, core
- **Data Center Design**: Spine-leaf architecture
- **WAN Design**: Hub-and-spoke, full mesh, partial mesh
- **Branch Design**: Simplified connectivity

**Redundancy and High Availability:**

- **Device Redundancy**: Dual power supplies, redundant supervisors
- **Link Redundancy**: EtherChannel, redundant paths
- **Path Redundancy**: Multiple routes, load balancing
- **Protocol Redundancy**: FHRP (HSRP/VRRP/GLBP)

### 5.2 Enterprise Routing

**EIGRP in Enterprise:**

- Fast convergence
- Support for multiple protocols (IPv4, IPv6, IPX, AppleTalk)
- Unequal cost load balancing (variance)
- Query process for route updates
- Stub routing for branch offices

**OSPF in Enterprise:**

- Area design for scalability
- Route summarization at area boundaries
- Virtual links for non-contiguous backbone
- OSPFv3 for IPv6
- Authentication (plain text, MD5, SHA)

**BGP in Enterprise:**

- Multihoming scenarios
- Policy-based routing
- Route filtering (prefix lists, AS path filters)
- Communities for traffic engineering
- Local preference and MED manipulation

### 5.3 Enterprise Switching

**Advanced Switching Features:**

- **Port Security**: MAC address limiting
- **DHCP Snooping**: Prevents rogue DHCP servers
- **Dynamic ARP Inspection**: Validates ARP packets
- **IP Source Guard**: Validates source IP addresses
- **Storm Control**: Limits broadcast/multicast/unicast storms

**VLAN Design:**

- End-to-end VLANs: Span multiple switches
- Local VLANs: Per access switch
- Voice VLANs: Separate VLAN for IP phones
- Management VLANs: Out-of-band management

**EtherChannel Best Practices:**

- Layer 2 EtherChannel: Switch-to-switch
- Layer 3 EtherChannel: Router-to-router
- Load balancing methods (src-dst-ip, src-dst-mac, etc.)
- PAgP vs LACP

### 5.4 Enterprise Security

**Access Control:**

- **AAA Framework**: Authentication, Authorization, Accounting
  - RADIUS: Remote Authentication Dial-In User Service
  - TACACS+: Terminal Access Controller Access-Control System Plus
- **802.1X**: Port-based network access control
  - Supplicant, Authenticator, Authentication Server
  - EAP methods (PEAP, EAP-TLS, EAP-FAST)

**Firewall Technologies:**

- **Stateful Firewalls**: Track connection state
- **Application Layer Gateways**: Deep packet inspection
- **Next-Generation Firewalls (NGFW)**: Application awareness, IPS
- **Web Application Firewalls (WAF)**: Protect web applications

**Intrusion Detection and Prevention:**

- **IDS**: Passive monitoring, alerting
- **IPS**: Active blocking of threats
- **Signature-based**: Known threat patterns
- **Anomaly-based**: Behavioral analysis

**Network Segmentation:**

- **DMZ**: Demilitarized zone for public servers
- **Internal Segmentation**: Department/function-based
- **Zero Trust**: Verify all access, trust nothing

### 5.5 Enterprise Wireless

**Wireless Design:**

- **Site Survey**: Coverage and capacity planning
- **AP Placement**: Optimal location for coverage
- **Channel Planning**: Minimize interference
- **Power Levels**: Balance coverage and interference
- **Roaming**: Seamless handoff between APs

**Wireless Controllers:**

- Centralized management
- WLAN configuration
- Radio resource management
- Guest access
- Captive portals

**Wireless Security:**

- WPA3 Enterprise
- 802.1X authentication
- Certificate-based authentication
- Guest network isolation
- Wireless intrusion detection

### 5.6 Network Automation

**Automation Tools:**

- **Ansible**: Configuration management and automation
- **Python**: Scripting and programmability
- **NETCONF/YANG**: Network configuration protocol
- **REST APIs**: HTTP-based network configuration
- **SNMP**: Monitoring and management

**Infrastructure as Code (IaC):**

- Version-controlled configurations
- Repeatable deployments
- Configuration templates
- Automated testing

**Network Programmability:**

- **Cisco**: NETCONF, RESTCONF, pyATS
- **Juniper**: NETCONF, PyEZ
- **Aruba**: REST APIs
- **Multi-vendor**: Ansible, Nornir

---