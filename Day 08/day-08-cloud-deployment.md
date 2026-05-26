# Day 08—Cloud Server Setup: Docker, Nginx & Web Deployment

# 

## Task

Today's goal is to deploy a real web server on the cloud and learn practical server management.  
You will:

* Launch a cloud instance (AWS EC2 or Utho)  
* Connect via SSH  
* Install Nginx  
* Configure security groups for web access (port 80 by default for nginx)  
* Extract and save logs to a file  
* Verify your webpage is accessible from the internet

This is real DevOps work—exactly what you'll do in production.

* Create AWS account and connect via SSH mobactream 

### **Install Docker & Nginx (20 minutes)**

Step 1: Update System  
Command : sudo apt-get update, then sudo apt-get upgrade.

**Why upgrade? It means whenever you update the server, you have to install new conf so use upgrade**  
	  
**Step 3: Install Nginx**

Sudo apt-get install niginx

**Verify Nginx is running:**  
systemctl status nginx

**To install Docker, you can refer to the link: [https://docs.docker.com/engine/install/ubuntu/](https://docs.docker.com/engine/install/ubuntu/)**

### Security Group Configuration (10 minutes)

* For that, you have to check if Nginx is running or not in the browser using your public IP of the instance; if not, change the inbound rule for HTTP IPv4 and port 80, and then it will run.