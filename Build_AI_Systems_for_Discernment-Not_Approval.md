# BUILD AI SYSTEMS FOR DISCERNMENT, NOT APPROVAL

## PROBLEM: COGNITIVE SURRENDER & AUTOMATION BIAS
* **Cognitive Surrender:** Occurs when humans forego deliberation, adopting AI output as their own with minimal scrutiny.
* **Wharton Study Findings:** AI amplified human reasoning (+25% performance) when correct but degraded human performance (-15%) when wrong. Notably, 80% of participants accepted incorrect AI answers.
* **Duolingo Case Study:** Highly trained proctors were secretly shown fake cheating flags. Despite >90% historical accuracy, proctors falsely accepted 50% of fake AI signals (a coin-flip rate), proving severe automation bias.

## SOLUTION: INTERACTION ENGINEERING
Instead of tweaking underlying ML models, tweak interaction loops to break automation bias.
* **Copy Change Intervention:** Guidelines were updated to explicitly state: 1) AI signals are only preliminary alerts. 2) Proctors must find independent video evidence.
* **Result:** Correct rejection rates of fake AI flags increased by 21%.
* **Paradigm Shift:** AI lifecycles are cyclical, not linear: `Model Output -> Interaction -> Human Behavior -> Data/Evals -> Model Improvements`.

## DESIGN PRINCIPLES FOR AI SYSTEMS

### ENGINEER REASONING
* Treat users as investigators, not just validators.
* **Surface Assumptions Early:** Have AI state assumptions before generating large outputs to save tokens & prevent downstream errors.
* **Weigh Trade-offs:** Require AI to present options & reasoning, allowing humans to opine & guide early.

### MATCH FRICTION TO STAKES
* **High-Stakes (e.g., exams, cheating detection):** Build in deliberate friction, speed bumps, & structured review gates. Slow users down to prevent rubber-stamping.
* **Low-Stakes (e.g., casual chat):** Optimize for seamless, frictionless interaction.

### EVERY INTERACTION IS A LABEL
* Do not rely purely on binary "Accept/Reject" logs.
* **Capture Diffs:** If a human clicks "Accept" but manually edits text, capture that delta to prevent polluting datasets with false-positive signals.
* **Track Indirect Metrics:** User questions, follow-ups, & overridden recommendations indicate trust levels & model failures.

### PROACTIVE EVALUATION DESIGN
* Stop asking "How do we evaluate models?" after building them.
* Define concrete success metrics proactively & design UX interactions to natively harvest specific, structured data.

## ACTIONABLE UI/UX PATTERNS
* **Split Compound Prompts:** Separate objective AI facts from subjective human policy decisions. Ask "Are headphones detected?" separately from "Should we flag this user for cheating?" to avoid penalizing valid edge cases (like hearing aids) while retaining accurate visual AI tracking data.
* **In-Line Contextual Feedback:** Avoid dumping overwhelming walls of text. Use highlight-&-hover markup UIs tying actionable feedback directly to specific, small portions of input text.
* **Junior Developer Agent Model:** Do not have AI dump massive, unreviewed code diffs all at once, nor ping users for every single line. Design AI agents to plan, surface design decisions, & deliver meaningful, reviewable chunks.

## KEY TAKEAWAY
Fixes often require engineering interactions natively rather than building better models or adding brute-force human oversight.
