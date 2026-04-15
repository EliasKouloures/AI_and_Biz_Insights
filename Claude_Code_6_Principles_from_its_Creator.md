# The Creator’s Guide to Claude Code: 6 Principles for Maximum Efficiency

This is a comprehensive breakdown of how Boris Cherny, the creator of Claude Code, uses his own tool. Despite having an engineering background, Cherny’s setup is surprisingly "vanilla." His efficiency comes not from complex configurations, but from a strategic, systematic approach to how he interacts with the AI.

Here are the 6 core principles Boris uses to build with Claude Code, complete with actionable workflows and specific prompts you can implement immediately.

---

## 1. Plan Mode: Move Slow to Move Fast
AI is great at solving problems, but it often solves the *wrong* problem if your initial request is vague. Cherny starts **80% of his sessions** in Plan Mode. The goal is to "babysit" Claude *before* it writes any code, locking in the architecture and requirements first. Once a solid plan is established, the actual building becomes almost automatic.

**Actionable Workflow:**
*   **Activate Plan Mode:** Hit `Shift + Tab` twice in your terminal to enter Plan Mode.
*   **Force an Interview:** Instead of just giving instructions, force Claude to ask you questions to uncover gaps in your assumptions.
*   **The Prompt to Use:** 
    > *"Before we start building, interview me about this: What is the core problem this solves? Who is this for? What does success look like? What should this NOT do? Summarize it back to me before we write any code."*

## 2. Keep `Claude.md` Minimal
When a mistake happens, standard practice is to update the `Claude.md` file (Claude's system prompt/cheat sheet) so it doesn't happen again. However, many users over-engineer this, leading to a massive, bloated file filled with contradictory rules that confuse the model. 

Cherny’s philosophy is to do the **minimal possible thing** to get the model on track.

**Actionable Workflow:**
*   **The Nuclear Option:** If your `Claude.md` is thousands of tokens long, delete it and start fresh. Models are constantly improving; the scaffolding you needed 6 months ago might now be built into the base model.
*   **The Maintenance Prompt:** If you are too scared to delete it, run this command periodically to clean it up:
    > *"Update my Claude.md to remove anything that's no longer needed, contradictory, duplicate information, or unnecessary bloat impacting effectiveness."*

## 3. Built-In Verification
Creating a feedback loop where Claude tests its own output can increase the quality of the final result by 2-3x. Instead of you manually testing the code and reporting back, give Claude the tools to verify it itself. 

**Actionable Workflow:**
*   **Provide Tools:** Tell Claude how to verify. E.g., "Start the server and verify the endpoint responds," or "Run these tests and confirm they pass."
*   **For Non-Code Tasks:** "Review this against my brand guidelines and flag anything that doesn't match."
*   **Update `Claude.md`:** Add this specific line to your `Claude.md` file to automate this process:
    > *"Before you do any work, mention how you could verify that work."*
*   **The Sanity Check Prompt:** After a long session of building, use this prompt:
    > *"Please go back and verify all your work so far. Make sure you used best practices, were efficient, and didn't introduce any issues."*

## 4. Multiply Yourself (Parallel Sessions)
Do not force one Claude session to do everything. Cherny advocates for spinning up multiple Claude sessions running in parallel. 

**Why this works:** Two context windows that don't know about each other tend to produce better results. If you pile too many different tasks into one session, the context gets "foggy" and the model starts making obvious mistakes. 

**Actionable Workflow:**
*   **Partition Tasks:** Treat different sessions like different employees. Have one session solely focused on data analysis, and a completely fresh session focused on building a UI component. 
*   **Start Fresh Often:** If a model is struggling, starting a brand new window with zero context baggage is often faster than trying to untangle the current session.

## 5. Systemize Your "Inner Loop"
Your "inner loop" consists of the repeatable tasks you do multiple times a day. Cherny uses **Slash Commands** and **Claude Skills** to document these processes so he never has to write the same prompt twice.

Think of a Skill as a documented playbook. Instead of explaining *how* to generate a specific report every time, you document the exact steps once as a Skill.

**Actionable Workflow:**
*   **Use Claude Skills:** Create specific skills for repetitive tasks (e.g., `/generate-weekly-report`). AI will execute the exact documented steps every time you call it, just referencing new data.
*   **The Discovery Prompt:** If you aren't sure what to automate, ask Claude:
    > *"Based on the project I'm working on, what Claude Skills should I create?"*

## 6. Build for the Future (Don't Over-Engineer)
**"Never bet against the model."** A common mistake is spending hours writing highly optimized, complex prompts to fix minor model behaviors. Because AI models are improving at a rapid pace, a more general, smarter model released next month will likely render your hyper-specific micro-tweaks obsolete.

**Actionable Workflow:**
*   **Stop Optimizing Prompts:** You don't need a perfectly optimized prompt; you just need to give the AI clear direction.
*   **Build an Information Moat:** Shift your energy away from prompt engineering and toward building your "information moat"—the quality of the context, data, and documentation you are feeding into the model. Focus on improving your systems, not hacking the current model's quirks.
