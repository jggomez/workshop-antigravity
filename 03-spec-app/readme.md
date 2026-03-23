# Project: AI-Powered Document Insight Manager

## Objective
The goal of this exercise is to simulate the **Spec-Driven Development (SDD)** process using AI Coding tools to generate a software solution based strictly on functional needs and quality attributes. 

We are moving away from "Vague Prompts" toward **Rigorous Specifications** (Deterministic programming).

**The focus is to:**
1.  **Identify Implicit Quality Attributes**: Extract non-functional requirements from the use case.
2.  **Formulate an Initial Spec/Prompt**: Integrate business needs and technical constraints into a "Mini-Spec".
3.  **Generate Code Structure**: Use an AI Agent (Antigravity/Gemini) to scaffold the solution based on the defined intent.

---

## The Business Case: AI-Powered Document Insight Manager

### User Journey
A client requires a software solution that allows users to perform the following actions:
* **Authentication**: Users must be able to sign in using their **Gmail account** (OAuth2/Google Auth).
* **Document Upload**: Seamlessly upload **PDF documents** for processing.
* **AI Analysis**: Automatically extract key **insights** from the document via content analysis.
* **Human-in-the-Loop**: Review and manually **modify** the AI-generated insights to ensure accuracy.
* **Persistence**: Save the modified insights into a secure database.
* **Traceability**: View a complete **history** of all previously analyzed documents.

---

## User Story Definition

### Prompt Structure

**Role:**
Act as a **Senior Business Analyst and Requirements Engineer** specialized in Agile methodologies and **Spec-Driven Development (SDD)**. Your goal is to deconstruct a product vision into clear, unambiguous functional value units that an AI agent can implement with high precision.

**Task:**
Based on the system description provided, you must:
1.  **Identify Actors:** Define all stakeholders, including end-users, administrators, and external system dependencies (APIs/Services).
2.  **Draft User Stories:** Create a comprehensive list of stories that strictly separate the **"What"** (business intent) from the **"How"** (technical implementation).
3.  **Define Acceptance Criteria (AC):** Provide detailed technical and functional criteria for each story using the **Gherkin format** (Given/When/Then).

**Refinements & Constraints:**
* **Professional Tone:** Use industry-standard technical terminology.
* **Business Value:** Every story must provide a measurable benefit to the user or the business.
* **Edge Case Mastery:** Explicitly identify potential edge cases (e.g., file upload limits, session timeouts, API latency) within the Acceptance Criteria.
* **Epics:** Group stories into logical Epics to maintain a clean architectural hierarchy if the scope is broad.

---

### Output Format
Present the final backlog in a Markdown table with the following structure:

| ID | Title | User Story | Acceptance Criteria (Gherkin) | Priority |
| :--- | :--- | :--- | :--- | :--- |
| **US-001** | Feature Name | "As a [role], I want to [action], so that [benefit]" | - **Given** [context] **When** [action] **Then** [result] (Include Edge Cases) | High/Med/Low |

---

## Initial Backlog
**Actors**: End-User, Google Auth Provider, AI Engine (Gemini), System Database.

| ID | Title | User Story | Acceptance Criteria (Gherkin) | Priority |
| :--- | :--- | :--- | :--- | :--- |
| **US-001** | Google Auth | As a user, I want to sign in with my Gmail account, so that my data remains private and secure. | **Given** the user is on the login page, **When** clicking "Sign in with Google," **Then** the OAuth2 flow starts and creates a secure session. **Edge Case:** Show "Session Timeout" message if high latency occurs. | High |
| **US-002** | PDF Upload | As a user, I want to upload a PDF document, so that the system can begin the analysis. | **Given** an active auth session, **When** selecting a PDF and clicking upload, **Then** the system validates and stores it securely. **Edge Case:** Reject files exceeding size limits or non-PDF formats. | High |
| **US-003** | AI Extraction | As a user, I want the system to analyze the PDF, so that I receive automated insights without manual reading. | **Given** a successful PDF upload, **When** processed by the Gemini engine, **Then** a structured list of insights appears. **Edge Case:** Implement retry logic or failure notifications if the API is latent or fails. | High |
| **US-004** | Refinement | As a user, I want to modify AI-generated insights, so that I can ensure final data accuracy. | **Given** the generated insights list, **When** editing a field and clicking save, **Then** the database updates the record. **Edge Case:** Prevent saving empty or malformed data through strict validation. | Medium |
| **US-005** | History | As a user, I want to view a list of previously analyzed documents, so that I can track my work over time. | **Given** the History view, **When** the page loads, **Then** the system retrieves and displays user-specific records from the database. **Edge Case:** Show a "No history found" state instead of an empty screen if no data exists. | Medium |

---

## Design UI using [Stitch](https://stitch.withgoogle.com/)

### Login
<img width="1600" height="1280" alt="screen" src="https://github.com/user-attachments/assets/5e840aa8-7980-4ead-a2bc-333736b79cde" />

### Process File
<img width="1600" height="1280" alt="screen" src="https://github.com/user-attachments/assets/84c39713-4de8-4f6f-a7e9-ff9d8b2d80f7" />

### Result
<img width="1600" height="1280" alt="screen" src="https://github.com/user-attachments/assets/572ed7cf-b3ad-464a-8aed-65335134e272" />

### Historical Data
<img width="1600" height="1280" alt="screen" src="https://github.com/user-attachments/assets/7d61ccb2-aa72-48dc-82c1-8330077df940" />

---

## Copy Spec.md
### Please copy spec.md to the Antigravity workspace for this workshop.
