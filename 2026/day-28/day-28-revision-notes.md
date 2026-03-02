# Day 28 – Progress Review & Challenges

# What You've Covered So Far

# Day 1 – DevOps & Cloud Intro
DevOps basics, SDLC, Cloud fundamentals

# Days 2–7 – Linux Fundamentals
Architecture, commands, processes, systemd, file system hierarchy, troubleshooting, text files

# Day 8 – Cloud Server Setup
Docker, Nginx, web deployment

# Days 9–11 – Users, Permissions & Ownership
User/group management, file permissions, `chmod`, `chown`, `chgrp`

# Day 12 – Revision Day
Recap of Days 1–11

# Day 13 – Volume Management
LVM: physical volumes, volume groups, logical volumes

# Days 14–15 – Networking
DNS, IP, subnets, ports, connectivity checks

# Days 16–18 – Shell Scripting
Variables, loops, arguments, error handling, functions

# Days 19–20 – Shell Projects
Log rotation, backup scripts, crontab, log analyzer

# Day 21 – Shell Cheat Sheet
Personal scripting reference

# Days 22–25 – Git & GitHub
Init, branch, merge, rebase, stash, cherry-pick, reset, revert, branching strategies

# Day 26 – GitHub CLI
Manage repos, PRs, issues from terminal

# Day 27 – GitHub Profile
Profile README, repo cleanup, branding

---

# Task 1 – Self-Assessment Checklist

Mark each:
- ✅ Can do confidently
- ⚠ Need to revisit
- ❌ Haven't done yet

---

# Linux Skills

- Navigate filesystem (`cd`, `ls`, `rm`, `mv`)
- Manage processes (`ps`, `top`, `kill`, `bg`, `fg`)
- Manage services (`systemctl start/stop/status`)
- Edit files (`vim`, `nano`)
- Troubleshoot (`top`, `free`, `df`, `du`)
- Explain FHS (`/etc`, `/var`, `/home`, `/tmp`)
- Manage users/groups (`useradd`, `passwd`)
- Set permissions (`chmod 755 file`)
- Change ownership (`chown`, `chgrp`)
- Manage LVM
- Check networking (`ping`, `curl`, `ss`, `dig`)
- Explain DNS, IP, subnets, ports

---

# Shell Scripting Skills

- Write scripts with variables & arguments
- Use `if/elif/else`, `case`
- Use `for`, `while`, `until`
- Define functions
- Use `grep`, `awk`, `sed`, `sort`, `uniq`
- Handle errors: `set -euo pipefail`
- Schedule jobs with `crontab`

---

# Git & GitHub Skills

- `git init`, `add`, `commit`, `log`
- Branching (`branch`, `checkout`, `switch`)
- `push`, `pull`
- Explain clone vs fork
- Merge (fast-forward vs merge commit)
- Rebase vs merge
- `git stash`
- `git cherry-pick`
- Squash merge
- `git reset` vs `git revert`
- Branching strategies (GitFlow, GitHub Flow, Trunk-Based)
- Use `gh` CLI

---

# Task 2 – Revisit Weak Spots

1. Pick 3 weak topics
2. Redo hands-on practice
3. Document learning in `day-28-notes.md`

---

# Task 3 – Quick-Fire Questions (Memory Test)

# chmod 755 script.sh
Owner: read/write/execute  
Group: read/execute  
Others: read/execute  

---

# Process vs Service
Process → running program  
Service → background process managed by systemd  

---

# Find Process Using Port 8080
`ss -tulnp | grep 8080`  
or  
`lsof -i :8080`

---

# set -euo pipefail
- `-e` → exit on error  
- `-u` → error on unset variable  
- `-o pipefail` → fail if any command in pipe fails  

---

# git reset --hard vs git revert
`reset --hard` → deletes commits  
`revert` → creates undo commit  

---

# Branch Strategy for 5 Devs Shipping Weekly
GitHub Flow ✅

---

# git stash
Temporarily saves uncommitted changes  
Used when switching branches quickly

---

# Run Script Daily at 3 AM
`0 3 * * * /path/script.sh`

---

# git fetch vs git pull
`fetch` → download changes  
`pull` → fetch + merge  

---

# What is LVM?
Logical Volume Manager  
Allows flexible resizing of storage without repartitioning  

---

# Task 4 – Organize Work

- Ensure Day 1–27 pushed to GitHub  
- Update `git-commands.md`  
- Update shell cheat sheet  
- Clean GitHub profile  

---

# Task 5 – Teach It Back Example

# Explaining Git Branching Simply

A branch in Git is like creating a copy of your project to work safely.  
You can experiment without breaking the main project.  
Once your work is ready, you merge it back.  
This allows multiple developers to work at the same time.  
Branches help avoid conflicts and keep development organized.
