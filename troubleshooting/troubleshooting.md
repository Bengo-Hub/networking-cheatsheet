# Network Troubleshooting and Optimization

**This section is part of the [Networking Principles Guide](../Networking-Principles.md)**

---

## Network Troubleshooting and Optimization

### Troubleshooting Methodology

**Systematic Approach:**

1. **Identify the Problem**: Gather symptoms and scope
2. **Collect Information**: Network topology, recent changes, error messages
3. **Formulate Hypothesis**: Possible causes based on symptoms
4. **Test Hypothesis**: Use appropriate tools and methods
5. **Implement Solution**: Apply fix and verify
6. **Document**: Record problem and solution

**OSI Model Troubleshooting:**

- **Layer 1 (Physical)**: Cable issues, connectors, link lights
- **Layer 2 (Data Link)**: MAC address issues, VLANs, STP loops
- **Layer 3 (Network)**: IP addressing, routing, ACLs
- **Layer 4 (Transport)**: TCP/UDP issues, port filtering
- **Layer 5-7 (Upper Layers)**: Application-specific issues

### Troubleshooting Tools

**Command-Line Tools:**

**ping - Connectivity Testing:**
```bash
# Basic ping
ping 8.8.8.8

# Linux/Mac options
ping -c 5 8.8.8.8          # Send 5 packets
ping -i 2 8.8.8.8          # Interval of 2 seconds
ping -s 1500 8.8.8.8       # Packet size 1500 bytes
ping -t 64 8.8.8.8         # TTL value

# Windows options
ping -n 5 8.8.8.8          # Send 5 packets
ping -t 8.8.8.8            # Ping until stopped
ping -l 1500 8.8.8.8       # Packet size

# IPv6
ping6 2001:4860:4860::8888
```

**traceroute/tracert - Path Discovery:**
```bash
# Linux/Mac
traceroute 8.8.8.8
traceroute -n 8.8.8.8              # No DNS resolution
traceroute -w 5 8.8.8.8            # Wait time 5 seconds

# Windows
tracert 8.8.8.8
tracert -d 8.8.8.8                 # No DNS resolution
tracert -h 30 8.8.8.8              # Max hops 30

# IPv6
traceroute6 2001:4860:4860::8888
```

**nslookup/dig - DNS Testing:**
```bash
# Basic DNS lookup
nslookup www.example.com
nslookup -type=MX example.com
nslookup -type=AAAA example.com

# Interactive mode
nslookup
> server 8.8.8.8
> set type=MX
> example.com

# dig (Linux/Mac)
dig www.example.com
dig @8.8.8.8 example.com MX
dig +trace example.com              # Trace resolution path
dig -x 192.0.2.1                    # Reverse DNS
```

**arp - MAC Address Resolution:**
```bash
# View ARP cache
arp -a                              # Windows/Linux
ip neigh show                       # Linux (iproute2)

# Delete ARP entry
arp -d 192.168.1.10                 # Windows/Linux
sudo ip neigh del 192.168.1.10 dev eth0  # Linux

# Add static ARP entry
arp -s 192.168.1.10 00-11-22-33-44-55    # Windows/Linux
```

**netstat/ss - Network Connections:**
```bash
# View all connections
netstat -a                          # Windows/Linux
netstat -an                         # Numeric addresses

# View routing table
netstat -r                          # Windows/Linux
netstat -rn                         # Numeric, no DNS

# View listening ports
netstat -l                          # Linux
netstat -an | findstr LISTENING     # Windows

# Modern Linux alternative: ss
ss -tuln                            # TCP/UDP listening, numeric
ss -a                               # All connections
ss -s                               # Summary statistics
```

**ifconfig/ipconfig - Interface Configuration:**
```bash
# Windows
ipconfig                            # Basic info
ipconfig /all                       # Detailed info
ipconfig /release                   # Release DHCP lease
ipconfig /renew                     # Renew DHCP lease
ipconfig /flushdns                  # Clear DNS cache

# Linux/Mac (ifconfig - legacy)
ifconfig                            # All interfaces
ifconfig eth0                       # Specific interface
ifconfig eth0 up                    # Enable interface
ifconfig eth0 down                  # Disable interface

# Linux (ip - modern)
ip addr show                        # Show all addresses
ip link show                        # Show all links
ip route show                       # Show routing table
ip -s link show eth0                # Statistics
```

**tcpdump - Packet Capture:**
```bash
# Capture all traffic
tcpdump -i eth0

# Capture specific host
tcpdump -i eth0 host 192.168.1.10

# Capture specific protocol
tcpdump -i eth0 tcp port 80

# Save to file
tcpdump -i eth0 -w capture.pcap

# Read from file
tcpdump -r capture.pcap

# Capture with verbose output
tcpdump -v -i eth0

# Capture specific number of packets
tcpdump -i eth0 -c 100
```

**telnet/nc - Port Connectivity Testing:**
```bash
# Test TCP port
telnet 192.168.1.10 80
nc -zv 192.168.1.10 80              # netcat

# Test UDP port
nc -uvz 192.168.1.10 53             # UDP DNS

# Test multiple ports
nc -zv 192.168.1.10 20-30           # Port range
```

**Additional Troubleshooting Commands:**
```bash
# Linux
route -n                            # Routing table
ip route                            # Modern routing commands
mtr 8.8.8.8                         # Combination ping/traceroute
tcpdump -i eth0                     # Packet capture
ethtool eth0                        # Ethernet interface info

# Windows
route print                         # Routing table
pathping 8.8.8.8                    # Combination ping/traceroute
netsh interface show interface      # Interface status
netsh wlan show profiles            # Wi-Fi profiles
```

**GUI Tools:**

- **Wireshark**: Packet analysis and protocol inspection
- **Network Analyzers**: Traffic monitoring and analysis
- **SNMP Tools**: Network monitoring and statistics
- **Bandwidth Monitors**: Traffic utilization analysis

**Cisco-Specific Tools:**

**Essential Show Commands:**

```cisco
! Interface information
show interfaces
show interfaces GigabitEthernet0/0
show interfaces status
show ip interface brief
show ipv6 interface brief

! Routing information
show ip route
show ip route 192.168.1.0
show ip route ospf
show ip route bgp
show ip route summary

! OSPF troubleshooting
show ip ospf
show ip ospf neighbor
show ip ospf neighbor detail
show ip ospf database
show ip ospf interface
show ip ospf events

! BGP troubleshooting
show ip bgp
show ip bgp summary
show ip bgp neighbors
show ip bgp neighbors 1.1.1.1
show ip bgp 192.168.1.0
show ip bgp regexp ^65000

! Switching troubleshooting
show mac address-table
show mac address-table dynamic
show spanning-tree
show spanning-tree root
show spanning-tree interface Gi0/1
show vlan brief
show interfaces trunk

! ARP and neighbors
show arp
show ip arp
show ipv6 neighbors

! ACLs and security
show access-lists
show ip access-lists
show policy-map interface
show crypto isakmp sa
show crypto ipsec sa

! System information
show version
show running-config
show startup-config
show ip protocols
show clock
show users
```

**Debug Commands (Use with Caution):**

```cisco
! Enable debugging
debug ip ospf adj
debug ip ospf events
debug ip ospf packet

debug ip bgp updates
debug ip bgp events
debug ip bgp keepalives

debug ip routing
debug ip icmp
debug arp

! View debug output
terminal monitor              ! View on console
terminal monitor logging      ! Log debug output

! Stop debugging
undebug all
no debug all
```

**Packet Capture (Cisco):**

```cisco
! Embedded Packet Capture (EPC)
monitor capture buffer BUFFER size 1024 max-size 1518
monitor capture point ip cef POINT Gi0/0 both
monitor capture point associate POINT BUFFER
monitor capture start POINT
! ... wait ...
monitor capture stop POINT
show monitor capture buffer BUFFER dump

! Wireshark/External capture
! Use SPAN (Switched Port Analyzer) or RSPAN
monitor session 1 source interface Gi0/1
monitor session 1 destination interface Gi0/10
```

### Common Issues and Solutions

**Connectivity Issues:**

- **No Link**: Check physical connections, cables, port status
- **Intermittent Connectivity**: Cable quality, interference, duplex mismatches
- **Slow Performance**: Bandwidth utilization, congestion, routing issues

**IP Addressing Issues:**

- **Duplicate IP Addresses**: DHCP conflicts, static IP collisions
- **Wrong Subnet**: Incorrect subnet mask or gateway
- **No IP Address**: DHCP server issues, network connectivity

**Routing Issues:**

- **No Route to Destination**: Missing routes, routing protocol problems
- **Suboptimal Routing**: Routing protocol convergence, metric issues
- **Routing Loops**: Incorrect route advertisements, redistribution issues

**Switching Issues:**

- **VLAN Problems**: Incorrect VLAN assignment, trunk configuration
  ```cisco
  ! Verify VLAN configuration
  show vlan brief
  show interfaces switchport
  show interfaces trunk
  
  ! Verify native VLAN matches on both ends
  show interfaces Gi0/1 switchport
  ```

- **STP Loops**: Spanning tree misconfiguration
  ```cisco
  ! Check for loops
  show spanning-tree
  show spanning-tree root
  show spanning-tree inconsistentports
  
  ! Verify port states
  show spanning-tree interface Gi0/1 detail
  ```

- **Broadcast Storms**: Loop prevention, broadcast domain issues
  ```cisco
  ! Monitor interface statistics
  show interfaces Gi0/1 | include broadcast
  show interface counters errors
  
  ! Enable storm control
  storm-control broadcast level 10.00
  ```

**Troubleshooting Scenarios:**

**Scenario 1: No Connectivity Between Hosts**

```
1. Ping test:
   ping 192.168.1.10

2. Check ARP:
   arp -a | findstr 192.168.1.10

3. Verify routing:
   route print | findstr 192.168.1.0
   
4. Check interface status:
   show interfaces Gi0/0
   
5. Verify VLAN/switchport:
   show interfaces switchport
   show mac address-table
```

**Scenario 2: Intermittent Connectivity**

```
1. Check interface errors:
   show interfaces Gi0/0 | include errors
   
2. Verify duplex/speed:
   show interfaces Gi0/0 | include duplex
   show interfaces Gi0/0 | include speed
   
3. Check for packet loss:
   ping -n 100 192.168.1.10
   
4. Verify STP status:
   show spanning-tree
   
5. Check for flapping routes:
   show ip route | include 192.168.1.0
   show log | include ospf
```

**Scenario 3: OSPF Neighbor Not Forming**

```
1. Check neighbor state:
   show ip ospf neighbor
   
2. Verify interfaces:
   show ip ospf interface
   show ip ospf interface Gi0/0
   
3. Check network type:
   show ip ospf interface detail
   
4. Verify area configuration:
   show ip ospf | include area
   
5. Check authentication:
   show ip ospf interface | include authentication
   
6. Verify MTU:
   show interfaces Gi0/0 | include MTU
```

**Scenario 4: BGP Route Not Received**

```
1. Check BGP session:
   show ip bgp summary
   show ip bgp neighbors 1.1.1.1
   
2. Verify BGP table:
   show ip bgp
   show ip bgp 192.168.1.0
   
3. Check received routes:
   show ip bgp neighbors 1.1.1.1 received-routes
   
4. Verify route filters:
   show ip bgp neighbors 1.1.1.1 | include Route-map
   
5. Check AS_PATH:
   show ip bgp 192.168.1.0 | include Path
```

**Scenario 5: DHCP Issues**

```
1. Check DHCP pool:
   show ip dhcp pool
   show ip dhcp binding
   
2. Verify relay agent:
   show ip helper-address
   
3. Check for DHCP server:
   show ip dhcp server statistics
   
4. Verify interface configuration:
   show ip interface Gi0/0
   
5. Test from client:
   ipconfig /release
   ipconfig /renew
   ipconfig /all
```

### Performance Optimization

**Bandwidth Management:**

- QoS implementation for critical traffic
- Bandwidth allocation and policing
- Traffic shaping and rate limiting

**Network Monitoring:**

- Baseline performance metrics
- Continuous monitoring and alerting
- Capacity planning based on trends

**Optimization Techniques:**

- Route summarization
- Network segmentation
- Load balancing
- Caching and content delivery

### Troubleshooting References

For router-specific troubleshooting, see:
- [Configuration Cheatsheet](../docs/Configuration-Cheatsheet.md)
- [IPv6 Workshop Guide](../docs/IPv6-Workshop-Guide.md) for IPv6-specific issues

**Trusted Resources:**
- **Cisco Troubleshooting Guides**: https://www.cisco.com/c/en/us/support/index.html
- **Wireshark Documentation**: https://www.wireshark.org/docs/
- **tcpdump Manual**: https://www.tcpdump.org/manpages/
- **RFC 792**: ICMP (Internet Control Message Protocol)
- **Packet Life Cheat Sheets**: http://packetlife.net/library/cheat-sheets/

---

