# Basic Network and Network Security

### OSI Model

- Application; layer 7 (and basically layers 5 & 6) (includes API, HTTP, etc.).
- Transport; layer 4 (TCP/UDP).
- Network; layer 3 (Routing).
- Datalink; layer 2 (Error checking and frame synchronization).
- Physical; layer 1 (Bits over fiber).

### Common Protocols and Ports

- HTTP/S 
  - Port 80, 443

- SSL/TLS
  - Port 443
  - Super important to learn this, includes learning about handshakes, encryption, signing, certificate authorities, trust systems. [A good primer on all these concepts and algorithms](https://english.ncsc.nl/publications/publications/2019/juni/01/it-security-guidelines-for-transport-layer-security-tls) is made available by the Dutch cybersecurity center.
  - Various attacks against older versions of SSL/TLS (with catchy names) on [Wikipedia](https://en.wikipedia.org/wiki/Transport_Layer_Security#Attacks_against_TLS/SSL).

- ICMP 
  - Ping and traceroute.

- Mail
  - SMTP ( Port 25, 587, 465)
  - IMAP (Port 143, 993)
  - POP3 (Port 110, 995)

- SSH 
  - Port 22
  - Handshake uses asymmetric encryption to exchange symmetric key.

- Telnet
  - Port 23, 992
  - Allows remote communication with hosts.

- ARP  
  - Who is 0.0.0.0? Tell 0.0.0.1.
  - Pairing MAC address with IP Address for IP connections. Looks at cache first.
  - A protocol used for mapping an IP address to a computer connected to a local network LAN. Since each computer has a unique physical address called a MAC address, the ARP converts the IP address to the MAC address. This ensures each computer has a unique network identification. 
  - Is ARP UDP or TCP? Neither 

- DHCP 
  - Port 67, 68, 546, 547
  - Automatic (leases IP address and remembers MAC and IP pairing in a table).
  - Manual (static IP set by administrator).
  - Dynamic (leases IP address, not persistent. Allocated by router).
  - `DHCPDISCOVER` -> `DHCPOFFER` -> `DHCPREQUEST` -> `DHCPACK`
  - Rogue DHCP: A rogue DHCP server can redirect IP address assignments to allow the hacker to identify and redirect the client computer to another network segment. The hacker can then sniff network traffic from the target machine 

- IRC 
  - Understand use by hackers (botnets).

- FTP/SFTP 
  - port 21, 22

- RPC 
  - Predefined set of tasks that remote clients can execute.
  - Used inside orgs. 

- Service ports
  - 0 - 1023: Reserved for common services - sudo required. 
  - 1024 - 49151: Registered ports used for IANA-registered services. 
  - 49152 - 65535: Dynamic ports that can be used for anything. 

### TCP / UDP

#### Explain the difference between TCP and UDP. 

TCP guarantees the recipient will receive the packets in order by numbering them. 

When using UDP, packets are just sent to the recipient. The sender will not wait to make sure the recipient received the packet — it will just continue sending the next packets. 

#### Which is more secure? TCP or UDP? Why?

TCP, TCP has to make connection 

### DNS

Port 53

Requests to DNS are usually UDP, unless the server gives a redirect notice asking for a TCP connection. Look up in cache happens first. DNS exfiltration. Using raw IP addresses means no DNS logs, but there are HTTP logs. DNS sinkholes.

In a reverse DNS lookup, PTR might contain- 2.152.80.208.in-addr.arpa, which will map to  208.80.152.2. DNS lookups start at the end of the string and work backwards, which is why the IP address is backwards in PTR.

#### DNS exfiltration 

- Sending data as subdomains. 
- 26856485f6476a567567c6576e678.badguy.com
- Doesn’t show up in http logs. 

#### DNS configs

- Start of Authority (SOA).
- IP addresses (A and AAAA).
- SMTP mail exchangers (MX).
- Name servers (NS).
- Pointers for reverse DNS lookups (PTR).
- Domain name aliases (CNAME).

#### What is the need of DNS monitoring 

The Domain Name System (DNS) allots your website under a certain domain that is easily recognizable and also keeps the information about other domain names. 

It works like a directory for everything on the internet. 

Thus, DNS monitoring is very important since you can easily visit a website without actually having to memorize their IP address. 

#### Authoritative DNS Servers vs. Recursive DNS Servers 

Authoritative name servers store DNS record information –usually a DNS hosting provider or domain registrar. 

Recursive name servers are the “middlemen” between authoritative servers and end-users because they have to recuse up the DNS tree to reach the name servers authoritative for storing the domain’s records.

#### What is DNS spoofing (cache poisoning)? How does it work?

### What is a subnet and how is it useful in security? 

You can control the flow of traffic using ACLs, QoS, or route-maps, enabling you to identify threats, close points of entry, and target your responses more easily. 

Limit access to resources on wireless clients, ensuring that valuable information isn’t easily accessible in remote locations. 

### What port does ping work over? 

ICMP does not use ports 

### Firewall / IPS / IDS

Rules to prevent incoming and outgoing connections.

A firewall is a device or service that acts as a gate keeper, deciding what enters and exits the network. It analyzes the traffic it sees passing through it by checking the packet headers and data. Based on its configuration, the firewall then decides accordingly whether to deny or allow traffic to pass through. 

#### Do you prefer filtered ports or closed ports on your firewall? Why?

#### IPS vs Firewall 

The primary function of a firewall is to prevent/control traffic flow from an untrusted network (outside). A firewall is not able to detect an attack in which the data is deviating from its regular pattern, whereas an IPS can detect and reset that connection as it has inbuilt anomaly detection 

#### NIDS 

NIDS (Network Intrusion Detection system) is a system that attempts to detect hacking activities, denial of service attacks or port scans on a computer network or a computer itself. The NIDS monitors network traffic and helps to detect these malicious activities by identifying suspicious patterns in the incoming packets. 

### HTTP

#### HTTP Header

- | Verb | Path | HTTP version |
- Domain
- Accept
- Accept-language
- Accept-charset
- Accept-encoding(compression type)
- Connection- close or keep-alive
- Referrer
- Return address
- Expected Size?

#### HTTP Response Header

- HTTP version
- Status Codes: 
  - 1xx: Informational Response
  - 2xx: Successful
  - 3xx: Redirection
  - 4xx: Client Error
  - 5xx: Server Error
- Type of data in response 
- Type of encoding
- Language 
- Charset

#### Common HTTP Attacks 

- SQL injection 
- URL interpretation 
- Impersonation 
- Buffer overflow 
- Session Hijacking 
- Cross-Site Scripting 

### What is DDoS  ?

A malicious attempt to make a server or a network resource unavailable to users. 

It is achieved by saturating a service, which results in its temporary suspension or interruption. 

A Denial of Service (DoS) attack involves a single machine used to either target a software vulnerability or flood a targeted resource with packets, requests or queries. 

A Distributed Denial of Service (DDoS) attack, however, uses multiple connected devices—often executed by botnets or, on occasion, by individuals who have coordinated their activity. 

### Traceroute

Usually uses UDP, but might also use ICMP Echo Request or TCP SYN. TTL, or hop-limit.

Initial hop-limit is 128 for windows and 64 for *nix. Destination returns ICMP Echo Reply

#### How does Traceroute work?

Small Time To Live (TTL) values are transmitted through packets via traceroute. This process prevents the packets from getting into loops. After the router subtracts from the given packet’s TTL, the packet immediately expires after the TTL reaches absolute zero. After that the sender is sent messages from Traceroute that exceed the time. When small values of TTL are used, the expiration happens quickly and thus the traceroute generates ICMP messages for identifying the router. 

#### How exactly does traceroute/tracert work at the protocol level? 

It actually keeps sending packets to the final destination; the only change is the TTL that’s used. The extra credit is the fact that Windows uses ICMP by default while Linux uses UDP. 

### Nmap

Network scanning tool

#### What does nmap -sS do?

TCP SYN (Stealth) scan https://nmap.org/book/synscan.html

#### What does nmap -sT do?

TCP connect scan https://nmap.org/book/scan-methods-connect-scan.html

### Certificate

Look at DigiNotar.

### What info do certs contain, how are they signed? 

#### How do web certificates for HTTPS work? 

CA (Certificate Authority), CRL(Certificate Revocation List), Online Certificate Status Protocol (OCSP) 

#### What is certificate pinning?

#### What is Certificate transparency ?

Can verify certificates against public logs 

### How Single Sign-On works? 

Bearer tokens, this can be stolen and used, just like cookies.

![SSO](../media/SSO.png)

### NAT 

Useful to understand IPv4 vs IPv6.

### Multiplex 

Timeshare, statistical share, just useful to know it exists.

### Intercepts (MITM) 

Understand PKI (public key infrastructure in relation to this).

### VPN 

Hide traffic from ISP but expose traffic to VPN provider.

### Tor 

Traffic is obvious on a network. 

How do organized crime investigators find people on tor networks. 

### Proxy  

Why 7 proxies won’t help you. 

### BGP

Border Gateway Protocol.

Holds the internet together.

### Network traffic tools

Wireshark

Tcpdump

Burp suite

### UDP Header

Source port

Destination port

Length

Checksum

### Broadcast domains and collision domains. 

### Root stores

### CAM table overflow