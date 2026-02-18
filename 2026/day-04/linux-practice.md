LINUX PRACTICE NOTE
Service Inspected: ssh

PROCESS CHECKS

ps aux | grep ssh
Shows running ssh processes and confirms if sshd is active.

pgrep sshd
Displays the Process ID (PID) of the ssh service if running.

top
Shows real-time CPU and memory usage to check system load and running processes.

SERVICE CHECKS

systemctl status ssh
Shows whether the ssh service is active, inactive, or failed.

systemctl list-units --type=service | grep ssh
Lists all active services and filters for ssh to confirm it is loaded and running.

systemctl restart ssh
Restarts the ssh service if it is not responding properly.

LOG CHECKS

journalctl -u ssh -n 20
Displays the last 20 log entries related to the ssh service.

tail -n 50 /var/log/auth.log
Shows the last 50 authentication log entries (useful for login issues).

PORT CHECK

ss -tulnp | grep 22
Checks if port 22 (default SSH port) is listening.

MINI TROUBLESHOOTING STEPS

If SSH is not working:

Step 1: Check process
ps aux | grep ssh

Step 2: Check service status
systemctl status ssh

Step 3: Restart service
sudo systemctl restart ssh

Step 4: Check logs
journalctl -u ssh -n 20

Step 5: Check port
ss -tulnp | grep 22

SUMMARY

Process commands confirm the service is running.
Service commands confirm service health and control it.
Log commands help identify errors.
Port checks confirm network connectivity.
