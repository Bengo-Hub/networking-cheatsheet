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

**Port Security Configuration (Cisco):**

```cisco
! Enable port security
interface GigabitEthernet0/1
  switchport mode access
  switchport port-security
  switchport port-security maximum 5
  switchport port-security violation restrict
  switchport port-security mac-address sticky
  
! View port security status
show port-security
show port-security address
show port-security interface Gi0/1
```

**Port Security Violation Actions:**
- **Protect**: Drop unauthorized frames, no logging
- **Restrict**: Drop frames and increment violation counter
- **Shutdown**: Shut down port (err-disable state)

**DHCP Snooping Configuration:**

```cisco
! Enable DHCP snooping globally
ip dhcp snooping
ip dhcp snooping vlan 10,20

! Trust uplink to legitimate DHCP server
interface GigabitEthernet0/24
  ip dhcp snooping trust
  
! View DHCP snooping bindings
show ip dhcp snooping binding
show ip dhcp snooping statistics
```

**Dynamic ARP Inspection (DAI) Configuration:**

```cisco
! Enable DAI on VLANs
ip arp inspection vlan 10,20

! Trust interfaces (uplinks)
interface GigabitEthernet0/24
  ip arp inspection trust
  
! Configure rate limiting
ip arp inspection limit rate 15 burst interval 1
  
! View DAI statistics
show ip arp inspection
show ip arp inspection statistics
```

**IP Source Guard Configuration:**

```cisco
! Enable IP Source Guard
interface GigabitEthernet0/1
  ip verify source
  ip verify source port-security  ! Use MAC binding table
```

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

**AAA Configuration (Cisco):**

```cisco
! Configure RADIUS server
aaa new-model
aaa authentication login default group radius local
aaa authorization exec default group radius local
aaa accounting exec default start-stop group radius

! RADIUS server settings
radius server RADIUS-SERVER
  address ipv4 192.168.100.10 auth-port 1812 acct-port 1813
  key MySecretKey

! TACACS+ server settings
tacacs server TACACS-SERVER
  address ipv4 192.168.100.20
  key MySecretKey

aaa authentication login TACACS group tacacs+ local
aaa authorization commands 15 TACACS group tacacs+ local
```

**802.1X Configuration:**

```cisco
! Enable 802.1X globally
dot1x system-auth-control

! Configure 802.1X on interface
interface GigabitEthernet0/1
  switchport mode access
  authentication port-control auto
  dot1x pae authenticator
  
! View 802.1X status
show dot1x all
show dot1x interface Gi0/1
show dot1x statistics
```

**802.1X Components:**
- **Supplicant**: Client device requesting network access
- **Authenticator**: Switch/access point enforcing access control
- **Authentication Server**: RADIUS server validating credentials

**EAP Methods:**
- **PEAP (Protected EAP)**: Microsoft, password-based
- **EAP-TLS**: Certificate-based, most secure
- **EAP-FAST**: Cisco, flexible authentication

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

**Network Automation Examples:**

**Ansible Playbook Example:**
```yaml
---
- name: Configure OSPF on routers
  hosts: routers
  tasks:
    - name: Enable OSPF
      cisco.ios.ios_ospf:
        state: present
        process_id: 1
        router_id: "{{ ansible_host }}"
        networks:
          - prefix: 192.168.1.0
            mask: 255.255.255.0
            area: 0
```

**Python NETCONF Example:**
```python
from ncclient import manager

with manager.connect(
    host='192.168.1.1',
    port=830,
    username='admin',
    password='password',
    hostkey_verify=False
) as m:
    # Get configuration
    config = m.get_config(source='running')
    
    # Edit configuration
    config_xml = """
    <config>
      <interfaces xmlns="urn:ietf:params:xml:ns:yang:ietf-interfaces">
        <interface>
          <name>GigabitEthernet0/0</name>
          <ipv4 xmlns="urn:ietf:params:xml:ns:yang:ietf-ip">
            <address>
              <ip>192.168.1.1</ip>
              <netmask>255.255.255.0</netmask>
            </address>
          </ipv4>
        </interface>
      </interfaces>
    </config>
    """
    m.edit_config(target='running', config=config_xml)
```

**SNMP Configuration:**
```cisco
! Enable SNMP
snmp-server community public RO
snmp-server community private RW
snmp-server location "Data Center 1"
snmp-server contact "admin@company.com"

! SNMPv3 (secure)
snmp-server user admin admin-group v3 auth sha MyAuthKey priv aes 128 MyPrivKey
snmp-server group admin-group v3 priv
snmp-server view admin-view internet included

! SNMP traps
snmp-server host 192.168.100.10 version 2c public
snmp-server enable traps
```

**SNMP Query Examples:**
```bash
# Get system description
snmpget -v2c -c public 192.168.1.1 1.3.6.1.2.1.1.1.0

# Walk interface table
snmpwalk -v2c -c public 192.168.1.1 1.3.6.1.2.1.2.2.1.2

# Get interface statistics
snmpget -v2c -c public 192.168.1.1 1.3.6.1.2.1.2.2.1.10.1  # InOctets
```

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

## References

**Enterprise Network Design:**
- **Cisco Enterprise Architecture**: https://www.cisco.com/c/en/us/td/docs/solutions/Enterprise/Campus/campover.html
- **RFC 5412**: Light-Weight Access Point Protocol (CAPWAP)

**Network Automation:**
- **Ansible Network Modules**: https://docs.ansible.com/ansible/latest/network/
- **NETCONF RFC 6241**: Network Configuration Protocol
- **YANG RFC 7950**: The YANG 1.1 Data Modeling Language
- **SNMP RFC 3410-3418**: SNMPv3 specifications

**Security Standards:**
- **802.1X**: Port-Based Network Access Control
- **RADIUS RFC 2865**: Remote Authentication Dial In User Service
- **TACACS+**: Terminal Access Controller Access-Control System Plus

---