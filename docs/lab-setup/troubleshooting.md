# Troubleshooting Virtual Labs

**This section is part of the [Virtual Lab Setup Guide](../Virtual-Lab-Setup-Guide.md)**

---

## Troubleshooting Virtual Labs

### Common Issues

#### Issue 1: VMs Not Getting IP Addresses

**Symptoms:**
- VM shows "No IP address"
- Cannot ping gateway

**Solutions:**
```bash
# Check network adapter configuration
# Verify VMnet/VMbridge settings
# Check DHCP server (if using)
# Verify network adapter type (VMXNET3 recommended)

# On Linux VMs
sudo dhclient -v
sudo ip link show
sudo ip addr show

# Check DHCP server status
sudo systemctl status isc-dhcp-server

# Manually assign IP (temporary)
sudo ip addr add 192.168.1.100/24 dev eth0
sudo ip link set eth0 up
```

#### Issue 2: Cannot Connect Between VMs

**Symptoms:**
- VMs on same network cannot ping each other
- Routing not working

**Solutions:**
```bash
# Verify network configuration
# Check firewall rules (iptables/ufw)
# Verify routing tables
ip route show
# Check ARP table
arp -a

# On VyOS
show ip route
show interfaces
ping <destination>

# Check firewall on Linux VMs
sudo ufw status
sudo iptables -L

# Disable firewall temporarily for testing
sudo ufw disable
```

#### Issue 3: High CPU Usage

**Symptoms:**
- Host system slow
- VMs unresponsive

**Solutions:**
- Reduce number of running VMs
- Lower vCPU allocation
- Enable CPU limits in Proxmox
- Check for CPU-intensive processes in VMs
- Use CPU pinning for critical VMs

**Proxmox CPU Limits:**
```bash
# Set CPU limit via web interface
# VM → Options → CPU → Limit to 50% (for example)
```

**VMware CPU Limits:**
- VM Settings → Processors → Limit CPU usage

#### Issue 4: Out of Memory

**Symptoms:**
- VMs fail to start
- Host system swapping

**Solutions:**
- Reduce VM memory allocation
- Enable memory ballooning (Proxmox)
- Close unnecessary VMs
- Add more RAM to host

**Proxmox Memory Ballooning:**
```bash
# Enable in VM settings
# VM → Options → Memory → Ballooning Device: Enable
```

#### Issue 5: Network Performance Issues

**Symptoms:**
- Slow network between VMs
- High latency

**Solutions:**
- Use VMXNET3 adapters (VMware)
- Use virtio network adapters (Proxmox)
- Check network adapter settings
- Verify no network loops
- Check STP configuration (if using switches)

**Proxmox Network Adapter:**
- VM → Hardware → Network Device → Model: VirtIO

**VMware Network Adapter:**
- VM Settings → Network Adapter → Adapter Type: VMXNET3

### Performance Optimization

#### Proxmox Optimization

```bash
# Enable CPU governor for performance
echo performance > /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor

# Optimize I/O scheduler
echo deadline > /sys/block/sda/queue/scheduler

# Enable huge pages (for better memory performance)
echo 1024 > /proc/sys/vm/nr_hugepages

# Make optimizations persistent
# Add to /etc/sysctl.conf
vm.nr_hugepages = 1024
```

#### VMware Optimization

1. **VM Settings:**
   - Enable "Virtualize Intel VT-x/EPT"
   - Use paravirtualized SCSI controller
   - Enable "Accelerate 3D graphics" (if needed)

2. **Host Settings:**
   - Disable unnecessary services
   - Set VM priority to "High"
   - Allocate sufficient resources

#### VM Optimization

```bash
# Install VMware Tools / QEMU Guest Agent
# Enable memory ballooning
# Use paravirtualized drivers
# Disable unnecessary services in VMs

# On Linux VMs
sudo systemctl disable snapd  # If not needed
sudo systemctl disable bluetooth  # If not needed
```

### Network Troubleshooting

#### Verify Network Connectivity

```bash
# Check interface status
ip link show

# Check IP addresses
ip addr show

# Check routing table
ip route show

# Test connectivity
ping -c 4 <gateway>
ping6 -c 4 <ipv6-gateway>

# Check DNS resolution
nslookup google.com
dig google.com
```

#### Router Troubleshooting

**VyOS:**
```bash
# Show interfaces
show interfaces

# Show IP routes
show ip route

# Show OSPF neighbors
show ip ospf neighbor

# Show BGP summary
show bgp summary

# Debug OSPF
debug ospf packet all
```

**FRR:**
```bash
# Access FRR shell
sudo vtysh

# Show routes
show ip route
show ipv6 route

# Show OSPF neighbors
show ip ospf neighbor
show ipv6 ospf neighbor

# Show BGP summary
show bgp summary
show bgp ipv6 summary
```

### Virtualization Platform Issues

#### Proxmox Issues

**VM Won't Start:**
```bash
# Check VM logs
qm config <VMID>
qm status <VMID>

# Check storage
df -h
pvesm status

# Check network bridges
ip link show
```

**Network Bridge Issues:**
```bash
# Restart networking
systemctl restart networking

# Check bridge status
brctl show

# Restart Proxmox services
systemctl restart pve-cluster
systemctl restart pvedaemon
```

#### VMware Issues

**VM Network Not Working:**
- Check Virtual Network Editor settings
- Verify VMnet configuration
- Restart VMware networking service (Windows)
- Check host firewall rules

**VM Performance Issues:**
- Verify VMware Tools installed
- Check resource allocation
- Verify hardware acceleration enabled

### IPv6-Specific Troubleshooting

For comprehensive IPv6 troubleshooting, see: [IPv6 Workshop Guide](../IPv6-Workshop-Guide.md) and [IPv6 Migration Tools](ipv6-migration-tools.md)

**Common IPv6 Issues:**
```bash
# Check IPv6 addresses
ip -6 addr show

# Check IPv6 routes
ip -6 route show

# Test IPv6 connectivity
ping6 -c 4 2001:4860:4860::8888

# Check IPv6 neighbors
ip -6 neigh show

# Check RA (Router Advertisement)
rdisc6 eth0
```

---

## Related Documentation

- For general network troubleshooting, see: [Network Troubleshooting](../../troubleshooting/troubleshooting.md)
- For IPv6 troubleshooting, see: [IPv6 Workshop Guide](../IPv6-Workshop-Guide.md)
- For performance optimization, see: [Best Practices](best-practices.md)

