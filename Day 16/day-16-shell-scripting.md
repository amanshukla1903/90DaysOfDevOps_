# **Day 16 – Shell Scripting Basics**

## **Objective**

Learn the fundamentals of shell scripting, including shebang, variables, user input, and conditional statements.

---

# **Task 1: Your First Script**

## **Create hello.sh**

\#\!/bin/bash

echo "Hello, DevOps\!"

Make it executable:

chmod \+x hello.sh

Run the script:

./hello.sh

### **Output**

Hello, DevOps\!

### **What happens if the shebang is removed?**

The script may still run if executed with:

bash hello.sh

However, without the shebang (`#!/bin/bash`), the operating system does not know which interpreter should execute the script when using `./hello.sh`.

---

# **Task 2: Variables**

## **Create variables.sh**

\#\!/bin/bash

NAME="Aman"  
ROLE="DevOps Engineer"

echo "Hello, I am $NAME and I am a $ROLE"

Run:

chmod \+x variables.sh  
./variables.sh

### **Output**

Hello, I am Aman and I am a DevOps Engineer

---

## **Single Quotes vs Double Quotes**

### **Double Quotes**

echo "My name is $NAME"

Output:

My name is Aman

### **Single Quotes**

echo 'My name is $NAME'

Output:

My name is $NAME

### **Observation**

* Double quotes expand variables.  
* Single quotes treat everything as plain text.

---

# **Task 3: User Input with read**

## **Create greet.sh**

\#\!/bin/bash

read \-p "Enter your name: " NAME  
read \-p "Enter your favourite tool: " TOOL

echo "Hello $NAME, your favourite tool is $TOOL"

Run:

chmod \+x greet.sh  
./greet.sh

### **Example Output**

Enter your name: Aman  
Enter your favourite tool: Docker

Hello Aman, your favourite tool is Docker

---

# **Task 4: If-Else Conditions**

## **Create check\_number.sh**

\#\!/bin/bash

read \-p "Enter a number: " NUM

if \[ "$NUM" \-gt 0 \]; then  
    echo "Positive Number"  
elif \[ "$NUM" \-lt 0 \]; then  
    echo "Negative Number"  
else  
    echo "Zero"  
fi

### **Example Output**

Enter a number: 10  
Positive Number

---

## **Create file\_check.sh**

\#\!/bin/bash

read \-p "Enter filename: " FILE

if \[ \-f "$FILE" \]; then  
    echo "File exists."  
else  
    echo "File does not exist."  
fi

### **Example Output**

Enter filename: notes.txt  
File exists.

---

# **Task 5: Combine It All**

## **Create server\_check.sh**

\#\!/bin/bash

SERVICE="nginx"

read \-p "Do you want to check the status? (y/n): " CHOICE

if \[ "$CHOICE" \= "y" \]; then

    if systemctl is-active \--quiet $SERVICE; then  
        echo "$SERVICE service is active."  
    else  
        echo "$SERVICE service is not active."  
    fi

elif \[ "$CHOICE" \= "n" \]; then  
    echo "Skipped."  
else  
    echo "Invalid option."  
fi

Run:

chmod \+x server\_check.sh  
./server\_check.sh

### **Example Output**

Do you want to check the status? (y/n): y

nginx service is active.

---

# **Commands Practiced**

chmod \+x  
./script.sh  
echo  
read  
if  
elif  
else  
fi  
systemctl is-active

---

# **Key Learning**

### **1\.**

The shebang (`#!/bin/bash`) tells Linux which interpreter should run the script.

### **2\.**

Variables make scripts reusable and easier to manage.

### **3\.**

Conditional statements (`if-else`) allow scripts to make decisions based on user input or system status.

---

# **Conclusion**

Today I learned the basics of shell scripting, including creating executable scripts, working with variables, taking user input, and using conditional statements. These concepts are the foundation for automation and scripting in DevOps.

Keep Learning.

Aman

