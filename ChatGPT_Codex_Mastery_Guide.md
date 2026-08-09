# Comprehensive Guide & Knowledge Base: ChatGPT Codex Mastery

## Executive Overview
This guide synthesises the 15 advanced tips, best practices, and power-user workflows for **ChatGPT Codex**. The focus is on automating administrative and technical workflows, optimizing model usage to save quotas, leveraging cross-thread agent communication, using scheduled/long-running autonomous loops, and setting up remote multi-device connections.

---

## The 15 Core Pro-Tips & Actionable Workflows

### 1. Web Browser & Local OS Automation
* **Browser Control:** Codex can autonomously navigate the web, perform multi-step market research, extract data, compare products, and output structured Excel files.
* **Administrative Delegation:** Handles repetitive online administrative tasks such as contacting customer support, requesting refunds, and scanning/archiving inbox emails.
* **Local System Optimization:** Authorise Codex to scan local filesystems, locate unnecessary bloatware, delete temp files, clear system memory, and optimize desktop hardware performance.

### 2. Native Voice Mode & Agent Orchestration
* **Multi-Agent Voice Interface:** Use native voice mode directly within the Codex interface to orchestrate multiple operational background agents hands-free.
* **Asynchronous Multi-Thread Delegation:** Issue complex verbal commands (e.g., *"Spin up a new thread and write a 100-word poem"*). Codex creates a child thread, runs the task in the background, and allows you to continue conversing uninterrupted.

### 3. Web Publishing via ChatGPT Sites
* **One-Click Deployment:** Instantly publish generated content—including interactive web pages, portfolios, documents, slides, and data spreadsheets—to the live web.
* **Inter-Agent Context Sharing:** By default, published sites are private but can be toggled to public. The generated URL can be fed directly to other AI agents as a structured external context source.

### 4. High-Priority Thread Pinning
* **Sidebar Management:** Pin core project workspaces to the top left sidebar using the pin icon or by right-clicking a chat (`Pin Chat`).
* **Focus Retention:** Prevents high-value or long-running operational threads from getting lost in general chat history.

### 5. Strategic Model Selection (GPT-5.6 Tiers)
Match the model tier to task complexity to preserve quota allocations and maximize execution speed:
* **Luna:** Lightweight, ultra-fast, and inexpensive. Ideal for simple tasks, minor formatting, text updates, and scheduled background tasks.
* **Terra:** Balanced middle-tier model for standard, everyday tasks.
* **Sol:** High-capacity flagship model designed for complex, deep-reasoning, and architectural tasks.

### 6. Fine-Tuning Thinking Effort
* **Reasoning Granularity:** For heavy models like **Soul**, manually adjust the thinking effort between *Light*, *Medium*, *High*, *Extra High*, and *Max*.
* **Cost-Efficient Hybrid Strategy:** Build core architectures or complex systems using **Soul** with High/Extra-High reasoning. Hand off fine-tuning, styling, color edits, or copy adjustments to **Luna** to conserve token quota.

### 7. Scheduled Background Tasks
* **Automated Recurring Routines:** Configure recurring background tasks in the `Scheduled` panel to execute daily or weekly (e.g., daily file cleanup, log reviews, uptime monitoring, morning calendar/email briefings).
* **Execution Options:** Run tasks in a **New Chat** (creates a fresh thread per run) or an **Existing Chat** (appends to a single ongoing thread).
* **Quota Optimization:** Set scheduled tasks to run on **GPT-5.6 Luna (Max Reasoning)** to minimize token consumption.

### 8. Native App Plugins & System Integrations
* **Direct Integration:** Connect ChatGPT natively to workspace applications, including Google Drive, Gmail, Google Calendar, GitHub, Notion, Asana, Linear, Dropbox, and PDF parsers.
* **API Accuracy:** Plugins give Codex direct operational awareness of application schemas, eliminating guesswork and preventing errors during file manipulation or email management.

### 9. Custom Workflows via Slash Commands (`/`)
* **Reusable Automation Templates:** Save multi-step prompt routines into custom "Skills" triggered instantly in any chat window using the `/` command.
* **Instant Skill Creation:** Convert any active conversation thread into a permanent skill by prompting: *"Create me a skill from this thread."*
* **Community Skills:** Import pre-built skills published by other users for specialized developer or business workflows.

### 10. Autonomous Long-Running Goals (`/goal`)
* **Persistent Execution Loops:** Trigger autonomous agent loops via `/goal` (or `/go`) that run continuously until a pre-defined condition is met.
* **Goal Types:**
  * **Verifiable Metrics:** Quantitative boundaries (e.g., *"Run until the site performance score reaches 90+"*).
  * **LLM-as-a-Judge:** Qualitative standards (e.g., *"Refine the user experience until it meets professional design standards"*).

### 11. Goal Execution Safeguards & Loop Libraries
* **Execution Boundaries:** Protect token usage and system resources by setting strict time limits on `/goal` commands (e.g., *"Run for a maximum of 3 hours"*).
* **Loop Library Integration:** Import proven loop templates and recipes from the community Loop Library to standardize autonomous long-running tasks.

### 12. Quota Management & Banked Resets
* **Usage Monitoring:** Track weekly limit consumption, usage percentages, and reset dates in `Settings > Usage & Billing`.
* **Banked Resets:** Use platform-granted banked resets to restore quota back to 100% if allocation runs out prior to the scheduled weekly reset. Note that banked resets carry expiration dates.

### 13. Cross-Thread System Awareness & Delegation
* **Global Ecosystem Search:** A single active thread can inspect, search, summarize, and extract information across all other threads in your account.
* **Inter-Thread Task Delegation:** Direct an active thread to pass instructions to another existing thread, trigger sub-tasks, retrieve outputs, and resume execution seamlessly.

### 14. Multi-Environment Code Execution (Local vs. Cloud)
* **Local Execution:** Executes code and tools directly on your host machine.
* **Cloud Execution:** Offloads code execution to cloud sandbox environments, allowing you to run multiple parallel coding agents simultaneously without consuming local hardware resources.

### 15. Remote Desktop Control via Mobile Pairing (`Connections`)
* **Remote Terminal Access:** Enable `Settings > Connections > Control this Mac/PC` and pair a mobile device by scanning the generated QR code.
* **On-the-Go Execution:** Remotely access, monitor, and execute desktop Codex threads, local coding projects, and background agents directly from a mobile phone anywhere in the world.

---

## Technical Matrix: Model & Execution Selection Guide

| Task Complexity | Recommended Model | Reasoning Level | Preferred Execution Mode |
| :--- | :--- | :--- | :--- |
| **System Architectural Design & Core Coding** | GPT-5.6 Soul | High / Extra High | Cloud / Local |
| **Iterative Edits, UI Tweaks, Styling** | GPT-5.6 Luna | Light / Medium | Local |
| **Daily Scheduled Maintenance & Monitoring** | GPT-5.6 Luna | Max Reasoning | Scheduled Background Chat |
| **Long-Running Autonomous Optimization** | GPT-5.6 Soul | High | Autonomous Loop (`/goal`) |
| **Remote Mobile Orchestration** | Any | Variable | Mobile Connections Pair |

---

## Implementation Checklist

- [ ] **Configure Connections:** Pair mobile device to primary desktop instance via `Settings > Connections` for remote access.
- [ ] **Set Up Plugins:** Link primary external apps (GitHub, Google Workspace, Notion, Linear) to enable native actions.
- [ ] **Build Scheduled Automations:** Set up daily morning briefings and automated log/file cleanups using **Luna**.
- [ ] **Standardize Skills:** Convert recurring prompts into slash-command skills (`/`) for rapid retrieval.
- [ ] **Monitor Usage:** Review `Usage & Billing` to verify remaining quota percentages and check for unused banked resets.
