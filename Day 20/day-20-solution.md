# Day 20 – Log Analyzer and Summary Report

## Task 1: Input and Validation

We begin the script with **input validation**. The script checks if a log file path was provided and whether the file exists. If the input is missing or the file is not found, it prints a clear error message and exits.

bash  
Copy  
\#\!/bin/bash  
set \-euo pipefail

*\# Check for argument*  
if \[ $\# \-ne 1 \]; then  
    echo "Usage: $0 \<path\_to\_logfile\>"  
    exit 1  
fi

logfile="$1"  
if \[ \! \-f "$logfile" \]; then  
    echo "Error: Log file '$logfile' does not exist."  
    exit 1  
fi

* The shebang (\#\!/bin/bash) and set \-euo pipefail ensure the script runs under Bash and exits on errors or undefined variables.  
* We use \-f to test for file existence. If not found, we exit with a message.

## Task 2: Error Count

Next, we count error messages. We search the log for lines containing ERROR or Failed (case-sensitive per requirements) and count them. We also get the total line count for the log.

bash  
Copy  
*\# Count total lines and errors*  
total\_lines=$(wc \-l \< "$logfile")  
error\_count=$(grep \-E \-c "ERROR|Failed" "$logfile")

* wc \-l gives the total number of lines in the file.  
* grep \-E \-c "ERROR|Failed" uses grep with extended regex (\-E) and count (\-c) to find lines matching either keyword. The \-c option directly returns the number of matching lines.

## Task 3: Critical Events

We extract **critical events** by looking for lines containing "CRITICAL". Using grep \-n prints each matching line with its line number.

bash  
Copy  
*\# Find critical events with line numbers*  
critical\_events=$(grep \-n "CRITICAL" "$logfile" || true)

* grep \-n "CRITICAL" prints lines with "CRITICAL" prefixed by their line number.  
* We use || true to avoid error status if no matches are found; we handle the empty case later.

## Task 4: Top Error Messages

To identify the top 5 error messages, we extract all lines with errors, isolate the message text, and count unique occurrences. We use awk, sort, uniq \-c, and sort \-nr in a pipeline.

bash  
Copy  
*\# Extract and count top 5 error messages*  
top\_errors=$(grep \-E "ERROR|Failed" "$logfile" \\  
    | awk '{for(i=3;i\<=NF;i++) printf $i " "; print ""}' \\  
    | sort | uniq \-c | sort \-nr | head \-5)

* grep \-E "ERROR|Failed" "$logfile" filters all error lines.  
* The awk command '{for(i=3;i\<=NF;i++) printf $i " "; print ""}' skips the first two fields (often date/time) and prints the rest, which is the error message.  
* We pipe to sort | uniq \-c | sort \-nr | head \-5 to count and sort the messages in descending order. This pattern is a common way to find the most frequent lines.

## Task 5: Generate Summary Report

We compile the results into a report file named log\_report\_\<date\>.txt. The report includes the date of analysis, log file name, total lines processed, total error count, top error messages, and critical events with line numbers.

bash  
Copy  
report\_file="log\_report\_$(date \+%Y-%m-%d).txt"

{  
    echo "Date of analysis: $(date)"  
    echo "Log file: $logfile"  
    echo "Total lines processed: $total\_lines"  
    echo "Total error count: $error\_count"  
    echo  
    echo "Top 5 error messages (most frequent first):"  
    echo "$top\_errors"  
    echo  
    echo "--- Critical Events (Line: Event) \---"  
    if \[ \-z "$critical\_events" \]; then  
        echo "None"  
    else  
        echo "$critical\_events" | while IFS= read \-r line; do  
            num="${line%%:\*}"  
            rest="${line\#\*:}"  
            echo "Line $num: $rest"  
        done  
    fi  
} \> "$report\_file"

echo "Summary report saved to $report\_file"

* We use $(date \+%Y-%m-%d) to include the date in the report filename.  
* Inside the report: the date of analysis, log file name, and counts are printed first.  
* We then list the top 5 errors (from $top\_errors).  
* For critical events, if none are found we print "None"; otherwise we reformat each grep \-n line as Line N: ....  
* Finally we notify that the report is saved.

**Sample output** (contents of log\_report\_\<date\>.txt) might look like:

yaml  
Copy  
Date of analysis: Wed Jul  1 02:30:00 UTC 2026  
Log file: sample\_log.log  
Total lines processed: 9  
Total error count: 5

Top 5 error messages (most frequent first):  
3 ERROR: Failed to connect to database  
1 ERROR: Timeout occurred  
1 ERROR: Failed to start service

\--- Critical Events (Line: Event) \---  
Line 3: 2026-07-01 08:10:00 CRITICAL: Disk space low  
Line 7: 2026-07-01 08:30:00 CRITICAL: Network down

This shows all required details: counts and listings as specified.

## Task 6 (Optional): Archive Processed Logs

After generating the report, we move the processed log file into an archive/ directory to keep things organized:

bash  
Copy  
*\# Move log to archive*  
archive\_dir="archive"  
mkdir \-p "$archive\_dir"  
mv "$logfile" "$archive\_dir/"  
echo "Log file moved to $archive\_dir/"

* mkdir \-p creates the archive directory if it doesn’t exist.  
* Then we move the log file into it. This archives the log after processing.

## Full Script: log\_analyzer.sh

Below is the complete script incorporating all tasks:

bash  
Copy  
\#\!/bin/bash  
set \-euo pipefail

*\# Input validation*  
if \[ $\# \-ne 1 \]; then  
    echo "Usage: $0 \<path\_to\_logfile\>"  
    exit 1  
fi

logfile="$1"  
if \[ \! \-f "$logfile" \]; then  
    echo "Error: Log file '$logfile' does not exist."  
    exit 1  
fi

*\# Count total lines and errors*  
total\_lines=$(wc \-l \< "$logfile")  
error\_count=$(grep \-E \-c "ERROR|Failed" "$logfile")

*\# Find critical events with line numbers*  
critical\_events=$(grep \-n "CRITICAL" "$logfile" || true)

*\# Extract and count top 5 error messages*  
top\_errors=$(grep \-E "ERROR|Failed" "$logfile" \\  
    | awk '{for(i=3;i\<=NF;i++) printf $i " "; print ""}' \\  
    | sort | uniq \-c | sort \-nr | head \-5)

*\# Generate summary report*  
report\_file="log\_report\_$(date \+%Y-%m-%d).txt"  
{  
    echo "Date of analysis: $(date)"  
    echo "Log file: $logfile"  
    echo "Total lines processed: $total\_lines"  
    echo "Total error count: $error\_count"  
    echo  
    echo "Top 5 error messages (most frequent first):"  
    echo "$top\_errors"  
    echo  
    echo "--- Critical Events (Line: Event) \---"  
    if \[ \-z "$critical\_events" \]; then  
        echo "None"  
    else  
        echo "$critical\_events" | while IFS= read \-r line; do  
            num="${line%%:\*}"  
            rest="${line\#\*:}"  
            echo "Line $num: $rest"  
        done  
    fi  
} \> "$report\_file"  
echo "Summary report saved to $report\_file"

*\# Archive processed log file*  
archive\_dir="archive"  
mkdir \-p "$archive\_dir"  
mv "$logfile" "$archive\_dir/"  
echo "Log file moved to $archive\_dir/"

### Commands/Tools Used

* **grep**: to search for "ERROR", "Failed", and "CRITICAL" in the log. Using grep \-c to count matches and grep \-n to include line numbers.  
* **wc \-l**: to count total lines in the log.  
* **awk**: to extract and concatenate fields of error messages (skipping timestamp fields).  
* **sort | uniq \-c | sort \-nr**: to count and sort unique error messages by frequency.  
* **date**: to get the current date for filenames and report header.  
* **mkdir**, **mv**: to create the archive directory and move files (as shown in the example script).

## What I Learned

1. **Automating Log Insights:** Using shell tools like grep, awk, and uniq makes it easy to scan logs and extract key information without reading line-by-line.  
2. **Efficient Summarization:** Pipelines (sort | uniq \-c | sort \-nr) provide a concise way to count and sort occurrences, useful for “top N” summaries.  
3. **Robust Scripting:** Incorporating set \-euo pipefail ensures errors are caught early, and validating inputs prevents silent failures.

This script effectively automates daily log analysis tasks, providing a quick summary report of errors and critical events.

Keep Learning.

Aman :::  
