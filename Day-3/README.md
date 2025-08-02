# 🧠 DevOps Batch-8: Linux For DevOps

---

### 1️⃣ **What is Linux?**

* An open-source, Unix-like OS kernel developed by Linus Torvalds.
* Used in servers, desktops, cloud environments, containers, and embedded systems.
* Built on the Linux kernel + GNU utilities.

---

### 2️⃣ **Why is Linux Needed in DevOps?**

* Core for running DevOps tools (Docker, Jenkins, Ansible, Kubernetes).
* Most cloud environments (AWS, GCP, Azure) use Linux-based OS.
* Scriptable and easily automated (Bash, Python).
* Better resource management for servers.

---

### 3️⃣ **How Linux Benefits DevOps**

* 💻 Stability, performance, scalability.
* 🔐 Enhanced security and permission model.
* ⚙️ Highly scriptable (automation-ready).
* 🧩 Rich ecosystem of tools and community support.
* 💸 Open-source (cost-effective).

---

### 4️⃣ **Windows vs Linux**

| Feature      | Windows                   | Linux                         |
| ------------ | ------------------------- | ----------------------------- |
| Source       | Proprietary (Microsoft)   | Open Source (Community)       |
| Usage        | Desktop-centric           | Server, Cloud, DevOps-centric |
| Command Line | PowerShell/Command Prompt | Bash/Zsh                      |
| File System  | NTFS                      | ext4, xfs                     |
| Security     | User-dependent            | Permission & role-based       |

---

### 5️⃣ **Networking in Linux**

* View IP: `ip a`, `ifconfig`
* Configure IP: `nmcli`, `nmtui`, `netplan`
* Routing Table: `ip route`
* DNS Config: `/etc/resolv.conf`
* Test: `ping`, `curl`, `wget`, `traceroute`, `netstat`, `ss`, `nmap`

---

### 6️⃣ **Linux Shell**

* Interface between user and kernel.
* **Types**: Bash (default), Zsh, Ksh, Fish.
* Used to run commands, scripts, automation workflows.

---

### 7️⃣ **Flavours of OS in Windows and Linux**

* **Windows**: Home, Pro, Enterprise, Server Editions.
* **Linux**:

  * Debian-based: Ubuntu, Kali
  * RHEL-based: CentOS, Fedora, Rocky, Alma
  * Lightweight: Alpine, Arch
  * Cloud-optimized: Amazon Linux, Ubuntu Server

---

### 8️⃣ **Setup Windows and Linux EC2 Instance**

* Use AWS Console or CLI.
* Choose AMI → Instance Type → Key Pair → Security Group (port 22/3389).
* Linux: Connect via SSH.
* Windows: Connect via RDP.

---

### 9️⃣ **Free Practice Without EC2**

* 🔗 [Katacoda](https://www.katacoda.com/)
* 🔗 [Play with Docker](https://labs.play-with-docker.com/)
* 🔗 [KodeKloud](https://kodekloud.com/)
* 🔗 [Ubuntu Pro Terminal](https://ubuntu.com/tutorials/command-line-for-beginners#1-overview)
* 🔗 [Replit](https://replit.com/)
* 🔗 [Glitch](https://glitch.com/)

---

### 🔟 **Connection Method: Windows vs Linux**

| OS      | Tool                | Default Port |
| ------- | ------------------- | ------------ |
| Windows | RDP / PuTTY         | 3389 / 22    |
| Linux   | SSH (`ssh user@ip`) | 22           |
| Mac     | Terminal SSH        | 22           |

---

### 1️⃣1️⃣ **SSH Key or Password**

* SSH Key is preferred (secure, automated, scalable).
* Key files: `.pem`, `.ppk`
* Use `ssh-keygen`, `ssh-copy-id`, and key pairs for authentication.
* Passwords are more vulnerable.

---

### 1️⃣2️⃣ **Essential Linux Commands**

* Files: `ls`, `cd`, `pwd`, `touch`, `mkdir`, `rm`, `cp`, `mv`
* Viewing: `cat`, `less`, `tail`, `head`
* Disk: `df -h`, `du -sh`
* Processes: `ps`, `top`, `htop`, `kill`
* Network: `ip`, `ss`, `netstat`, `curl`
* Permissions: `chmod`, `chown`, `umask`

---

### 1️⃣3️⃣ **Terminal Utilities**

* CLI Editors: `nano`, `vim`, `vi`
* Monitoring: `top`, `htop`, `watch`
* Multiplexer: `tmux`, `screen`
* Logs: `tail -f`, `journalctl`

---

### 1️⃣4️⃣ **User Management**

* Add user: `adduser username`
* Delete user: `userdel username`
* User roles: `usermod -aG group user`
* Switch: `su`, `sudo -i`, `whoami`
* Configs: `/etc/passwd`, `/etc/shadow`

---

### 1️⃣5️⃣ **File Permission**

* `ls -l`: View permissions
* Permissions: r (read), w (write), x (execute)
* `chmod 755 file`
* `chown user:group file`

---

### 1️⃣6️⃣ **Special Permissions**

* **SetUID** (`chmod 4755`): Run with owner's privilege.
* **SetGID** (`chmod 2755`): Run with group’s privilege.
* **Sticky Bit** (`chmod 1777`): Restricts deletion to file owners (e.g. `/tmp`).

---

### 1️⃣7️⃣ **Install and Manage Packages**

| OS Family | Package Manager     | Examples            |
| --------- | ------------------- | ------------------- |
| Debian    | `apt`, `dpkg`       | `apt install nginx` |
| RHEL      | `yum`, `dnf`, `rpm` | `yum install httpd` |
| Alpine    | `apk`               | `apk add curl`      |

---

### 1️⃣8️⃣ **Service Management**

* **Systemd** commands:

  * Start: `systemctl start nginx`
  * Stop: `systemctl stop nginx`
  * Enable: `systemctl enable nginx`
  * Status: `systemctl status nginx`
  * Logs: `journalctl -u nginx`

---

### 1️⃣9️⃣ **Bash Scripting**

* Start with: `#!/bin/bash`
* Use: Variables, if-else, loops, functions.

```bash
#!/bin/bash
echo "Hello, $USER!"
uptime
```

---

### 2️⃣0️⃣ **Python Scripting**

* Python is pre-installed on most Linux distros.
* Use for automation, data parsing, monitoring.

```python
#!/usr/bin/python3
import os
print("Hostname:", os.uname().nodename)
```

---

### 2️⃣1️⃣ **Troubleshooting Tips**

* **Disk Issues**: `df -h`, `du -sh *`, `mount`
* **Package Errors**: `apt update`, `yum clean all`, `dpkg --configure -a`
* **Service Failures**: `systemctl status`, `journalctl -xe`
* **Network**: `ping`, `ss`, `curl`, `traceroute`

---

### 2️⃣2️⃣ **Monitoring Commands**

* `top`, `htop`: CPU, memory
* `free -m`: RAM usage
* `vmstat`, `iostat`: System performance
* `uptime`: Load average
* `netstat -tuln`, `ss -tuln`: Listening ports
* `ps aux --sort=-%mem`: High memory-consuming processes

---

# 🌐 Top 10 Free Linux & Kubernetes Playground Websites

This curated list provides **free and browser-based playgrounds** to practice **Linux commands**, **Kubernetes**, **Docker**, **Git**, and more — no installation or cloud subscription needed.

---

## 🚀 1. [KillerCoda](https://killercoda.com/)
- **Focus:** Linux, Kubernetes, Docker, Git, Helm
- **Features:**
  - Real interactive terminal
  - Sandbox + guided scenarios
  - No signup required for many labs
- **Best For:** Kubernetes hands-on practice, DevOps learning

---

## 📘 2. [Katacoda](https://katacoda.com/)
- **Focus:** Kubernetes, Docker, Linux, Helm
- **Features:** Step-by-step interactive scenarios
- **Note:** Now part of O’Reilly learning platform

---

## 🧪 3. [Play with Kubernetes](https://labs.play-with-k8s.com/)
- **Focus:** Real K8s multi-node cluster
- **Features:** Simulate clusters, run real-time K8s commands
- **Session Limit:** 4 hours

---

## 🐳 4. [Play with Docker](https://labs.play-with-docker.com/)
- **Focus:** Docker CLI, Swarm
- **Features:** Instant containers, multi-host support
- **Bonus:** Linux Alpine base system

---

## 👨‍💻 5. [KodeKloud Labs](https://kodekloud.com/labs/)
- **Focus:** Linux, Kubernetes, Ansible, Terraform, Git
- **Features:** Scenario-based hands-on labs
- **Free Tier:** Limited but sufficient for beginners

---

## 📦 6. [Kubernetes Bootcamp (Official)](https://kubernetes.io/docs/tutorials/kubernetes-basics/)
- **Focus:** Kubernetes basics
- **Features:** Built-in interactive terminal and tutorials

---

## 🧰 7. [Instruqt](https://instruqt.com/)
- **Focus:** Linux, DevOps, Kubernetes, Terraform
- **Features:** Real browser-based environments, community tracks

---

## 🖥️ 8. [TutorialsPoint Terminal](https://www.tutorialspoint.com/unix_terminal_online.php)
- **Focus:** Linux/Unix CLI
- **Features:** Simple browser shell to test Linux commands

---

## ☁️ 9. [Google Cloud Shell](https://shell.cloud.google.com/)
- **Focus:** Linux terminal with GCP tools
- **Features:** 5 GB persistent disk, preinstalled tools (gcloud, kubectl, Python)

---

## 🧑‍🔧 10. [GitPod](https://gitpod.io/)
- **Focus:** Linux shell, DevOps workflows, Kubernetes dev
- **Features:** Full dev environments, VS Code in browser

---

## ✅ Bonus
- [AWS CloudShell](https://aws.amazon.com/cloudshell/)
- [Replit](https://replit.com/)
- [Glitch](https://glitch.com/)
- [DevOps Playground](https://www.devopsplayground.com/)

---

## 🛠️ Ideal For:
- Practicing Linux & Kubernetes CLI
- Learning DevOps tools hands-on
- Preparing for certifications (CKA, CKAD, etc.)

> 💬 Feel free to fork this list and contribute more platforms!

---
