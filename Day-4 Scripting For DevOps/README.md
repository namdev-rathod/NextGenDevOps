# 🚀 DevOps Scripting Essentials — Bash & Python for Real-Time Automation

> 📌 **Master practical automation with Bash & Python** — From fundamentals to real-world DevOps scripting projects.

---

## 1. What is Shell Scripting?

Bash (Bourne Again SHell) is the default shell for most Linux distributions.
Bash scripts are text files containing shell commands executed sequentially.

Shell scripting is the process of writing a series of commands in a text file (called a *script*) that can be executed by a shell interpreter (like **Bash**).
It automates repetitive tasks, simplifies complex operations, and is widely used in **system administration, application deployment, and DevOps workflows**.

**Advantages:**

✅ Direct interaction with OS commands.

✅ Lightweight, no interpreter installation needed on Linux.

✅ Best suited for system administration tasks.

**Structure of a Bash Script:**

```bash
#!/bin/bash     # Shebang line - interpreter
# Comments
variable="value" # Variables
command          # Linux commands
if condition; then
    commands
fi               # Control structures
```

---

## 💡 2. Why We Use Shell Scripting & Its Benefits

✅ **Automation** – Eliminates repetitive manual tasks.

✅ **Efficiency** – Simplifies complex commands into single execution.

✅ **Integration** – Works with tools like `awk`, `sed`, `grep`, APIs, and databases.

✅ **Cross-Platform** – Runs on most UNIX/Linux distributions.

✅ **Cost & Time Savings** – Speeds up deployments and reduces human error.


---

## 3. Introduction to Bash & Python Scripting

### **Bash Scripting**

Bash is a Unix shell and command language used for task automation directly on Linux/Unix environments.
It’s lightweight, fast, and ideal for system-level operations.

### **Python Scripting** 

Python is a versatile high-level language, widely used for **automation, data processing, API integrations**, and **DevOps tooling**.
It’s known for its readability, large library ecosystem, and cross-platform compatibility.

---

## ⚔️ 4. Bash vs Python — A Quick Comparison

| Feature ⚙️        | Bash 🐚                                     | Python 🐍                                      |
| ----------------- | ------------------------------------------- | ---------------------------------------------- |
| **Speed**         | Very fast for simple commands & system ops  | Slightly slower but powerful for complex logic |
| **Readability**   | Compact, but less readable for complex code | Very readable & beginner-friendly              |
| **Portability**   | Works natively on UNIX/Linux systems        | Cross-platform (Linux, macOS, Windows)         |
| **Best Use Case** | System admin tasks, file ops, server mgmt   | API calls, data processing, advanced logic     |

---

## 📌 5. Common Use Cases

### **Bash Use Cases**

* System updates & health checks 🖥️
* Log file monitoring & backups 📂
* Automated deployments 🚀

### **Python Use Cases**

* API automation 🌐
* Data extraction & transformation 📊
* Cloud resource provisioning ☁️

---

## 💻 6. Real-Time Projects

### **Bash Projects** 🐚

#### **1️⃣ Automated Server Backup**

**Description:** Creates daily compressed backups of important directories.
**Use Case:** Disaster recovery & data safety.

```bash
#!/bin/bash
backup_dir="/root/backup"
source_dir="/var/www/html"
mkdir -p "$backup_dir"
tar -cvzf "$backup_dir/backup_$(date +%Y%m%d_%H%M%S).tar.gz" "$source_dir"
echo "✅ Backup completed successfully."
```

**(A) Automated Backup Script**

```bash
#!/bin/bash
backup_dir="/var/backups"
source_dir="/var/www/html"
mkdir -p "$backup_dir"

echo "Starting backup..."
tar -czf "$backup_dir/backup_$(date +%F_%H-%M-%S).tar.gz" "$source_dir"
echo "Backup completed successfully."
```

**Use Case:** Schedule with cron to run daily.

**(B) Log File Monitoring for Errors**

```bash
#!/bin/bash
log_file="/var/log/syslog"
error_count=$(grep -c "ERROR" "$log_file")

if [ "$error_count" -gt 0 ]; then
    echo "[$(date)] Errors found: $error_count" >> /var/log/error_monitor.log
fi
```

**Use Case:** Detect and log errors in production systems.

**(C) Disk Space Alert**

```bash
#!/bin/bash
threshold=80
df -h | awk 'NR>1 {print $5 " " $1}' | while read output; do
    usage=$(echo $output | awk '{print $1}' | tr -d '%')
    partition=$(echo $output | awk '{print $2}')
    if [ $usage -ge $threshold ]; then
        echo "Warning: $partition is $usage% full."
    fi
done
```

**Use Case:** Trigger alerts when disk space exceeds a threshold.

---

#### **2️⃣ System Health Monitoring**

**Description:** Monitors CPU, memory, and disk usage, and alerts when thresholds exceed.
**Use Case:** Prevent server downtime by early detection of resource issues.

```bash
#!/bin/bash
cpu=$(top -bn1 | grep "Cpu(s)" | awk '{print $2 + $4}')
disk=$(df / | grep / | awk '{ print $5 }' | sed 's/%//g')
if [ "$cpu" -gt 80 ] || [ "$disk" -gt 80 ]; then
    echo "⚠️ High resource usage detected!"
else
    echo "✅ System is healthy."
fi
```

---

#### **3️⃣ Log File Error Alerts**

**Description:** Checks logs for error keywords and sends alerts.
**Use Case:** Helps in quick incident response for production systems.

```bash
#!/bin/bash
log_file="/var/log/syslog"
if grep -qi "error" "$log_file"; then
    echo "⚠️ Errors found in system logs."
else
    echo "✅ No critical errors detected."
fi
```

---

### **Python Projects** 🐍

Python is a high-level, interpreted language with excellent support for scripting and automation.

**Advantages:**

✅ Cross-platform.

✅ Rich standard library + third-party packages.

✅ Better suited for complex logic, APIs, and data processing.

**Basic Structure of a Python Script:**

```bash
#!/usr/bin/python3
# Comments
variable = "value"
print(variable)

if condition:
    # do something
```

**Real-Time Examples**

**(A) File Backup Script**

```python
#!/usr/bin/python3
import os
import shutil
from datetime import datetime

source_dir = "/var/www/html"
backup_dir = "/var/backups"

os.makedirs(backup_dir, exist_ok=True)
backup_name = f"backup_{datetime.now().strftime('%Y%m%d_%H%M%S')}.tar.gz"
shutil.make_archive(os.path.join(backup_dir, backup_name.replace(".tar.gz", "")), 'gztar', source_dir)

print("Backup completed successfully.")
```

**Use Cases:** Works cross-platform, integrates with logging and email notifications.

**(B) Monitor Website Availability**

```python
#!/usr/bin/python3
import requests
from datetime import datetime

url = "https://uxito.net"

try:
    response = requests.get(url, timeout=5)
    if response.status_code == 200:
        print(f"{datetime.now()} - {url} is UP")
    else:
        print(f"{datetime.now()} - {url} is DOWN (Status {response.status_code})")
except requests.exceptions.RequestException as e:
    print(f"{datetime.now()} - {url} is DOWN ({e})")
```

**Use Case:** Monitor service health and integrate with alerting systems.

#### **Website Uptime Checker**

**Description:** Checks if a website is online and responds within a given time.
**Use Case:** Monitor production websites for outages.

```python
import requests

url = "https://uxito.net"
try:
    response = requests.get(url, timeout=5)
    if response.status_code == 200:
        print("✅ Website is UP.")
    else:
        print(f"⚠️ Website returned status {response.status_code}")
except requests.exceptions.RequestException:
    print("❌ Website is DOWN.")
```

---

#### **AWS S3 Bucket Backup Script**

**Description:** Uploads local files to S3 for backup purposes.
**Use Case:** Cloud-based backup strategy.

```python
import boto3
import os

s3 = boto3.client('s3')
bucket_name = "my-backup-bucket"
folder = "/path/to/data"

for file in os.listdir(folder):
    file_path = os.path.join(folder, file)
    if os.path.isfile(file_path):
        s3.upload_file(file_path, bucket_name, file)
        print(f"✅ Uploaded {file} to S3.")
```

---

#### **Automated Email Alert System**

**Description:** Sends an email alert when a specific condition is met.
**Use Case:** Notify admins of critical events.

```python
import smtplib
from email.mime.text import MIMEText

msg = MIMEText("⚠️ High CPU usage detected on server.")
msg["Subject"] = "Server Alert"
msg["From"] = "admin@uxito.net"
msg["To"] = "ops@uxito.net"

with smtplib.SMTP("smtp.uxito.net") as server:
    server.login("admin@uxito.net", "password")
    server.sendmail(msg["From"], [msg["To"]], msg.as_string())

print("✅ Alert email sent.")
```

---

### **Choosing Between Bash and Python**

| Feature         | Bash                               | Python                              |
| --------------- | ---------------------------------- | ----------------------------------- |
| **Best for**    | System administration, quick tasks | Complex logic, cross-platform tasks |
| **Speed**       | Faster for simple OS commands      | Slightly slower for small scripts   |
| **Libraries**   | Limited (mostly system utilities)  | Huge ecosystem (requests, pandas…)  |
| **Readability** | Can get messy with complex logic   | Clear and maintainable              |
| **Portability** | Unix/Linux native                  | Cross-platform (Windows/Linux/Mac)  |


---

# **1. Real-Time Bash Scripting Examples**

---

## **Bash Example 1 – Automated Log Rotation**

**Purpose:** Rotate and compress old logs to save disk space.

```bash
#!/bin/bash
log_dir="/var/log/myapp"
backup_dir="/var/backups/myapp_logs"
mkdir -p "$backup_dir"

find "$log_dir" -type f -name "*.log" -mtime +7 -exec tar -czf "$backup_dir/logs_$(date +%F).tar.gz" {} +
find "$log_dir" -type f -name "*.log" -mtime +7 -delete

echo "Old logs archived and deleted."
```

**Use Case:** Run via cron to keep production log files small.

---

## **Bash Example 2 – Service Health Check**

**Purpose:** Check if a service is running and restart if stopped.

```bash
#!/bin/bash
service_name="nginx"

if ! systemctl is-active --quiet $service_name; then
    echo "[$(date)] $service_name is DOWN. Restarting..."
    systemctl start $service_name
else
    echo "[$(date)] $service_name is UP."
fi
```

**Use Case:** Keeps critical services like `nginx`, `mysql`, etc. always running.

---

## **Bash Example 3 – Daily Database Backup**

**Purpose:** Backup MySQL database daily.

```bash
#!/bin/bash
backup_dir="/var/backups/mysql"
mkdir -p "$backup_dir"
db_name="mydb"
db_user="root"
db_pass="password"

mysqldump -u $db_user -p$db_pass $db_name > "$backup_dir/${db_name}_$(date +%F).sql"
gzip "$backup_dir/${db_name}_$(date +%F).sql"

echo "Database backup completed: $backup_dir/${db_name}_$(date +%F).sql.gz"
```

**Use Case:** Used in production to automate DB backups.

---

# **2. Real-Time Python Scripting Examples**

---

## **Python Example 1 – Server Resource Monitoring**

**Purpose:** Monitor CPU, RAM, and Disk usage; send alerts when thresholds exceed.

```python
#!/usr/bin/python3
import psutil
import smtplib

# Thresholds
CPU_THRESHOLD = 80
MEM_THRESHOLD = 80

# Check CPU
cpu_usage = psutil.cpu_percent(interval=1)
mem_usage = psutil.virtual_memory().percent

if cpu_usage > CPU_THRESHOLD or mem_usage > MEM_THRESHOLD:
    alert_message = f"ALERT! CPU: {cpu_usage}% | Memory: {mem_usage}%"
    print(alert_message)

    # Email alert (example)
    server = smtplib.SMTP('smtp.uxito.net', 587)
    server.starttls()
    server.login("user@uxito.net", "password")
    server.sendmail("user@uxito.net", "admin@uxito.net", alert_message)
    server.quit()
else:
    print(f"CPU: {cpu_usage}% | Memory: {mem_usage}% - OK")
```

**Use Case:** Monitor production server health & alert admins.

---

## **Python Example 2 – API Data Fetch & Save**

**Purpose:** Fetch GitHub user details via API and store in JSON file.

```python
#!/usr/bin/python3
import requests
import json

username = "octocat"
url = f"https://api.github.com/users/{username}"
response = requests.get(url)

if response.status_code == 200:
    data = response.json()
    with open(f"{username}_details.json", "w") as f:
        json.dump(data, f, indent=4)
    print(f"User data saved for {username}")
else:
    print(f"Failed to fetch data: {response.status_code}")
```

**Use Case:** Automate API integrations for reporting dashboards.

---

## **Python Example 3 – S3 File Upload**

**Purpose:** Upload a local file to AWS S3 bucket.

```python
#!/usr/bin/python3
import boto3

s3 = boto3.client('s3')
bucket_name = "my-backup-bucket"
file_path = "/var/backups/mysql_backup.sql.gz"

try:
    s3.upload_file(file_path, bucket_name, "mysql_backup.sql.gz")
    print("File uploaded successfully to S3.")
except Exception as e:
    print(f"Upload failed: {e}")
```

**Use Case:** Backup automation to cloud storage in DevOps pipelines.

---

## **How to Use Them Together (Bash + Python Hybrid Example)**

* **Bash** → Runs system commands, handles scheduling, and triggers Python scripts.
* **Python** → Handles advanced logic, data processing, API calls.

**Example:**

```bash
#!/bin/bash
# Run server monitoring (Python script)
python3 /opt/scripts/server_monitor.py
# If monitoring finds issues, it logs them, and this Bash script emails logs
cat /var/log/server_monitor.log | mail -s "Server Alert" admin@uxito.net
```

---



## 📚 7. Best Reference Links

🔹 [GeeksforGeeks - Shell Scripting](https://www.geeksforgeeks.org/introduction-linux-shell-shell-scripting/)

🔹 [TutorialsPoint - Bash Scripting](https://www.tutorialspoint.com/unix/shell_scripting.htm)

🔹 [FreeCodeCamp - Bash Guide](https://www.freecodecamp.org/news/shell-scripting-crash-course-how-to-write-bash-scripts-in-linux/)

🔹 [Python Official Documentation](https://docs.python.org/3/tutorial/)

🔹 [AWS Boto3 Documentation](https://boto3.amazonaws.com/v1/documentation/api/latest/index.html)

---


