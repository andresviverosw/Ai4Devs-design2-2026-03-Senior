# User Stories, Backlog & Implementation Tickets — LTI (AVW)

**Author initials:** AVW  
**Source PRD / design:** `LTI-AVW.md` (LTI Talent Tracking System — Design Document v1.0)  
**Date:** April 2026  

This document applies the **senior Product Owner** story structure you specified (role / action / benefit, BDD acceptance criteria, complexity, INVEST reflection). The **product description** used for the stories is **LTI (Lean Talent Intelligence)** — the AI-native ATS defined in `LTI-AVW.md` — not the unrelated e-learning example sometimes bundled with the same template text.

---

## 1. User stories (INVEST-aligned)

### US-01 — AI-assisted job requisition draft from role brief

**Title:** Create a job requisition with an AI-generated job description draft from a structured role brief  

**Story:** As a **hiring manager**, I want to **submit a role brief (title, level, team, skills) and receive an editable AI-generated JD draft**, so that **I can open a requisition quickly without starting from a blank page**.

**Acceptance criteria (BDD):**

1. **Given** I am authenticated as a hiring manager for my company, **when** I submit a valid role brief with required fields, **then** the system creates a job in `draft` status and stores an initial JD draft linked to that job.  
2. **Given** a job is in `draft` status, **when** I request “regenerate JD” with the same or updated brief, **then** the system produces a new draft version and preserves prior versions for audit.  
3. **Given** the AI provider is unavailable or times out, **when** I submit the brief, **then** the job is still created in `draft` with a clear error state and no partial overwrite of my manual text.

**Complexity:** **L**  

**Brief INVEST evaluation:**  
- **I:** Can be built behind a feature flag independent of publishing.  
- **N:** Wording, tone, and fields are negotiable with PM/legal.  
- **V:** Directly supports the “AI Copilot at JD creation” value from the PRD.  
- **E:** Estimable once LLM contract and prompt strategy are fixed.  
- **S:** Large due to LLM integration, versioning, and resilience.  
- **T:** Testable via API/UI and mocked LLM responses.

---

### US-02 — Approve job requisition and publish to configured channels

**Title:** Approve a requisition and publish the job to selected channels (career site + external boards stub)  

**Story:** As a **recruiter**, I want to **route an approved job through publishing to selected channels**, so that **candidates can discover the role and apply through tracked sources**.

**Acceptance criteria (BDD):**

1. **Given** a job in `pending_approval`, **when** an approver approves it, **then** its status becomes `approved` and publishing actions become available to authorized recruiters.  
2. **Given** an approved job, **when** I select one or more channels and confirm publish, **then** the system creates `JOB_CHANNEL` records with `published`/`failed` per channel and timestamps.  
3. **Given** a channel publish fails, **when** the publish job completes, **then** I see which channels failed, can retry per channel, and application tracking still attributes `source` correctly for successful channels.

**Complexity:** **L**  

**Brief INVEST evaluation:**  
- **I:** Depends on job existing but can use stub connectors for MVP.  
- **N:** Channel list and approval rules are negotiable.  
- **V:** Unlocks inbound applications — core funnel.  
- **E:** Estimable per connector; MVP can cap at 1–2 integrations.  
- **S:** Large due to workflow + external I/O + retries.  
- **T:** Testable with contract tests / sandbox webhooks.

---

### US-03 — Application intake with resume upload and structured parsing

**Title:** Submit an application with resume upload and AI-assisted structured profile extraction  

**Story:** As a **candidate**, I want to **apply to a published job with my resume and basic details**, so that **my skills and experience are captured consistently for recruiters**.

**Acceptance criteria (BDD):**

1. **Given** a published job with an active apply URL, **when** I submit required fields and a resume file (PDF/DOCX), **then** an `APPLICATION` is created in the initial pipeline stage and the file is stored securely (e.g., S3 with presigned access).  
2. **Given** a new application, **when** parsing completes successfully, **then** `parsed_profile` contains structured fields (skills, experience, education) aligned to the data model in `LTI-AVW.md`.  
3. **Given** parsing fails or returns low confidence, **when** the recruiter opens the application, **then** they see a visible “parse incomplete” state and can manually correct key fields before screening.

**Complexity:** **L**  

**Brief INVEST evaluation:**  
- **I:** Can ship with manual correction path without screening.  
- **N:** Parser schema and confidence thresholds negotiable.  
- **V:** Core ATS ingestion path.  
- **E:** Estimable with golden-file tests for resumes.  
- **S:** Large (uploads, PII, parsing, async jobs).  
- **T:** Testable with fixture PDFs and mocked parser.

---

### US-04 — Explainable AI screening against a per-job rubric

**Title:** Run AI screening to score an application against a job rubric with explainable breakdown and bias flags  

**Story:** As a **recruiter**, I want **each application scored against the job’s rubric with explanations and fairness flags**, so that **I can trust shortlists and comply with our DEI commitments**.

**Acceptance criteria (BDD):**

1. **Given** a job with a configured scoring rubric and an application with a parsed profile, **when** screening runs, **then** `ai_match_score`, `ai_score_breakdown`, and a human-readable explanation artifact are persisted and idempotent for the same `(application_id, rubric_version)`.  
2. **Given** screening output, **when** I view the candidate, **then** I see top strengths, gaps vs JD, and any `bias_flag` with severity and rationale fields suitable for audit.  
3. **Given** the screening service degrades, **when** screening is triggered, **then** the application remains in a queueable failed state with retry/backoff and no false “completed screening” status.

**Complexity:** **L**  

**Brief INVEST evaluation:**  
- **I:** Behind flag; can operate after intake (US-03).  
- **N:** Rubric dimensions and model behavior negotiable with compliance.  
- **V:** Primary differentiator in `LTI-AVW.md`.  
- **E:** Harder to estimate until pilot data; treat as spike + bounded MVP rubric.  
- **S:** Large (LLM + scoring + bias checks + persistence).  
- **T:** Golden scenarios + red-team prompts for bias proxy cases.

---

### US-05 — Collaborative pipeline board with stage moves and internal comments

**Title:** Move applications through a Kanban pipeline with internal comments and real-time updates  

**Story:** As a **recruiter**, I want to **move candidates across stages on a shared pipeline board and leave internal comments**, so that **hiring managers and I stay aligned without leaving the ATS**.

**Acceptance criteria (BDD):**

1. **Given** a job with ordered `PIPELINE_STAGE` rows, **when** I move an application to another stage, **then** an `APPLICATION_STAGE_LOG` entry records who moved it, timestamps, and optional scorecard payload requirements per stage rules.  
2. **Given** an application profile, **when** I add an internal comment with @mention syntax, **then** mentioned users receive in-app notification (email optional) and the thread is visible to permitted roles only.  
3. **Given** two users viewing the same job pipeline, **when** one moves a card, **then** the other user’s board reflects the change within agreed latency (e.g., ≤ 5s MVP) via WebSocket or polling fallback.

**Complexity:** **M**  

**Brief INVEST evaluation:**  
- **I:** Can start read-only board then add moves.  
- **N:** Collaboration depth negotiable (MVP: comments + moves).  
- **V:** Daily recruiter value; supports collaborative review use case.  
- **E:** Estimable by slice (CRUD vs realtime).  
- **S:** Medium (realtime adds complexity).  
- **T:** Integration tests for permissions and concurrency on stage moves.

---

## 2. MVP prioritization order (with justification)

**Recommended build order:**

| Order | Item | Rationale |
|------:|------|-----------|
| 1 | **US-01** | Establishes the `JOB` aggregate and AI JD path — prerequisite data model and permissions for everything else. |
| 2 | **US-02** | Without publish/approval, there is no trustworthy “source of truth” job state for candidates and channel analytics. |
| 3 | **US-03** | Creates `APPLICATION` + `CANDIDATE` + document storage — the funnel entry that proves end-to-end hiring flow. |
| 4 | **US-05** | Recruiters need a workable pipeline immediately; early value does not require AI scores (manual triage first). |
| 5 | **US-04** | Adds the differentiated AI screening layer once data ingestion and workflow rails exist — reduces rework if rubric/scoring changes after real applications land. |

**MVP slice narrative:** *Create → approve/publish → apply/parse → collaborate in pipeline → augment with explainable AI screening.*

---

## 3. Product backlog

**Prioritization method:** **Value vs. risk (thin vertical slices)** with a **sequential dependency** gate (job → publish → apply → workflow → AI).  

**MoSCoW tags** are shown for clarity; all five items are **Must** for the stated MVP, but **delivery is sequenced**, not parallelized blindly.

| Rank | ID | Story | Priority | MoSCoW | Complexity | Dependency notes |
|-----:|----|-------|----------|--------|------------|------------------|
| 1 | US-01 | AI-assisted job requisition draft | P0 | Must | L | None (foundational). |
| 2 | US-02 | Approve & publish to channels | P0 | Must | L | Requires US-01 job states. |
| 3 | US-03 | Application intake + parsing | P0 | Must | L | Requires published job (US-02). |
| 4 | US-05 | Pipeline board + comments + realtime | P0 | Must | M | Requires applications (US-03). |
| 5 | US-04 | Explainable AI screening + flags | P0 | Must | L | Requires parsed profile + rubric on `JOB` (US-01/03). |

**Backlog hygiene rules (for implementation kickoff):**

- Each story ships with **observability** (structured logs + trace IDs on async jobs) and **RBAC** checks on tenant boundaries (`company_id`).  
- **Definition of Ready:** schema sketch, API contract draft, UX wire for primary path, LLM failure modes documented.  
- **Definition of Done:** automated tests for happy path + permission denial + idempotent async processing where applicable.

---

## 4. First story selected — detailed work tickets (technical)

**Selected story:** **US-01 — AI-assisted job requisition draft from role brief** (first backlog item).

### Epic technical context (from `LTI-AVW.md`)

- Entities involved: **`COMPANY`**, **`USER`**, **`JOB`** (draft fields, rubric placeholder optional), future **`AI_INTERACTION_LOG`**.  
- Services alignment: **Job Service** + **AI Copilot Service** (MVP may implement Copilot as a module behind Job Service until split).

---

### Ticket T-01 — Database: core tenancy and job draft tables

**Description:** Add PostgreSQL migrations for `companies`, `users` (minimal), and `jobs` including status enum (`draft`, `pending_approval`, … stub), `role_brief` JSON, `description` text, `created_by`, timestamps.  

**Technical notes:**

- Enforce `NOT NULL` on `company_id`, `created_by`, `title`, `status`.  
- Index `(company_id, status, created_at DESC)` for list screens.  

**Definition of Done:** migration up/down verified on clean DB; seed script optional for local dev.

---

### Ticket T-02 — API: create draft job from role brief (REST)

**Description:** Implement `POST /api/v1/jobs` accepting role brief payload; returns `201` with `job_id` and `status=draft`. Validate input schema (Zod/OpenAPI).  

**Technical notes:**

- AuthN: JWT claim → `user_id`, `company_id`.  
- AuthZ: role `hiring_manager` or `recruiter` per company policy (MVP: allow both).  
- Idempotency-Key header optional for safe retries.

**Definition of Done:** contract published in OpenAPI; unit tests for validation branches.

---

### Ticket T-03 — Async job: JD generation worker + LLM adapter boundary

**Description:** Enqueue `GenerateJobDescription` task on job creation (or explicit endpoint) consumed by worker; integrate LLM via provider-agnostic adapter (`generateJdDraft(brief, tone, locale)`).  

**Technical notes:**

- Store prompt hash + model name on `AI_INTERACTION_LOG` (or MVP table) for audit.  
- Implement **timeout**, **retry with backoff**, and **circuit breaker** counters.  
- Persist output to `jobs.description` **versioned** (add `job_description_versions` table recommended).

**Definition of Done:** worker integration test with mocked LLM HTTP; failure modes covered.

---

### Ticket T-04 — Prompt templates & guardrails for JD generation

**Description:** Centralize prompt templates; enforce non-discriminatory language guardrails list (rule-based pre-check + LLM self-critique step optional).  

**Technical notes:**

- Template variables: title, level, team, skills, location policy.  
- Add **PII scrubbing** on brief fields if free text allowed.

**Definition of Done:** golden-file tests for prompt rendering; red-team examples documented.

---

### Ticket T-05 — Frontend: “New requisition” wizard (MVP)

**Description:** Multi-step form: Role brief → Review AI draft → Save draft. Handles loading/error states; uses optimistic UI only where safe.  

**Technical notes:**

- Accessibility: labels, keyboard nav, form errors.  
- Poll or subscribe for async JD completion (MVP: poll `GET /jobs/:id`).

**Definition of Done:** e2e smoke: create draft → see AI text or error banner.

---

### Ticket T-06 — Observability & audit for JD generation

**Description:** Structured logs (`job_id`, `user_id`, `latency_ms`, `provider`, `outcome`), metrics counters, trace propagation from API → queue → worker.  

**Technical notes:**

- Mask secrets; never log full prompts containing PII in production log level.

**Definition of Done:** dashboard stub or local log verification checklist.

---

### Ticket T-07 — QA harness & fixtures

**Description:** Provide dev fixtures: sample brief JSON, mocked LLM responses, PDF not needed here; document local runbook.  

**Definition of Done:** `README` section or team wiki link from repo root (optional follow-up).

---

## 5. Effort estimates (Fibonacci story points, T-shirt, hours)

**Estimation approach:** **Planning Poker–style Fibonacci** for **story points (SP)** relative to team baseline; **T-shirt** for communication; **hours** as a **planning forecast** for the first milestone (not a commitment).  

**Assumption:** 1 SP ≈ “half-day to one day of focused work” for a mature team **only as a planning anchor** — calibrate in real sprint planning.

### 5.1 Story-level sizing (for roadmap)

| Story | T-shirt | Fibonacci SP (team relative) | Notes |
|-------|---------|-------------------------------|--------|
| US-01 | L | **21** | LLM + async + UX + versioning |
| US-02 | L | **21** | Approvals + multi-channel I/O |
| US-03 | L | **21** | Uploads, PII, async parsing |
| US-04 | L | **34** | Highest uncertainty (model + fairness) |
| US-05 | M | **13** | Realtime/presence adds variance |

### 5.2 Ticket-level estimates (US-01 breakdown)

| Ticket | T-shirt | Fibonacci SP | Hours (forecast) |
|--------|---------|--------------|------------------|
| T-01 | S | **3** | 6h |
| T-02 | M | **5** | 12h |
| T-03 | L | **8** | 20h |
| T-04 | M | **5** | 12h |
| T-05 | L | **8** | 24h |
| T-06 | S | **3** | 8h |
| T-07 | S | **2** | 6h |

**Total (US-01 tickets):** **34 SP** (Planning Poker sum) · **~98 hours** forecasted engineering time (1 engineer) before calibration; parallelizing backend/frontend reduces calendar time.

---

## 6. GitHub Project — tracking stories and tickets

`gh` (GitHub CLI) is **not available** in this environment and no **`GITHUB_TOKEN`** is configured, so the project cannot be created programmatically from here. Use one of the following.

### Option A — GitHub UI (recommended, fastest)

1. Open the repository: [andresviverosw/Ai4Devs-design2-2026-03-Senior](https://github.com/andresviverosw/Ai4Devs-design2-2026-03-Senior).  
2. Go to **Projects** → **New project** → choose **Board** or **Table**.  
3. Name: **LTI AVW — MVP delivery**.  
4. Link the project to this repository (or the org) per GitHub’s linking dialog.  
5. Create custom fields (optional but useful):  
   - **Story points** (number)  
   - **T-shirt** (single select: S/M/L)  
   - **Area** (single select: Backend / Frontend / AI / Infra)  
6. Create parent items for **US-01 … US-05**, then child **Issues** for **T-01 … T-07** linked to US-01 (GitHub sub-issues / task lists, or markdown checklists in the parent issue).

### Option B — GitHub CLI later (`gh`)

After [installing GitHub CLI](https://cli.github.com/), authenticate (`gh auth login`), then you can script issue creation from this file’s tables and attach them to a Project V2. That gives you repeatable backlog imports for later sprints.

### Suggested initial board columns

**Backlog → Ready → In Progress → In Review → Done**, with **WIP limit 2** on *In Progress* for the MVP team to protect throughput.

---

*End of document.*
