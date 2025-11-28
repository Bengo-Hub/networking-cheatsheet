# Virtual Network Device Software

**This section is part of the [Virtual Lab Setup Guide](../Virtual-Lab-Setup-Guide.md)**

---

## Virtual Network Device Software

### Router Virtualization Options

**1. VyOS (Open Source Router OS)**
- **Similar to**: Juniper JunOS, Cisco IOS-XE
- **Download**: https://github.com/vyos/vyos-rolling/releases
- **Format**: ISO or pre-built VM image
- **Resources**: 512 MB RAM, 1 vCPU, 2 GB disk
- **Features**: 
  - Full routing protocol support (OSPF, BGP, IS-IS)
  - MPLS support
  - VPN (IPsec, OpenVPN)
  - Firewall and NAT
  - **IPv6 Support**: Full IPv6 routing, OSPFv3, BGP IPv6, IS-IS IPv6

**VyOS Installation:**
```bash
# Download ISO
wget https://github.com/vyos/vyos-rolling/releases/download/current/vyos-1.4-rolling-amd64.iso

# Create VM in Proxmox/VMware:
# - 512 MB RAM
# - 1 vCPU
# - 2 GB disk
# - Boot from ISO
# - Install to disk
# - Default login: vyos/vyos
```

**2. FRR (Free Range Routing)**
- **Similar to**: Cisco IOS routing features
- **Installation**: Linux-based (Ubuntu/Debian)
- **Resources**: 1 GB RAM, 1 vCPU, 5 GB disk
- **Features**: OSPF, BGP, IS-IS, RIP, EIGRP (partial)
- **IPv6 Support**: OSPFv3, BGP IPv6, IS-IS IPv6, RIPng

**FRR Installation (Ubuntu VM):**
```bash
# Install Ubuntu Server 22.04
# Then install FRR
sudo apt update
sudo apt install frr frr-pythontools

# Enable routing protocols
sudo sed -i 's/bgpd=no/bgpd=yes/' /etc/frr/daemons
sudo sed -i 's/ospfd=no/ospfd=yes/' /etc/frr/daemons
sudo sed -i 's/ospf6d=no/ospf6d=yes/' /etc/frr/daemons  # IPv6 OSPF
sudo systemctl restart frr
```

**3. Cisco CSR 1000v (Virtual Router)**
- **Similar to**: Cisco IOS-XE
- **Download**: Requires Cisco account (Cisco VIRL/CML)
- **Resources**: 2 GB RAM, 2 vCPUs, 8 GB disk
- **Features**: Full Cisco IOS-XE feature set
- **IPv6 Support**: Full IPv6 support

**4. Juniper vMX (Virtual Router)**
- **Similar to**: Juniper MX series
- **Download**: Requires Juniper account
- **Resources**: 4 GB RAM, 2 vCPUs, 8 GB disk
- **Features**: Full Junos feature set
- **IPv6 Support**: Full IPv6 support

### Switch Virtualization Options

**1. Open vSwitch (OVS)**
- **Similar to**: Standard Layer 2 switch
- **Installation**: Linux-based
- **Resources**: 512 MB RAM, 1 vCPU, 2 GB disk
- **Features**: VLANs, STP, LACP, OpenFlow
- **IPv6 Support**: IPv6 routing, IPv6 VLANs

**OVS Installation:**
```bash
# Ubuntu/Debian
sudo apt install openvswitch-switch openvswitch-common

# Basic configuration
sudo ovs-vsctl add-br br0
sudo ovs-vsctl add-port br0 eth0
```

**2. Cisco IOU/IOL (IOS on Unix/Linux)**
- **Similar to**: Cisco IOS switches
- **Download**: Requires Cisco Learning Network account
- **Resources**: 256 MB RAM, 1 vCPU, 100 MB disk
- **Features**: Full Cisco switch feature set
- **IPv6 Support**: IPv6 switching and routing

**3. Arista vEOS (Virtual EOS)**
- **Similar to**: Arista switches
- **Download**: Requires Arista account
- **Resources**: 2 GB RAM, 2 vCPUs, 4 GB disk
- **IPv6 Support**: Full IPv6 support

### Firewall Virtualization Options

**1. pfSense (Open Source Firewall)**
- **Similar to**: Commercial firewalls (Check Point, Fortinet)
- **Download**: https://www.pfsense.org/download/
- **Resources**: 1 GB RAM, 1 vCPU, 8 GB disk
- **Features**: 
  - Stateful firewall
  - VPN (IPsec, OpenVPN, WireGuard)
  - IDS/IPS (Suricata, Snort)
  - Traffic shaping
  - Web proxy
- **IPv6 Support**: Full IPv6 firewall, NAT64, 464XLAT

**pfSense Installation:**
```bash
# Download ISO
# Create VM:
# - 1 GB RAM minimum
# - 1 vCPU
# - 8 GB disk
# - 2 network adapters (WAN, LAN)
# - Boot from ISO and install
```

**2. OPNsense (pfSense Fork)**
- **Similar to**: pfSense with modern UI
- **Download**: https://opnsense.org/download/
- **Resources**: 1 GB RAM, 1 vCPU, 8 GB disk
- **IPv6 Support**: Full IPv6 support, NAT64

**3. VyOS (Router with Firewall)**
- Can function as firewall with zone-based firewall
- See router section above
- **IPv6 Support**: IPv6 firewall rules

**4. Linux iptables/nftables**
- **Similar to**: Basic packet filtering
- **Installation**: Any Linux distribution
- **Resources**: 512 MB RAM, 1 vCPU, 2 GB disk
- **IPv6 Support**: ip6tables, nftables IPv6

### GNS3 and EVE-NG (Network Emulation Platforms)

**GNS3 (Graphical Network Simulator)**
- **Purpose**: Network topology design and emulation
- **Download**: https://www.gns3.com/
- **Supports**: 
  - Cisco IOU/IOL
  - Cisco VIRL images
  - VyOS, FRR
  - VirtualBox, VMware, QEMU integration
- **IPv6 Support**: Full IPv6 emulation support

**GNS3 Installation:**
```bash
# Linux
sudo add-apt-repository ppa:gns3/ppa
sudo apt update
sudo apt install gns3-gui gns3-server

# Windows/Mac: Download installer from website
```

**EVE-NG (Emulated Virtual Environment)**
- **Purpose**: Professional network emulation
- **Download**: https://www.eve-ng.net/
- **Format**: OVA for VMware/Proxmox
- **Resources**: 8 GB RAM, 4 vCPUs, 50 GB disk minimum
- **Supports**: All major vendor images
- **IPv6 Support**: Full IPv6 emulation support

**EVE-NG Installation on Proxmox:**
1. Download EVE-NG OVA
2. Convert OVA to Proxmox format:
```bash
# Install qemu-img tools
apt install qemu-utils

# Convert OVA
tar -xvf EVE-NG.ova
qemu-img convert -f vmdk -O qcow2 disk1.vmdk eve-ng.qcow2

# Upload to Proxmox and create VM
```

**EVE-NG Installation on VMware:**
1. File → Deploy OVF Template
2. Select EVE-NG OVA file
3. Configure resources (8 GB RAM, 4 vCPUs)
4. Power on and access web UI: https://IP_ADDRESS

---

## Related Documentation

- For router configuration examples, see: [Configuration Cheatsheet](../Configuration-Cheatsheet.md)
- For IPv6 implementation, see: [IPv6 Workshop Guide](../IPv6-Workshop-Guide.md)
- For lab topologies, see: [Lab Topology Examples](lab-topologies.md)
- For IPv6 migration tools, see: [IPv6 Migration Tools](ipv6-migration-tools.md)

