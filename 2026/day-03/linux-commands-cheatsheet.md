LINUX DEVOPS CHEAT SHEET
(Process Management | File System | Networking Troubleshooting)

PROCESS MANAGEMENT

View Running Processes
ps aux
ps aux | grep nginx

Real-Time Monitoring
top
htop

Kill a Process
kill <PID>
kill -9 <PID>

Manage Services (systemd)
systemctl status nginx
systemctl start nginx
systemctl stop nginx
systemctl restart nginx

Check Background Jobs
jobs

FILE SYSTEM COMMANDS

Check Current Directory
pwd

List Files
ls
ls -la
ls -lh

Change Directory
cd /path/to/folder
cd ..
cd ~

Create Files and Folders
touch file.txt
mkdir folder

Delete Files and Folders
rm file.txt
rm -rf folder

Copy Files and Folders
cp file.txt /tmp/
cp -r folder /tmp/

Move Files
mv file.txt /home/user/

Check Permissions
ls -l

Change Permissions
chmod +x script.sh

Change Ownership
chown user:group file.txt

Check Disk Space
df -h

Check Folder Size
du -sh *
du -sh folder/

NETWORKING TROUBLESHOOTING

Check IP Address
ip a

Test Internet Connectivity
ping google.com

Check Open Ports
ss -tulnp
netstat -tulnp

Check If Specific Port Is Listening
ss -tulnp | grep 8080

Test Web Service
curl http://localhost:8080

curl -I http://example.com

DNS Check
nslookup google.com
dig google.com

Check Firewall Status
ufw status

BASIC DEVOPS TROUBLESHOOTING FLOW

If application is not working:

Check service status
systemctl status appname

Check if port is listening
ss -tulnp | grep portnumber

Test locally
curl localhost:portnumber

Check disk space
df -h

Check CPU and memory
top

Important Reminders

High CPU -> use top
High Memory -> use free -h
Port not accessible -> use ss -tulnp
Disk full -> use df -h
Service down -> use systemctl

You can print this and keep it beside your laptop while practicing on EC2.
