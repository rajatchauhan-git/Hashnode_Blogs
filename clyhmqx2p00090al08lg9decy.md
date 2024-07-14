---
title: "Log Analyzer and Report Generator"
datePublished: Thu Jul 11 2024 18:56:17 GMT+0000 (Coordinated Universal Time)
cuid: clyhmqx2p00090al08lg9decy
slug: log-analyzer-and-report-generator
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1720724090649/78b09abb-9159-4805-930c-81e6e865946f.png
tags: devops, shell-scripting, 90daysofdevops, trainwithshubham, shellscripting-devops, loganalysis

---

Write a Bash script that automates the process of analyzing log files and generating a daily summary report. The script should perform the following steps:

1. **Input:** The script should take the path to the log file as a command-line argument.
    
2. **Error Count:** Analyze the log file and count the number of error messages. An error message can be identified by a specific keyword (e.g., "ERROR" or "Failed"). Print the total error count.
    
3. **Critical Events:** Search for lines containing the keyword "CRITICAL" and print those lines along with the line number.
    
4. **Top Error Messages:** Identify the top 5 most common error messages and display them along with their occurrence count.
    
5. **Summary Report:** Generate a summary report in a separate text file. The report should include:
    
    * Date of analysis
        
    * Log file name
        
    * Total lines processed
        
    * Total error count
        
    * Top 5 error messages with their occurrence count
        
    * List of critical events with line numbers
        

```bash
#!/bin/bash

# Function to display usage information
usage() {
        echo "Usage: $0 /home/ubuntu/logs/days.log"
        exit 1
}

if [ $# -ne 1 ]; then
        usage
fi

log_file=$1

# Check if the log file is a valid regular file
if [ ! -f "$log_file" ]; then
        echo "Error: log file $log_file does not exist."
        exit 1
fi

# Variables defined
error_keyword="ERROR"
critical_keyword="CRITICAL"
date=$(date +"%Y-%m-%d")
summary_report="summary_report_$date.txt"
archive_dir="processed_logs"
total_lines=$(wc -l < "$log_file")

# Create summary report
{
        echo "Date of analysis: $date"
        echo "Log file name: $log_file"
        echo "Total lines in the log file: $total_lines"
} > "$summary_report"

# Total error count
error_count=$(grep -c "$error_keyword" "$log_file")
echo "Total error count: $error_count" >> "$summary_report"

# Get the list of critical events with line number
critical_events=$(grep -n "$critical_keyword" "$log_file")
echo "List of critical events with line number:" >> "$summary_report"
echo "$critical_events" >> "$summary_report"

# Extract error messages, count occurrences, sort by frequency, and display the top 5
top_five=$(grep -i "$error_keyword" "$log_file" | awk '{print $1,$2,$3,$4,$5}' | sort | uniq -c | sort -nr | head -n 5)
echo "Top 5 error messages with their occurrence count:" >> "$summary_report"
echo "$top_five" >> "$summary_report"

#grep -i Searches for lines containing the word error (case insensitive) in the log file.
#sort: Sorts the lines to prepare them for counting unique occurrences
#uniq -c: Counts the unique occurrences of each line
#sort -nr: Sorts the counted occurrences in numeric order (descending).
#head -n 5: Displays the top 5 lines
```

## Output:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720723844855/c4fb6208-a43b-442f-b465-96aec1afc145.png align="center")