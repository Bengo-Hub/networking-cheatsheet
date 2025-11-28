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

**DHCP (Dynamic Host Configuration Protocol):**
- Automatically assigns IP addresses and network configuration (ports 67/68)
- DORA process: Discover, Offer, Request, Acknowledge
- Lease time management
- DHCP relay agents

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