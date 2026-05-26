* # Day 09 – Linux User & Group Management Challenge

## Task

Today's goal is to practice user and group management by completing hands-on challenges.  
Figure out how to:

* Create users and set passwords  
* Create groups and assign users  
* Set up shared directories with group permissions

Use what you learned from Days 1-7 to find the right commands\!

### **Task 1: Create Users**

Create three users with home directories and passwords: 

* tokyo  
* berlin  
* professor  
  **Commands:**   
    
  sudo useradd \-m tokyo  
  sudo useradd \-m berlin  
  sudo useradd \-m professor  
    
* Add password : sudo passwd username


  ### Task 2: Create Groups 

Create two groups:

* developers  
* admins  
    
    
  **Commands:**   
  sudo groupadd admins  
  Sudo groupadd developers  
    
  Verify: cat /etc/group | grep developers  
  	cat /etc/group | grep admin  
  


  ### Task 3: Assign to Groups 

Assign users:

* tokyo → developers  
* berlin → developers \+ admins (both groups)  
* professor → admins  
  Commands:   
  		sudo gpasswd \-a tokyo developers  
  		sudo usermod \-aG admin,developers berlin  
  		sudo gpasswd \-a professor admins  
    
  Verify: getent group | grep admins or id username   
  


  ### Task 4: Shared Directory

1. Create directory: /opt/dev-project  
2. Set group owner to developers  
3. Set permissions to 775 (rwxrwxr-x)  
4. Test by creating files as tokyo and berlin

Verify: Check permissions and test file creation

1. Create directory: /opt/dev-project  
     
   Commands :  	cd /opt  
   sudo mkdir dev-project  
     
   2\. Set group owner to developers

sudo chown :developers /opt/dev-project

3\. Set permissions to 775 (rwxrwxr-x)

sudo chmod 775 /opt/dev-project

Verify: ls \-l: drwxrwxr-x 2 root developers 4096 May 23 21:45 dev-project  
		

4\. Test by creating files as tokyo and berlin

cd /opt/dev-project    
touch text.txt

### Task 5: Team Workspace 

1. Create user nairobi with home directory  
2. Create group project-team  
3. Add nairobi and tokyo to project-team  
4. Create /opt/team-workspace directory  
5. Set group to project-team, permissions to 775  
6. Test by creating file as nairobi

1. Create user nairobi with home directory

sudo useradd nairobi

2\. Create group project-team

sudo groupadd project-team  
cat /etc/group | grep project-teams

3\. Add nairobi and tokyo to project-team

sudo usermod \-aG project-team nairobi  
sudo usermod \-aG project-team tokyo  
For verification: Groups Nairobi and tokyo

4\. Create /opt/team-workspace directory

mkdir team-workspace 

5\. Set group to project-team, permissions to 775

sudo chmod 775 project-team/

6\. Test by creating file as nairobi

touch test.txt   
Permission denied   
