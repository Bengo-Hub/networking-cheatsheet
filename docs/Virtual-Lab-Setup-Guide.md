# Virtual Networking Lab Setup Guide
## Complete Guide for Proxmox and VMware Environments

---

## Table of Contents

1. [Introduction](#introduction)
2. [Hardware Requirements](lab-setup/hardware-requirements.md)
3. [Proxmox Setup (Test Server)](lab-setup/proxmox-setup.md)
4. [VMware Setup (PC/Desktop)](lab-setup/vmware-setup.md)
5. [Virtual Network Device Software](lab-setup/virtual-device-software.md)
6. [IPv6 Migration Tools](lab-setup/ipv6-migration-tools.md)
7. [Network Topology Examples](lab-setup/lab-topologies.md)
8. [Troubleshooting Virtual Labs](lab-setup/troubleshooting.md)
9. [Best Practices](lab-setup/best-practices.md)
10. [References](#references)

---

## Introduction

This guide provides step-by-step instructions for setting up comprehensive virtual networking labs using Proxmox (for test servers) and VMware (for personal computers). These labs enable hands-on practice with routers, switches, firewalls, and end devices that closely simulate real-world vendor equipment.

**What You'll Learn:**
- Setting up Proxmox VE on a test server
- Configuring VMware Workstation/Player on a PC
- Deploying virtual network devices (routers, switches, firewalls)
- Creating realistic network topologies for different scenarios
- Optimizing performance and resource allocation
- Using IPv6 migration tools and transition mechanisms

**Lab Scenarios Covered:**
- **Core Telecommunications**: Service provider networks, MPLS, BGP
- **Enterprise Networks**: Campus networks, data centers, WAN connectivity
- **End-User Networks**: Home networks, SOHO, IoT environments

**Prerequisites:**
- Basic understanding of networking concepts (see [Networking Principles](../Networking-Principles.md))
- Familiarity with Linux command line (for Proxmox)
- Understanding of virtualization concepts

---

## Quick Start Guide

### For Proxmox (Test Server)

1. **Check Hardware Requirements**: See [Hardware Requirements](lab-setup/hardware-requirements.md)
2. **Install Proxmox VE**: Follow [Proxmox Setup Guide](lab-setup/proxmox-setup.md)
3. **Deploy Virtual Devices**: See [Virtual Network Device Software](lab-setup/virtual-device-software.md)
4. **Create Lab Topology**: See [Network Topology Examples](lab-setup/lab-topologies.md)

### For VMware (PC/Desktop)

1. **Check Hardware Requirements**: See [Hardware Requirements](lab-setup/hardware-requirements.md)
2. **Install VMware**: Follow [VMware Setup Guide](lab-setup/vmware-setup.md)
3. **Deploy Virtual Devices**: See [Virtual Network Device Software](lab-setup/virtual-device-software.md)
4. **Create Lab Topology**: See [Network Topology Examples](lab-setup/lab-topologies.md)

---

## Section Overview

### [Hardware Requirements](lab-setup/hardware-requirements.md)

Covers minimum and recommended hardware specifications for both Proxmox and VMware environments, resource allocation guidelines, and virtualization support requirements.

**Key Topics:**
- Minimum vs. Recommended Requirements
- Resource Allocation per Device Type
- Virtualization Support Verification

### [Proxmox Setup](lab-setup/proxmox-setup.md)

Complete guide for installing and configuring Proxmox VE on a test server, including network configuration, storage setup, and optimization.

**Key Topics:**
- Proxmox VE Installation
- Network Bridge Configuration
- Virtual Device Image Upload
- Performance Optimization

### [VMware Setup](lab-setup/vmware-setup.md)

Step-by-step instructions for setting up VMware Workstation/Player on a PC or desktop, including network configuration and optimization.

**Key Topics:**
- VMware Installation
- Virtual Network Configuration
- VM Template Creation
- Performance Tuning

### [Virtual Network Device Software](lab-setup/virtual-device-software.md)

Comprehensive overview of virtual router, switch, and firewall software options, including installation and configuration examples.

**Key Topics:**
- Router Virtualization (VyOS, FRR, Cisco CSR, Juniper vMX)
- Switch Virtualization (Open vSwitch, Cisco IOU, Arista vEOS)
- Firewall Virtualization (pfSense, OPNsense, VyOS)
- Network Emulation Platforms (GNS3, EVE-NG)

### [IPv6 Migration Tools](lab-setup/ipv6-migration-tools.md)

Detailed guide to open-source IPv6 transition mechanisms, testing tools, and migration software for IPv6 deployment.

**Key Topics:**
- NAT64/SIIT (Jool, TAYGA)
- 464XLAT Implementation
- MAP-T/MAP-E
- IPv6 Testing Tools (ping6, traceroute6, mtr6, ndisc6)
- IPv6 Migration Software (DHCPv6, RADVD, BIND9, FRR IPv6)

### [Network Topology Examples](lab-setup/lab-topologies.md)

Complete lab topologies for core telecommunications, enterprise, and end-user networking scenarios with configuration examples.

**Key Topics:**
- Core Telco Lab (MPLS, BGP VPN)
- Enterprise Lab (Three-Tier Design)
- End-User Lab (Home Network, IoT)
- Lab Size Examples (Small, Medium, Large)

### [Troubleshooting Virtual Labs](lab-setup/troubleshooting.md)

Common issues and solutions for virtual lab environments, performance optimization, and network troubleshooting.

**Key Topics:**
- Common VM Issues
- Network Connectivity Problems
- Performance Optimization
- IPv6-Specific Troubleshooting

### [Best Practices](lab-setup/best-practices.md)

Best practices for lab organization, resource management, network design, security, and documentation.

**Key Topics:**
- Naming Conventions
- IP Addressing Schemes
- Resource Management
- Backup and Recovery
- Security Best Practices

---

## Integration with Other Documentation

This lab setup guide integrates with other documentation in this repository:

### Related Guides

- **[Networking Principles](../Networking-Principles.md)**: Core networking concepts and fundamentals
- **[Configuration Cheatsheet](../Configuration-Cheatsheet.md)**: Router and switch configuration commands
- **[IPv6 Workshop Guide](../IPv6-Workshop-Guide.md)**: Comprehensive IPv6 implementation guide
- **[Test Lab Addresses](../Test-Lab-Addresses.md)**: IP address allocation tables for lab environments

### Networking Concepts

- **[Beginner Fundamentals](../beginner/fundamentals.md)**: Basic networking concepts, OSI model, IP addressing
- **[Intermediate Concepts](../intermediate/concepts.md)**: VLANs, STP, routing protocols, WAN technologies
- **[Expert Advanced Topics](../expert/advanced-topics.md)**: Advanced OSPF, BGP, MPLS, SDN, NFV

### Domain-Specific Networking

- **[Core Telecommunications](../core-telco/telecommunications.md)**: Service provider networking, 5G, transport networks
- **[Enterprise Networking](../enterprise/enterprise-networking.md)**: Campus networks, data centers, enterprise security
- **[End-User Networking](../end-user/end-user-networking.md)**: Home networks, SOHO, IoT networking

### Security and Troubleshooting

- **[Security Principles](../security/security-principles.md)**: Network security, firewalls, VPNs, encryption
- **[Troubleshooting](../troubleshooting/troubleshooting.md)**: Network troubleshooting methodology and tools

### Emerging Technologies

- **[Emerging Technologies](../emerging-technologies/emerging-technologies.md)**: 6G, quantum networking, edge computing, IPv6 evolution

---

## Lab Scenarios by Networking Domain

### Core Telecommunications Labs

**Use Cases:**
- Service Provider Network Simulation
- MPLS VPN Configuration
- BGP Route Reflection
- IS-IS Core Routing

**Recommended Setup:**
- Proxmox on test server
- 4-6 Provider Routers (VyOS or FRR)
- MPLS-enabled topology
- See [Core Telco Lab Topology](lab-setup/lab-topologies.md#core-telecommunications-lab-setup)

**Related Documentation:**
- [Core Telecommunications Networking](../core-telco/telecommunications.md)
- [Advanced Routing Topics](../expert/advanced-topics.md)
- [Configuration Cheatsheet](../Configuration-Cheatsheet.md)

### Enterprise Network Labs

**Use Cases:**
- Three-Tier Hierarchical Design
- VLAN Configuration
- Inter-VLAN Routing
- Enterprise Security Policies

**Recommended Setup:**
- VMware on PC/Desktop or Proxmox
- 2-4 Routers (VyOS)
- 2-4 Switches (Open vSwitch)
- 1-2 Firewalls (pfSense)
- Multiple end devices

**Related Documentation:**
- [Enterprise Networking](../enterprise/enterprise-networking.md)
- [Intermediate Concepts](../intermediate/concepts.md)
- [Security Principles](../security/security-principles.md)

### End-User Network Labs

**Use Cases:**
- Home Network Configuration
- IoT Network Segmentation
- SOHO Network Setup
- Guest Network Isolation

**Recommended Setup:**
- VMware on PC/Desktop
- 1 Router (VyOS or pfSense)
- 1 Switch (Open vSwitch)
- Multiple end devices

**Related Documentation:**
- [End-User Networking](../end-user/end-user-networking.md)
- [Beginner Fundamentals](../beginner/fundamentals.md)

### IPv6 Migration Labs

**Use Cases:**
- Dual-Stack Configuration
- NAT64 Deployment
- IPv6-only Network Testing
- 464XLAT Implementation

**Recommended Setup:**
- Proxmox or VMware
- Routers with IPv6 support (VyOS, FRR)
- NAT64 gateway (Jool or TAYGA)
- IPv6-enabled end devices

**Related Documentation:**
- [IPv6 Workshop Guide](../IPv6-Workshop-Guide.md)
- [IPv6 Migration Tools](lab-setup/ipv6-migration-tools.md)
- [Emerging Technologies](../emerging-technologies/emerging-technologies.md)

---

## Getting Started Checklist

### Pre-Installation

- [ ] Review [Hardware Requirements](lab-setup/hardware-requirements.md)
- [ ] Verify virtualization support in BIOS/UEFI
- [ ] Choose virtualization platform (Proxmox or VMware)
- [ ] Plan lab topology and resource allocation

### Installation

- [ ] Install Proxmox VE or VMware (see respective setup guides)
- [ ] Configure network bridges/VMnets
- [ ] Upload virtual device images
- [ ] Create VM templates

### Lab Setup

- [ ] Deploy virtual devices according to topology
- [ ] Configure network interfaces
- [ ] Set up routing protocols
- [ ] Configure security policies
- [ ] Test connectivity

### Documentation

- [ ] Document network topology
- [ ] Record IP address allocations
- [ ] Document configurations
- [ ] Create network diagrams

---

## References

### Virtualization Platforms

- **Proxmox VE**: https://www.proxmox.com/
- **VMware Workstation**: https://www.vmware.com/products/workstation-pro.html
- **VMware Player**: https://www.vmware.com/products/workstation-player.html

### Virtual Network Devices

- **VyOS**: https://github.com/vyos/vyos-rolling/releases
- **FRR**: https://frrouting.org/
- **pfSense**: https://www.pfsense.org/
- **OPNsense**: https://opnsense.org/
- **Open vSwitch**: https://www.openvswitch.org/
- **GNS3**: https://www.gns3.com/
- **EVE-NG**: https://www.eve-ng.net/

### IPv6 Migration Tools

- **Jool**: https://www.jool.mx/
- **TAYGA**: https://github.com/fwdillema/tayga
- **clatd**: https://github.com/toreanderson/clatd

### Standards and RFCs

- **RFC 6146**: Stateful NAT64
- **RFC 7915**: IP/ICMP Translation Algorithm (SIIT)
- **RFC 6877**: 464XLAT
- **RFC 7599**: MAP-T
- **RFC 7597**: MAP-E

### Related Documentation

- [Networking Principles](../Networking-Principles.md)
- [Configuration Cheatsheet](../Configuration-Cheatsheet.md)
- [IPv6 Workshop Guide](../IPv6-Workshop-Guide.md)
- [Test Lab Addresses](../Test-Lab-Addresses.md)

---

## Support and Contributions

For issues, questions, or contributions related to this lab setup guide:

1. Review the [Troubleshooting](lab-setup/troubleshooting.md) section
2. Check related documentation sections
3. Refer to vendor documentation for specific devices
4. Consult RFC documents for protocol details

---

**Last Updated**: 2025-01-27

**Version**: 2.0
