# **Why, and How You Need to Sandbox AI-Generated Code**

## **Executive Summary**

Running AI-generated code is functionally identical to running untrusted code from the internet. By default, an AI agent operates with the exact same privileges as your application—meaning it can read environment variables, access your database, or exfiltrate data. To secure your systems, you must abandon blocklists and adopt **Capability-Based Security**: isolating the execution environment and strictly enumerating what the code is allowed to do.

## ---

**1\. The Core Threat Model**

There are three primary risk scenarios when executing AI-generated code, none of which require the AI to be inherently malicious:

* **The Hallucinating LLM:** The model generates broken code. It imports non-existent modules, creates infinite loops, or writes recursive functions with no base case, leading to memory exhaustion and server crashes.  
* **The "Helpful" LLM:** The model attempts to be overly helpful by reading process.env to debug, fetching internal URLs for context, or dumping your database credentials into logs.  
* **The Compromised Prompt (Most Dangerous):** The model processes adversarial user input (e.g., indirect prompt injection via a parsed document) that explicitly instructs it to exfiltrate environment variables, API keys, or sensitive user data to an external server.

## ---

**2\. The Solution: Capability-Based Security**

The fundamental principle of sandboxing is: **Don't enumerate what to block. Enumerate what to allow.**

Instead of trying to anticipate and block every dangerous system call (the "Master Key" approach), grant the sandbox an empty environment and explicitly pass in only the specific bindings, restricted database interfaces, and loggers the code needs to execute its task (the "Specific Keys" approach).

## ---

**3\. The Isolation Spectrum**

Depending on the use case, choose between two primary sandboxing architectures. **Never use eval() for untrusted code.**

| Feature | V8 Isolates (Dynamic Workers) | Containers (Sandbox SDK) |
| :---- | :---- | :---- |
| **Startup Time** | Sub-millisecond (\~1ms) | Seconds (\~1-5s) |
| **Isolation Level** | Process-level | Full Linux OS |
| **Capabilities** | JS/Python/WASM only. No file system, stateless. | Full filesystem, Network, Arbitrary binaries (Git, NPM). |
| **Best Used For** | AI agent tool-calling, rapid data transformation, short-lived functions, fast iterations. | Full app environments, package installations, running dev servers, deploying apps. |

### **Approach A: V8 Isolates (The Fast Brain)**

Used for rapid, stateless execution. In this model, you spin up a fresh JavaScript runtime environment.

* **Security Implementation:** Set globalOutbound: null to block all external network access. Pass highly restricted RPC stubs (e.g., a locked-down database.query() function) instead of full database access.

### **Approach B: Containers (The Workbench)**

Used when the AI needs a real file system, requires package managers (npm install, pip), or needs to expose a port.

* **Security Implementation:** Requires heavier orchestration. Use a stateful coordinator (like a Durable Object) to manage the lifecycle of the container VM.

## ---

**4\. Universal Security Checklist for Sandboxing**

Regardless of whether you use Isolates or Containers, these 8 rules are mandatory for production:

1. **Default Deny Network Access:** Never allow outbound network requests unless explicitly required. If network access is needed, route it through an internal proxy service where you can enforce allowlists, rate limiting, and logging.  
2. **Grant Explicit Capabilities Only:** Provide RPC stubs, not raw access. If the code needs database access, provide a function that only accepts specific queries, rather than raw database credentials.  
3. **Isolate Per User (Crucial):** One ID per user \= one sandbox. **Never share sandboxes between users.** If User A and User B share a sandbox, they share a file system, leading to immediate cross-tenant data leaks.  
4. **Set Resource Limits:** Always enforce strict timeouts, memory caps, and CPU limits to prevent infinite loops and fork bombs from burning your compute budget.  
5. **Proxy Secrets (Never Inject Them):**  
   * *Bad:* Passing API\_KEY into the sandbox's environment variables. Any code running inside can read and leak it.  
   * *Good:* Proxy requests through your main worker. The sandbox calls your internal API, and your internal worker attaches the authentication header before sending it upstream.  
6. **Always Clean Up After Execution:** Containers cost money and leave residual security surfaces. Use try...finally blocks to explicitly destroy the sandbox and release resources the moment the session ends or times out.  
7. **Log and Audit:** Maintain full visibility. Log what code ran, who triggered it, and when it executed.  
8. **Validate Input Before Sandboxing:** Do not blindly trust the LLM's output. Run basic syntax validations and length checks before passing the generated code into the execution environment.
