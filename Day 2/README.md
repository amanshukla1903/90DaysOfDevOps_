# Day 02 – Linux Architecture, Processes, and systemd

## Task

Today’s goal is to understand how Linux works under the hood.  
You will create a short note that explains:

* The core components of Linux (kernel, user space, init/systemd)  
* How processes are created and managed  
* What systemd does and why it matters

This is the foundation for all troubleshooting you will do as a DevOps engineer.

## Expected Output

* The core components of Linux (kernel, user space, init/systemd)

Linux mainly has three important parts: kernel, user space, and systemd/init.

The kernel is the heart of Linux. It connects the software with the hardware and manages things like memory, CPU, devices, files, and processes.

User Space is the area where users work. All applications, commands, and tools like the terminal, browser, and shell run in user space.

Init or systemd is the first process that starts after the Linux system boots. It manages system services, starts background processes, and controls startup and shutdown operations. Nowadays, most Linux systems use systemd because it is faster and more efficient.

* How processes are created and managed.  
    
  In Linux, a process is created whenever a program or command is executed. The system creates a new process using the kernel, gives it a unique Process ID (PID), and allocates memory and CPU resources for it.   
  Linux manages processes by scheduling CPU time, controlling memory usage, and tracking process states like running, sleeping, or stopped. Users and administrators can monitor and manage processes using commands like `"ps," "top," "htop," and "kill."`  
  


* What systemd does and why it matters 

	  
`systemd` is the service manager in Linux that starts and manages system services and background processes during boot. It also handles restarting failed services and controls system startup and shutdown.

It is important because it makes Linux systems faster, more organized, and easier to manage.

⇒ Everything in a Linux file or directory.

⇒ Everything in a Linux is a process.

**Commands that I practice today** 

	

	\`cd\`—for changing directory

	pwd \- present working directory

	ls—list directory and files

	/ \- root directory

	cat \- view what is in inside in a file 

	vi—create a file and open immediately 

echo \- print the file 

top \- for see how much resources taking.

systemctl \- is basically for run and checking if any services are running

**A process in Linux goes through different states depending on what it is doing.**

* **Running** → The process is currently using the CPU or ready to run.  
* **Sleeping** → The process is waiting for something, like user input or a file response.  
* **Stopped** → The process has been paused or stopped manually.  
* **Zombie** → The process has finished its work, but its entry still exists until the parent process removes it.  
* **Dead/Terminated** → The process has completely ended and is removed from memory.

