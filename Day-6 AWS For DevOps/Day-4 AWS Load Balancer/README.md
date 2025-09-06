# 📘 DevOps Training Notes – **AWS Load Balancers (Elastic Load Balancing)**

Load Balancing is a critical component in **high availability** and **scalable architecture**. AWS provides **Elastic Load Balancing (ELB)** service to automatically distribute incoming traffic across multiple targets such as **EC2, ECS, EKS, Lambda, and IP addresses**.

---

## 1. 🔹 What is a Load Balancer?

* A **load balancer** acts as a traffic distributor that routes client requests to multiple backend servers (targets).
* Ensures:

  * **High availability** → Traffic automatically re-routed if one target fails.
  * **Scalability** → Handles millions of requests by distributing traffic.
  * **Security** → Integrates with WAF, SSL/TLS offloading.
  * **Flexibility** → Supports different protocols (HTTP, HTTPS, TCP, UDP, gRPC).

👉 **Example:** A website running on 3 EC2 instances behind an Application Load Balancer (ALB). If one instance fails, traffic is rerouted to healthy instances.

---

## 2. 🔹 Types of AWS Load Balancers

AWS offers 4 types of load balancers under **Elastic Load Balancing (ELB)**:

### 2.1 **Application Load Balancer (ALB)**

* Works at **Layer 7 (HTTP/HTTPS)**.
* Best for **web applications** and **microservices**.
* Features:

  * Path-based routing (`/api`, `/images`).
  * Host-based routing (`app.example.com`, `api.example.com`).
  * Supports WebSockets & gRPC.
  * SSL termination.
  * Authentication with Cognito/IdP.
* **Use Case:** Routing traffic to different microservices in EKS/ECS based on URL paths.

---

### 2.2 **Network Load Balancer (NLB)**

* Works at **Layer 4 (TCP, UDP, TLS)**.
* Ultra-low latency, millions of requests per second.
* Preserves client IP.
* Supports static IP and Elastic IPs.
* **Use Case:** High-performance gaming servers, financial transactions, IoT devices.

---

### 2.3 **Gateway Load Balancer (GWLB)**

* Works at **Layer 3 (IP)**.
* Routes traffic to **third-party virtual appliances** like firewalls, intrusion detection/prevention systems.
* Supports transparent **inline inspection**.
* **Use Case:** Deploying Palo Alto firewall or IDS/IPS solutions in AWS.

---

### 2.4 **Classic Load Balancer (CLB)** *(Legacy)*

* Supports both Layer 4 & Layer 7.
* Being phased out → Use ALB or NLB instead.
* **Use Case:** Only for legacy apps still running on older AWS setups.

---

## 3. 🔹 Load Balancer Components

Every load balancer has these building blocks:

* **Listeners**:

  * Define protocol & port for frontend connections.
  * Example: `HTTP:80` → `EC2:8080`.

* **Target Groups**:

  * Group of registered targets (EC2, ECS, IP, Lambda).
  * Each target group has a **health check** configuration.

* **Health Checks**:

  * Periodic checks to see if a target is healthy.
  * Example: ALB health check on `/health` endpoint.

* **Rules & Routing**:

  * Based on host header, path, query string, or HTTP headers.
  * Example:

    * `api.example.com` → Microservice A.
    * `web.example.com` → Frontend service.

* **Security**:

  * **SSL/TLS termination** at LB → reduces CPU load on backend.
  * **Integration with AWS WAF** for DDoS & OWASP Top 10 protection.

---

## 4. 🔹 Load Balancer Networking

* **VPC Integration** → Load balancers must be deployed in subnets.
* **Internet-Facing LB** → Accessible from the internet.
* **Internal LB** → Used inside private VPCs for service-to-service communication.
* **Cross-Zone Load Balancing** → Distributes traffic evenly across all AZs.

👉 **Best Practice:** Always deploy LB across **multiple AZs** for high availability.

---

## 5. 🔹 Monitoring & Logging

* **CloudWatch Metrics**:

  * `RequestCount` → Total requests served.
  * `TargetResponseTime` → Latency between LB and target.
  * `HTTPCode_ELB_4XX/5XX` → Client/server errors.

* **Access Logs**:

  * Store detailed logs (request, client IP, latency) in **S3**.
  * Useful for debugging & analytics.

* **AWS X-Ray**:

  * For tracing requests through ALB.

---

## 6. 🔹 Load Balancer Security

* **Security Groups**:

  * ALB/NLB must allow inbound traffic on listener ports.
  * Target EC2 instances must allow inbound only from LB SG.

* **SSL/TLS Certificates**:

  * Managed via **AWS Certificate Manager (ACM)**.
  * Supports multiple domain certificates (SAN).

* **AWS WAF (Web Application Firewall)**:

  * Protects against SQL injection, XSS, bots.

👉 **Best Practice:** Terminate SSL at ALB → forward traffic internally using HTTP.

---

## 7. 🔹 Cost Considerations

* Billed for:

  1. **Load balancer hours** (uptime).
  2. **LCU (Load Balancer Capacity Units)** = new connections + active connections + processed bytes.

👉 **Cost Optimization:**

* Use NLB for high-volume TCP traffic.
* Use ALB for HTTP/HTTPS workloads.
* Stop unused dev/test LBs during off-hours.

---

## 8. 🔹 DevOps Best Practices

✅ Use **Infrastructure as Code (IaC)** → Terraform, AWS CDK, CloudFormation.
✅ Use **Target Groups** with Auto Scaling Groups (ASG) for EC2.
✅ Always configure **health checks** properly (`/health` endpoint).
✅ Enable **access logs & CloudWatch alarms**.
✅ Use **WAF + Shield** for production workloads.
✅ Implement **blue/green or canary deployments** with ALB rules.

---

## 9. 🔹 Real-Time DevOps Use Cases

1. **Blue/Green Deployment**

   * Two target groups (v1 & v2).
   * Switch traffic gradually using ALB rules.

2. **Microservices Routing**

   * `api.example.com` → ECS service.
   * `web.example.com` → EC2 frontend.

3. **Hybrid Architecture**

   * NLB fronting an on-premises VPN endpoint.

4. **Security Appliances**

   * GWLB routing traffic to firewall appliances.

5. **Serverless Integration**

   * ALB routing requests directly to **Lambda functions**.

---

📌 **Summary Table**

| LB Type | Layer | Protocols                     | Best Use Case                 |
| ------- | ----- | ----------------------------- | ----------------------------- |
| ALB     | L7    | HTTP, HTTPS, gRPC, WebSockets | Web apps, microservices       |
| NLB     | L4    | TCP, UDP, TLS                 | High performance, IoT, gaming |
| GWLB    | L3    | IP                            | Firewalls, IDS/IPS            |
| CLB     | L4/L7 | TCP, HTTP, HTTPS              | Legacy apps                   |