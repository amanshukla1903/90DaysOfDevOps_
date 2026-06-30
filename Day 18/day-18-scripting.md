# **Day 18 – Shell Scripting: Functions, Strict Mode & Reusable Scripts**

## **Objective**

Learn how to write cleaner, reusable, and safer shell scripts using functions, strict mode, local variables, and modular scripting.

---

# **Task 1: Basic Functions**

## **Create functions.sh**

\#\!/bin/bash

greet() {  
    echo "Hello, $1\!"  
}

add() {  
    SUM=$(($1 \+ $2))  
    echo "Sum \= $SUM"  
}

greet "Aman"  
add 10 20

Run:

chmod \+x functions.sh  
./functions.sh

### **Output**

Hello, Aman\!  
Sum \= 30

### **Observation**

Functions make scripts reusable and reduce duplicate code.

---

# **Task 2: Functions with Return Values**

## **Create disk\_check.sh**

\#\!/bin/bash

check\_disk() {  
    echo "Disk Usage:"  
    df \-h /  
}

check\_memory() {  
    echo "Memory Usage:"  
    free \-h  
}

check\_disk  
echo  
check\_memory

Run:

chmod \+x disk\_check.sh  
./disk\_check.sh

### **Observation**

The script displayed disk usage and memory usage in separate sections, making the output easier to read.

---

# **Task 3: Strict Mode — set \-euo pipefail**

## **Create strict\_demo.sh**

\#\!/bin/bash

set \-euo pipefail

echo $NAME

Run:

chmod \+x strict\_demo.sh  
./strict\_demo.sh

### **Observation**

The script immediately stopped because the variable `NAME` was not defined.

---

### **What does each flag do?**

#### **set \-e**

Stops the script immediately if any command returns an error.

#### **set \-u**

Treats undefined variables as errors and exits the script.

#### **set \-o pipefail**

Returns an error if any command in a pipeline fails instead of only checking the last command.

---

# **Task 4: Local Variables**

## **Create local\_demo.sh**

\#\!/bin/bash

demo\_local() {  
    local NAME="Aman"  
    echo "Inside Function: $NAME"  
}

demo\_global() {  
    ROLE="DevOps Engineer"  
}

demo\_local  
echo "Outside Function: $NAME"

demo\_global  
echo "Global Variable: $ROLE"

Run:

chmod \+x local\_demo.sh  
./local\_demo.sh

### **Observation**

* Local variables were available only inside the function.  
* Global variables remained accessible outside the function.

---

# **Task 5: System Info Reporter**

## **Create system\_info.sh**

\#\!/bin/bash

set \-euo pipefail

system\_info() {  
    echo "===== System Information \====="  
    hostname  
    uname \-a  
}

uptime\_info() {  
    echo  
    echo "===== Uptime \====="  
    uptime  
}

disk\_usage() {  
    echo  
    echo "===== Disk Usage \====="  
    du \-sh /\* 2\>/dev/null | sort \-hr | head \-5  
}

memory\_usage() {  
    echo  
    echo "===== Memory Usage \====="  
    free \-h  
}

cpu\_process() {  
    echo  
    echo "===== Top 5 CPU Processes \====="  
    ps aux \--sort=-%cpu | head \-6  
}

main() {  
    system\_info  
    uptime\_info  
    disk\_usage  
    memory\_usage  
    cpu\_process  
}

main

Run:

chmod \+x system\_info.sh  
./system\_info.sh

### **Observation**

The script generated a clean system report containing hostname, operating system details, uptime, disk usage, memory usage, and the top CPU-consuming processes.

---

# **Commands Practiced**

chmod \+x  
set \-euo pipefail  
df \-h  
free \-h  
du \-sh  
hostname  
uname \-a  
uptime  
ps aux

---

# **Key Learning**

### **1\.**

Functions make shell scripts modular, reusable, and easier to maintain.

### **2\.**

Using `set -euo pipefail` helps create safer scripts by detecting errors early.

### **3\.**

Local variables prevent accidental modification of values outside a function and improve script readability.

---

# **Conclusion**

Today I learned how to organize shell scripts using functions, use strict mode for better error handling, work with local variables, and build a reusable system information reporting script. These practices improve the reliability and maintainability of automation scripts used in DevOps.

Keep Learning.

Aman

