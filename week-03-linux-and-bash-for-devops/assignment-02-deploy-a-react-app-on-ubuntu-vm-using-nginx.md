# Assignment 2 — Deploy a React App on Ubuntu VM Using Nginx

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will deploy a React application on an Ubuntu EC2 instance and serve it using Nginx. You will provision a Linux server, install the required tools, personalize the application with your details, and verify that it is publicly accessible via a browser.

---

# Task 1 — Setup Environment (Node.js & npm)

## Goal

Install Node.js and npm on the Ubuntu VM and verify the installation.

### Evidence

#### Screenshot 1 — Output of `node -v && npm -v` showing installed versions

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f8ec0b76-91e9-4d60-9afa-ee3dd7a4b8c9" />


---

# Task 2 — Setup Environment (Nginx)

## Goal

Install Nginx, start the service, and confirm it is running.

### Evidence

#### Screenshot 2 — Output of `systemctl status nginx --no-pager` showing Active (running)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2c755c1f-ee53-4bc4-a4b5-3f3453551209" />


---

# Task 3 — Clone React Application

## Goal

Clone the project repository and verify the project files are present.

### Evidence

#### Screenshot 3 — Output of `ls` inside the `my-react-app` directory showing project files

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f7386e1f-ebe5-4866-91af-6ef0caabe788" />


---

# Task 4 — Modify Application (Personalization)

## Goal

Update `App.js` with your full name and the current date.

### Evidence

#### Screenshot 4 — `nano App.js` open showing your full name and date filled in

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2a361569-22c1-418b-9552-e1ca183a6e23" />


---

# Task 5 — Build React Application

## Goal

Install dependencies and generate the production build.

### Evidence

#### Screenshot 5 — Output of `ls` inside `my-react-app` showing the `build/` folder generated

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/bd9bffe9-0a6b-46b9-b632-a2cb2e32f59d" />


---

# Task 6 — Deploy React Build to Nginx Web Root

## Goal

Copy the production build files to the Nginx web root directory.

### Evidence

#### Screenshot 6 — Output of `ls /var/www/html/` showing the deployed build contents

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/181c9223-5205-4c41-aa8f-53d9c0e6f661" />


---

# Task 7 — Configure Nginx for React Application

## Goal

Apply Nginx configuration for React routing and confirm the service is active.

### Evidence

#### Screenshot 7 — Output of `systemctl is-active nginx` showing `active`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/87b84a8c-a282-4d8c-837e-4087d0564d19" />


---

#### Screenshot 8 — Output of `cat /etc/nginx/sites-available/default` showing the Nginx config
<img width="1920" height="1080" alt="Screenshot (227)" src="https://github.com/user-attachments/assets/3b259b2c-ec69-4106-9e9e-80c5b7c179c8" />


---

# Task 8 — Test Deployment

## Goal

Verify the React application is publicly accessible via the server's public IP.

### Evidence

#### Screenshot 9 — Output of `curl ifconfig.me` showing the server's public IP address

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/865b555e-a9b8-4fa9-8f0d-69cbdd4982bb" />


---

#### Screenshot 10 — Browser showing the deployed React app at `http://<public-ip>` with your name and date visible

<img width="1920" height="1080" alt="Screenshot (251)" src="https://github.com/user-attachments/assets/52a09ab2-8190-429c-aead-9ba3bc3399c1" />


---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

https://lnkd.in/p/dNU3iRwZ

---

#### Screenshot — LinkedIn post showing the deployed application

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e5d8a298-fcac-4647-84be-d053f92cb02c" />


---

# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- Do not expose sensitive information (keys, passwords, account IDs)

---

# Completion Checklist

- [✅] Node.js and npm installed and verified (Screenshot 1)
- [✅] Nginx installed and running (Screenshot 2)
- [✅] Repository cloned and files verified (Screenshot 3)
- [✅] App.js updated with full name and date (Screenshot 4)
- [✅] Production build generated (Screenshot 5)
- [✅] Build files deployed to Nginx web root (Screenshot 6)
- [✅] Nginx configured and active (Screenshots 7 & 8)
- [✅] Public IP retrieved (Screenshot 9)
- [✅] React app accessible in browser with personal details visible (Screenshot 10)
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
