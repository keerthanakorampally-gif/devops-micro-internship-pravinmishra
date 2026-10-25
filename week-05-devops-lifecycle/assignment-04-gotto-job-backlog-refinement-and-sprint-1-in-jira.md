<img width="1920" height="1080" alt="Screenshot (652)" src="https://github.com/user-attachments/assets/2ba3c599-9440-4210-bff7-65760dc0725a" /># Assignment 4 — Gotto Job: Backlog Refinement & Sprint 1 in Jira

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this 90-minute, time-boxed exercise, you will act as a Scrum team — or run in Solo Mode, playing every role yourself — to turn the Gotto Job template into a value-ordered backlog, estimate the work in story points, plan Sprint 1, open the burndown chart, and ship one small UI-only increment (text, color, spacing, a label, or a CTA — no backend changes).

---

# Task 1 — Roles & Mode Setup (Team vs Solo)

## Goal

Choose Team Mode or Solo Mode, and document how each Scrum role (Product Owner, Scrum Master, Dev Lead, DevOps Lead) was handled.

### Evidence

#### Screenshot 1 — Jira "Create project" screen, or the project sidebar after creation

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b075026a-e5f8-4039-aba4-6eddeb373d44" />


### Notes

Write one line for each role: PO (what you prioritized), SM (how you ensured process), Dev Lead (what you built), DevOps Lead (how you shipped).

PO: Prioritized backlog user stories, website navigation updates, and responsive layouts to maximize user value.

SM: Facilitated daily standups, sprint tracking, and retrospectives to maintain Agile momentum and remove blockers.

Dev Lead: Built and polished the DMI website frontend, including navigation headers, hero sections, and custom versioned footers.

DevOps Lead: Shipped updates seamlessly via automated Git workflows and continuous deployment to the AWS EC2 server.


# Task 2 — Create the Jira Project (Team-managed → Scrum)

## Goal

Create a Team-managed Scrum project named `Gotto Job – Team <#>` (Team Mode) or `Gotto Job – <YourName>` (Solo Mode).

### Evidence

#### Screenshot 2 — Project created page showing the project name and key

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f05d5893-2888-41aa-9f74-ee30ec537c63" />


# Task 3 — Create the Epic

## Goal

Create the Epic `Improve Gotto Job UI discoverability & trust` to group the UI improvement initiative.

### Evidence

#### Screenshot 3 — Backlog showing the Epic panel with the Epic visible

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/7931844a-ac29-4938-a1a3-4d907c70990c" />


# Task 4 — Seed the Product Backlog (6–8 Stories + Fibonacci Points + Ranking)

## Goal

Create at least six Stories under the Epic, estimate each with 1, 2, or 3 story points, and rank them by value.

### Evidence

#### Screenshot 4 — Backlog showing the Epic and at least six Stories under it

<img width="1920" height="1080" alt="Screenshot (646)" src="https://github.com/user-attachments/assets/a073b6d8-ad35-4c68-b443-c4317fc78222" />


#### Screenshot 5 — One Story opened showing its Story Points and acceptance criteria filled in

<img width="1920" height="1080" alt="Screenshot (647)" src="https://github.com/user-attachments/assets/6d1e082f-2be5-4b23-a154-85a2fd42fa88" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/07e07d68-d8e8-4153-af23-1c0ee5d8a897" />


# Task 5 — Planning Poker (Estimate + Debate Notes)

## Goal

Confirm the Story Points (1, 2, or 3) for each Story and record brief reasoning for each estimate.

### Evidence

#### Screenshot 6 — Backlog showing Story Points visible, or two or three Stories opened showing their points

<img width="1920" height="1080" alt="Screenshot (649)" src="https://github.com/user-attachments/assets/e3901156-a1af-4f01-a16f-7325ad28933f" />


### Notes

For each story, explain in one or two lines why it is a 1, 2, or 3 (mention any debate, even in Solo Mode).

GJK-2 (Update Hero Section text & CTA buttons) — 1 Story Point
Reasoning: Straightforward text and button link updates on the landing page header. Solo debate: Considered a 2 due to potential styling tweaks, but kept at 1 because it's purely frontend text and primary CTA redirection without complex logic.

GJK-3 (Implement responsive mobile navigation menu) — 2 Story Points
Reasoning: Requires CSS media queries and hamburger menu toggle behavior to ensure usability on mobile devices. Solo debate: Evaluated as a 1 for simplicity, but bumped to 2 to account for testing across different screen resolutions.

GJK-4 (Update primary brand color scheme across UI components) — 1 Story Point
Reasoning: Quick CSS variable update for primary color branding. Solo debate: Quick implementation time, but requires checking all buttons and links for consistency across pages.

GJK-5 (Add user trust badges and partner logos) — 1 Story Point
Reasoning: Simple HTML asset placement and image alignment in the footer/trust section. Solo debate: Low complexity; straight asset integration.

GJK-6 (Optimize landing page images & load speed) — 2 Story Points
Reasoning: Image compression, format conversion (WebP), and layout shift checks. Solo debate: Small scope, but requires verification of performance scores to ensure compliance.

GJK-7 (Add footer version tag and updated links) — 1 Story Point
Reasoning: Low-effort text and hyperlink update in the static footer template. Solo debate: Very minor change, unanimously estimated as a 1.

# Task 6 — Sprint Planning: Create Sprint 1 + Sprint Goal + Scope

## Goal

Create Sprint 1, move three or four Stories into it (approximately 3–6 points), set the Sprint Goal, and break each selected Story into Build, Verify, Deploy, and Screenshot Sub-tasks.

### Evidence

#### Screenshot 7 — Sprint 1 with the selected Stories inside it

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/35facbd0-e335-45ec-b3ed-8f7993958aef" />


#### Screenshot 8 — One Story showing the Sub-tasks created

<img width="1920" height="1080" alt="Screenshot (652)" src="https://github.com/user-attachments/assets/387d3778-7868-4b1a-b218-c5747b3ea610" />




# Task 7 — Reports: Open Burndown Chart

## Goal

Open the Burndown Chart and confirm it exists for Sprint 1. It is acceptable if the chart is not yet populated.

### Evidence

#### Screenshot 9 — Burndown Chart page opened, even if empty

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/67d4c819-1d48-443d-8838-04003bdfb105" />


# Task 8 — Ship One Small Increment (Build + Deploy + Proof)

## Goal

Implement one small UI-only Story from Sprint 1, commit it, deploy it live, and move the Story and its Sub-tasks to Done in Jira.

### Evidence

#### Screenshot 10 — Jira board showing the Story moved to Done

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/1e82c4ae-a288-4b83-8926-f5d8b2b9cad1" />


#### Screenshot 11 — Git commit output

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b0075b37-3e9f-4c18-844c-9053f41ae862" />


#### Screenshot 12 — Live URL in the browser showing the UI change, with the URL visible

<img width="1015" height="667" alt="Screenshot (665)" src="https://github.com/user-attachments/assets/0dc05708-823c-4611-adda-b8effd99817b" />


# Task 9 — Retro Notes (Scrum Pillar + Value)

## Goal

Add a retro comment covering what went well, what to improve, one Scrum pillar observed (Transparency, Inspection, or Adaptation), and one Scrum value (Openness, Focus, Commitment, Courage, or Respect).

### Evidence

#### Screenshot 13 — Jira retro comment visible

Add your screenshot here.

---

# Task 10 — LinkedIn Post (Mandatory)

## Goal

Publish a LinkedIn post about what you delivered, including your live URL, three to five lines on what you did and learned, and one screenshot (Burndown Chart, Sprint board, or the live UI change).

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`Add your URL here`

---

#### Screenshot 14 — Published LinkedIn post

Add your screenshot here.

---

# Submission Instructions

- Add all 14 required screenshots
- Full name must be visible in required screenshots
- Do not expose sensitive information (keys, passwords, account IDs)

---

# Completion Checklist

- [ ] Task 1: Team Mode or Solo Mode selected and all four roles documented (Screenshot 1 & Notes)
- [ ] Task 2: Team-managed Scrum project created with the required name (Screenshot 2)
- [ ] Task 3: UI improvement Epic created (Screenshot 3)
- [ ] Task 4: 6–8 Stories added under the Epic and ranked by value (Screenshots 4 & 5)
- [ ] Task 5: Story Points set (1, 2, or 3) with reasoning recorded (Screenshot 6 & Notes)
- [ ] Task 6: Sprint 1 created with Sprint Goal, 3–4 Stories, and Sub-tasks (Screenshots 7 & 8)
- [ ] Task 7: Burndown Chart opened (Screenshot 9)
- [ ] Task 8: One UI-only increment implemented, committed, deployed, and verified (Screenshots 10–12)
- [ ] Task 9: Retro comment with one Scrum pillar and one Scrum value (Screenshot 13)
- [ ] Task 10: Mandatory LinkedIn post published with the live URL, backlog refinement, Sprint planning, one shipped increment, proof, and Screenshot 14
- [ ] Full Name visible in required screenshots
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
