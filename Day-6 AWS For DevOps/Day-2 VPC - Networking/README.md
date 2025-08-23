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

## 5️⃣ IP Classes (IPv4)

| Class | Range                       | Default Subnet Mask | Use Case        |
| ----- | --------------------------- | ------------------- | --------------- |
| A     | 1.0.0.0 – 126.255.255.255   | /8                  | Large networks  |
| B     | 128.0.0.0 – 191.255.255.255 | /16                 | Medium networks |
| C     | 192.0.0.0 – 223.255.255.255 | /24                 | Small networks  |
| D     | 224.0.0.0 – 239.255.255.255 | N/A                 | Multicast       |
| E     | 240.0.0.0 – 255.255.255.255 | N/A                 | Experimental    |

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

## 🔑 Best Practices

1. Always use **Custom VPCs** for production
2. Place sensitive workloads in **private subnets**
3. Use **NAT Gateway** for private subnet internet access
4. Use **Transit Gateway** for multi-VPC connectivity
5. Enable **VPC Flow Logs** to monitor traffic
6. Avoid using **Default VPC** in production

---

✅ This covers everything about **VPC, IP addressing, subnets, NAT, Transit Gateway, Direct Connect, security, and best practices**, with real-world examples and visuals for teaching.

---