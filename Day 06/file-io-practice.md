# Day 06 – Linux Fundamentals: Read and Write Text Files

## Task

This is a continuation of Day 05, but much simpler.  
Today’s goal is to practice basic file read/write using only fundamental commands.  
You will create a small text file and practice:

* Creating a file  
* Writing text to a file  
* Appending new lines  
* Reading the file back

Keep it basic and repeatable.

Follow these rules while creating your practice note:

* Create a file named notes.txt

**touch notes.txt** 

* Wrote something using vi; also, you can write in when you create a file using \> or \>\>

* Use \`cat\` to read the full file  
  Output: Linux is based on the UNIX operating system. UNIX is a powerful, multi-user, multitasking operating system originally developed in the 1970s at AT\&T Bell Labs. It laid the foundation for many modern operating systems, including Linux.  
* Linux is free and open-source, accessible to everyone.  
* This promotes global collaboration and innovation.  
* Linux offers efficient performance and strong security.  
* It works well across many devices and industries.

* **Use head and tail to read parts of the file**

		

	**Commands: ** head \-n 2 notes.txt

* **tail \-n 2 notes.txt**

	

**Commands: ** tail \-n 2 notes.txt

* **Use tee once to write and display at the same time**

	You can write in the same time but if anything in the file will be overridden.

 

	

