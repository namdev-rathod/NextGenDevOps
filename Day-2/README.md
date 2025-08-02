## 🚀 **Day-2: DevOps Networking Basics**

---

### 🌐 **1. IP Address**

#### 🔹 What is it?

An **IP address** (Internet Protocol address) identifies a device on a network.

#### 🔹 Types:

* **Private IP:** Used within internal networks (e.g., `192.168.1.1`)
* **Public IP:** Used on the internet (e.g., `8.8.8.8`)

#### 🔹 Example:

```bash
ip a                   # Show local IP
curl ifconfig.me       # Show public IP
```

---

### 🧱 **2. Networking in Linux**

#### 🔹 Purpose:

Manage how your system connects to other systems and the internet.

#### 🔹 Useful Commands:

| Command                 | Description                    |
| ----------------------- | ------------------------------ |
| `ip a`                  | View IP addresses & interfaces |
| `ip r`                  | View routing table             |
| `ping google.com`       | Check connectivity             |
| `traceroute google.com` | Trace the path packets take    |
| `netstat -tulnp`        | View open ports & services     |
| `ss -tuln`              | Similar to netstat (modern)    |
| `nslookup google.com`   | Check DNS resolution           |

---

### 🌐 **3. DNS (Domain Name System)**

#### 🔹 What is it?

DNS translates **domain names** (e.g., `google.com`) to **IP addresses** (e.g., `142.250.194.14`).

#### 🔹 Example:

```bash
nslookup dev.to
dig google.com
cat /etc/resolv.conf     # Check system's DNS servers
```

---

### 🔥 **4. Firewall**

#### 🔹 What is it?

A **firewall** controls **inbound and outbound** traffic to/from your system or server based on rules.

#### 🔹 Example:

```bash
sudo ufw status           # On Ubuntu
sudo firewall-cmd --state # On RHEL/CentOS
```

#### 🔹 Common Ports:

| Port | Service |
| ---- | ------- |
| 22   | SSH     |
| 80   | HTTP    |
| 443  | HTTPS   |

---

### 🔁 **5. NAT (Network Address Translation)**

#### 🔹 What is it?

**NAT** allows **multiple private IPs** to share a **single public IP** to access the internet.

#### 🔹 Where used?

* Home routers
* Docker containers
* AWS NAT Gateways

#### 🔹 Example in Docker:

```bash
docker run -d nginx
docker inspect <container_id> | grep IPAddress
curl http://localhost
```

---

### 🧰 **6. Proxy**

#### 🔹 What is it?

A **proxy server** acts as an intermediary between a client and the internet.

#### 🔹 Types:

* **Forward Proxy:** Controls outgoing traffic (e.g., corporate firewall)
* **Reverse Proxy:** Routes incoming requests to backend services (e.g., Nginx, HAProxy)

#### 🔹 Example:

```bash
# Set proxy temporarily
export http_proxy=http://proxy.example.com:8080
export https_proxy=https://proxy.example.com:8080
```

---

### 🧪 **7. Linux Networking Commands – Summary**

| Command             | Use                            |
| ------------------- | ------------------------------ |
| `ip a`              | Show IP address and interfaces |
| `ip r`              | Show routing info              |
| `ping <host>`       | Check if host is reachable     |
| `traceroute <host>` | Trace route to a host          |
| `nslookup <domain>` | DNS query                      |
| `dig <domain>`      | Advanced DNS query             |
| `netstat -tulnp`    | Show network connections       |
| `ss -tuln`          | Show listening sockets         |
| `curl <url>`        | Test HTTP requests             |
| `wget <url>`        | Download files via HTTP/HTTPS  |

---

### 📌 Summary Table

| Concept          | Description                            | Example                          |
| ---------------- | -------------------------------------- | -------------------------------- |
| IP Address       | Unique device ID on network            | `ip a`                           |
| DNS              | Translates domain to IP                | `nslookup google.com`            |
| Firewall         | Controls traffic rules                 | `ufw status`                     |
| NAT              | Private → Public IP mapping            | Docker container internet access |
| Proxy            | Intermediary for network traffic       | `export http_proxy=...`          |
| Linux Networking | CLI tools to manage/check connectivity | `ping`, `traceroute`, `curl`     |

---