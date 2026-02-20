# Networking Notes – Quick Reference

## 1️⃣ OSI vs TCP/IP
OSI Layer      | TCP/IP Layer       | Notes
---------------|-----------------|------------------------
7. Application | Application      | HTTP, DNS, SSH
6. Presentation| Application      | Encryption, formatting
5. Session     | Application      | Connection control
4. Transport   | Transport        | TCP/UDP, ports
3. Network     | Internet         | IP, routing
2. Data Link   | Network Interface| MAC, switches
1. Physical    | Network Interface| Cables, NICs

Tip: OSI = conceptual; TCP/IP = practical.

## 2️⃣ Key Commands
# IP & Routing
ip addr           # Show IPs
ip route          # Show routing table

# Connectivity
ping <host>       # Test reachability
traceroute <host> # Trace path
nslookup <host>   # DNS lookup

# Services & Ports
ss -tulnp         # Show listening ports
nc -zv host port  # Test port/service

## 3️⃣ Troubleshooting Flow
1. Check IP: ip addr
2. Check routing: ip route
3. Test connectivity: ping <gateway> → ping 8.8.8.8
4. Check DNS: nslookup google.com
5. Check service port: nc -zv host port

Interpretation:
- Ping OK, DNS fails → DNS problem
- Ping fails → Network/Layer 3 problem
- Port closed → Application/Transport issue

## 4️⃣ Common Linux Interfaces
Interface | Purpose                 | Status
----------|------------------------|-------
lo        | Loopback 127.0.0.1      | Always UP
ens5      | Primary interface (cloud VM)| UP, private IP
docker0   | Docker bridge           | DOWN if no containers


## 6️⃣ Mini Network Check Example
ping google.com
nslookup google.com
nc -zv google.com 443
