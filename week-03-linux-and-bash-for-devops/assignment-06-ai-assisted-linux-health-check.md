# Assignment 6 — Build an AI-Assisted Linux Health Check (AI-Assisted Linux Incident Triage)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will build a read-only Bash triage script that checks the health of your Ubuntu server and Nginx application, connect it to Claude Code as a reusable `/linux-triage` skill, simulate a controlled Nginx incident, use the skill to gather and analyze evidence, recover the service manually, and verify recovery. The workflow follows the Agentic Loop: Gather → Analyze → Human Act → Verify.

---

# Task 1 — Confirm the Healthy Baseline and Create the Workspace

## Goal

Confirm that Nginx and the React application are healthy before building the automation.

### Evidence

#### Screenshot 1 — Output of `systemctl is-active nginx`, `ss -ltn | grep ':80'`, and `curl -I http://localhost`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/afe48e4f-801b-48ae-8948-f616def2d3c5" />


#### Screenshot 2 — Output of `pwd` and `find . -maxdepth 4 -type d | sort` showing the workspace folder structure

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/57755e88-3496-4bce-b6b8-2560824b0bd7" />


### Notes

Answer the following in your own words:

**1. What proves that Nginx is running?**
The output of the command systemctl is-active nginx returning an active status directly confirms that the Nginx service process is currently running in the background on the system.


**2. What proves that the server is listening for HTTP traffic?**

Running ss -ltn | grep ':80' shows an active socket listening on port 80 (the standard HTTP port). Additionally, executing curl -I http://localhost returns an HTTP/1.1 200 OK status header, proving that the web server is actively accepting and responding to incoming HTTP requests.

**3. Why must you capture a healthy baseline before simulating an incident?**

Capturing a healthy baseline establishes a known-good standard for how the system, ports, and services behave under normal operations. Having this benchmark allows you to verify that initial conditions are operational and provides a clear point of comparison so you can accurately detect, isolate, and verify failures during an incident simulation—as well as confirm complete recovery afterward.

# Task 2 — Create Project Context and Safety Rules in CLAUDE.md

## Goal

Tell Claude exactly what this project does and what it is not allowed to do.

### Evidence

#### Screenshot 3 — CLAUDE.md open in VS Code showing all four sections (Project Overview, Incident Workflow, Safety Rules, Output Rules)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d3fd9b2b-f92d-4a3e-b457-775abbe40f8a" />


### Notes

Answer the following in your own words:

**1. Why should Claude receive project-specific operational rules?**

Project-specific operational rules provide essential context and boundaries for the AI assistant. They align Claude’s suggestions with your environment's specific setup, coding standards, directory structures, and safety requirements—preventing generic, invalid, or destructive commands.

**2. Why is the human required to execute the recovery command?**

Requiring a human operator to execute recovery commands enforces a "human-in-the-loop" safety standard. This prevents automated systems or AI tools from applying changes blindly, ensuring every action is reviewed, verified, and audited before making live changes to system configurations or services.

**3. Which rule prevents Claude from making an unsupported diagnosis?**

The Incident Workflow rule (specifically step 1 and step 2 requiring service status, port binding checks, and system log reviews before taking action) combined with the Output Rules (requiring reproducible terminal commands and expected outputs for verification) prevents unsupported diagnoses. They force recommendations to be grounded directly in verified diagnostic evidence rather than assumptions.

# Task 3 — Use Agentic AI to Plan Before Writing the Script

## Goal

Use Claude Code to inspect the environment and produce a read-only plan before creating any Bash code.

### Evidence

#### Screenshot 4 — Claude Code showing the five-check plan and read-only inspection results

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. Which part of this task represents the Gather phase?**

The Gather phase is represented by running diagnostic commands to collect baseline information about the environment—specifically checking service status with systemctl is-active nginx, verifying port bindings via ss -ltn | grep ':80', inspecting HTTP headers using curl -I http://localhost, and checking the workspace structure with pwd and find.

**2. Did Claude follow the instruction not to create files? How did you verify this?**

Yes, Claude followed the instruction. This was verified by checking the terminal output before and after the interaction (such as running ls -lah or directory tree checks) to confirm that no unauthorized files or untracked modifications were written to the file system during the diagnostic phase.

**3. Why is planning before coding useful in DevOps automation?**

Planning before coding prevents misconfigurations, reduces downtime, and ensures that scripts account for edge cases and existing dependencies. It establishes a safe, repeatable framework where logic can be reviewed against safety rules before executing automated changes on live infrastructure.

# Task 4 — Build the Linux Triage Bash Script

## Goal

Create one Bash script that gathers consistent Linux and Nginx health evidence.

### Evidence

#### Screenshot 5 — Top section of `linux-triage.sh` showing variables, thresholds, and the checks array

Add your screenshot here.

---

#### Screenshot 6 — Middle section showing check functions and conditionals

Add your screenshot here.

---

#### Screenshot 7 — Bottom section showing the loop, summary function, and exit behavior

Add your screenshot here.

---

#### Screenshot 8 — Output of `bash -n scripts/linux-triage.sh` (no syntax errors) and `ls -l scripts/linux-triage.sh` showing executable permission

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. What is stored in the checks array?**

The checks array stores a list of specific system items, service names, port numbers, or check tasks (such as nginx, 80, or health status indicators) that the script needs to iterate through and validate sequentially.

**2. How does the `for` loop use that array?**

The for loop iterates over each element in the checks array one by one. During each iteration, it assigns the current item to a loop variable and executes the function or check command associated with that specific item.

**3. Why are the health checks separated into functions?**

Separating health checks into functions modularizes the script, making the code cleaner, easier to read, and reusable. It keeps individual check logic isolated, so if a health check needs to be modified or updated, it can be changed in one place without altering the main loop or overall script structure.

**4. What is the purpose of `$(...)` in this script?**

The $() syntax represents command substitution in Bash. It executes the command enclosed within the parentheses inside a subshell and returns its standard output, allowing the script to capture command results directly into variables or evaluate them inline (e.g., USER=$(whoami) or STATUS=$(systemctl is-active nginx)).

**5. Why does the script use different exit codes for HEALTHY, WARN, and FAIL?**

Using distinct exit codes (such as 0 for HEALTHY, 1 for WARN, and 2 for FAIL) allows external automated tools, CI/CD pipelines, and monitoring systems to programmatically detect the exact operational status of the script. This enables downstream systems to react conditionally—such as passing a build on success, sending an alert on warning, or immediately triggering automated failover and rollback procedures on failure.

# Task 5 — Run and Understand the Healthy-State Report

## Goal

Run the Bash script against the healthy server and verify that it creates a report.

### Evidence

#### Screenshot 9 — Output of `./scripts/linux-triage.sh` showing your Full Name and all five check results

Add your screenshot here.

---

#### Screenshot 10 — Output showing the captured exit code and final summary

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. What is the overall status of your healthy baseline?**

The overall status of the healthy baseline is HEALTHY (or operational). All core system components are functioning as expected—the Nginx service process is active, the web server is actively listening on port 80, and HTTP requests return a standard 200 OK response.

**2. Which exact Linux evidence proves the application is serving traffic?**

Two specific command outputs prove the application is actively serving traffic:

ss -ltn | grep ':80': Shows an active socket listening on port 80, confirming the server accepts incoming HTTP connections.

curl -I http://localhost: Returns an HTTP/1.1 200 OK response header, proving the application receives HTTP requests and successfully serves back the response payload.

**3. Did your script return exit code 0 or 1? Explain why.**

The script returned exit code 0. In standard Bash conventions, an exit code of 0 indicates successful execution with no critical failures encountered (HEALTHY baseline state). Exit code 1 (or higher) is reserved to signal a warning, error, or health check failure to calling processes or pipelines.

**4. What is the difference between a warning and a failure in this script?**

Warning (WARN): Indicates a non-critical anomaly or threshold condition (e.g., elevated disk usage or high memory consumption) where the application is still functioning, but requires attention before it escalates into an outage.

Failure (FAIL): Indicates a critical service outage or broken dependency (e.g., Nginx service stopped or port 80 unreachable) where the application cannot serve traffic, requiring immediate intervention or automated failover.

# Task 6 — Create and Run the /linux-triage Skill

## Goal

Turn the Bash script into a reusable, manually invoked Agentic AI workflow.

### Evidence

#### Screenshot 11 — `SKILL.md` showing the frontmatter, allowed tool restrictions, and safety rules

Add your screenshot here.

---

#### Screenshot 12 — `/linux-triage` output for the healthy server

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. Why does this skill have Bash, Read, and Grep, but not Write?**

Add your answer here.

---

**2. Why is `disable-model-invocation: true` useful for this skill?**

Add your answer here.

---

**3. What part is performed by Bash, and what part is performed by Claude?**

Add your answer here.

---

**4. Why is this better than asking Claude "Is my server healthy?" without giving it evidence?**

Add your answer here.

---

# Task 7 — Simulate an Nginx Incident and Let the Skill Diagnose It

## Goal

Create a controlled service failure, gather evidence through Bash, and let Claude analyze the evidence without taking recovery action.

### Evidence

#### Screenshot 13 — Output showing Nginx is inactive and the HTTP request fails

Add your screenshot here.

---

#### Screenshot 14 — `/linux-triage` output showing failed evidence, most likely cause, and a suggested recovery command

Add your screenshot here.

---

#### Screenshot 15 — `incident-failure-report.txt` showing the failed checks and your Full Name

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. Which three checks failed?**

Add your answer here.

---

**2. What evidence supports the conclusion that Nginx is unavailable?**

Add your answer here.

---

**3. Did Claude execute the recovery command? Why is that important?**

Add your answer here.

---

**4. Which phase of the Agentic Loop is represented by the Bash report?**

Add your answer here.

---

**5. Which phase is represented by Claude's explanation?**

Add your answer here.

---

# Task 8 — Recover Manually, Verify Again, and Write the Incident Summary

## Goal

Recover the service as the human operator and prove that the system is healthy again.

### Evidence

#### Screenshot 16 — Output showing Nginx is active and `curl -I http://localhost` returns 200 OK

Add your screenshot here.

---

#### Screenshot 17 — Second `/linux-triage` output showing successful recovery with no FAIL results

Add your screenshot here.

---

#### Screenshot 18 — Output of `ls -lah reports` showing both `incident-failure-report.txt` and `recovery-report.txt`

Add your screenshot here.

---

#### Screenshot 19 — `incident-summary.md` showing all required sections and your Full Name

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. What action did you execute manually?**

Add your answer here.

---

**2. What evidence proves that the service recovered?**

Add your answer here.

---

**3. Why is the second triage run necessary?**

Add your answer here.

---

**4. What could go wrong if an AI agent automatically restarted every failed service?**

Add your answer here.

---

**5. In one sentence, explain the difference between using AI as a chatbot and using AI in this agentic workflow.**

Add your answer here.

---

# Incident Summary

Fill in all seven sections below in your own words.

**Full Name:** Add your full name here

**Date:** DD/MM/YYYY

---

**1. Reported Symptom**

Add your answer here.

---

**2. Evidence Collected**

Add your answer here.

---

**3. Most Likely Cause**

Add your answer here.

---

**4. Human-Approved Recovery Action**

Add your answer here.

---

**5. Verification**

Add your answer here.

---

**6. Safety Decision**

Add your answer here.

---

**7. Agentic Loop Mapping**

Add your answer here.

---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`Add your URL here`

---

#### Screenshot — Published LinkedIn post

Add your screenshot here.

---

# GitHub Repository URL

Paste the URL of your GitHub folder or repository containing the assignment files here:

`Add your URL here`

---

# Submission Instructions

- Add all required screenshots in your submission
- Full Name must be visible in required screenshots and the Bash report
- All written answers must be in your own words
- Do not expose sensitive information (keys, passwords, AWS account IDs, tokens)
- GitHub URL must be included in this document

---

# Completion Checklist

- [ ] Task 1: Healthy baseline confirmed, workspace created (Screenshots 1–2, Notes answered)
- [ ] Task 2: CLAUDE.md created with all four sections (Screenshot 3, Notes answered)
- [ ] Task 3: Five-check plan produced by Claude using read-only tools (Screenshot 4, Notes answered)
- [ ] Task 4: `linux-triage.sh` created, syntax validated, executable permission set (Screenshots 5–8, Notes answered)
- [ ] Task 5: Healthy-state report generated with no FAIL result (Screenshots 9–10, Notes answered)
- [ ] Task 6: `/linux-triage` skill created and run successfully on healthy server (Screenshots 11–12, Notes answered)
- [ ] Task 7: Nginx incident simulated, failed evidence captured, Claude did not execute recovery (Screenshots 13–15, Notes answered)
- [ ] Task 8: Nginx recovered manually, recovery verified, reports saved, incident summary complete (Screenshots 16–19, Notes answered)
- [ ] Incident summary contains all seven required sections
- [ ] LinkedIn post published and URL submitted
- [ ] Full Name visible in all required screenshots and the Bash report
- [ ] Skill does not have Write permission
- [ ] Skill did not execute any recovery commands
- [ ] No sensitive data exposed

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
