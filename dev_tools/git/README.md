# Git

Git is a version-control system that records changes to project files as commits.
Its history lets you compare versions, recover earlier work, and develop
alternatives on branches. This folder covers the concepts and command-line
operations used to maintain a computational project.

## Essential commands

In an existing repository, review and record saved edits:

```sh
git status
git diff
git add README.md
git diff --staged
git commit -m "Document the calculation method"
```

Replace `README.md` with the file you intend to record. A commit saves the selected
changes in local history; publishing them to a remote repository is a separate step.

## Reference

- [Cheat sheet](git_cheat_sheet.md) — Repositories, staging, branches, synchronization, and recovery.
