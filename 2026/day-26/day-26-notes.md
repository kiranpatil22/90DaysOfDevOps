# Day 26 – GitHub CLI (gh) Hands-On

# Task 1 – Install and Authenticate

# Install GitHub CLI
(Download from https://cli.github.com or use package manager)

Windows:
`winget install GitHub.cli`

Mac:
`brew install gh`

Linux:
`sudo apt install gh`

---

# Authenticate
`gh auth login`

Follow prompts:
- GitHub.com
- HTTPS
- Login via browser

---

# Verify Login
`gh auth status`

Shows:
- Logged-in account
- Active hostname
- Token scopes

---

# Authentication Methods Supported by gh
- Browser-based OAuth login
- Personal Access Token (PAT)
- SSH authentication
- GitHub Enterprise support

---

# Task 2 – Working with Repositories

# Create New Repo (Public + README)
`gh repo create test-repo --public --clone --add-readme`

---

# Clone Repo Using gh
`gh repo clone username/repo-name`

---

# View Repo Details
`gh repo view username/repo-name`

---

# List All Your Repositories
`gh repo list`

---

# Open Repo in Browser
`gh repo view --web`

---

# Delete Repo (Be Careful)
`gh repo delete username/test-repo`

---

# Task 3 – Issues

# Create Issue
`gh issue create --title "Bug Fix" --body "Fix login issue" --label bug`

---

# List Open Issues
`gh issue list`

---

# View Specific Issue
`gh issue view 12`

---

# Close Issue
`gh issue close 12`

---

# Using gh issue in Automation
- Can auto-create issues from CI failures
- Can close issues after successful deployment
- Can generate release reports
- Useful in DevOps pipelines

---

# Task 4 – Pull Requests

# Create Branch
`git checkout -b feature-branch`

# Make Changes + Commit
`git add .`  
`git commit -m "New feature"`

# Push Branch
`git push origin feature-branch`

# Create Pull Request
`gh pr create --title "New Feature" --body "Adds new feature"`

---

# List Open PRs
`gh pr list`

---

# View PR Details
`gh pr view 5`

---

# Merge PR from Terminal
`gh pr merge 5`

---

# Merge Methods Supported
- Merge commit
- Squash merge
- Rebase merge

Example:
`gh pr merge 5 --squash`  
`gh pr merge 5 --rebase`

---

# Review Someone Else's PR

View PR:
`gh pr view 8`

Checkout locally:
`gh pr checkout 8`

Approve:
`gh pr review 8 --approve`

Request changes:
`gh pr review 8 --request-changes`

Comment:
`gh pr review 8 --comment`

---

# Task 5 – GitHub Actions (Preview)

# List Workflow Runs
`gh run list`

---

# View Specific Workflow Run
`gh run view 123456`

---

# Useful in CI/CD Because
- Monitor pipeline status from terminal
- Download logs for debugging
- Trigger workflows
- Integrate into deployment scripts

---

# Task 6 – Useful gh Tricks

# Raw GitHub API Calls
`gh api repos/{owner}/{repo}`

---

# Manage Gists
`gh gist create file.txt`  
`gh gist list`

---

# Manage Releases
`gh release create v1.0.0 --notes "Initial release"`  
`gh release list`

---

# Create Aliases
`gh alias set co 'pr checkout'`

---

# Search Repositories
`gh search repos devops --limit 5`
