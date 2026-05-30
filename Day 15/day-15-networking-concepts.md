# **Day 15 – Networking Concepts: DNS, IP, Subnets & Ports**

## **Objective**

Understand the core networking concepts every DevOps engineer should know, including DNS, IP addressing, subnetting, CIDR notation, and common network ports.

---

# **Task 1: DNS – How Names Become IPs**

## **What happens when you type google.com in a browser?**

When a user enters google.com in a browser, the system first checks its local DNS cache. If the IP address is not found, it sends a DNS query to a DNS server. The DNS server resolves the domain name into an IP address and returns it. The browser then connects to that IP address and loads the website.

---

## **DNS Record Types**

### **A Record**

Maps a domain name to an IPv4 address.

### **AAAA Record**

Maps a domain name to an IPv6 address.

### **CNAME Record**

Creates an alias from one domain name to another.

### **MX Record**

Specifies the mail server responsible for receiving emails.

### **NS Record**

Identifies the authoritative DNS servers for a domain.

---

## **Command**

dig google.com

### **Observation**

Example A Record:

google.com.    300    IN    A    142.250.193.14

TTL Example:

300

The TTL (Time To Live) tells DNS resolvers how long they can cache the record.

---

# **Task 2: IP Addressing**

## **What is an IPv4 Address?**

An IPv4 address is a 32-bit numerical address used to identify devices on a network.

Example:

192.168.1.10

It consists of four octets separated by dots.

---

## **Public vs Private IP Address**

### **Public IP**

A globally routable IP address accessible over the Internet.

Example:

8.8.8.8

### **Private IP**

Used inside local networks and cannot be directly accessed from the Internet.

Example:

192.168.1.10

---

## **Private IP Ranges**

10.0.0.0 – 10.255.255.255

172.16.0.0 – 172.31.255.255

192.168.0.0 – 192.168.255.255

---

## **Command**

ip addr show

### **Observation**

Example:

192.168.1.20

This is a private IP address because it belongs to the 192.168.x.x range.

---

# **Task 3: CIDR & Subnetting**

## **What does /24 mean?**

In:

192.168.1.0/24

The first 24 bits represent the network portion and the remaining 8 bits are available for hosts.

---

## **Why Do We Subnet?**

Subnetting divides a large network into smaller networks.

Benefits:

* Better network organization  
* Improved security  
* Reduced broadcast traffic  
* Easier network management

---

## **CIDR Table**

| CIDR | Subnet Mask | Total IPs | Usable Hosts |
| ----- | ----- | ----- | ----- |
| /24 | 255.255.255.0 | 256 | 254 |
| /16 | 255.255.0.0 | 65,536 | 65,534 |
| /28 | 255.255.255.240 | 16 | 14 |

---

# **Task 4: Ports – The Doors to Services**

## **What is a Port?**

A port is a communication endpoint used by applications and services on a computer.

Ports allow multiple services to use the same IP address simultaneously.

---

## **Common Ports**

| Port | Service |
| ----- | ----- |
| 22 | SSH |
| 80 | HTTP |
| 443 | HTTPS |
| 53 | DNS |
| 3306 | MySQL |
| 6379 | Redis |
| 27017 | MongoDB |

---

## **Command**

ss \-tulpn

### **Observation**

Example:

tcp LISTEN 0 511 \*:80

Nginx listening on Port 80\.

tcp LISTEN 0 128 \*:22

SSH listening on Port 22\.

---

# **Task 5: Putting It Together**

## **You run curl [http://myapp.com:8080](http://myapp.com:8080/)**

What networking concepts are involved?

* DNS resolves myapp.com to an IP address.  
* TCP establishes a connection.  
* Port 8080 identifies the application service.  
* HTTP sends the request and receives the response.

---

## **Your app cannot reach a database at 10.0.1.50:3306. What would you check first?**

I would verify:

* Network connectivity using ping.  
* Database port accessibility using nc or telnet.  
* Security group/firewall rules.  
* Database service status.

---

# **What I Learned**

### **1\.**

DNS converts human-readable domain names into IP addresses so systems can communicate.

### **2\.**

Subnetting helps organize networks efficiently and reduces unnecessary traffic.

### **3\.**

Ports allow multiple services such as SSH, HTTP, and databases to operate on the same server.

---

# **Commands Practiced**

dig google.com  
ip addr show  
ss \-tulpn  
ping google.com  
curl \-I https://google.com

---

# **Conclusion**

Today I learned how DNS resolution works, how IP addressing and subnetting are structured, and how ports allow services to communicate across networks. These concepts are fundamental for troubleshooting and managing infrastructure in DevOps and Cloud environments.

Keep Learning.

Aman

