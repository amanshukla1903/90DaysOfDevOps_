# Day 04 – Linux Practice: Processes and Services

## Task

Today’s goal is to practice Linux fundamentals with real commands.  
You will create a short practice note by actually running basic commands and capturing what you see:

* Check running processes  
* Inspect one systemd service  
* Capture a small troubleshooting flow

* ps aux | head

→ shows the first few running processes currently active in the Linux system.

* Top  
  displays live system processes, CPU usage, memory usage, and overall system performance in real time. 

**Inspect the service Nginx.** 

* `systemctl status nginx` → checks whether the Nginx service is running, stopped, or failed and shows its current status details.


**`journalctl -u nginx --no-pager | tail -n 20` → shows the last 20 log entries of the Nginx service for troubleshooting and checking recent activity/errors.**

* `tail -n 20 /var/log/syslog` → displays the last 20 lines from the system log file to check recent system activity and errors.

# **Mini Troubleshooting Example**

**\#\# Mini Troubleshooting**

**Problem:**  
**The Nginx website was not loading properly.**

Steps Taken:  
1\. Checked nginx process using:  
  \`\`\`bash  
  ps aux | grep nginx  
  \`\`\`

2\. Verified nginx service status:  
  \`\`\`bash  
  systemctl status nginx  
  \`\`\`

3\. Checked nginx logs:  
  \`\`\`bash  
  journalctl \-u nginx \--no-pager | tail \-n 20  
  \`\`\`

4\. Checked access and error logs:  
  \`\`\`bash  
  tail \-n 20 /var/log/nginx/access.log  
  tail \-n 20 /var/log/nginx/error.log  
  \`\`\`

5\. Restarted nginx service:  
  \`\`\`bash  
  sudo systemctl restart nginx  
