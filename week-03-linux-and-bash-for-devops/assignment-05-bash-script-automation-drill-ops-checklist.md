# Assignment 5 — Bash Script Automation Drill (OPS Checklist)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will practice Bash scripting by building a series of small automation scripts covering environment setup, variables, arrays, loops, file conditionals, if-else logic, and functions. These scripts form the foundation of real-world Linux automation used in DevOps, cloud, and production support environments.

---

# Task 1 — Bash Environment & Workspace Setup

## Goal

Verify that Bash is available on your system and create a clean workspace for this assignment.

### Evidence

#### Screenshot 1 — Output of `echo $SHELL` and `bash --version`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e6412710-7a09-4ae5-84ff-a7e9621ae39d" />


---

#### Screenshot 2 — Output of `pwd` and `ls -lah` showing the scripts directory

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/cf51ba7a-7b02-4f78-b022-0e5f6aaf4e18" />


---

### Notes

Answer the following in your own words:

**1. What is Bash?**

Bash (Bourne Again SHell) is a command-line interpreter and scripting language used primarily in Unix-like operating systems such as Linux and macOS. It provides a text-based interface where users can type commands to interact directly with the operating system kernel, navigate the filesystem, execute programs, and automate repetitive administrative tasks through shell scripts.


**2. What is the difference between shell and Bash?**

Shell: A general, umbrella term for any user interface—command-line or graphical—that accepts user input and communicates with the operating system's kernel. Command-line shells define the standard specifications and interfaces for command execution (e.g., the standard POSIX shell /bin/sh).

Bash: A specific, popular implementation of a command-line shell. It is an expanded version of the original Bourne shell (sh) that incorporates extra features like command-line editing, command history, tab completion, arrays, and enhanced scripting capabilities.


**3. Why is it important to confirm the Bash version before writing scripts?**

Confirming the Bash version ensures script compatibility, reliability, and security across environments:
Feature Availability: Newer versions of Bash introduce features and syntax improvements (such as associative arrays introduced in Bash 4.0 or custom string manipulation methods) that fail on legacy versions (like macOS's default Bash 3.2).

Cross-Environment Consistency: Knowing the exact version prevents runtime errors when moving scripts between development, staging, and production servers.
Security & Optimization: Checking the version guarantees that your scripts aren't running on outdated shells containing known security vulnerabilities or deprecated behaviors.


# Task 2 — Your First Bash Script

## Goal

Create your first Bash script, make it executable, and run it from the terminal.

### Evidence

#### Screenshot 1 — Content of `first-script.sh`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/cb4fddb8-fc2d-44d3-8b81-b79b0f4e3a68" />


---

#### Screenshot 2 — Output of `./first-script.sh`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/4b914008-9f84-4b25-8047-01ab8d3e2c1e" />


---

#### Screenshot 3 — Output of `ls -l first-script.sh` showing executable permission

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/4d3a846c-822a-46ca-945b-b8a37b7f38fb" />


---

### Notes

Answer the following in your own words:

**1. What is the purpose of `#!/bin/bash`?**
The #!/bin/bash line—known as a shebang—is placed at the very top of a script file to instruct the operating system on which interpreter to use when executing the file. By pointing directly to /bin/bash, it ensures that the system processes the script using the Bash shell rather than a default or alternative shell (like sh or zsh), preserving intended syntax and feature compatibility.



**2. Why do we use `chmod +x` before running a script?**

In Linux and Unix-like operating systems, newly created text files do not have execution permissions enabled by default for security reasons. Running chmod +x filename.sh modifies the file's permission flags by adding the eXecute permission. This tells the system that the file contains an executable program, allowing users or automated tasks to trigger it directly as a command.


**3. What is the difference between running a script using `./script.sh` and `bash script.sh`?**
./script.sh (Direct Execution):
Requires the file to have executable permissions (chmod +x).
Reads the shebang (#!/bin/bash) at the top of the file to determine which interpreter to invoke.
Executes the script in a brand-new subshell environment defined by that shebang.
bash script.sh (Explicit Interpreter Call):
Does not require the file to have executable permissions (only read permission is needed).
Forces the script to run specifically through the bash interpreter, completely ignoring any shebang line present in the file.
Explicitly passes the file as an argument to the bash binary.




# Task 3 — Variables: User Information Script

## Goal

Use variables to store and display user-related information.

### Evidence

#### Screenshot 1 — Content of `user-info.sh`

Add your screenshot here.

---

#### Screenshot 2 — Output of `./user-info.sh`

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. What is a variable in Bash?**

Add your answer here.

---

**2. Why should we avoid spaces around the `=` sign when creating variables?**

Add your answer here.

---

**3. How do you access the value stored inside a Bash variable?**

Add your answer here.

---

# Task 4 — Arrays & Loops: Tools Checklist Script

## Goal

Use arrays and loops to print a checklist of tools used in Bash scripting.

### Evidence

#### Screenshot 1 — Content of `tools-checklist.sh`

Add your screenshot here.

---

#### Screenshot 2 — Output of `./tools-checklist.sh`

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. What is an array in Bash?**

Add your answer here.

---

**2. Why are arrays useful in scripts?**

Add your answer here.

---

**3. What does `"${tools[@]}"` mean?**

Add your answer here.

---

**4. What is the purpose of the `for` loop in this script?**

Add your answer here.

---

# Task 5 — Loops: Number Counter Script

## Goal

Use loops to repeat a task multiple times.

### Evidence

#### Screenshot 1 — Content of `counter.sh`

Add your screenshot here.

---

#### Screenshot 2 — Output of `./counter.sh`

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. What is a loop?**

Add your answer here.

---

**2. Why do we use loops in Bash scripting?**

Add your answer here.

---

**3. How many times did the loop run in your script?**

Add your answer here.

---

**4. What would you change if you wanted the loop to run 10 times?**

Add your answer here.

---

# Task 6 — Files & Conditionals: File Validation Script

## Goal

Use file checks and conditionals to verify whether files and directories exist.

### Evidence

#### Screenshot 1 — Output of `ls -lah ../test-folder`

Add your screenshot here.

---

#### Screenshot 2 — Content of `file-check.sh`

Add your screenshot here.

---

#### Screenshot 3 — Output of `./file-check.sh`

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. What does `-d` check in Bash?**

Add your answer here.

---

**2. What does `-f` check in Bash?**

Add your answer here.

---

**3. Why should file and directory paths be stored in variables?**

Add your answer here.

---

**4. What happens if the file does not exist?**

Add your answer here.

---

# Task 7 — Conditionals: Pass or Retry Script

## Goal

Use if-else conditionals to make decisions based on a variable value.

### Evidence

#### Screenshot 1 — Content of `score-check.sh` with `score=85`

Add your screenshot here.

---

#### Screenshot 2 — Output showing `Result: Pass`

Add your screenshot here.

---

#### Screenshot 3 — Content of `score-check.sh` with `score=55`

Add your screenshot here.

---

#### Screenshot 4 — Output showing `Result: Retry`

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. What is the purpose of if-else in Bash?**

Add your answer here.

---

**2. What does `-ge` mean?**

Add your answer here.

---

**3. Why should conditions be tested with different values?**

Add your answer here.

---

**4. How can conditionals help in automation scripts?**

Add your answer here.

---

# Task 8 — Functions: Final Bash Automation Script

## Goal

Create a final Bash script using functions to organize reusable code.

### Evidence

#### Screenshot 1 — Content of `final-automation.sh`

Add your screenshot here.

---

#### Screenshot 2 — Output of `./final-automation.sh`

Add your screenshot here.

---

#### Screenshot 3 — Output of `ls -lah` showing all created scripts

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. What is a function in Bash?**

Add your answer here.

---

**2. Why are functions useful in scripts?**

Add your answer here.

---

**3. Which functions did you create in this script?**

Add your answer here.

---

**4. How does this final script combine variables, arrays, loops, conditionals, files, and functions?**

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

# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- All script files must be created and run successfully
- Required notes must be answered clearly for every task
- Do not expose sensitive information (keys, passwords, credentials)

---

# Completion Checklist

- [ ] Task 1: Environment setup verified, workspace created (Screenshots 1–2, Notes answered)
- [ ] Task 2: First script created, executed, permissions verified (Screenshots 1–3, Notes answered)
- [ ] Task 3: Variables script created and run (Screenshots 1–2, Notes answered)
- [ ] Task 4: Arrays and loops script created and run (Screenshots 1–2, Notes answered)
- [ ] Task 5: Counter loop script created and run (Screenshots 1–2, Notes answered)
- [ ] Task 6: File validation script created and run (Screenshots 1–3, Notes answered)
- [ ] Task 7: Pass/Retry conditional script tested with both values (Screenshots 1–4, Notes answered)
- [ ] Task 8: Final automation script created and run (Screenshots 1–3, Notes answered)
- [ ] All scripts run without errors
- [ ] Full Name visible in all required screenshots
- [ ] LinkedIn post published and URL submitted
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
