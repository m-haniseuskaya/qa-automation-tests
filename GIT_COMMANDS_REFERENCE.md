# Git Commands Reference for QA Automation Engineers
## Complete Guide with Real Scenarios

---

## TABLE OF CONTENTS
1. [Initial Setup](#1-initial-setup)
2. [Standard QA Workflow](#2-standard-qa-workflow)
3. [Branch Management](#3-branch-management)
4. [Viewing Information](#4-viewing-information)
5. [Committing & Pushing](#5-committing--pushing)
6. [Pulling & Syncing](#6-pulling--syncing)
7. [Fixing Mistakes](#7-fixing-mistakes-emergency-commands)
8. [Pull Request Workflow](#8-pull-request-workflow)
9. [Cleanup & Maintenance](#9-cleanup--maintenance)
10. [Advanced Scenarios](#10-advanced-scenarios)

---

# 1. INITIAL SETUP

## First Time Only - Configure Git

```powershell
# Set your name (one time)
git config --global user.name "Marina Haniseuskaya"

# Set your email (one time)
git config --global user.email "m.haniseuskaya@company.com"

# Verify configuration
git config --list
```

## Clone Repository

```powershell
# Clone with default folder name
git clone https://github.com/company/qa-tests.git

# Clone into specific folder
git clone https://github.com/company/qa-tests.git my-project

# Clone single branch (faster for large repos)
git clone --branch main --single-branch https://github.com/company/qa-tests.git
```

---

# 2. STANDARD QA WORKFLOW

## ⭐ RECOMMENDED WORKFLOW FOR EACH TASK

### Step 1: Prepare Main Branch
```powershell
# Make sure you're on main/master
git switch main

# Get latest changes from GitHub
git pull origin main

# Verify you're up to date
git status
# Output should be: "Your branch is up to date with 'origin/main'"
```

### Step 2: Create Feature Branch
```powershell
# Create and switch to new branch in one command
git switch -c feature/login-tests

# OR older way (still works)
git checkout -b feature/login-tests
```

### Step 3: Work on Your Tests
```powershell
# Create/edit test files
code login_tests.md

# Check what changed
git status

# See exact changes
git diff login_tests.md

# See all changes
git diff
```

### Step 4: Stage & Commit Changes
```powershell
# Stage specific file
git add login_tests.md

# Stage all changes
git add .

# Commit with clear message
git commit -m "Add login feature test cases"

# Verify commit was created
git log --oneline -1
```

### Step 5: Push to GitHub
```powershell
# First time pushing this branch (use -u flag)
git push -u origin feature/login-tests

# After that, just push
git push
```

### Step 6: Update Before PR (Important!)
```powershell
# Pull latest main into your feature branch
git pull origin main

# Resolve conflicts if any (see section 7)

# Push the merge
git push origin feature/login-tests
```

### Step 7: Create PR on GitHub
- Go to GitHub repository
- Click "Pull Requests" tab
- Click "New pull request"
- Base: main, Compare: feature/login-tests
- Add title and description
- Click "Create pull request"

### Step 8: After Merge - Cleanup
```powershell
# Switch to main
git switch main

# Pull merged changes
git pull origin main

# Delete feature branch locally
git branch -d feature/login-tests

# Delete on GitHub (optional, GitHub can auto-delete)
git push origin --delete feature/login-tests
```

---

# 3. BRANCH MANAGEMENT

## Create Branches

```powershell
# Create feature branch (for new tests)
git branch feature/payment-tests

# Create bugfix branch (for fixing tests)
git branch bugfix/fix-login-assertion

# Create hotfix branch (for urgent fixes)
git branch hotfix/critical-test-failure

# Create and switch in one command
git switch -c feature/new-tests
```

## Switch Between Branches

```powershell
# Switch to existing branch
git switch main

# Switch to branch and create if doesn't exist
git switch -c feature/new-tests

# Old way (still works)
git checkout main
git checkout -b feature/new-tests
```

## List Branches

```powershell
# List only local branches
git branch

# List with last commit info
git branch -v

# List with remote tracking info
git branch -vv

# List all branches (local + remote)
git branch -a

# List remote branches only
git branch -r
```

## Rename Branch

```powershell
# Rename current branch
git branch -m feature/old-name feature/new-name

# Rename specific branch
git branch -m feature/old-name feature/new-name

# If already pushed, also update remote
git push origin --delete feature/old-name
git push -u origin feature/new-name
```

## Delete Branches

```powershell
# Delete local branch (safe - won't delete if not merged)
git branch -d feature/login-tests

# Force delete local branch (dangerous!)
git branch -D feature/login-tests

# Delete branch on GitHub
git push origin --delete feature/login-tests

# Delete multiple branches
git branch -d feature/test1 feature/test2 feature/test3
```

---

# 4. VIEWING INFORMATION

## Check Current Status

```powershell
# See current branch, changed files, staged changes
git status

# Short status format
git status -s
```

## View Commit History

```powershell
# Last 3 commits (one line each)
git log --oneline -3

# All commits with details
git log

# Commits with diffs
git log -p

# Commits on this branch not in main
git log --oneline main..HEAD

# Commits since 2 days ago
git log --since="2 days ago"

# Commits by specific author
git log --author="Marina"

# Search commit messages
git log --grep="password reset"
```

## Compare Changes

```powershell
# Unstaged changes
git diff

# Changes in specific file
git diff password_reset_tests.md

# Staged changes
git diff --staged

# Diff between branches
git diff main feature/login-tests

# Diff between commits
git diff abc1234 def5678

# Show stats (how many lines changed)
git diff --stat
```

## Show Specific Commit

```powershell
# Show commit details
git show abc1234

# Show commit with diff
git show abc1234 --stat

# Show specific file in commit
git show abc1234:path/to/file.md
```

## Check Remote

```powershell
# Show remote repositories
git remote -v

# Show remote branch details
git ls-remote origin
```

---

# 5. COMMITTING & PUSHING

## Stage Files

```powershell
# Stage specific file
git add password_reset_tests.md

# Stage all changes in folder
git add tests/

# Stage all changes everywhere
git add .

# Stage part of file (interactive)
git add -p

# Unstage file (remove from staging)
git restore --staged password_reset_tests.md
```

## Commit Changes

```powershell
# Commit with message
git commit -m "Add password reset test cases"

# Commit with detailed message
git commit -m "Add password reset test cases" -m "Includes: valid email, invalid email, expired link"

# Amend last commit (fix message or add files)
git commit --amend -m "Fixed message"

# Amend without changing message
git commit --amend --no-edit

# See last commit
git show HEAD
```

## Push Changes

```powershell
# First time pushing new branch
git push -u origin feature/login-tests

# Regular push (after -u is set)
git push

# Push specific branch
git push origin feature/login-tests

# Push all branches
git push --all

# Delete remote branch
git push origin --delete feature/old-branch

# Force push (dangerous - only if you know what you're doing)
git push --force
```

---

# 6. PULLING & SYNCING

## Pull Latest Changes

```powershell
# Pull latest main branch
git pull origin main

# Pull current branch (if upstream set)
git pull

# Fetch without merging (just download)
git fetch

# Fetch all remotes
git fetch --all
```

## Update Feature Branch with Latest Main

```powershell
# While on your feature branch
git pull origin main

# This merges main INTO your branch
# Now your branch has both your work AND latest main code
```

## Sync Workflow Example

```powershell
# Make sure main is up to date
git switch main
git pull origin main

# Update feature branch
git switch feature/login-tests
git pull origin main

# Now feature branch has latest main + your work
git push
```

---

# 7. FIXING MISTAKES (EMERGENCY COMMANDS)

## ⚠️ Problem: Uncommitted Changes & Can't Switch Branches

```powershell
# Error: "Your local changes would be overwritten"

# Solution 1: Commit your changes (RECOMMENDED)
git add .
git commit -m "Save work in progress"
git switch other-branch

# Solution 2: Stash changes (save temporarily)
git stash
git switch other-branch
# Later, restore changes
git stash pop
```

## ⚠️ Problem: Changed File Before Committing

```powershell
# You edited file but haven't committed yet
# Want to undo changes

# Discard changes to specific file
git restore password_reset_tests.md

# Discard ALL changes (careful!)
git restore .

# See what you're about to discard
git diff password_reset_tests.md
```

## ⚠️ Problem: Staged File But Don't Want to Commit

```powershell
# You ran git add but haven't committed

# Unstage file
git restore --staged password_reset_tests.md

# Verify it's unstaged
git status
```

## ⚠️ Problem: Committed But Haven't Pushed

```powershell
# You committed locally but want to undo

# Option 1: Undo commit but keep changes (RECOMMENDED)
git reset --soft HEAD~1
# Changes go back to staging area
git status  # You'll see your changes staged

# Option 2: Undo commit and keep changes unstaged
git reset --mixed HEAD~1
# Changes stay but are unstaged
git status  # You'll see your changes unstaged

# Option 3: Undo commit and discard changes (DANGEROUS)
git reset --hard HEAD~1
# Your changes are GONE forever!
```

## ⚠️ Problem: Wrong Message in Last Commit (Not Pushed)

```powershell
# You committed with wrong message

# Fix it
git commit --amend -m "Correct message here"

# Verify
git log --oneline -1
```

## ⚠️ Problem: Committed to Wrong Branch (Not Pushed)

```powershell
# You made 3 commits on main but should be on feature branch
# Solution: Move commits to correct branch

# Create feature branch (includes your commits)
git branch feature/correct-branch

# Reset main to remote state
git reset --hard origin/main

# Switch to feature branch
git switch feature/correct-branch

# Now your commits are on correct branch!
```

## ⚠️ Problem: Committed to Main by Accident (Not Pushed)

```powershell
# You're on main and made commits that should be on feature branch

# See what you committed
git log --oneline -3

# Create feature branch from current state
git switch -c feature/my-work

# Go back to main
git switch main

# Reset main to what it should be
git reset --hard origin/main

# Check feature branch has your work
git switch feature/my-work
git log --oneline -3

# Now push feature branch
git push -u origin feature/my-work
```

## ⚠️ Problem: Merged Wrong Branch

```powershell
# You pulled/merged something you didn't mean to

# Undo the merge (if just happened)
git reset --hard HEAD~1

# Or revert the merge commit
git revert -m 1 HEAD
# This creates a NEW commit that undoes the merge
# Safer than reset because it keeps history
```

## ⚠️ Problem: Already Pushed Wrong Commits

```powershell
# You pushed commits to main that shouldn't be there
# IMPORTANT: Never force push to shared main branch!

# Solution 1: Create revert commit (RECOMMENDED for shared branches)
git revert abc1234
# This creates NEW commit that undoes the bad commit
git push

# Solution 2: If it's your feature branch, can force push
git push --force-with-lease
# Safer than --force, refuses to overwrite others' work
```

## ⚠️ Problem: Lost Commits / Undo Reset

```powershell
# You did git reset --hard and lost commits
# Don't worry, they're in reflog!

# See all recent actions
git reflog

# Restore to specific point
git reset --hard abc1234

# Example reflog output:
# abc1234 HEAD@{0}: reset: moving to HEAD~1
# def5678 HEAD@{1}: commit: Add password tests
# ghi9012 HEAD@{2}: commit: Add login tests
```

## ⚠️ Problem: Merge Conflict

```powershell
# You pulled/merged and Git shows conflicts

# See conflicted files
git status

# Open conflicted file in editor
code conflicted_file.md

# Look for conflict markers:
# <<<<<<< HEAD
# Your changes
# =======
# Their changes
# >>>>>>> branch-name

# Edit file to keep what you want
# Remove conflict markers
# Save file

# Mark as resolved
git add conflicted_file.md

# Complete merge
git commit -m "Resolve merge conflict"

# Test your changes
# ... run tests ...

# Push
git push
```

---

# 8. PULL REQUEST WORKFLOW

## Before Creating PR

```powershell
# Make sure everything is committed
git status
# Should show: "nothing to commit, working tree clean"

# Update feature branch with latest main
git pull origin main

# Verify changes
git diff main feature/your-branch

# See your commits
git log --oneline main..HEAD

# Push updates
git push
```

## Review Your Own Work

```powershell
# See commits on your branch
git log --oneline master..feature/login-tests

# See diff vs main
git diff master feature/login-tests

# See detailed diff with stats
git diff master feature/login-tests --stat
```

## After PR is Approved

```powershell
# Merge on GitHub by clicking "Merge pull request"

# Or merge locally (if team wants)
git switch main
git pull origin main
git merge feature/login-tests
git push origin main
```

## After Merge - Cleanup

```powershell
# Update local main
git switch main
git pull origin main

# Delete feature branch locally
git branch -d feature/login-tests

# Delete on GitHub
git push origin --delete feature/login-tests

# Remove stale remote branches
git fetch --prune
```

---

# 9. CLEANUP & MAINTENANCE

## Delete Old Branches

```powershell
# List merged branches
git branch --merged

# Delete all merged branches
git branch -d feature/login-tests feature/payment-tests

# Delete branch not on current branch (won't work if current branch)
git branch -D feature/old-feature

# Delete branch on GitHub
git push origin --delete feature/old-branch
```

## Clean Up Remote References

```powershell
# Remove deleted remote branches from local list
git fetch --prune

# Remove all stale branches in one go
git remote prune origin
```

## Clean Up Local Repository

```powershell
# Remove untracked files (be careful!)
git clean -fd

# See what would be deleted (safe preview)
git clean -fd --dry-run
```

## Remove Accidentally Committed Files

```powershell
# Remove file from Git but keep it locally
git rm --cached password_reset_tests.md

# Then commit
git commit -m "Remove accidentally committed file"

# Or use this to remove from Git history (advanced)
git filter-branch --tree-filter 'rm -f password_reset_tests.md' HEAD
```

---

# 10. ADVANCED SCENARIOS

## Stash - Temporary Save

```powershell
# Save uncommitted changes temporarily
git stash

# See what's stashed
git stash list

# Apply last stash
git stash pop

# Apply specific stash
git stash pop stash@{0}

# Keep stash after applying
git stash apply

# Delete stash
git stash drop stash@{0}

# Create stash with message
git stash save "WIP: password reset tests"
```

## Cherry Pick - Copy Specific Commits

```powershell
# Copy specific commit from another branch
git cherry-pick abc1234

# Copy multiple commits
git cherry-pick abc1234 def5678 ghi9012

# Copy commits from another branch
git cherry-pick feature/other-branch~2..feature/other-branch
```

## Rebase - Organize Commits (Advanced)

```powershell
# Interactive rebase last 3 commits
git rebase -i HEAD~3

# Rebase on main (dangerous - only on feature branches!)
git rebase main

# Continue after conflict
git rebase --continue

# Abort rebase
git rebase --abort
```

## Search Code History

```powershell
# Search for text in commit history
git log -S "password reset"

# Search in specific author's commits
git log --author="Marina" --grep="test"

# Find when line was added/changed
git blame password_reset_tests.md

# Find which commit deleted something
git log --diff-filter=D -- deleted_file.md
```

## Create Patch

```powershell
# Create patch file from commits
git format-patch main..feature/login-tests

# Apply patch
git apply 0001-add-login-tests.patch
```

## Tag Releases

```powershell
# Create tag
git tag v1.0.0

# Push tag
git push origin v1.0.0

# List tags
git tag

# Delete tag
git tag -d v1.0.0
```

---

# QUICK REFERENCE CHEATSHEET

## Most Used Commands

```powershell
# 1. Start work
git switch main && git pull origin main
git switch -c feature/feature-name

# 2. Check changes
git status
git diff

# 3. Save work
git add .
git commit -m "message"

# 4. Push
git push -u origin feature/feature-name

# 5. Update from main
git pull origin main

# 6. Cleanup
git switch main
git pull origin main
git branch -d feature/feature-name
```

## Branching Naming Convention (QA)

```
feature/feature-name          # New test automation
feature/login-tests           # Tests for login
feature/payment-validation    # Tests for payments

bugfix/bug-name               # Fix for broken tests
bugfix/fix-login-assertion    # Fix specific assertion

hotfix/critical-issue         # Urgent fix
hotfix/ci-broken              # CI pipeline broken

chore/refactor-tests          # Code cleanup
chore/update-dependencies     # Update libraries
```

## Commit Message Format

```
# Good format:
git commit -m "Add login feature test cases"

# Even better (if needed):
git commit -m "Add login feature test cases" -m "- Valid credentials test
- Invalid password test
- Empty username test"

# Bad format:
git commit -m "changes"
git commit -m "fix"
git commit -m "test"
```

---

# TROUBLESHOOTING BY SITUATION

| Situation | Command | Result |
|-----------|---------|--------|
| Can't switch branches | `git status` then `git add . && git commit -m "..."` | Can now switch safely |
| Wrong commit message | `git commit --amend -m "new message"` | Message fixed (before push) |
| Undo last commit | `git reset --soft HEAD~1` | Changes back to staging |
| Discard changes | `git restore .` | Changes deleted (careful!) |
| Wrong branch commits | `git switch -c feature/correct && git switch main && git reset --hard origin/main` | Commits moved to correct branch |
| Merge conflict | Edit file + `git add` + `git commit` | Conflict resolved |
| Already pushed wrong thing | `git revert abc1234` | Creates undo commit (safe) |
| Lost commits | `git reflog` then `git reset --hard abc1234` | Commits restored |
| Stash changes | `git stash` | Work saved temporarily |
| Need work back | `git stash pop` | Work restored |

---

# DANGEROUS COMMANDS (BE CAREFUL!)

```powershell
# ❌ DANGEROUS: Force push (overwrites team's work)
git push --force
# USE THIS INSTEAD:
git push --force-with-lease

# ❌ DANGEROUS: Hard reset (deletes local changes forever)
git reset --hard
# USE THIS INSTEAD:
git reset --soft  # or stash first

# ❌ DANGEROUS: Force delete branch
git branch -D feature/name
# USE THIS INSTEAD:
git branch -d feature/name  # Won't delete if not merged

# ❌ DANGEROUS: Rewrite shared history
git rebase main  # Only on feature branches!
# NOT on shared main or master branch

# ❌ DANGEROUS: Clean untracked files
git clean -fd
# USE THIS FIRST:
git clean -fd --dry-run  # Preview what will delete
```

---

# TIPS FOR QA AUTOMATION

1. **Always pull before starting work**
   ```powershell
   git switch main && git pull origin main
   ```

2. **Always update before PR**
   ```powershell
   git pull origin main
   ```

3. **Commit frequently with clear messages**
   ```powershell
   git commit -m "Add test case for X"  # Good
   git commit -m "update"                # Bad
   ```

4. **Never work on main directly**
   - Always create feature branch first
   - main should only get code through PRs

5. **Review your diff before committing**
   ```powershell
   git diff
   ```

6. **Verify nothing is uncommitted before switching**
   ```powershell
   git status  # Should be clean
   ```

7. **Delete merged branches regularly**
   ```powershell
   git branch --merged | grep -v main | xargs git branch -d
   ```

8. **Use descriptive branch names**
   - `feature/login-tests` ✅ Good
   - `test1` ❌ Bad

9. **Run tests before pushing**
   ```powershell
   npx playwright test
   git push
   ```

10. **When in doubt, ask or check**
    ```powershell
    git status
    git log --oneline -3
    git branch -vv
    ```

---

**Version 1.0 | For QA Automation Engineers | Complete Git Reference**
**Last Updated: June 2026**
