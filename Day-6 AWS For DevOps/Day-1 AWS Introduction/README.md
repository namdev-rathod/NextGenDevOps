# 🌟 Day-1 Introduction to Cloud & AWS

### ☁️ What is Cloud Technologies?

Cloud technologies allow businesses and individuals to use computing resources like servers, databases, storage, networking, and applications over the internet instead of owning and maintaining physical hardware.

👉 Example: Netflix doesn’t run its own massive data centers — it uses **AWS Cloud** to stream billions of hours of content globally.

---

### 🏢 On-Premises vs Cloud Technologies

* **On-Premises**: Companies buy and maintain physical servers, networking devices, cooling, and security on their own premises.

  * ❌ High upfront costs
  * ❌ Limited scalability (takes months to add new hardware)
  * ❌ Maintenance overhead (security patches, upgrades, electricity, staff)

* **Cloud**: Rent resources on-demand from providers like AWS, Azure, or GCP.

  * ✅ Pay-as-you-go pricing
  * ✅ Infinite scalability within minutes
  * ✅ Managed infrastructure (security, upgrades, availability)

👉 Example: Startups like **Airbnb** scaled rapidly on AWS without buying servers upfront.

---

### 🎯 Benefits of Cloud

* **Cost Efficiency** 💰 – Only pay for what you use (e.g., EC2 per second billing).
* **Scalability** 📈 – Scale up during high traffic (Amazon Prime Day) and scale down during low usage.
* **Global Reach** 🌍 – Deploy apps close to customers worldwide.
* **High Availability & Reliability** 🔄 – Built-in redundancy using Availability Zones.
* **Security** 🔒 – Enterprise-grade security managed by AWS.

---


## 🏢 On-Premises vs ☁️ Cloud (CAPEX vs OPEX)

| Aspect          | On-Premises (CAPEX) 💰                                      | Cloud (OPEX) ☁️                         |
| --------------- | ----------------------------------------------------------- | --------------------------------------- |
| **Cost Model**  | Large upfront investment in servers, data centers, licenses | Pay-as-you-go (per hour/GB/service)     |
| **Scalability** | Limited, need to buy new hardware                           | Highly scalable, almost instant         |
| **Maintenance** | Company responsible (hardware, power, cooling, staff)       | Managed by cloud provider               |
| **Flexibility** | Low – fixed re
sources                                       | High – resources on demand              |
| **Risk**        | Risk of underutilization or over-provisioning               | Reduced risk, only pay for what you use |
| **Example**     | Bank builds \$2M data center                                | Startup spends \$200/month on AWS       |

---

### 📌 Short Definitions

* **CAPEX (Capital Expenditure)**: *Upfront, long-term investment in physical infrastructure (servers, data centers, licenses).*
* **OPEX (Operational Expenditure)**: *Ongoing cost where you pay only for what you use (subscription/pay-per-use model).*

---

⚡ Quick Analogy:

* **CAPEX = Buying a Car 🚗** (big one-time cost, you own it, maintenance is your responsibility).
* **OPEX = Using Uber/Ola 🚕** (pay per ride, no ownership, provider maintains it).

---

### 🚀 AWS Free Tier (Free Plan) – 2025 Update

## 🆕 What Changed After **July 15, 2025**?

* 🎁 **\$100 AWS Credits** instantly on sign-up.
* ➕ **Earn up to \$100 more** by completing simple **hands-on activities** (e.g., launch EC2, deploy Lambda, configure RDS, set a budget, test Amazon Bedrock).
  👉 [AWS Blog – Free Tier Update](https://aws.amazon.com/blogs/aws/aws-free-tier-update-new-customers-can-get-started-and-explore-aws-with-up-to-200-in-credits/?utm_source=chatgpt.com)
* 🆓 Explore AWS with the **Free Plan** (risk-free, no bills unless you upgrade).
  👉 [AWS Free Tier Overview](https://aws.amazon.com/free/?utm_source=chatgpt.com)
* ♾️ **30+ Always-Free Services** remain available, e.g., Lambda, DynamoDB, S3, CloudWatch.
  👉 [AWS Docs – Free Tier Services](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/free-tier.html?utm_source=chatgpt.com)
* ⏳ Free Plan lasts **6 months or until credits expire**.
  👉 [AWS Docs – Free Plan Details](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/free-tier-plans.html?utm_source=chatgpt.com)

---

## 📊 Free Plan vs Paid Plan (Comparison)

| Feature                    | Free Plan (New Accounts)                                                                                                                          | Paid Plan (Optional Upgrade)          |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------- |
| **Initial Credits**        | \$100 sign-up + earn \$100 via activities                                                                                                         | Same                                  |
| **Access to AWS Services** | Limited set + always-free services                                                                                                                | Full access to 150+ AWS services      |
| **Charges**                | None while credits last                                                                                                                           | Pay-as-you-go (credits applied first) |
| **Account Duration**       | Ends after 6 months or credits expire                                                                                                             | Unlimited (pay-as-you-go)             |
| **Post-Expiry**            | Can be upgraded within 90 days ([docs](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/free-tier-plans.html?utm_source=chatgpt.com)) | Continuous usage                      |
| **Eligibility**            | Only for new accounts (legacy Free Tier unaffected)                                                                                               | Available to all accounts             |

---

## 💡 Benefits

* 🎯 **Beginner-friendly onboarding**: Start with credits, no billing risk.
* 🛠️ **Earn by learning**: Hands-on with real services.
* 🛡️ **Cost safety net**: No surprise bills, credits enforce limits.
* 🔄 **Always-free core services**: Lambda, DynamoDB, CloudWatch, S3.

---

## 📝 Getting Started

1. **Sign up** → [AWS Free Tier Page](https://aws.amazon.com/free/?utm_source=chatgpt.com)
2. **Complete activity goals** → Earn full \$200 credits.
3. **Enable AWS Budgets** → [Docs – AWS Budgets](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html?utm_source=chatgpt.com)
4. **Track usage** → [AWS Cost Explorer](https://docs.aws.amazon.com/cost-management/latest/userguide/ce-what-is.html?utm_source=chatgpt.com)
5. **Upgrade if needed** before Free Plan expires.

👉 Example: Many students and startups begin with the Free Tier to test ideas before investing.

🔗 [AWS Free Tier Official Page](https://aws.amazon.com/free/)

---

### 🌍 AWS Global Infrastructure

AWS has the **largest cloud infrastructure in the world**.

* **Regions** 🌎: Physical locations around the world (e.g., `us-east-1` in Virginia, `ap-south-1` in Mumbai). Currently, AWS has **36 Regions** and expanding.
* **Availability Zones (AZs)** 🏗️: Each region has **2–6 AZs**, which are isolated data centers connected with low-latency networking. If one AZ goes down, others keep running.
* **Edge Locations** ⚡: 600+ points of presence used by **CloudFront CDN** to cache content closer to users for low-latency performance.

👉 Example:

* Netflix uses **AWS Regions** and **Edge Locations** to ensure smooth streaming worldwide.
* Amazon.com itself relies on **multi-AZ deployments** for 24/7 uptime during huge sales like Black Friday.

🔗 [AWS Global Infrastructure](https://aws.amazon.com/about-aws/global-infrastructure/)

---

### 💰 AWS Budget Setup (Cost Control from Day 1)

AWS provides **Budgets & Cost Explorer** to track and manage costs.

* **Set a Budget** 📊: Define a monthly threshold (e.g., \$10).
* **Alerts** 🔔: Receive email alerts when usage crosses 80% or 100% of your budget.
* **Best Practice**: Always enable **Billing Alerts** immediately after account creation to avoid accidental charges.

👉 Example: Many learners forget to delete unused EC2 instances and get charged. A budget alert prevents surprise bills.

---



