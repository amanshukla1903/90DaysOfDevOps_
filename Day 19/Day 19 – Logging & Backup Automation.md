# Day 19 – Logging & Backup Automation (Project)

## Objective

Automate server maintenance tasks by writing shell scripts for log rotation and backups, and schedule them with cron.

---

## Task 1: Log Rotation Script

Create **log\_rotate.sh** that:

* Takes a log directory as an argument (e.g., /var/log/myapp).  
* Exits with an error if the directory doesn't exist.  
* Compresses .log files older than 7 days using gzip.  
* Deletes .gz files older than 30 days.  
* Prints how many files were compressed and deleted.

bash  
Copy

\#\!/bin/bash

set \-euo pipefail

LOG\_DIR="$1"

if \[ \! \-d "$LOG\_DIR" \]; then

    echo "ERROR: Directory $LOG\_DIR not found."

    exit 1

fi

echo "Starting log rotation for: $LOG\_DIR"

*\# Compress .log files older than 7 days*

mapfile \-t OLD\_LOGS \< \<(find "$LOG\_DIR" \-type f \-name "\*.log" \-mtime \+7)

for file in "${OLD\_LOGS\[@\]}"; do

    gzip "$file"

done

echo "Compressed ${\#OLD\_LOGS\[@\]} old log files."

*\# Delete .gz files older than 30 days*

mapfile \-t OLD\_ARCHIVES \< \<(find "$LOG\_DIR" \-type f \-name "\*.gz" \-mtime \+30)

for file in "${OLD\_ARCHIVES\[@\]}"; do

    rm "$file"

done

echo "Deleted ${\#OLD\_ARCHIVES\[@\]} old archives."

echo "Log rotation completed."

Make it executable and run (example):

bash  
Copy

chmod \+x log\_rotate.sh

./log\_rotate.sh /var/log/myapp

### Output

text  
Copy

Starting log rotation for: /var/log/myapp

Compressed 2 old log files.

Deleted 1 old archives.

Log rotation completed.

### Observation

The script identified and compressed 2 .log files older than 7 days, and removed 1 old .gz file older than 30 days. This automates log housekeeping without manual intervention.

---

## Task 2: Server Backup Script

Create **backup.sh** that:

* Takes a source directory and a backup destination as arguments.  
* Exits with an error if the source directory doesn't exist.  
* Creates a timestamped .tar.gz archive (e.g., backup-2026-07-01.tar.gz).  
* Verifies the archive was created successfully.  
* Prints the archive name and size.  
* Deletes backups older than 14 days from the destination.

bash  
Copy

\#\!/bin/bash

set \-euo pipefail

SOURCE="$1"

DEST="$2"

if \[ \! \-d "$SOURCE" \]; then

    echo "ERROR: Source $SOURCE not found."

    exit 1

fi

mkdir \-p "$DEST"

FILENAME="backup-$(date \+%Y-%m-%d).tar.gz"

tar \-czf "$DEST/$FILENAME" "$SOURCE"

if \[ \-f "$DEST/$FILENAME" \]; then

    echo "Backup created: $FILENAME"

    echo "Size: $(du \-sh "$DEST/$FILENAME" | cut \-f1)"

else

    echo "ERROR: Failed to create backup."

    exit 1

fi

*\# Delete backups older than 14 days*

find "$DEST" \-type f \-name "backup-\*.tar.gz" \-mtime \+14 \-delete

echo "Old backups cleaned up."

Run the script (example):

bash  
Copy

chmod \+x backup.sh

./backup.sh /var/www/myapp /backups

### Output

text  
Copy

Backup created: backup-2026-07-01.tar.gz

Size: 120M

Old backups cleaned up.

### Observation

This script created a daily backup named with today’s date, displayed its size, and then removed any backup archives older than 14 days. Using tar with \-czf and a date-based filename makes it easy to manage and identify backups.

---

## Task 3: Crontab

Use cron to schedule these scripts. First, check current cron jobs:

bash  
Copy

crontab \-l

(Cron syntax uses five fields: minute, hour, day of month, month, day of week.)

sql  
Copy

\* \* \* \* \* command

┬ ┬ ┬ ┬ ┬

│ │ │ │ │

│ │ │ │ └ Day of week (0-7, where 0 or 7 \= Sunday)

│ │ │ └── Month (1-12)

│ │ └──── Day of month (1-31)

│ └────── Hour (0-23)

└──────── Minute (0-59)

Add cron entries (example paths) to run tasks automatically:

* **Daily log rotation at 2:00 AM:**  
* swift  
* Copy

0 2 \* \* \* /home/user/log\_rotate.sh /var/log/myapp

*   
* **Weekly backup on Sunday at 3:00 AM:**  
* swift  
* Copy

0 3 \* \* 0 /home/user/backup.sh /var/www/myapp /backups

*   
* **Health check every 5 minutes:**  
* ruby  
* Copy

\*/5 \* \* \* \* /home/user/health\_check.sh

* 

### Observation

These cron entries automate the maintenance tasks:

* Log rotation runs daily at 2 AM.  
* Backup runs every Sunday at 3 AM.  
* (A health-check script is scheduled to run every 5 minutes for monitoring.)

---

## Task 4: Scheduled Maintenance Script

Create **maintenance.sh** to run both scripts and log the process. It will:

* Call the log rotation and backup scripts.  
* Log all output with timestamps to /var/log/maintenance.log.

bash  
Copy

\#\!/bin/bash

set \-euo pipefail

LOG\_FILE="/var/log/maintenance.log"

log() {

    echo "\[$(date '+%Y-%m-%d %H:%M:%S')\] $1" | tee \-a "$LOG\_FILE"

}

log "===== Maintenance Started \====="

log "Running log rotation..."

bash /home/user/log\_rotate.sh /var/log/myapp \>\> "$LOG\_FILE" 2\>&1

log "Log rotation done."

log "Running backup..."

bash /home/user/backup.sh /var/www/myapp /backups \>\> "$LOG\_FILE" 2\>&1

log "Backup done."

log "===== Maintenance Finished \====="

Run the maintenance script (example):

bash  
Copy

chmod \+x maintenance.sh

./maintenance.sh

### Output

text  
Copy

\[2026-07-01 01:00:00\] \===== Maintenance Started \=====

\[2026-07-01 01:00:00\] Running log rotation...

\[2026-07-01 01:00:03\] Log rotation done.

\[2026-07-01 01:00:03\] Running backup...

\[2026-07-01 01:00:10\] Backup done.

\[2026-07-01 01:00:10\] \===== Maintenance Finished \=====

#### Cron Entry for maintenance.sh

To schedule the maintenance script at 1:00 AM daily:

bash  
Copy

0 1 \* \* \* /home/user/maintenance.sh

### Observation

The maintenance.sh script logs each action with a timestamp (using the log() function and tee). It ran the log rotation and backup scripts in sequence. All output (including errors) goes into /var/log/maintenance.log, making it easy to audit what happened at each step.

---

# Commands Practiced

* find (with \-mtime to locate old files)  
* gzip, tar (for compression and archiving)  
* du (to check file size)  
* rm (to delete files)  
* date (to generate timestamps in filenames)  
* crontab (to schedule tasks)  
* echo, tee (for logging output)

---

# What I Learned

* Using find with age filters (\-mtime) and gzip allows automating log file rotation and cleanup.  
* Creating backups with tar \-czf and including a date in the filename ensures clear, versioned archives and simplifies retention policy.  
* Scheduling scripts via cron (and logging their output with tee) automates maintenance reliably, and timestamped logs help debug issues later.

Aman :::

