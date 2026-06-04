# Git Validation Test - Topic 2: Branches & Main Commands
## For QA Automation Engineers - Strong Junior Level

**Duration:** 60-90 minutes
**Difficulty:** Basic → Intermediate → Strong Level
**Purpose:** Validate and strengthen your Git knowledge to interview-ready level

---

## TABLE OF CONTENTS

- [Part 1: Theory Questions](#part-1-theory-questions)
- [Part 2: Practical Tasks](#part-2-practical-tasks)
- [Part 3: Interview-Style Explanations](#part-3-interview-style-explanations)
- [Part 4: Real QA Scenario Analysis](#part-4-real-qa-scenario-analysis)
- [Submission Guide](#submission-guide)

---

# PART 1: THEORY QUESTIONS

## Section 1.1: Understanding Branches (Basic → Intermediate)

### Question 1.1.1 (Basic)
**What is a Git branch and why do QA engineers need them?**

Your answer should include:
- What a branch is (simple definition)
- Why it's useful for QA work
- An example of when you'd create a branch

---

### Question 1.1.2 (Basic)
**What is the `main` branch?**

Your answer should explain:
- What is special about the main branch
- Why we don't commit directly to main (from a QA perspective)
- What happens after code is merged to main

---

### Question 1.1.3 (Intermediate)
**Explain the difference between these two scenarios:**

**Scenario A:** You create a branch `feature/login-tests`, add 5 test cases, and commit them.
**Scenario B:** You commit 5 test cases directly to main.

What are the advantages and disadvantages of each approach in a team environment?

---

### Question 1.1.4 (Intermediate)
**You're working on test cases for a payment feature on your branch `feature/payment-tests`. Your teammate is working on login tests on `feature/login-tests`. Meanwhile, a developer pushed a critical bug fix to `main`.**

- Do your teammates' changes affect your work? Why or why not?
- Can you see their test cases in your branch?
- How would you get their changes if needed?

---

## Section 1.2: Git Commands & Workflow (Basic → Strong)

### Question 1.2.1 (Basic)
**Match each command to its purpose:**

| Command | Purpose |
|---------|---------|
| `git clone` | A) Move to a different branch |
| `git branch` | B) Save changes locally with a message |
| `git switch` | C) Download project from GitHub |
| `git add` | D) See which branch you're on |
| `git commit` | E) Prepare files for saving |
| `git push` | F) Send commits to GitHub |
| `git pull` | G) Get latest changes from GitHub |

---

### Question 1.2.2 (Intermediate)
**Explain what happens at each step:**

```powershell
git switch main
git pull origin main
git branch feature/new-tests
git switch feature/new-tests
# (create and edit test files)
git add .
git commit -m "Add tests for forgot password"
git push -u origin feature/new-tests
```

For each line, write:
1. What the command does
2. What state you're in after executing it
3. Why this step is important

---

### Question 1.2.3 (Strong)
**Your project has this structure:**

```
main (on GitHub):       commit A → commit B → commit C
                         \
feature/payment-tests:   commit B → commit P1 → commit P2
(your local branch)
```

**Current situation:**
- You're on `feature/payment-tests` locally
- Your teammate pushed commit C to main
- You haven't pushed yet

**Answer these:**
- What will happen if you run `git pull origin main`?
- Should you do it? Why or why not?
- What's the correct next step?

---

## Section 1.3: Repository Basics (Basic → Intermediate)

### Question 1.3.1 (Basic)
**What does `git clone` do?**

Explain:
- What it downloads
- Why you use it
- What happens locally after cloning

---

### Question 1.3.2 (Intermediate)
**You're starting as a new QA engineer. Your team has a test repository on GitHub: `https://github.com/company/qa-tests.git`**

- What command do you run to get the project?
- What folder structure do you get?
- Can you immediately start creating branches?
- What do you do next?

---

### Question 1.3.3 (Intermediate)
**After cloning a repository, you run `git branch` and only see `main`. But on GitHub, you see 3 branches: `main`, `feature/login-tests`, `feature/payment-tests`.**

- Why don't you see the other branches locally?
- How do you work on `feature/payment-tests`?
- After switching to that branch, where does your work go?

---

## Section 1.4: Keeping Code In Sync (Intermediate → Strong)

### Question 1.4.1 (Intermediate)
**You've been working on `feature/payment-tests` for 2 days. Meanwhile, your team pushed updates to main. You're about to submit a PR.**

**Before creating the PR, should you:**
- A) Submit PR immediately with your code
- B) Pull main into your branch first
- C) Switch to main, pull, then switch back to your branch

**Which is correct? Explain why.**

---

### Question 1.4.2 (Strong)
**Compare these two approaches:**

**Approach 1:**
```powershell
git switch feature/payment-tests
git add .
git commit -m "Add payment tests"
git push
# → Create PR on GitHub
```

**Approach 2:**
```powershell
git switch main
git pull origin main
git switch feature/payment-tests
git pull origin main  # Pull main into feature branch
git add .
git commit -m "Add payment tests"
git push
# → Create PR on GitHub
```

- What's the difference?
- When would you use each approach?
- Which is better practice? Why?

---

### Question 1.4.3 (Strong)
**You haven't pushed your branch yet. You want to get the latest main code into your feature branch. Which commands work, and why?**

**Option A:**
```powershell
git switch main
git pull origin main
```

**Option B:**
```powershell
git pull origin main
```

**Option C:**
```powershell
git switch feature/payment-tests
git pull origin main
```

Explain what each does and which is correct.

---

## Section 1.5: Team Workflows (Intermediate → Strong)

### Question 1.5.1 (Intermediate)
**Describe the typical QA Git workflow in your team:**

Your answer should cover:
1. How you start new work
2. How you handle your branch
3. How teammates get your work
4. How your work gets to main

---

### Question 1.5.2 (Strong)
**Three QA engineers are working on a test suite together:**

- **Marina:** Working on `feature/login-tests`
- **John:** Working on `feature/payment-tests`  
- **Alex:** Working on `feature/user-profile-tests`

All three finished and created PRs. The team lead approves them one by one and merges them to main.

**Questions:**
1. Do the other QAs' merges affect your work before you merge?
2. After your PR is merged, what should you do locally?
3. If you need John's tests (before his PR is merged), what do you do?

---

# PART 2: PRACTICAL TASKS

## Task 2.1: Repository Setup & First Workflow

**Objective:** Demonstrate you can clone and start work properly.

### 2.1.1 - Clone the Repository

**Your task:**
1. Clone this repository: `https://github.com/m-haniseuskaya/qa-automation-tests.git`
   - To a NEW folder location (not your existing one)
   - Name it: `qa-tests-validation`

**After cloning, answer:**
- What is the full path to the cloned repository?
- Run `git branch` - what do you see?
- Run `git log --oneline -3` - what do the commits show?
- What is the current state of the `main` branch?

**Expected deliverable:**
- Screenshot of cloned folder structure
- Output of `git branch` command
- Output of `git log --oneline -3` command
- Explanation of what each shows

---

### 2.1.2 - Prepare to Start Work

**Your task:**
Before creating a feature branch, ensure main is up-to-date.

```powershell
git switch main
git pull origin main
```

**After executing, answer:**
- What did each command do?
- Are you on main?
- What does the pull output tell you?

**Expected deliverable:**
- Screenshots showing the commands and output
- Explanation of what happened

---

## Task 2.2: Create & Work on Feature Branch

**Objective:** Create a feature branch and demonstrate understanding of branch isolation.

### 2.2.1 - Create Feature Branch

**Your task:**
Create a new branch for test cases on a new QA scenario:

```powershell
git branch feature/password-reset-tests
git switch feature/password-reset-tests
```

**Answer:**
- Verify you're on the new branch (show command + output)
- List all branches (show command + output)
- Which branch has the `*` symbol and why?

**Expected deliverable:**
- Screenshots showing branch creation and verification
- Explanation of branch symbols

---

### 2.2.2 - Create Test File on Your Branch

**Your task:**
1. Create a new test file: `password_reset_tests.md`
2. Add these test cases:
   ```
   # Password Reset Feature - Test Cases
   
   ## Test Case 1: Valid Email
   - Input: valid email address
   - Expected: Reset email sent
   - Status: Ready for automation
   
   ## Test Case 2: Invalid Email
   - Input: non-existent email
   - Expected: Error message shown
   - Status: Ready for automation
   ```

3. Save the file

**Answer:**
- Run `git status` - what do you see?
- Run `git diff` - what changed?
- Why is this important to check before committing?

**Expected deliverable:**
- Screenshot of `git status` output
- Screenshot of `git diff` output
- File content screenshot
- Explanation of status and diff

---

### 2.2.3 - Commit Your Work

**Your task:**
Stage and commit your work with a clear message.

```powershell
git add password_reset_tests.md
git commit -m "Add password reset feature test cases"
```

**Answer:**
- What does `git add` do?
- Why do we need both `add` and `commit`?
- Show the commit output and explain what each part means

**Expected deliverable:**
- Screenshots of commands and output
- Explanation of add vs commit
- Interpretation of commit output

---

### 2.2.4 - Verify Branch Isolation

**Your task:**
Demonstrate that your work is isolated on this branch:

```powershell
# Check your branch
git log --oneline -3

# Switch to main
git switch main

# Check main's history
git log --oneline -3

# Check files on main
ls
```

**Answer:**
- Does main have your new test file? Why or why not?
- Can you see your commit on main?
- Switch back to your branch and verify your file is there

**Expected deliverable:**
- Screenshots showing:
  - Your branch's log
  - Main's log
  - Files on main
  - Files on your branch
- Explanation of branch isolation

---

## Task 2.3: Push to GitHub

**Objective:** Demonstrate understanding of pushing and remote tracking.

### 2.3.1 - Push Your Branch

**Your task:**
```powershell
git switch feature/password-reset-tests
git push -u origin feature/password-reset-tests
```

**Answer:**
- What does `-u origin` mean?
- What does the output tell you?
- Go to GitHub and verify your branch exists there
- Screenshot of your branch on GitHub

**Expected deliverable:**
- Screenshots of push command and output
- Screenshot of your branch on GitHub
- Explanation of `-u` flag

---

### 2.3.2 - Verify Remote Tracking

**Your task:**
```powershell
git branch -v
```

**Answer:**
- What does `-v` flag show?
- What information is displayed?
- How does it tell you the branch is on GitHub?

**Expected deliverable:**
- Screenshot of `git branch -v` output
- Explanation of what you see

---

## Task 2.4: Simulate Team Update (Sync with Main)

**Objective:** Practice pulling latest main when teammates make changes.

### 2.4.1 - Simulate Teammate's Update

**Your task:**
1. Switch to main
2. Pull latest (to get any updates)
3. Create a test file simulating a teammate's work:
   ```powershell
   code temp_teammate_work.md
   ```
4. Add some content, save, and commit:
   ```powershell
   git add temp_teammate_work.md
   git commit -m "Simulate teammate adding a new file"
   ```

**This simulates:** A teammate pushed new work to main

---

### 2.4.2 - Pull Latest Main into Your Branch

**Your task:**
1. Switch back to your feature branch
2. Pull main into it:
   ```powershell
   git pull origin main
   ```

**Answer:**
- Why would you do this before creating a PR?
- What happens to your files when you pull main?
- Do you see the temp file on your feature branch? Explain.

**Expected deliverable:**
- Screenshots of pull command and output
- List of files on your branch after pulling
- Explanation of pulling main into feature branch

---

## Task 2.5: Complex Scenario - Multiple Branches

**Objective:** Demonstrate understanding of working with multiple branches.

### 2.5.1 - Create Second Feature Branch

**Your task:**
```powershell
git switch main
git pull origin main
git branch feature/two-factor-auth-tests
git switch feature/two-factor-auth-tests
```

**Answer:**
- How many branches do you have now?
- Which one are you currently on?
- Show `git branch` output

---

### 2.5.2 - Work on Second Branch

**Your task:**
1. Create file: `two_factor_auth_tests.md`
2. Add content:
   ```
   # Two-Factor Auth - Test Cases
   
   ## Test Case 1: SMS Code
   - Input: Valid phone, correct SMS code
   - Expected: Access granted
   - Status: Ready for automation
   ```
3. Add and commit

**Answer:**
- Show the commit
- Switch to `feature/password-reset-tests` - do you see this file? Why?
- Switch back - is your file there?

**Expected deliverable:**
- Commit screenshots
- Evidence of branch isolation
- Explanation of why files are different on different branches

---

### 2.5.3 - Push Both Branches

**Your task:**
```powershell
git push -u origin feature/two-factor-auth-tests
git switch feature/password-reset-tests
# Make sure it's already pushed
git push
```

**Answer:**
- Go to GitHub - see both branches?
- Screenshot of GitHub showing both branches

---

## Task 2.6: Read & Interpret a Diff

**Objective:** Demonstrate you can read and understand Git diffs.

### 2.6.1 - Make a Change to Existing File

**Your task:**
1. Switch to your `feature/password-reset-tests` branch
2. Edit `password_reset_tests.md` and add:
   ```
   ## Test Case 3: Expired Link
   - Input: Expired reset link
   - Expected: Error "Link expired, request new reset"
   - Status: Ready for automation
   ```

3. Run:
   ```powershell
   git diff password_reset_tests.md
   ```

**Answer:**
- Show the diff output
- Identify the lines with `+` (added)
- Identify the lines with `-` (deleted)
- What do the unchanged lines show you?

---

### 2.6.2 - Interpret Complex Diff

**Your task:**
Run:
```powershell
git log -p --oneline -2
```

This shows 2 recent commits with their diffs.

**Answer:**
- What does `-p` flag do?
- Show the output
- Identify what was added vs deleted in each commit
- Explain why this information is useful for QA

---

## Task 2.7: Real QA Scenario - Code Review Preparation

**Objective:** Prepare your work for team review (as if before creating PR).

### 2.7.1 - Review Your Own Work

**Your task:**
Before submitting to team, review what you've done:

```powershell
git log --oneline feature/password-reset-tests..main
git diff feature/password-reset-tests main
```

**Answer:**
- What commits are on your branch that aren't on main?
- What's the diff between your branch and main?
- Is your work ready for team review? Why or why not?

---

### 2.7.2 - Ensure Your Branch is Up-to-Date

**Your task:**
```powershell
# Pull latest main
git switch main
git pull origin main

# Switch back to your branch
git switch feature/password-reset-tests

# Pull main into your branch
git pull origin main
```

**Answer:**
- Why do this before creating a PR?
- Did anything change in your branch?
- Are you ready to push to GitHub?

---

# PART 3: INTERVIEW-STYLE EXPLANATIONS

**These questions simulate real interview scenarios. Answer as you would in an interview.**

## Question 3.1
**"Tell me about your experience with Git. How have you used it in QA automation?"**

Your answer should cover:
- What you've done with Git
- Why it matters for QA
- Specific tools/commands you use
- An example from your training

---

## Question 3.2
**"Explain the Git workflow your team uses for test automation."**

Your answer should include:
- How you start working on a feature
- How branches are named and used
- How code gets reviewed
- How it reaches production/main

---

## Question 3.3
**"What's the purpose of branching in Git? Why not just commit everything to main?"**

Explain:
- Technical reasons (isolation, safety)
- Team reasons (review, collaboration)
- QA-specific reasons (testing, validation)

---

## Question 3.4
**"A developer asks: 'Why do QA engineers need to use Git? Can't the developers handle it?' - How do you respond?"**

Your answer should explain:
- Why QA needs Git for test code
- Benefits for QA workflow
- How it improves testing process

---

## Question 3.5
**"You're on a feature branch and want to get the latest main code. What's the difference between these two approaches?"**

**Approach A:**
```powershell
git switch main
git pull origin main
git switch feature/my-tests
# (continue working)
```

**Approach B:**
```powershell
git pull origin main
# (while on feature/my-tests)
```

Explain:
- What each does
- Which is correct and why
- When you'd use each

---

## Question 3.6
**"Explain what happens when you `git clone` a repository. What do you get? What's already set up?"**

Your answer should cover:
- What files you get
- What branches you get
- What remote tracking is set up
- What you need to do before starting work

---

## Question 3.7
**"You accidentally started working on main instead of creating a feature branch. You made 3 commits. How do you fix this?"**

Provide:
- The problem in detail
- The solution steps
- Why this solution works
- How to prevent it next time

---

## Question 3.8
**"How do you keep your local repository in sync with the team's GitHub repository?"**

Explain:
- When you need to sync
- How `git pull` works
- When to update from main
- Best practices

---

# PART 4: REAL QA SCENARIO ANALYSIS

## Scenario 4.1: Multi-Feature Testing

**Context:** Your QA team is testing a new e-commerce platform. Three features are being tested:
1. **Checkout Flow** (Marina - you)
2. **Discount Codes** (John)
3. **User Reviews** (Alex)

**Situation:**
- You started `feature/checkout-tests` 2 days ago
- John finished his tests and merged to main yesterday
- Alex is still working on her tests
- A critical bug was found and fixed in main
- You haven't committed your latest changes yet

**Questions:**
1. How does John's merge affect your work? Explain.
2. How do you get the bug fix into your tests?
3. Should you merge before John and Alex? Why?
4. What Git commands do you run and in what order?

---

## Scenario 4.2: Handling Updates

**Context:** You're testing the payment feature.

**Timeline:**
- Day 1: Create branch `feature/payment-tests`
- Day 2-3: Add test cases, commit, push
- Day 4 (morning): Start work on new test cases
- Day 4 (afternoon): Developer adds new payment method to the code

**Questions:**
1. Your tests are outdated. What do you do?
2. Do you need to create a new branch? Why or why not?
3. How do you update your test branch with the new code?
4. Walk through the exact Git commands.

---

## Scenario 4.3: Branch Management

**Context:** You've been working for 2 weeks. You have:
- `feature/login-tests` (merged last week)
- `feature/payment-tests` (merged 3 days ago)
- `feature/checkout-flow-tests` (in progress)
- `feature/user-profile-tests` (in progress)
- `bugfix/test-assertion-error` (needs fixing)

**Questions:**
1. Which branches should be deleted? Why?
2. Which branches should still exist? Why?
3. How do you clean up locally?
4. How do you verify what's on GitHub?

---

## Scenario 4.4: Conflict Resolution (Optional - Advanced)

**Context:** You and another QA were working on the same test file (unlikely but possible).

**Situation:**
```
File: test_utils.md
Your branch added: Test Case for API timeout
Main added: Helper function documentation
```

When you try to pull main into your branch, Git warns about conflicts.

**Questions:**
1. Why does this happen?
2. How do you resolve it?
3. What tools can help you see the conflict?
4. How do you avoid this in the future?

---

# SUBMISSION GUIDE

## How to Submit Your Answers

**For Theory Questions (Part 1):**
- Write clearly and concisely
- Show your understanding in your own words
- Include examples where relevant

**For Practical Tasks (Part 2):**
- Show screenshots of:
  - Terminal/PowerShell commands and output
  - File content
  - GitHub repository view
- Include explanations for each screenshot
- Demonstrate you understand what you're doing

**For Interview Questions (Part 3):**
- Write as you would speak in an interview
- Be professional but conversational
- Show depth of understanding
- Use specific examples

**For Scenarios (Part 4):**
- Analyze each situation
- Provide step-by-step solutions
- Explain the reasoning behind each step
- Show alternative approaches if they exist

---

## Success Criteria

You'll be evaluated on:

| Criteria | What We're Looking For |
|----------|----------------------|
| **Understanding** | Can you explain WHY, not just HOW? |
| **Application** | Can you apply concepts to new situations? |
| **Completeness** | Do you cover all aspects of the question? |
| **Clarity** | Is your explanation clear and well-organized? |
| **Accuracy** | Are your answers technically correct? |
| **Depth** | Do you show strong-level knowledge? |

---

## After Submission

I will:
1. Analyze all your answers
2. Identify strong areas and gaps
3. Point out mistakes with explanations
4. Ask follow-up questions if needed
5. Provide a skill level assessment
6. Create an improvement plan if needed
7. Generate a comprehensive reference document

---

**Total Time Estimate:**
- Part 1 (Theory): 20-25 minutes
- Part 2 (Practical): 35-45 minutes
- Part 3 (Interview): 15-20 minutes
- Part 4 (Scenarios): 10-15 minutes
- **Total: 60-90 minutes**

---

**Ready to begin? Start with Part 1 and work through each section. You can answer all parts at once or one part at a time. Let me know when you're done with each section!**
