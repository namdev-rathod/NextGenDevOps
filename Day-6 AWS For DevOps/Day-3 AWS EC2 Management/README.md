# 📘 DevOps Training Notes – **EC2 Management**

Amazon Elastic Compute Cloud (**EC2**) is the core compute service in AWS. It provides resizable virtual servers in the cloud that can run applications, host workloads, and scale as per demand. For DevOps engineers, EC2 is the foundation for building, deploying, and managing scalable applications.

---

## 1. 🔹 What is EC2?

* EC2 = Elastic Compute Cloud → Infrastructure-as-a-Service (IaaS).
* Provides secure, resizable compute capacity.
* Can launch servers (instances) on demand, without buying hardware.
* Instances can be integrated with **EBS (storage)**, **VPC (networking)**, and **IAM (security)**.

👉 **Example:** Hosting a Node.js application on an EC2 instance inside a VPC with a load balancer.

---

## 2. 🔹 EC2 Instance Types

EC2 instances are grouped by families, optimized for different workloads:

| **Family**                               | **Optimized For**      | **Example Use Case**         |
| ---------------------------------------- | ---------------------- | ---------------------------- |
| **General Purpose (t3, m5)**             | Balanced CPU & Memory  | Web servers, small DBs       |
| **Compute Optimized (c5)**               | High CPU               | Gaming servers, CI/CD builds |
| **Memory Optimized (r5, x1)**            | High RAM               | In-memory DBs, caching       |
| **Storage Optimized (i3, d2)**           | High IOPS & Throughput | Data warehousing, big data   |
| **Accelerated Computing (p3, g4, inf1)** | GPUs, ML, HPC          | AI/ML, graphics rendering    |

👉 **DevOps Tip:** Always match instance type with workload to avoid **over-provisioning costs**.

---

## 3. 🔹 Instance Types Comparison

* **x86 vs ARM (Graviton)**

  * Graviton (AWS ARM-based CPUs) → Cheaper (\~40% cost savings), energy efficient.
  * x86 → Legacy apps, broader compatibility.

* **On-Demand vs Spot vs Reserved**

  * **On-Demand**: Pay per second/minute, flexible, no commitments.
  * **Reserved**: 1–3 year contracts, cheaper (up to 72%).
  * **Spot Instances**: Cheapest (up to 90% savings), but can be terminated anytime. Great for CI/CD builds, batch jobs.

👉 **DevOps Use Case:** Use **Spot instances for Jenkins workers**, On-Demand for critical workloads, Reserved for predictable apps.

---

## 4. 🔹 Elastic IPs & Networking

* **Public IP**: Assigned dynamically when an instance starts; changes on stop/start.
* **Elastic IP (EIP)**: Static IPv4 address, persistent even after stopping/starting.
* **Private IP**: Used for internal communication inside a VPC.

👉 **Best Practice:** Use **Elastic Load Balancer (ELB)** or **Route 53 DNS** instead of relying on Elastic IPs.

---

## 5. 🔹 EC2 Storage Management

* **EBS (Elastic Block Store)** → Persistent storage attached to instances. Types:

  * gp3 (General Purpose SSD) → Balanced price/performance.
  * io2 (Provisioned IOPS SSD) → High-performance DBs.
  * st1 (Throughput Optimized HDD) → Big data, log storage.
* **Instance Store** → Temporary storage, deleted on stop/terminate.
* **EFS (Elastic File System)** → Managed NFS, shared across instances.

👉 **DevOps Tip:** Store **application logs on EFS or S3**, not on instance root volume.

---

## 6. 🔹 EC2 Security

* **Security Groups** → Virtual firewalls (allow rules only).
* **NACLs (Network ACLs)** → Subnet-level rules (allow + deny).
* **IAM Roles** → Assign permissions to EC2 (e.g., access S3, Secrets Manager).
* **Key Pairs (SSH keys)** → Used for secure login.

👉 **Best Practice:** Use **SSM Session Manager** instead of SSH for audit & security.

---

## 7. 🔹 Scaling & High Availability

* **Elastic Load Balancer (ELB)**: Distributes traffic across EC2s.
* **Auto Scaling Groups (ASG)**: Scales instances in/out based on demand.
* **Placement Groups**:

  * Cluster → Low latency, high throughput.
  * Spread → Fault tolerance across hardware.
  * Partition → Big data workloads.

👉 **DevOps Real Case:** Configure **ASG + ELB** to handle peak traffic during sales events.

---

## 8. 🔹 Monitoring & Maintenance

* **CloudWatch Metrics**: CPU, Network, Disk.
* **CloudWatch Logs**: Collect app/system logs.
* **SSM Agent**: Run automation scripts across fleet.
* **EC2 Instance Connect**: Browser-based SSH access.

👉 **Cost Optimization Tip:**

* Stop unused dev/test instances outside office hours.
* Use **AWS Instance Scheduler Lambda** for automation.

---

## 9. 🔹 Backup & Recovery

* **Snapshots**: Incremental backups of EBS volumes.
* **AMI (Amazon Machine Image)**: Pre-baked OS + App image for launching multiple identical servers.
* **Disaster Recovery**: Cross-region replication of AMIs and snapshots.

👉 **DevOps Use Case:** Create AMIs for **golden images** of Jenkins or Nginx servers.

---

## 10. 🔹 Best Practices for DevOps

✅ Use **Infrastructure as Code (IaC)** → Terraform, AWS CDK, CloudFormation.
✅ Keep **immutable infrastructure** → Replace instances with new AMIs instead of manual patching.
✅ Always enable **detailed monitoring**.
✅ Tag resources (`Environment=Dev`, `Owner=TeamA`).
✅ Enforce **least privilege IAM roles**.
✅ Automate patching using **SSM Patch Manager**.
