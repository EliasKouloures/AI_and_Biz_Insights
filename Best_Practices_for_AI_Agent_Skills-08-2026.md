# 5 Best Practices for AI Agent Skills

---

## Executive Summary

AI Agent Skills are a standardized, lightweight format (as defined by the `agentskills.io` specification) for imparting procedural domain knowledge to LLM agents. While language models already possess enormous amounts of fact-based knowledge, they lack your specific workflow.

However, poorly designed skills lead to context overload, inaccurate results, computational errors, and security risks. This guide shows you how to build robust, high-performing, and secure skills.

---

## Core Architecture of an Agent Skill

An agent skill is based on a simple folder structure:

skill-folder/
├── SKILL.md # Required: YAML metadata + core instructions (<500 lines)
├── references/ # Optional: Detailed documentation (loaded only when needed)
└── scripts/ # Optional: Deterministic code (Python, Bash, etc.)

---

## The 5 Best Practices for AI Agent Skills

### 1. The description is the trigger
* **How it works:** Upon startup, the agent loads *only* the YAML header (`name` and `description`) of all installed skills to conserve context memory. The actual content of `SKILL.md` is not loaded until the skill is triggered.
* **Limitations:**
* `name`: Maximum **64 characters**.
* `description`: Maximum **1,024 characters**.
* **Practical Tips:**
* Describe exactly **WHAT** the skill does and **WHEN** (under what conditions/user intents) it should be used.
* Avoid vague descriptions (e.g., *“Generates compliance reports”*).
* Use precise triggers (e.g., *“Generates the monthly compliance report from internal data. Use when asked for the compliance report or the monthly report.”*).
* **Be slightly “pushy”:** LLMs tend to ignore skills (undertriggering). It’s better to slightly exaggerate the description than to undersell the skill.


### 2. Build on Real Expertise
* **The Pitfall:** If you ask an AI to “write me a skill for X,” you’ll get generic, cliché-filled text (*“Validate the inputs,”* *“Handle errors appropriately.”*).
* **Two paths to real expertise:**
1. **Manual walkthrough:** Walk through the task yourself once and document the exact steps, corrections, and edge cases.
2. **Artifact synthesis:** Extract workflows from existing documents (runbooks, PR feedback, old reports, incident logs).
* **Key takeaway:** Contribute your subject matter expertise and leave only the actual execution (“typing”) to the agent.
* **Required:** Add a dedicated **“Gotchas”** section to the `SKILL.md` file. Document all non-obvious edge cases and environment-specific quirks there—situations where the model would make mistakes without guidance.


### 3. Use the context sparingly (Progressive Disclosure)
* **Problem:** As soon as a skill is triggered, the content of `SKILL.md` appears in the active context window and competes with the system prompt and the chat history.
* **Guidelines:**
* Keep the `SKILL.md` file under **~500 lines (~5,000 tokens)**.
* Do not explain basics that the model already knows (e.g., what a PDF is or how SQL works).
* **Progressive Disclosure Pattern:** Store extensive references, schemas, or instructions in the `references/` folder. The agent will only open these files when it actually needs them during execution.


### 4. Use deterministic scripts for fragile steps
* **Basic rule:** Adapt the style of instructions to the fragility of the step:
* **Flexible/Open:** Instructions in natural language.
* **Fragile/Precise/Math:** Deterministic code (`scripts/`).
* **Implementation:** Place executable scripts in the `scripts/` folder.
* **Instruction in the prompt:** Explicitly tell the agent: *“Run `scripts/script1.py`”*—do not leave the logic up to the model’s improvisation.
* **Advantages:**
* **Saves tokens:** The code does not need to be loaded into the context window.
* **Zero error rate:** Math, data formatting, or reconciliation are executed precisely without any hallucinated logic.


### 5. Check third-party skills before running them
* **Security risk:** Skills can execute code and have access to your local file system, environment variables, and API keys.
* **Audit Results (over 4,000 scanned skills):**
* **>35%** had security vulnerabilities.
* **13%** contained critical threats (prompt injections, data exfiltration, malware).
* **Security rule:** Treat third-party agent skills like unverified software dependencies (npm/pip packages). Manually analyze prompts, scripts, and network calls before executing a skill.

---

## Actionable Checklist

| Area | Checkpoint | Status |
| :--- | :--- | :---: |
| **Trigger** | YAML `name` ≤ 64 characters, `description` ≤ 1,024 characters with clarity on WHAT & WHEN | [ ] |
| **Content** | Based on a real walkthrough/artifacts; includes a “Gotchas” section | [ ] |
| **Context** | `SKILL.md` ≤ 500 lines (~5k tokens); additional documentation moved to `references/` | [ ] |
| **Execution** | Fragile steps & calculations stored as a script in the `scripts/` folder | [ ] |
| **Security**| Third-party skills checked for prompt injections and file access before execution | [ ] |
