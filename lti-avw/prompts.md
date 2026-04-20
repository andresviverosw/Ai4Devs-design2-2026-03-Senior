# prompts.md — LTI-AVW Design Session Log

This file records the full conversation that led to the creation of the **LTI-AVW** design document for the LTI Talent Tracking System.

---

## Session Metadata

| Field | Value |
|---|---|
| **Session date** | April 2026 |
| **Output document** | LTI-AVW.md |
| **Diagram format** | Mermaid |
| **Participants** | User (Product Owner), AI Architect Assistant |

---

## Prompt 1 — Initial Design Request

**Role:** User  
**Attachment:** `LTI_ATS_diagram.avif` — A circular infographic illustrating the 7 phases of an Applicant Tracking System: Creating Jobs → Jobs Published on Job Boards / Website / Social Media → Job Applications Received → Applications are Reviewed → Online Tests are Conducted → Interviews are Scheduled → Selected Applicants are Hired.

**Message:**

> You are an expert software architect and product manager with experience in applicant tracking system software.
> The goal is to design and document a software system following the phases of:
>
> * Research and analysis
> * Use cases
> * Data modeling
> * High level design
>
> LTI is a startup that wants to develop the ATS (Applicant-Tracking System) of the future. For context, the image attached provides information on all phases of the ATS process. With this in mind, the idea is to define those key features that will make LTI stand out from the competition:
>
> * Increasing efficiency for HR departments
> * Improve real-time collaboration between recruiters and managers
> * Automations
> * AI assistance in various tasks
>
> It's time to brainstorm, research what the keys to success might be, and write it down for the rest of the team.
> Your mission is to design the first version of the system, delivering the following artifacts:
>
> * ✅ Brief description of LTI software, added value and competitive advantages.
> * ✅ Explanation of the main functions.
> * ✅ Add a Lean Canvas diagram to understand the business model.
> * ✅ Description of the 3 main use cases, with the diagram associated with each one.
> * ✅ Data model that covers entities, attributes (name and type) and relationships.
> * ✅ High-level system design, both explained and with an attached diagram.
> * ✅ C4 diagram that goes in depth into one of the system components, whichever you prefer.
>
> Document everything in a single markdown document named LTI-AVW. This entire conversation must be stored in a separate file called prompts.md.
> Use mermaid for diagrams. Ask me any questions you may have.

---

## Response 1 — AI Architect Assistant

**Processing steps performed:**

1. Converted the uploaded AVIF image to PNG for rendering.
2. Analysed the ATS lifecycle diagram — identified 7 phases:
   - Creating Jobs
   - Jobs Published on Job Boards, Website, Social Media, etc.
   - Job Applications Received
   - Applications are Reviewed
   - Online Tests are Conducted
   - Interviews are Scheduled
   - Selected Applicants are Hired
3. Assessed that all requirements were sufficiently clear and detailed — no clarifying questions needed.
4. Proceeded to generate the full **LTI-AVW.md** design document.

**Document sections produced:**

| # | Section | Description |
|---|---|---|
| 1 | Product Overview | Description, value proposition, competitive advantage comparison table, 6 key differentiators |
| 2 | Main Functions | 10 core functional areas with detailed sub-capabilities |
| 3 | Lean Canvas | Mermaid `graph TB` diagram with all 9 Lean Canvas sections: Problem, Solution, UVP, Unfair Advantage, Customer Segments, Key Metrics, Channels, Cost Structure, Revenue Streams |
| 4.1 | Use Case 1 | AI-Assisted Job Creation & Multi-Channel Publishing — Mermaid flowchart with 5 actors |
| 4.2 | Use Case 2 | Collaborative Application Review with AI Screening — Mermaid flowchart with 4 actors |
| 4.3 | Use Case 3 | Assessment, Interview Scheduling & Hire Decision — Mermaid flowchart with 7 actors |
| 5 | Data Model | Mermaid ER diagram with 16 entities, full attribute lists (name + type), and all relationships |
| 6 | High-Level System Design | Architecture explanation with decision table + Mermaid `graph TB` covering client, edge, core domain services, AI services, data, integrations, and observability layers |
| 7.1 | C4 Level 1 | System Context diagram for the AI Screening Engine |
| 7.2 | C4 Level 2 | Container diagram for the AI Screening Engine |
| 7.3 | C4 Level 3 | Component diagram showing the 8-step screening pipeline (Ingestor → Parser → Embedder → Matcher → Scorer → Bias Detector → Ranker → Explainer) |

**Design choices and rationale:**

- **C4 deep-dive target:** The AI Screening Engine was selected as the component for C4 depth because it is LTI's primary technical differentiator and the most architecturally complex subsystem. It integrates LLM-based parsing, vector embeddings, semantic similarity search, multi-criteria scoring, bias detection, and explainability generation in a single orchestrated pipeline.

- **Architecture pattern:** Cloud-native microservices on AWS, domain-driven decomposition, event-driven async automation via EventBridge, PostgreSQL + pgvector for relational and vector data, Redis for queuing and real-time pub/sub, WebSockets for live collaboration.

- **Lean Canvas format:** Represented using Mermaid `graph TB` with `subgraph` blocks to approximate the standard 9-box Lean Canvas grid layout, since Mermaid does not have a native Lean Canvas diagram type.

- **Use case diagrams:** Represented as Mermaid `flowchart TD` diagrams with styled actor nodes and dashed `-.->` lines to distinguish AI-assisted steps from human-initiated actions, approximating UML use case diagram semantics within Mermaid's supported syntax.

**Output files created:**
- `/outputs/LTI-AVW.md` — Main design document
- `/outputs/prompts.md` — This conversation log

---

*End of session log.*
