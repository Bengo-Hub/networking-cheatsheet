# IPv6 Migration Tools and Software

**This section is part of the [Virtual Lab Setup Guide](../Virtual-Lab-Setup-Guide.md)**

---

## IPv6 Migration Tools and Software

This section covers open-source tools and software for IPv6 migration, transition mechanisms, and testing. For comprehensive IPv6 implementation guidance, see the [IPv6 Workshop Guide](../IPv6-Workshop-Guide.md).

### IPv6 Transition Mechanisms

#### 1. Jool (NAT64 and SIIT)

**Jool** is a stateful NAT64 and stateless SIIT (Stateless IP/ICMP Translation) implementation for Linux.

**Features:**
- **NAT64**: Translates IPv6 packets to IPv4 and vice versa
- **SIIT**: Stateless translation (no connection tracking)
- **DNS64**: Can work with DNS64 servers
- **High Performance**: Kernel-based implementation

**Installation (Ubuntu/Debian):**
```bash
# Add Jool repository
sudo add-apt-repository ppa:nicmx/jool
sudo apt update
sudo apt install jool-dkms jool-tools

# Load kernel module
sudo modprobe jool
```

**NAT64 Configuration:**
```bash
# Create NAT64 instance
sudo jool instance add "nat64" --netfilter --pool6 64:ff9b::/96

# Add IPv4 pool
sudo jool pool4 add "nat64" --tcp 192.0.2.1-192.0.2.10 60000-61000
sudo jool pool4 add "nat64" --udp 192.0.2.1-192.0.2.10 60000-61000
sudo jool pool4 add "nat64" --icmp 192.0.2.1-192.0.2.10

# Enable NAT64
sudo jool -i nat64 --enable

# Verify status
sudo jool -i nat64 --display
```

**SIIT Configuration:**
```bash
# Create SIIT instance
sudo jool instance add "siit" --netfilter

# Configure EAM (Explicit Address Mapping)
sudo jool -i siit eamt add 2001:db8::/32 192.0.2.0/24

# Enable SIIT
sudo jool -i siit --enable
```

**Resources:**
- **Official Website**: https://www.jool.mx/
- **GitHub**: https://github.com/NICMx/Jool
- **Documentation**: https://www.jool.mx/en/documentation.html
- **RFC 6146**: Stateful NAT64
- **RFC 7915**: IP/ICMP Translation Algorithm (SIIT)

#### 2. TAYGA (NAT64)

**TAYGA** is a user-space NAT64 implementation for Linux.

**Features:**
- Simple configuration
- Works with any Linux distribution
- Good for testing and small deployments

**Installation:**
```bash
# Ubuntu/Debian
sudo apt install tayga

# Or compile from source
git clone https://github.com/fwdillema/tayga.git
cd tayga
./configure
make
sudo make install
```

**Configuration:**
```bash
# Edit /etc/tayga.conf
tun-device nat64
ipv4-addr 192.0.2.1
prefix 2001:db8:1::/96
dynamic-pool 192.0.2.128/25
```

**Start TAYGA:**
```bash
sudo tayga -c /etc/tayga.conf
```

**Resources:**
- **GitHub**: https://github.com/fwdillema/tayga
- **RFC 6146**: Stateful NAT64

#### 3. 464XLAT

**464XLAT** provides IPv4 connectivity to IPv6-only clients using CLAT (Customer-side Translator) and PLAT (Provider-side Translator).

**Components:**
- **CLAT**: Client-side translator (on end device)
- **PLAT**: Provider-side translator (NAT64 gateway)

**CLAT Configuration (Linux):**
```bash
# Install clatd
sudo apt install clatd

# Configure /etc/clatd.conf
clat-v6-addr: 2001:db8::1
clat-v4-addr: 192.0.2.1
clat-v4-prefix: 192.0.2.0/24
```

**Resources:**
- **RFC 6877**: 464XLAT
- **clatd**: https://github.com/toreanderson/clatd

#### 4. MAP-T (Mapping of Address and Port with Translation)

**MAP-T** is a stateless IPv4-IPv6 translation mechanism.

**Implementation:**
- **MAP-T**: Linux kernel support (since kernel 4.18)
- **MAP-E**: Mapping of Address and Port with Encapsulation

**Configuration Example:**
```bash
# MAP-T configuration (requires kernel 4.18+)
# Configure MAP domain
ip -6 route add 2001:db8::/96 via fe80::1 dev eth0
```

**Resources:**
- **RFC 7599**: Mapping of Address and Port with Translation (MAP-T)
- **RFC 7597**: Mapping of Address and Port with Encapsulation (MAP-E)

### IPv6 Testing and Validation Tools

#### 1. ping6 / ping (IPv6)

**Basic IPv6 connectivity testing:**
```bash
# Ping IPv6 address
ping6 2001:4860:4860::8888

# Ping with interface specification
ping6 -I eth0 2001:4860:4860::8888

# Ping with count
ping6 -c 4 2001:4860:4860::8888
```

#### 2. traceroute6 / traceroute (IPv6)

**IPv6 path discovery:**
```bash
# Traceroute IPv6
traceroute6 2001:4860:4860::8888

# Traceroute with interface
traceroute6 -i eth0 2001:4860:4860::8888
```

#### 3. mtr6 (My Traceroute for IPv6)

**Advanced path analysis:**
```bash
# Install mtr
sudo apt install mtr-tiny

# IPv6 traceroute
mtr6 2001:4860:4860::8888

# Continuous monitoring
mtr6 --report --report-cycles 10 2001:4860:4860::8888
```

#### 4. ndisc6 (IPv6 Neighbor Discovery)

**Neighbor Discovery Protocol tools:**
```bash
# Install ndisc6
sudo apt install ndisc6

# Send Router Solicitation
rdisc6 eth0

# Send Neighbor Solicitation
ndisc6 fe80::1 eth0

# Show IPv6 neighbors
ip -6 neigh show
```

#### 5. IPv6 Address Calculator

**Online Tools:**
- **IPv6 Subnet Calculator**: https://www.subnet-calculator.com/ipv6.php
- **IPv6 Address Planner**: https://www.ultratools.com/tools/ipv6SubnetCalculator

**Command-line Tools:**
```bash
# Install ipv6calc
sudo apt install ipv6calc

# Convert IPv6 address formats
ipv6calc --in ipv6addr --out ipv6addr 2001:db8::1

# Calculate subnet
ipv6calc --in ipv6addr --out ipv6addr 2001:db8::/48
```

#### 6. IPv6 Connectivity Testing

**Test IPv6 Connectivity:**
```bash
# Test IPv6 connectivity
curl -6 https://ipv6.google.com

# Test with specific interface
curl -6 --interface eth0 https://ipv6.google.com

# Test DNS resolution
dig AAAA google.com
```

### IPv6 Migration Software

#### 1. ISC DHCP (DHCPv6)

**DHCPv6 Server:**
```bash
# Install ISC DHCP server
sudo apt install isc-dhcp-server

# Configure /etc/dhcp/dhcpd6.conf
subnet6 2001:db8::/64 {
    range6 2001:db8::100 2001:db8::200;
    option dhcp6.name-servers 2001:4860:4860::8888;
}
```

**Resources:**
- **ISC DHCP**: https://www.isc.org/dhcp/
- **RFC 3315**: DHCP for IPv6

#### 2. RADVD (Router Advertisement Daemon)

**SLAAC Configuration:**
```bash
# Install radvd
sudo apt install radvd

# Configure /etc/radvd.conf
interface eth0 {
    AdvSendAdvert on;
    prefix 2001:db8::/64 {
        AdvOnLink on;
        AdvAutonomous on;
        AdvRouterAddr on;
    };
}
```

**Resources:**
- **RADVD**: https://github.com/radvd-project/radvd
- **RFC 4861**: Neighbor Discovery for IP version 6

#### 3. BIND9 (DNS with IPv6)

**IPv6 DNS Configuration:**
```bash
# Install BIND9
sudo apt install bind9

# Configure /etc/bind/named.conf.options
options {
    listen-on-v6 { any; };
    forwarders {
        2001:4860:4860::8888;
        2001:4860:4860::8844;
    };
}
```

**Resources:**
- **BIND9**: https://www.isc.org/bind/
- **RFC 3596**: DNS Extensions to Support IPv6

#### 4. FRR (Free Range Routing) - IPv6 Support

**IPv6 Routing Protocols:**
```bash
# Enable IPv6 OSPF
sudo vtysh
configure terminal
router ospf6
ospf6 router-id 1.1.1.1
interface eth0 area 0.0.0.0
exit
```

**Resources:**
- **FRR**: https://frrouting.org/
- **IPv6 OSPF**: RFC 5340
- **IPv6 BGP**: RFC 2545

### IPv6 Monitoring and Analysis Tools

#### 1. Wireshark (IPv6 Packet Analysis)

**Capture IPv6 Traffic:**
```bash
# Install Wireshark
sudo apt install wireshark

# Capture IPv6 traffic
sudo tshark -i eth0 ipv6

# Display filter for IPv6
wireshark -f "ipv6"
```

#### 2. tcpdump (IPv6 Packet Capture)

**IPv6 Packet Capture:**
```bash
# Capture IPv6 traffic
sudo tcpdump -i eth0 ip6

# Capture specific IPv6 address
sudo tcpdump -i eth0 host 2001:db8::1

# Capture IPv6 ICMP
sudo tcpdump -i eth0 ip6 and icmp6
```

#### 3. IPv6 Flow Monitoring

**Tools:**
- **nfdump**: NetFlow analysis tool
- **pmacct**: Network accounting tool
- **sflow**: sFlow monitoring

### IPv6 Migration Checklist Tools

#### 1. IPv6 Readiness Assessment

**Online Tools:**
- **IPv6 Test**: https://test-ipv6.com/
- **IPv6 Connectivity Test**: https://ipv6-test.com/

**Command-line Assessment:**
```bash
# Check IPv6 connectivity
ping6 -c 4 2001:4860:4860::8888

# Check IPv6 routing
ip -6 route show

# Check IPv6 addresses
ip -6 addr show

# Check IPv6 neighbors
ip -6 neigh show
```

#### 2. IPv6 Address Planning Tools

**Tools:**
- **IPv6 Subnet Calculator**: Command-line and web-based
- **IPv6 Address Planner**: For enterprise planning

### Integration with Virtual Labs

**Using IPv6 Tools in Virtual Labs:**

1. **NAT64 Lab Setup:**
   - Deploy Jool or TAYGA on a Linux VM
   - Configure NAT64 translation
   - Test IPv6-only clients accessing IPv4 resources

2. **Dual-Stack Lab:**
   - Configure routers with both IPv4 and IPv6
   - Test dual-stack connectivity
   - Verify protocol preference

3. **IPv6-only Lab:**
   - Configure 464XLAT for IPv4 connectivity
   - Test IPv6-only network with IPv4 service access

---

## Related Documentation

- For comprehensive IPv6 implementation, see: [IPv6 Workshop Guide](../IPv6-Workshop-Guide.md)
- For router configuration with IPv6, see: [Configuration Cheatsheet](../Configuration-Cheatsheet.md)
- For lab address allocations, see: [Test Lab Addresses](../Test-Lab-Addresses.md)
- For emerging IPv6 technologies, see: [Emerging Technologies](../../emerging-technologies/emerging-technologies.md)

## References

**RFC Documents:**
- **RFC 6146**: Stateful NAT64
- **RFC 7915**: IP/ICMP Translation Algorithm (SIIT)
- **RFC 6877**: 464XLAT
- **RFC 7599**: MAP-T
- **RFC 7597**: MAP-E
- **RFC 3315**: DHCPv6
- **RFC 4861**: IPv6 Neighbor Discovery
- **RFC 4862**: IPv6 Stateless Address Autoconfiguration

**Open Source Projects:**
- **Jool**: https://www.jool.mx/
- **TAYGA**: https://github.com/fwdillema/tayga
- **clatd**: https://github.com/toreanderson/clatd
- **FRR**: https://frrouting.org/
- **RADVD**: https://github.com/radvd-project/radvd
- **BIND9**: https://www.isc.org/bind/

**Testing Resources:**
- **IPv6 Test**: https://test-ipv6.com/
- **IPv6 Connectivity Test**: https://ipv6-test.com/
- **IPv6 Subnet Calculator**: https://www.subnet-calculator.com/ipv6.php

