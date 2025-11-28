# Proxmox Setup for Virtual Networking Labs

**This section is part of the [Virtual Lab Setup Guide](../Virtual-Lab-Setup-Guide.md)**

---

## Proxmox Setup (Test Server)

### Proxmox VE Installation

**Step 1: Download Proxmox VE**
- Download ISO from: https://www.proxmox.com/en/downloads
- Latest stable version recommended (Proxmox VE 8.x)

**Step 2: Create Bootable USB**
```bash
# Linux/Mac
dd if=proxmox-ve_8.x.iso of=/dev/sdX bs=4M status=progress

# Windows: Use Rufus or similar tool
# Download Rufus: https://rufus.ie/
```

**Step 3: Install Proxmox VE**
1. Boot from USB drive
2. Select "Install Proxmox VE"
3. Accept license agreement
4. Select target disk (SSD recommended)
5. Configure:
   - Country/Timezone
   - Keyboard layout
   - Password (root password)
   - Network:
     - Hostname (e.g., proxmox-lab.local)
     - IP address (e.g., 192.168.100.10)
     - Gateway (e.g., 192.168.100.1)
     - DNS servers (e.g., 8.8.8.8, 1.1.1.1)
6. Review and confirm installation
7. Wait for installation to complete (~10-15 minutes)
8. Reboot and access web interface: https://IP_ADDRESS:8006

### Initial Proxmox Configuration

**Access Web Interface:**
- URL: `https://192.168.100.10:8006`
- Username: `root`
- Password: (set during installation)

**Configure Storage:**

1. **Add Local Storage (if needed):**
   - Datacenter → Storage → Add
   - Type: Directory
   - ID: local-vm
   - Path: `/var/lib/vz`
   - Content: Disk image, ISO image, Container template

2. **Add NFS/iSCSI Storage (optional):**
   - For shared storage across multiple Proxmox nodes
   - Useful for clustering

**Configure Network:**

1. **Create Virtual Networks:**
   - Datacenter → Network → Create
   - Create VLANs for lab segmentation:
     - `vmbr1`: Management network (VLAN 10)
     - `vmbr2`: Lab network 1 (VLAN 100)
     - `vmbr3`: Lab network 2 (VLAN 200)
     - `vmbr4`: WAN simulation (VLAN 1000)

2. **Bridge Configuration Example:**
```bash
# Edit /etc/network/interfaces
auto vmbr1
iface vmbr1 inet static
    address 192.168.10.1/24
    bridge-ports none
    bridge-stp off
    bridge-fd 0
```

**Enable Virtualization Features:**

```bash
# Check CPU virtualization support
egrep -c '(vmx|svm)' /proc/cpuinfo

# Enable nested virtualization (for running VMs inside VMs)
echo "options kvm-intel nested=1" >> /etc/modprobe.d/kvm.conf
# OR for AMD:
# echo "options kvm-amd nested=1" >> /etc/modprobe.d/kvm.conf

# Reboot to apply
reboot
```

### Upload Virtual Device Images

**Supported Formats:**
- QEMU/KVM images (.qcow2, .raw)
- ISO images for installation
- Container templates (LXC)

**Upload Process:**

1. **Via Web Interface:**
   - Select storage (local)
   - Upload → Select file
   - Upload router/switch/firewall images

2. **Via Command Line (SCP):**
```bash
# From your local machine
scp router-image.qcow2 root@192.168.100.10:/var/lib/vz/template/qemu/

# Or use Proxmox storage path
scp image.qcow2 root@192.168.100.10:/tmp/
# Then move to storage via web interface
```

**Common Virtual Device Images:**
- VyOS (router): https://github.com/vyos/vyos-rolling/releases
- pfSense (firewall): https://www.pfsense.org/download/
- OPNsense (firewall): https://opnsense.org/download/
- Linux VMs (Ubuntu, Debian, CentOS) for end devices

### Proxmox Optimization

**Performance Tuning:**

```bash
# Enable CPU governor for performance
echo performance > /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor

# Optimize I/O scheduler
echo deadline > /sys/block/sda/queue/scheduler

# Enable huge pages (for better memory performance)
echo 1024 > /proc/sys/vm/nr_hugepages
```

**VM Template Creation:**

1. **Create VyOS Router Template:**
   - Create VM in Proxmox
   - Name: vyos-router-template
   - OS: Linux 5.x
   - RAM: 512 MB
   - Disk: 2 GB
   - Network: vmbr1
   - Install VyOS from ISO
   - Configure basic settings
   - Convert to template: Right-click → Convert to Template

2. **Clone Templates for Lab:**
   - Right-click template → Clone
   - Configure unique hostname and IP
   - Start cloned VM

---

## Related Documentation

- For hardware requirements, see: [Hardware Requirements](hardware-requirements.md)
- For virtual device software, see: [Virtual Network Device Software](virtual-device-software.md)
- For lab topologies, see: [Lab Topology Examples](lab-topologies.md)
- For troubleshooting, see: [Troubleshooting Virtual Labs](troubleshooting.md)

