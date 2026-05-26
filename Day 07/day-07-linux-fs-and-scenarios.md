# Day 07 – Linux File System Hierarchy & Scenario-Based Practice

## Task

Today's goal is to understand where things live in Linux and practice troubleshooting like a DevOps engineer.  
You will create notes covering:

* Linux File System Hierarchy (the most important directories)  
* Practice solving real-world scenarios step by step

This consolidates your Linux fundamentals and prepares you for real-world troubleshooting.

### Part 1: Linux File System Hierarchy

* **/ (root)**

Contains the entire Linux filesystem hierarchy.  
 All directories start from this root directory.

**Command:**

**ls \-l /**

**Observation:**  
 Saw directories like home, etc, var, tmp.

**I would use this when...**  
 **I need to navigate the Linux filesystem structure.**

---

* **/home**

Contains personal directories for normal users.  
 Users store files, downloads, and configurations here.

**Command:**   ls \-l /home

**Observation:**  
 Saw user home directories.

**I would use this when...**  
 I need to access user files or application data.

---

* **/root**

**Home directory for the root user.**  
 **Stores administrative files and scripts.**

**Command:**

sudo ls \-l /root

**Observation:**  
 Saw root-owned configuration and files.

**I would use this when...**  
 I perform system administration tasks.

---

* **/etc**

Contains system-wide configuration files.  
 Most service configurations are stored here.

**Command:**

ls \-l /etc | head

**Observation:**  
 **Saw directories like nginx, ssh, and systemd.**

I would use this when...  
 I need to modify service or system configurations.

---

* **/var/log**

Stores application and system log files.  
 Very important for troubleshooting.

**Command:**

ls \-l /var/log | head

**Observation:**  
 **Saw files like syslog, auth.log, nginx logs.**

**I** would use this when...  
 I troubleshoot system or application issues**.**

---

* **/tmp**

Stores temporary files created by applications.  
 Files here may be removed automatically.

**Command:**

ls \-l /tmp | head

**Observation:**  
 **Saw temporary directories and files.**

I would use this when...  
 I need temporary storage during testing or scripting.

---

* **/bin**

Contains essential Linux command binaries.  
 Basic commands required for system operation are stored here.

**Command:**

ls \-l /bin | head

**Observation:**  
 **Saw binaries like bash, ls, cp.**

I would use this when...  
 I want to locate core Linux commands.

---

* **/usr/bin**

Contains user-level binaries and installed programs.  
 Most applications are stored here.

**Command:**

ls \-l /usr/bin | head

**Observation:**  
 Saw many executable programs and utilities.

I would use this when...  
 I need to find installed application binaries.

---

* **/opt**

Contains optional and third-party applications.  
 Custom software installations are commonly stored here.

**Command:**

ls \-l /opt

* **Question: How do you check if the 'nginx' service is running?**

Ans- \> systemctl status nginx

* **For list of all services are running right now** 

Command:  
systemctl list-units \--type=service  
	  
Why this command?  
To list all active systemd services running on the system.

* **If those services are not running, then run the following command:**

	  
	Command:  
systemctl is-enabled nginx 

Why this command?  
To check if nginx starts automatically after reboot.

What I learned:  
Always verify service startup behavior during troubleshooting.

* **If you want to stop the services:** 

	systemctl stop nginx

* **Scenario 1: Service Not Starting**

Step 1:  
 Command:

systemctl status myapp

Why:  
 To check whether the service is active, failed, or stopped.

---

Step 2:  
 Command:

journalctl \-u myapp \-n 50 \--no-pager

Why:  
 To review the latest logs and identify startup errors.

---

Step 3:  
 Command:

systemctl is-enabled myapp

Why:  
 To verify whether the service is configured to start automatically after reboot.

---

Step 4:  
 Command:

systemctl restart myapp

Why:  
 To attempt restarting the service after reviewing logs and status.

---

Scenario 2: High CPU Usage

Step 1:  
 Command:

top

Why:  
 To monitor live CPU and memory usage of running processes.

---

Step 2:  
 Command:

ps aux \--sort=-%cpu | head \-10

Why:  
 To identify the top CPU-consuming processes.

---

Step 3:  
 Command:

ps \-p \<PID\> \-o pid,ppid,cmd,%cpu,%mem

Example:

ps \-p 2456 \-o pid,ppid,cmd,%cpu,%mem

Why:  
 To inspect detailed information about the high CPU process.

---

Step 4:  
 Command:

htop

Why:  
 To get an interactive and easier view of system resource usage.

---

Scenario 3: Finding Service Logs

Step 1:  
 Command:

systemctl status docker

Why:  
 To check whether the docker service is running correctly.

---

Step 2:  
 Command:

journalctl \-u docker \-n 50 \--no-pager

Why:  
 To view the latest 50 lines of docker service logs.

---

Step 3:  
 Command:

journalctl \-u docker \-f

Why:  
 To monitor docker logs in real time.

---

Step 4:  
 Command:

journalctl \-u docker \--since today

Why:  
 To review logs generated since today for troubleshooting.

---

Scenario 4: File Permissions Issue

Step 1:  
 Command:

ls \-l /home/user/backup.sh

Why:  
 To check the current file permissions.

---

Step 2:  
 Command:

chmod \+x /home/user/backup.sh

Why:  
 To add execute permission to the script.

---

Step 3:  
 Command:

ls \-l /home/user/backup.sh

Why:  
 To verify the execute permission was successfully added.

---

Step 4:  
 Command:

./backup.sh  
