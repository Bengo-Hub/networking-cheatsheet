# Network Security Principles

**This section is part of the [Networking Principles Guide](../Networking-Principles.md)**

---

## Network Security Principles

### 7.1 Security Fundamentals

**CIA Triad:**

- **Confidentiality**: Data is accessible only to authorized users
- **Integrity**: Data is accurate and unmodified
- **Availability**: Systems and data are accessible when needed

**Defense in Depth:**

- Multiple layers of security
- No single point of failure
- Physical, network, host, application security

**Least Privilege:**

- Users have minimum necessary access
- Principle of least privilege
- Role-based access control (RBAC)

**Zero Trust Architecture:**

- Never trust, always verify
- Verify every access request
- Micro-segmentation
- Continuous monitoring

### 7.2 Network Security Technologies

**Firewalls:**

- **Packet Filtering**: Rules based on headers
- **Stateful Inspection**: Track connection state
- **Application Firewall**: Layer 7 inspection
- **Next-Generation Firewall**: Deep packet inspection, IPS, application awareness

**VPN Technologies:**

**IPsec VPN (RFC 4301, RFC 4303, RFC 4302):**

IPsec provides secure communication at the network layer with three main components:

- **AH (Authentication Header) - RFC 4302**:
  - Provides data integrity and authentication
  - Does NOT provide encryption
  - Protocol number: 51
  - Detects modification, replay attacks
  - Less commonly used (ESP preferred)

- **ESP (Encapsulating Security Payload) - RFC 4303**:
  - Provides encryption, integrity, and authentication
  - Protocol number: 50
  - More commonly used (includes AH functionality)

**IPsec Modes:**

1. **Transport Mode**:
   - Protects payload only
   - Original IP header unchanged
   - Used for host-to-host communication
   - Example: Host A to Host B encryption

2. **Tunnel Mode**:
   - Protects entire IP packet
   - Creates new IP header
   - Used for site-to-site VPNs
   - Example: Router-to-router VPN tunnels

**IKE (Internet Key Exchange) - RFC 7296:**

IKE establishes and manages IPsec security associations (SAs) through two phases:

**Phase 1 - ISAKMP SA Establishment:**
- Establishes secure channel for Phase 2
- Modes: Main Mode (6 messages) or Aggressive Mode (3 messages)
- Authenticates peers and establishes shared secret
- Creates IKE SA (bidirectional)

**Phase 2 - IPsec SA Establishment:**
- Negotiates IPsec parameters
- Creates IPsec SAs (unidirectional pairs)
- Uses Quick Mode (3 messages)
- Can establish multiple SAs

**IKE Encryption and Authentication:**
- **Encryption Algorithms**: AES (128/192/256-bit), 3DES, DES
- **Hash Algorithms**: SHA-256, SHA-1, MD5
- **DH Groups**: Diffie-Hellman key exchange (groups 1, 2, 5, 14, etc.)
- **Authentication Methods**: Pre-shared keys (PSK), RSA signatures, ECDSA

**IPsec Configuration Example (Cisco Site-to-Site VPN):**

```cisco
! Phase 1 (ISAKMP) Policy
crypto isakmp policy 10
  encryption aes 256
  hash sha256
  authentication pre-share
  group 14
  lifetime 3600

! Pre-shared key
crypto isakmp key MySecretKey address 203.0.113.1

! Phase 2 (IPsec) Transform Set
crypto ipsec transform-set MYTRANSFORM esp-aes 256 esp-sha256-hmac
  mode tunnel

! Crypto Map
crypto map MYMAP 10 ipsec-isakmp
  set peer 203.0.113.1
  set transform-set MYTRANSFORM
  match address VPN-ACL

! Apply to interface
interface GigabitEthernet0/0
  crypto map MYMAP

! ACL for interesting traffic
ip access-list extended VPN-ACL
  permit ip 192.168.1.0 0.0.0.255 192.168.2.0 0.0.0.255
```

**IPsec Verification Commands:**

```cisco
show crypto isakmp sa              ! Phase 1 status
show crypto ipsec sa               ! Phase 2 status
show crypto ipsec sa detail        ! Detailed SA information
show crypto engine connections active ! Active crypto connections
debug crypto isakmp                ! Debug IKE negotiations
debug crypto ipsec                 ! Debug IPsec operations
```

- **SSL/TLS VPN**: Application-layer VPN
  - Uses TLS/SSL encryption (port 443)
  - Clientless or thin client
  - Example: AnyConnect, OpenVPN
  - Advantages: Easy client deployment, firewall-friendly

- **WireGuard**: Modern, fast VPN protocol
  - Simpler than IPsec
  - Cryptographically secure
  - Faster than OpenVPN/IPsec
  - Growing adoption

**Encryption:**

- **Symmetric Encryption**: Same key for encryption and decryption
  - **AES** (Advanced Encryption Standard): AES-128, AES-192, AES-256
  - **3DES**: Legacy, being phased out
  - **DES**: Obsolete, insecure
  - Fast, used for bulk data encryption

- **Asymmetric Encryption**: Public/private key pairs
  - **RSA**: RSA-2048, RSA-4096 (key exchange, digital signatures)
  - **ECC** (Elliptic Curve Cryptography): Smaller keys, same security
    - P-256, P-384, P-521 curves
  - **DH** (Diffie-Hellman): Key exchange (not encryption)
  - Used for key exchange and digital signatures

- **Hashing**: One-way function for integrity
  - **SHA-256, SHA-384, SHA-512**: Secure Hash Algorithm
  - **SHA-1**: Deprecated, insecure
  - **MD5**: Obsolete, insecure
  - Used in HMAC (Hash-based Message Authentication Code)

- **Digital Signatures**: Verify message authenticity and integrity
  - Combines hashing with asymmetric encryption
  - Non-repudiation (sender cannot deny sending)
  - Examples: RSA signatures, ECDSA signatures

### 7.3 Security Best Practices

- Regular security audits and penetration testing
- Network segmentation and isolation
- Strong authentication mechanisms (multi-factor authentication)
- Regular firmware and software updates
- Security monitoring and logging (SIEM)
- Incident response planning
- Employee security training
- Access control lists (ACLs) on network devices

**Access Control Lists (ACLs) Configuration:**

**Standard ACL (Numbered 1-99, 1300-1999):**
```cisco
! Block specific host
access-list 10 deny host 192.168.1.100
access-list 10 permit any

! Apply to interface
interface GigabitEthernet0/0
  ip access-group 10 out
```

**Extended ACL (Numbered 100-199, 2000-2699):**
```cisco
! Allow HTTP from specific network
access-list 100 permit tcp 192.168.1.0 0.0.0.255 any eq 80
access-list 100 permit tcp 192.168.1.0 0.0.0.255 any eq 443
access-list 100 deny ip any any

! Apply to interface
interface GigabitEthernet0/0
  ip access-group 100 in
```

**Named ACL:**
```cisco
! Create named ACL
ip access-list extended WEBSERVER-ACL
  permit tcp 192.168.1.0 0.0.0.255 host 10.0.0.10 eq 80
  permit tcp 192.168.1.0 0.0.0.255 host 10.0.0.10 eq 443
  deny ip any any

! Apply to interface
interface GigabitEthernet0/1
  ip access-group WEBSERVER-ACL in
```

**ACL Verification:**
```cisco
show access-lists
show ip access-lists
show ip access-lists WEBSERVER-ACL
show ip interface Gi0/0 | include access-group
```

### 7.4 Security References

**RFC Documents:**
- **RFC 4301**: Security Architecture for the Internet Protocol (IPsec)
- **RFC 4302**: IP Authentication Header (AH)
- **RFC 4303**: IP Encapsulating Security Payload (ESP)
- **RFC 7296**: Internet Key Exchange Protocol Version 2 (IKEv2)
- **RFC 5246**: The Transport Layer Security (TLS) Protocol Version 1.2
- **RFC 8446**: The Transport Layer Security (TLS) Protocol Version 1.3

**Trusted Resources:**
- **OWASP**: https://owasp.org/ (Web Application Security)
- **NIST Cybersecurity Framework**: https://www.nist.gov/cyberframework
- **CIS Controls**: https://www.cisecurity.org/controls/
- **Cisco Security Documentation**: https://www.cisco.com/c/en/us/products/security/index.html

---
