# Assignment 3 — Building Your Command Center

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will build a local Claude Skills system by creating the `.claude/skills/` folder structure, adding predefined skill files, and executing a real agentic command (`/scaffold-terraform`) to generate infrastructure code. You will also observe how skills enforce tool restrictions and enable controlled automation.

---

# Task 1 — Create the Skill Folder Structure

## Goal

Create the required `.claude/skills/` directory structure for all skills.

### Evidence

#### Screenshot 1 — VS Code sidebar showing `.claude/skills/` folder with all 4 subfolders visible

<img width="854" height="524" alt="Screenshot 2026-09-24 161431" src="https://github.com/user-attachments/assets/66665b1e-864c-4c38-88f1-573fdbe4ee13" />



---

# Task 2 — Add the Skill Files

## Goal

Place all required skill files into their correct directories and verify their configuration.

### Evidence

#### Screenshot 2 — `.claude/skills/scaffold-terraform/` open in VS Code showing both `SKILL.md` and `template-spec.md`
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ac186f9a-a327-4101-8b13-37e36b5a9311" />




#### Screenshot 3 — Screenshot 3 — `tf-plan/SKILL.md` frontmatter showing `allowed-tools: Bash, Read, Grep` (no Write) and `disable-model-invocation: true`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/fb5ee676-ebef-4b9d-89d4-ca376b03ac3d" />


---

# Task 3 — Run /scaffold-terraform

## Goal

Execute the `/scaffold-terraform` skill to generate a full Terraform infrastructure setup.

### Evidence

#### Screenshot 4 — Claude's response showing the scaffold complete with the file list

<img width="1920" height="3264" alt="Screenshot_4_combined" src="https://github.com/user-attachments/assets/92eb95d1-a1e5-48ab-9c5b-323bfe778a77" />


---

#### Screenshot 5 — VS Code sidebar showing the `terraform/` folder with all generated files inside

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/69ebd5f3-cdf9-4051-ae6d-16634d70546b" />


---

# Task 4 — Run terraform init and /tf-plan

## Goal

Initialize Terraform and execute the `/tf-plan` skill to observe plan execution and output analysis.

### Evidence

#### Screenshot 6 — Claude's `/tf-plan` response showing it ran the command and analyzed the result (pass or auth error both count)


<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/edb9315d-69ba-46b8-a39d-22ab632e7b34" />

---

# Submission Instructions

- Ensure `.claude/skills/` folder and all skill files are committed to your GitHub repository
- Run all commands successfully and capture required screenshots
- Push final changes to your forked repository

---

## GitHub Repository URL

Paste your forked repository URL here:
https://github.com/keerthanakorampally-gif/Ultimate-Agentic-DevOps-with-Claude-Code.git



## LinkedIn post URL

Paste your forked repository URL here:

https://lnkd.in/p/gVs3k6X3
---

# Completion Checklist

- [✅] `.claude/skills/` folder created with all 4 skill folders
- [✅] All skill files placed correctly
- [✅] `tf-plan/SKILL.md` shows correct `allowed-tools` restrictions
- [✅] `/scaffold-terraform` executed successfully
- [✅] Terraform files generated inside `terraform/` folder
- [✅] `terraform init` executed successfully
- [✅] `/tf-plan` executed and output analyzed by Claude
- [✅] All required screenshots added
- [✅] GitHub repository URL included
- [✅] LinkedIn post URL included

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
