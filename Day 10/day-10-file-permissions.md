# Day 10 – File Permissions & File Operations Challenge

## Task

Master file permissions and basic file operations in Linux.

* Create and read files using touch, cat, vim  
* Understand and modify permissions using chmod

### **ask 1: Create Files** 

1. **Create empty file devops.txt using touch**

	touch devops.txt

2. **Create notes.txt with some content using cat or echo**

	echo "This is my Linux practice note." \> notes.txt   
	cat \> notes.txt

Then type:

This is my Linux practice note.  
Learning Linux commands.

3. **Create script.sh using vim with content: echo "Hello, DevOps."**

	vim [script.sh](http://script.sh)   
		\#\!/bin/bash  
echo  "Hello, DevOps."

Run:

./script.sh

### **Task 2: Read Files**

1. **Read notes.txt using cat**

	cat notes.txt

2. **View script.sh in vim read-only mode**

   vim \-R script.sh

3. **Display first 5 lines of /etc/passwd using head**

		head \-n 5 /etc/passwd

	

4. **Display last 5 lines of /etc/passwd using tail**

		tail \-n 5 /etc/passwd

### **Task 3: Understand Permissions**

	**Check File Permissions**

Use:

ls \-l notes.txt

Example output:

\-rw-r--r-- 1 ubuntu ubuntu 25 Aug 20 10:30 notes.txt

Understanding:

* `-` → regular file  
* `rw-` → owner permissions  
* `r--` → group permissions  
* `r--` → others permissions

---

# **Check Directory Permissions**

Use:

ls \-ld /opt/dev-project

Example:

drwxrwxr-x 2 root developers 4096 Aug 20 10:35 /opt/dev-project

Understanding:

* `d` → directory  
* `rwx` → owner can read/write/execute  
* `rwx` → group can read/write/execute  
* `r-x` → others can read/execute only

---

# **Change Permissions**

Give execute permission:

chmod \+x script.sh

Verify:

ls \-l script.sh

Expected:

\-rwxr-xr-x  
---

# **Remove Write Permission**

Use:

chmod \-w notes.txt

Check:

ls \-l notes.txt

Observation:  
 Write permission removed from file.

---

# **Numeric Permissions**

Example:

chmod 755 script.sh

Meaning:

* 7 → rwx  
* 5 → r-x  
* 5 → r-x

---

# **Permission Reference**

| Number | Permission |
| ----- | ----- |
| 7 | rwx |
| 6 | rw- |
| 5 | r-x |
| 4 | r-- |

---

# **Useful Practice Commands**

chmod 644 notes.txt  
chmod 755 script.sh  
chmod 775 /opt/dev-project

### **Task 4: Modify Permissions**

1. Make script.sh executable → run it with ./[script.sh](http://script.sh)

	chmod 764 

2. **Set devops.txt to read-only (remove write for all)**

	Set devops.txt to read-only (remove write for all)  
Use:  
chmod a-w devops.txt  
**Verify:**  
L	s \-l devops.txt  
**Expected permission example**:  
\-r--r--r--  
---

---

# Create project/ directory with permission 755

Create directory:  
mkdir project  
Set permissions:  
chmod 755 project  
Verify:  
ls \-ld project  
Expected:  
drwxr-xr-x  
Meaning:

3. Owner → rwx  
4. Group → r-x  
5. Others → r-x

6.   
7.   
8. 

**3\. Set notes.txt to 640 (owner: rw, group: r, others: none)**  
Use:  
chmod 640 notes.txt  
**Verify:**  
ls \-l notes.txt  
**Expected:**  
\-rw-r-----  
Meaning:

* Owner → read/write  
* Group → read only  
* Others → no permission

		

9. Create directory project/ with permissions 755

		Create a project/directory with permission 755  
Create directory:  mkdir project  
Set permissions:   chmod 755 project  
Verify:                    ls \-ld project  
Expected:              drwxr-xr-x  
Meaning:

10. Owner → rwx  
11. Group → r-x  
12. Others → r-x