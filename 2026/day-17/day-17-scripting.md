BASH SCRIPTING NOTES – LOOPS, ARGUMENTS, PACKAGES, ERRORS

========================

TASK 1: FOR LOOP

for_loop.sh

#!/bin/bash

fruits=("Apple" "Banana" "Orange" "Mango" "Grapes")

for fruit in "${fruits[@]}"

do

echo "$fruit"

done


count.sh

#!/bin/bash

for i in {1..10}

do

echo "$i"

done

========================

TASK 2: WHILE LOOP

countdown.sh

#!/bin/bash

echo "Enter a number:"

read num

while [ "$num" -ge 0 ]

do

echo "$num"

num=$((num - 1))

done

echo "Done!"

========================

TASK 3: COMMAND LINE ARGUMENTS

greet.sh

#!/bin/bash

if [ -z "$1" ]; then

echo "Usage: ./greet.sh <name>"

exit 1

fi

echo "Hello, $1!"


# args_demo.sh

#!/bin/bash

echo "Script name: $0"

echo "Total arguments: $#"

echo "All arguments: $@"

========================

TASK 4: INSTALL PACKAGES SCRIPT

install_packages.sh

#!/bin/bash

Check if running as root

if [ "$EUID" -ne 0 ]; then

echo "Run as root"

exit 1

fi

packages=("nginx" "curl" "wget")

for pkg in "${packages[@]}"

do

echo "Checking $pkg..."

if command -v dpkg &> /dev/null; then

   dpkg -s "$pkg" &> /dev/null

   installed=$?

elif command -v rpm &> /dev/null; then

  rpm -q "$pkg" &> /dev/null

   installed=$?

else

  echo "Unsupported package manager"

  exit 1

fi

if [ "$installed" -eq 0 ]; then

   echo "$pkg is already installed. Skipping."

else

  echo "$pkg is not installed. Installing..."

  if command -v apt &> /dev/null; then

  apt update && apt install -y "$pkg"

   elif command -v yum &> /dev/null; then

   yum install -y "$pkg"

  elif command -v dnf &> /dev/null; then

  dnf install -y "$pkg"
    fi

fi

echo "-----------------------------------"

done

========================

TASK 5: ERROR HANDLING


safe_script.sh

#!/bin/bash

set -e

mkdir /tmp/devops-test || echo "Directory already exists"

cd /tmp/devops-test || { echo "Failed to navigate to directory"; exit 1; }

touch testfile.txt || { echo "Failed to create file"; exit 1; }

echo "Script completed successfully."

========================

IMPORTANT COMMANDS

Make script executable:

chmod +x scriptname.sh

Run script:

./scriptname.sh

Run as root:

sudo ./scriptname.sh

========================

KEY CONCEPTS SUMMARY

For loop syntax:

for item in list; do

command

done

While loop syntax:

while [ condition ]; do

command

done

Arguments:

$1 = first argument

$# = number of arguments

$@ = all arguments

$0 = script name

Check if root:

if [ "$EUID" -ne 0 ]; then

echo "Run as root"

exit 1



fi
