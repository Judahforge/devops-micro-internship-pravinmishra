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

![ Output of `echo $SHELL` and `bash --version](./screenshots/echo.png)

---

#### Screenshot 2 — Output of `pwd` and `ls -lah` showing the scripts directory

![`pwd` and `ls -lah](./screenshots/ls-lah.png)

---

### Notes

Answer the following in your own words:

**1. What is Bash?**

Bash (Bourne Again Shell) is a command-line interpreter used in Linux systems to execute commands and automate tasks through scripts.
---

**2. What is the difference between shell and Bash?**

A shell is a program that allows users to communicate with the operating system using commands. Bash is one type of shell with additional features for scripting and automation.
---

**3. Why is it important to confirm the Bash version before writing scripts?**

Different Bash versions may support different features. Checking the version ensures that scripts will run correctly in the current environment.
---

# Task 2 — Your First Bash Script

## Goal

Create your first Bash script, make it executable, and run it from the terminal.

### Evidence

#### Screenshot 1 — Content of `first-script.sh`

![Content of `first-script.sh](./screenshots/bash%20content.png)

---

#### Screenshot 2 — Output of `./first-script.sh`

![Output of `./first-script.sh](./screenshots/shoutput.png)

---

#### Screenshot 3 — Output of `ls -l first-script.sh` showing executable permission

![executable permission](./screenshots/permission.png)

---

### Notes

Answer the following in your own words:

**1. What is the purpose of `#!/bin/bash`?**

It tells the operating system that the script should be executed using the Bash interpreter.
---

**2. Why do we use `chmod +x` before running a script?**

chmod +x gives the script executable permission, allowing it to run like a program.
---

**3. What is the difference between running a script using `./script.sh` and `bash script.sh`?**

./script.sh runs the script directly and requires executable permission. bash script.sh runs the script through Bash without needing executable permission.
---

# Task 3 — Variables: User Information Script

## Goal

Use variables to store and display user-related information.

### Evidence

#### Screenshot 1 — Content of `user-info.sh`

![Content of `user-info.sh](./screenshots/usinfo.png)

---

#### Screenshot 2 — Output of `./user-info.sh`

![Output of `./user-info.sh](./screenshots/usrn.png)

---

### Notes

Answer the following in your own words:

**1. What is a variable in Bash?**

A variable is a container used to store information that can be reused inside a script.
---

**2. Why should we avoid spaces around the `=` sign when creating variables?**

Bash sees it as a command
---

**3. How do you access the value stored inside a Bash variable?**

by adding $
---

# Task 4 — Arrays & Loops: Tools Checklist Script

## Goal

Use arrays and loops to print a checklist of tools used in Bash scripting.

### Evidence

#### Screenshot 1 — Content of `tools-checklist.sh`

![Content of `tools-checklist.sh](./screenshots/arrayc.png)

---

#### Screenshot 2 — Output of `./tools-checklist.sh`

![Output of `./tools-checklist.sh](./screenshots/arrayr.png)

---

### Notes

Answer the following in your own words:

**1. What is an array in Bash?**

An array is a variable that stores multiple values in one place.
---

**2. Why are arrays useful in scripts?**

Arrays make it easier to manage and process multiple related items.
---

**3. What does `"${tools[@]}"` mean?**

It represents all values stored inside the tools array.
---

**4. What is the purpose of the `for` loop in this script?**

It repeats an action for every item inside the array.
---

# Task 5 — Loops: Number Counter Script

## Goal

Use loops to repeat a task multiple times.

### Evidence

#### Screenshot 1 — Content of `counter.sh`

![Content of `counter.sh](./screenshots/conterc.png)

---

#### Screenshot 2 — Output of `./counter.sh`

![Output of `./counter.sh](./screenshots/counterr.png)

---

### Notes

Answer the following in your own words:

**1. What is a loop?**

A loop repeats a set of commands multiple times until a condition is completed.
---

**2. Why do we use loops in Bash scripting?**

They reduce repeated commands and make automation easier.
---

**3. How many times did the loop run in your script?**

5 times.
---

**4. What would you change if you wanted the loop to run 10 times?**

change {1..5} to {1..10}
---

# Task 6 — Files & Conditionals: File Validation Script

## Goal

Use file checks and conditionals to verify whether files and directories exist.

### Evidence

#### Screenshot 1 — Output of `ls -lah ../test-folder`

![ls -lah ../test-folder](./screenshots/test%20folder.png)

---

#### Screenshot 2 — Content of `file-check.sh`

![Content of `file-check.sh](./screenshots/fileC.png)

---

#### Screenshot 3 — Output of `./file-check.sh`

![Output of `./file-check.sh](./screenshots/fileR.png)

---

### Notes

Answer the following in your own words:

**1. What does `-d` check in Bash?**

It checks whether a directory exists.
---

**2. What does `-f` check in Bash?**

It checks whether a file exists.
---

**3. Why should file and directory paths be stored in variables?**

It makes scripts easier to read, modify, and maintain.
---

**4. What happens if the file does not exist?**

The script executes the else statement and displays that the file does not exist.
---

# Task 7 — Conditionals: Pass or Retry Script

## Goal

Use if-else conditionals to make decisions based on a variable value.

### Evidence

#### Screenshot 1 — Content of `score-check.sh` with `score=85`

![Content of `score-check.sh` with `score=85](./screenshots/scoreC.png)

---

#### Screenshot 2 — Output showing `Result: Pass`

![ Output showing `Result: Pass](./screenshots/scoreR.png)

---

#### Screenshot 3 — Content of `score-check.sh` with `score=55`

![Content of `score-check.sh` with `score=55](./screenshots/score1C.png)

---

#### Screenshot 4 — Output showing `Result: Retry`

![Output showing `Result: Retry](./screenshots/score1R.png)

---

### Notes

Answer the following in your own words:

**1. What is the purpose of if-else in Bash?**

It allows scripts to make decisions based on conditions.
---

**2. What does `-ge` mean?**

Greater than or equal to.
---

**3. Why should conditions be tested with different values?**

It ensures the script works correctly in different situations.
---

**4. How can conditionals help in automation scripts?**

They allow scripts to automatically choose actions based on different conditions.
---

# Task 8 — Functions: Final Bash Automation Script

## Goal

Create a final Bash script using functions to organize reusable code.

### Evidence

#### Screenshot 1 — Content of `final-automation.sh`

![Content of `final-automation.sh](./screenshots/finalC.png)

---

#### Screenshot 2 — Output of `./final-automation.sh`

![Output of `./final-automation.sh](./screenshots/systemctl%20status.png)

---

#### Screenshot 3 — Output of `ls -lah` showing all created scripts

![ls -lah` showing all created scripts](./screenshots/script.png)

---

### Notes

Answer the following in your own words:

**1. What is a function in Bash?**

A function is a reusable block of commands that performs a specific task.
---

**2. Why are functions useful in scripts?**

Functions organize scripts, reduce repeated code, and make scripts easier to maintain.
---

**3. Which functions did you create in this script?**

I created show_info, show_tools, and check_file functions.
---

**4. How does this final script combine variables, arrays, loops, conditionals, files, and functions?**

The script uses variables to store values, arrays to store tools, loops to display items, conditionals to check files, and functions to organize reusable tasks.
---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`https://www.linkedin.com/posts/judah-oyekunle-devops-engineer_devops-linux-bash-ugcPost-7483997560722944000-a1qW/?utm_source=share&utm_medium=member_desktop&rcm=ACoAAD1QcSsBayL-iIJCb39J7WoJCnjtf7N2fMA`

---

#### Screenshot — Published LinkedIn post

![Published LinkedIn post](./screenshots/linked3.png)

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

- 🌐 DMI Official Website: https://pravinmishra.com/dmi  
- 🎓 DevOps for Beginners (Udemy): https://www.udemy.com/course/devops-for-beginners-docker-k8s-cloud-cicd-4-projects/  
- 🎓 Agentic AI DevOps with Claude Code: https://www.udemy.com/course/ultimate-agentic-ai-devops-with-claude-code/  
- 🎓 DevOps with Claude Code: Terraform, EKS, ArgoCD & Helm: https://www.udemy.com/course/devops-with-claude-code-terraform-eks-argocd-helm/  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*