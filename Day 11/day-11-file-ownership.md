# Day 11 – File Ownership Challenge (chown & chgrp)

## Task

Master file and directory ownership in Linux.

* Understand file ownership (user and group)  
* Change file owner using chown  
* Change file group using chgrp  
* Apply ownership changes recursively


### **Understanding Ownership**

When you run:

ls \-l

You will see output like the following:

\-rw-r--r-- 1 aman developers 245 May 22 10:30 notes.txt

Breakdown:

\-rw-r--r--  → Permissions  
1            → Link count  
aman         → Owner  
developers   → Group  
245          → File size  
May 22 10:30 → Date & time  
notes.txt    → File name

## **Difference Between Owner and Group**

### **Owner**

* The **owner** is the user who created the file or has ownership of it.  
* Usually, the creator of the file becomes the owner automatically.  
* The owner can control permissions and modify the file.

Example:

aman

Here, `aman` is the owner.

---

### **Group**

* A **group** is a collection of users.  
* Multiple users can belong to the same group.  
* Group permissions allow several users to access the same file based on assigned permissions.

Example:

developers

Here, `developers` is the group assigned to the file.

### **Task 2: Basic chown Operations**

1. **Create file devops-file.txt**

		**touch devops-file.txt** 

2. **Check current owner: ls \-l devops-file.txt**

	**ls \-l** 	  
	

3. **Change owner to tokyo (create user if needed)**

	**sudo chown tokyo devops-file.txt**

4. **Change owner to berlin**

	**sudo chown berlin devops-file.txt**

5. **Verify the changes**  
    ls \-l  
     
     
     
     
   

### **Task 3: Basic chgrp Operations**

### **Create file team-notes.txt**

	touch team-notes.txt

1. **Check current group: ls \-l team-notes.txt**

		user \-ubuntu group \-ubuntu

2. **Create group: sudo groupadd heist-team**

	Done  
	

3. **Change file group to heist-team**

		sudo chown ubuntu:heist-team team-notes.txt

4. **Verify the change**  
   **ls \-l**   
     
   \-rw-rw-r-- 1 ubuntu heist-team    0 May 27 01:10 team-notes.txt  
     
   

### **Task 4: Combined Owner & Group Change** 

### **Using \`chown\`, you can change both owner and group together:**

1. **Create file project-config.yaml**

		touch project-config.yml

2. **Change owner to professor AND group to heist-team (one command)**

		sudo chown profesor:heist-team project-config.yml 	  
	

3. **Create directory app-logs/**

		mkdir app-logs  
	

4. **Change its owner to berlin and group to heist-team**  
   	sudo chown berlin:heist-team app-logs/

### **Task 5: Recursive Ownership (20 minutes)**

1. **Create directory structure:**

**mkdir \-p heist-project/vault**  
**mkdir \-p heist-project/plans**  
**touch heist-project/vault/gold.txt**  
**touch heist-project/plans/strategy.conf**

2. **Create group planners: sudo groupadd planners**  
3. **Change ownership of the entire heist project/directory:**  
   * **Owner: professor**  
   * **Group: planners**  
   * **Use recursive flag (-R)**  
4. **Verify all files and subdirectories changed: ls \-lR heist-project/**  
     
     
 


## **Step 1: Create Directory Structure**

mkdir \-p heist-project/vault  
mkdir \-p heist-project/plans

Create files:

touch heist-project/vault/gold.txt  
touch heist-project/plans/strategy.conf  
---

## **Step 2: Create Group**

sudo groupadd planners

Verify group:

cat /etc/group | grep planners  
---

## **Step 3: Change Ownership Recursively**

sudo chown \-R professor:planners heist-project/

Explanation:

* `professor` → owner  
* `planners` → group  
* `-R` → recursive (all files and subdirectories)

---

## **Step 4: Verify Ownership**

ls \-lR heist-project/

Expected output example:

heist-project/:  
total 8  
drwxr-xr-x 2 professor planners 4096 May 27 06:20 plans  
drwxr-xr-x 2 professor planners 4096 May 27 06:20 vault

heist-project/plans:  
total 0  
\-rw-r--r-- 1 professor planners 0 May 27 06:20 strategy.conf

heist-project/vault:  
total 0  
\-rw-r--r-- 1 professor planners 0 May 27 06:20 gold.txt

---

### **Task 6: Practice Challenge (20 minutes)**

1. **Create users: tokyo, berlin, nairobi (if not already created)**  
   * Already created  
       
2. **Create groups: vault-team, tech-team**

		 sudo groupadd vault-team  
		 sudo groupadd tech-team

3. **Create directory: bank-heist**  
   	mkdir bank-heist  
   	  
     
4. **Create 3 files inside:**  
   touch bank-heist/access-codes.txt  
   touch bank-heist/blueprints.pdf  
   touch bank-heist/escape-plan.txt

5. **Set different ownership:**  
   * access-codes.txt → owner: tokyo, group: vault-team  
   * blueprints.pdf → owner: berlin, group: tech-team  
   * escape-plan.txt → owner: nairobi, group: vault-team

     sudo chown tokyo:vault-team access-codes.txt 

     sudo chown berlin:tech-team blueprints.pdf 

     sudo chown nairob:vault-team escape-plan.txt 

**Verify: ls \-l bank-heist/**

	\-rw-rw-r-- 1 tokyo   vault-team 0 May 27 01:35 access-codes.txt  
\-rw-rw-r-- 1 berlin  tech-team  0 May 27 01:35 blueprints.pdf  
\-rw-rw-r-- 1 nairobi vault-team 0 May 27 01:35 escape-plan.txt  
	  
