# Router Configuration Cheatsheet
## Cisco and Juniper Commands

---

## IP Address Blocks

### AFRINIC IP Blocks

**IPv4 Block:** `172.16.0.0/22`

- `172.16.0.0/24` - Loopback Addresses
- `172.16.1.0/24` - Laptops Addresses
- `172.16.2.0/24` - Router Interface 1 Addresses
- `172.16.3.0/24` - Router Interface 2 Addresses

**IPv6 Block:** `2001:db8:1::/48`

- `2001:db8:1:0::/64` - Loopback Addresses
- `2001:db8:1:1::/64` - Laptops Addresses
- `2001:db8:1:2::/64` - Router Interface 1 Addresses
- `2001:db8:1:3::/64` - Router Interface 2 Addresses

---

## Cisco IOS Configuration (FRR/Quagga)

### Initial Access

```bash
# Login to router
R1:~$ sudo vtysh

# Login credentials: user binary, password binary
```

### Basic Configuration

#### Change Router Hostname

```
conf t
  hostname R#
end
write
```

#### Loopback Interface Configuration

```
conf t
interface lo
 ip address 172.16.0.1/32
 ipv6 address 2001:db8:1::1/128
end
write
```

#### Ethernet Interface Configuration

**First Interface (ens18):**

```
conf t
interface ens18
 ip address 172.16.2.2/32
 ipv6 address 2001:db8:1:2::2/64
end
write
```

**Second Interface (ens19):**

```
conf t
interface ens19
 ip address 172.16.3.2/32
 ipv6 address 2001:db8:1:3::2/64
end
write
```

### IS-IS Routing Configuration

```
conf t
router isis 1
 net 49.0001.1720.1600.0002.00
 topology ipv6-unicast
exit

interface lo
 ipv6 router isis 1
end

interface eth0
 ipv6 router isis 1
exit
write
```

### Verification Commands

```
show ipv6 route
show isis neighbor
```

---

## Juniper/VyOS Configuration

### Initial Access

```bash
# Login credentials: user vyos, password vyos

# Enter configuration mode
configure
```

### Basic Configuration

#### Set Router Hostname

```
set system host-name 'R30'
```

#### Loopback Interface Configuration [RouterID]

```
set interfaces loopback lo description 'Router-ID'
set interfaces loopback lo address 172.16.0.1/32
set interfaces loopback lo address 2001:db8:1::1/128
```

#### Ethernet Interface Configuration

**First Interface (eth1):**

```
set interfaces ethernet eth1 address 172.16.2.2/24
set interfaces ethernet eth1 address 2001:db8:1:2::2/64
```

**Second Interface (eth0):**

```
set interfaces ethernet eth0 address 172.16.3.2/24
set interfaces ethernet eth0 address 2001:db8:1:3::2/64
```

### IS-IS Routing Configuration

```
set protocols isis interface lo passive
set protocols isis interface eth1
set protocols isis interface eth1 network point-to-point
set protocols isis level 'level-2'
set protocols isis log-adjacency-changes
set protocols isis metric-style 'wide'
set protocols isis net '49.0001.1720.1600.0002.00'
```

### Verification Commands

```
show configuration
show interfaces
show isis neighbor
show ip route isis
show ipv6 route isis
```

---

## Notes

- **IP Addresses**: All IP addresses shown are examples. Replace with the addresses allocated to your specific router.
- **IS-IS NET**: The NET address should be generated from your loopback IPv4 address. Format: `49.0001.XXXX.XXXX.XXXX.00`
- **Interface Names**: Interface names may vary (ens18, ens19, eth0, eth1, etc.) depending on your system configuration.
- **Dual-Stack**: Both configurations support dual-stack (IPv4 and IPv6) operation.

