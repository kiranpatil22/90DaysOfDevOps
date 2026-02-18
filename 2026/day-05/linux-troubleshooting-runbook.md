LINUX RUNBOOK DRILL
Target Service: ssh

ENVIRONMENT BASICS

Command:
uname -a

Output:
Linux ip-172-31-30-174 5.15.0-105-generic x86_64 GNU/Linux

Observation:
Ubuntu-based Linux kernel 5.15 running on x86_64.

Command:
cat /etc/os-release

Output:
NAME="Ubuntu"
VERSION="22.04.3 LTS (Jammy Jellyfish)"

Observation:
System is Ubuntu 22.04 LTS.

FILESYSTEM SANITY

Command:
mkdir /tmp/runbook-demo

Command:
cp /etc/hosts /tmp/runbook-demo/hosts-copy

Command:
ls -l /tmp/runbook-demo

Output:
-rw-r--r-- 1 root root 411 Feb 18 10:22 hosts-copy

Observation:
Filesystem writable, copy successful, permissions normal.

CPU / MEMORY

Command:
ps -o pid,pcpu,pmem,comm -p $(pgrep sshd)

Output:
PID %CPU %MEM COMMAND
612 0.0 0.3 sshd

Observation:
SSH using minimal CPU and memory.

Command:
free -h

Output:
Mem: 914Mi total, 404Mi used, 509Mi available
Swap: 0B

Observation:
Memory healthy, no swap configured.

DISK / IO

Command:
df -h

Output:
/dev/xvda1 8.0G 2.1G 5.6G 28% /

Observation:
Disk usage normal, plenty of free space.

Command:
du -sh /var/log

Output:
45M /var/log

Observation:
Log directory small, no excessive growth.

NETWORK

Command:
ss -tulpn | grep 22

Output:
LISTEN 0 128 0.0.0.0:22 0.0.0.0:* users:(("sshd",pid=612))

Observation:
SSH listening correctly on port 22.

Command:
curl -I http://localhost

Output:
curl: (7) Failed to connect

Observation:
No web service running locally (expected on minimal server).

LOGS

Command:
journalctl -u ssh -n 20

Output:
Started OpenBSD Secure Shell server.
Accepted publickey for ubuntu

Observation:
SSH started successfully, login attempts recorded.

Command:
tail -n 20 /var/log/auth.log

Output:
Accepted publickey for ubuntu from 10.0.0.5

Observation:
Recent successful login, no authentication failures.

SUMMARY

System healthy.
SSH service active and listening.
No high CPU, memory, disk, or log errors observed.

IF THIS WORSENS

Restart service:
sudo systemctl restart ssh

Increase log inspection:
journalctl -u ssh -f

Deep process tracing:
sudo strace -p <sshd-pid>
