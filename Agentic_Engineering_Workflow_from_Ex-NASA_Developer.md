# Agentic Engineering Workflow from Ex-NASA Developer

Insights from Dexter "Dex" Horvath (Founder of Human Layer, Ex-NASA Engineer, pioneer of "Context Engineering") 

---

## Executive Summary

AI coding agents can solve isolated problems efficiently, but letting them run unsupervised leads to maintainability issues, code bloat, and subtle architectural decay. Dexter Horvath argues against fully autonomous "lights-off software factories." Instead, he advocates for an **Agentic Engineering Workflow** anchored by structured program design, vertical slice development, rigorous context engineering, and human-in-the-loop oversight.

---

## Key Takeaways & Core Concepts

### 1. The Flaw of Current AI Coding Benchmarks
* **Static Problem Sets:** Benchmarks like SWE-bench evaluate one-off, static bug fixes in isolation rather than long-term feature evolution.
* **No Penalty for Bad Code ("Slop"):** Reward functions in reinforcement learning (RL) prioritize test pass rates. They do not penalize sloppy architecture, redundant code, or defensive hacks.
* **The "Fast Oracle" Problem:** Unit tests run in seconds, enabling RL loops. However, the cost of bad architecture compounds over weeks or months, making maintainability hard to reward in training.
* **Benchmark Innovations:** Modern benchmarks are beginning to incorporate LLM quality judges, pre-patch verification (checking if agents wrote tautological tests), and functional equivalence scoring.

---

### 2. The Evolution of Software Factories & Why "Lights-Off" Fails
* **Traditional vs. Agentic Factories:** Automated tooling replaces manual coding, reducing build time to minutes. However, code review remains a major bottleneck.
* **The "Lights-Off Factory" Pitfall:** Fully autonomous code generation (without human code reading) leads to codebase degradation. When complex bugs inevitably occur, engineers face weeks of debugging unmaintainable code.
* **Incident & Support Triage:** Highly effective automation routes monitoring alerts (e.g., Sentry, uptime errors) directly to AI agents, which generate instant root-cause reports or draft pull requests.

---

### 3. Dexter’s 4-Stage Agentic Program Design Workflow

To maintain high code quality and reduce review overhead, engineers should spend brief periods upfront defining specifications before letting agents generate code.


┌─────────────────────────────────────────────────────────┐
│ 1. Product & Measurable Goals │
│ • Define user problem, mockups, and target metrics │
└────────────────────────────┬────────────────────────────┘
│
▼
┌─────────────────────────────────────────────────────────┐
│ 2. System Architecture │
│ • Map services, schemas, migrations, & endpoints │
└────────────────────────────┬────────────────────────────┘
│
▼
┌─────────────────────────────────────────────────────────┐
│ 3. Program Design & Call Stack │
│ • Define file structure, types, & method signatures │
└────────────────────────────┬────────────────────────────┘
│
▼
┌─────────────────────────────────────────────────────────┐
│ 4. Vertical Slices ("Tracer Bullets") │
│ • Build & test end-to-end features incrementally │
└─────────────────────────────────────────────────────────┘


1. **Product & Measurable Goals:** Define user problems, write Amazon-style press releases/PRDs, and prototype UIs with raw HTML/mockups. Give agents deterministic metrics (e.g., conversion, performance) to optimize.
2. **System Architecture:** Draft service boundaries, database schemas, and API contracts upfront.
3. **Program Design & Call Stack Mapping:** Explicitly outline file locations, data types, method signatures, call stacks, and test definitions in low-token conversations before code generation.
4. **Vertical Slices (Tracer Bullets):** Agents naturally build horizontally (e.g., full DB layer, then full API, then full UI), making intermediate testing impossible. Force agents to build vertical end-to-end slices (Mock API → Stub UI → Real Endpoint → Business Logic) to verify correctness early.

---

### 4. Context Engineering & The "Dumb Zone"
* **Context Engineering Defined:** Managing exact token selection and context structure to maximize model reasoning quality.
* **Documentation inside the Repository:** Store Architectural Decision Records (`/doc/ADR`) and environment configurations as Markdown files inside the project repository so agents can discover them natively without expensive prompt overhead.
* **The "Dumb Zone" & Context Anxiety:** As context fills (~100k+ tokens), reasoning quality degrades and models exhibit "context anxiety," cutting corners or rushing output.
* **Actionable Remediation:** When reaching high token usage, instruct the agent to summarize current progress into a specification file, then start a clean chat session seeded with that document.

---

### 5. Engineering Mindset & Strategic Focus
* **Identify True Bottlenecks (*The Goal* Principle):** Optimizing code generation speeds is useless if human review, product strategy, or market distribution is the bottleneck.
* **Avoid Tooling Distractions:** Do not waste excessive time building complex agent tooling at the expense of shipping real user value.
* **Agility over Size:** Small teams using structured agentic workflows can out-execute large corporate product teams encumbered by bureaucracy.

---

## Summary Action Plan for Developers

1. **Stop Yolo-Prompting Multi-Thousand Line PRs:** Spend 15–20 minutes defining product specs, API signatures, and call stacks before invocation.
2. **Enforce Vertical Slice Building:** Prompt agents to deliver runnable end-to-end prototypes step-by-step rather than massive horizontal codebase rewrites.
3. **Maintain Repo Context:** Document key architecture decisions (`/doc/ADR/*.md`) directly in the codebase for model context retrieval.
4. **Manage Token Limits:** Compact and reset chat sessions when reaching ~100k tokens to avoid reasoning degradation.
5. **Automate Triage, Keep Code Review:** Automate bug/incident reporting to draft PRs, but retain human understanding of core business logic.

