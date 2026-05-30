# **Day 14 – Networking Fundamentals & Hands-on Checks**

## **Objective**

Learn the basics of networking and practice common troubleshooting commands used in real-world Linux and DevOps environments.

---

# **Quick Concepts**

## **OSI Model vs TCP/IP Model**

### **OSI Model (7 Layers)**

1. Physical  
2. Data Link  
3. Network  
4. Transport  
5. Session  
6. Presentation  
7. Application

### **TCP/IP Model (4 Layers)**

1. Link  
2. Internet  
3. Transport  
4. Application

### **Observation**

The OSI model is mainly used for understanding networking concepts, while the TCP/IP model is the practical model used on the Internet.

---

## **Where Common Protocols Fit**

| Protocol | Layer |
| ----- | ----- |
| IP | Internet / Network |
| TCP | Transport |
| UDP | Transport |
| DNS | Application |
| HTTP | Application |
| HTTPS | Application |

### **Example**

curl https://example.com

Application Layer (HTTPS) → TCP → IP

---

# **Hands-on Checklist**

## **1\. Identity Check**

Command:

hostname \-I

OR

ip addr show

### **Observation**

Displayed the IP address assigned to the machine.

### **Why?**

Helps identify the current network identity of the server.

---

## **2\. Reachability Test**

Command:

ping google.com

### **Observation**

Received replies successfully with low latency and 0% packet loss.

### **Why?**

Confirms network connectivity and DNS resolution.

---

## **3\. Path Check**

Command:

traceroute google.com

OR

tracepath google.com

### **Observation**

Displayed the network path taken to reach the destination host.

### **Why?**

Useful for identifying routing issues and slow network hops.

---

## **4\. Listening Ports**

Command:

ss \-tulpn

### **Observation**

Found services listening on ports such as:

* SSH → Port 22  
* Nginx → Port 80

### **Why?**

Helps identify active services and open ports.

---

## **5\. DNS Resolution**

Command:

dig google.com

OR

nslookup google.com

### **Observation**

Successfully resolved the domain name to an IP address.

### **Why?**

Verifies DNS functionality.

---

## **6\. HTTP Check**

Command:

curl \-I https://google.com

### **Observation**

Received an HTTP response successfully.

Example:

HTTP/2 200

### **Why?**

Confirms the web service is reachable and responding.

---

## **7\. Connection Snapshot**

Command:

netstat \-an | head

### **Observation**

Displayed active network connections and listening ports.

Observed:

* LISTEN connections  
* ESTABLISHED connections

### **Why?**

Provides a quick overview of network activity.

---

# **Mini Task – Port Probe**

## **Identify Listening Port**

Command:

ss \-tulpn

Example:

SSH service listening on port 22\.

---

## **Test Connectivity**

Command:

nc \-zv localhost 22

### **Observation**

Connection succeeded.

Port 22 was reachable.

### **If Not Reachable**

Next checks:

systemctl status ssh

sudo ufw status

Check service status and firewall rules.

---

# **Reflection**

## **Which command gives the fastest signal when something is broken?**

ping

Reason:

Quickly tells whether the target is reachable and if packet loss exists.

---

## **What layer would you inspect if DNS fails?**

Application Layer

Commands:

dig

nslookup

---

## **What layer would you inspect if HTTP 500 appears?**

Application Layer

Check:

* Web server logs  
* Application logs  
* Backend service status

---

## **Two Follow-Up Checks During an Incident**

### **1\. Check Service Status**

systemctl status nginx

### **2\. Review Logs**

journalctl \-u nginx \-n 50 \--no-pager

---

# **Key Learning**

Today I learned how to verify connectivity, check DNS resolution, inspect open ports, trace network paths, and validate HTTP responses. These commands provide the foundation for troubleshooting network and application issues in Linux environments.

Keep Learning.

Aman

