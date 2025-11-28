# Networking Cheatsheet

A comprehensive collection of networking documentation covering router configurations, IPv6 implementation, networking principles, and lab resources.

## Quick Start

This repository is organized into two main categories:

1. **Main Guides**: Comprehensive documentation files
   - [Networking Principles Guide](Networking-Principles.md) - **Start here for learning networking**
   - [Virtual Lab Setup Guide](docs/Virtual-Lab-Setup-Guide.md) - **Complete guide for setting up virtual networking labs**
   - [Router Configuration Cheatsheet](docs/Configuration-Cheatsheet.md) - Router configuration commands
   - [IPv6 Workshop Guide](docs/IPv6-Workshop-Guide.md) - IPv6 implementation guide
   - [Test Lab Addresses](docs/Test-Lab-Addresses.md) - Lab address allocations

2. **Organized Sections**: Detailed subsections of the Networking Principles Guide
   - Beginner, Intermediate, Expert levels
   - Core Telco, Enterprise, End-User domains
   - Security, Troubleshooting, Emerging Technologies

## Main Documentation Files

### 📚 [Networking Principles Guide](Networking-Principles.md)

**The main guide covering networking from beginner to expert levels.**

A progressive, comprehensive guide organized by skill level and domain:
- **[Beginner Level](beginner/fundamentals.md)**: Fundamentals, OSI/TCP-IP models, basic protocols
- **[Intermediate Level](intermediate/concepts.md)**: Routing, switching, WAN technologies, QoS
- **[Expert Level](expert/advanced-topics.md)**: MPLS, SDN, NFV, network virtualization
- **[Core Telecommunications](core-telco/telecommunications.md)**: Telecom architecture, RAN, core networks
- **[Enterprise Networking](enterprise/enterprise-networking.md)**: Enterprise design, security, automation
- **[End-User Networking](end-user/end-user-networking.md)**: Home, SOHO, IoT networking
- **[Security Principles](security/security-principles.md)**: Network security fundamentals
- **[Troubleshooting](troubleshooting/troubleshooting.md)**: Problem-solving and optimization
- **[Emerging Technologies](emerging-technologies/emerging-technologies.md)**: Future trends and innovations

### 🖥️ [Virtual Lab Setup Guide](docs/Virtual-Lab-Setup-Guide.md)

**Complete guide for setting up virtual networking labs with Proxmox and VMware.**

- Hardware requirements and resource planning
- Proxmox VE installation and configuration (test servers)
- VMware Workstation/Player setup (PC/desktop)
- Virtual network device software (routers, switches, firewalls)
- IPv6 migration tools (Jool, TAYGA, 464XLAT, MAP-T/MAP-E)
- Lab topologies for core telco, enterprise, and end-user networks
- Troubleshooting and best practices

**Perfect for hands-on learning and testing network configurations.**

### 🔧 [Router Configuration Cheatsheet](docs/Configuration-Cheatsheet.md)

**Practical router configuration commands and examples.**

- Cisco IOS configuration (FRR/Quagga)
- Juniper/VyOS configuration commands
- IS-IS routing protocol setup
- Interface and loopback configuration examples
- Dual-stack (IPv4/IPv6) configurations

### 🌐 [IPv6 Workshop Guide](docs/IPv6-Workshop-Guide.md)

**Comprehensive IPv6 implementation guide.**

- IPv6 policy and planning phases
- Core network deployment with IS-IS
- Enterprise network deployment strategies
- End-user network configuration
- Hands-on lab exercises
- Transition strategies (dual-stack, NAT64/DNS64)

### 🧪 [Test Lab Address Allocation](docs/Test-Lab-Addresses.md)

**Address allocation tables for test lab environments.**

- IPv4 address blocks (172.16.0.0/22)
- IPv6 address blocks (2001:db8:1::/48)
- Router loopback addresses (R1-R50)
- Interface address tables
- IS-IS NET address generation

## Repository Structure

```
networking-cheatsheet/
├── Networking-Principles.md          # Main guide (links to all sections)
├── README.md                          # This file
│
├── beginner/                          # Beginner level content
│   └── fundamentals.md
├── intermediate/                      # Intermediate level content
│   └── concepts.md
├── expert/                            # Expert level content
│   └── advanced-topics.md
├── core-telco/                        # Telecommunications networking
│   └── telecommunications.md
├── enterprise/                        # Enterprise networking
│   └── enterprise-networking.md
├── end-user/                          # End-user networking
│   └── end-user-networking.md
├── security/                          # Network security
│   └── security-principles.md
├── troubleshooting/                   # Troubleshooting guide
│   └── troubleshooting.md
├── emerging-technologies/             # Future trends
│   └── emerging-technologies.md
│
└── docs/                              # Configuration and reference docs
    ├── Virtual-Lab-Setup-Guide.md     # Virtual lab setup guide
    ├── lab-setup/                      # Lab setup sections
    │   ├── hardware-requirements.md
    │   ├── proxmox-setup.md
    │   ├── vmware-setup.md
    │   ├── virtual-device-software.md
    │   ├── ipv6-migration-tools.md
    │   ├── lab-topologies.md
    │   ├── troubleshooting.md
    │   └── best-practices.md
    ├── Configuration-Cheatsheet.md
    ├── IPv6-Workshop-Guide.md
    └── Test-Lab-Addresses.md
```

## How to Use This Repository

### For Beginners

1. Start with **[Networking Principles Guide](Networking-Principles.md)**
2. Read through **[Beginner Level Fundamentals](beginner/fundamentals.md)**
3. Set up a virtual lab using **[Virtual Lab Setup Guide](docs/Virtual-Lab-Setup-Guide.md)**
4. Practice with **[Router Configuration Cheatsheet](docs/Configuration-Cheatsheet.md)**
5. Use **[Test Lab Addresses](docs/Test-Lab-Addresses.md)** for IP planning

### For Intermediate Learners

1. Review **[Intermediate Level Concepts](intermediate/concepts.md)**
2. Study **[Enterprise Networking](enterprise/enterprise-networking.md)**
3. Practice IPv6 with **[IPv6 Workshop Guide](docs/IPv6-Workshop-Guide.md)**
4. Learn troubleshooting techniques

### For Experts

1. Deep dive into **[Expert Level Advanced Topics](expert/advanced-topics.md)**
2. Study **[Core Telecommunications Networking](core-telco/telecommunications.md)**
3. Explore **[Emerging Technologies](emerging-technologies/emerging-technologies.md)**
4. Implement advanced configurations

### For Specific Use Cases

- **Virtual Lab Setup**: Follow [Virtual Lab Setup Guide](docs/Virtual-Lab-Setup-Guide.md)
- **Router Configuration**: See [Configuration Cheatsheet](docs/Configuration-Cheatsheet.md)
- **IPv6 Deployment**: Follow [IPv6 Workshop Guide](docs/IPv6-Workshop-Guide.md)
- **IPv6 Migration Tools**: See [IPv6 Migration Tools](docs/lab-setup/ipv6-migration-tools.md)
- **Lab Address Planning**: Reference [Test Lab Addresses](docs/Test-Lab-Addresses.md)
- **Network Security**: Read [Security Principles](security/security-principles.md)
- **Problem Solving**: Check [Troubleshooting Guide](troubleshooting/troubleshooting.md)

## Purpose

This repository serves as a reference and educational resource for:

- Network engineers configuring routers and switches
- IPv6 implementation teams
- Students learning networking fundamentals
- Professionals preparing for networking certifications
- Anyone interested in understanding modern networking principles

## Key Features

✅ **Progressive Learning Path**: From beginner to expert levels  
✅ **Domain Coverage**: Core telco, enterprise, and end-user networking  
✅ **Practical Examples**: Real configuration commands and examples  
✅ **Virtual Lab Setup**: Complete guide for Proxmox and VMware environments  
✅ **IPv6 Migration Tools**: Open-source tools for IPv6 transition  
✅ **Lab Resources**: Complete address allocation for test environments  
✅ **Cross-Referenced**: Links between related topics and documents  
✅ **Comprehensive**: Covers theory, implementation, and troubleshooting  

## Contributing

Contributions are welcome! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### Areas for Contribution

- Additional router/switch configuration examples
- IPv6 deployment strategies and best practices
- Networking fundamentals and educational content
- Lab setup guides and troubleshooting tips
- Security best practices
- Network design principles

## License

See [LICENSE](LICENSE) file for details.

## Disclaimer

The configuration examples and addresses in this repository are intended for educational and lab purposes. Always verify configurations in a non-production environment before deploying to production networks.

---

**Quick Links**: [Main Guide](Networking-Principles.md) | [Virtual Lab Setup](docs/Virtual-Lab-Setup-Guide.md) | [Config Cheatsheet](docs/Configuration-Cheatsheet.md) | [IPv6 Guide](docs/IPv6-Workshop-Guide.md) | [Lab Addresses](docs/Test-Lab-Addresses.md)
