# 🛠️ **AWS Lambda Functions – Beginner Guide**

---

## 🌍 What is AWS Lambda?

* AWS Lambda is a **Serverless Compute Service** offered by AWS.
* *Serverless* doesn’t mean there are no servers. It means **you don’t manage the servers** – AWS does that for you.
* You just write your code (called a **Lambda Function**) and upload it. AWS takes care of:

  * Provisioning servers ⚙️
  * Scaling automatically 📈
  * Managing high availability 💯

👉 In short, **you focus on code, AWS manages infrastructure**.

---

## 🤔 Why use Lambda?

* 🚀 **No server management** – You don’t need to launch or maintain EC2.
* 💸 **Cost-effective** – You pay only when your code runs (Pay-Per-Request).
* 📈 **Scalable** – Automatically scales up and down depending on the number of requests.
* 🔌 **Easy integrations** – Can be triggered by AWS services like S3, API Gateway, DynamoDB, CloudWatch, etc.

---

## 🏗️ How Lambda Works (Basic Flow)

1. **Event Trigger** – Something happens (like uploading a file to S3 📂).
2. **Lambda Invokes Function** – AWS automatically runs your function code.
3. **Execution Environment** – AWS provides runtime (Node.js, Python, Java, etc.).
4. **Return Response** – Lambda returns output to the triggering service or API.

Example:

* Upload a photo to **S3** → Lambda function triggers → Creates a thumbnail → Saves it back to **S3**.

---

## ⚡ Key Concepts in Lambda

### 1. **Function** 📝

Your code (business logic) written in supported languages (Node.js, Python, Java, Go, etc.).

### 2. **Event** 📩

The input that triggers Lambda (API request, S3 upload, CloudWatch alarm, etc.).

### 3. **Handler** 🔄

The entry point of your Lambda function.

* Example in Node.js:

  ```js
  exports.handler = async (event) => {
      return "Hello from Lambda!";
  };
  ```

### 4. **Execution Role (IAM Role)** 🔐

Lambda needs permissions to access other AWS resources (like S3, RDS, DynamoDB).

* Example: If your function writes to S3, give **S3 write permission** via IAM role.

### 5. **Runtime** ⏳

Environment where your code runs. AWS provides runtimes like:

* Node.js
* Python
* Java
* Go
* .NET Core

### 6. **Timeout** ⏱️

Maximum time your Lambda can run (default 3 sec, max 15 min).

### 7. **Memory Allocation** 💾

You can configure memory (128 MB – 10 GB). CPU is allocated in proportion to memory.

---

## 🔗 Common Triggers for Lambda

* **API Gateway** 🌐 → For REST APIs
* **S3** 📂 → For file uploads
* **DynamoDB Streams** 📊 → For database changes
* **CloudWatch** ⏰ → For scheduled jobs (cron)
* **SNS** 📢 → For notifications

---

## 💡 Real-Time Use Cases of Lambda

* 🖼️ **Image Processing** – Resize/Compress images on upload.
* 📊 **Data Transformation** – Convert CSV to JSON before storing.
* 🔔 **Notifications** – Trigger an email/SMS when an event occurs.
* 🔄 **ETL Jobs** – Extract, Transform, Load data pipelines.
* 🌐 **Serverless APIs** – Run backend logic via API Gateway + Lambda.

---

## 🏆 Advantages of Lambda

✅ Fully managed (no servers)
✅ Pay only for execution time
✅ Highly scalable
✅ Integrates with many AWS services

---

## ⚠️ Limitations of Lambda

❌ Max execution time = 15 minutes
❌ Limited temporary storage (/tmp up to 512MB or configurable ephemeral storage up to 10GB)
❌ Cold start issue (slight delay when function runs after being idle)
❌ Not ideal for heavy long-running tasks

---

## 📌 Example – Simple Lambda Flow

1. User uploads a file to S3 → 📂
2. Lambda triggers → 🏃‍♂️
3. Function processes file → 🛠️
4. Result stored in DynamoDB → 📊

All done without provisioning a single server 🎉.