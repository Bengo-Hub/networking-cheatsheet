# IPv6 Comprehensive Workshop Guide
## From Guidelines to Core, Enterprise, and End-User Networking

---

## Table of Contents

1. [Key Guidelines for IPv6 Implementation](#key-guidelines-for-ipv6-implementation)
2. [Workshop Overview and Structure](#workshop-overview-and-structure)
3. [IPv6 in the Core Network](#ipv6-in-the-core-network)
4. [Hands-On Lab Exercises](#hands-on-lab-exercises)
5. [Enterprise Network Deployment](#enterprise-network-deployment)
6. [End-User Network Configuration](#end-user-network-configuration)

---

## Key Guidelines for IPv6 Implementation

### Core Policy Principles

1. **Mandate IPv6 Support**: The policy should mandate that all new IT procurement and services are IPv6-capable and support operating in an IPv6-only environment.

2. **Establish Milestones**: Define clear, time-bound milestones for the transition, such as the Government's goal of 50% IPv6-only operation by the end of fiscal year X.

3. **Phase Out IPv4**: State the strategic intent to eventually phase out the use of IPv4 for all systems.

4. **Security Integration**: Ensure that security plans, assessments, and monitoring processes address the use of IPv6 from the outset.

---

## Implementation Phases

### Phase 1: Initiation and Planning

1. **Form an Integrated Task Force**: Establish a team with members from acquisition, policy, and technical departments to govern the effort.

2. **Gather Requirements**: Collect technical and business requirements across all technology pillars (networking, systems, storage, applications, etc.).

3. **Develop an Addressing Plan**: Plan addressing based on the total number of sites, reserving blocks for infrastructure, and using consistent subnet prefix sizes (e.g., a minimum of a `/48` for each site).

4. **Acquire Resources**: Obtain necessary IPv6 address blocks from a Regional Internet Registry (AFRINIC).

### Phase 2: Assessment and Design

1. **Assess Current Readiness**: Perform an automated discovery to audit all current devices and software for IPv6 capability.

2. **Identify Gaps**: Verify which hardware and software can be upgraded and plan for the replacement of non-compliant devices.

3. **Conduct Pilots**: Identify opportunities for IPv6 pilots and complete at least one operational pilot of an IPv6-only system to gain experience and identify lessons learned.

4. **Design Architecture**: Design the network architecture to support native IPv6 operation, considering dual-stack (IPv4/IPv6) as a transition mechanism.

### Phase 3: Implementation and Deployment

1. **Implement in Phases**: Deploy the solution in a phased manner to minimize disruption to existing operations.

2. **Upgrade Public Services**: Prioritize the upgrade of public-facing servers and services (web, email, DNS, etc.) to use native IPv6.

3. **Enable Internal Systems**: Gradually enable IPv6 on internal client applications, servers, and supporting enterprise networks.

4. **Leverage Vendor Support**: Work with procurement authorities to ensure vendors provide products and services that can operate in an IPv6-only environment.

### Phase 4: Operations, Maintenance, and Security

1. **Monitor Compliance**: Continuously monitor and manage compliance with federal/organizational guidance and industry best practices.

2. **Address Security**: Ensure all security services (firewalls, identity management, logging) are fully functional in an IPv6 environment. Block unmanaged IPv6 traffic if necessary during the early stages of transition to prevent security vulnerabilities.

3. **Provide Training**: Offer capacity building and specialized training for network engineers and IT staff.

4. **Conduct Audits**: Periodically perform conformance audits to measure the level of IPv6 implementation across the network.

---

## Workshop Overview and Structure

### Workshop Schedule

- **09:00 - 10:30**: Session 1 - Introductions and IPv6 Fundamentals
- **11:00 - 13:00**: Session 2 - Hands-On Labs
- **14:00 - 15:30**: Session 3 - IPv6 Deployment Strategies
- **16:00 - 17:00**: Session 4 - Advanced Topics and Q&A

### Workshop Roadmap

The workshop covers a comprehensive one-week program:

- **Day 1**: IPv6 For Policy Makers and Business Leaders
- **Day 2**: IPv6 Project Planning and National IPv6 Council
- **Day 3**: Translation Strategies (RFC 6333, RFC 6146, RFC 6147)
- **Day 4**: Hands-On Labs - DS-Lite, NAT64 & DNS64
- **Day 5**: IPv6 Deployment - Internet Backbones, Enterprise Networks, Data Centers & Cloud
- **Day 6**: Hands-On Labs - OSPFv3, ISIS, BGP
- **Day 7**: IPv6 Test Bed and Benchmarking

### Lab Environment

- **Virtualization**: The lab environment uses virtualization with a number of virtual nodes
- **Group Assignments**: Participants work in groups
- **Collaboration**: Hands-on collaboration is emphasized
- **Infrastructure**: Each group receives Internet Resources including ASN, IPv4, and IPv6 address blocks

### Workshop Outcomes

1. **Hands-On Technical Skills**: Participants shall leave with hands-on experience in configuring and troubleshooting dual-stack, NAT64/DNS64, and IPv6-only networks.

2. **Real World Practical Solutions**: Each participant shall develop a project (e.g., a transition plan or configuration template) applicable to their own network needs.

### Project Options (Stand-Off)

1. **Dual-Stack Lite (DS-Lite)**: Focus on the configuration and troubleshooting of a DS-Lite deployment in a lab environment.

2. **NAT64/DNS64**: This project would involve building and testing a NAT64/DNS64 setup, paying special attention to DNS configuration and traffic flow.

3. **6to4 or IPv6-only with 6rd**: Teams would work on establishing an IPv6-only network and using a tunneling protocol to reach the IPv4 internet.

---

## IPv6 in the Core Network

### Introduction to IS-IS Lab

This lab adds IS-IS to the configured, addressed, and confirmed working backbone facing internal interfaces.

**Prerequisites**: The setup lab must have been completed.

### IPv4 and IPv6 Addressing

#### IPv4 Allocation
- `192.168.100.0/27` - Core
- `192.168.101.0/27` - RouterID

#### IPv6 Allocation
- `2001:0db8:0:1::/64` - Core
- `2001:0db8:0:2::/64` - RouterID

### IS-IS Setup

We will enable IS-IS routing on the router. We will use `v6lab` as the IS-IS ID in the configuration.

For this lab, we use level-2 in one area (`49.0001`) and use wide metrics (IOS default is the historical narrow metric and is not considered good practice due to the limited scope available).

#### IS-IS NET Address Configuration

We will use the simpler method here, the convention used for IPv6 deployments, where the format used will be the following: `49.0001.loopback-address#.00`.

For this lab our point of presence number is zero as we only have one PoP.

**Example:**
```
router isis v6lab
net 49.0001.0000.0000.0000.00
```

#### Setting IS-IS Type

IS-IS on Cisco IOS defaults to having each IS existing in level-1 and level-2 at the same time. As we learned in the workshop, this is unnecessary and wasteful, and so we need to change the default to level-2-only, which has been the industry best practice for many years.

```
router isis v6lab
is-type level-2-only
```

#### Setting Wide Metrics

We also set the metric-style to wide. IS-IS supports two types of metric, narrow (historic now and not suitable for modern networks) and wide. IOS still defaults to narrow metrics, so we need to enter explicit configuration to change this to wide.

```
router isis v6lab
metric-style wide
```

#### Setting Up Multi-Topology

As we will be running a dual stack network in future, we need to activate multi-topology. This creates a separate IPv4 and IPv6 topology database within the IS-IS process, meaning that the network can support routers that may only run single protocol (IPv4), and we can incrementally deploy IPv6 if we wish.

```
router isis v6lab
address-family ipv6
multi-topology
```

#### Changing the Default Metric

The default metric in IS-IS is 10 on all interfaces irrespective of their physical bandwidth. It is considered best practice these days to change the default metric from 10 to a very high value, for example 100000, so that network outages will not be caused by misconfiguration of newly introduced routers, or misconfigured interfaces which could accidentally and unintentionally take full traffic load.

We now set the default metric for both IPv4 and IPv6 topologies to be 100000:

```
router isis v6lab
metric 100000
```

#### Create the Authentication Key Chain

As we will be using neighbor authentication as discussed in the IS-IS presentation, first we create the authentication key-chain. We are using `v6lab` as the key here.

```
key chain isis-key
key 1
key-string v6lab
```

#### Enabling Logging

It is helpful to have IS-IS notify of adjacency changes, and these are sent to the router's logging system, and can be sent to the operator's log collecting system (when configured). To turn on IS-IS adjacency logging:

```
router isis v6lab
log-adjacency-changes
```

To see any log messages on the router, use the command `show logging` - in the setup lab we added detailed timestamps to all the log messages and so the IS-IS logs will also appear with those.

#### Setting IS-IS Metric on Each Interface

Here is an example configuration setting the IS-IS metric for IPv4 and IPv6 on an interface `Fa0/0`:

```
interface fa0/0
isis metric 2
```

Each team member should now go to each active interface on their router and set the IS-IS metric on them. Only do this for active interfaces - each router has 4 interfaces, but only a subset of those are in use - consult the network diagram if you are unsure which interface to setup metric.

#### Activating IS-IS on Interfaces

All connected interfaces can now to be enabled within IS-IS. Note that IS-IS considers an ethernet interface as a broadcast interface by default, so will normally proceed with a DIS election once enabled and the first neighbour is found.

We are using ethernet as a point-to-point link here, so we need to notify this in the configuration. Below is an example configuration activating IS-IS on a point-to-point interface `GigabitEthernet0/0`:

```
interface fa0/0
isis network point-to-point
ip router isis v6lab
```

**Note**: The IS-IS ID on the interfaces must match the router's IS-IS ID. Spelling mistakes will result in a new IS-IS process being created on the router (it can support multiple). Each router team should now go to back to each active interface on their router and enable IS-IS on them.

#### Announce the Loopback Host Route

Finally we need to announce the Loopback addresses (IPv4) in IS-IS. (On some versions of Cisco IOS we cannot do this until we have at least one interface active for IS-IS on the router.)

We do not need to set up IS-IS adjacencies on the loopback interface as there are no neighbours there, so we mark it as passive:

```
router isis v6lab
passive-interface loopback0
```

**Note**: This will tell IS-IS to install the loopback interface addresses (IPv4) in the IS-IS RIB. We do NOT need to add an `ip router isis` statement onto the loopback interface itself. This is different from the required OSPF configuration, and often catches many network engineers and operators out, especially those who are learning IS-IS after gaining experience with OSPF on the Cisco platform.

#### Distributing Default Route - RouterX ONLY

RouterX has the transit link to the outside world. So that other routers in the lab can also access the outside world, RouterX team now has to distribute this default route to the rest of our AS and to the rest of the lab.

To distribute to the other routers in the lab, RouterX needs to configure the following in their IS-IS set up:

```
router isis v6lab
default-information originate
```

Once the configuration has been added, all other routers in the lab should have a default route for IPv4 pointing to RouterX.

**Important Note**: This configuration will unconditionally originate the default route from RouterX. This is usually sufficient for simple cases where there is one exit from a network to the transit ISPS provider.

#### Testing

Once IS-IS is working on your router, check with your neighbours if IS-IS is working too. Then check that you can reach all other routers the network. Easiest way to test this it to ping the IPv4 loopback addresses for each router.

Does it all work? If not, what could be wrong? And ask the binary labs mentors if you need assistance… If there are problems, use the following commands to help determine the cause:

- `show isis neighbor`
- `show isis database`
- `show ip route isis`
- `show ipv6 route isis`

---

## Hands-On Lab Exercises

### Lab 1: Basic IPv6 Configuration

#### Basic Configuration Commands

**VyOS/Juniper Style:**

```
set system host-name 'RouterName'
set service dns forwarding name-server <address>
set interfaces loopback <interface> address <address>
set interfaces ethernet <interface> description <description>
set interfaces ethernet <interface> mtu <mtu>
set interfaces ethernet <interface> address <address | dhcp | dhcpv6>
set interfaces ethernet <interface> disable
```

#### Loopback Interface Configuration [RouterID]

```
set interfaces loopback lo description 'Router-ID'
set interfaces loopback lo address 192.168.101.11/32
set interfaces loopback lo address 2001:0db8:0:2::11/128
```

#### Ethernet Interface Configuration

```
set interfaces ethernet eth0 address 192.168.100.11/27
set interfaces ethernet eth0 address 2001:db8::11/64
set interfaces ethernet eth0 address dhcp
set interfaces ethernet eth0 address dhcpv6
set interfaces ethernet eth0 mtu 1600
```

#### IS-IS Routing Configuration

```
set protocols isis interface lo passive
set protocols isis interface eth0
set protocols isis interface eth0 network point-to-point
set protocols isis level 'level-2'
set protocols isis log-adjacency-changes
set protocols isis metric-style 'wide'
set protocols isis net '49.0001.1921.6825.5255.00'
```

#### Show Commands for Verification

```
show configuration
show interfaces
show isis neighbor
show ip route isis
show ipv6 route isis
```

### Lab 2: Implementing IPv6

**Let's Implement IPv6** - This lab adds IPv6 addressing and routing to the existing IPv4 IS-IS configuration.

---

## Enterprise Network Deployment

### Enterprise Network Considerations

1. **Dual-Stack Deployment**: Start with dual-stack (IPv4/IPv6) to ensure backward compatibility while transitioning.

2. **Address Planning**: Allocate `/48` prefixes for each site, with `/64` subnets for each network segment.

3. **Routing Protocols**: Deploy OSPFv3 or IS-IS for IPv6 routing within the enterprise.

4. **Security**: Implement IPv6-aware firewalls and security policies from the beginning.

5. **DNS**: Ensure DNS servers support AAAA records and IPv6 transport.

6. **Application Support**: Verify all critical applications support IPv6.

### Enterprise Network Best Practices

- Use consistent addressing schemes across all sites
- Implement proper prefix delegation for branch offices
- Monitor IPv6 traffic and performance
- Maintain IPv4/IPv6 dual-stack during transition period
- Document all IPv6 configurations and changes

---

## End-User Network Configuration

### End-User Network Setup

1. **Router Configuration**: Configure customer edge routers with IPv6 support.

2. **Prefix Delegation**: Use DHCPv6-PD (Prefix Delegation) for automatic prefix assignment.

3. **SLAAC**: Enable Stateless Address Autoconfiguration (SLAAC) for end devices.

4. **DNS Configuration**: Configure IPv6 DNS servers (2001:4860:4860::8888, 2001:4860:4860::8844).

5. **Firewall Rules**: Implement appropriate firewall rules for IPv6 traffic.

### End-User Network Checklist

- [ ] Router supports IPv6
- [ ] IPv6 prefix received from ISP
- [ ] IPv6 addresses assigned to interfaces
- [ ] IPv6 routing configured
- [ ] DNS servers configured for IPv6
- [ ] Firewall rules updated for IPv6
- [ ] End devices receiving IPv6 addresses
- [ ] Connectivity verified (ping6, traceroute6)

---

## Troubleshooting Commands

### General Verification

```bash
# Show IPv6 interfaces
show ipv6 interface brief

# Show IPv6 routes
show ipv6 route

# Show IS-IS neighbors
show isis neighbor

# Show IS-IS database
show isis database

# Ping IPv6 address
ping6 <ipv6-address>

# Traceroute IPv6
traceroute6 <ipv6-address>
```

### Common Issues and Solutions

1. **No IPv6 Connectivity**: Check interface configuration, routing protocol status, and firewall rules.

2. **IS-IS Adjacency Issues**: Verify NET addresses, authentication keys, and interface configuration.

3. **Address Assignment Problems**: Check DHCPv6 or SLAAC configuration.

4. **Routing Issues**: Verify routing protocol configuration and route redistribution.

---

## Workshop Resources

### Lab Infrastructure

- **Virtual Routers**: FRR, ROS, VYOS
- **Access**: OOB - SSID
- **Management**: https://192.168.20.4:8006
- **Credentials**: root / s3@c0m

### Getting Help

**At any time during the workshop, please ask questions!**

The mentors and instructors are available to assist with:
- Configuration issues
- Troubleshooting problems
- Understanding concepts
- Best practices guidance

---

## Conclusion

This comprehensive guide provides a step-by-step approach to IPv6 implementation from policy guidelines through core network deployment, enterprise networks, and end-user configurations. Follow the phases systematically, conduct thorough testing at each stage, and leverage the hands-on lab exercises to build practical experience.

Remember: IPv6 deployment is a journey, not a destination. Start with dual-stack, gradually enable IPv6 services, and continuously monitor and optimize your IPv6 network.

