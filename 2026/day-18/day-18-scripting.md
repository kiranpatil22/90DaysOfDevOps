#!/bin/bash



greet() {

    name=$1

    echo "My name is $name"

}



add() {

    num1=$1

    num2=$2

    sum=$((num1 + num2))



    echo "Sum: $sum"

}



greet "devops"

add 5 10



# disk-check -----



#!/bin/bash



# Exit if any command fails

set -e



# ----------------------------

# Function: check_disk

# ----------------------------

check_disk() {

    echo "===== Disk Usage (/) ====="

    df -h / | tail -n 1

    echo

}



# ----------------------------

# Function: check_memory

# ----------------------------

check_memory() {

    echo "===== Memory Usage ====="

    free -h

    echo

}



# ----------------------------

# Main Section

# ----------------------------



echo "System Resource Report"

echo "-----------------------"



check_disk

check_memory



echo "Report Complete."



# strict-demo



#!/bin/bash



# Enable Strict Mode

set -euo pipefail



echo "Strict Mode Demo"

echo "------------------"



# 1️⃣ set -u demonstration (undefined variable)

echo "Testing undefined variable..."

echo "Value of MY_VAR is: $MY_VAR"



# 2️⃣ set -e demonstration (command failure)

echo "Testing failing command..."

ls /this_directory_does_not_exist



# 3️⃣ set -o pipefail demonstration

echo "Testing pipeline failure..."

grep "text" nonexistentfile.txt | wc -l



echo "This line will not execute if any error occurs."



# local / global variables 



#!/bin/bash



echo "Variable Scope Demo"

echo "--------------------"



#Global variable

var="I am global"



echo "Before function call: var = $var"

echo



# ---------------------------------

# Function using LOCAL variable

# ---------------------------------

local_function() {

    local var="I am local"

    echo "Inside local_function: var = $var"

}



# ---------------------------------

# Function using GLOBAL variable

# ---------------------------------

global_function() {

    var="I changed the global variable"

    echo "Inside global_function: var = $var"

}



# Call local function

local_function

echo "After local_function call: var = $var"

echo



# Call global function

global_function

echo "After global_function call: var = $var"



# system-info



#!/bin/bash



set -euo pipefail



# -----------------------------------

# Print Section Header

# -----------------------------------

print_header() {

    echo

    echo "========================================"

    echo "$1"

    echo "========================================"

}



# -----------------------------------

# Hostname and OS Info

# -----------------------------------

system_identity() {

    print_header "SYSTEM INFORMATION"



    echo "Hostname : $(hostname)"

    echo "OS       : $(uname -s)"

    echo "Kernel   : $(uname -r)"



   if [ -f /etc/os-release ]; then

       echo "Distro   : $(grep PRETTY_NAME /etc/os-release | cut -d= -f2 | tr -d '"')"

    fi

}



# -----------------------------------

# Uptime

# -----------------------------------

system_uptime() {

   print_header "SYSTEM UPTIME"



  uptime -p

}



# -----------------------------------

# Disk Usage (Top 5 by Size)

# -----------------------------------

disk_usage() {

  print_header "TOP 5 DISK USAGE (Largest Directories in /)"



du -h / 2>/dev/null | sort -rh | head -n 5 || true

}



# -----------------------------------

# Memory Usage

# -----------------------------------

memory_usage() {

   print_header "MEMORY USAGE"



  free -h

}



# -----------------------------------

# Top 5 CPU Processes

# -----------------------------------

top_cpu_processes() {

  print_header "TOP 5 CPU-CONSUMING PROCESSES"


   ps -eo pid,comm,%cpu --sort=-%cpu | head -n 6

}



# -----------------------------------

# Main Function

# -----------------------------------

main() {

   echo

   echo "******** SYSTEM REPORT ********"

   echo "Generated on: $(date)"

   echo



   system_identity

  system_uptime

   disk_usage

   memory_usage

   top_cpu_processes



   echo

   echo "******** END OF REPORT ********"

  echo

}



# Run main

main
