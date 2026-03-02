# Day 24 – Merge, Rebase, Stash, Cherry-Pick Notes

# Fast-Forward Merge
No new commits on main → branch pointer moves forward

## Command
    git checkout main  
    git merge feature-login


# Merge Commit
Both branches have commits → Git creates merge commit

## Command
    git merge feature-signup


# Merge Conflict
Same line edited in both branches → manual resolution needed

## Command
    git merge feature-branch


# Rebase
Moves feature commits on top of updated main (linear history)
## Command (Avoid if already pushed)
    git rebase main

## Command
    git checkout feature-dashboard  
    git rebase main


# Never Rebase Pushed Commits
Rewrites history and breaks shared repositories


# Squash Merge
Combines multiple commits into one commit

## Command
    git merge --squash feature-profile  
    git commit -m "Feature profile complete"


# Regular Merge
Keeps all commits + adds merge commit

## Command
    git merge feature-settings


# Git Stash
Temporarily saves uncommitted changes

## Command
    git stash


# Git Stash Pop
Applies stash and removes it

## Command
    git stash pop


# Git Stash Apply
Applies stash but keeps it saved

## Command
    git stash apply stash@{0}


# Cherry-Pick
 Copies one specific commit to current branch

## Command
    git cherry-pick <commit-id>
