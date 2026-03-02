Day 23 Notes – Git Branching & GitHub
Task 1 – Theory

• Branch: Separate line of development.
• Why branches? Keeps main stable, safe development, multiple developers can work.
• HEAD: Pointer to current branch and latest commit.
• Switching branches: Files change to match that branch.

Task 2 – Branch Commands

List branches:
git branch

Create branch:
git branch feature-1

Switch branch:
git checkout feature-1

Create + switch:
git checkout -b feature-2

Using switch:
git switch feature-1

Commit in feature branch:
git add .
git commit -m "message"

Delete branch:
git branch -d branch-name

Difference:
git checkout → old, used for branches & files
git switch → new, only for branches

Task 3 – Push to GitHub

Add remote:
git remote add origin <url>

Push main:
git push -u origin main

Push feature branch:
git push -u origin feature-1

origin = your repo
upstream = original repo (after fork)

Task 4 – Fetch vs Pull

git fetch → download only
git pull → download + merge

Task 5 – Clone vs Fork

Clone → copy repo to local machine
Fork → create your own copy on GitHub

Use clone → when you just need local copy
Use fork → when contributing to others project

Sync fork:
git fetch upstream
git merge upstream/main

If you want ultra-short exam version (1–2 lines per answer), tell me 👍
