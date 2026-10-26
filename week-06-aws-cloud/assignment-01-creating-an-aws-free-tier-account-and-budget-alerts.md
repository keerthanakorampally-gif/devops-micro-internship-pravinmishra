# Assignment 1 — Creating an AWS Free Tier Account & Setting Up Budget Management and Alerts

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will create your own AWS Free Tier account and configure budget management with cost alerts. This is an important first step: it lets you follow along with the rest of the course, and the alerts help ensure you do not exceed your budget.

---

# Task 1 — Sign Up for AWS and Access the Console

## Goal

Create your AWS Free Tier account, select the Basic Support Plan (Free), and log in to the AWS Management Console.

> yes I created my AWS free tier account

# Task 2 — Create a Monthly Cost Budget with Alerts

## Goal

In the Billing Dashboard, create a monthly Cost Budget with a name, amount, and start month, then configure alert thresholds (e.g. 50%, 80%, 100%) and a notification email address.

### Evidence

#### Screenshot 1 — AWS Budget setup page showing the budget name, budget amount, and alert thresholds

<img width="1920" height="1080" alt="Screenshot (698)" src="https://github.com/user-attachments/assets/04575a0f-cc26-43ac-81c2-a724bc68fa2a" />
<img width="1920" height="1080" alt="Screenshot (699)" src="https://github.com/user-attachments/assets/ab9b2f6a-8adc-4a35-8422-963ce085684c" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d759afc4-501d-4ebf-bed9-ff442b11a4a6" />


### Notes

Answer the following in your own words:

**1. Why is it important to set up budget alerts when using an AWS account?**

Prevents Unexpected Billing Spikes: Cloud services operate on a pay-as-you-go model. Automated processes, misconfigured services, or forgotten resources (such as active EC2 instances or unattached EBS volumes) can accumulate high charges very quickly without real-time monitoring.

Proactive Risk Mitigation: Budget alerts notify you (via email or SNS) as soon as spending breaches a specific percentage (e.g., 50%, 80%, or 100%) of your monthly threshold. This allows you to inspect and terminate unintended resources before incurring heavy costs, rather than discovering a high bill at the end of the month.

Ensures Free Tier and Internship Safety: For developers, students, and interns, budget alerts help ensure that resource usage stays strictly within expected free-tier allowances or designated project budgets, preventing out-of-pocket expenses.

Early Detection of Security Incidents: A sudden, unexpected surge in resource utilization can indicate a security breach—such as compromised IAM credentials being used to run unauthorized resource mining or compute workloads. Cost alerts act as an early-warning diagnostic tool for security anomalies.

Encourages Operational Accountability: Setting cost and usage boundaries fosters financial discipline and encourages proper resource lifecycle management (e.g., shutting down sandbox environments when not in use).

# Submission Instructions

- Add the required screenshot in your submission
- Do not expose sensitive billing, card, identity, or account information

---

# Completion Checklist

- [✅] AWS Free Tier account created and Basic Support Plan (Free) selected
- [✅] Logged in to the AWS Management Console
- [✅] Monthly Cost Budget created with name, amount, and start month
- [✅] Budget alert thresholds and notification email configured
- [✅] Screenshot captured showing budget name, amount, and thresholds (Screenshot 1)
- [✅] Notes question answered
- [✅] No sensitive billing or account information exposed

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
