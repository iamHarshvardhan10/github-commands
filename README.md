# 📘 Git & GitHub — Complete Reference Guide

> A comprehensive cheat sheet with descriptions for every command, plus a full team workflow guide for collaborating on GitHub.

---

## 📑 Table of Contents

### Part 1 — Command Reference
- [Getting & Creating Projects](#1-getting--creating-projects)
- [Basic Snapshotting](#2-basic-snapshotting)
- [Branching & Merging](#3-branching--merging)
- [Sharing & Updating Projects](#4-sharing--updating-projects)
- [Inspection & Comparison](#5-inspection--comparison)

### Part 2 — Team Workflow Guide
- [The Workflow at a Glance](#-the-team-workflow-at-a-glance)
- [Phase 1 — Set Up](#phase-1--set-up--join-the-project)
- [Phase 2 — Start Working](#phase-2--start-working--before-every-task)
- [Phase 3 — Code & Commit](#phase-3--code--commit--while-you-work)
- [Phase 4 — Push to GitHub](#phase-4--share-your-work--push-to-github)
- [Phase 5 — Pull Request](#phase-5--pull-request--get-your-code-reviewed)
- [Phase 6 — Merge & Clean Up](#phase-6--merge--clean-up)
- [Phase 7 — Handling Conflicts](#phase-7--handling-merge-conflicts)
- [Quick Reference Tables](#-quick-reference--commands-by-scenario)
- [Golden Rules](#-golden-rules-for-team-git)

---

# Part 1 — Command Reference

## 1. Getting & Creating Projects

| Command | Syntax | Description |
|--------|--------|-------------|
| `git init` | `git init` | Initializes a new empty Git repository in the current directory. Creates a hidden `.git` folder that tracks all version history and configuration for the project. |
| `git clone` | `git clone ssh://git@github.com/[username]/[repo].git` | Creates a full local copy of a remote repository, including all branches, commits, and history. The cloned repo is automatically linked to the original (origin). |

---

## 2. Basic Snapshotting

| Command | Syntax | Description |
|--------|--------|-------------|
| `git status` | `git status` | Displays the state of the working directory and staging area. Shows which files are modified, staged for commit, or untracked — helps you understand what will go into your next commit. |
| `git add [file]` | `git add [file-name.txt]` | Stages a specific file, adding its changes to the index so they're included in the next commit. Only staged changes are committed. |
| `git add -A` | `git add -A` | Stages ALL changes at once — new files, modifications, and deletions — from the entire working directory. Useful for committing all pending work in one step. |
| `git commit` | `git commit -m "[message]"` | Records a snapshot of the staged changes to the repository history. The `-m` flag lets you write an inline commit message describing what changed and why. |
| `git rm` | `git rm -r [file-name.txt]` | Removes a file (or folder with `-r`) from both the working directory and the staging area. The deletion will be recorded in the next commit. |
| `git remote -v` | `git remote -v` | Lists all remote connections associated with your local repository, showing their names and URLs. Helps verify which remote servers your project is connected to. |

---

## 3. Branching & Merging

| Command | Syntax | Description |
|--------|--------|-------------|
| `git branch` | `git branch` | Lists all local branches. The currently active branch is marked with an asterisk (`*`). Useful for reviewing your branching structure. |
| `git branch -a` | `git branch -a` | Lists all branches — both local and remote-tracking. Gives a complete picture of all available branches across the repository. |
| `git branch [name]` | `git branch [branch name]` | Creates a new branch at the current commit without switching to it. Branches allow you to develop features or fixes in isolation from the main codebase. |
| `git branch -d` | `git branch -d [branch name]` | Safely deletes a local branch. Git will refuse to delete it if it has unmerged changes, protecting you from accidental data loss. |
| `git push --delete` | `git push origin --delete [branch name]` | Deletes a branch from the remote repository. Useful for cleaning up after a feature branch has been merged. |
| `git checkout -b` | `git checkout -b [branch name]` | Creates a new branch AND immediately switches to it in one step. This is the most common way to start working on a new feature. |
| `git checkout -b [origin]` | `git checkout -b [branch] origin/[branch]` | Creates a local branch that tracks a specific remote branch, then switches to it. Useful for working on an existing remote feature branch. |
| `git branch -m` | `git branch -m [old name] [new name]` | Renames a local branch. Does not affect the remote — you'll need to push and delete the old remote branch separately. |
| `git checkout [name]` | `git checkout [branch name]` | Switches your working directory to the specified branch. Any uncommitted changes may need to be stashed first. |
| `git checkout -` | `git checkout -` | Quickly toggles back to the previously checked-out branch. Handy when switching back and forth between two branches. |
| `git checkout --` | `git checkout -- [file-name.txt]` | Discards all uncommitted changes to a specific file, restoring it to its last committed state. ⚠️ This is irreversible — use with caution. |
| `git merge [branch]` | `git merge [branch name]` | Merges the specified branch into the currently active branch. Incorporates all commits from that branch into your current one. |
| `git merge [src→tgt]` | `git merge [source branch] [target branch]` | Merges a source branch into a target branch explicitly. This makes the target explicit, rather than relying on the current checkout. |
| `git stash` | `git stash` | Temporarily saves your uncommitted changes to a stack, leaving a clean working directory. Great for quickly switching context without losing work. |
| `git stash clear` | `git stash clear` | Permanently removes all entries from the stash stack. Use this to clean up after you no longer need the saved states. |
| `git stash pop` | `git stash pop` | Applies the most recently stashed changes back to your working directory and removes them from the stash stack. |

---

## 4. Sharing & Updating Projects

| Command | Syntax | Description |
|--------|--------|-------------|
| `git push origin` | `git push origin [branch name]` | Uploads the specified local branch and its commits to the remote repository. Does not set up tracking — you'll need to specify the branch each time. |
| `git push -u` | `git push -u origin [branch name]` | Pushes to the remote and sets the upstream tracking reference so future `git push` and `git pull` commands work without arguments. |
| `git push` | `git push` | Pushes commits on the current branch to its configured upstream remote branch. Only works if tracking is already set up. |
| `git push --delete` | `git push origin --delete [branch name]` | Removes the specified branch from the remote repository. Useful for cleaning up merged or abandoned remote feature branches. |
| `git pull` | `git pull` | Fetches the latest changes from the remote and merges them into your current local branch. Combines `git fetch` and `git merge` in one step. |
| `git pull origin` | `git pull origin [branch name]` | Explicitly pulls changes from the specified remote branch into your current local branch. Useful when pulling from a branch other than the default. |
| `git remote add` | `git remote add origin ssh://git@github.com/[user]/[repo].git` | Links your local repository to a remote server by adding a named remote (usually `origin`). Required to push or pull from a new remote location. |
| `git remote set-url` | `git remote set-url origin ssh://git@github.com/[user]/[repo].git` | Updates the URL of an existing remote (e.g., switching from HTTPS to SSH). Useful for re-authenticating or migrating to a new server. |

---

## 5. Inspection & Comparison

| Command | Syntax | Description |
|--------|--------|-------------|
| `git log` | `git log` | Displays the full commit history of the current branch, showing commit hashes, authors, dates, and messages. Scroll with arrow keys; press `Q` to exit. |
| `git log --summary` | `git log --summary` | Shows the commit log with additional detail, including which files were added, modified, or deleted in each commit. Great for understanding the scope of changes. |
| `git log --oneline` | `git log --oneline` | Outputs a compact, single-line-per-commit view of the commit history, showing just the short hash and message. Ideal for a quick overview of recent activity. |
| `git diff` | `git diff [source branch] [target branch]` | Compares the differences between two branches, showing exactly which lines were added or removed. Useful for reviewing changes before performing a merge. |

> 💡 **Tip:** Use `git help [command]` in your terminal to get the official manual page for any command.

---

---

# Part 2 — Team Workflow Guide

> Everything your team needs to collaborate safely and efficiently on GitHub.

> 📌 **How This Guide Works:** Follow each Phase in order. Every phase has steps with exact commands to type, tips, and warnings. Use the Quick-Reference tables at the bottom to look up commands at a glance.

---

## 🗺 The Team Workflow at a Glance

```
1. Clone / Pull  →  2. Create Branch  →  3. Code & Commit  →  4. Push Branch  →  5. Pull Request  →  6. Review & Merge
```

---

## Phase 1 — Set Up / Join the Project

> Done **once** when you first join a team repository.

### Step 1 — Clone the Repository to Your Computer

Get the SSH URL from the GitHub repo page (green **Code** button → SSH tab), then run:

```bash
git clone git@github.com:your-org/project-name.git   # downloads the whole repo
cd project-name                                        # move into the folder
```

> 💡 Use SSH (not HTTPS) so you never have to type a password again. Make sure you have added your SSH key to GitHub first.

### Step 2 — Verify Your Remote Connection

Confirm that your local repo is linked to the correct remote repository.

```bash
git remote -v   # should show origin pointing to your repo
```

You should see `origin` listed with the fetch and push URLs. If it is blank, you skipped the clone step.

### Step 3 — Configure Your Identity

Set your name and email so every commit is attributed correctly. This is a **one-time global setup**.

```bash
git config --global user.name "Your Name"
git config --global user.email "you@company.com"
```

> ⚠️ Commits with the wrong email will not link to your GitHub profile. Use the same email as your GitHub account.

---

## Phase 2 — Start Working / Before Every Task

> Run these **every time** you pick up a new task or ticket.

### Step 1 — Always Start From the Latest `main`

Before creating any branch, make sure your local `main` is up to date with the team's remote.

```bash
git checkout main          # switch to main branch
git pull origin main       # download latest team changes
```

> ⚠️ Never skip this step. Starting from stale code causes painful merge conflicts later.

### Step 2 — Create a New Feature Branch

Each task gets its own branch. Use a clear naming convention so teammates understand what you are working on.

```bash
git checkout -b feature/login-page   # create + switch to new branch
```

**Naming conventions your team should agree on:**

| Prefix | Purpose |
|--------|---------|
| `feature/` | New functionality |
| `bugfix/` | Fixing a bug |
| `hotfix/` | Urgent production fix |
| `chore/` | Config, docs, cleanup |

> 💡 Include your ticket number for traceability: `feature/PROJ-42-login-page`

### Step 3 — Confirm You Are on the Right Branch

Before writing any code, double-check which branch is active.

```bash
git branch    # asterisk (*) shows active branch
git status    # also shows current branch + file status
```

---

## Phase 3 — Code & Commit / While You Work

> 🔁 **The Core Loop:** Edit files → `git add` → `git commit` → Repeat. Commit small and often — do not wait until you are done.

### Step 1 — Check What You Have Changed

Before staging anything, see exactly what has changed in your working directory.

```bash
git status          # overview: modified, untracked, staged files
git diff            # see exact line-by-line changes (unstaged)
git diff --staged   # see changes already staged for commit
```

### Step 2 — Stage Your Changes

Add only the files relevant to this commit. Do not bundle unrelated changes together.

```bash
git add src/login.js   # stage a specific file
git add src/           # stage an entire folder
git add -A             # stage ALL changes (use carefully)
```

> ⚠️ Avoid `git add -A` blindly — you might accidentally stage debug logs, `.env` files, or build output. Check `.gitignore` is set up first.

### Step 3 — Commit With a Clear Message

A good commit message explains **WHAT** changed and **WHY**, not how.

```bash
git commit -m "feat: add email validation to login form"
```

**Follow the Conventional Commits format:**

| Prefix | When to Use |
|--------|------------|
| `feat:` | New feature |
| `fix:` | Bug fix |
| `docs:` | Documentation only |
| `refactor:` | Code restructure, no behaviour change |
| `test:` | Adding or fixing tests |

> 💡 Commit every time you finish a small, working piece. Each commit should pass tests on its own.

### Step 4 — Need to Undo? Here Is How

```bash
git restore [file]                      # discard unstaged changes to a file
git restore --staged [file]             # unstage a file (keep changes)
git commit --amend -m "new message"     # fix the last commit message
```

> ⚠️ Never use `git reset --hard` or `git push --force` on shared branches (`main`, `develop`). Only use force-push on your own personal branches.

---

## Phase 4 — Share Your Work / Push to GitHub

> Send your branch to the remote so the team can see it.

### Step 1 — Push Your Branch to GitHub

The first time you push a new branch, use `-u` to set the upstream tracking.

```bash
git push -u origin feature/login-page   # first push of this branch
git push                                 # all subsequent pushes (tracking already set)
```

> 💡 Push regularly — even before the feature is done — so your work is backed up and teammates can see your progress.

### Step 2 — Stay In Sync With the Team

While you are working, others are merging code into `main`. Pull their updates into your branch regularly to avoid a giant merge conflict at the end.

```bash
git checkout main
git pull origin main                   # get latest team changes
git checkout feature/login-page
git merge main                         # bring those changes into your branch
```

> ⚠️ Do this at least once a day, especially before opening a Pull Request.

---

## Phase 5 — Pull Request / Get Your Code Reviewed

> Request that your branch be merged into `main`.

### Step 1 — Open a Pull Request on GitHub

After pushing, go to your repository on github.com. GitHub will show a yellow banner offering to create a PR — click it, or go to **Pull Requests → New Pull Request**.

**Fill in your PR with:**
- A clear title summarising the change
- A description: what changed, why, and how to test it
- Link to the related ticket/issue if applicable
- Assign at least one reviewer from your team

> 💡 Keep PRs small (under 400 lines changed). Large PRs get poor reviews. Split big features into multiple PRs.

### Step 2 — Respond to Review Comments

Reviewers will leave comments. For each requested change:

1. Make the fix in your local branch
2. Stage and commit the change
3. Push — the PR updates automatically

```bash
git add [file]
git commit -m "fix: address review comment on validation"
git push   # PR auto-updates on GitHub
```

> 💡 Reply to each comment on GitHub to let reviewers know you addressed it. Mark threads as resolved once fixed.

---

## Phase 6 — Merge & Clean Up

> After the PR is approved.

### Step 1 — Merge the Pull Request

Once approved, merge on GitHub using the green **Merge pull request** button. Use **Squash and merge** if your team wants a clean, single-commit history per feature.

> ⚠️ Do NOT merge your own PR unless your team policy allows it. Always wait for at least one approval.

### Step 2 — Update Your Local `main`

After the merge, bring your local machine up to date.

```bash
git checkout main
git pull origin main   # now includes your merged feature
```

### Step 3 — Delete the Feature Branch

Clean up stale branches — they pile up fast on big teams.

```bash
git branch -d feature/login-page                   # delete local branch
git push origin --delete feature/login-page        # delete remote branch
```

> 💡 GitHub can auto-delete branches after merge. Enable this in **Settings → General → "Automatically delete head branches"**.

---

## Phase 7 — Handling Merge Conflicts

> What to do when Git cannot auto-merge.

> ⚡ **What is a conflict?** A conflict happens when two teammates edited the same lines of the same file. Git marks the conflicting sections with `<<<<<<<`, `=======`, and `>>>>>>>` markers. You must resolve them manually.

### Step 1 — Identify and Resolve Conflicts

When a merge fails, Git will tell you which files conflict. Open each one and look for the markers.

```bash
git status   # shows all conflicted files in red
```

Inside the conflicting file you will see:

```
<<<<<<< HEAD
your changes here
=======
teammate changes here
>>>>>>> main
```

Edit the file to keep the correct version (could be yours, theirs, or a blend of both). Delete all the marker lines when done.

### Step 2 — Mark as Resolved and Commit

After editing every conflicting file, stage them and commit.

```bash
git add [resolved-file.js]                             # mark each conflict resolved
git commit -m "merge: resolve conflict in login module"
```

> 💡 Use a merge tool like VS Code, IntelliJ, or `git mergetool` for a visual side-by-side view — much easier than editing raw markers.

---

## ⚡ Quick Reference — Commands by Scenario

### Daily Workflow

| Action | Command | When to Use |
|--------|---------|-------------|
| Check status | `git status` | See what files changed before staging |
| Pull latest code | `git pull origin main` | Every morning and before creating a branch |
| Create branch | `git checkout -b feature/name` | Start every new task on a fresh branch |
| Stage file | `git add [file]` | Select which changes go into the next commit |
| Commit | `git commit -m "type: message"` | Save a snapshot with a clear description |
| Push branch (first time) | `git push -u origin feature/name` | First push of a new branch |
| Push again | `git push` | Subsequent pushes once tracking is set |
| View history | `git log --oneline` | Quick overview of recent commits |

### Staying In Sync With Team

| Action | Command | When to Use |
|--------|---------|-------------|
| Update local main | `git pull origin main` | Fetch and merge latest team commits into main |
| Merge main into branch | `git merge main` | Bring team updates into your feature branch |
| See all branches | `git branch -a` | View local and remote branches |
| See remote info | `git remote -v` | Check which remote server you are connected to |
| Fetch without merging | `git fetch origin` | Download updates without applying them yet |
| Compare branches | `git diff main feature/name` | Preview what will change in a merge |

### Fixing Mistakes

| Action | Command | When to Use |
|--------|---------|-------------|
| Discard file changes | `git restore [file]` | Throw away unstaged edits to a file |
| Unstage a file | `git restore --staged [file]` | Remove from staging area, keep your edits |
| Fix last commit message | `git commit --amend -m "new msg"` | Only if you have not pushed yet |
| Stash work-in-progress | `git stash` | Temporarily save changes to switch context |
| Bring back stash | `git stash pop` | Restore the most recently stashed changes |
| See stash list | `git stash list` | View all stashed change sets |

### Branch Clean-Up

| Action | Command | When to Use |
|--------|---------|-------------|
| Delete local branch | `git branch -d feature/name` | Safe delete (warns if unmerged) |
| Delete remote branch | `git push origin --delete feature/name` | Remove branch from GitHub |
| Rename local branch | `git branch -m old-name new-name` | Rename without losing history |
| List merged branches | `git branch --merged` | Find branches safe to delete |

---

## 🏆 Golden Rules for Team Git

| | Rule |
|--|------|
| 🚫 | Never commit directly to `main` or `develop`. Always use a branch. |
| 🔄 | Pull from `main` every morning and before opening a Pull Request. |
| 📦 | Keep commits small and focused. One logical change per commit. |
| ✍️ | Write meaningful commit messages. Your future self will thank you. |
| 👀 | Review others' Pull Requests promptly — do not leave teammates blocked. |
| 🧹 | Delete branches after merge. A tidy repo is a happy repo. |
| 🔒 | Never force-push to shared branches. Talk to your team first. |
| 🔑 | Never commit secrets, passwords, or `.env` files. Add them to `.gitignore`. |

---

> 💡 **Tip:** Use `git help [command]` in your terminal to get the official manual page for any command.
