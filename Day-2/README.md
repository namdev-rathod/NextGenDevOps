# 🚀 DevOps Day-2: Networking Basics

A comprehensive beginner-friendly guide to understanding core networking concepts essential for DevOps Engineers.

<img width="1536" height="1024" alt="vpc" src="https://github.com/user-attachments/assets/b9cf5e0b-3975-4d3e-9963-ceed2ce68615" />

---

## 🌐 1. What is an IP Address?

An **IP Address (Internet Protocol Address)** uniquely identifies a device on a network.

### 🔹 Types of IPs:

* **Private IP:** Used in internal/local networks (e.g., `192.168.0.0/16`, `10.0.0.0/8`, `172.16.0.0/12`)
* **Public IP:** Globally routable IP for accessing over the internet (e.g., `8.8.8.8`)

### 🔹 Check Your IP:

```bash
ip a                  # Show local (private) IP
curl ifconfig.me      # Show public IP
```

---

## 🧱 2. Linux Networking Basics

Linux provides powerful tools to interact with networking components.

### 🔹 Common Commands:

| Command             | Description                          |
| ------------------- | ------------------------------------ |
| `ip a`              | Show all IPs and interfaces          |
| `ip r`              | View routing table                   |
| `ping <host>`       | Test network connectivity            |
| `traceroute <host>` | Trace route to destination           |
| `netstat -tulnp`    | Show open ports (legacy)             |
| `ss -tuln`          | Show open ports (modern replacement) |
| `nslookup <domain>` | DNS query                            |
| `dig <domain>`      | Advanced DNS lookup                  |

---

## 🌐 3. DNS - Domain Name System

DNS translates human-readable domain names (e.g., `google.com`) into machine-readable IP addresses.

### 🔹 Test DNS:

```bash
nslookup google.com
dig google.com
cat /etc/resolv.conf  # DNS resolver config
```

---

## 🔥 4. Firewall

A **firewall** filters inbound and outbound traffic based on defined rules.

### 🔹 Common Ports:

| Port | Protocol |
| ---- | -------- |
| 22   | SSH      |
| 80   | HTTP     |
| 443  | HTTPS    |

### 🔹 Check Firewall:

```bash
sudo ufw status           # Ubuntu
sudo firewall-cmd --state # RHEL/CentOS
```

---

## 🔁 5. NAT - Network Address Translation

NAT allows multiple devices with private IPs to access the internet using a single public IP.

### 🔹 Usage:

* Home/Office Routers
* AWS NAT Gateway
* Docker bridge networks

### 🔹 Docker NAT Example:

```bash
docker run -d nginx
docker inspect <container_id> | grep IPAddress
curl http://localhost
```

---

## 🧰 6. Proxy Servers

A **proxy** is an intermediary server between a client and another server.

### 🔹 Types:

* **Forward Proxy:** Controls outbound traffic (corporate firewalls)
* **Reverse Proxy:** Controls inbound traffic and routes to backend services (e.g., NGINX, HAProxy)

### 🔹 Set Proxy (Temp):

```bash
export http_proxy=http://proxy.example.com:8080
export https_proxy=https://proxy.example.com:8080
```

---

## 🧱 OSI Model – 7 Networking Layers

The **OSI (Open Systems Interconnection)** model describes how data moves through a network, broken into 7 layers. Each layer has its specific function and interacts only with the layers directly above and below it.

### 📊 OSI Layer Table

| Layer | Layer Name         | Description                                                                                                         | Examples                                    |
| ----- | ------------------ | ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------- |
| 7     | Application Layer  | Interfaces with end-user applications; responsible for network services to applications.                            | HTTP, FTP, SMTP, DNS                        |
| 6     | Presentation Layer | Translates, encrypts, or compresses data from the application layer.                                                | SSL/TLS, JPEG, MPEG                         |
| 5     | Session Layer      | Manages sessions or connections between applications.                                                               | NetBIOS, RPC                                |
| 4     | Transport Layer    | Provides reliable data transfer via segmentation, error detection, and flow control.                                | TCP, UDP                                    |
| 3     | Network Layer      | Routes packets across networks and handles logical addressing.                                                      | IP (IPv4/IPv6), ICMP                        |
| 2     | Data Link Layer    | Transfers data between devices on the same network; handles MAC addressing and error correction at the frame level. | Ethernet, PPP, Switch                       |
| 1     | Physical Layer     | Transmits raw bit stream over the physical medium.                                                                  | Cables, Hubs, Network Interface Cards (NIC) |

---

### 📘 Easy-to-Remember Mnemonic

To recall the layers in order:

**A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing
→ (Application, Presentation, Session, Transport, Network, Data Link, Physical)

---

### 🛠️ Use in DevOps

| OSI Layer         | Relevance in DevOps                                                 |
| ----------------- | ------------------------------------------------------------------- |
| Application Layer | Web apps, APIs, browser interactions                                |
| Transport Layer   | TCP/UDP port management, firewall rules                             |
| Network Layer     | IP routing, VPCs, NAT Gateways, VPN setups                          |
| Data Link Layer   | Less common in DevOps, relevant in debugging packet delivery issues |
| Physical Layer    | Not usually managed by DevOps (handled by cloud provider)           |

---

## 📚 8. Private IP Ranges

| Range                         | CIDR Notation    | IP Count       |
| ----------------------------- | ---------------- | -------------- |
| 10.0.0.0 – 10.255.255.255     | `10.0.0.0/8`     | \~16.7 million |
| 172.16.0.0 – 172.31.255.255   | `172.16.0.0/12`  | \~1 million    |
| 192.168.0.0 – 192.168.255.255 | `192.168.0.0/16` | \~65,000       |

---

## 🛠️ 9. Useful Linux Tools

| Tool             | Use Case                       |
| ---------------- | ------------------------------ |
| `ping`           | Test reachability              |
| `curl`           | Test web/server endpoints      |
| `wget`           | Download files from internet   |
| `telnet`         | Test port connectivity         |
| `netstat` / `ss` | Check listening ports/services |
| `ip`             | IP/routing interface info      |
| `traceroute`     | Show network hops              |
| `tcpdump`        | Packet capture tool            |

---

## 🧪 10. Testing Examples

```bash
ping google.com                    # Connectivity test
traceroute google.com              # Path tracing
curl -I https://www.google.com     # HTTP headers
nslookup dev.to                    # DNS resolution
```

---

## 📌 Summary Table

| Concept          | Description                            | Example                    |
| ---------------- | -------------------------------------- | -------------------------- |
| IP Address       | Unique device ID on network            | `ip a`                     |
| DNS              | Resolves domain to IP                  | `nslookup google.com`      |
| Firewall         | Controls traffic rules                 | `ufw status`               |
| NAT              | Private → Public IP mapping            | Used in Docker, AWS NAT GW |
| Proxy            | Mediates traffic between client/server | `export http_proxy=...`    |
| OSI Model        | 7-layer network model                  | Transport = TCP, UDP       |
| Linux Networking | CLI tools for network troubleshooting  | `ping`, `ss`, `traceroute` |

---
