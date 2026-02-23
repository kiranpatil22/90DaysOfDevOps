#!/bin/bash

# --- Validation (Task 1) ---

if [ $# -eq 0 ]; then

   echo "Error: No log file path provided."
   
   echo "Usage: $0 /path/to/logfile"

   exit 1

fi

LOG_FILE="$1"

if [ ! -f "$LOG_FILE" ]; then

  echo "Error: File '$LOG_FILE' does not exist."
    
   exit 1

fi


# --- Variables ---

DATE=$(date +%Y-%m-%d)

REPORT_FILE="log_report_${DATE}.txt"

TOTAL_LINES=$(wc -l < "$LOG_FILE")

ERROR_COUNT=$(grep -Ei "ERROR|Failed" "$LOG_FILE" | wc -l)


# --- Generate Report ---

{

echo "==============================="

echo "        LOG ANALYSIS REPORT"

echo "==============================="

echo "Date of analysis: $DATE"

echo "Log file name: $LOG_FILE"

echo "Total lines processed: $TOTAL_LINES"

echo "Total error count: $ERROR_COUNT"

echo ""


echo "--- Top 5 Error Messages ---"

grep -i "ERROR" "$LOG_FILE" \

| sed 's/.*ERROR[[:space:]]*//' \

| sort \

| uniq -c \

| sort -rn \

| head -5

echo ""


echo "--- Critical Events ---"

awk '/CRITICAL/ { print "Line " NR ": " $0 }' "$LOG_FILE"

echo ""

echo "========= END OF REPORT ========="

} > "$REPORT_FILE"



echo "Report generated: $REPORT_FILE"
