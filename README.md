# Network_Task_02_Rahan_Raj
This task covers the fundamentals of network devices, IP addressing concepts, and how data travels across a network.

> **Intern:** Rahan Raj K R  
> **Date:** June 2025  
> **Organization:** White Band Associates
---

## Table of Contents

- [Part A – Network Devices](#part-a--network-devices)
- [Part B – IP Address Classification](#part-b--ip-address-classification)
- [Part C – Understanding My Network](#part-c--understanding-my-network)
- [Part D – Network Communication Diagram](#part-d--network-communication-diagram)
- [Part E – Practical Command Exercise](#part-e--practical-command-exercise)
- [Tools Used](#tools-used)


---



## Part A – Network Devices

Explanation of six core network devices.

---

### Router

| Field | Details |
|---|---|
| **Purpose** | Connects a local network to the internet |
| **How it works** | Reads destination IP addresses on each packet and forwards them along the best available path using routing tables |
| **Real-world use** | The Wi-Fi box provided by your ISP at home; enterprise-grade routers in offices and data centres |

---

### Switch

| Field | Details |
|---|---|
| **Purpose** | Connects multiple devices within the same local area network (LAN) |
| **How it works** | Uses MAC addresses to send data only to the specific device it is meant for, unlike a hub which sends to everyone |
| **Real-world use** | Office networks connecting PCs, printers, and servers together on the same floor |

---

### Hub

| Field | Details |
|---|---|
| **Purpose** | Connects multiple devices within a LAN (older technology) |
| **How it works** | Broadcasts every packet to all connected devices regardless of destination; each device decides whether the packet is for them |
| **Real-world use** | Largely obsolete today; replaced by switches due to inefficiency and security concerns |

---

### Access Point (AP)

| Field | Details |
|---|---|
| **Purpose** | Extends a wired network by broadcasting a wireless (Wi-Fi) signal |
| **How it works** | Connects to a router or switch via an Ethernet cable and creates a wireless access zone for nearby devices |
| **Real-world use** | Wi-Fi extenders in large offices, university campuses, shopping centres |

---

### Firewall

| Field | Details |
|---|---|
| **Purpose** | Monitors and filters incoming and outgoing network traffic based on defined security rules |
| **How it works** | Acts as a security checkpoint — it inspects packets and blocks or allows them depending on rules set by the administrator |
| **Real-world use** | Windows Defender Firewall on personal PCs; enterprise hardware firewalls (e.g. Cisco) protecting company networks |

---

### Modem

| Field | Details |
|---|---|
| **Purpose** | Connects a home or office network to the Internet Service Provider (ISP) |
| **How it works** | Modulates and demodulates signals — converts analog signals from telephone or cable lines into digital signals computers understand |
| **Real-world use** | The device your ISP installs at your premises; the router then plugs into it |

---

## Part B – IP Address Classification

### Private IP Ranges (RFC 1918)

| Range | CIDR Notation |
|---|---|
| 10.0.0.0 – 10.255.255.255 | 10.0.0.0/8 |
| 172.16.0.0 – 172.31.255.255 | 172.16.0.0/12 |
| 192.168.0.0 – 192.168.255.255 | 192.168.0.0/16 |

Any IP address that does not fall within these ranges is a **Public IP** and is routable on the internet.

---

### Classification Results

| IP Address | Classification | Reason |
|---|---|---|
| `192.168.1.10` | **Private** | Falls within the 192.168.0.0/16 range |
| `10.0.0.5` | **Private** | Falls within the 10.0.0.0/8 range |
| `172.16.5.20` | **Private** | Falls within the 172.16.0.0/12 range |
| `8.8.8.8` | **Public** | Google's public DNS server — internet routable |
| `1.1.1.1` | **Public** | Cloudflare's public DNS server — internet routable |
| `192.168.100.1` | **Private** | Falls within the 192.168.0.0/16 range |

> **Key rule:** Private IPs are used inside local networks only. They are never directly reachable from the internet. Routers use NAT (Network Address Translation) to map private IPs to a single public IP when communicating with the outside world.

---

## Part C – Understanding My Network


### Device Network Info

| Field | Value |
|---|---|
| **IPv4 Address** | 192.168.1.9  |
| **Default Gateway** | 192.168.1.1  |
| **DNS Server** |  8.8.8.8  |
| **IP Range** |  192.168.0.0/16 |
| **Public or Private?** | Private |

---

### Questions & Answers

**Q1: Which IP range does your device belong to?**  
My device's IPv4 address falls within the `192.168.0.0/16` private range, which is
the most commonly used range in home and small office networks.

**Q2: Is it public or private?**  
Private. My device is not directly accessible from the internet.

**Q3: What role does your router play in your network?**  
My router acts as the default gateway. All traffic from my device
destined for the internet passes through it. 

**Q4: What would happen if the DNS server stopped working?**  
I would be unable to browse websites by domain name (e.g. `google.com`).
However, I could still reach websites by typing their IP address directly
into the browser. DNS is the phonebook of the internet — without it,
names cannot be resolved to addresses.

---

## Part D – Network Communication Diagram

### What happens when you open www.google.com

![Network Communication Flow Diagram](./diagram/network%20communication%20flow.png)


---

### Step-by-Step Explanation

| Step | Component | What happens |
|---|---|---|
| 1 | **Your device** | You type `www.google.com`. The browser checks its cache, then the OS cache, then the hosts file for a known IP. |
| 2 | **Router** | If no cached IP is found, your device sends a DNS query. The router forwards it out to the internet. |
| 3 | **DNS server** | The DNS server looks up `www.google.com` and replies with its IP address (e.g. `142.250.74.46`). |
| 4 | **Google server** | Your device opens a TCP connection (SYN → SYN-ACK → ACK) to that IP and sends an HTTPS request. |
| 5 | **Response** | Google's server sends back the webpage data. Your browser renders it on screen. |

---

## Part E – Practical Command Exercise

All commands were run on **Windows** using Command Prompt (`cmd`).

---

### Command 1: `ipconfig /all`

```
ipconfig /all
```

**Purpose:** Displays full network configuration including IPv4 address,
default gateway, DNS server, MAC address, and DHCP status.


---

### Command 2: `nslookup google.com`

```
nslookup google.com
```

**Purpose:** Queries the DNS server to resolve `google.com` into an IP address.

![nslookup](./command%20outputs/nslookup.png)

>  

---

### Command 3: `ping google.com`

```
ping google.com
```

**Purpose:** Tests connectivity to Google's server and measures round-trip latency.

![ping output](./command%20outputs/ping%20.png)

> **Ping result:** Successful — 4 replies received, average latency = 148ms 

---

### Questions & Answers

**Q1: What IP address did DNS return for Google?**  
The `nslookup` command returned `142.250.x.x` as Google's IP address.
This is the address my device used to make the actual HTTP/S connection.

**Q2: Was the ping successful?**  
Yes. The ping command returned 4 successful replies with low latency,
confirming that my device has a working connection to Google's servers.

**Q3: Why is DNS important before communication begins?**  
Computers communicate using IP addresses, not domain names. DNS translates
`google.com` (human-readable) into `142.250.x.x` (machine-readable) so
the device knows where to send the request. Without a working DNS server,
browsing by domain name would be difficult.



---

## Tools Used

| Tool | Purpose |
|---|---|
| Windows Command Prompt | Running `ipconfig /all`, `nslookup`, `ping` |
| draw.io  | Creating the network communication flow diagram |
| Git & GitHub | Version control and task submission |


---



