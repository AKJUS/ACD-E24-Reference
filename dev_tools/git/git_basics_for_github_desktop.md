# Git Basics for GitHub Desktop Beginners

## Table of Contents
1. [Version Control in Plain Language](#version-control-in-plain-language)
2. [Git vs. GitHub vs. GitHub Desktop](#git-vs-github-vs-github-desktop)
3. [Core Concepts Cheat Sheet](#core-concepts-cheat-sheet)
4. [How a Change Travels](#how-a-change-travels)
5. [Everyday Workflow in GitHub Desktop](#everyday-workflow-in-github-desktop)
6. [Commit Example Step by Step](#commit-example-step-by-step)
7. [Syncing with GitHub (Push & Pull)](#syncing-with-github-push--pull)
8. [Branches Without Fear](#branches-without-fear)
9. [Undoing Mistakes Safely](#undoing-mistakes-safely)
10. [Assignment/Project Checklist](#assignmentproject-checklist)
11. [Try It Yourself](#try-it-yourself)
12. [Quick Reference](#quick-reference)

---

## Version Control in Plain Language
Version control is like a **time machine for your project**. Imagine you’re writing a story, and every time you finish a chapter, you save a snapshot of your work. If you ever want to go back to an earlier version, you can hop into your time machine and revisit that exact moment. Git does this for your code and files.

This means you never lose your work—even if you make mistakes or accidentally delete something important. Instead of hoping you remember what you changed or keeping many confusing copies, Git keeps a neat timeline of every meaningful version called *commits*. Each commit has a message explaining what changed, so you can understand your project’s history.

**Mini example**
- You write a lab report.
- Your partner edits the introduction, you update the graphs.
- Instead of emailing files back and forth, Git saves each change as a *commit* with a message like "Add intro" or "Update graphs".
- You can revisit any commit, compare versions, or recover deleted content.

The key takeaway: Git keeps your work organized and recoverable. GitHub Desktop gives you buttons for the most important Git actions, making it easier to use without typing commands.

---

## Git vs. GitHub vs. GitHub Desktop

| Tool | What it is | Why you care | Beginner Example |
| --- | --- | --- | --- |
| **Git** | Version control engine running on your computer | Tracks changes, remembers history | You save your work with detailed notes on what you did. |
| **GitHub** | Website hosting Git repositories in the cloud | Stores backups, lets teammates and instructors see your work | Your instructor grades your assignments here, and teammates can collaborate. |
| **GitHub Desktop** | App that talks to Git locally and GitHub online | Gives you a point-and-click way to commit, push, pull, and manage branches | You click buttons to save changes, upload work, and get updates without typing commands. |

Think of GitHub Desktop as a friendly translator between you and the Git/GitHub world, helping you focus on your work instead of the technical details.

---

## Core Concepts Cheat Sheet

| Word | Plain meaning | Where you see it | Beginner-friendly example |
| --- | --- | --- | --- |
| **Repository (repo)** | Project folder that Git tracks | Local folder on your computer and matching repo on GitHub | Like a project folder with superpowers that remembers every change you make |
| **Working directory** | The actual files you edit | Your code editor or Finder/Explorer | The place where you write and save your files, like your desktop workspace |
| **Staging** | Picking which changes go into the next commit | Checkboxes beside files in GitHub Desktop | Choosing which edits to include in your next saved snapshot, like packing only some items for a trip |
| **Commit** | Saved snapshot with a short message | `History` tab in GitHub Desktop | Taking a photo of your project at a moment in time, with a label explaining what’s new |
| **Branch** | Alternate timeline for changes | Branch dropdown in GitHub Desktop | A separate path to try new ideas without messing up your main work |
| **Remote** | Copy of your repo stored elsewhere (usually GitHub) | Shows up as `origin` inside GitHub Desktop | Your project’s backup copy stored safely online, like cloud storage |

---

## How a Change Travels
```
Edit files        Stage selected files       Make a commit       Sync with GitHub
┌──────────┐      ┌──────────────────┐      ┌──────────────┐    ┌───────────────┐
│Working   │ ===> │Staging area      │ ===> │Commit history│ => │GitHub (remote)│
│directory │      │("Changes" list)  │      │("History")   │    │"Push"/"Pull"  │
└──────────┘      └──────────────────┘      └──────────────┘    └───────────────┘
```

**Short story scenario:**  
You edit a file called `notes.txt` to add some new information. When you open GitHub Desktop, you see `notes.txt` listed under `Changes`. You check the box next to it to stage it, then write a commit message like "Add class notes". You click `Commit to main` to save this snapshot locally. Finally, you click `Push origin` to upload your changes to GitHub, so your work is backed up and visible to others.

If you ever feel lost, ask yourself: *"Am I editing? staging? committing? or syncing?"*

---

## Everyday Workflow in GitHub Desktop
1. **Fetch/Pull first** – Click `Fetch origin`, then `Pull` if it appears. Start from the latest version to avoid conflicts.
2. **Work on files** – Use your editor. Save often.
3. **Review changes** – Switch to GitHub Desktop. The `Changes` tab lists modified files.
4. **Stage intentionally** – By default, changed files are **checked** to be included. Uncheck anything that isn’t ready so it’s not included in this commit.
5. **Write a clear summary** – Use the Summary box with a verb + topic ("Add lab instructions"). Optional description for details.  
   If all listed changes belong together, you can commit them at once; otherwise make separate, focused commits.
6. **Commit to main (or current branch)** – Hit the commit button.
7. **Push to GitHub** – Click `Push origin` to back up your work online.
8. **Repeat** – Small, frequent commits make life easier.

---

## Commit Example Step by Step
Imagine you add instructions to `README.md` and a screenshot `images/setup.png`.

1. **After editing**
   - GitHub Desktop shows both files under `Changes`.

2. **Stage the right files**
   - Leave both checked because they belong together.

3. **Check the diff**
   - Click each file to preview the green additions and red removals.

4. **Write your message**
   - Summary: `Add setup guide section`
   - Description: `Document installation steps and include setup screenshot.` (optional)

5. **Commit**
   - Click `Commit to main`. The snapshot is stored locally.

6. **Push**
   - Click `Push origin` so GitHub has the same history.

**What it looks like in the timeline**
```
main branch history (newest on top)
┌──────────────────────────────────────────┐
│Add setup guide section   ← your commit   │
├──────────────────────────────────────────┤
│Create starter files                      │
├──────────────────────────────────────────┤
│Initial commit                            │
└──────────────────────────────────────────┘
```

---

**Second example:**  
You edit two unrelated files: `README.md` and `notes.txt`. You want to keep your commits focused, so you:

- Stage and commit `README.md` first with the message: `Update README with new instructions`.
- Then stage and commit `notes.txt` separately with the message: `Add class notes for week 2`.
- Push both commits to GitHub.

This way, your commit history stays clear and easy to understand.

---

## Syncing with GitHub (Push & Pull)
```
                 Push (upload commits)
Your computer ───────────────────────────► GitHub
     ▲                                        │
     │ Pull / Fetch (download commits)        │
     └────────────────────────────────────────┘
```
- **Push** when you want GitHub to have your latest commits.
- **Fetch** checks whether GitHub has new commits.
- **Pull** brings those new commits to your computer and merges them into your branch.

**Metaphor:**  
*Push* is like uploading your homework to turn it in. *Pull* is like downloading updated class notes from your teacher so you have the latest version.

Habit: *fetch + pull* before you start working, *push* after you commit.

---

## Branches Without Fear
Branches let you experiment without breaking the main timeline.

```
main:    o───o───o──┐
                    │
feature:            o──o──o
```

- `main` (or `master`) is the stable branch.
- Create a new branch in GitHub Desktop when trying a feature or fixing a bug.
- Commit on the branch. When ready, merge it into `main` via GitHub Desktop or a pull request on GitHub.

**Scenario:**  
You have an assignment due soon but want to try a new design idea without risking your current work. You create a branch called `design-experiment`, work there safely, and if it looks good, merge it back into `main`. If not, you can discard it without affecting your main assignment.

If branches sound advanced, remember: you can stick to `main` until you need them.

---

## Undoing Mistakes Safely
| Situation | GitHub Desktop option | What it does |
| --- | --- | --- |
| **Undo last commit (not pushed yet)** | In **History**, select the most recent commit and click **Undo** | Puts the commit’s changes back into **Changes** so you can edit and recommit. The button is unavailable if the commit was already pushed. |
| **Revert a specific commit** | In **History**, right‑click the commit → **Revert Changes in Commit** | Creates a new commit that reverses the selected commit without removing history. |
| **Reset to a commit** *(if available in your version)* | In **History**, right‑click a commit → **Reset to commit…** | Rewinds local history to that commit; intervening changes return to **Changes**. Does not affect the remote until you push. |
| **Discard uncommitted file changes** | In **Changes**, right‑click a file → **Discard changes…** (or menu: **Branch → Discard all changes…**) | Reverts file(s) to the last commit. **Destructive** — usually cannot be undone. |
| **Recover a deleted/overwritten file** | Open **History**, select a prior commit, click the file in the diff and copy its contents back | Restores content from a previous snapshot.

**What to do if you panic:**  
Don’t rush to discard changes or delete branches. Instead, commit your current work (even if incomplete), push it to GitHub, and ask for help from a teammate or instructor. Having your work saved remotely means you can always recover it.

---

## Assignment/Project Checklist
- Pull latest work from GitHub before editing.
- Create a branch if working on something risky or long-running.
- Make small, focused commits (one idea per commit) with clear messages.
- Push at the end of each work session or milestone.
- Verify your repository on GitHub before deadlines.
- **Important:** Always push BEFORE the deadline (e.g., before October 10) so the latest work is visible on GitHub.

---

## Try It Yourself
1. Create a practice repository.
2. Open it in GitHub Desktop.
3. Add a new text file called `practice.txt` with a sentence.
4. Commit with the message `Add practice note`.
5. Change the sentence, commit again.
6. View the `History` tab to compare commits.
7. Try `Fetch origin` and `Push origin` to see the sync steps.
8. **Variation:** Create a second file called `practice2.txt` and commit it separately with a clear message like `Add second practice file`.

---

## Quick Reference

- 🔄 **Before coding**: `Fetch origin` → ⬇️ `Pull`  

- ✍️ **After coding**: review `Changes` → write commit message → ✅ `Commit` → ⬆️ `Push origin`  
  - If all changes belong together, commit once.  
  - If they are unrelated, split into multiple focused commits.  

- ✅ **Undo commit**: available only for the latest local commit if it hasn’t been pushed yet (button appears in **Changes**)  
  *(Use if you want to re-edit your last commit before sharing it)*

- 🌀 **Revert commit**: in **History**, right‑click a past commit → *Revert Changes in Commit*  
  *(Creates a new commit that cancels the selected one without deleting history)*

- ⏪ **Reset to commit** *(if available)*: in **History**, right‑click → *Reset to commit…*  
  *(Moves your branch back locally; changes come back into **Changes**)  

- 💥 **Discard changes**: in **Changes**, right‑click file → *Discard changes…*  
  *(Resets file to last commit; destructive — no undo!)*

- ⬆️ **Need backup**: always Push to GitHub.  
- 🔙 **Need older version**: browse **History** and open past commits.

Keep this guide nearby while you work. With a few repetitions, the Git language will feel natural.
