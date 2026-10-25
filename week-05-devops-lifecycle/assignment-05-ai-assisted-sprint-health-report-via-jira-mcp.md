# Assignment 5 — AI-Assisted Sprint Health Report via Jira MCP

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will connect Claude Code to your Jira board through an MCP server, the same way you connected it to GitHub in Week 2, and build a read-only `/sprint-health` skill. The skill reads your current sprint through Jira's API and reports sprint velocity, stories at risk of missing the sprint, and items missing an estimate — but it must never create, edit, comment on, or transition a single ticket itself. You will prove that boundary holds by making a real change on the board yourself and confirming the skill only ever reports, never acts.

---

# Task 1 — Create a Jira API Token

## Goal

Generate an API token from your Atlassian account that the MCP server will use to authenticate with your Jira site. Do not screenshot the token value itself.

### Evidence

#### Screenshot 1 — Jira API token creation confirmation page showing the token name, with the token value not visible

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/33c9afa3-da57-4dfb-834e-14793bf1bec7" />


### Notes You Must Write (Very Important):

Why does the MCP server need your site URL and account email in addition to the token?

Account Identification / Username: The account email identifies who is making the request and links the operation to your specific user profile within the organization or cloud workspace.

Workspace / Tenant Routing: The site URL (e.g., your unique Atlassian instance domain) tells the client where to direct the API requests. Because cloud services often host thousands of separate customer tenants on the same base domain, the specific URL ensures that queries and commands reach your correct organization workspace rather than a generic or incorrect endpoint.

Authentication and Authorization: While the token provides the secure cryptographic credentials (secret) to prove you are authorized, the email and site URL provide the necessary context to know whose account is acting and which specific cloud instance or environment to target.

# Task 2 — Create .mcp.json at the Project Root

## Goal

Create or update `.mcp.json` at your project root with a Jira MCP server block, following the same shape as the GitHub MCP server you configured in Week 2.

### Evidence

#### Screenshot 2 — `.mcp.json` open in VS Code showing the Jira server configuration

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/a6486d2b-a559-4d69-82b4-e3a66f7554b5" />


### Notes You Must Write (Very Important):

Compare this jira block to the github block from Week 2 Assignment 5. The GitHub server ran via npx (a Node.js package); this one runs via uvx (a Python package) — what stays exactly the same shape despite that difference, and why doesn't Claude Code care which language a given MCP server is written in?

What stays exactly the same shape:
The core structural JSON schema (mcpServers, server key names, and environment variable passing) remains identical. Regardless of whether the underlying executable is launched via Node.js (npx) or Python (uvx), the configuration format defined in .mcp.json always wraps the server execution command and its arguments inside the same standard mcpServers object dictionary.

Why Claude Code doesn't care which language the MCP server is written in:
Claude Code communicates with all MCP servers through the standardized Model Context Protocol (MCP), which operates via standard input/output (stdio) or JSON-RPC message passing over standard streams. Because the protocol abstracts away the underlying implementation details, Claude Code treats every server as a uniform tool provider—sending JSON-RPC requests and receiving structured tool definitions and responses, entirely agnostic of whether the server code is written in TypeScript/Node.js, Python, Go, or any other language.

# Task 3 — Add Your Credentials to settings.local.json

## Goal

Add your Jira site URL, account email, and API token to `.claude/settings.local.json`, and confirm that file is listed in `.gitignore` so it is never committed.

### Evidence

#### Screenshot 3 — `settings.local.json` open in VS Code showing the `env` section, with the actual token value blurred or covered

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/6f8805fa-2a21-4d0d-8339-19ecc832495f" />


### Notes You Must Write (Very Important):

Why must JIRA_API_TOKEN live in settings.local.json and never in .mcp.json?

Separation of Team Configuration vs. Personal Credentials: .mcp.json is checked into version control (GitHub) to define the shared server setup and structure for the entire team, whereas settings.local.json contains personal environment variables and user-specific credentials.

Security & Preventing Secret Leaks: Putting secret tokens like JIRA_API_TOKEN in .mcp.json would commit them directly to your public or team GitHub repository, exposing sensitive credentials to anyone with access to the codebase.

Gitignore Protection: settings.local.json is explicitly gitignored (.gitignore) so that personal tokens remain strictly local on your machine and are never accidentally tracked, pushed, or leaked.

# Task 4 — Verify the Connection with /mcp

## Goal

Restart Claude Code and confirm the Jira MCP server shows as connected.

### Evidence

#### Screenshot 4 — `/mcp` output showing `jira: connected`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2e625b10-b22d-4319-b058-55452a33548f" />


# Task 5 — Run a Live Query to Prove Real Board Data

## Goal

Ask Claude to list the issues in your current active sprint through the Jira MCP connection, and confirm the result matches what you see on your live board in the browser.

### Evidence

#### Screenshot 5 — Claude's response showing the live sprint issue list retrieved via Jira MCP

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/bac0f57d-21c8-4231-a04f-3e6da0a92b94" />


### Notes You Must Write (Very Important):

How did you confirm this was real board data and not something Claude guessed?

Add your answer here

---

# Task 6 — Build the /sprint-health Skill

## Goal

Create a `/sprint-health` skill restricted to read-only Jira tools plus `Read`, with no issue-mutating tools and no `Write`. Run it and confirm it produces a report covering sprint velocity, at-risk stories, and items missing an estimate.

### Evidence

#### Screenshot 6 — `SKILL.md` frontmatter showing `allowed-tools` limited to read-only Jira tools plus `Read`, with `disable-model-invocation: true`

Add your screenshot here.

#### Screenshot 7 — `/sprint-health` output showing the full triage report against your real sprint

Add your screenshot here.

### Notes You Must Write (Very Important):

1. Which Jira MCP tools does this skill's allowed-tools list include, and which mutating tools (create issue, update issue, transition issue, add comment) does it deliberately exclude?

Add your answer here

2. Why does a Scrum Master need this restriction more than almost any other role in this course?

Add your answer here

---

# Task 7 — Prove the Skill Never Mutates the Board

## Goal

Manually update one ticket on your board in the browser (for example, move a story to "Done" or add a missing estimate), then run `/sprint-health` again and confirm the new report reflects your change — proving the skill only ever reads live state and never wrote to the board itself.

### Evidence

#### Screenshot 8 — Second `/sprint-health` run showing the report now reflects your manual board change

Add your screenshot here.

### Notes You Must Write (Very Important):

Map this assignment to Gather → Analyze → Human Act → Verify from Week 3 Assignment 6. Which step did you perform manually in the browser, and why must that step stay human?

Add your answer here

---

# Submission Instructions

Complete all tasks in sequence.

Your submission must include:
- All 8 required screenshots
- All the required notes

---

# Completion Checklist

- [ ] Task 1: Jira API token created, value never screenshotted (Screenshot 1)
- [ ] Task 2: `.mcp.json` has the Jira server block (Screenshot 2)
- [ ] Task 3: Credentials stored in `settings.local.json`, token blurred, file gitignored (Screenshot 3)
- [ ] Task 4: `/mcp` shows the Jira server connected (Screenshot 4)
- [ ] Task 5: Live query returned real sprint data, verified against the browser (Screenshot 5)
- [ ] Task 6: `/sprint-health` skill created with correct read-only `allowed-tools`, and produced a full report (Screenshots 6–7)
- [ ] Task 7: A manual board change was reflected in a second `/sprint-health` run (Screenshot 8)
- [ ] Skill never created, edited, transitioned, or commented on any issue
- [ ] Reflection answered (Notes)
- [ ] No API token value exposed

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
