# Vibe Engineering

In the agentic era, coding is no longer about syntax; it’s about **intent and orchestration**. **Vibe Engineering** is the technical discipline of using natural language and semantic intuition to guide autonomous agents through rigorous architectural boundaries.

#### **What is Vibe Engineering?**
Vibe Engineering is the shift from "writing code" to **"steering outcomes."** It acknowledges that while an AI can generate text, only a human architect can ensure the "vibe" (the underlying quality, user experience, and architectural integrity) is correct. It combines the speed of generative AI with the precision of **Spec-Driven Development (SDD)** to eliminate the "gravity" of boilerplate tasks.

* **Read this blog:** [Vibe Engineering: How to Build Pro-Grade Software Without the AI Technical Debt](https://jggomezt.medium.com/vibe-engineering-how-to-build-pro-grade-software-without-the-ai-technical-debt-ec7c0ad9d11b)

---

#### **The Verification Cycle: Step-by-Step Process**
To prevent the AI from creating a "Big Ball of Mud," every task must follow this four-step recursive loop. Treat all AI-generated code as a **draft**, never as final production code.

**1. Generate**
* **Action:** Use layered prompts (Context → Task → Constraints) to create the initial logic.
* **Goal:** Obtain a functional baseline that matches the User Stories defined in the `spec.md`.

**2. Understand**
* **Action:** Inspect the **diff** of the changes. Read the code to ensure the architecture remains clean.
* **Critical Question:** "Does this follow our Clean Architecture? Is it leaking Firebase logic into the Use Cases?" **Do not accept code blindly.**

**3. Improve (The "What Could Go Wrong?" Technique)**
* **Action:** Perform a **Code Smell and Refactoring** analysis. Ask the agent: *"Looking at this code, what could go wrong in the real world? List edge cases, performance bottlenecks, and missing error handling."*
* **Goal:** Use specialized **Skills** to identify technical debt early and update the code to cover identified risks.

**4. Integrate**
* **Action:** Test the change without mercy.
* **The Rhythm:** Apply the change → Reload the page/service → Verify the specific behavior → Ensure no regressions in existing features.

---

#### **Vibe Engineering Resources**
To master this discipline and apply it to the **AI-Powered Document Insight Manager**, you can access the official documentation and playbook.

* **Download the Playbook:** [Vibe Engineering Playbook](https://devhack.co/academy-ai/vibe/index.html)
    * *This resource contains the advanced prompt engineering patterns, "Ruthless Revert" strategies, and the Goldilocks Zone framework for agentic orchestration.*
