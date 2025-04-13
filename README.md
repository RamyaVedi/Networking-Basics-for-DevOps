# Networking-Basics-for-DevOps
Explore core networking concepts through a blend of theory and hands-on practice. This repository offers a comprehensive guide tailored for DevOps professionals, culminating in a practical mini-project to solidify your understanding.

**1.Network**: Devices (Nodes) Linked to Exchange Data via Protocols
      A network is a group of devices (like computers, servers, or phones) that communicate with each other using standardized rules called protocols (e.g., TCP, HTTP). These devices are connected via physical or wireless means (like cables or Wi-Fi) to share data, resources, or services.

**Nodes**: Any device on the network (your laptop, a cloud server, a router).
**Data Exchange**: Sending files, streaming videos, or pinging a server.
**Protocols**: Standardized instructions, e.g., TCP ensures reliable delivery, HTTP defines web requests.

**Task**:Test a network connection: ping google.com -c 4 (sends 4 messages to Google’s server).
Look for “4 packets transmitted, 4 received” (success) and “time=X ms” (speed).
If it fails, try ping 8.8.8.8 (Google’s IP directly).

**2. IP Addresses: Unique Identifiers for Devices on a Network**
      Every device (laptop, server, router) needs one to send or receive messages. Without IP addresses, networks would be chaos, like mailing letters without addresses.
             *Assigned automatically (via DHCP, like your router at home) or manually (e.g., setting a server’s IP).
             *Two types: IPv4 (older, common) and IPv6 (newer, future-proof).
      **Task**:ip addr show.
            *Find the inet line under an interface (e.g., eth0 or wlan0), like inet 172.17.0.2/16. That’s your device’s IP.
**3. IPv4: 32-bit, e.g., 192.168.1.1 (Limited, ~4 Billion Addresses)**
     ** What is it**?
            IPv4 is the most common format for IP addresses, using 32 bits (4 bytes) written as four numbers (0–255) separated by dots, e.g., 192.168.1.1.
                  *32-bit math: 2³² = ~4.3 billion possible addresses.
                  *Problem: The internet grew too big, and we’re running out of IPv4 addresses (like running out of phone numbers in a small town).
                  *Solution: Tricks like NAT (sharing one public IP for many devices) and IPv6 (below).
            Example: Your home router might use 192.168.1.1, and your laptop gets 192.168.1.100.
      **Task**Run: ping 192.168.1.1 (likely your router’s IP; adjust if your network uses a different range, like 10.0.0.1).
                  Success means you reached a local device.
                  Failure is okay (WSL’s virtual network may block it).
**4. IPv6: 128-bit, e.g., 2001:0db8::1 (Massive Address Space)**
      **What is it?**
            IPv6 is the newer IP format, using 128 bits for a near-infinite number of addresses (2¹²⁸, or ~340 undecillion). It’s written as eight groups of hexadecimal digits separated by colons, with shortcuts like :: for zeros, e.g.,                                              2001:0db8:0000:0000:0000:0000:0000:0001 becomes 2001:0db8::1.
                  Why? Solves IPv4’s shortage. Every device can have a unique public IP without NAT.
                  Adoption: Growing but slower than expected (many networks still rely on IPv4).
                  Example: Google’s servers use IPv6 like 2607:f8b0:4004:0809::200e.
**5. Public vs. Private: Public (Internet-Routable, like 8.8.8.8); Private (Local, like 192.168.x.x)**
      **What is it?**
            IP addresses are split into public and private to organize networks:
            **Public IPs**: Globally unique, routable on the internet.
                  Example: 8.8.8.8 (Google’s DNS server).
                  Assigned by organizations like IANA, used by servers or cloud resources.
            **Private IPs**: Reserved for local networks, not internet-routable.
                  Ranges:
                        10.0.0.0 – 10.255.255.255 (big networks).
                        172.16.0.0 – 172.31.255.255 (medium).
                        192.168.0.0 – 192.168.255.255 (home/small offices).
                  Example: Your laptop’s 192.168.1.100 or a Docker container’s 172.17.0.2.
            **How it works**: Private IPs talk to the internet via NAT (Network Address Translation), where your router swaps private IPs for a public one.
**6. Subnets: Groups of IPs (e.g., 192.168.1.0/24 Means 256 Addresses)**
      **What is it?**
            A subnet (subnetwork) is a smaller chunk of a network, grouping IP addresses to organize devices or control traffic. It’s defined by a range, like 192.168.1.0/24, where:
                  192.168.1.0: Network address (start of the range).
                  /24: Subnet mask, meaning the first 24 bits are fixed, leaving 8 bits for devices (2⁸ = 256 addresses, from 192.168.1.0 to 192.168.1.255).
                  Uses: Separate departments (e.g., HR vs. IT), isolate cloud resources, or limit access.
                  Example: Your home Wi-Fi might use 192.168.1.0/24, with your router at 192.168.1.1 and your laptop at 192.168.1.100.
      **Task**:
            Run: ip addr. Look for the subnet mask (e.g., inet 172.17.0.2/16).
            /16 means 65,536 addresses (2¹⁶, from 172.17.0.0 to 172.17.255.255).
            Check your network: ip route. Note the default gateway (e.g., 172.17.0.1).
