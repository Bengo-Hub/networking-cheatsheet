# VMware Setup for Virtual Networking Labs

**This section is part of the [Virtual Lab Setup Guide](../Virtual-Lab-Setup-Guide.md)**

---

## VMware Setup (PC/Desktop)

### VMware Workstation/Player Installation

**Step 1: Download VMware**
- **VMware Workstation Pro**: https://www.vmware.com/products/workstation-pro.html
  - Paid license required
  - Advanced features (snapshots, cloning, teams)
- **VMware Workstation Player**: https://www.vmware.com/products/workstation-player.html
  - Free for personal use
  - Basic virtualization features

**Step 2: Install VMware**
1. Run installer
2. Follow installation wizard
3. Accept license agreement
4. Choose installation location
5. Complete installation and restart

**Step 3: Enable Virtualization**
- Ensure BIOS/UEFI settings:
  - Intel: Enable "Intel Virtualization Technology (VT-x)"
  - AMD: Enable "AMD-V" or "SVM"
- Enable "Virtualization Based Security" in Windows (if applicable)

### VMware Network Configuration

**Default Virtual Networks:**
- **VMnet0 (Bridged)**: Direct connection to physical network
- **VMnet1 (Host-only)**: Isolated network, host can access
- **VMnet8 (NAT)**: Network Address Translation

**Create Custom Virtual Networks:**

1. **Edit → Virtual Network Editor** (requires admin rights)
2. **Add Network:**
   - VMnet2: Host-only (192.168.100.0/24) - Management
   - VMnet3: Host-only (192.168.200.0/24) - Lab Network 1
   - VMnet4: Host-only (192.168.300.0/24) - Lab Network 2
   - VMnet5: NAT (10.0.0.0/24) - Internet simulation

**Network Configuration Example:**
```
VMnet2 (Host-only):
  Subnet: 192.168.100.0
  Subnet mask: 255.255.255.0
  DHCP: Enabled (192.168.100.128-192.168.100.254)
```

**VMware Network Adapter Types:**
- **Bridged**: VM appears as separate device on physical network
- **NAT**: VM shares host's IP, can access internet
- **Host-only**: Isolated network, no internet access
- **Custom**: Connect to specific VMnet

### VMware Optimization Settings

**VMware Settings:**
1. **Edit → Preferences:**
   - Memory: Reserve enough for host OS
   - Processors: Enable "Virtualize Intel VT-x/EPT"
   - Display: Optimize for performance

2. **VM Settings (per VM):**
   - **Processors:**
     - Number of processors: 2-4
     - Enable "Virtualize Intel VT-x/EPT"
   - **Memory:**
     - Allocate based on device requirements
   - **Hard Disk:**
     - Type: SCSI (recommended) or SATA
     - Disk size: Based on requirements
   - **Network Adapter:**
     - Adapter type: VMXNET3 (best performance)
     - Network connection: Custom (select VMnet)

**Performance Tips:**
- Use SSD for VM storage
- Allocate sufficient RAM (avoid swapping)
- Enable hardware acceleration
- Use VMXNET3 network adapters
- Disable unnecessary services in VMs

### VMware VM Template Creation

**Create Template VM:**
1. Install OS (Ubuntu Server, VyOS, etc.)
2. Configure basic settings
3. Install VMware Tools
4. Shut down VM
5. Right-click → Manage → Clone
6. Select "Create a full clone"
7. Use cloned VM as template

---

## Related Documentation

- For hardware requirements, see: [Hardware Requirements](hardware-requirements.md)
- For Proxmox setup, see: [Proxmox Setup Guide](proxmox-setup.md)
- For virtual device software, see: [Virtual Network Device Software](virtual-device-software.md)
- For troubleshooting, see: [Troubleshooting Virtual Labs](troubleshooting.md)

