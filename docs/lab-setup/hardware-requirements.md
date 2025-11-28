# Hardware Requirements for Virtual Networking Labs

**This section is part of the [Virtual Lab Setup Guide](../Virtual-Lab-Setup-Guide.md)**

---

## Hardware Requirements

### Minimum Requirements (Basic Lab)

**For VMware on PC/Desktop:**
- **CPU**: Intel Core i5 (4 cores) or AMD Ryzen 5 (4 cores) - 64-bit
- **RAM**: 16 GB (8 GB for host, 8 GB for VMs)
- **Storage**: 100 GB free space (SSD recommended)
- **Network**: Gigabit Ethernet adapter
- **OS**: Windows 10/11, Linux, or macOS

**For Proxmox on Test Server:**
- **CPU**: Intel Xeon or AMD EPYC (8+ cores recommended)
- **RAM**: 32 GB (16 GB minimum)
- **Storage**: 200 GB+ (SSD recommended for better performance)
- **Network**: Gigabit or 10 Gigabit Ethernet
- **Virtualization Support**: Intel VT-x/AMD-V enabled in BIOS

### Recommended Requirements (Advanced Lab)

**For VMware on PC/Desktop:**
- **CPU**: Intel Core i7/i9 (8+ cores) or AMD Ryzen 7/9 (8+ cores)
- **RAM**: 32 GB or more
- **Storage**: 500 GB+ NVMe SSD
- **Network**: 2.5 Gbps or 10 Gbps Ethernet
- **GPU**: Optional (for GPU passthrough if needed)

**For Proxmox on Test Server:**
- **CPU**: Intel Xeon (16+ cores) or AMD EPYC (16+ cores)
- **RAM**: 64 GB or more
- **Storage**: 1 TB+ NVMe SSD or enterprise SSD
- **Network**: 10 Gigabit Ethernet (multiple interfaces)
- **RAID**: Hardware RAID controller (optional, for redundancy)

### Resource Allocation Guidelines

**Per Virtual Router/Switch:**
- **CPU**: 1-2 vCPUs
- **RAM**: 512 MB - 2 GB (depending on device type)
- **Storage**: 1-4 GB (for OS images)

**Per Firewall:**
- **CPU**: 2-4 vCPUs
- **RAM**: 2-4 GB
- **Storage**: 8-20 GB

**Per End Device (Linux/Windows):**
- **CPU**: 1-2 vCPUs
- **RAM**: 1-4 GB
- **Storage**: 10-50 GB

**Example Lab Resource Planning:**
- Small Lab (5 routers, 2 switches, 1 firewall, 3 end devices):
  - Total RAM: ~12-16 GB
  - Total Storage: ~50 GB
  - Total vCPUs: ~15-20

- Medium Lab (10 routers, 5 switches, 2 firewalls, 10 end devices):
  - Total RAM: ~32-48 GB
  - Total Storage: ~150 GB
  - Total vCPUs: ~40-50

- Large Lab (20 routers, 10 switches, 4 firewalls, 20 end devices):
  - Total RAM: ~64-96 GB
  - Total Storage: ~300 GB
  - Total vCPUs: ~80-100

### Virtualization Support Requirements

**BIOS/UEFI Settings:**
- **Intel Processors**: Enable "Intel Virtualization Technology (VT-x)"
- **AMD Processors**: Enable "AMD-V" or "SVM Mode"
- **IOMMU/VT-d**: Enable for device passthrough (optional)

**Verification:**
```bash
# Linux: Check CPU virtualization support
egrep -c '(vmx|svm)' /proc/cpuinfo

# Windows: Check via System Information
# System Information → System Summary → Processor
# Look for "Virtualization Enabled"
```

---

## Related Documentation

- For Proxmox setup, see: [Proxmox Setup Guide](proxmox-setup.md)
- For VMware setup, see: [VMware Setup Guide](vmware-setup.md)
- For virtual device software, see: [Virtual Network Device Software](virtual-device-software.md)
- For lab topology examples, see: [Lab Topology Examples](lab-topologies.md)

