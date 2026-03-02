## Day 23 – Git Branching Notes

# What is a branch in Git?
A branch is a separate line of development.
It lets you work on new features or fixes without affecting the main code.
Git creates a default branch called main.

# Why use branches instead of committing everything to main?
Branches keep main stable and production-ready.
They allow multiple developers to work at the same time.
They prevent unfinished or buggy code from breaking the main project.
They make testing and code review easier.

# What is HEAD in Git?
HEAD is a pointer to the current branch and its latest commit.
It tells Git where you are currently working.

# What happens when you switch branches?
Git updates your working files to match the selected branch.
HEAD moves to that branch.
If you have uncommitted changes, Git may ask you to commit or stash them first.
