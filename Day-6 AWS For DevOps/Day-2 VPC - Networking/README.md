# 🌐 Day-2 AWS VPC – Virtual Private Cloud (Complete Guide)

---

## 1️⃣ What is a VPC?

A **VPC (Virtual Private Cloud)** is a logically isolated virtual network in AWS where you can **launch resources (EC2, RDS, Lambda, etc.) with full control over networking**.

**Key Features:**

* Define your **IP address range**
* Create **subnets** (public/private)
* Control **routing** and **gateways**
* Apply **security groups** and **network ACLs**

**Example:**

* Netflix uses VPCs to isolate web servers, application servers, and databases across multiple regions.

---

## 2️⃣ Why VPC is Needed?

* 🔒 **Security:** Isolate resources from other customers.
* 🌍 **Global control:** Deploy resources in specific **Availability Zones (AZs)**.
* ⚡ **High availability:** Use multi-AZ and multi-subnet designs.
* 🔄 **Connectivity:** Connect multiple VPCs or on-prem networks via **Transit Gateway** or **Direct Connect**.

**Example:**

* A bank keeps its database in a private subnet, while web servers in a public subnet handle client requests.

---

## 3️⃣ Default VPC vs Custom VPC

| Feature        | Default VPC            | Custom VPC                              |
| -------------- | ---------------------- | --------------------------------------- |
| Subnets        | Public only            | Public + Private as needed              |
| Control        | Limited                | Full control over IP, routing, gateways |
| Security       | Less secure by default | High control with SG & NACL             |
| Recommendation | For learning/testing   | Recommended for production              |

> ✅ Best Practice: Always use **Custom VPCs** for production workloads.

---

## 4️⃣ IP Addressing in VPC

* **CIDR Block:** Defines your VPC range, e.g., `10.0.0.0/16` → 65,536 IPs

* **Subnetting:** Divide VPC into smaller networks

  * Public: `10.0.1.0/24` → 256 IPs
  * Private: `10.0.2.0/24` → 256 IPs

* **IP Types:**

  * Private IP 🏠: Internal communication (`10.0.2.5`)
  * Public IP 🌐: Internet-facing (`3.25.78.12`)

* **MAC Address 🖧:** Each network interface gets a unique MAC for internal routing

---

## 🏠 Private IP Address Ranges (RFC 1918)

These are reserved ranges you can use inside your **VPCs**, offices, and internal networks. They are **not routable on the internet**.

| Range                             | CIDR             | Size (# of IPs) | Common Use Case                           |
| --------------------------------- | ---------------- | --------------- | ----------------------------------------- |
| **10.0.0.0 – 10.255.255.255**     | `10.0.0.0/8`     | \~16.7 million  | Large enterprises, AWS VPC default option |
| **172.16.0.0 – 172.31.255.255**   | `172.16.0.0/12`  | \~1 million     | Medium networks, corporate VPNs           |
| **192.168.0.0 – 192.168.255.255** | `192.168.0.0/16` | 65,536          | Small/home networks, labs                 |

> ✅ In AWS VPCs, the most **commonly used ranges** are `10.0.0.0/16` or `172.16.0.0/16`.

---

## 6️⃣ Subnets

* **Subnet:** Subdivision of VPC CIDR block
* **Public Subnet 🌐:**

  * Direct internet access via **Internet Gateway (IGW)**
  * Example: EC2 web servers
* **Private Subnet 🏠:**

  * No direct internet access
  * Outbound internet via **NAT Gateway**
  * Example: RDS, internal apps

---

## 7️⃣ Key VPC Components

| Component                         | Description                                        | Example / Emoji                            |
| --------------------------------- | -------------------------------------------------- | ------------------------------------------ |
| **Internet Gateway (IGW)**        | Connects VPC to internet                           | 🌐 Public EC2s access internet             |
| **NAT Gateway / NAT Instance**    | Enables private subnet EC2s to access internet     | 🔄 DB server downloads OS updates          |
| **Route Table**                   | Controls traffic routing between subnets, IGW, NAT | 🛣️ Routes 10.0.1.0 → IGW, 10.0.2.0 → NAT  |
| **Security Groups (SG)**          | Stateful firewall for EC2                          | 🛡️ Web server allows port 80/443          |
| **Network ACL (NACL)**            | Stateless firewall at subnet level                 | 🚦 Block/allow IP ranges                   |
| **VPC Peering / Transit Gateway** | Connect multiple VPCs privately                    | 🔗 Transit Gateway for Dev/Test/Prod VPCs  |
| **Direct Connect**                | Dedicated private link to on-prem                  | ⚡ Bank connecting data center to AWS       |
| **VPC Endpoints**                 | Private access to AWS services without internet    | 🔌 S3, DynamoDB access from private subnet |

---

## 8️⃣ NAT Gateway / NAT Instance

* Private subnet cannot access internet directly
* **Solution:** NAT Gateway → highly available & managed
* Example: `10.0.2.5 → NAT → 3.25.78.12` to download updates

---

## 9️⃣ Transit Gateway 🔗

* Central hub connecting **multiple VPCs and on-prem networks**
* Simplifies connectivity → avoids mesh peering complexity
* Example: Connect Dev, Test, and Prod VPCs of an enterprise

---

## 🔟 Direct Connect ⚡

* Dedicated network link from on-premises to AWS
* Provides **low latency, high bandwidth**, private connection
* Example: Bank connects ERP systems to AWS without going through the public internet

---

## 1️⃣1️⃣ Example VPC Architecture

```
VPC CIDR: 10.0.0.0/16
-------------------------------------------------
| Public Subnet 10.0.1.0/24 🌐               | → Web EC2, IGW
| Private Subnet 10.0.2.0/24 🏠               | → DB RDS, NAT access
| NAT Gateway 🔄                               | → Private subnet internet
| Transit Gateway 🔗                           | → Connect multiple VPCs
| Direct Connect ⚡                             | → On-prem private link
| Security Groups 🛡️ & NACLs 🚦              | → Firewall & traffic rules
-------------------------------------------------
```

**Scenario Example:**

* E-commerce website:

  * **Public subnet:** EC2 web servers with IGW
  * **Private subnet:** RDS MySQL for backend
  * NAT gateway for patching private servers
  * Transit Gateway connects Dev, Test, Prod VPCs
  * Direct Connect links on-prem inventory system

---

# 🛡️ NACL vs Security Group in AWS VPC

---

## 1️⃣ Security Group (SG)

* **Definition:** A **stateful virtual firewall** at the **instance level**.
* Controls **inbound and outbound traffic** for EC2 instances.
* **Stateful:** If an inbound rule allows traffic, the response is automatically allowed.
* **Applied to:** EC2, RDS, Lambda (VPC-enabled)

**Example:**

* EC2 web server allows inbound port 80/443 from the internet.
* Any outbound response to the requester is automatically allowed.

---

## 2️⃣ Network ACL (NACL)

* **Definition:** A **stateless firewall** applied at the **subnet level**.
* Controls **inbound and outbound traffic** for all instances in a subnet.
* **Stateless:** Return traffic must have explicit rules.
* **Applied to:** Entire subnet, affecting all resources inside.

**Example:**

* Block IP range `192.168.10.0/24` from accessing subnet.
* Even if SG allows traffic, NACL can block it.

---

## 3️⃣ Comparison Table: NACL vs Security Group

| Feature                  | Security Group 🛡️                   | Network ACL 🚦                                              |
| ------------------------ | ------------------------------------ | ----------------------------------------------------------- |
| **Scope**                | Instance-level                       | Subnet-level                                                |
| **Stateful / Stateless** | Stateful                             | Stateless                                                   |
| **Inbound Rules**        | Allowed automatically for responses  | Explicit rules required for inbound/outbound                |
| **Outbound Rules**       | Explicitly defined                   | Explicitly defined                                          |
| **Default Behavior**     | Deny all inbound, allow all outbound | Allow all inbound & outbound by default                     |
| **Rule Order**           | Evaluated collectively               | Evaluated **numerically** (lowest number first)             |
| **Number of Rules**      | Up to 60 inbound/outbound per SG     | Up to 20 inbound + 20 outbound per NACL (default)           |
| **Can Block IPs**        | No, only allow rules                 | Yes, can explicitly allow or deny                           |
| **Best Use Case**        | Instance-specific firewall           | Subnet-wide extra security layer, block known malicious IPs |

---

# ⚖️ Stateful vs Stateless

---

## 1️⃣ **Stateful**

👉 A **stateful system/firewall** remembers the **connection state**.

* If you allow traffic **in one direction**, the **return traffic is automatically allowed**.
* No need to explicitly define the return rule.

🔑 **Key Points:**

* Tracks the session/connection (like a conversation).
* Simplifies rules → you only allow one side.
* Example in AWS → **Security Groups (SGs)**.

**Example:**

* You allow **inbound HTTP (TCP 80)** from the internet to an EC2 instance.
* When the server replies, the **outbound response is automatically allowed**.

✅ Security Group = **Stateful**

---

## 2️⃣ **Stateless**

👉 A **stateless system/firewall** does **not remember connection states**.

* You must explicitly define rules for **both inbound and outbound traffic**.
* More granular control, but requires careful configuration.

🔑 **Key Points:**

* Doesn’t track sessions.
* Every packet is checked individually.
* Example in AWS → **Network ACL (NACLs)**.

**Example:**

* If you allow **inbound HTTP (TCP 80)** from the internet,
* You also must allow **outbound TCP (1024-65535)** (ephemeral ports) for the response.

✅ NACL = **Stateless**

---

## 📊 Comparison Table

| Feature                   | Stateful 🔒 (SG)        | Stateless 🚦 (NACL)          |
| ------------------------- | ----------------------- | ---------------------------- |
| **Remembers connection?** | Yes ✅                   | No ❌                         |
| **Response traffic**      | Auto allowed            | Needs explicit rule          |
| **Ease of use**           | Simpler                 | More complex                 |
| **AWS Example**           | Security Group          | Network ACL                  |
| **Best For**              | Instance-level firewall | Subnet-level extra filtering |

---

## 🎯 Easy Analogy

* **Stateful:** Like a **doorman** – if you are let in, the doorman remembers you and lets you out without asking again.
* **Stateless:** Like a **robotic gate** – it checks **every time** you go in or out, no memory of who you are.

---

## 🔑 Best Practices

1. Always use **Custom VPCs** for production
2. Place sensitive workloads in **private subnets**
3. Use **NAT Gateway** for private subnet internet access
4. Use **Transit Gateway** for multi-VPC connectivity
5. Enable **VPC Flow Logs** to monitor traffic
6. Avoid using **Default VPC** in production

---
