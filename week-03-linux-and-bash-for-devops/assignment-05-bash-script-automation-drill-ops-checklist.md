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
<img width="1920" height="1080" alt="Screenshot (322)" src="https://github.com/user-attachments/assets/14a4c62e-36d1-4918-8efa-210b68e3dfa2" />



#### Screenshot 2 — Output of `./user-info.sh`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/fe144f3f-0cb6-4cc0-bab1-40e6a054164c" />


### Notes

Answer the following in your own words:

**1. What is a variable in Bash?**

A variable in Bash is a named storage location used to hold data—such as text strings, numbers, filenames, or command outputs—in system memory. Variables allow scripts to store information dynamically, reuse values across multiple commands, and manipulate data during script execution.

---

**2. Why should we avoid spaces around the `=` sign when creating variables?**
Bash treats spaces as command arguments and delimiters. If you put spaces around the = sign (for example, NAME = Keerthana), Bash interprets the word before the space (NAME) as a standalone command to execute, and = Keerthana as positional parameters passed to that non-existent command. This results in a "command not found" syntax error.

---

**3. How do you access the value stored inside a Bash variable?**
To access or reference the value stored inside a variable, prefix the variable's name with a dollar sign ($). For example, if you assign NAME="Keerthana", you retrieve and print its value using echo $NAME or echo "${NAME}". The dollar sign tells the shell to perform variable expansion, replacing the variable name with its actual stored content before executing the command.

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
An array in Bash is a variable that can hold multiple data values simultaneously under a single variable name. Instead of storing a single string or number, an array acts as an ordered collection of elements, where each value is assigned a specific index number (starting at index 0) or a custom key (in associative arrays) to easily identify and retrieve it.

**2. Why are arrays useful in scripts?**

Arrays are essential in scripting for several reasons:
Efficient Data Grouping: They allow you to group related items—such as list of server IP addresses, filenames, user accounts, or package names—into one manageable variable rather than creating separate variables for every single item (server1, server2, server3).
Simplified Looping: Arrays integrate seamlessly with for loops, enabling scripts to automate repetitive actions on sets of data dynamically (e.g., iterating through a list of files to back them up one by one).
Cleaner and Maintainable Code: By reducing redundant code and hardcoded values, arrays keep scripts concise, easier to read, and simpler to modify or expand when adding new data items in the future.

**3. What does `"${tools[@]}"` mean?**

In Bash, "${tools[@]}" expands to all elements contained within the tools array.
The @ symbol acts as a wildcard index that selects every item in the array.
Wrapping it in double quotes ("${tools[@]}") ensures that if an individual array element contains spaces or special characters, Bash preserves each item as a distinct, intact argument rather than splitting them into separate words.

---

**4. What is the purpose of the `for` loop in this script?**

The for loop automates iteration through the elements of a collection (such as array items or a sequence of numbers). Its purpose in the script is to sequentially pick up each item in the array, store it temporarily in a loop variable, and execute the specified set of commands inside the do ... done block once for every item until all elements have been processed.

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

A loop is a fundamental programming construct that repeatedly executes a specific block of code as long as a specified condition is true or until every item in a sequence (such as a list, array, or range of numbers) has been processed.



**2. Why do we use loops in Bash scripting?**

Loops are used in Bash scripting to automate repetitive tasks and process dynamic sets of data efficiently. Instead of writing identical or near-identical commands multiple times, a loop allows you to execute operations—such as batch-renaming files, checking service statuses, or reading lines from a text file—using a single, clean block of code.

**3. How many times did the loop run in your script?**

The loop ran 5 times (iterating through the 5 elements defined in the tools array or range {1..5}).

**4. What would you change if you wanted the loop to run 10 times?**
To make the loop execute 10 times:

If using a sequence range, change {1..5} to {1..10}:

Bash
for i in {1..10}; do
If using a standard C-style loop, change the upper limit condition to <= 10 or < 11:

Bash
for ((i=1; i<=10; i++)); do
If using an array, ensure the array contains 10 items for the for item in "${array[@]}" construct to iterate through.

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

The -d flag is a conditional file test operator that checks whether a specified path exists and is a directory. In an if [ -d "$path" ] statement, it returns true (0) if the path is a valid directory, and false (1) if it does not exist or points to a regular file/other file type.

**2. What does `-f` check in Bash?**
The -f flag is a conditional test operator that checks whether a specified path exists and is a regular file (such as a text file, script, or image, as opposed to a directory or device file). In an if [ -f "$file" ] statement, it returns true (0) if the file exists and is a standard file.


**3. Why should file and directory paths be stored in variables?**
Storing paths in variables provides key benefits for script maintainability:

Single Point of Update: If a file or folder directory changes, you only need to update the path once in the variable definition rather than hunting down every instance throughout the script.

Prevents Syntax & Typo Errors: Reusing a variable (e.g., "$LOG_DIR") ensures consistency and avoids subtle bugs caused by typing errors in long directory paths.

Improves Code Readability: Using descriptive variable names (like BACKUP_PATH or CONFIG_FILE) makes the script's purpose clearer and easier to understand.

**4. What happens if the file does not exist?**

The -f flag is a conditional test operator that checks whether a specified path exists and is a regular file (such as a text file, script, or image, as opposed to a directory or device file). In an if [ -f "$file" ] statement, it returns true (0) if the file exists and is a standard file.

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

The if-else statement is a control flow structure that allows a script to make decisions based on specific conditions. It checks whether a condition (such as a file check or numeric comparison) evaluates to true or false; if true, it executes one block of code, and if false, it executes an alternative block (or continues down the script).

**2. Why are functions useful in scripts?**

n Bash numeric comparisons, -ge stands for "Greater than or Equal to". In a test condition like [ "$age" -ge 18 ], it evaluates to true if the value on the left is numerically equal to or larger than the value on the right.

**3. Which functions did you create in this script?**

Testing conditions with different values (including boundary and edge cases) ensures that the script behaves correctly under all possible scenarios. It verifies that both the if and else (or elif) logical branches execute as expected, catching logic bugs, syntax errors, or unexpected crashes before deploying the script to production.

**4. How does this final script combine variables, arrays, loops, conditionals, files, and functions?**

Conditionals enable automation scripts to dynamically adapt to real-world server environments without human intervention. They allow scripts to:

Perform Error Handling: Verify if a required service, file, or network interface is active before attempting to run a task.

Prevent Unnecessary Work: Skip setup steps if a directory or user account already exists.

Recover Automatically: Trigger fallback procedures (e.g., restarting a service or alerting an admin) if a health check fails.

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

[https://www.linkedin.com/posts/keerthana-korampally_devops-aws-nginx-activity-7247291839102812160-xX9](https://www.linkedin.com/posts/keerthana-korampally_devops-aws-nginx-activity-7247291839102812160-xX9)_

#### Screenshot — Published LinkedIn post

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/17144db5-e5e5-494b-a389-60162473587b" />


# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- All script files must be created and run successfully
- Required notes must be answered clearly for every task
- Do not expose sensitive information (keys, passwords, credentials)

---

# Completion Checklist

- [✅] Task 1: Environment setup verified, workspace created (Screenshots 1–2, Notes answered)
- [✅] Task 2: First script created, executed, permissions verified (Screenshots 1–3, Notes answered)
- [✅] Task 3: Variables script created and run (Screenshots 1–2, Notes answered)
- [✅] Task 4: Arrays and loops script created and run (Screenshots 1–2, Notes answered)
- [✅] Task 5: Counter loop script created and run (Screenshots 1–2, Notes answered)
- [✅] Task 6: File validation script created and run (Screenshots 1–3, Notes answered)
- [✅] Task 7: Pass/Retry conditional script tested with both values (Screenshots 1–4, Notes answered)
- [✅] Task 8: Final automation script created and run (Screenshots 1–3, Notes answered)
- [✅] All scripts run without errors
- [✅] Full Name visible in all required screenshots
- [✅] LinkedIn post published and URL submitted
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
