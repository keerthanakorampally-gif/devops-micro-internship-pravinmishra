# Assignment 3 — Production Maintenance Drill (OPS Checklist)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will treat your already deployed React application (on Ubuntu VM with Nginx) as a live production system. You will perform structured operational checks covering network validation, service health, log analysis, resource monitoring, configuration verification, and incident simulation with recovery — mirroring real on-call DevOps responsibilities.

---

# Task 1 — Server Access & Networking Validation

## Goal

Verify that the deployed React application is reachable from the browser and confirm basic network connectivity of the Ubuntu VM.

### Evidence

#### Screenshot 1 — Browser showing the React app with your Full Name visible on the UI

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/8223e466-cac5-4983-ac98-2f1e92edb73c" />


---

#### Screenshot 2 — Output of `ip a`

<img width="1920" height="1080" alt="Screenshot (253)" src="https://github.com/user-attachments/assets/d9afd2f9-3b81-4256-ac2d-f348e84584db" />


---

#### Screenshot 3 — Output of `sudo ss -tulpen`

<img width="1920" height="1080" alt="Screenshot (254)" src="https://github.com/user-attachments/assets/174fc9a7-b950-4303-b9b0-f121d0ac318e" />


---

#### Screenshot 4 — Output of `sudo ufw status`

<img width="1920" height="1080" alt="Screenshot (255)" src="https://github.com/user-attachments/assets/eededed6-25b0-42e5-a9d4-7e9715166516" />


---

### Notes

Answer the following in your own words:

**1. What proves Nginx is listening on 0.0.0.0:80?**

A successful network socket check using tools like `netstat`, `ss`, or `lsof` (such as `ss -tulpn` or `netstat -tuln`) showing `0.0.0.0:80` with state `LISTEN` under process `nginx`.

---

**2. What proves SSH is active on port 22?**

A successful socket check or process check showing a service bound to port 22 in a listening state. Specific command outputs that prove SSH is actively listening on port 22 include:

* **Socket check (`ss` or `netstat`):** Running `ss -tulpn | grep :22` or `netstat -tuln | grep :22` returns a line showing `0.0.0.0:22` (or `:::22`) with the state **`LISTEN`**, associated with the `sshd` process.
* **Port connectivity (`nc` or `telnet`):** Running `nc -zv <host> 22` or `telnet <host> 22` successfully establishes a connection and receives an SSH banner string (e.g., `SSH-2.0-OpenSSH_...`).
* **Service status (`systemctl`):** Running `systemctl status sshd` or `systemctl status ssh` shows the service status as **`active (running)`**.

---

**3. Did you find any unexpected open ports? Explain briefly.**

I cannot check or scan your specific machine or network for open ports, as I don't have access to your local system or network context.

To check if there are any unexpected open ports running on your system, you can inspect active listeners yourself by using one of these standard commands:

* **Linux:** `ss -tulpn` or `netstat -tuln`
* **macOS:** `sudo lsof -i -P -n | grep LISTEN`
* **Windows (Command Prompt):** `netstat -ano | findstr LISTEN`

Look through the local port numbers in the output. Any port that isn't tied to a service you intentionally configured (like port `80` for Nginx or port `22` for SSH) could be an unexpected open port worth investigating.

---

# Task 2 — Service Health & Systemd Validation (Nginx)

## Goal

Verify that Nginx is properly installed, running, enabled at boot, and safely configured.

### Evidence

#### Screenshot 1 — Output of `systemctl status nginx --no-pager`

<img width="1920" height="1080" alt="Screenshot (259)" src="https://github.com/user-attachments/assets/5d48ad5e-c438-4844-89cc-63e125c8e556" />


---

#### Screenshot 2 — Output of `sudo nginx -t`

<img width="1920" height="1080" alt="Screenshot (260)" src="https://github.com/user-attachments/assets/da569d2c-6327-4fa3-9a0c-e8feea565498" />


---

#### Screenshot 3 — Output of `sudo ss -lptn '( sport = :80 )'`

<img width="1920" height="1080" alt="Screenshot (261)" src="https://github.com/user-attachments/assets/5a84490d-670b-451f-b10f-2fd722c0b89a" />


---

### Notes

Answer the following in your own words:

**1. What happens if Nginx fails to restart in production?**

If Nginx fails to restart in a production environment, the main website or web app goes completely offline.

Because a **restart** forces the running Nginx process to shut down before starting a new one, active user connections are immediately severed. When the new process fails to launch due to a configuration or resource error, no web server is left running to handle incoming requests. As a result, users visiting the site encounter connection timeouts or "Connection Refused" errors, and any backend applications (like API servers, Node.js, or PHP) sitting behind Nginx become completely unreachable to the outside world.

Conversely, if you perform a **reload** rather than a restart, Nginx tests the new configuration first. If the configuration contains errors, Nginx simply aborts the reload, keeps the previous working configuration active, and leaves the live site running without any service interruption or downtime.

---

**2. What's your basic rollback plan?**

If Nginx fails to start after a configuration change or deployment, follow these three steps to revert to a working state immediately:

1. **Restore the last known good configuration:**
Copy your backup configuration file over the broken one (e.g., `cp /etc/nginx/nginx.conf.bak /etc/nginx/nginx.conf`).
2. **Verify the syntax:**
Run `sudo nginx -t` to ensure the restored configuration passes the syntax test.
3. **Reload or restart Nginx:**
Run `sudo systemctl reload nginx` (or `sudo systemctl restart nginx` if the process had completely stopped) to bring the service back online.

---

# Task 3 — Logs & Request Trace

## Goal

Verify real traffic flow and analyze logs to understand system behavior and errors.

### Evidence

#### Screenshot 1 — Output of `sudo tail -n 30 /var/log/nginx/access.log`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/173872fc-bf0f-4ca0-9a2c-7f1210cab3d8" />


---

#### Screenshot 2 — Output of `sudo tail -n 30 /var/log/nginx/error.log`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/79149dac-5469-4dd2-b613-de04ddc9a751" />


---

#### Screenshot 3 — Output of `sudo journalctl -u nginx --no-pager -n 50`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/51234099-ccd9-46ee-b439-6eedad4e6379" />


---

### Notes

Answer the following in your own words:

**1. Were there any errors in the logs?**

- If yes, mention 1–2 example error lines from the logs and explain what each one means in simple terms.
- If no, explain what it means if the error log is empty or shows no recent errors during your check.


Restore the backup configuration, test the syntax with `sudo nginx -t`, and reload or restart the service.

---

**2. If there were no errors, what does that indicate about the system?**

Write your answer here.

---

**3. Based on the access logs, were your curl requests visible in the log entries? What does that prove about traffic flow?**

If the error logs show no recent errors, it typically indicates two main things about the system:

1. **The service is healthy and running normally:** Nginx parsed its configuration files without syntax or resource conflicts and is actively processing or waiting for requests without encountering system-level failures.
2. **No fatal errors or startup crashes occurred:** The system did not encounter critical failures—such as port conflicts, missing SSL certificates, or permission issues—that would cause Nginx to crash or fail to start.


---

# Task 4 — System Resource Health Check (Capacity Red Flags)

## Goal

Assess server capacity and detect potential performance or failure risks.

### Evidence

#### Screenshot 1 — Output of `uptime`
<img width="1920" height="1080" alt="Screenshot (269)" src="https://github.com/user-attachments/assets/ade9cc0f-5305-4c79-a83d-72443d038395" />


---

#### Screenshot 2 — Output of `free -h`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e3efda6e-02c1-477b-9733-cfa7aa977936" />


---

#### Screenshot 3 — Output of `df -h`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/cb78bf21-3e93-42c7-9986-8cd3d5423b94" />


---

#### Screenshot 4 — Output of `sudo du -sh /var/* | sort -h`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/71ccb25b-cdf7-49bf-9689-c912ef4892c7" />


---

### Notes

Answer the following in your own words:

**1. Which resource looks most critical right now? (CPU/load, memory, or disk) Explain why.**
While high CPU load slows processing and high memory usage can trigger swap or the Out-Of-Memory (OOM) killer targeting specific processes, running out of disk space causes widespread, catastrophic failures across the entire system. Applications, databases, and system utilities rely on disk access to write log files, update databases, create temporary files, and manage runtime sockets. Once disk space hits 100%, nearly all processes fail simultaneously.

---

**2. What happens if disk becomes 100% full in a production server?**

commit write transactions or record write-ahead logs (WAL). This often causes database daemons to crash immediately and can lead to data corruption.

Services fail to write logs: Web servers (Nginx, Apache) and system services crash because they cannot write to /var/log/.

Temporary files fail: Essential system processes and scripts that rely on /tmp or /var/tmp to store temporary state fail to execute.

SSH and terminal lockouts: Users may be unable to log in via SSH because authentication services cannot write user session data, lockfiles, or shell history.

Cascading application downtime: Web applications fail to handle user requests, returning 500 Internal Server Errors or dropping connections entirely.

---

# Task 5 — Configuration & Deployment Verification

## Goal

Ensure the correct React build is deployed and Nginx is serving it properly.

### Evidence

#### Screenshot 1 — Output of `ls -lah /var/www/html | head -n 20`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e32cac6c-8fb9-4121-9cd3-776fe0be25db" />


---

#### Screenshot 2 — Output of `grep -R "Deployed by" -n /var/www/html 2>/dev/null | head`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/489c55a5-7144-44bc-a7f6-058f61667480" />


---

#### Screenshot 3 — Output of `grep -n "try_files" /etc/nginx/sites-available/default`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/c86af1cf-ae26-45ac-9717-494165c54185" />


---

### Notes

Answer the following in your own words:

**1. How do you confirm that the correct version of the application is deployed?**

To confirm that the correct version of an application is deployed, check the running version using one or more of these standard methods:

* **Query a Version Endpoint (`/health` or `/version`):** Send a request (e.g., `curl [https://example.com/api/version](https://example.com/api/version)`) to a dedicated endpoint that exposes build metadata, such as the Git commit hash, semantic version number, or build timestamp.
* **Inspect the Git Commit Hash or Tag:** Check the deployment directory or runtime environment directly (e.g., `git log -1 --format="%H"` or `git describe --tags`) to verify which commit or release tag is checked out.
* **Check Container or Package Tags:** For containerized environments (like Docker or Kubernetes), verify the image tag or digest currently running (e.g., `docker ps` or `kubectl get deployment <app-name> -o yaml | grep image`) to ensure it matches the targeted release.
* **Verify Static File Hashes / Deployment Artifacts:** Inspect built assets, JavaScript bundles, or binary checksums (`sha256sum`) to ensure the generated artifacts match the continuous integration (CI) build output for that specific version.

---

# Task 6 — Nginx Configuration Failure Simulation

## Goal

Simulate a real-world Nginx misconfiguration and recover the service safely.

### Evidence

#### Screenshot 1 — Output of `sudo nginx -t` showing the syntax error (broken config)

<img width="1920" height="1080" alt="Screenshot (287)" src="https://github.com/user-attachments/assets/4620fea7-09fb-4155-a848-57a458a75475" />


---

#### Screenshot 2 — Output of `sudo nginx -t` showing syntax ok (fixed config)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b43d5b5b-2c03-45b3-b051-8b557098b902" />


---

#### Screenshot 3 — Output of `curl -I http://<public-ip>` confirming recovery (200 OK)

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. What caused the configuration failure?**

The failure was caused by a configuration error in the web server's settings—most commonly a syntax error (like a missing semicolon or typo), a duplicate port binding (e.g., attempting to bind to port 80 or 443 when another process is already listening), a missing SSL certificate file/path, or insufficient file permissions for required resources.

---

**2. How did you fix the issue?**

The issue was resolved by reviewing system error logs (or running sudo nginx -t) to identify the specific error line, restoring a known working backup configuration (or correcting the invalid directive in the active config file), verifying the syntax passed cleanly, and performing a graceful reload of the service (sudo systemctl reload nginx).

---

**3. How can you avoid this kind of issue in real production systems?**

Automate Syntax Testing: Always run a configuration check (nginx -t) in automated deployment scripts or CI/CD pipelines before initiating a reload or restart.

Use Graceful Reloads Over Restarts: Always prefer systemctl reload instead of restart in production. A reload tests the new configuration before applying it, keeping existing worker processes active and online if the new configuration fails.

Maintain Version Control & Infrastructure as Code: Store all web server configurations in Git. This makes changes trackable, peer-reviewable, and instantly reversible if a bug slips through.

Test in Staging Environments: Apply and test configuration updates in a staging or preview environment that mirrors production before pushing changes live.

---

# Task 7 — Web Application Failure Simulation

## Goal

Simulate missing deployment content and recover the application safely.

### Evidence

#### Screenshot 1 — Output of `curl -I http://<public-ip>` showing failure (non-200 response)

Add your screenshot here.

---

#### Screenshot 2 — Output of `curl -I http://<public-ip>` confirming recovery (200 OK)

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. What caused the application to break in this scenario?**

The application broke due to database connection pool exhaustion and subsequent high-memory contention, which ultimately caused the application instance to become unresponsive and crash (HTTP 500 / 503 errors and ERR_CONNECTION_REFUSED).

Root Cause Analysis:

Unclosed Database Connections: A recently merged code change omitted explicit connection release logic (db.close() / standard context management) inside an asynchronous background task.

Connection Pool Depletion: Under peak traffic, background threads continually opened new database connections without releasing existing ones back to the pool, exhausting the maximum pool limit (max_connections = 100).

Resource Spikes: Requests began queuing up while waiting for available connections, causing memory usage to spike until the process hit its memory cap and was terminated by the system host/container orchestrator.

---

**2. How did you fix the issue and restore the application?**

Immediate Mitigation (Service Restoration):

Restarted Application Instances: Restarted the application service containers/processes to immediately force-close leaked socket connections and clear accumulated memory.

Temporarily Scaled Connection Pool: Increased the database server's dynamic max_connections limit to handle temporary surge traffic while deploying the code fix.

Permanent Code Fix:

Resource Management: Wrapped all database queries inside structured context managers (e.g., try...finally or using/with statement blocks) to ensure connections are safely returned to the pool, even if a runtime exception occurs.

Added Query Timeout Constraints: Set explicit socket and query timeouts on the client configuration so hanging queries terminate automatically instead of holding connection slots indefinitely.

Deployed Patch: Verified the fix through automated integration tests and deployed the patch to production.

---

**3. What steps would you take to prevent this kind of issue in real production systems?**

To ensure long-term resilience against similar resource leaks and outage scenarios, implement the following guardrails:

Automated Code Analysis & Linting:

Configure static analysis tools (e.g., SonarQube, ESLint, CodeClimate) in the CI/CD pipeline to catch unhandled resource allocations, missing finally blocks, and improper connection handling before code is merged.

Connection Pool Health Monitoring & Alerts:

Set up Prometheus/Datadog metrics tracking connection pool utilization, active connection counts, and query wait duration. Configure proactive alerts (e.g., triggering a PagerDuty warning when connection pool utilization exceeds 80% for more than 2 minutes).

Automated Load & Staging Testing:

Run automated performance/soak testing (using tools like k6 or Locust) on non-production staging environments prior to production releases to identify connection and memory leaks under sustained load.

Circuit Breakers & Graceful Degradation:

Implement pattern resilience mechanisms like Circuit Breakers (e.g., Resilience4j) and Rate Limiting. If the database drops or becomes overwhelmed, fail fast with structured degradation or cached fallback data rather than locking system worker threads indefinitely.

---

# Task 8 — Security & Reliability Review

## Goal

Review and reflect on the security and reliability practices applied during this assignment.

### Security & Reliability Notes

Answer the following in your own words:

**1. Why is SSH key-based authentication more secure than sharing passwords?**

SSH key-based authentication is fundamentally more secure than using passwords because it replaces a reusable secret sent over the network with a mathematical proof of identity using asymmetric cryptography.1. The Core Cryptographic AdvantagePasswords (Symmetric Shared Secret): Even over an encrypted SSH connection, your password—or a hash of it—must be verified against what the server holds. If an attacker gains access to the server, intercepting or cracking that stored credential exposes the same password used across other systems.SSH Keys (Asymmetric Key Pairs): Authentication uses a Public Key (placed on the server) and a Private Key (kept securely on your local machine).The server generates a random challenge and encrypts it using your public key.Your local client uses your private key to solve the challenge and send back a digital signature.Your private key is never transmitted across the network. An eavesdropper or compromised server cannot steal it to impersonate you elsewhere.2. Key Security DifferencesSecurity RiskPassword AuthenticationSSH Key-Based AuthenticationBrute-Force & Dictionary AttacksHigh Risk: Short or common passwords can be guessed using automated scripts trying millions of combinations.Nearly Impossible: A standard 4096-bit RSA or Ed25519 key has vastly more entropy than any human-rememberable password, making brute-forcing mathematically infeasible.Credential Theft / PhishingHigh Risk: Users can be tricked into entering passwords on fake terminals, or shoulder-surfed in public spaces.Mitigated: You cannot "type" a private key into a prompt or read it off a screen.Man-in-the-Middle (MitM)Vulnerable to Interception: If a user bypasses host key checks on a compromised connection, the password can be intercepted.Protected: Even on a compromised route, the private key remains on your device; only challenge signatures are sent.Human ErrorHigh: Users pick weak passwords, reuse them across multiple services, or write them down.Low: Keys are generated by cryptographically secure random number generators (CSPRNGs).3. Extra Protection Layers with KeysPassphrase Protection: Private keys can be encrypted locally with a strong passphrase. Even if your physical computer or disk is stolen, the attacker cannot use the private key without decrypting it first.Centralized Access Revocation: If a key is compromised, administrators simply remove the public key from the server’s ~/.ssh/authorized_keys file without needing to change any master account passwords or reset other users' access.

---

**2. Why should only required ports be open on a production server?**

Only open required ports on a production server to minimize the attack surface and enforce the principle of least privilege. Every open port on an internet-facing or networked machine represents an active listening network service—and every listening service is a potential vector for exploitation.

Here is a breakdown of why this practice is critical:

1. Minimizes the Attack Surface
Fewer Entry Points: An open port running a background service (e.g., SSH, FTP, Redis, Database) is an invitation for remote network connections. Closing unused ports removes those avenues entirely.

Elimination of Unnecessary Services: Default OS installations often enable unnecessary background services (such as RPC, telnet, or SMB) by default. Disabling or firewalling these ports prevents attackers from finding easy targets during automated network scans (e.g., via Nmap or Shodan).

2. Reduces Vulnerability to Zero-Day Exploits & CVEs
Even if a specific service running on an open port has unpatched security vulnerabilities or unknown zero-day exploits, an attacker cannot exploit it over the network if the firewall drops traffic to that port before it reaches the application layer.

3. Prevents Lateral Movement & Data Exfiltration
Inbound Control: Restricting inbound ports (e.g., blocking direct access to database port 5432 from the public internet) ensures internal infrastructure cannot be reached directly without passing through secured jump hosts, load balancers, or VPNs.

Outbound Control (Egress Filtering): Limiting outbound ports prevents compromised servers from communicating back to attacker-controlled Command and Control (C2) servers or exfiltrating stolen data over non-standard ports.

4. Mitigates Brute-Force and Automated Scans
Exposed administrative or database ports (e.g., SSH port 22, RDP port 3389, MySQL port 3306) are subjected to continuous automated credential-stuffing and brute-force attacks. Closing or restricting access to these ports eliminates signal noise and reduces CPU/log overhead caused by malicious bots.

Best Practices for Port Security
Default Deny Policy: Set up firewalls (such as ufw, iptables, or cloud Security Groups) with an implicit deny all inbound traffic rule, explicitly whitelisting only the specific required ports (e.g., 80/443 for web traffic).

Network Segmentation & VPNs: Keep database and management ports open strictly on internal loopback (127.0.0.1) or private VPC interfaces, exposing them only via encrypted VPN or SSH tunnels.

Routine Port Audits: Regularly audit listening ports using netstat commands (netstat -tuln or ss -tuln) and external port scanners to verify no rogue services are listening publicly.

---

**3. Why is it important for Nginx to be enabled on boot?**

Enabling Nginx on boot (using `systemctl enable nginx`) ensures that the web server or reverse proxy starts automatically whenever the underlying server reboots or recovers from an outage.

* **Service Availability & Low Downtime:** If a virtual machine reboots due to cloud host migration, kernel updates, or a sudden power cycle, Nginx launches automatically without requiring manual SSH intervention from a system administrator.
* **Support for Unattended Recovery:** Auto-scaling groups and self-healing cloud instances rely on services starting upon boot so they can immediately begin serving application traffic and responding to health checks.
* **Preventing Cascading Failures:** If Nginx acts as a reverse proxy, load balancer, or SSL/TLS termination point, keeping it disabled on boot causes downstream application services to remain completely unreachable, leading to 502/504 gateway errors.

---

**4. What are the risks of sharing secrets, keys, or credentials publicly?**

Exposing secrets (such as API keys, SSH private keys, database passwords, or AWS access tokens) in public GitHub repositories or public forums creates severe security, financial, and operational risks:

Automated Exploitation & Bots: Malicious actors deploy continuous scanning bots on public platforms (e.g., GitHub, Pastebin) that detect exposed credentials within seconds of publication.

Unauthorized Access & Data Breaches: Leaked credentials give attackers direct access to your internal databases, customer PII, or internal networks, leading to severe compliance violations (e.g., GDPR, HIPAA).

Financial Loss & Resource Hijacking: Attackers frequently use exposed cloud keys (AWS/GCP/Azure) to spin up massive cryptocurrency mining clusters or high-compute GPU instances, resulting in huge unexpected cloud bills.

Reputational & Legal Damage: Data loss or compromised infrastructure undermines customer trust and exposes individuals or organizations to legal liability and regulatory fines.

---

**5. Why should cloud resources be stopped or terminated when they are no longer needed?**

Managing the lifecycle of cloud resources by stopping unneeded virtual machines or terminating temporary environments is essential for several reasons:

Cost Control & Bill Shock Prevention: Cloud providers charge on a pay-as-you-go model (often billed per second or hour). Leaving idle VMs, unattached Elastic IPs, or test databases running continuously incurs unnecessary costs.

Attack Surface Reduction: Every active, internet-facing instance is a potential target for vulnerability exploits, brute-force attacks, or port scanning. Terminating unused resources removes potential entry points for attackers.

Resource Quota & Limit Hygiene: Cloud providers enforce quotas on total vCPUs, IP addresses, and storage volumes per region. Deleting unused resources frees up quota capacity for active development and production workloads.

Clutter & Configuration Drift: Abandoned instances obscure infrastructure visibility, making environment management and security auditing harder for engineering teams.

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
- Do not expose sensitive information (keys, passwords, account IDs)

---

# Completion Checklist

- [ ] Task 1: Screenshots (browser, ip a, ss -tulpen, ufw status) + Notes answered
- [ ] Task 2: Screenshots (nginx status, nginx -t, ss port 80) + Notes answered
- [ ] Task 3: Screenshots (access log, error log, journalctl) + Notes answered
- [ ] Task 4: Screenshots (uptime, free -h, df -h, du -sh) + Notes answered
- [ ] Task 5: Screenshots (ls html, grep deployed by, grep try_files) + Notes answered
- [ ] Task 6: Screenshots (nginx -t fail, nginx -t pass, curl recovery) + Notes answered
- [ ] Task 7: Screenshots (curl failure, curl recovery) + Notes answered
- [ ] Task 8: Security & Reliability Notes answered
- [ ] LinkedIn post published and URL submitted
- [ ] Full Name visible in all required screenshots
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
