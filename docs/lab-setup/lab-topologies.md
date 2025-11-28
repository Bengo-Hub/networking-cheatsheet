# Network Topology Examples for Virtual Labs

**This section is part of the [Virtual Lab Setup Guide](../Virtual-Lab-Setup-Guide.md)**

---

## Network Topology Examples

### Core Telecommunications Lab Setup

#### Lab Topology Overview

**Core Telco Lab Components:**
- Service Provider Routers (BGP, MPLS)
- Core Switches (high-speed switching)
- Edge Routers (customer-facing)
- Transport Network Simulation
- Customer Premises Equipment (CPE)

#### Proxmox Setup for Core Telco Lab

**Network Configuration:**

```bash
# /etc/network/interfaces
auto vmbr0
iface vmbr0 inet static
    address 192.168.100.10/24
    gateway 192.168.100.1
    bridge-ports enp3s0
    bridge-stp off
    bridge-fd 0

# Core network (MPLS backbone)
auto vmbr1
iface vmbr1 inet manual
    bridge-ports none
    bridge-stp off
    bridge-fd 0

# Customer networks
auto vmbr2
iface vmbr2 inet manual
    bridge-ports none
    bridge-stp off
    bridge-fd 0
```

#### Core Telco Lab Topology

**Physical Topology:**
```
Internet
   |
[P-RTR-01]---[P-RTR-02]
   |            |
[PE-RTR-01]  [PE-RTR-02]
   |            |
[CE-RTR-01]  [CE-RTR-02]
   |            |
[Customer Networks]
```

**VyOS Configuration Examples:**

**P-RTR-01 (Provider Core Router):**
```vyos
# Configure interfaces
set interfaces ethernet eth0 address '10.0.0.1/30'
set interfaces ethernet eth1 address '10.0.0.5/30'
set interfaces loopback lo address '1.1.1.1/32'

# Configure IS-IS (or OSPF)
set protocols isis net '49.0001.0001.0001.0001.00'
set protocols isis interface eth0
set protocols isis interface eth1
set protocols isis interface lo passive

# Configure MPLS
set protocols mpls interface eth0
set protocols mpls interface eth1

# Configure LDP
set protocols ldp interface eth0
set protocols ldp interface eth1
```

**PE-RTR-01 (Provider Edge Router):**
```vyos
# Configure MPLS VPN
set protocols bgp address-family ipv4-vpn
set protocols bgp neighbor 1.1.1.1 remote-as 65000
set protocols bgp neighbor 1.1.1.1 update-source lo
set protocols bgp neighbor 1.1.1.1 address-family ipv4-vpn

# Configure VRF for customer
set vrf name CUSTOMER-A table '100'
set vrf name CUSTOMER-A protocols bgp address-family ipv4-unicast
set vrf name CUSTOMER-A protocols bgp address-family ipv4-unicast export vpn-export
set vrf name CUSTOMER-A protocols bgp address-family ipv4-unicast import vpn-import
```

**Testing Core Telco Lab:**
```bash
# On VyOS routers
show ip route
show ip route isis
show mpls ldp neighbor
show bgp summary
show bgp vpnv4 unicast
ping 1.1.1.1 source 1.1.1.2
```

For detailed MPLS and BGP configuration, see: [Advanced Routing Topics](../../expert/advanced-topics.md)

---

### Enterprise Network Lab Setup

#### Lab Topology Overview

**Enterprise Lab Components:**
- Core Switches (high-speed backbone)
- Distribution Switches (aggregation)
- Access Switches (end device connectivity)
- Routers (WAN connectivity, inter-VLAN routing)
- Firewalls (security policies)
- Servers (DNS, DHCP, file servers)
- End Devices (workstations, printers, IP phones)

#### VMware Setup for Enterprise Lab

**VMware Network Configuration:**

Create custom VMnets:
- **VMnet10**: Management VLAN (192.168.10.0/24)
- **VMnet11**: Core Network (10.0.0.0/24)
- **VMnet12**: Distribution Network (10.0.1.0/24)
- **VMnet13**: Access Network - Sales (192.168.20.0/24)
- **VMnet14**: Access Network - Engineering (192.168.30.0/24)
- **VMnet15**: Access Network - Guest (192.168.40.0/24)
- **VMnet16**: WAN Simulation (203.0.113.0/24)

#### Enterprise Lab Topology

**Three-Tier Hierarchical Design:**

```
                    [Internet]
                       |
                  [Firewall]
                       |
              [Core Switch-01]
              /            \
    [Dist-SW-01]      [Dist-SW-02]
         |                  |
    [Access-SW-01]    [Access-SW-02]
         |                  |
    [Workstations]    [Servers]
```

**VyOS Router Configuration (Core Router):**

```vyos
# Configure interfaces
set interfaces ethernet eth0 address '10.0.0.1/24'
set interfaces ethernet eth1 address '10.0.1.1/24'
set interfaces ethernet eth2 address '203.0.113.2/30'
set interfaces loopback lo address '192.168.1.1/32'

# Configure OSPF
set protocols ospf area 0 network '10.0.0.0/16'
set protocols ospf area 0 network '192.168.1.1/32'

# Configure BGP for internet connectivity
set protocols bgp 65001 neighbor 203.0.113.1 remote-as 65000
set protocols bgp 65001 network '192.168.0.0/16'
```

**Open vSwitch Configuration (Access Switch):**

```bash
# Create bridge
sudo ovs-vsctl add-br br0

# Add ports
sudo ovs-vsctl add-port br0 eth1 tag=20  # Sales VLAN
sudo ovs-vsctl add-port br0 eth2 tag=30  # Engineering VLAN
sudo ovs-vsctl add-port br0 eth3 tag=40  # Guest VLAN

# Configure trunk port
sudo ovs-vsctl add-port br0 eth0 trunks=20,30,40

# Enable STP
sudo ovs-vsctl set bridge br0 stp_enable=true
```

**pfSense Firewall Configuration:**

1. Access web UI: https://192.168.1.1
2. Initial setup wizard
3. Configure interfaces:
   - WAN: 203.0.113.2/30
   - LAN: 10.0.0.254/24
   - OPT1: 10.0.1.254/24
4. Configure firewall rules:
   - Allow LAN to WAN
   - Block WAN to LAN (except established)
   - Allow inter-VLAN as needed

For detailed VLAN and switching configuration, see: [Intermediate Concepts](../../intermediate/concepts.md)

#### Enterprise Services Setup

**DHCP Server (Ubuntu VM):**

```bash
# Install DHCP server
sudo apt install isc-dhcp-server

# Configure /etc/dhcp/dhcpd.conf
subnet 192.168.20.0 netmask 255.255.255.0 {
  range 192.168.20.100 192.168.20.200;
  option routers 192.168.20.1;
  option domain-name-servers 8.8.8.8, 1.1.1.1;
  option domain-name "company.local";
}

# Start service
sudo systemctl start isc-dhcp-server
```

**DNS Server (Ubuntu VM with BIND9):**

```bash
# Install BIND9
sudo apt install bind9

# Configure /etc/bind/named.conf.local
zone "company.local" {
    type master;
    file "/etc/bind/db.company.local";
}

# Create zone file
# Start service
sudo systemctl start bind9
```

For detailed enterprise networking, see: [Enterprise Networking](../../enterprise/enterprise-networking.md)

---

### End-User Network Lab Setup

#### Lab Topology Overview

**End-User Lab Components:**
- Home Router/Gateway
- Access Point (Wi-Fi simulation)
- End Devices (laptops, phones, IoT devices)
- Internet Gateway (ISP simulation)

#### Simple Home Network Lab

**Topology:**
```
[Internet/ISP]
    |
[Home Router] (VyOS or pfSense)
    |
[Switch] (Open vSwitch or simple bridge)
    |
[Devices] (Ubuntu VMs)
```

**Home Router Configuration (VyOS):**

```vyos
# WAN interface (to internet)
set interfaces ethernet eth0 address dhcp
set interfaces ethernet eth0 description 'WAN'

# LAN interface
set interfaces ethernet eth1 address '192.168.1.1/24'
set interfaces ethernet eth1 description 'LAN'

# Configure NAT
set nat source rule 100 outbound-interface eth0
set nat source rule 100 source address '192.168.1.0/24'
set nat source rule 100 translation address masquerade

# Configure DHCP server
set service dhcp-server shared-network-name LAN subnet 192.168.1.0/24 default-router '192.168.1.1'
set service dhcp-server shared-network-name LAN subnet 192.168.1.0/24 dns-server '8.8.8.8'
set service dhcp-server shared-network-name LAN subnet 192.168.1.0/24 range 0 start '192.168.1.100'
set service dhcp-server shared-network-name LAN subnet 192.168.1.0/24 range 0 stop '192.168.1.200'

# Configure firewall
set firewall name WAN_IN default-action 'drop'
set firewall name WAN_IN rule 10 action 'accept'
set firewall name WAN_IN rule 10 state established 'enable'
set firewall name WAN_IN rule 10 state related 'enable'

set interfaces ethernet eth0 firewall in name 'WAN_IN'
```

**ISP Simulation Router (VyOS):**

```vyos
# Configure as internet gateway
set interfaces ethernet eth0 address '203.0.113.1/30'
set interfaces ethernet eth1 address '8.8.8.1/24'  # Simulated internet

# Configure NAT for customers
set nat source rule 100 outbound-interface eth1
set nat source rule 100 source address '203.0.113.0/30'
set nat source rule 100 translation address masquerade

# Configure default route (simulated)
set protocols static route 0.0.0.0/0 next-hop 8.8.8.254
```

#### IoT Network Lab

**Topology with IoT Segmentation:**

```
[Internet]
    |
[Router] (VyOS)
    |
[Switch]
    /    |    \
[LAN] [IoT] [Guest]
```

**VyOS Router with IoT VLAN:**

```vyos
# Configure VLANs
set interfaces ethernet eth1 vif 10 address '192.168.1.1/24'  # Main LAN
set interfaces ethernet eth1 vif 20 address '192.168.20.1/24'  # IoT VLAN
set interfaces ethernet eth1 vif 30 address '192.168.30.1/24'  # Guest VLAN

# Firewall rules to isolate IoT
set firewall name IoT_IN default-action 'drop'
set firewall name IoT_IN rule 10 action 'accept'
set firewall name IoT_IN rule 10 destination address '192.168.1.100'  # Allow to server only
set firewall name IoT_IN rule 10 protocol 'tcp'
set firewall name IoT_IN rule 10 destination port '443'

set interfaces ethernet eth1 vif 20 firewall in name 'IoT_IN'
```

For detailed end-user networking, see: [End-User Networking](../../end-user/end-user-networking.md)

---

### Lab Size Examples

#### Small Enterprise Lab (VMware)

**Components:**
- 2 Routers (VyOS)
- 2 Switches (Open vSwitch)
- 1 Firewall (pfSense)
- 3 End Devices (Ubuntu)

**Resource Requirements:**
- Total RAM: ~8 GB
- Total Storage: ~30 GB
- Total vCPUs: ~10

**Network Configuration:**
- VMnet10: Management (192.168.10.0/24)
- VMnet11: Core (10.0.0.0/24)
- VMnet12: Users (192.168.20.0/24)

#### Service Provider Lab (Proxmox)

**Components:**
- 4 Provider Routers (VyOS)
- 2 Customer Edge Routers (VyOS)
- 2 Customer Networks (Ubuntu VMs)

**Resource Requirements:**
- Total RAM: ~6 GB
- Total Storage: ~20 GB
- Total vCPUs: ~12

**MPLS VPN Configuration:**
- Provider routers run IS-IS and MPLS
- PE routers run BGP VPNv4
- Customer routers connect via VRF

#### Complete Lab Environment

**Full Enterprise + Service Provider:**

**Proxmox Setup:**
- 1 Proxmox host
- Multiple VMs:
  - 6 Routers (VyOS)
  - 4 Switches (Open vSwitch)
  - 2 Firewalls (pfSense)
  - 10 End Devices (Ubuntu)
  - 2 Servers (Ubuntu with services)

**Resource Requirements:**
- Total RAM: ~32 GB
- Total Storage: ~150 GB
- Total vCPUs: ~40

---

## Related Documentation

- For hardware requirements, see: [Hardware Requirements](hardware-requirements.md)
- For router configuration, see: [Configuration Cheatsheet](../Configuration-Cheatsheet.md)
- For IPv6 lab setup, see: [IPv6 Workshop Guide](../IPv6-Workshop-Guide.md)
- For troubleshooting, see: [Troubleshooting Virtual Labs](troubleshooting.md)

