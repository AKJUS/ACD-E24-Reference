# Git cheat sheet

Git records the history of a project's files. This guide explains repositories,
commits, branches, and synchronization, then provides a command reference for
inspecting changes, recording work, and recovering earlier versions.

**Contents:** [Fundamentals](#fundamentals) · [Command-line reference](#command-line-reference)

## Fundamentals

A repository contains the project files and their recorded history. Use that
history to compare versions, recover committed content, and develop alternatives
on separate branches.

### Working tree, staging area, and commits

| Term | Meaning |
| --- | --- |
| **Working tree** | The files currently present in the project directory. |
| **Staging area** | The changes selected for the next commit. |
| **Commit** | A recorded snapshot with an author, timestamp, message, and link to its preceding history. |
| **Branch** | A named line of development that advances as commits are added. |
| **Remote** | A named connection to another repository; a clone usually calls its source `origin`. |

Saving in an editor changes a file on disk. Staging selects changes, and committing
records them in local history. Pushing transfers local commits to a remote.

```text
Edit and save → Review and stage → Commit locally → Push to a remote
```

A local commit survives further edits, but it does not provide an off-device copy.
Unsaved and uncommitted work is not protected by commit history.

### Inspect changes before recording them

A **diff** compares two versions. Read it before committing: check the intended
changes, unexpected deletions, and files generated while running the program.
Group related edits and write a commit message that explains the change, such as
`Normalize the distance field before mapping RGB channels`.

A `.gitignore` file excludes matching untracked paths from normal staging. It is
useful for caches, generated output, and local environments. It does not remove
files already committed to the repository.

### Fetch, pull, and push

| Operation | Effect |
| --- | --- |
| **Fetch** | Downloads remote commits and updates knowledge of the remote's branches without replacing working files. |
| **Pull** | Fetches and integrates remote changes into the current branch. |
| **Push** | Sends local commits to a remote where the account has write access. |

Inspect local work before pulling. Commit it on the appropriate branch or
preserve it separately. A commit records your version but does not guarantee
that subsequent changes can be combined without conflicts.

Cloning copies a repository locally. Forking creates another repository under an
account on the hosting service. A fork is useful for independently developed
changes or contributions when direct write access is unavailable; it is not
necessary merely to download updates.

### Branches, merging, and pull requests

A branch lets you develop an alternative without advancing another branch.
Switching branches changes the checked-out files in the same project directory.
Commit or preserve unfinished edits before switching.

A **merge** combines histories. A **pull request** proposes a merge and provides
a place to inspect and discuss the changes. The proposal and the merge are
separate actions.

If changes cannot be merged automatically, resolve the conflict by reading both
versions and producing the intended combined result. Verify the affected code
before recording the resolution.

### Recovering work

Start by locating the relevant commit and examining its diff. You can recover
specific content and record the repair as a new commit. A **revert** records an
inverse change while preserving history.

**Discard** removes selected uncommitted edits. **Reset** can move branch history
and, depending on its mode, replace staged or working content. Inspect the
operation and preserve required work before using either. Rewriting shared
history affects anyone working from that history.

## Command-line reference

Run repository commands from its project directory. Replace uppercase placeholders
with the relevant URL or identifier. Inspect `git status` before changing history
or integrating remote work.

### Create or clone

Clone an existing repository:

```sh
git clone REPOSITORY_URL
```

Cloning configures the remote as `origin`; it does not require a subsequent
`git init`. For a new local project, navigate to its directory and run:

```sh
git init -b main
```

### Configure commit identity

```sh
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

These settings identify commits; they do not authenticate with a hosting service.
Omit `--global` when deliberately configuring only the current repository.

### Inspect

| Command | Purpose |
| --- | --- |
| `git status` | Current branch and changed files. |
| `git diff` | Changes not yet staged. |
| `git diff --staged` | Changes selected for the next commit. |
| `git log --oneline -10` | Ten most recent commits. |
| `git show COMMIT_ID` | Inspect one commit. |
| `git remote -v` | Remote names and URLs. |
| `git branch` | Local branches and the current selection. |

### Stage and commit

Save the files first. This example records a change to `README.md`:

```sh
git diff
git add README.md
git diff --staged
git commit -m "Explain the coordinate system and units"
```

To unstage a file while retaining its working edits:

```sh
git restore --staged README.md
```

### Synchronize

```sh
git fetch origin
git pull --ff-only
git push
```

These are separate operations. Fetch downloads remote history; pull updates the
current branch; push uploads local commits. The `--ff-only` option refuses a pull
that would require merging diverged histories. If it stops, inspect the histories
rather than forcing the update.

A push requires a configured remote and write access. For a newly created branch,
set its upstream when first publishing it:

```sh
git push -u origin compare-fields
```

### Branch and merge

Start an experiment from the current commit:

```sh
git switch -c compare-fields
```

After committing the work, return to the target branch and merge when appropriate:

```sh
git switch main
git merge compare-fields
```

Check that `main` is the intended target. Resolve conflicts, run the affected code,
and inspect the result before pushing. To delete the local branch after it has
been merged:

```sh
git branch -d compare-fields
```

The lowercase `-d` refuses to delete a branch Git considers unmerged. Deleting a
local branch does not delete a remote branch.

### Reverse a committed change

```sh
git revert COMMIT_ID
```

This creates an inverse change without removing the original history. Inspect the
result because later work may depend on the reverted commit. Preserve uncommitted
work before any recovery operation.
