# Google Antigravity Configuration

Based on the architectural shift toward **Agentic AI-First Development**, this section details how to configure the environment to move from being a "typist" to an **Architect**.

#### **1. What is Antigravity and Why Use It?**
**Google Antigravity** is an agent-first development platform built on a fork of VS Code. Unlike traditional IDEs that offer "autocomplete" plugins, Antigravity assumes the **AI agent is the primary worker**.

* **The "Why":** Its name refers to providing "liftoff" from the heavy "gravity" of tedious tasks (boilerplate, environment setup, manual debugging). It allows you to manage **outcomes and architectures** rather than individual lines of code.

#### **2. Agent Manager (Mission Control)**
The **Agent Manager** is a dedicated dashboard that bifurcates the IDE, separating manual editing from AI orchestration.
* **Asynchronous Work:** You can spawn multiple agents to work on different tasks (e.g., one researching an API while another writes tests) in parallel.
* **Planning vs. Fast Mode:** You can set the "thinking budget." *Planning mode* forces the agent to create a task list for your review before coding, while *Fast mode* executes quick commands directly.

#### **3. MCP Servers (The Agent's "Hands")**
The **Model Context Protocol (MCP)** is an open standard that connects the AI to the outside world.
* **Capabilities:** Through MCP, the agent can read live databases, query tickets, or execute cloud commands.
* **Project Context:** For this project, you would enable the **Firebase MCP** to allow the agent to create projects and enable services autonomously in your Google Cloud console.

```json
"stitch": {
  "serverUrl": "https://stitch.googleapis.com/mcp",
  "headers": {
    "X-Goog-Api-Key": ""
  },
  "disabled": true
}
```

#### **4. Rules: The "Laws" of the Workspace**
Rules are baseline instructions the agent **must always follow** without being reminded in the chat.

* **Rule 1: `architectural-alignment.md`**
    > "Always follow the Clean Architecture structure defined in `/design.md`. Logic must reside in `src/use-cases`, and Firebase-specific calls must be isolated in `src/adapters`. Never bypass the established directory hierarchy."
* **Rule 2: `spec-fidelity.md`**
    > "Before implementation, cross-reference the `spec.md` and `design.md` files. All Acceptance Criteria (Gherkin) must be converted into test cases. Reject any implementation that violates the security tactics defined in the ASRs."

#### **5. Workflows: Repeatable Industrial Processes**
Workflows are saved, on-demand prompts triggered with a `/` command for repetitive multi-step tasks.

* **Workflow 1: `/deploy-hosting`**
    > 1. Run `npm run build`.
    > 2. Validate that the `public` folder contains the new build.
    > 3. Execute `firebase deploy --only hosting`.
    > 4. Provide the live URL and a summary of the deployed version.
* **Workflow 2: `/run-local`**
    > 1. Check if the Firebase emulators are installed.
    > 2. Execute `firebase emulators:start` or `firebase serve`.
    > 3. Verify that the local Firestore and Auth services are reachable.
    > 4. Open the local URL using the **Browser Subagent** to confirm the UI loads correctly.

#### **6. Skills (Specialized Knowledge)**
Skills are specialized packages of knowledge (docs, scripts, or examples) that remain idle until needed.
* **The "Progressive Disclosure" Benefit:** They prevent "tool bloat" because they are only loaded into the agent's context window when a task matches the skill's metadata.
* **Example:** You can create a **"Firebase-AI-Logic-Skill"** containing the specific JSON schema for Gemini-3-flash-preview prompts, which the agent will only load when it's time to configure the extraction engine.
