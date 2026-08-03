
# Architectural Blueprint: Building an AI Knowledge Base (KB)

## 1. Core Principles & Constraints

* **Selective Context Retrieval:** An AI KB will grow massively, but supplying entire document repositories per prompt dilutes context and increases costs. The architecture must enable precise, modular retrieval so the AI accesses *only* the specific data needed.
* **Single Source of Truth:** Never duplicate existing information across documents. Information must exist in only one location to avoid maintenance conflicts.
* **Subscription vs. API Cost Optimization:** Using frontier models (OpenAI/Anthropic) via flat-rate subscriptions with native connectors (e.g., Claude Code, Claude Cowork, Codex) costs **~4%** of what raw pay-per-token API usage would cost for equivalent workload volumes.

---

## 2. Information Categorization Framework
Every piece of company information must be mapped into one of **three operational buckets**:

```
                              ┌───────────────────────────────────┐
                              │      Enterprise Data Sources      │
                              └─────────────────┬─────────────────┘
                                                │
         ┌──────────────────────────────────────┼──────────────────────────────────────┐
         ▼                                      ▼                                      ▼
┌───────────────────┐                  ┌───────────────────┐                  ┌───────────────────┐
│   1. Workspaces   │                  │ 2. Knowledge Base │                  │     3. Skills     │
└────────┬──────────┘                  └────────┬──────────┘                  └────────┬──────────┘
         │                                      │                                      │
  • Live operational data                • Structured ref data                 • Task execution logic
  • Tooling: Gmail, Slack,               • Format: Markdown (.md)              • Tooling: Native Claude/
    Notion, Monday                       • Hosted: GitHub / DB                   ChatGPT Skills
  • Method: Read/Write APIs              • Standard: Google OKF                • Advantage: Lower latency
```

### 1. Workspaces (Live Operational Data)
* **What Lives Here:** Daily communication, active task tracking, operational updates, and transactional data.
* **Platforms:** Gmail, Slack, Notion, Monday.com.
* **Integration Strategy:** Connect directly via native read/write integrations. Avoid copying workspace data into static documents.

### 2. Knowledge Base (Structured Reference Data)
* **What Lives Here:** Permanent company context, technical documentation, standard reference materials, and SOP details.
* **Format:** Plaintext Markdown (`.md`) files following standardized schema.
* **Integration Strategy:** Connect via read/write version-controlled repositories or databases.

### 3. AI Skills (Task Execution Logic)
* **What Lives Here:** Instructions written *specifically for the AI*, including step-by-step process guidance, internal organizational rules, and standardized execution protocols.
* **Placement:** Stored natively within AI platform environments (e.g., Claude Custom Skills / Custom GPTs).
* **Advantage:** Native skills run faster and consume fewer context resources than referencing external SOP documents via connectors.

---

## 3. Standard & Format Selection

* **Standard:** **Google’s Open Knowledge Format (OKF)**
  * **Origin:** Standardized framework derived from Andre Karpathy's *LLM Wiki* concept.
  * **Value:** Provides a formal structure for organizing, linking, and retrieving modular knowledge blocks efficiently.
  * **Implementation Prompt:** Point the AI to Google's public OKF GitHub repository and instruct it to create a custom skill to organize raw data into OKF compliance.
* **File Type:** **Markdown (`.md`)**
  * Essential for lightweight formatting, programmatic parsing, and native bidirectional editing by LLMs.

---

## 4. Infrastructure & Storage Evaluation

| Storage Option | Read/Write Capability | Permissions Control | Best For |
| :--- | :--- | :--- | :--- |
| **GitHub** *(Recommended)* | **Bidirectional** (Natively reads & writes via Claude/ChatGPT connectors) | **Repo-Level Only** (Coarse read/write access across entire repo) | Team KBs requiring autonomous AI maintenance. |
| **Firebase / Supabase** | **Bidirectional** (Via database API calls) | **Granular / Role-Based** (Restricts specific rows/folders per user) | Team KBs requiring multi-tiered access permissions. |
| **Google Drive / Docs** | **Read Only** (Requires CLI workarounds for writing) | **Folder/Doc Level** | Legacy document viewing (Not recommended for scalable AI KBs). |
| **Local Storage + Obsidian** | **Bidirectional** (Direct local file access) | **Single User** | Solopreneurs or single-operator setups. |
| **Notion** | **Bidirectional** | **Workspace Level** | Integrated workspaces, though slower and less flexible for core KB structure. |

---

## 5. Summary Implementation Roadmap

1. **Standardize Format:** Adopt Markdown (`.md`) and Google’s OKF structure.
2. **Setup Repository:** Store `.md` files in a GitHub repo (or Supabase/Firebase if granular permissions are required).
3. **Connect Native Subscriptions:** Link the repo directly to Claude / ChatGPT subscription environments to allow autonomous reading and updating.
4. **Extract Workspaces:** Connect live platforms (Slack, Gmail, Notion) via native connectors; do not duplicate this data into static files.
5. **Convert Execution Guidelines to Skills:** Move all "how-to" procedural guides and logic directly into native system **Skills** for lower latency and efficient execution.
