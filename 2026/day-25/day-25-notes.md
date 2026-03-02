# Day 25 – Git Reset, Revert, Branching Strategies

# Task 1 – Git Reset (Hands-On)

# Step 1 – Create 3 Commits
`git commit -m "Commit A"`  
`git commit -m "Commit B"`  
`git commit -m "Commit C"`

---

# git reset --soft

## Command
`git reset --soft HEAD~1`

## What Happens
- Moves HEAD back by 1 commit
- Changes stay staged
- Nothing is deleted

---

# git reset --mixed (Default)

## Command
`git reset --mixed HEAD~1`

## What Happens
- Moves HEAD back by 1 commit
- Changes move to working directory
- Files become unstaged

---

# git reset --hard

## Command
`git reset --hard HEAD~1`

## What Happens
- Moves HEAD back by 1 commit
- Deletes changes permanently
- Working directory reset to that commit

---

# Reset Difference Summary

## --soft
Moves HEAD only → Keeps changes staged

## --mixed
Moves HEAD → Keeps changes but unstaged

## --hard
Moves HEAD → Deletes changes completely

---

# Which is Destructive?
`--hard` is destructive  
Because it permanently deletes uncommitted changes.

---

# When to Use Each

## --soft
When you want to edit or combine commits.

## --mixed
When you want to unstage changes but keep code.

## --hard
When you want to completely discard changes.

---

# Should You Reset Pushed Commits?
No ❌  
It rewrites history and breaks shared repositories.

---

# Task 2 – Git Revert (Hands-On)

# Step 1 – Create 3 Commits
`git commit -m "Commit X"`  
`git commit -m "Commit Y"`  
`git commit -m "Commit Z"`

---

# Revert Middle Commit

## Command
`git revert <commit-id-of-Y>`

## What Happens
- Creates a new commit that undoes Y
- Original commit Y stays in history

---

# Is Commit Y Still in git log?
Yes ✅  
Revert does NOT remove history.

---

# Reset vs Revert

## git reset
- Rewrites history
- Moves branch pointer backward
- Can delete commits

## git revert
- Adds new commit that undoes changes
- Keeps history intact
- Safe for shared branches

---

# Why Revert is Safer?
Because it does NOT rewrite commit history.

---

# When to Use Revert vs Reset

## Use Reset
- Local branch
- Before pushing
- Cleaning up commits

## Use Revert
- Shared branch
- Production branch
- After pushing

---

# Task 3 – Reset vs Revert Comparison

| Feature | git reset | git revert |
|----------|------------|-------------|
| What it does | Moves branch pointer | Creates undo commit |
| Removes commit from history? | Yes | No |
| Safe for pushed branches? | No | Yes |
| When to use | Local cleanup | Undo in shared repo |

---

# Task 4 – Branching Strategies

# GitFlow

## How It Works
Separate branches for `main`, `develop`, `feature`, `release`, `hotfix`

## Flow
main  
└── develop  
  └── feature branches  

## Used In
Large teams, scheduled releases
