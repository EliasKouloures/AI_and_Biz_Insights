# ANTHROPIC FIRESIDE CHAT: CLAUDE CODE, CLAUDE TAG & FABLE (KNOWLEDGE GRAPH)

## 1. CORE ENTITIES & AI AGENTS
* **Claude Code:** CLI-based autonomous coding agent. Evolved from requiring heavy manual oversight (micromanaging permissions) to effectively "one-shotting" complex features.
* **Claude Tag:** Proactive, multiplayer Slackbot agent. Currently authors and lands 65% of Anthropic's internal product engineering PRs. Operates proactively (e.g., monitoring bug channels to auto-fix issues) and features shared team memory stored as channel-specific Markdown files.
* **Fable & Opus 4.8:** Frontier models driving step-change improvements in agentic autonomy, enabling tools to require significantly less explicit prompting.

## 2. ENGINEERING PARADIGM SHIFTS
* **Velocity Compression:** Product ideation-to-deployment timelines have shrunk from 6-12 months down to approximately 1 week.
* **Skillset Pivot:** Basic execution is commoditized. A high premium is now placed on product taste, business sense, and elevated ambition to tackle larger problems.
* **Codebases = Executable Specs:** Legacy warnings against complete rewrites are obsolete. Codebases are now treated as dynamic specs, making complete codebase translations (e.g., porting from Bun to Rust) fast and viable.

## 3. PROMPTING & SYSTEM ARCHITECTURE
* **80% System Prompt Reduction:** Frontier models (Fable) suffered from over-constraint. Removing rigid examples and negative constraints ("do not do X") drastically improved model creativity, adaptability, and reliability.
* **Model-Tiered Prompting:** Older/smaller models still require exhaustive system prompts. Only frontier models possess the intrinsic judgment (e.g., knowing when to verify a UI change vs. a backend change) to operate safely with minimized prompts.
* **Human-less Code Review:** Anthropic has fully automated code reviews for outer codebase layers. Trust was established via a 6-month loop of converting past incident reports into strict, non-regressing evaluation sets.

## 4. SECURITY & AUTO MODE
* **Auto Mode by Default:** The hardened execution environment for long-running workflows. It utilizes a background Sonnet classifier to dynamically evaluate tool usage and bash calls, comparing them against the user's original conversational intent.
* **Proxy Credential Injection:** Agents never hold raw API tokens. Sandboxed network requests are intercepted, and real credentials (e.g., DataDog) are securely injected mid-flight to prevent token exfiltration.

## 5. EMERGENT CAPABILITIES & USE CASES
* **End-to-End Video Production:** Fable can ingest raw A/V files and HTML slide decks to autonomously transcribe, cut, dynamically crop, and animate conference videos using FFmpeg and Remotion.
* **Vibe-Coding Workflows:** Claude efficiently orchestrates multi-agent pipelines for tasks like game development (prompting Gemini/Sea Dance to generate 2D sprites and JSON hitboxes) and automating complex physical logistics (scraping climbing routes and matching them with Airbnb and flight APIs).
* **"Remote Control" Pattern:** Engineers frequently spawn local headless agent sessions on laptops, but command and monitor the execution remotely via mobile devices.
