# Day 12 – Breather & Revision (Days 01–11)

\#\# What to Review

\#\#\# Mindset & Plan

After revisiting my Day 01 learning plan, my goals are still aligned with becoming a skilled DevOps and Cloud Engineer.

Current focus areas:  
\- Linux fundamentals  
\- Troubleshooting  
\- AWS & Cloud  
\- Docker  
\- Service management  
\- File permissions and ownership

Small tweaks:  
\- Spend more time on shell scripting  
\- Improve troubleshooting speed  
\- Practice real-world DevOps scenarios daily

\---

\# Processes & Services Review

\#\# Command 1  
\`\`\`bash  
ps aux | head  
\`\`\`

\#\#\# Observation  
This command showed the currently running processes along with CPU and memory usage.  
It helps quickly identify active services and running applications.

\---

\#\# Command 2  
\`\`\`bash  
systemctl status nginx  
\`\`\`

\#\#\# Observation  
The nginx service was active and running successfully.  
This command is useful for checking service health and troubleshooting startup failures.

\---

\#\# Command 3  
\`\`\`bash  
journalctl \-u nginx \--no-pager | tail \-n 20  
\`\`\`

\#\#\# Observation  
The latest nginx logs showed successful service activity with no critical errors.

\---

\# File Skills Practice

\#\# Append Text Using echo \>\>

\`\`\`bash  
echo "Linux revision practice" \>\> notes.txt  
\`\`\`

\#\#\# Result  
Successfully appended new text into the file without overwriting existing content.

\---

\#\# Change Permissions Using chmod

\`\`\`bash  
chmod 755 script.sh  
\`\`\`

\#\#\# Result  
The script became executable for the owner, group, and others.

\---

\#\# Change Ownership Using chown

\`\`\`bash  
sudo chown tokyo:developers devops-file.txt  
\`\`\`

\#\#\# Result  
The file owner and group were updated successfully.

\---

\#\# Verify File Permissions

\`\`\`bash  
ls \-l  
\`\`\`

\#\#\# Observation  
Verified ownership, permissions, and file details correctly.

\---

\# Cheat Sheet Refresh

\#\# Top 5 Commands I Would Use During an Incident

| Command | Purpose |  
|---|---|  
| \`top\` | Monitor CPU and memory usage |  
| \`ps aux\` | Check running processes |  
| \`systemctl status nginx\` | Verify service health |  
| \`journalctl \-u nginx \-f\` | Monitor service logs live |  
| \`df \-h\` | Check disk space usage |

\---

\# User & Group Sanity Check

\#\# Create User

\`\`\`bash  
sudo useradd \-m revision-user  
\`\`\`

\---

\#\# Verify User

\`\`\`bash  
id revision-user  
\`\`\`

\#\#\# Observation  
Verified the user ID, group ID, and assigned groups successfully.

\---

\#\# Ownership Verification

\`\`\`bash  
sudo chown revision-user:developers devops-file.txt  
ls \-l devops-file.txt  
\`\`\`

\#\#\# Observation  
Ownership changes were reflected correctly.

\---

\# Mini Self-Check

\#\# Which 3 commands save you the most time right now, and why?

\#\#\# 1\. top  
Helps monitor system resource usage in real time.

\#\#\# 2\. systemctl status  
Quickly checks whether services are running or failed.

\#\#\# 3\. journalctl  
Useful for troubleshooting logs and identifying service issues.

\---

\# How do you check if a service is healthy?

\#\# Commands I run first

\`\`\`bash  
systemctl status nginx  
journalctl \-u nginx \--no-pager | tail \-n 20  
ps aux | grep nginx  
\`\`\`

These commands help verify:  
\- Service status  
\- Recent logs  
\- Running processes

\---

\# How do you safely change ownership and permissions without breaking access?

\#\# Example

\`\`\`bash  
sudo chown tokyo:developers app.log  
chmod 640 app.log  
\`\`\`

\#\#\# Why?  
\- Owner gets read/write access  
\- Group gets read access  
\- Others get no access

This prevents unauthorized access while maintaining required permissions.

\---

\# Focus for the Next 3 Days

\#\# Learning Goals

\- Shell scripting basics  
\- Docker containers and images  
\- Networking troubleshooting  
\- SSH and SCP practice  
\- Git & GitHub workflows

\---

\# Final Reflection

During the first 12 days, I improved my understanding of:  
\- Linux administration  
\- Troubleshooting  
\- Services and logs  
\- Permissions and ownership  
\- User management  
\- Cloud server basics

I will continue practicing daily to strengthen my DevOps and Cloud Engineering skills.

\---

Keep Learning 🚀  
Aman 