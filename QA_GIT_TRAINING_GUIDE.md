# Git for QA Automation Engineers - Practical Training Guide

## Quick Start (TL;DR)

If you just need to remember the workflow, here it is:

```powershell
# 1. Get latest main
git switch main
git pull origin main

# 2. Create feature branch
git branch feature/your-feature-name
git switch feature/your-feature-name

# 3. Work - edit files, save
code your_file.md

# 4. Save your work locally
git add .
git commit -m "Clear message about what you did"

# 5. Send to GitHub
git push -u origin feature/your-feature-name

# 6. Create Pull Request on GitHub website
# (Team reviews it)

# 7. Merge on GitHub, then cleanup locally
git switch main
git pull origin main
git branch -d feature/your-feature-name
```

---

## Table of Contents

1. [What is Git? (For QA Engineers)](#what-is-git)
2. [Essential Commands Explained](#essential-commands)
3. [Real QA Workflow](#real-workflow)
4. [Common Tasks with Steps](#common-tasks)
5. [Understanding Diffs](#understanding-diffs)
6. [Troubleshooting](#troubleshooting)
7. [Quick Reference](#quick-reference)

---

## What is Git? (For QA Engineers) {#what-is-git}

### Simple Definition
Git is a **time machine for your code**. Every time you save your work, Git remembers it. You can see who changed what, when, and why.

### Why QA Engineers Need Git

- **Track test case changes** - Know which version of tests were used
- **Collaborate without conflicts** - Multiple QAs working on different features
- **Get feedback before merging** - Pull Requests let team review your tests
- **Revert mistakes** - Go back to working code if something breaks
- **See test history** - Understand why a test was written

### Git vs GitHub

| Git | GitHub |
|-----|--------|
| Software on your computer | Website/server |
| Tracks changes locally | Stores code online |
| Works offline | Needs internet |
| Your private workspace | Team collaboration space |

---

## Essential Commands Explained {#essential-commands}

### 1. `git init` - Start Tracking a Project

**When:** First time setting up a project on your computer

```powershell
git init
```

**What it does:** Creates a hidden `.git` folder that tracks everything.

**Real scenario:** You got a new test project. Run this once to start tracking.

---

### 2. `git config` - Tell Git Who You Are

**When:** First time using Git (one-time setup)

```powershell
git config --global user.name "Marina Haniseuskaya"
git config --global user.email "m.haniseuskaya@company.com"
```

**What it does:** Sets your name/email so Git knows who made changes.

**Verify it worked:**
```powershell
git config --list
```

---

### 3. `git branch` - Create Separate Workspaces

**When:** Starting work on a new feature/test

```powershell
# See all branches
git branch

# Create new branch
git branch feature/payment-tests

# Create and switch (shortcut)
git checkout -b feature/payment-tests
```

**What it does:** Creates an isolated copy of the code where you work without affecting others.

**Branch naming convention (QA):**
- `feature/feature-name` - New feature tests
- `bugfix/bug-name` - Test cases for bug verification
- `hotfix/issue-name` - Urgent fixes

**Real scenario:** You need to write tests for the "Forgot Password" feature. Create branch `feature/forgot-password-tests`.

---

### 4. `git switch` / `git checkout` - Move Between Branches

**When:** You need to work on a different branch

```powershell
# Modern way (git switch)
git switch feature/payment-tests

# Old way (git checkout) - still works
git checkout feature/payment-tests
```

**What it does:** Changes your workspace to a different branch.

**Real scenario:** You're done with payment tests. Switch to main: `git switch main`

---

### 5. `git add` - Stage Files for Saving

**When:** You edited files and want to prepare them for saving

```powershell
# Add specific file
git add login_tests.md

# Add all changed files
git add .
```

**What it does:** Tells Git "I want to save these files in my next commit."

**Real scenario:** You added 3 new test cases. Use `git add .` to prepare all of them.

---

### 6. `git commit` - Save with a Message

**When:** After staging files, you want to save with a description

```powershell
git commit -m "Add payment test cases for credit card validation"
```

**What it does:** Creates a snapshot with a timestamp and message. Your team knows what changed.

**Good commit messages (QA):**
- ✅ `"Add test cases for login feature"`
- ✅ `"Fix test assertion for email validation"`
- ✅ `"Add edge case tests for zero amount payment"`
- ❌ `"update stuff"`
- ❌ `"testing"`

**Real scenario:** You finished writing 4 new test cases. Commit with clear message so teammates understand.

---

### 7. `git push` - Send to GitHub

**When:** You finished work on a branch and want teammates to see it

```powershell
# First time pushing this branch
git push -u origin feature/payment-tests

# After that, just:
git push
```

**What it does:** Uploads your commits to GitHub so others can see and review them.

**Real scenario:** You finished payment tests. Push to GitHub. Your team lead gets a notification and reviews your code.

---

### 8. `git pull` - Get Latest Changes

**When:** Before starting new work or when teammates pushed updates

```powershell
# Get latest main
git pull origin main

# Or just
git pull
```

**What it does:** Downloads the latest code from GitHub to your computer.

**Real scenario:** A developer fixed a bug. You need the latest code. Use `git pull` to get it.

---

### 9. `git status` - Check Current State

**When:** You want to see what changed

```powershell
git status
```

**What it does:** Shows which branch you're on, what files changed, what's staged.

**Real scenario:** You made changes. Use `git status` to see what you need to add/commit.

---

### 10. `git log` - View History

**When:** You want to see previous commits

```powershell
# See all commits (one per line)
git log --oneline

# See detailed info
git log

# Exit with 'q'
```

**What it does:** Shows all your saved work with timestamps and messages.

**Real scenario:** You need to know when a test case was added. Check `git log`.

---

### 11. `git diff` - See What Changed

**When:** You want to see exact changes before committing

```powershell
# See changes not yet committed
git diff

# See changes in a specific file
git diff login_tests.md
```

**What it does:** Shows exactly what lines were added (+) and deleted (-).

**Real scenario:** You edited a test case. Use `git diff` to verify your changes before committing.

---

### 12. `git remote add` - Connect to GitHub (One-Time)

**When:** First time connecting local project to GitHub

```powershell
git remote add origin https://github.com/your-username/your-repo.git
```

**What it does:** Tells Git where your GitHub repository is.

**Real scenario:** You created a new repo on GitHub. Run this once to connect locally.

---

## Real QA Workflow {#real-workflow}

### Complete Workflow: From Start to Finish

#### Scenario
Your team lead assigns: "Create test cases for User Login feature"

#### Step 1: Prepare Main (5 minutes)

```powershell
# Make sure you're on main
git switch main

# Get latest code from GitHub
git pull origin main
```

✅ You're ready to start work

#### Step 2: Create Feature Branch (1 minute)

```powershell
# Create branch for this feature
git branch feature/login-tests

# Switch to your branch
git switch feature/login-tests

# Verify you're on it
git branch
```

**Output:**
```
* feature/login-tests
  main
```

✅ Branch created

#### Step 3: Create Test File (10 minutes)

```powershell
# Open VS Code to create/edit file
code login_tests.md
```

**Add your test cases in VS Code:**
```
# Login Feature - Test Cases

## Test Case 1: Valid Login
- Input: username="user1", password="correct"
- Expected: User logged in, dashboard shown
- Priority: High
- Status: Ready for automation

## Test Case 2: Invalid Password
- Input: username="user1", password="wrong"
- Expected: Error "Invalid credentials"
- Priority: High
- Status: Ready for automation
```

Save (Ctrl + S) and close VS Code.

✅ File created with test cases

#### Step 4: Check What Changed (2 minutes)

```powershell
# See what you changed
git status

# See exact changes
git diff
```

**Output:**
```
On branch feature/login-tests

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        login_tests.md
```

✅ Git sees your new file

#### Step 5: Stage Your Work (1 minute)

```powershell
# Add all changes
git add .
```

**Verify:**
```powershell
git status
```

**Output:**
```
On branch feature/login-tests

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   login_tests.md
```

✅ File is staged

#### Step 6: Commit (1 minute)

```powershell
# Save with a message
git commit -m "Add login feature test cases"
```

**Output:**
```
[feature/login-tests abc1234] Add login feature test cases
 1 file changed, 12 insertions(+)
 create mode 100644 login_tests.md
```

✅ Saved locally

#### Step 7: Push to GitHub (1 minute)

```powershell
# Send to GitHub
git push -u origin feature/login-tests
```

**Output:**
```
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Create a pull request for 'feature/login-tests' on GitHub by visiting:
remote:   https://github.com/your-username/repo/pull/new/feature/login-tests
```

✅ Your work is on GitHub!

#### Step 8: Create Pull Request on GitHub (3 minutes)

1. Go to your GitHub repository
2. Click "Pull requests" tab
3. Click "New pull request"
4. Set Base: `main`, Compare: `feature/login-tests`
5. Click "Create pull request"
6. Add title: `Add login feature test cases`
7. Add description:
   ```
   ## Summary
   Test cases for login functionality
   
   ## Test Cases Added
   - Valid login scenario
   - Invalid password handling
   
   ## Ready for: Automation development
   ```
8. Click "Create pull request"

✅ PR created for review

#### Step 9: Team Reviews (varies)

Your team lead reviews the PR and either:
- **Approves** → You merge
- **Requests changes** → You make changes and push (PR updates automatically)

#### Step 10: Merge to Main (2 minutes)

On GitHub PR page:
1. Click "Merge pull request"
2. Click "Confirm merge"

**Output:**
```
Pull request successfully merged and closed
```

✅ Your code is now in main!

#### Step 11: Cleanup (2 minutes)

```powershell
# Switch to main
git switch main

# Get latest (includes your merged code)
git pull origin main

# Delete the feature branch locally
git branch -d feature/login-tests

# Verify
git branch
```

**Output:**
```
* main
```

✅ Workspace clean, ready for next task

---

## Common Tasks with Steps {#common-tasks}

### Task 1: I Need to Make Changes to an Existing Test Case

```powershell
# Make sure main is updated
git switch main
git pull origin main

# Create feature branch
git branch feature/update-login-tests
git switch feature/update-login-tests

# Edit the file
code login_tests.md

# View changes
git diff

# Commit
git add .
git commit -m "Update login test cases with new validation rules"

# Push
git push -u origin feature/update-login-tests

# Create PR on GitHub
# → Merge after review
# → Delete branch
```

### Task 2: I Need to See What a Teammate Changed

```powershell
# Make sure main is updated
git switch main
git pull origin main

# Their changes are now in main
# Open the file to see what changed
code test_file.md

# Or see history
git log --oneline
```

### Task 3: I Made a Mistake in a Commit Message

```powershell
# If not pushed yet
git commit --amend -m "New correct message"
git push -u origin feature/branch-name

# If already pushed
# Just create another commit with correct message
# Mention in PR: "Previous commit message had typo"
```

### Task 4: I Committed to Main by Mistake (Happens to Everyone!)

```powershell
# See what you committed
git log --oneline

# Create a branch from where you are
git branch feature/fix-name

# Move main back to where it should be
git switch main
git reset --hard origin/main

# Now your work is safe in the feature branch
git switch feature/fix-name
```

### Task 5: I Need to Cancel My Uncommitted Changes

```powershell
# See what changed
git status

# Discard changes to a file
git restore login_tests.md

# Or discard ALL changes
git restore .
```

---

## Understanding Diffs {#understanding-diffs}

### What is a Diff?

A diff shows exactly what changed in your code:
- `+` lines (green) = Added
- `-` lines (red) = Deleted
- No symbol (white) = Unchanged context

### Real Example from a PR

```diff
# Login Feature Test Cases

## Test Case 1: Valid Login
- Input: username="user1", password="pass123"
- Expected: User logged in
+ Expected: User logged in successfully, dashboard shown
- Status: Pending

## Test Case 2: Invalid Password
- Input: username="user1", password="wrong"
- Expected: Error "Invalid credentials"
  Status: Ready for automation

+ ## Test Case 3: Empty Username
+ - Input: username="", password="pass123"
+ - Expected: Error "Username required"
+ - Status: Ready for automation
```

**What changed:**
1. Line 6: Updated expected result description
2. Line 8: Removed "Pending" status
3. Lines 13-16: Added new test case

### How to Read a Diff in GitHub

1. Go to your PR
2. Click "Files changed" tab
3. Look for green `+` (additions) and red `-` (deletions)
4. Scroll through to understand what you added/changed
5. Click on lines to leave comments

### Why Diffs Matter for QA

- **During review:** You can see what tests teammates added
- **Before merging:** Verify changes are correct
- **Documentation:** Every change is documented with context
- **Debugging:** If tests break, diffs show what changed

---

## Troubleshooting {#troubleshooting}

### Problem: "fatal: not a git repository"

**Cause:** You're not in a Git project folder

**Solution:**
```powershell
# Navigate to your project folder
cd path/to/your/project

# Initialize Git (if new project)
git init

# Or clone existing project
git clone https://github.com/your-repo
```

### Problem: "Please commit your changes or stash them before you switch branches"

**Cause:** You have uncommitted changes and tried to switch branches

**Solution:**
```powershell
# Option 1: Commit your changes
git add .
git commit -m "Save work in progress"

# Option 2: Discard changes (if you don't need them)
git restore .
```

### Problem: "Everything up-to-date" when pushing

**Cause:** You already pushed this code

**Solution:** This isn't an error! Your code is already on GitHub.

### Problem: Merge Conflicts (when pulling)

**Cause:** Multiple people edited the same file

**Solution:**
```powershell
# Check which files have conflicts
git status

# Open the file and look for conflict markers:
# <<<<<<<
# your changes
# =======
# their changes
# >>>>>>>

# Edit to keep what you want
# Then commit
git add .
git commit -m "Resolve merge conflict in login_tests.md"
```

### Problem: "Permission denied" when pushing

**Cause:** Git can't authenticate to GitHub

**Solution:**
```powershell
# Set up SSH or Personal Access Token
# (Ask your team IT or GitHub docs for details)
```

### Problem: Accidentally Deleted Local Branch

**Cause:** Used `git branch -D` instead of checking out first

**Solution:**
```powershell
# It's probably still on GitHub
git branch feature/branch-name origin/feature/branch-name

# Or pull from GitHub
git fetch origin
git checkout feature/branch-name
```

---

## Quick Reference {#quick-reference}

### Command Cheat Sheet

| Task | Command |
|------|---------|
| Check current branch | `git branch` |
| Create branch | `git branch feature/name` |
| Switch branch | `git switch branch-name` |
| See changes | `git diff` |
| Stage files | `git add .` |
| Save locally | `git commit -m "message"` |
| Send to GitHub | `git push` |
| Get latest | `git pull origin main` |
| See history | `git log --oneline` |
| Check status | `git status` |
| Delete branch | `git branch -d feature/name` |
| Discard changes | `git restore .` |

### Daily QA Workflow (Quick)

```
1. git switch main
2. git pull origin main
3. git branch feature/your-feature
4. git switch feature/your-feature
5. (edit files)
6. git add .
7. git commit -m "message"
8. git push -u origin feature/your-feature
9. (create PR on GitHub)
10. (merge on GitHub)
11. git switch main
12. git pull origin main
13. git branch -d feature/your-feature
```

### Branch Naming Examples (QA)

```
feature/login-tests
feature/payment-validation
feature/user-profile-update
bugfix/fix-email-test-assertion
hotfix/critical-test-failure
```

### Good Commit Messages

✅ `"Add test cases for payment validation"`
✅ `"Fix email validation test assertion"`
✅ `"Add edge case tests for zero amount"`
✅ `"Update login test for new password rules"`

❌ `"changes"`
❌ `"fix"`
❌ `"testing"`
❌ `"asdf"`

---

## Tips for QA Engineers

1. **Always start with `git pull main`** - Ensures you have latest code
2. **Create one branch per task** - Don't mix features
3. **Commit frequently** - Better to have many small commits than one huge one
4. **Write clear commit messages** - Future you will thank you
5. **Review your own diff first** - Before asking teammates to review
6. **Ask for help early** - Git problems are easier to fix early
7. **Delete branches after merging** - Keeps repository clean
8. **Never force push** - Unless you know exactly what you're doing
9. **Test locally before pushing** - Run your tests to make sure they work
10. **Wait for approval before merging** - Don't rush PR reviews

---

## Final Reminders

- **Git is your safety net** - You can't lose your work if it's committed
- **GitHub is collaboration** - Always push and let teammates review
- **Branches are your friends** - Use them to experiment without risk
- **Commits are documentation** - Good messages help the whole team
- **PRs are learning opportunities** - Code review improves everyone

---

## Need More Help?

- **GitHub Docs:** https://docs.github.com
- **Git Documentation:** https://git-scm.com/doc
- **Ask Your Team:** Your QA team has used this - ask them!

---

**Version 1.0 | For QA Automation Engineers | Practical Reference**
