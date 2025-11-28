# Beginner Level Fundamentals

**This section is part of the [Networking Principles Guide](../Networking-Principles.md)**

---

## Beginner Level Fundamentals

### 1.1 What is Computer Networking?

**Definition**: A computer network is an interconnected system of computers and devices that communicate to share resources, information, and services. Networks enable data transfer, resource sharing, and collaborative computing.

**Goals of Computer Networks:**

1. **Cost Reduction**: Sharing hardware and software resources reduces expenses
2. **High Reliability**: Redundancy and backups ensure data restoration and system availability
3. **Flexibility**: Efficient sharing of files and resources at variable speeds
4. **Powerful Communication Medium**: Enables fast data access and communication
5. **Enhanced Security**: Controlled designs and backup systems improve security and reliability

### 1.2 Network Types and Classifications

**By Geographic Scope:**

- **Personal Area Network (PAN)**: Connects devices within a person's workspace (typically <10 meters)
  - Examples: Bluetooth connections, USB connections between devices
- **Local Area Network (LAN)**: Covers a small geographic area like a building or campus
  - Examples: Office networks, home networks, school networks
- **Metropolitan Area Network (MAN)**: Covers a city or large campus
  - Examples: City-wide Wi-Fi, campus networks connecting multiple buildings
- **Wide Area Network (WAN)**: Spans large geographic areas, connecting multiple LANs
  - Examples: Internet, corporate networks connecting remote offices
- **Global Area Network (GAN)**: Spans multiple countries and continents
  - Examples: Global corporate networks, international internet connections

**By Connection Method:**

- **Wired Networks**: Use physical cables (Ethernet, fiber optic)
- **Wireless Networks**: Use radio waves (Wi-Fi, Bluetooth, cellular)

**By Topology:**

- **Star**: All nodes connect to a central hub or switch
- **Bus**: All devices share a single communication line
- **Ring**: Each device connects to two others, forming a circle
- **Mesh**: Devices are interconnected with multiple paths (full mesh or partial mesh)
- **Tree**: Hierarchical structure with root, branches, and leaves
- **Hybrid**: Combination of multiple topologies

### 1.3 Network Models: OSI and TCP/IP

#### OSI Model (Open Systems Interconnection)

The OSI model is a seven-layer conceptual framework that standardizes network functions to support interoperability between different systems:

**Layer 7 - Application Layer**
- Purpose: Interfaces with software applications to deliver network services
- Protocols: HTTP, HTTPS, FTP, SMTP, DNS, DHCP, Telnet, SSH
- Functions: User interface, email services, file transfer, directory services
- Data Unit: Message/Data

**Layer 6 - Presentation Layer**
- Purpose: Translates data into formats usable by the application layer
- Functions: Data encryption/decryption, data compression, character encoding translation
- Protocols: SSL/TLS (for encryption), ASCII, EBCDIC, JPEG, MPEG
- Data Unit: Message/Data

**Layer 5 - Session Layer**
- Purpose: Manages sessions or connections between devices
- Functions: Establishes, maintains, and terminates sessions, synchronization, dialog control
- Protocols: NetBIOS, RPC, PPTP, L2TP
- Data Unit: Message/Data

**Layer 4 - Transport Layer**
- Purpose: Ensures reliable data delivery, manages flow control, and handles retransmission
- Functions: Segmentation, flow control, error recovery, connection management
- Protocols: TCP (reliable), UDP (unreliable), SCTP
- Data Unit: Segment (TCP) or Datagram (UDP)

**Layer 3 - Network Layer**
- Purpose: Handles routing and forwarding of data packets across networks
- Functions: Logical addressing (IP addresses), routing, path determination, packet fragmentation
- Protocols: IP (IPv4, IPv6), ICMP, IGMP, ARP, OSPF, BGP, IS-IS
- Data Unit: Packet

**Layer 2 - Data Link Layer**
- Purpose: Ensures error-free data transfer between devices connected to the same network
- Functions: Physical addressing (MAC addresses), error detection/correction, flow control, frame synchronization
- Sublayers:
  - LLC (Logical Link Control): Manages error control and flow control
  - MAC (Media Access Control): Controls access to the physical medium
- Protocols: Ethernet, PPP, HDLC, Frame Relay, ATM
- Data Unit: Frame

**Layer 1 - Physical Layer**
- Purpose: Manages the physical connection between devices
- Functions: Bit transmission, electrical/optical signaling, physical topology, cable specifications
- Components: Cables (twisted pair, fiber optic, coaxial), connectors, hubs, repeaters, transceivers
- Data Unit: Bit

#### TCP/IP Model

The TCP/IP model simplifies the OSI model into four practical layers used in real-world networking:

**Layer 4 - Application Layer**
- Combines OSI Layers 5, 6, and 7
- Protocols: HTTP, HTTPS, FTP, SMTP, DNS, DHCP, SNMP, Telnet, SSH

**Layer 3 - Transport Layer**
- Corresponds to OSI Layer 4
- Protocols: TCP, UDP, SCTP

**Layer 2 - Internet Layer**
- Corresponds to OSI Layer 3
- Protocols: IP, ICMP, IGMP, ARP

**Layer 1 - Network Access Layer (Link Layer)**
- Combines OSI Layers 1 and 2
- Protocols: Ethernet, Wi-Fi, PPP, Frame Relay

### 1.4 Network Devices and Components

**Basic Network Devices:**

1. **Hub**: Layer 1 device that broadcasts all data to all connected devices
   - Simple but inefficient; rarely used in modern networks
   - Creates a single collision domain

2. **Switch**: Layer 2 device that intelligently forwards data to specific devices
   - Uses MAC addresses to make forwarding decisions
   - Creates separate collision domains for each port
   - Types: Unmanaged, Managed, Layer 3 switches

3. **Router**: Layer 3 device that routes data between different networks
   - Uses IP addresses to make routing decisions
   - Connects LANs to WANs
   - Maintains routing tables

4. **Bridge**: Layer 2 device that connects network segments
   - Filters traffic based on MAC addresses
   - Less common in modern networks (replaced by switches)

5. **Access Point (AP)**: Device that allows wireless devices to connect to a wired network
   - Acts as a bridge between wireless and wired networks
   - Implements Wi-Fi standards (802.11a/b/g/n/ac/ax)

6. **Modem**: Modulates and demodulates signals for transmission over telephone lines or cable
   - Converts digital data to analog signals and vice versa
   - Used for internet connectivity (DSL, cable modems)

7. **Firewall**: Security device that monitors and controls network traffic
   - Filters traffic based on security rules
   - Can be hardware or software-based

8. **Network Interface Card (NIC)**: Hardware component that connects a device to a network
   - Each NIC has a unique MAC address
   - Can be wired (Ethernet) or wireless (Wi-Fi)

### 1.5 Transmission Media

**Wired Media:**

1. **Twisted Pair Cable**
   - **Unshielded Twisted Pair (UTP)**: Common in LANs, categories (Cat5e, Cat6, Cat6a, Cat7)
   - **Shielded Twisted Pair (STP)**: Better EMI protection, used in noisy environments
   - Maximum distance: ~100 meters for Ethernet
   - Standards: TIA/EIA-568

2. **Coaxial Cable**
   - Used for cable TV and broadband internet
   - Types: Thicknet, Thinnet
   - Better shielding than twisted pair
   - Higher bandwidth capacity

3. **Fiber Optic Cable**
   - Uses light to transmit data
   - Types: Single-mode (long distances) and Multi-mode (shorter distances)
   - Advantages: High bandwidth, immunity to EMI, secure transmission
   - Disadvantages: Higher cost, fragile
   - Common standards: Single-mode (1310nm, 1550nm), Multi-mode (850nm, 1300nm)

**Wireless Media:**

1. **Radio Waves**
   - Wi-Fi (2.4 GHz, 5 GHz, 6 GHz bands)
   - Bluetooth (2.4 GHz ISM band)
   - Cellular networks (various frequency bands)

2. **Microwave**
   - Point-to-point communication
   - Used for long-distance wireless links
   - Requires line of sight

3. **Infrared**
   - Short-range communication
   - Used in remote controls, short-range device communication
   - Requires line of sight

4. **Satellite**
   - Global coverage
   - High latency
   - Used for remote areas and global communication

### 1.6 IP Addressing Fundamentals

**IPv4 Addressing:**

- **Format**: 32-bit address written as four octets (e.g., 192.168.1.1)
- **Address Classes** (Historical):
  - Class A: 0.0.0.0 to 127.255.255.255 (8-bit network, 24-bit host)
  - Class B: 128.0.0.0 to 191.255.255.255 (16-bit network, 16-bit host)
  - Class C: 192.0.0.0 to 223.255.255.255 (24-bit network, 8-bit host)
  - Class D: 224.0.0.0 to 239.255.255.255 (multicast)
  - Class E: 240.0.0.0 to 255.255.255.255 (reserved)

- **CIDR (Classless Inter-Domain Routing)**:
  - Modern approach using subnet masks
  - Notation: IP address/prefix length (e.g., 192.168.1.0/24)
  - More flexible than classful addressing

- **Private IP Address Ranges** (RFC 1918):
  - 10.0.0.0/8 (10.0.0.0 to 10.255.255.255)
  - 172.16.0.0/12 (172.16.0.0 to 172.31.255.255)
  - 192.168.0.0/16 (192.168.0.0 to 192.168.255.255)

- **Special Addresses**:
  - 127.0.0.0/8: Loopback addresses (127.0.0.1)
  - 169.254.0.0/16: APIPA (Automatic Private IP Addressing)
  - 0.0.0.0: Default route or "any address"
  - 255.255.255.255: Broadcast address

**IPv6 Addressing:**

- **Format**: 128-bit address written in hexadecimal (e.g., 2001:0db8:85a3:0000:0000:8a2e:0370:7334)
- **Simplified notation**: Leading zeros can be omitted, consecutive zeros can be replaced with :: (once per address)
- **Address Types**:
  - Global Unicast: Public routable addresses (2000::/3)
  - Link-Local: Used for communication on a single link (fe80::/10)
  - Unique Local: Private addresses (fc00::/7)
  - Multicast: One-to-many communication (ff00::/8)
  - Anycast: One-to-nearest communication (uses unicast addresses)

> **For lab address allocations and examples, see [Test Lab Addresses](../docs/Test-Lab-Addresses.md)**

### 1.7 Subnetting Basics

**Purpose of Subnetting:**

- Improve network performance and security
- Reduce network congestion
- Efficient use of IP address space
- Isolate network segments

**Subnetting Concepts:**

- **Subnet Mask**: Identifies network and host portions of an IP address
  - Example: 255.255.255.0 (/24) for 192.168.1.0/24
- **Network Address**: First address in a subnet (all host bits = 0)
- **Broadcast Address**: Last address in a subnet (all host bits = 1)
- **Host Addresses**: Usable addresses between network and broadcast addresses

**Subnetting Example:**

- Network: 192.168.1.0/24
- Subnet Mask: 255.255.255.0
- Network Address: 192.168.1.0
- Broadcast Address: 192.168.1.255
- Usable Host Range: 192.168.1.1 to 192.168.1.254 (254 hosts)

#### Detailed Subnetting Calculations

**Understanding CIDR Notation:**

CIDR (Classless Inter-Domain Routing) notation expresses both the IP address and its subnet mask in a single format: `IP_address/prefix_length`

- **Prefix Length**: Number of bits used for the network portion
- Example: `192.168.1.0/24` means:
  - First 24 bits = network portion
  - Last 8 bits = host portion
  - Subnet mask: 255.255.255.0

**Step-by-Step Subnetting Calculation:**

**Example 1: Creating 4 Subnets from 192.168.1.0/24**

1. **Determine required subnets**: Need 4 subnets
2. **Calculate subnet bits**: 2^2 = 4 subnets (need 2 bits)
3. **Calculate new prefix**: 24 + 2 = /26
4. **Calculate hosts per subnet**: 2^(32-26) - 2 = 2^6 - 2 = 64 - 2 = 62 hosts per subnet
5. **Subnet mask**: 255.255.255.192 (binary: 11111111.11111111.11111111.11000000)

**Subnet Breakdown:**
- **Subnet 1**: 192.168.1.0/26
  - Network: 192.168.1.0
  - Broadcast: 192.168.1.63
  - Hosts: 192.168.1.1 to 192.168.1.62 (62 hosts)

- **Subnet 2**: 192.168.1.64/26
  - Network: 192.168.1.64
  - Broadcast: 192.168.1.127
  - Hosts: 192.168.1.65 to 192.168.1.126 (62 hosts)

- **Subnet 3**: 192.168.1.128/26
  - Network: 192.168.1.128
  - Broadcast: 192.168.1.191
  - Hosts: 192.168.1.129 to 192.168.1.190 (62 hosts)

- **Subnet 4**: 192.168.1.192/26
  - Network: 192.168.1.192
  - Broadcast: 192.168.1.255
  - Hosts: 192.168.1.193 to 192.168.1.254 (62 hosts)

**Example 2: Variable Length Subnet Mask (VLSM)**

**Scenario**: Need to subnet 172.16.0.0/16 for:
- LAN A: 500 hosts
- LAN B: 200 hosts
- LAN C: 50 hosts
- WAN links: 2 hosts each (5 links)

**Calculations:**

1. **LAN A (500 hosts)**: Need 2^9 = 512 addresses (9 host bits)
   - Subnet: 172.16.0.0/23
   - Hosts: 172.16.0.1 to 172.16.1.254 (510 usable)

2. **LAN B (200 hosts)**: Need 2^8 = 256 addresses (8 host bits)
   - Subnet: 172.16.2.0/24
   - Hosts: 172.16.2.1 to 172.16.2.254 (254 usable)

3. **LAN C (50 hosts)**: Need 2^6 = 64 addresses (6 host bits)
   - Subnet: 172.16.3.0/26
   - Hosts: 172.16.3.1 to 172.16.3.62 (62 usable)

4. **WAN Links (2 hosts each)**: Need 2^2 = 4 addresses (2 host bits)
   - Link 1: 172.16.3.64/30 (hosts: .65, .66)
   - Link 2: 172.16.3.68/30 (hosts: .69, .70)
   - Link 3: 172.16.3.72/30 (hosts: .73, .74)
   - Link 4: 172.16.3.76/30 (hosts: .77, .78)
   - Link 5: 172.16.3.80/30 (hosts: .81, .82)

**Subnetting Cheat Sheet:**

| Prefix | Subnet Mask | Hosts | Networks (/24) |
|--------|-------------|-------|----------------|
| /30 | 255.255.255.252 | 2 | 64 |
| /29 | 255.255.255.248 | 6 | 32 |
| /28 | 255.255.255.240 | 14 | 16 |
| /27 | 255.255.255.224 | 30 | 8 |
| /26 | 255.255.255.192 | 62 | 4 |
| /25 | 255.255.255.128 | 126 | 2 |
| /24 | 255.255.255.0 | 254 | 1 |

**Formula Reference:**
- Number of subnets = 2^(subnet_bits)
- Hosts per subnet = 2^(host_bits) - 2
- Block size = 2^(host_bits)

### 1.8 Basic Protocols

**HTTP/HTTPS (Hypertext Transfer Protocol):**
- **HTTP**: Application layer protocol for web communication (port 80)
  - Stateless protocol
  - Request-response model
  - Methods: GET, POST, PUT, DELETE, etc.
- **HTTPS**: Secure version using TLS/SSL (port 443)
  - Encrypted communication
  - Authentication and integrity

**DNS (Domain Name System):**
- Translates domain names to IP addresses (port 53)
- Hierarchical distributed database
- Record types: A, AAAA, CNAME, MX, NS, PTR, TXT
- Resolvers and authoritative servers

**Detailed DNS Resolution Process (RFC 1034, RFC 1035):**

**DNS Query Types:**
- **Recursive Query**: Client asks DNS server to resolve fully
- **Iterative Query**: DNS server refers client to another server

**DNS Resolution Steps:**

1. **Client Request**: Browser requests "www.example.com"
2. **Local Cache Check**: Client checks local DNS cache first
3. **Recursive Resolver**: Queries ISP's DNS resolver
4. **Root Server**: Resolver queries root DNS server (.)
5. **TLD Server**: Root refers to .com TLD server
6. **Authoritative Server**: TLD refers to example.com nameserver
7. **IP Address Returned**: Authoritative server returns IP address
8. **Cache Storage**: Resolver caches result for TTL period

**DNS Record Types:**

- **A Record**: Maps hostname to IPv4 address
  ```
  www.example.com.    IN    A    192.0.2.1
  ```

- **AAAA Record**: Maps hostname to IPv6 address
  ```
  www.example.com.    IN    AAAA    2001:db8::1
  ```

- **CNAME Record**: Canonical name (alias)
  ```
  www.example.com.    IN    CNAME    example.com.
  ```

- **MX Record**: Mail exchange server
  ```
  example.com.        IN    MX    10    mail.example.com.
  ```

- **NS Record**: Nameserver delegation
  ```
  example.com.        IN    NS    ns1.example.com.
  ```

- **PTR Record**: Reverse DNS (IP to name)
  ```
  1.2.0.192.in-addr.arpa.    IN    PTR    www.example.com.
  ```

- **TXT Record**: Text information (SPF, DKIM)
  ```
  example.com.    IN    TXT    "v=spf1 mx ~all"
  ```

**DNS Query Commands:**

```bash
# Basic DNS lookup
nslookup www.example.com
nslookup -type=MX example.com    # Query MX records
nslookup -type=AAAA example.com  # Query IPv6 records

# Detailed DNS queries (Linux/Mac)
dig www.example.com
dig example.com MX               # Query MX records
dig @8.8.8.8 example.com        # Query specific DNS server
dig +trace example.com          # Trace DNS resolution path
dig -x 192.0.2.1                # Reverse DNS lookup

# Windows PowerShell
Resolve-DnsName example.com
Resolve-DnsName example.com -Type MX
```

**DNS Configuration Files:**

```bash
# Linux: /etc/resolv.conf
nameserver 8.8.8.8
nameserver 8.8.4.4
search example.com

# Windows: Network adapter settings or PowerShell
Set-DnsClientServerAddress -InterfaceIndex 12 -ServerAddresses 8.8.8.8,8.8.4.4
```

**DHCP (Dynamic Host Configuration Protocol):**
- Automatically assigns IP addresses and network configuration (ports 67/68)
- DORA process: Discover, Offer, Request, Acknowledge
- Lease time management
- DHCP relay agents

**Detailed DHCP DORA Process (RFC 2131):**

1. **DISCOVER** (Client → Server):
   - Client broadcasts DHCPDISCOVER message (UDP port 67)
   - Source IP: 0.0.0.0 (client has no IP yet)
   - Destination IP: 255.255.255.255 (broadcast)
   - Contains: Client MAC address, requested parameters

2. **OFFER** (Server → Client):
   - DHCP server(s) respond with DHCPOFFER message
   - Contains: Offered IP address, subnet mask, lease time, default gateway, DNS servers
   - Server reserves the IP address temporarily

3. **REQUEST** (Client → Server):
   - Client broadcasts DHCPREQUEST message
   - Accepts offer from chosen server
   - May include option to request specific IP (if renewing)

4. **ACKNOWLEDGE** (Server → Client):
   - Server sends DHCPACK confirming the lease
   - Client configures its interface with provided parameters
   - Lease timer starts

**DHCP Lease Renewal Process:**

- **T1 (50% of lease)**: Client attempts renewal with original server (unicast)
- **T2 (87.5% of lease)**: If T1 fails, client broadcasts REQUEST for any server
- **Lease Expiration**: Client must release IP or request new lease

**DHCP Relay Agent Configuration:**

```bash
# Cisco Router DHCP Relay Configuration
interface GigabitEthernet0/0
  ip helper-address 192.168.100.10  # DHCP Server IP
  ip address 192.168.1.1 255.255.255.0
```

**DHCP Options (Common):**
- **Option 1**: Subnet Mask
- **Option 3**: Default Gateway (Router)
- **Option 6**: DNS Servers
- **Option 51**: IP Address Lease Time
- **Option 82**: Relay Agent Information (for DHCP snooping)

**Verification Commands:**

```bash
# Windows
ipconfig /all                    # View DHCP lease details
ipconfig /release                # Release DHCP lease
ipconfig /renew                  # Renew DHCP lease

# Linux
dhclient -v                      # Request/renew DHCP lease
dhclient -r                      # Release DHCP lease
cat /var/lib/dhcp/dhclient.leases # View lease information

# Router/Switch (Cisco)
show ip dhcp binding             # View DHCP bindings
show ip dhcp pool                # View DHCP pool configuration
debug ip dhcp server events      # Debug DHCP process
```

**FTP (File Transfer Protocol):**
- Transfers files between hosts (ports 20/21)
- Control connection (21) and data connection (20)
- Modes: Active and Passive
- Secure versions: FTPS, SFTP

**SMTP/POP3/IMAP (Email Protocols):**
- **SMTP**: Sends email (port 25, 587, 465)
- **POP3**: Retrieves email from server (port 110, 995)
- **IMAP**: Manages email on server (port 143, 993)

**SSH (Secure Shell):**
- Encrypted remote access (port 22)
- Replaces insecure Telnet
- Key-based authentication
- Port forwarding capabilities

**Telnet:**
- Unencrypted remote access (port 23)
- Legacy protocol, largely replaced by SSH
- Still used for some device management

**SNMP (Simple Network Management Protocol):**
- Network monitoring and management (ports 161/162)
- Versions: v1, v2c, v3 (secured)
- Get, Set, Trap operations
- MIB (Management Information Base)

### 1.9 Basic Troubleshooting Tools

**ping:**
- Tests connectivity to a host
- Uses ICMP echo request/reply
- Syntax: `ping <hostname or IP>`
- Options: `-c` (count), `-t` (TTL), `-s` (size)

**traceroute / tracert:**
- Shows the path packets take to a destination
- Uses TTL expiration to map route
- Syntax: `traceroute <hostname or IP>` (Linux/Mac)
- Syntax: `tracert <hostname or IP>` (Windows)

**ipconfig / ifconfig:**
- Displays network configuration
- `ipconfig` (Windows): Shows IP, subnet mask, default gateway
- `ifconfig` (Linux/Mac): Shows interface configuration
- Options: `/all` (Windows), `-a` (Linux)

**arp:**
- Displays and manages ARP cache
- Maps IP addresses to MAC addresses
- Syntax: `arp -a` (view cache), `arp -d` (delete entry)

**nslookup / dig:**
- DNS query tools
- `nslookup`: Interactive and non-interactive DNS queries
- `dig`: More detailed DNS queries (Linux/Mac)

**netstat:**
- Displays network connections and routing tables
- Syntax: `netstat -a` (all connections), `netstat -r` (routing table)

**Wireshark:**
- Packet analyzer for deep inspection
- Captures and analyzes network traffic
- GUI-based tool with powerful filtering

---

## 1.10 Detailed Protocol Explanations

### TCP/IP Protocol Deep Dive

#### TCP (Transmission Control Protocol) - RFC 793

**TCP Characteristics:**
- **Connection-oriented**: Establishes connection before data transfer
- **Reliable**: Guarantees delivery and ordering
- **Flow Control**: Prevents sender from overwhelming receiver
- **Congestion Control**: Adapts to network conditions
- **Full-duplex**: Bi-directional communication

**TCP Three-Way Handshake:**

The TCP connection establishment process:

```
1. CLIENT → SERVER: SYN (Synchronize)
   - Sets SYN flag = 1
   - Random initial sequence number (e.g., seq = 1000)
   - Client enters SYN-SENT state

2. SERVER → CLIENT: SYN-ACK (Synchronize-Acknowledge)
   - Sets SYN flag = 1, ACK flag = 1
   - Acknowledges client's sequence number (ack = 1001)
   - Server's random sequence number (e.g., seq = 5000)
   - Server enters SYN-RECEIVED state

3. CLIENT → SERVER: ACK (Acknowledge)
   - Sets ACK flag = 1
   - Acknowledges server's sequence number (ack = 5001)
   - Increments own sequence number (seq = 1001)
   - Both enter ESTABLISHED state

Connection Established - Data transfer can begin
```

**TCP Header Structure (20 bytes minimum):**

```
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|          Source Port          |       Destination Port        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                        Sequence Number                        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Acknowledgment Number                      |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|  Data |           |U|A|P|R|S|F|                               |
| Offset| Reserved  |R|C|S|S|Y|I|            Window             |
|       |           |G|K|H|T|N|N|                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|           Checksum            |         Urgent Pointer        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Options                    |    Padding    |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

**TCP Flags:**
- **SYN**: Synchronize sequence numbers (connection initiation)
- **ACK**: Acknowledgment field is valid
- **FIN**: Finish (connection termination)
- **RST**: Reset connection
- **PSH**: Push function (immediate delivery)
- **URG**: Urgent pointer is valid

**TCP Connection Termination (Four-Way Handshake):**

```
1. CLIENT → SERVER: FIN
   - Client wants to close connection
   - Client enters FIN-WAIT-1 state

2. SERVER → CLIENT: ACK
   - Server acknowledges FIN
   - Server enters CLOSE-WAIT state
   - Client enters FIN-WAIT-2 state

3. SERVER → CLIENT: FIN
   - Server is ready to close
   - Server enters LAST-ACK state

4. CLIENT → SERVER: ACK
   - Client acknowledges server's FIN
   - Client enters TIME-WAIT state (2MSL)
   - Server enters CLOSED state
```

**TCP Flow Control:**

- **Window Size**: Amount of data receiver can accept
- **Sliding Window**: Window size adjusts based on receiver buffer
- **Zero Window**: Receiver sends window size = 0 to pause transmission

**TCP Congestion Control Algorithms:**

- **Slow Start**: Exponential increase in congestion window
- **Congestion Avoidance**: Linear increase after threshold
- **Fast Retransmit**: Retransmit after 3 duplicate ACKs
- **Fast Recovery**: Reduce congestion window by half

#### UDP (User Datagram Protocol) - RFC 768

**UDP Characteristics:**
- **Connectionless**: No connection establishment
- **Unreliable**: No delivery guarantees
- **Low overhead**: 8-byte header (vs 20-byte TCP)
- **No flow control or congestion control**
- **Used for**: DNS, DHCP, SNMP, streaming media

**UDP Header Structure (8 bytes):**

```
 0      7 8     15 16    23 24    31
+--------+--------+--------+--------+
|     Source      |   Destination   |
|      Port       |      Port       |
+--------+--------+--------+--------+
|                 |                 |
|     Length      |    Checksum     |
+--------+--------+--------+--------+
|                                   |
|            Data                   |
+-----------------------------------+
```

**When to Use TCP vs UDP:**

| TCP | UDP |
|-----|-----|
| HTTP, HTTPS, FTP, SSH, Telnet | DNS, DHCP, SNMP, TFTP |
| Email (SMTP, IMAP) | Streaming media (RTP) |
| Database connections | Real-time gaming |
| File transfers | VoIP (some implementations) |

#### ICMP (Internet Control Message Protocol) - RFC 792

**ICMP Functions:**
- Error reporting
- Network diagnostics
- Ping (Echo Request/Reply)
- Traceroute (TTL exceeded messages)

**Common ICMP Messages:**
- **Type 0**: Echo Reply (ping reply)
- **Type 3**: Destination Unreachable
- **Type 8**: Echo Request (ping)
- **Type 11**: Time Exceeded (traceroute)
- **Type 12**: Parameter Problem

#### ARP (Address Resolution Protocol) - RFC 826

**ARP Process:**

1. **Host A** wants to send packet to **Host B** (192.168.1.10)
2. **Host A** checks ARP cache for 192.168.1.10's MAC address
3. If not found, **Host A** broadcasts ARP Request:
   - "Who has 192.168.1.10? Tell 192.168.1.5"
4. **Host B** responds with ARP Reply:
   - "192.168.1.10 is at MAC-address-XX:XX:XX:XX:XX:XX"
5. **Host A** updates ARP cache and sends packet

**ARP Table Commands:**

```bash
# View ARP cache
arp -a                    # Windows/Linux
ip neigh show            # Linux (iproute2)
show ip arp              # Cisco IOS

# Delete ARP entry
arp -d 192.168.1.10      # Windows
sudo arp -d 192.168.1.10 # Linux
clear arp-cache          # Cisco IOS

# Add static ARP entry
arp -s 192.168.1.10 00-11-22-33-44-55  # Windows/Linux
arp 192.168.1.10 0011.2233.4455 ARPA  # Cisco IOS
```

### Protocol References

**RFC Documents:**
- **RFC 791**: Internet Protocol (IP)
- **RFC 792**: Internet Control Message Protocol (ICMP)
- **RFC 793**: Transmission Control Protocol (TCP)
- **RFC 768**: User Datagram Protocol (UDP)
- **RFC 826**: Ethernet Address Resolution Protocol (ARP)
- **RFC 2131**: Dynamic Host Configuration Protocol (DHCP)
- **RFC 1034/1035**: Domain Name System (DNS)
- **RFC 1918**: Address Allocation for Private Internets
- **RFC 2460**: Internet Protocol, Version 6 (IPv6)

**Trusted Online Resources:**
- IETF RFC Repository: https://www.ietf.org/standards/rfcs/
- Wireshark Protocol Reference: https://www.wireshark.org/docs/
- Cisco Documentation: https://www.cisco.com/c/en/us/support/index.html
- Network Encyclopedia: Various networking concepts and protocols

---