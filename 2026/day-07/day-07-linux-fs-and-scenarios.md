Core Rule:
Always check status first → read logs → verify configuration → take action.

SCENARIO 1: Service Not Starting (myapp)

Step 1:
systemctl status myapp
Why: Check if service is active, failed, or stopped.

Step 2:
journalctl -u myapp -n 50
Why: View recent logs to identify error messages.

Step 3:
systemctl is-enabled myapp
Why: Check if service is configured to start on boot.

Step 4:
systemctl restart myapp
Why: Attempt restart after identifying or fixing issue.

Learning:
Always check status → then logs → then boot configuration.

SCENARIO 2: High CPU Usage

Step 1:
top
Why: View real-time CPU usage and active processes.

Step 2:
ps aux --sort=-%cpu | head -10
Why: List top 10 CPU-consuming processes.

Step 3:
pgrep <process-name>
Why: Find PID of suspicious process.

Step 4:
kill <PID>
Why: Stop runaway process if necessary.

Learning:
Identify high CPU process → note PID → investigate or stop safely.

SCENARIO 3: Finding Service Logs (docker)

Step 1:
systemctl status docker
Why: Confirm service state before checking logs.

Step 2:
journalctl -u docker -n 50
Why: View last 50 log entries for errors.

Step 3:
journalctl -u docker -f
Why: Follow logs in real-time for live troubleshooting.

Learning:
systemd services store logs in journald → use journalctl.

SCENARIO 4: File Permission Issue

Problem:
./backup.sh → Permission denied

Step 1:
ls -l /home/user/backup.sh
Why: Check current permissions.

Step 2:
chmod +x /home/user/backup.sh
Why: Add execute permission.

Step 3:
ls -l /home/user/backup.sh
Why: Confirm ‘x’ permission added.

Step 4:
./backup.sh
Why: Test execution.

Learning:
No ‘x’ permission = cannot execute.

TROUBLESHOOTING FLOW SUMMARY

Service issue:
systemctl status → journalctl → restart → verify enable

CPU issue:
top → ps sorted by CPU → identify PID → take action

Log issue:
systemctl status → journalctl -u service

Permission issue:
ls -l → chmod → verify → retry

KEY PRINCIPLE

Do not memorize commands.
Follow the pattern:

Observe
Investigate
Validate
Act
Verify
