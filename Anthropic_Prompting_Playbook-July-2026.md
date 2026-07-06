# 📘 Anthropic Core Team's Prompting Playbook: Comprehensive Summary

This guide breaks down Anthropic’s official methodology for prompt engineering, focusing on evaluating, migrating, and optimizing prompts for complex agentic workflows.

## 🛠 CORE PHILOSOPHY: EVAL-DRIVEN OPTIMIZATION
You cannot reliably improve a prompt without an evaluation framework. Evals provide the rigor needed to determine if a change actually moved the needle or just shifted the failure to another area.

### 1. Build a Robust Eval Set
* **Control Cases:** Standard inputs that should *always* pass to catch broad regressions.
* **Edge Cases & Policy Boundaries:** Inputs that have historically caused issues or test the limits of your rules.
* **Must-Escalate / Must-Refuse Cases:** Inputs the model explicitly should *not* attempt to handle itself.
* *Mechanics:* Use a one-line pass criterion or an automated LLM-as-a-judge (model grader) for each test.

### 2. The Iterative Workflow
1.  **Establish a Baseline:** Run the existing prompt against the eval set.
2.  **Change ONE Thing at a Time:** Isolate variables to understand the exact impact of your edits.
3.  **Run Full Eval Set:** Re-run *all* tests after every single change, as fixes often cause regressions elsewhere.
4.  **Repeat Until Green.**

---

## 🏗 SCENARIO 1: Fixing a Degraded Legacy Prompt
**The Problem:** An existing production prompt has accumulated months of disorganized patches and rules ("prompt rot"). When migrating to a new model, performance unexpectedly degrades.

### Phase 1: Hygiene & Structure (Prompting 101)
Before tweaking logic, clean the prompt's architecture.
* **Assign a Clear Role & Task:** Define exactly who the AI is and what it is doing.
* **Use XML Tags:** Clearly separate `<instructions>`, `<data>`, `<policy_doc>`, and `<tone>`. This helps the model map relationships and allows you to curate information easily.
* **Strip Cruft:** Remove redundant or obvious instructions.
* *Result:* Often fixes simple formatting or retrieval failures immediately.

### Phase 2: Output Contracts
* Define exactly how the model should respond using layout tags (e.g., `<output_format>`).
* Force the model to wrap its final user-facing response in specific tags (e.g., `<reply>`) to make parsing programmatic, safe, and deterministic for your backend.

### Phase 3: Targeted Failure Analysis & Tool Use
**The Symptom:** The model fails at complex logic (e.g., calculating prorated billing).
* **Diagnosis:** LLMs are inherently bad at precise mathematical logic based on complex, conflicting textual rules.
* **The Solution (Reasoning + Tools):** 1. Give the model a `<reasoning>` or `<scratchpad>` block to "think" before answering.
    2. Offload the calculation to an API/Tool. Explicitly instruct the model: *"Use the `calculate_proration` tool—do not estimate it yourself."*

### Phase 4: Re-balancing Defensive Prompting
**The Symptom:** The model refuses to escalate issues or acts overly cautious (e.g., trying to solve a billing dispute itself instead of transferring to a human).
* **Diagnosis:** Old patches (e.g., *"Avoid escalating because it costs $8"*) accumulate and contradict main goals. Newer models take these defensive instructions very literally, causing "instruction-following over-caution."
* **The Solution:** Rewrite negative constraints into balanced, objective-based rules.
    * *Bad:* "Avoid transferring to a Care Specialist unless absolutely necessary."
    * *Good:* "Escalations cost $8, but a wrong answer on a dispute costs a refund + customer trust. Route any mention of a dispute to a Care Specialist. Do not attempt to explain it."

---

## 🤖 SCENARIO 2: Building a Complex Agent from Scratch
**The Problem:** Building a scheduling agent with strict constraint-satisfaction rules (e.g., 8 employees, no "clopens", specific shift availability).

### The Progression of Prompting Complexity
1.  **Simple Prompt:** Fails entirely (0/5 passes). LLMs struggle with zero-shot hard constraint satisfaction.
2.  **Larger Model (e.g., Opus):** Still fails (0/5 passes). Brute intelligence isn't enough to solve combinatorial logic.
3.  **Adaptive Thinking (Extended Reasoning Tokens):** Improves significantly (3/5 passes), but at a very high latency and token cost.
4.  **Structured Prompt:** Adding XML tags and itemizing rules explicitly improves adherence, but still doesn't achieve perfection.
5.  **The Ultimate Fix: Generate ➔ Evaluate ➔ Repair (Self-Correction Loop)**
    * Do not rely on the LLM to get it right on the first try.
    * Build a deterministic Python script/evaluator to check the LLM's generated schedule against your hard rules.
    * If rules are violated, feed the exact `violations_found` back into the prompt dynamically and ask the LLM to repair its previous output.
    * *Result:* Perfect score (5/5 passes) reliably and efficiently.

---

## ⚡ SUMMARY OF ACTIONABLE BEST PRACTICES (TL;DR)
1.  **Never optimize without an Eval Suite.** You are flying blind without one.
2.  **Use XML Tags extensively** for structuring prompts (strict separation of concerns).
3.  **Give models space to think.** Always utilize a `<reasoning>` block before final outputs.
4.  **Don't force LLMs to do math or hard lookups.** Pass them tools/APIs.
5.  **Audit your prompts for "Defensive Debt."** Remove outdated, hyper-specific negative constraints that confuse newer, more instruction-obedient models.
6.  **For strict constraints, use code to verify.** Implement a programmatic `Generate -> Evaluate -> Repair` loop rather than relying on perfect zero-shot text generation.
