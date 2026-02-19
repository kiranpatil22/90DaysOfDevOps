Files Created

script.sh

devops.txt

notes.txt

project/ (directory)

Permission Changes
1️⃣ script.sh

Before:

-rw-r--r--


After:

-rwxr-xr-x


✔ Made executable using chmod +x

2️⃣ devops.txt

Before:

-rw-r--r--


After:

-r--r--r--


✔ Removed write permission for owner, group, and others (a-w)

3️⃣ notes.txt

Before:

-rw-r--r--


After (640):

-rw-r-----


✔ Owner: read & write
✔ Group: read only
✔ Others: no access

4️⃣ project/ (directory)

After Creation (755):

drwxr-xr-x


✔ Owner: full access
✔ Group: read & execute
✔ Others: read & execute

Commands Used
# Make script executable
chmod +x script.sh
ls -l script.sh
./script.sh

# Remove write permission for all
chmod a-w devops.txt
ls -l devops.txt

# Set notes.txt to 640
chmod 640 notes.txt
ls -l notes.txt

# Create project directory with 755
mkdir project
chmod 755 project
ls -ld project
