# Understanding is the new bottleneck

## 1. Executive Summary
As AI agents increasingly write vast amounts of code (e.g., 50,000-line PRs), human engineers face a growing risk of accumulating "cognitive debt". While AI efficiently automates correctness and verification loops, human understanding remains critical for creative participation and systemic ideation. Litt presents three actionable frameworks—Explanations, Micro Worlds, and Shared Spaces—to leverage AI not to remove humans from the loop, but to intentionally deepen their understanding of agent-generated systems.

## 2. Core Philosophy: Why Understanding Still Matters
*   **Beyond Correctness Checking:** The traditional human role of reviewing code strictly for errors (spec matching, architecture, production safety) is decreasing as AI self-verification improves. 
*   **Understanding to Participate:** Maintaining rich conceptual structures in your head allows for fluent recombination of ideas and creative leaps. Without this foundation, engineers lose the ability to actively participate in a project's evolution.
*   **Avoiding "Cognitive Debt":** Popularized by Margaret Storey, this concept parallels technical debt. "Vibe coding" with AI works temporarily, but eventually leads to a complete loss of project comprehension once your understanding degrades.

## 3. Actionable Techniques & Frameworks

### A. Explanations (The "Explain Diff" Skill)
Instead of reviewing raw file diffs, use AI to generate personalized "curriculums" that teach the code change.
*   **Background First:** Direct agents to teach how the broader system works before introducing specific code changes.
*   **Intuition Before Details:** Summarize the core intent and conceptual trick (e.g., "make the garden feel 3D using 2D tricks") before dumping raw code.
*   **Interactive Figures:** Embed manipulatable components to visually demonstrate spatial or logic changes directly in the documentation.
*   **Literate Code Diffs:** Walk through files in a logical teaching sequence with explanatory prose bridging each block.
*   **The "Speed Regulator" Quiz:** Inspired by Andy Matuschak's philosophy that passive reading fails, append a 5-question interactive quiz to the bottom of the explainer. **Rule:** You cannot approve the AI's code for review until you pass the quiz.

### B. Micro Worlds
Use AI to build ephemeral, interactive UIs solely to help you build intuition for complex systems—inspired by Seymour Papert's "Mathland".
*   **Visual Debuggers:** Generate temporary dashboards that visualize state at every step (e.g., a timeline-scrubbing UI to watch an interpreter execute logic step-by-step).
*   **Interactive Migrations:** Instead of running a black-box script to port a codebase, have AI generate a visual step-by-step UI where you click "next" to execute and observe the file movements sequentially.

### C. Shared Spaces
Move AI interactions from isolated local silos into collaborative team environments.
*   **Multiplayer Agent Chat:** Utilize shared threads where multiple humans and multiple agents can discuss context together, analogous to a Slack channel.
*   **Collaborative Documents:** Bring agents into shared workspaces so team members can leave comments on AI-generated plans, ensuring collective team understanding rather than single-developer silos.

## 4. Conclusion
We must return to Alan Kay’s original vision for personal computing from 50 years ago: technology should level up human capabilities, not replace them [00:17:31]. By using AI to create interactive learning environments and custom explanations, developers can achieve a richer, more intuitive understanding of their systems than ever before.
