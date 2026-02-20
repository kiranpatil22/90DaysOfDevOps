# Networking Notes – DevOps Essentials (Day 15)
Task 1: DNS – How Names Become IPs

What happens when you type google.com in a browser:

Browser asks the local DNS resolver for google.com.

Resolver queries root → TLD → authoritative DNS if not cached.

Resolver returns the IP address, browser connects via HTTP/HTTPS.

# DNS Record Types (1 line each):

A → Domain → IPv4 address

AAAA → Domain → IPv6 address

CNAME → Alias → Another domain

MX → Mail server for domain

NS → Authoritative name server

# Example (dig google.com)

ANSWER SECTION: google.com. 299 IN A 142.250.190.78


A record: 142.250.190.78

TTL: 299 seconds

# Task 2: IP Addressing

IPv4: 32-bit address (e.g., 192.168.1.10) → 4 octets separated by dots

Public IP: Globally routable (e.g., 8.8.8.8)

Private IP: Local only (e.g., 192.168.1.10)

Private IP ranges:

10.0.0.0 – 10.255.255.255

172.16.0.0 – 172.31.255.255

192.168.0.0 – 192.168.255.255

# Check on Linux:

ip addr show 

Identify private IPs (matches above ranges)

# Task 3: CIDR & Subnetting

/24 in 192.168.1.0/24 → first 24 bits = network, 8 bits = hosts

Usable hosts:

/24 → 256 – 2 = 254

/16 → 65,536 – 2 = 65,534

/28 → 16 – 2 = 14

Why subnet: Divide large networks into smaller, manageable segments; control traffic and improve security

# Quick CIDR Exercise:

CIDR	Subnet Mask	Total IPs	Usable Hosts
/24	255.255.255.0	256	254
/16	255.255.0.0	65,536	65,534
/28	255.255.255.240	16	14
Task 4: Ports – The Doors to Services

Port: Logical “door” on a host for a specific service

Why needed: Allows multiple services on same IP (e.g., web + SSH)

# Common Ports:

Port	Service
22	SSH
80	HTTP
443	HTTPS
53	DNS
3306	MySQL
6379	Redis
27017	MongoDB

# Check listening ports:

ss -tulpn | grep ssh

Match service to at least 2 ports (e.g., 22 → sshd, 3306 → mysqld)

# Task 5: Putting It Together

curl http://myapp.com:8080 → Concepts involved:

DNS resolution → IP

Routing to host

Transport layer → TCP port 8080

Application layer → HTTP

App can’t reach DB at 10.0.1.50:3306 → Check first:

Network connectivity (ping/traceroute to 10.0.1.50)

Firewall rules or security groups

DB service running on port 3306
