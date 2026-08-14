# Anthropic's CCA Exam as a Field-Guide for Agentic Engineering

**Speaker:** Frank Coyle (UC Berkeley Computer Science Professor)

**Context:** Breaking down the new Claude Certified Architect (CCA) exam to extract practical patterns and anti-patterns for Agentic AI development.

---

## 1. EXECUTIVE SUMMARY
The transition to Agentic AI requires shifting from simple sequential prompting to robust, loop-driven architectures. Frank Coyle leverages Anthropic's Claude Certified Architect (CCA) exam as a practical field guide to building reliable AI systems. His core thesis emphasizes that understanding architectural **anti-patterns** (what *not* to do) is the single most critical path to mastering agentic engineering.

## 2. CORE CONCEPTS & PHILOSOPHY
* **The "Make" Philosophy:** "Nothing is a mistake... experiment, experiment, experiment." (Sister Corita Kent). Hands-on building is non-negotiable.
* **The Power of Loops:** Drawing on the 1966 Böhm-Jacopini theorem (which proved sequence + selection + iteration = Turing complete), Coyle asserts that **loops** are the definitive unlock for modern AI. Loops bring Turing completeness to LLM workflows, moving them beyond static prompts.
* **Anti-Patterns as Guides:** Just as Object-Oriented Programming required "design patterns" in the 90s, the agentic era requires *agentic patterns* and *agentic anti-patterns* to prevent systemic failures like runaway context windows or agent groupthink.

## 3. CLAUDE CERTIFIED ARCHITECT (CCA) EXAM OVERVIEW
* **Logistics:** Scenario-based, timed, and proctored. Available to individuals for $99 (retake allowed once every 6 months).
* **Format:** Multiple-choice, but heavily grounded in rigorous, realistic constraints across 6 production scenarios (the exam randomly selects 4 to test you on).
* **The 5 Exam Domains:**
  1. **Agentic Architecture:** (27%)
  2. **Claude Code Configuration & Workflows:** (20%)
  3. **Prompt Engineering:** (Focus on JSON output structuring)
  4. **Tool Design & Model Context Protocol (MCP) Integration**
  5. **Context Management & Reliability**

---

## 4. THE AGENTIC SCENARIOS: PATTERNS VS. ANTI-PATTERNS

### Scenario 1: Customer Support Resolution (The Agentic Loop)
* **Anti-Pattern:** Letting the agent generate a response and blindly trusting/using that raw output.
* **Pattern (The `while` loop):** Build a loop relying on the `stop_reason`. 
* **Mechanism:** LLMs are probabilistic next-word predictors—they *cannot* execute tools natively. They only format parameters for *your code* to execute.
* **Actionable Rule:** Always evaluate the `stop_reason` (e.g., `tool_use` or `out_of_tokens`). If the model stops because it wants to use a tool, run the tool locally, feed the result back, and continue the loop. Have a human-in-the-loop escalation protocol for low-confidence outputs.

### Scenario 2: Code Generation with Claude
* **Anti-Pattern:** A single, monolithic set of instructions for the entire codebase.
* **Pattern:** Hierarchical `.claude.md` markdown files.
* **Mechanism:** Anthropic recommends a 3-tier rule hierarchy:
  1. Top-level project rules.
  2. Rules inside specific project folders.
  3. Rules inside specific sub-directories.

### Scenario 3: Multi-Agent Research System
* **Anti-Pattern 1 (The "Handyman"):** Creating a single "God Agent" overloaded with every available tool (akin to hiring a carpenter who brings plumbing and electrical tools and claims they can do it all).
* **Anti-Pattern 2 (Context Spillover):** Letting a sub-agent's context leak into the main orchestrator's context, wasting tokens/money and degrading LLM accuracy.
* **Pattern 1 (Strict Specialization):** Give agents exactly 1-2 specialized tools. Apply single-responsibility principles.
* **Pattern 2 (Combating Groupthink):** When utilizing a "Critic Agent", pass *only* the claim and the evidence. Do *not* pass the previous agent's "chain-of-thought" or reasoning processes. Agents are highly susceptible to sycophantic "groupthink" and will agree with previous agents if they see their reasoning.

### Scenario 4: Developer Productivity & Subtask Isolation
* **Anti-Pattern:** Allowing every subtask to dump its full logs/output into the primary thread, leading to unbounded context growth.
* **Pattern (Fork & Summate):** Fork the sub-agent into an isolated thread. Once finished, generate a dense *summary* of the task and append *only the summary* back to the overriding main context.
* **Pattern (Context Compaction):** Actively monitor token counts. If passing a threshold (e.g., >150,000 tokens), execute custom context compression logic or rely on built-in compaction algorithms before continuing the loop.

### Scenario 5: Continuous Integration (CI) with Claude Code
* **Anti-Pattern:** Leaving interactive modes enabled in automated CI pipelines (causes the agent to stall endlessly waiting for human permission).
* **Pattern (Headless Execution):** Configure Claude to run strictly straight-through for CI/CD pipelines.
* **Cost Optimization (Batch API):** If immediate results aren't needed (e.g., overnight log analysis), package automated tasks into the Batch API for a 50% token cost reduction, guaranteed within 24 hours.

---

## 5. ACTIONABLE CHECKLIST FOR AGENTIC ENGINEERS
- [ ] **Shift from Sequential to Loop-Based Thinking:** Base your orchestrator logic on `while` loops triggered and governed by model `stop_reasons`.
- [ ] **Never Trust Agent Tool Execution:** Code your orchestrator to intercept `tool_use` parameters, execute the tool securely in your own environment, and feed the raw result back into the agent's loop.
- [ ] **Enforce Principle of Least Privilege:** Strip sub-agents of extraneous tools; restrict them to single-responsibility functions.
- [ ] **Sanitize Context Handoffs:** Blind "Critic Agents" to previous agents' inner monologues to force independent, un-biased evaluations.
- [ ] **Implement Context Compaction:** Set a hard token limit script that automatically triggers summarization/compaction on your main thread to prevent context degradation and save money.
- [ ] **Use Hierarchical Configs:** Set up layered `.claude.md` files that map directly to your repository's physical architecture.
