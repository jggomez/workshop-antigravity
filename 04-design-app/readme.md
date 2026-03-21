# Design App

In this phase, we transition from functional requirements to **Architectural Design**. Before defining components or code, we must establish the **Quality Attributes** (Non-Functional Requirements) that will govern the system's behavior, performance, and security.

## Quality Attributes Definition
Quality Attributes are the measurable properties of a system that indicate how well it satisfies the needs of its stakeholders. Following the **ISO/IEC 25010** standard, we focus on characteristics like **Functional Suitability, Performance Efficiency, and Security** to ensure the "AI-Powered Document Insight Manager" is production-ready, not just a prototype.

---

## Prompt: Quality Attribute & Trade-off Analysis

**Role:**
Act as a **Senior Software Architect**. Your specialty is **trade-off analysis** and the definition of **Quality Attributes** (Availability, Scalability, Security, Maintainability, etc.) following industry standards.

**Task:**
Based on the previously generated User Stories, you must:
1.  **Identify Critical Quality Attributes:** Determine which attributes are essential for the system's success.
2.  **Draft Detailed Quality Attribute Scenarios:** Define scenarios including Source, Stimulus, Artifact, Environment, Response, and Response Measure.
3.  **List Constraints:** Identify Technical, Business, Budgetary, or Legal Compliance constraints.
4.  **Identify Conflicts:** Detect potential trade-offs (e.g., High Security vs. Low Latency).

**Refinements:**
* **Quantitative Precision:** Use specific metrics (e.g., "Latency < 200ms") instead of vague terms like "fast".
* **Architectural Impact:** Classify attributes based on how they influence the core design.
* **Terminology:** Use **ISO/IEC 25010** standard terminology.

**Output Format:**
* **Scenario Table:** Attribute | Scenario (Stimulus/Response) | Success Metric | Priority (H/M/L).
* **Constraints List:** Category | Description | Design Impact.
* **Trade-off Matrix:** Brief explanation of which attribute is sacrificed in favor of another and the architectural reasoning.

---

## Critical Step: Human-in-the-Loop Review
In **Vibe Engineering**, the output of this prompt is treated as a **draft**, not an oracle. As the Architect, you must:
* **Verify** that the quantitative metrics are realistic for the chosen tech stack (e.g., Gemini API latency).
* **Validate** that the security scenarios address risks like unauthorized data access.
* **Refine** the trade-offs to ensure they align with business priorities.

## Quality Attribute Analysis: AI-Powered Document Insight Manager

### Quality Attribute Scenario Table

These scenarios define how the system must behave under specific stimuli to meet high-level quality goals.

| Attribute (ISO 25010) | Scenario (Stimulus/Response) | Success Metric | Priority |
| :--- | :--- | :--- | :--- |
| **Security (Confidentiality)** | An unauthorized user attempts to access another user's document history (US-005). | Access is denied; unauthorized attempt is logged. | **High** |
| **Performance (Latency)** | User clicks "Sign in with Google" (US-001) under normal network conditions. | OAuth2 redirect occurs in **< 500ms**. | **High** |
| **Performance (Time Behavior)** | User triggers "AI Extraction" (US-003) for a standard 10-page PDF. | Insights are extracted and rendered in **< 10 seconds**. | **High** |
| **Reliability (Recoverability)** | Gemini API fails or times out during PDF analysis (US-003). | System triggers a retry (max 3) and notifies user after 3 failures. | **Medium** |
| **Maintainability (Modularity)** | Developer adds a new AI model provider beside Gemini. | Changes are isolated to the AI Service layer without affecting UI or DB. | **Medium** |

---

### Constraints List

Constraints are non-negotiable limitations that significantly influence architectural decisions.

| Category | Description | Design Impact |
| :--- | :--- | :--- |
| **Technical** | Integration with **Gemini API** for content analysis. | Architecture must handle asynchronous API calls and potential latency. |
| **Compliance** | **OAuth2 / Google Auth** requirement for all user access. | Mandatory Identity Provider (IdP) integration; no local password storage allowed. |
| **Technical** | **PDF Format** is the only supported input for document upload. | Requires a specialized parsing layer (e.g., pdf.js or server-side parser). |

---

### Trade-off Matrix

Architectural design is the art of balancing conflicting goals. Below are the primary trade-offs identified for this system.

| Trade-off | Sacrifice | Benefit | Architectural Reasoning |
| :--- | :--- | :--- | :--- |
| **Security vs. Latency** | **Latency** (minor increase) | **High Confidentiality** | Implementing Row-Level Security (RLS) and OAuth2 token verification on every request adds overhead but is mandatory to protect private PDF data. |
| **Reliability vs. Cost** | **Cost** (API credits) | **High Robustness** | Implementing retry logic for AI extraction (US-003) increases API consumption costs but prevents the "brittle system" failure where a single network hiccup breaks the user journey. |
| **Performance vs. Modularity** | **Performance** (minor) | **Maintainability** | Using a structured abstraction layer for the AI Engine (instead of direct API calls) allows switching providers easily but adds a small amount of execution overhead. |

---

## Architecture Decisions (Design Phase)

Architecture Decisions represent the strategic choices that define the structure, behavior, and "skeleton" of the system. In **Spec-Driven Development (SDD)**, this phase is critical because it prevents the AI from creating a "Big Ball of Mud." By defining the architecture upfront, we ensure the generated code is modular, testable, and secure. These decisions act as the high-level **Guardrails** that keep the development agent aligned with long-term maintainability.

### Critical Review Protocol
Before proceeding, remember that as a **Lead Architect**, you must review the AI's output to ensure:
* **Feasibility**: Can the chosen stack actually deliver the success metrics defined in the previous step?
* **Simplicity**: Avoid "Over-engineering." Does the business case really need Microservices, or is a Modular Monolith more efficient for an MVP?
* **Consistency**: Ensure the design patterns directly address the **Acceptance Criteria** and **Quality Attributes** previously established.

---

## Prompt: Architectural Design & Strategy

**Role:**
Act as a **Principal Software Architect**. You are an expert in architectural styles (Hexagonal, Event-Driven, Serverless, Microservices) and **Cloud Design Patterns**.

**Task:**
Design the high-level structure of the system. To do this, you must:
1.  **Select and Justify the Primary Architectural Style:** Choose the best fit for the "AI-Powered Document Insight Manager."
2.  **Identify Required Design Patterns:** Solve specific domain problems (e.g., handling heavy PDF processing or AI latency).
3.  **Define Communication & State Strategy:** Determine synchronous vs. asynchronous flows and how the system manages state.

**Refinements:**
* **ASR Alignment:** Justify every decision based strictly on the **Quality Attribute Scenarios** (Security, Latency, Reliability) defined in the previous phase.
* **Macro Principles:** Apply **SOLID** and **DRY** principles at the architectural level.
* **Resilience:** Consider horizontal scalability and fault tolerance for AI service dependencies.

**Output Format:**
* **Proposed Architecture:** Style name and a high-level summary.
* **Justification:** Direct link to the prioritized Quality Attributes.
* **Applied Patterns Table:** Pattern | Problem it solves | Specific application in this system.
* **Recommended Tech Stack:** Suggestions for Languages, DBs, and Middleware.

---

### Final Architectural Design

As the **Principal Software Architect**, I have finalized the design for this **Serverless BaaS** solution. This architecture transitions from a "Pure Vibe" approach to **Vibe Engineering** by enforcing a **Client-Side Clean Architecture** using pure HTML and Tailwind CSS. This ensures high performance, security, and modularity without the need for a custom backend.

---

### Architecturally Significant Requirements (ASRs) - Complete List

The following ASRs drive the core design of the system. Each decision is analyzed based on its context, solution, and the resulting trade-offs to ensure a production-grade result.

#### **ASR-01: Identity & Data Privacy (Security)**
* **Context:** Users upload sensitive PDF documents. These files and their derived insights must remain private and accessible only by the document owner.
* **Solution:** Integrate **Firebase Auth** using Google Sign-In for identity. Implement **Firestore and Storage Security Rules** that validate the `request.auth.uid` against the `userid` field in each document.
* **Justification:** Moving authorization to the infrastructure layer ensures that data cannot be leaked even if the client-side code is compromised.
* **Pros:** Robust security, zero backend code to maintain, and seamless integration with Google’s ecosystem.
* **Cons:** Tight coupling with Firebase's proprietary security rule language.

#### **ASR-02: Automated Analysis Workflow (Reliability)**
* **Context:** Extracting insights via LLM is an expensive and potentially slow process that may fail due to API timeouts or malformed PDFs.
* **Solution:** Utilize the **Firebase AI Logic Extension** configured with `gemini-3-flash-preview`. The UI observes a status field in Firestore to provide real-time feedback.
* **Justification:** An event-driven approach offloads heavy processing from the user's browser, allowing for managed retries and background execution.
* **Pros:** Scalable, asynchronous execution, and built-in retry logic.
* **Cons:** Potential "cold start" latency for initial cloud function triggers.

#### **ASR-03: Responsive "Vibe" & Interaction (Performance)**
* **Context:** Users require a fluid experience when navigating history or editing insights.
* **Solution:** Use **HTML5/Tailwind CSS** for a lightweight UI and **Firestore Real-time Listeners** for state synchronization.
* **Justification:** Eliminating heavy JavaScript frameworks reduces the bundle size and improves Time-to-Interactive (TTI), while Firestore provides immediate "optimistic" updates.
* **Pros:** Near-instant load times, offline support, and a highly responsive UI.
* **Cons:** Requires manual DOM manipulation or a lightweight reactivity library to manage state in pure HTML.

#### **ASR-04: Error Handling & Observability (Reliability)**
* **Context:** Without a custom backend, errors in AI extraction or storage must be visible to the user to avoid "silent failures."
* **Solution:** Implement an **Audit Log** collection in Firestore where the AI Extension writes execution status and errors.
* **Justification:** Provides a shared log between the agent and the developer to debug failed extractions and maintain system health.
* **Pros:** Improved troubleshooting and clear feedback for the end-user.
* **Cons:** Small increase in Firestore write operations.

#### **ASR-05: Integrity of Extracted Insights (Functional Suitability)**
* **Context:** AI-generated insights can be "hallucinated" or malformed, potentially breaking the UI structure.
* **Solution:** Implement a **Schema Validation** tactic in the "Human-in-the-Loop" review phase.
* **Justification:** Ensures that all saved insights adhere to a strict structure before being persisted, preventing technical debt in the data layer.
* **Pros:** Guaranteed data consistency and simplified frontend rendering.
* **Cons:** Slight increase in client-side processing logic.

---

### Design Tactics

Tactics are specific architectural actions used to satisfy the ASRs.

#### **1. Authentication & Authorization (Security)**
* **Context:** Unauthorized access to private PDFs and their extracted metadata.
* **Tactic:** **Credential-Based Identity** via Firebase Auth and **Row-Level Security** in Firestore.
* **Implementation:** The UI only renders data where `userid == firebase.auth().currentUser.uid`. This is reinforced by a "Zero-Trust" rule in Firestore: `allow read, write: if request.auth != null && request.auth.uid == resource.data.userid`.

#### **2. Asynchronous Processing (Performance)**
* **Context:** Blocking the UI while waiting for the AI model to process a document.
* **Tactic:** **Asynchronous Callback / Reactive State**.
* **Implementation:** The client initiates an upload and immediately returns to a "Processing" state. Using the **Observer Pattern**, the UI listens for updates in Firestore. This effectively manages the feedback loop without freezing the browser.

#### **3. Managed Infrastructure (Scalability & Availability)**
* **Context:** Managing peaks in traffic and ensuring the service is always available globally.
* **Tactic:** **Serverless BaaS (Backend-as-a-Service)**.
* **Implementation:** Using **Firebase Storage** and **Cloud Functions** (AI Logic) ensures the system scales horizontally by default. Availability is offloaded to the cloud provider, achieving high uptime without manual server maintenance.

---

### Architectural Pattern Decisions

* **Client-Side Clean Architecture:** The project is organized into **Entities** (Insights), **Use Cases** (ProcessDocument), and **Adapters** (FirebaseRepository). This protects the business logic from being tangled with Firebase SDK specifics.

* **Observer Pattern:** The UI layer "listens" to Firestore snapshots. When the AI Logic Extension updates the database, the view reflects the change automatically.

---

### Technical Stack (The Blueprint)

* **UI/UX:** HTML5 + **Tailwind CSS v3+**.
* **Client Logic:** Vanilla JavaScript (ES6+) following Clean Architecture layers.
* **Identity:** **Firebase Auth** (Gmail Provider).
* **Database:** **Cloud Firestore**.
    * *Collection `Users`:* `{ id, name, url_avatar, email }`
    * *Collection `UserDocuments`:* `{ userid, docname, insights: [], summary, storage_path }`
* **File Storage:** **Firebase Storage**.
* **Intelligence:** **Firebase AI Logic Extension** (`gemini-3-flash-preview`).

---

## Copy design.md
### Please copy design.md to the Antigravity workspace for this workshop.
