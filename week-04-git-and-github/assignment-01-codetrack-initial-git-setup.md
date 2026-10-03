# Assignment 1 — CodeTrack: Initial Git Setup (Local Only)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will set up Git correctly on your local machine before starting the CodeTrack project. You will create a local repository and configure your Git identity at both the repository level (local) and the machine level (global). This assignment is local only — you will not push anything to GitHub yet.

---

# Task 1 — Create the CodeTrack Project and Initialize Git

## Goal

Create a `CodeTrack` project folder and initialize it as a Git repository.

### Evidence

#### Screenshot 1 — Output of `git init` inside `CodeTrack` showing "Initialized empty Git repository"

<img width="1920" height="1080" alt="Screenshot (367)" src="https://github.com/user-attachments/assets/b2ba2cbe-8049-4be3-8ece-f7b666dec93e" />


#### Screenshot 2 — Output of `ls -a` showing the `.git` folder

<img width="949" height="1047" alt="Screenshot (368)" src="https://github.com/user-attachments/assets/0fdef283-3d9c-44f9-a17d-31cf4243f436" />



### Notes

**1. What is the `.git` folder, and why does it matter?**

The .git folder is the hidden database and core engine of your Git repository. When you run git init, Git creates this directory to store all the tracking data, history, and configuration for your project.

Why It Matters
Complete Version History: It tracks every commit, stash, and branch, recording the exact history of every file change made over time.

Metadata & Configuration: It stores repository settings (such as remote URLs and user info) in its config file, as well as staging area information in the index file.

Separation from Working Code: Your actual source code files stay clean in your project folder (the working directory), while all version control mechanics happen behind the scenes inside .git.

# Task 2 — Configure Git Identity Locally (Repository-Only)

## Goal

Set your Git username and email for the `CodeTrack` repository only, using `git config --local`.

### Evidence

#### Screenshot 3 — Output of `git config --local --list` showing your `user.name` and `user.email`

<img width="1920" height="1080" alt="Screenshot (370)" src="https://github.com/user-attachments/assets/0caf0c17-06ee-4a95-83be-7e3ec1182461" />


# Task 3 — Configure Git Identity Globally

## Goal

Set a global Git username and email for this machine using `git config --global`. Note that CodeTrack's local settings still take priority over these.

### Evidence

#### Screenshot 4 — Output of `git config --global --list` showing your `user.name` and `user.email`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/1d01fc6a-f442-4f0b-a18d-e487006c6213" />


# Submission Instructions

- Add all required screenshots in your submission
- Full Name must be visible in required screenshots
- Do not expose passwords, access tokens, or private keys

---

# Completion Checklist

- [✅] `CodeTrack` folder created and initialized as a Git repository (Screenshots 1–2)
- [✅] Explanation of the `.git` folder written in your own words
- [✅] Local `user.name` and `user.email` configured and verified (Screenshot 3)
- [✅] Global `user.name` and `user.email` configured and verified (Screenshot 4)
- [✅] No sensitive data exposed

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
