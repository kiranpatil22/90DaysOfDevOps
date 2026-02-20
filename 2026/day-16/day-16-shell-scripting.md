# name print
#!/bin/bash

NAME="Alice"

ROLE="DevOps Engineer"

# Double quotes → variables expanded
echo "Hello, I am $NAME and I am a $ROLE"

# Single quotes → variables not expanded
echo 'Hello, I am $NAME and I am a $ROLE'

# Challenge Tasks – Bash Scripting Fundamentals

---

## Task 1: Your First Script
**hello.sh**

# user input with vriables 

#!/bin/bash

read -p "Enter your name: " name

read -p "Enter your favourite tool: " tool

echo "Hello $name, your favourite tool is $tool"

# if-else condition 

#!/bin/bash

read -p "Enter a number: " num

if [ "$num" -gt 0 ]; then

  echo "The number $num is positive."

elif [ "$num" -lt 0 ]; then

  echo "The number $num is negative."

else
 
  echo "The number is zero."

fi

# file check

#!/bin/bash
read -p "Enter filename: " file

if [ -f "$file" ]; then

  echo "File $file exists."

else

  echo "File $file does not exist."
  
  fi

# server check

#!/bin/bash

SERVICE="nginx"

read -p "Do you want to check the status? (y/n): " choice

if [ "$choice" == "y" ]; then

  systemctl status $SERVICE --no-pager > /dev/null 2>&1
  if [ $? -eq 0 ]; then
        echo "$SERVICE is active."
    else
        echo "$SERVICE is not active."
    fi
else
    echo "Skipped."
fi







