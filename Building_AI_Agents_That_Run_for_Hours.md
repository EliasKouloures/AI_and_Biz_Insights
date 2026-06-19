# 🧠 Building AI Agents That Run for Hours

## 1. 🎯 EXECUTIVE SUMMARY
Building autonomous AI coding agents capable of continuous, multi-hour operation requires co-evolving foundational LLM with a robust architectural scaffold (harness). Overcoming inherent LLM limitations—such as context rot, poor multi-step planning, and self-evaluation blindness—is best achieved through an adversarial, multi-agent architecture (Planner, Generator, Evaluator) that persists state to a file system rather than relying solely on context window.

---

## 2. 🚧 3 CORE BOTTLENECKS OF LONG-RUNNING AGENTS
Before implementing solutions, it is crucial to understand why base models fail when running autonomously for extended periods:

* **Context Management Failures:** 
    * *Amnesia:* Loss of historical context when starting fresh sessions.
    * *Context Rot:* Degradation of logical coherence as context window fills.
    * *Context Anxiety:* Model rushes to complete tasks prematurely when approaching token limits.
* **Planning Deficiencies:** Models attempt to "one-shot" entire applications, resulting in half-baked features, orphaned UI elements, or running out of context mid-build.
* **Self-Evaluation Blindspots:** LLMs are inherently sycophantic. They exhibit "generosity bias" toward their own outputs, frequently rubber-stamping broken code or hallucinated backend logic as "complete."

---

## 3. 🏗️ STATE-OF-THE-ART HARNESS ARCHITECTURE
To build complex applications (e.g., a fully functional retro game engine) autonomously, Anthropic utilizes a highly structured, adversarial loop.

### A. Planner Role
* Takes a vague, single-line human prompt and breaks it down into a high-level sprint spec.
* **Critical Constraint:** Planner deliberately avoids mapping out granular technical details. Over-specifying upfront leads to cascading architectural errors that compound over a multi-hour run.

### B. Adversarial "Generator-Evaluator" Pattern
Shamelessly inspired by GANs (Generative Adversarial Networks), this isolates generation and critique into separate context windows.
* **Contract Negotiation:** Before writing any code, Generator and Evaluator agents negotiate via markdown files on disk to define what "done" actually means. They iterate back and forth until they agree on exact, granular, and actionable test assertions.
* **Harsh Evaluation:** Evaluator does not just read code diffs; it actively uses tools (like Playwright) to navigate live UI, take screenshots, and test physics/logic. 
* **Overcoming Sycophancy:** While tuning a Builder to be self-critical is nearly impossible, tuning a standalone Critic agent to be ruthlessly harsh is highly tractable. Out of box, Claude is a poor QA agent and requires heavy, aggressive system prompting to overcome its generosity bias.

### C. Grading Subjective Quality ("Taste")
Subjective concepts like UI design are fully gradable if explicitly defined.
* **Rubric:** Use a strict 4-point criteria: *Design, Originality, Craft, Functionality*. 
* **Preventing "AI Slop":** Weight rubric heavily toward Design and Originality to penalize generic AI outputs (e.g., defaulting to purple gradients). 

---

## 4. 📈 HARNESS EVOLUTION VS. MODEL CAPABILITY
As frontier models improve, required scaffolding simplifies. Frontier shifts, and harness must adapt:
* **Evolution of Endurance:** Opus 3.7 maxed out at 1 hour of autonomous coding. Opus 4.6 can maintain coherence for 12+ hours with a minimal scaffold.
* **Dropping Redundancy:** Previous setups (like those for Opus 4.5) required constant context resets and rigid sprint decompositions. With Opus 4.6, models can hold 2-hour continuous builds in a single session, relying purely on server-side token compaction. 

---

## 5. 🛠️ ACTIONABLE ENGINEERING BEST PRACTICES
For developers building their own long-running agent workflows:

1.  **Self-Evaluation is a Trap:** Never ask a model to grade its own code within same context window. Always separate generator and critic.
2.  **Filesystem State > Context State:** Decouple agent memory from context window. Use local JSON/Markdown files to log progress, state, and learnings. This allows harness to completely reset or swap models mid-run without losing structural progress.
3.  **Compaction Over Summaries:** Lossy summarization handoffs between agents cause rapid conceptual drift. Rely on structured document handoffs or context compaction.
4.  **Embrace Deterministic Looping:** Adopt patterns similar to "Ralph Wiggum loop"—feeding instructions into a CLI continuously. It is better to fail predictably than to succeed unpredictably.
5.  **Read Traces Manually:** Ultimate debugging loop for agent engineering is not automated evals, but sitting down and reading full agent transcripts manually. Empathizing with model's missteps is only reliable way to patch harness prompts.
