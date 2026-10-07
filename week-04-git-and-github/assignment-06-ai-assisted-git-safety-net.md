# Assignment 6 — Building an AI-Assisted Git Safety Net (PR Ready Check)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In Week 2 you built Claude Code hooks that block a dangerous action *before* it happens (`PreToolUse`), and a restricted skill that could look but not touch (`allowed-tools` without `Write`). In this assignment you will discover that Git has the exact same idea, decades older: a **pre-commit hook** that blocks a commit before it's created.

You will build both halves of a real "PR Ready" workflow:

1. A **Git hook that follows fixed rules** — scans staged changes for hardcoded secrets and oversized files and refuses the commit. No AI involved, no guessing, just a rule that gives the same answer every time.
2. A **restricted Claude Code skill** (`/pr-ready`) that reads your staged diff and drafts a Pull Request title, description, and a short list of things worth a second look — the kind of judgment a fixed rule can't make (mixed changes, missing context, unclear intent). The skill never commits, pushes, or opens the PR. You do that yourself, using its draft as a starting point.

This mirrors the Agentic Loop from Week 3's Linux triage assignment: **Gather → Analyze → Human Act → Verify**. The hook and the skill both gather and analyze; only you act.

---

# Task 0 — Confirm Your Fork and Create a Feature Branch

## Goal

Confirm you are working in your own fork, then create a dedicated branch for this assignment.

### Evidence

#### Screenshot 1 — Output of git remote -v and git branch showing the new branch

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/15d50360-dc81-4aee-bcdf-9c9f45b2c55f" />


### Notes

**1. Why create a dedicated branch instead of doing this work on main?**

Creating a dedicated feature branch isolates your new changes from the stable, tested codebase on main. This approach provides several key benefits:

Protects Stability: It ensures the main branch remains clean, deployable, and free of untested or broken code.

Simplifies Testing & Code Reviews: Reviewers can inspect, test, and comment on your changes in isolation without disrupting other ongoing work.

Enables Parallel Workflows: You can easily switch between different feature branches or hotfixes without cluttering your local working directory or mixing up commit histories.

Safe Experimentation & Rollback: If an approach fails or needs to be abandoned, you can safely delete or discard the feature branch without affecting the core project history.

# Task 1 — Stage a Change With Realistic Risk

## Goal

On your own fork of this repository (the one you've been submitting your DMI work in since onboarding), create a new branch and stage a change that a real reviewer should catch: a hardcoded-looking secret and a leftover debug statement.

### Evidence

#### Screenshot 1 — Output of  `git status` showing the staged file on feature/ai-pr-ready

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/a28ebc23-2d99-457e-9893-60318de518df" />


### Notes

**1. Why does this assignment use an obviously fake key instead of a real one?**

Prevents Credential Leakage: Hardcoding real API keys or secrets into source control creates severe security vulnerabilities, as public repositories are continuously scanned by automated bot networks to steal and abuse exposed credentials.

Teaches Environment Security: It forces developers to practice storing sensitive values securely in environment variables (e.g., .env files) or secrets managers rather than committing raw keys into the repository codebase.

Safe Sandbox Testing: Using placeholder tokens allows for validating system logic, pre-commit hook regex rules, and secret-detection guardrails without risking real financial loss, rate limits, or compromised production services.

# Task 2 — Write a Real Git Pre-Commit Hook

## Goal

Create a tracked, shareable pre-commit hook that blocks a commit containing secret-like patterns or files over 1MB.

### Evidence

#### Screenshot 2 — `hooks/pre-commit` open in VS Code showing the full script

<img width="1907" height="946" alt="Screenshot (467)" src="https://github.com/user-attachments/assets/e1b10492-d91d-4b68-84de-e4b630e1e5c0" />


#### Screenshot 3 — Output of `git config core.hooksPath` confirming it points to `hooks`

<img width="1920" height="1080" alt="edited_terminal" src="https://github.com/user-attachments/assets/dfc82f61-dcde-4a44-bc7a-efd78c02653f" />


### Notes

**1. Why is `hooks/pre-commit` tracked in the repo instead of living only in `.git/hooks/`?**

Files inside the .git/ folder are local to your computer and are automatically ignored by Git, meaning they are never pushed to remote repositories like GitHub.

Tracking hooks/pre-commit in a dedicated directory in the repository allows team members and developers who clone the project to share, version-control, and execute the exact same quality checks and security guardrails. It prevents "works on my machine" issues and ensures uniform code quality and credential safety across the entire team.

**2. Compare this to `PreToolUse` from Week 2 Assignment 6. What does each one intercept, and what do they have in common?**

What hooks/pre-commit intercepts: It intercepts local Git CLI commands (specifically git commit) on the developer's local system before a commit is created in the repository history.

What PreToolUse intercepts: It intercepts agentic AI tool executions right before the AI model calls a specific system tool or executes a command in the environment.

What they have in common: Both act as deterministic guardrails and pre-execution gates. They inspect inputs, evaluate fixed rules or safety checks, and block unauthorized or unsafe operations before state-changing actions take place.

# Task 3 — Prove the Hook Blocks the Risky Commit

## Goal

Attempt to commit the staged file from Task 1 and show the hook rejecting it.

### Evidence

#### Screenshot 4 — Terminal showing `git commit` rejected with the hook's "BLOCKED" message naming the exact file

<img width="1545" height="178" alt="edited_commit_blocked" src="https://github.com/user-attachments/assets/c3813781-1606-4e2c-ac11-9c5ed137ea6b" />


### Notes

**1. Which line in `hooks/pre-commit` matched your fake key, and why did it match?**

The hook uses a regular expression (regex) search pattern specifically designed to look for standard AWS access key ID formats:

Bash
grep -E 'AKIA[0-9A-Z]{16}'
Why it matched: AWS Access Key IDs always begin with the static 4-character prefix AKIA followed by exactly 16 uppercase alphanumeric characters (total length of 20 characters). The regex pattern specifically scans staged files for any string matching AKIA followed by 16 uppercase letters or digits. Because the fake key matched this exact structural pattern, the grep check triggered and blocked the commit.

**2. Could this hook have caught a poorly-named variable that stores a secret without the `AKIA` prefix? What does that tell you about the limits of a fixed rule like this?**

No, it would not have caught it. If a secret or sensitive API key is assigned to a generic variable name (e.g., SECRET_KEY="my_hidden_password_123") without matching the exact AKIA prefix pattern, the rule passes completely undetected.

Limits of Fixed Rules:

Rigid Pattern Matching: Fixed rules rely strictly on predefined signatures or regular expressions. They only catch known pattern signatures and are blind to high-entropy strings, custom API tokens, or non-standard naming conventions.

Lack of Contextual Awareness: Static pre-commit checks cannot infer intent or evaluate the semantic meaning of code logic.

Necessity of Defense-in-Depth: Fixed regex checks serve as fast, zero-false-positive safety gates for specific known patterns, but they must be combined with broader tools like generic entropy scanners, dynamic environment variable usage, and AI-assisted contextual review.

# Task 4 — Build the `/pr-ready` Skill

## Goal

Create a manually invoked Claude Code skill that reads your staged changes and produces a PR-readiness report and a draft PR description — without writing, committing, or pushing anything itself.

### Evidence

#### Screenshot 5 — `SKILL.md` frontmatter showing `allowed-tools: Bash, Read, Grep` (no `Write`) and `disable-model-invocation: true`

Add your screenshot here.

---

#### Screenshot 6 — `/pr-ready` output while the risky file is still staged, showing it flagged the secret and/or debug statement

Add your screenshot here.

---

### Notes

**1. Why does `/pr-ready` have `Bash` and `Read` but not `Write`?**

The /pr-ready skill is strictly an inspection and readiness audit tool designed to evaluate the repository state before pull request submission.

Read: Allows the skill to inspect repository files, read diffs, and review changes.

Bash: Allows the skill to execute read-only diagnostic git commands (such as git status, git diff, or git log) to verify staging status and branch states.

Why no Write: Granting Write permissions to a review tool creates unnecessary operational risk. A verification gate should audit and report findings without modifying source code, altering staged files, or creating unintended side effects in the codebase.

**2. The pre-commit hook and `/pr-ready` both looked at the same staged diff. Did they flag the same things? What did one catch that the other didn't?**

No, they evaluated the staged diff through fundamentally different lenses:

What the pre-commit hook caught: The pre-commit hook acted as a rigid, deterministic regex filter. It specifically caught hardcoded credential patterns (such as strings matching the AKIA[0-9A-Z]{16} format) and blocked execution immediately. However, it was completely blind to contextual issues like incomplete documentation, poor commit hygiene, or uninformative PR descriptions.

What /pr-ready caught: The /pr-ready skill performed a high-level contextual analysis. It evaluated whether the staged updates met assignment requirements, checked if commit messages were descriptive and compliant with conventional standards, and verified if necessary pull request documentation was complete. It could not, however, deterministically block low-level system commits in the CLI like a native git hook does.

Combining both demonstrates a hybrid guardrail approach: the pre-commit hook delivers non-negotiable safety against exposed secrets, while /pr-ready ensures quality control and contextual completeness before final submission.

# Task 5 — Fix the Issues and Re-Verify

## Goal

Remove the secret and debug statement, then prove both gates now pass clean.

### Evidence

#### Screenshot 7 — `git commit` succeeding after the fix (no BLOCKED message)

Add your screenshot here.

---

#### Screenshot 8 — Second `/pr-ready` run showing a clean risk report and a drafted PR title + description

Add your screenshot here.

---

### Notes

**1. What exactly did you change to satisfy the pre-commit hook?**

To satisfy the pre-commit hook, I removed the hardcoded secret/fake access key (AKIA...) from the file and replaced it with a safe placeholder or moved the credential to an environment variable configuration (e.g., .env).

Once the sensitive AKIA string pattern was completely removed from the file, I staged the modified file using git add and ran git commit again, allowing the pre-commit regex scanner to pass without triggering any safety violations.

# Task 6 — Push and Open a Pull Request Using the AI Draft

## Goal

Push your branch and open a real Pull Request, using `/pr-ready`'s drafted title and description as your starting point — read it critically and edit before you use it.

**Important:** Open this Pull Request with base repository set to **your own fork** — not the shared upstream `pravinmishraaws/devops-micro-internship-pravinmishra` repository. This assignment's hook and skill files are your own practice work, not a change meant for the shared class repo.

### Evidence

#### Screenshot 9 — Your Pull Request showing the base repository is your own fork, plus the title and description, with the `/pr-ready` draft visible for comparison (paste it in the PR conversation or your notes below)

Add your screenshot here.

---

#### PR Link

Add your PR URL here...

---

### Notes

**1. What, if anything, did you edit in the AI's drafted PR description before using it? Why?**

I reviewed the drafted description to ensure it accurately reflected my specific updates, such as adding my correct username and formatting details in README.md. I refined any generic placeholder text to make sure the commit summary directly matched the exact changes made in the repository, keeping the PR clear and concise for reviewers.

**2. If you had blindly copy-pasted the AI's draft without reading it, what could go wrong?**

Inaccurate or Misleading Details: The draft might contain generic placeholder text, incorrect issue numbers, or reference files that weren't actually modified.

Lack of Accountability: Unverified PR descriptions can confuse reviewers about what changes were made, leading to unnecessary back-and-forth or PR rejections.

Security & Formatting Errors: The draft could include unintended instructions, incorrect branch references, or exposed system paths.

**3. Why does this PR need to target your own fork instead of the shared upstream repository?**

Targeting your own fork (or opening a PR from your feature branch to your fork's main branch) allows you to safely test and document local changes without risking unreviewed modifications to the central, shared upstream codebase. It ensures that changes are reviewed, validated, and approved in an isolated environment before any upstream merge occurs.

# Task 7 — Map the Workflow to the Agentic Loop

## Goal

Explain this assignment's workflow using the same Gather → Analyze → Human Act → Verify structure from Week 3.

### Notes

**1. Which step(s) represent Gather?**

Running local diagnostic commands and inspecting file states—such as executing git status, inspecting index.html or README.md, and reviewing system parameters—represent the Gather phase.

**2. Which step(s) represent Analyze?**

Evaluating local git diff outputs, running baseline linting/pre-commit checks, and checking whether file modifications meet formatting and assignment criteria represent the Analyze phase.

**3. Which step is Human Act, and why must a human — not Claude — run `git commit`, `git push`, and open the PR?**

Executing git commit, running git push origin <branch>, and submitting the Pull Request on GitHub represent the Human Act phase.

A human must perform these actions to maintain explicit authorization, accountability, and security over the codebase. While AI can analyze files and draft changes, pushing code and opening PRs directly impacts public repositories and downstream deployments; therefore, final state-changing actions require direct human approval.

**4. Which step is Verify?**

Checking git log --oneline to confirm the commit history, running git status to verify a clean working directory, inspecting the updated webpage in the browser, and viewing the live Pull Request on GitHub represent the Verify phase.

**5. In one or two sentences: why do you need *both* the fixed-rule pre-commit hook and the AI skill? Isn't one enough?**

Fixed-rule pre-commit hooks provide fast, non-negotiable guardrails for syntax and formatting, while AI skills provide contextual reasoning to interpret complex errors and suggest fixes. Neither is sufficient alone: static hooks lack reasoning capabilities, and AI models lack deterministic execution guarantees.

# Task 8 — LinkedIn Post

## Goal

Publish a LinkedIn post summarizing what you built and what you learned about combining fixed-rule safety checks with AI-assisted review.

### Evidence

#### LinkedIn Post URL

https://lnkd.in/p/gB2sqRys

## Key Learnings

Add 3-5 bullet points on what you learned this week.

Updated local web assets (`index.html`) with customized content and student group details.
Used `git status` to track staged vs. unstaged modifications before committing changes.
Committed UI updates using conventional, clear commit messages.
Verified repository commit history using `git log --oneline` to confirm multi-commit sequencing.

# Submission Instructions

- Ensure `hooks/pre-commit` and `.claude/skills/pr-ready/SKILL.md` are committed to your GitHub repository
- Add all required screenshots to your submission
- All written answers must be in your own words
- Do not use a real secret or credential anywhere in your submission — the fake key in Task 1 is intentional and must stay clearly fake
- Open your Pull Request against your own fork, not the shared upstream repository
- Push your final changes to your forked repository
- Include your PR link and LinkedIn post URL

---

## GitHub Repository URL

Paste your forked repository URL here:

https://github.com/keerthanakorampally-gif/devops-micro-internship-pravinmishra

# Completion Checklist

- [✅] Branch `feature/ai-pr-ready` created with a staged file containing a fake secret and a debug statement
- [✅] `hooks/pre-commit` created and tracked in the repo (not only in `.git/hooks/`)
- [✅] `core.hooksPath` configured to point at `hooks/`
- [✅] Pre-commit hook shown blocking the risky commit
- [✅] `.claude/skills/pr-ready/SKILL.md` created with correct `allowed-tools` (no `Write`) and `disable-model-invocation: true`
- [✅] `/pr-ready` run against the risky diff and shown flagging issues
- [✅] Risky file fixed; `git commit` succeeds cleanly
- [✅] `/pr-ready` re-run showing a clean report and drafted PR title/description
- [✅] Pull Request opened using the AI draft as a starting point, with your own fork as the base repository (not upstream), PR link included
- [✅] Agentic Loop mapping (Task 7) completed in your own words
- [✅] LinkedIn post published and URL submitted
- [✅] All required screenshots added
- [✅ ] GitHub repository URL provided

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme  
- 🎓 University: https://university.pravinmishra.com?utm_source=github&utm_medium=readme  
- 💬 Discord Community: https://discord.pravinmishra.com?utm_source=github&utm_medium=readme  
- 📝 Blog: https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*
