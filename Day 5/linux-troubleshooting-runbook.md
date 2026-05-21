# Day 05 – Linux Troubleshooting Drill: CPU, Memory, and Logs

## ask

Today’s goal is to run a focused troubleshooting drill.  
You will pick a running process/service on your system and:

* Capture a quick health snapshot (CPU, memory, disk, network)  
* Trace logs for that service  
* Write a mini runbook describing what you did and what you’d do next if things were worse

This turns yesterday’s practice into a repeatable troubleshooting routine.

### What’s a runbook?

A runbook is a short, repeatable checklist you follow during an incident: the exact commands you run, what you observed, and the next actions if the issue persists. Keep it concise so you can reuse it under pressure.

**Create the Runbook File** 

touch [linux-troubleshooting-runbook.md](http://linux-troubleshooting-runbook.md)

Then open it via vi and file name 

**Paste this first:**

\# Linux Troubleshooting Runbook

\#\# Target Service / Process  
NGINX Web Server

# **Environment Basics**

Now run:

uname \-a

I will see something like the following:

Linux ip-172-31-34-16 7.0.0-1004-aws \#4-Ubuntu SMP PREEMPT Mon Apr 13 13:14:24 UTC 2026 x86\_64 GNU/Linux

Copy the small output and add it in the markdown file

uname \-a  
Linux ip-172-31-34-16 7.0.0-1004-aws \#4-Ubuntu SMP PREEMPT Mon Apr 13 13:14:24 UTC 2026 x86\_64 GNU/Linux

**Now run the command.**   
cat /etc/os-release and copy and peast in md file 

PRETTY\_NAME="Ubuntu 26.04 LTS"  
NAME="Ubuntu"  
VERSION\_ID="26.04"  
VERSION="26.04 (Resolute Raccoon)"  
VERSION\_CODENAME=resolute  
ID=ubuntu  
ID\_LIKE=debian  
HOME\_URL="https://www.ubuntu.com/"  
SUPPORT\_URL="https://help.ubuntu.com/"  
BUG\_REPORT\_URL="https://bugs.launchpad.net/ubuntu/"  
PRIVACY\_POLICY\_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"  
UBUNTU\_CODENAME=resolute  
LOGO=ubuntu-logo

**CPU & Memory Checks**   
pgrep nginx  
2194  
2196  
2197

  PID %CPU %MEM COMMAND  
   2194  0.0  1.0 nginx  
   2196  0.0  0.6 nginx  
   2197  0.0  0.6 nginx

Now run:

tail \-n 20 /var/log/nginx/error. log

Add observation:

No major errors were found in the nginx error logs.

**Quick Findings**   
\#\# Quick Findings

\- NGINX service is active and running.  
\- CPU and memory usage are stable.  
\- Disk usage is healthy.  
\- Network connectivity is working.  
\- No major errors found in logs.

**If This Worsens** 

\#\# If This Worsens (Next Steps)

1\. Restart nginx service:  
\`\`\`bash  
sudo systemctl restart nginx  
\`\`\`

2\. Verify nginx configuration:  
\`\`\`bash  
nginx \-t  
\`\`\`

3\. Monitor logs continuously:  
\`\`\`bash  
journalctl \-u nginx \-f  
\`\`\`

4\. Check live resource usage:  
\`\`\`bash  
top  
\`\`\`

5\. Capture deeper diagnostics:  
\`\`\`bash  
strace \-p \<nginx-pid\>  
\`\`\`

Save the file and use for latter  
Aman