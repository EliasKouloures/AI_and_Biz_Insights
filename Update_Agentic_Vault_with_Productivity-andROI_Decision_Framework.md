# Update my Agentic Vault with a Productivity & ROI Decision Framework

You are working inside my existing Agentic Vault.

Your task is to **integrate a durable decision framework for prioritizing customer work, backlog items, bugs, automations, AI use cases, product ideas, and internal improvements**.

Do not merely summarize this prompt. Inspect the existing vault structure and **actually update the appropriate Markdown files and agent instructions** so that future agents use this framework when making recommendations or prioritization decisions.

## 1. Preserve the existing Vault

Before editing:

- Inspect the existing structure, including files such as `CLAUDE.md`, `AGENTS.md`, customer folders, project files, backlog files, TODO files, strategy documents, and existing system/agent instructions.
- Preserve existing customer information, project context, terminology, conventions, and source-of-truth files.
- Do not duplicate large policy blocks across many files if one canonical guideline plus references is cleaner.
- Prefer minimal, coherent edits over unnecessary restructuring.
- Never mix confidential information between customers.
- Customer-specific recommendations must always use only the context available for that customer.

If a suitable strategy/guidelines file already exists, extend it.

Otherwise create a canonical file with an appropriate name such as:

`Productivity-and-ROI-Decision-Framework.md`

or place it in the Vault's existing strategy / operating-system / guidelines area.

Then add concise references to it from relevant agent instruction files such as `CLAUDE.md` and/or `AGENTS.md`.

---

# 2. Core mental model

Use the following model whenever evaluating work.

There are three distinct productivity layers:

## Layer 1 — Individual / Management Productivity

Question:

> How can a person perform an existing information task faster or more easily?

Examples:

- writing emails faster
- summarizing documents
- creating presentations
- generating reports
- drafting text
- helping a developer write code faster
- speeding up research
- assisting a manager with information processing

This can be valuable, but it often improves a person **inside an unchanged workflow**.

Do not automatically equate faster individual work with meaningful business productivity.

---

## Layer 2 — Operational Productivity

Question:

> How can the actual value-producing workflow of the organization become faster, cheaper, more reliable, more scalable, or more automated?

Examples:

- reducing manual steps in a customer workflow
- automating case handling
- removing recurring operational bottlenecks
- eliminating handoffs
- integrating AI directly into a production workflow
- reducing errors or rework
- shortening cycle time
- allowing the same team to serve more customers
- turning previously manual processes into software-driven processes
- enabling a product or service that could not economically exist before

This is usually the **higher-leverage technology investment**.

A technology embedded directly into value creation is generally more strategically important than a technology that merely helps employees perform surrounding information work faster.

Use this as an important default prior:

> Prefer improving the business system over merely making people inside the existing system faster.

But treat this as a heuristic, not a dogma.

---

## Layer 3 — Judgment / Management Effectiveness

Question:

> Are we working on the right thing in the first place?

Examples:

- deciding which customer problem deserves attention
- choosing which AI use case should be built
- deciding what NOT to build
- identifying the actual bottleneck
- allocating engineering or consulting capacity
- killing low-value projects
- selecting the workflow where automation has the greatest leverage
- deciding where human judgment must remain
- recognizing that a proposed optimization addresses the wrong problem

This layer determines **where Layers 1 and 2 should be applied**.

As AI makes execution cheaper, good judgment becomes increasingly important.

Therefore:

> Better execution of the wrong task is not productivity.

And:

> Before optimizing a workflow, verify that the workflow or outcome itself is worth optimizing.

---

# 3. Primary decision principle

When evaluating backlog items, customer requests, bugs, ideas, automations, or AI use cases, reason in this order:

### Step 1 — Outcome

What customer, user, operational, or business outcome are we trying to improve?

Avoid evaluating tasks solely by how interesting or technically sophisticated they are.

### Step 2 — Bottleneck

What currently limits that outcome?

Examples:

- human labor
- latency
- missing information
- poor UX
- errors
- coordination
- integration gaps
- unreliable software
- lack of automation
- decision quality
- adoption
- organizational constraints

Do not optimize a non-bottleneck unless there is another compelling reason.

### Step 3 — Productivity layer

Classify the opportunity primarily as:

- `L1 Individual Productivity`
- `L2 Operational Productivity`
- `L3 Judgment / Management Effectiveness`

Some initiatives may span multiple layers.

State the dominant layer.

### Step 4 — Leverage

Ask:

> Does this merely accelerate an existing task, or does it remove / redesign part of the workflow?

Prefer, all else equal:

`workflow redesign`
>
`workflow automation`
>
`task automation`
>
`task assistance`

Do not force automation where human judgment creates meaningful value.

### Step 5 — ROI

Evaluate expected value relative to implementation and maintenance cost.

---

# 4. Prioritization framework

When useful, score candidate work from 1–5 on the following dimensions.

Do not pretend the scores are precise measurements. They are structured judgment aids.

## Positive factors

### A. Direct customer / business impact

Does this materially improve:

- customer value
- revenue
- retention
- conversion
- service quality
- mission impact
- strategic differentiation

### B. Operational leverage

How directly does this improve the organization's actual value-producing workflow?

High score:

- core workflow changes
- end-to-end process improvement
- important bottleneck removal

Low score:

- isolated convenience
- cosmetic optimization
- minor personal productivity

### C. Frequency / volume

How often does the problem or task occur?

Prefer fixing a 5-minute problem occurring 10,000 times over a 60-minute problem occurring twice, unless strategic impact says otherwise.

### D. Time / cost saved

Estimate meaningful recurring savings.

Think in:

`frequency × effort per occurrence × number of affected people`

### E. Error / risk / rework reduction

Does the work reduce:

- failures
- support burden
- manual corrections
- quality issues
- operational risk
- repeated debugging
- downstream rework

### F. Cycle-time reduction

Does it shorten the time from request → delivered outcome?

Especially valuable when latency itself harms customers or blocks downstream work.

### G. Scalability

Does this allow substantially more work or customers without proportional increases in headcount or complexity?

### H. Reusability

Can the capability, pattern, component, learning, or automation be reused:

- elsewhere for the same customer
- across multiple projects
- across multiple customers
- inside the Vault's future workflows

### I. Strategic / learning value

Will solving this teach us something important, validate an assumption, unlock future opportunities, or create an option with asymmetric upside?

---

# 5. Negative factors

Also evaluate:

### J. Implementation effort

Engineering / consulting / coordination effort.

### K. Ongoing maintenance

Consider:

- API dependencies
- brittle integrations
- model maintenance
- data pipelines
- monitoring
- support
- prompt maintenance
- operational ownership

### L. Risk and uncertainty

Examples:

- unclear user need
- unreliable AI behavior
- security/privacy concerns
- compliance constraints
- dependency risk
- poor data quality
- adoption risk

### M. Workflow disruption

A technically good solution can have negative ROI if it creates excessive organizational friction.

---

# 6. Default prioritization heuristic

When comparing otherwise similar opportunities, prefer work with:

**high customer/business impact  
× high frequency  
× high operational leverage  
× high scalability**

and

**low implementation + maintenance effort**

A useful conceptual model is:

`Priority ≈ Expected recurring value × confidence / total lifecycle cost`

Do not treat this as literal accounting unless real data exists.

Use ranges and assumptions when necessary.

---

# 7. Special rule for AI / LLM use cases

Do not prioritize an AI use case merely because an LLM can perform the task.

Ask:

> Where does the AI sit in the workflow?

Distinguish:

### AI Assistant

Human → AI → Human continues workflow

Example:

AI drafts an email.

Usually Layer 1.

### AI-Enhanced Task

Human performs a real operational task with AI assistance.

Example:

Support employee uses AI to diagnose a customer issue.

Potential Layer 1 + Layer 2.

### AI-Integrated Workflow

AI is directly embedded into the operational system.

Example:

Incoming support case → classify → retrieve context → propose/execute action → update systems → escalate only exceptions.

Primarily Layer 2.

### AI-Native Workflow / Product

The workflow or product would be economically or practically impossible in its current form without AI.

Potentially highest strategic leverage.

Therefore:

> Do not stop at "give everyone an AI copilot."

Always ask whether the workflow itself can be redesigned around AI.

At the same time, do not automate for automation's sake.

Human judgment, trust, UX, reliability, and economics remain constraints.

---

# 8. Special rule for bug prioritization

Do not rank bugs only by technical severity.

Estimate business impact.

Consider:

`Bug ROI ≈ frequency × affected users × business impact × downstream friction / fix effort`

High-priority bugs often include bugs that:

- block important workflows
- occur frequently
- affect many users
- damage customer trust
- cause repeated support work
- generate manual workarounds
- create downstream errors
- prevent adoption
- make important automation unreliable
- disproportionately consume engineering or consulting time

A technically ugly bug with little real-world impact may be lower priority than a small bug repeatedly disrupting a core customer workflow.

Also consider whether the bug reveals a **systemic design problem** rather than treating every symptom independently.

---

# 9. Special rule for backlog / TODO prioritization

For each meaningful backlog item, try to identify:

- desired outcome
- affected customer/user
- current pain
- frequency
- current workaround
- estimated value
- dominant productivity layer
- bottleneck addressed
- implementation effort
- recurring benefit
- dependencies
- confidence
- next smallest useful step

Avoid giant undifferentiated TODO lists.

Where appropriate, group work into:

- `Must fix`
- `High-leverage operational`
- `Strategic experiment`
- `Individual productivity`
- `Maintenance / hygiene`
- `Low-value / reconsider`
- `Blocked / needs evidence`

---

# 10. Kill / reconsider criteria

Actively challenge work when:

- it optimizes a workflow that should disappear
- the problem occurs rarely
- the workaround is already cheap
- implementation cost exceeds recurring value
- AI is being added primarily for novelty
- the solution creates more operational complexity than it removes
- the customer problem is poorly evidenced
- the task produces output but not a meaningful outcome
- the work accelerates production of artifacts nobody meaningfully uses
- there is a simpler non-AI solution
- the feature increases maintenance burden without strategic advantage

Agents should feel permitted to recommend:

> Do not build this.

or:

> Defer until we have evidence.

or:

> Solve the upstream problem instead.

---

# 11. Important nuance

Do NOT interpret this framework as:

"Operational Productivity is always more important than Management Productivity."

Instead use:

> Operational improvements often provide greater technology leverage because they change the value-producing system itself.

But:

> Judgment determines which operational problem is worth solving.

And:

> As AI reduces implementation cost, choosing the correct problem becomes more important, not less.

Therefore the ideal sequence is:

`Good judgment`
→ `choose high-value bottleneck`
→ `improve/redesign operation`
→ `use individual productivity tools where helpful`

---

# 12. Expected agent behavior

Whenever an agent is asked questions such as:

- "What should I work on next?"
- "Which use case should we prioritize?"
- "Which bug should I fix?"
- "Is this AI automation worth building?"
- "Which backlog item has the highest ROI?"
- "How should we improve this workflow?"
- "Should this be automated?"
- "What should we build for this customer?"

the agent should NOT merely rank items intuitively.

Instead it should use the framework above and, where possible, explicitly surface:

1. the desired outcome
2. the bottleneck
3. the productivity layer
4. expected operational leverage
5. recurring impact
6. implementation / lifecycle cost
7. uncertainty
8. recommendation

For important decisions, prefer a compact table such as:

| Item | Outcome | Layer | Impact | Frequency | Operational leverage | Effort | Confidence | Recommendation |
|---|---|---|---|---|---|---|---|---|

Only use elaborate scoring when it improves the decision.

Do not create fake precision.

---

# 13. Customer-specific reasoning

Apply this framework separately for every customer.

For example, a high-value priority for one department or customer may be irrelevant to a different one.

Always account for:

- customer goals
- project phase
- existing systems
- stakeholders
- constraints
- contract/scope
- actual user behavior
- strategic importance
- technical architecture
- unresolved blockers

Do not allow global heuristics to overwrite concrete customer evidence.

Customer context beats generic best practice.

---

# 14. Continuous improvement

Whenever new evidence appears — customer feedback, usage data, implementation experience, repeated support issues, new AI capabilities, changing economics — update the prioritization.

Treat backlog priority as dynamic.

A task's priority can increase or decrease when:

- frequency changes
- implementation cost falls
- AI capabilities improve
- customer strategy changes
- dependencies disappear
- evidence invalidates assumptions
- a new operational bottleneck becomes visible

---

# 15. Make this durable in the Vault

Now inspect the Vault and implement the framework.

Specifically:

1. Identify the best canonical location for these principles.
2. Create or update the relevant Markdown guideline.
3. Add concise instructions/references in `CLAUDE.md`, `AGENTS.md`, or equivalent agent-entry files so future agents know to consult and apply it.
4. Where backlog/TODO conventions exist, incorporate the useful metadata or decision fields without unnecessarily rewriting existing content.
5. Do not automatically reprioritize every existing customer backlog unless enough context exists.
6. If obvious current priorities can be improved using this framework, annotate them conservatively rather than fabricating certainty.
7. Keep one canonical source of truth rather than maintaining conflicting copies.
8. Preserve all customer-specific context.
9. At the end, provide a concise change report containing:
   - files created
   - files modified
   - key rules added
   - any assumptions
   - any places where existing instructions conflict with this framework

The end goal is:

> Future agents operating in this Vault should optimize for meaningful customer and business outcomes — not merely task completion — and should systematically distinguish individual productivity, operational productivity, and judgment when deciding what deserves attention.
