PAGE 1 – CORE COMMANDS & CONCEPTS
1️⃣ Users & Groups
Create User

useradd -m username
passwd username

Delete User

userdel username
userdel -r username (removes home directory)

Create Group

groupadd groupname

Add User to Group

usermod -aG groupname username

Verify

id username
getent passwd username

2️⃣ File Ownership
Check Ownership

ls -l

Format:
-rw-r--r-- 1 owner group size date filename

Owner → individual user
Group → shared access group

Change Owner

chown username filename

Change Group

chgrp groupname filename

Change Owner + Group

chown owner:group filename

Recursive Change

chown -R owner:group directory/

Always verify:
ls -l
ls -lR directory/

3️⃣ Permissions Basics

Permission examples:
644 → rw-r--r--
755 → rwxr-xr-x
775 → rwxrwxr-x

Change permissions:
chmod 775 filename

Set shared directory:
chown :groupname directory
chmod 775 directory
chmod g+s directory (inherit group)

Avoid:
chmod 777 (security risk)

4️⃣ File & Directory Operations

Create file:
touch filename

Append text:
echo "text" >> file.txt

Copy:
cp source destination

Create directory:
mkdir dirname
mkdir -p parent/child

Remove directory:
rm -rf directory (use carefully)

PAGE 2 – SERVICES, PROCESSES & REVISION
5️⃣ Processes

View processes:
ps aux

Search process:
ps aux | grep nginx

Kill process:
pkill -u username

6️⃣ Services (systemctl)

Check service:
systemctl status ssh

Start service:
systemctl start ssh

Stop service:
systemctl stop ssh

Restart:
systemctl restart ssh

Enable at boot:
systemctl enable ssh

7️⃣ Logs (journalctl)

Check service logs:
journalctl -u ssh

Recent logs:
journalctl -u ssh --no-pager | tail

System errors:
journalctl -xe

8️⃣ Practical Ownership Scenarios Practiced

✔ Created shared directories (/opt/team-workspace)
✔ Assigned group ownership
✔ Set 775 permissions
✔ Used su - username to test access
✔ Changed ownership recursively
✔ Verified with ls -l and id

9️⃣ Troubleshooting Flow You Practiced

Check ownership → ls -l

Check user groups → id username

Fix ownership → chown user:group file

Fix permissions → chmod 775 file

Verify again → ls -l

If service issue → systemctl status + journalctl

🔟 Top 5 Commands for Incidents

ls -l
systemctl status <service>
journalctl -u <service>
ps aux
chown

Focus Areas Moving Forward

• Permission numbers (644 vs 755 vs 775)
• Recursive ownership safety
• Service troubleshooting
• Reading logs confidently
• Avoiding 777 mistakes
