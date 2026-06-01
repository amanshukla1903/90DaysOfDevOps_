# **Day 17 – Shell Scripting: Loops, Arguments & Error Handling**

## **Objective**

Learn how to use loops, command-line arguments, package installation automation, and basic error handling in shell scripts.

---

# **Task 1: For Loop**

## **Create for\_loop.sh**

\#\!/bin/bash

for fruit in Apple Banana Mango Orange Grapes  
do  
    echo $fruit  
done

Run:

chmod \+x for\_loop.sh  
./for\_loop.sh

### **Output**

Apple  
Banana  
Mango  
Orange  
Grapes

---

## **Create count.sh**

\#\!/bin/bash

for num in {1..10}  
do  
    echo $num  
done

Run:

chmod \+x count.sh  
./count.sh

### **Output**

1  
2  
3  
4  
5  
6  
7  
8  
9  
10

---

# **Task 2: While Loop**

## **Create countdown.sh**

\#\!/bin/bash

read \-p "Enter a number: " NUM

while \[ $NUM \-ge 0 \]  
do  
    echo $NUM  
    ((NUM--))  
done

echo "Done\!"

Run:

chmod \+x countdown.sh  
./countdown.sh

### **Example Output**

Enter a number: 5

5  
4  
3  
2  
1  
0

Done\!

---

# **Task 3: Command-Line Arguments**

## **Create greet.sh**

\#\!/bin/bash

if \[ $\# \-eq 0 \]  
then  
    echo "Usage: ./greet.sh \<name\>"  
else  
    echo "Hello, $1\!"  
fi

Run:

./greet.sh Aman

### **Output**

Hello, Aman\!

---

## **Create args\_demo.sh**

\#\!/bin/bash

echo "Script Name: $0"  
echo "Total Arguments: $\#"  
echo "All Arguments: $@"

Run:

./args\_demo.sh DevOps Linux Docker

### **Output**

Script Name: ./args\_demo.sh  
Total Arguments: 3  
All Arguments: DevOps Linux Docker

---

# **Task 4: Install Packages via Script**

## **Create install\_packages.sh**

\#\!/bin/bash

if \[ "$EUID" \-ne 0 \]  
then  
    echo "Please run as root."  
    exit 1  
fi

PACKAGES="nginx curl wget"

for pkg in $PACKAGES  
do  
    if dpkg \-s $pkg &\>/dev/null  
    then  
        echo "$pkg is already installed."  
    else  
        echo "Installing $pkg ..."  
        apt-get install \-y $pkg  
    fi  
done

Run:

sudo ./install\_packages.sh

### **Observation**

* Installed missing packages.  
* Skipped packages already installed.

---

# **Task 5: Error Handling**

## **Create safe\_script.sh**

\#\!/bin/bash

set \-e

mkdir /tmp/devops-test || echo "Directory already exists"

cd /tmp/devops-test || {  
    echo "Failed to enter directory"  
    exit 1  
}

touch test.txt || {  
    echo "Failed to create file"  
    exit 1  
}

echo "Script completed successfully."

Run:

chmod \+x safe\_script.sh  
./safe\_script.sh

### **Example Output**

Directory already exists  
Script completed successfully.

---

# **Commands Practiced**

chmod \+x  
for  
while  
read  
$1  
$\#  
$@  
set \-e  
dpkg \-s  
apt-get install

---

# **Key Learning**

### **1\.**

For loops and while loops help automate repetitive tasks.

### **2\.**

Command-line arguments make scripts reusable and flexible.

### **3\.**

Error handling using `set -e`, `||`, and exit codes makes scripts safer and more reliable.

---

# **Conclusion**

Today I learned how to automate repetitive tasks using loops, pass values using command-line arguments, install packages through scripts, and handle errors effectively. These concepts are essential for writing reliable automation scripts in DevOps environments.

Keep Learning.

Aman

