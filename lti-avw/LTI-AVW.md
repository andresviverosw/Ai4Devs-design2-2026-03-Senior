# LTI Talent Tracking System — Design Document

**Document ID:** LTI-AVW  
**Version:** 1.0  
**Date:** April 2026  
**Authors:** LTI Product & Architecture Team

---

## Table of Contents

1. [Product Overview](#1-product-overview)
2. [Main Functions](#2-main-functions)
3. [Business Model — Lean Canvas](#3-business-model--lean-canvas)
4. [Use Cases](#4-use-cases)
5. [Data Model](#5-data-model)
6. [High-Level System Design](#6-high-level-system-design)
7. [C4 Diagram: AI Screening Engine](#7-c4-diagram-ai-screening-engine)

---

## 1. Product Overview

### 1.1 Description

**LTI (Lean Talent Intelligence)** is an AI-native Applicant Tracking System designed for the next generation of talent acquisition. Unlike legacy ATS platforms built on static workflows and keyword filters, LTI is architected around three foundational pillars: **real-time collaboration**, **intelligent automation**, and **deep AI assistance** — empowering HR teams and hiring managers to hire faster, fairer, and smarter.

LTI manages the full recruitment lifecycle as illustrated in the ATS process diagram: from AI-assisted job creation and multi-channel publishing, through application ingestion and AI-powered screening, to interview scheduling, online assessments, collaborative evaluation, and offer management — all in a single deeply integrated platform.

### 1.2 Added Value & Competitive Advantages

| Dimension | Legacy ATS | LTI |
|---|---|---|
| **Screening** | Rule-based keyword filters | AI semantic matching with explainable scores and bias detection |
| **Collaboration** | Email threads and static stage updates | Real-time shared pipeline with inline annotations, @mentions, and scorecards |
| **Automation** | Basic email templates | End-to-end event-driven automation engine with configurable rules |
| **Insights** | Static, periodic reports | Live dashboards with predictive hire quality and pipeline health scores |
| **Candidate Experience** | One-way black-box process | Transparent pipeline with AI-generated feedback at each stage |
| **Integration** | Limited connectors | Native connectors for 50+ job boards, HRIS systems, calendars, and assessment tools |
| **AI** | Bolted-on chatbot | LLM integrated natively across every lifecycle phase |

**Key differentiators:**

- 🤖 **AI Copilot** embedded at every workflow step: JD generation, resume scoring, interview question suggestions, offer drafting, and conversational Q&A on pipeline status.
- 👥 **Collaborative Hiring Rooms** — real-time, async-friendly workspaces where recruiters and hiring managers co-evaluate candidates using structured scorecards and live discussion threads.
- ⚡ **Event-Driven Automation Engine** — a visual rule builder with pre-built recipes that automates repetitive tasks while keeping humans in control of decisions.
- 📊 **Predictive Analytics** — AI models for hire quality prediction, offer acceptance probability, pipeline health scoring, and DEI gap detection.
- 🔍 **Semantic Search** — natural language search across all candidates, resumes, notes, and evaluations using vector embeddings.
- 🛡️ **Fairness by Design** — bias detection is embedded into the AI screening pipeline, not a post-hoc audit step.

---

## 2. Main Functions

### 2.1 Job Management
- AI-assisted job description generation from minimal input (role title, level, team context, required skills)
- Compensation benchmarking recommendations at JD creation time
- Customizable approval workflows for job requisition sign-off
- One-click multi-channel publishing to job boards (LinkedIn, Indeed, Glassdoor, Wellfound), company career pages, and social media
- Job template library with version control and cloning

### 2.2 Application Ingestion & Parsing
- Multi-source application aggregation: direct apply, email parsing, LinkedIn EasyApply, employee referrals, and agency submissions
- AI-powered resume parsing with structured data extraction: skills taxonomy, years of experience per domain, education, certifications, and inferred seniority
- Duplicate candidate detection and automatic profile merging across sources
- GDPR/CCPA-compliant data handling with per-candidate consent tracking and right-to-erasure workflows

### 2.3 AI-Powered Screening
- Semantic matching between candidate profiles and job requirements — goes beyond keyword overlap to understand contextual relevance
- Customizable multi-criteria scoring rubrics per role (e.g., skills depth, culture fit signals, seniority calibration)
- Automated bias detection: flags screening criteria or score rationale that proxies protected attributes
- Shortlist generation with explainable AI scoring: ranked reasons per candidate surfaced to recruiter

### 2.4 Collaborative Review Pipeline
- Kanban-style pipeline view shared in real time across all stakeholders
- Inline commenting, @mentions, reactions, and private notes on candidate profiles
- Structured scorecards per pipeline stage with aggregate team scoring
- Conflict-of-interest detection and recusal workflow for interviewers with prior relationships

### 2.5 Assessments & Tests
- Built-in assessment library: coding challenges, cognitive aptitude, and situational judgment tests
- Third-party assessment integrations: HackerRank, Codility, Pymetrics, and others via webhook
- Automated proctoring hooks and result ingestion
- Assessment result normalization and integration into candidate composite score

### 2.6 Interview Scheduling
- AI-optimized scheduling that cross-checks all interviewer calendars, preferred time zones, and interview load balance
- Self-serve candidate scheduling portal with automated multi-channel reminders
- Panel interview coordination with automatic conflict detection
- AI-generated interview prep packets per interviewer: candidate summary, tailored question suggestions, and scorecard template

### 2.7 Offer Management
- Offer letter generation with integrated compensation benchmarking data
- Configurable offer approval workflows with version tracking
- Digital signing integrations: DocuSign and HelloSign
- Counter-offer and negotiation state tracking
- Backup candidate auto-activation on offer decline

### 2.8 Analytics & Reporting
- Real-time pipeline dashboards: funnel conversion rates, time-to-fill, cost-per-hire, source quality
- DEI metrics tracking and gap analysis per pipeline stage
- Hiring manager and interviewer satisfaction scores (NPS)
- Predictive models: offer acceptance probability, candidate drop-off risk, hire quality forecast

### 2.9 Automation Engine
- Visual no-code workflow builder for custom automation rules
- Pre-built automation recipes (e.g., "Auto-advance if assessment score > 80", "Notify hiring manager when 5 candidates reach final round", "Send rejection if idle > 14 days")
- Event-driven webhook platform for custom integrations
- Audit log of all automated actions with human override capability

### 2.10 AI Copilot
- Contextual assistant available on every screen in the platform
- Capabilities: summarize candidate profile, suggest interview questions, flag profile inconsistencies, draft rejection or offer emails, answer pipeline questions in natural language
- Memory across a hiring cycle: Copilot retains context of prior candidate evaluations within a job

---

## 3. Business Model — Lean Canvas

```mermaid
%%{init: {'theme': 'base'}}%%
graph TB
    subgraph CANVAS["LTI — Lean Canvas"]
        direction TB

        subgraph TOP[" "]
            direction LR
            P["📌 PROBLEM\n──────────────────\n1. Legacy ATS tools rely on\n   keyword filters — poor\n   candidate quality signal\n2. Collaboration happens\n   outside the system via\n   email and spreadsheets\n3. AI is a bolt-on feature,\n   not core to the workflow\n4. Scheduling and coordination\n   consumes recruiter time\n5. Poor candidate experience\n   causes drop-off at key stages"]

            SOL["💡 SOLUTION\n──────────────────\nAI-native ATS platform with:\n• Semantic resume scoring\n  + explainable AI shortlists\n• Real-time Collaborative\n  Hiring Rooms with scorecards\n• Event-driven Automation\n  Engine with no-code builder\n• AI Copilot embedded across\n  every lifecycle phase\n• Integrated scheduling,\n  assessments, and e-signing"]

            UVP["⭐ UNIQUE VALUE\nPROPOSITION\n──────────────────\nHire smarter,\nfaster, and fairer.\n\nThe only ATS where AI\nis not a feature — it\nis the foundation.\n\nCut time-to-hire 40%.\nImprove DEI outcomes.\nKeep humans in control\nof every decision."]

            UA["🔒 UNFAIR\nADVANTAGE\n──────────────────\n• Proprietary AI scoring\n  model trained on hiring\n  outcome data\n• Bias detection embedded\n  in screening pipeline\n• Deep calendar + HRIS\n  native integrations\n• Network effects from\n  recruiter community\n• Compound data flywheel:\n  more hires → better model"]

            CS["👥 CUSTOMER\nSEGMENTS\n──────────────────\nPrimary:\n• Mid-market companies\n  (100–5,000 employees)\n• High-volume hiring teams\n• Tech-forward HR orgs\n\nSecondary:\n• RPO firms\n• Staffing agencies\n\nEarly adopters:\n• Series A/B startups\n  scaling teams fast"]
        end

        subgraph MID[" "]
            direction LR
            KM["📊 KEY METRICS\n──────────────────\n• Time-to-hire reduction\n• Recruiter NPS (target: 50+)\n• Candidate satisfaction score\n• AI screening precision/recall\n• Monthly active users (MAU)\n• Pipeline stage conversion rate\n• Churn rate by tier\n• Revenue per recruiter seat"]

            CH["📢 CHANNELS\n──────────────────\nInbound:\n• SEO + HR thought leadership\n• HR community presence\n  (SHRM, People Ops forums)\nOutbound:\n• SDR + LinkedIn ABM\n• HR tech conference presence\nPartnerships:\n• HRIS vendor co-selling\n• HR consulting firms\nProduct-led:\n• Freemium / 30-day trial\n• Recruiter referral program"]
        end

        subgraph BOT[" "]
            direction LR
            COST["💸 COST STRUCTURE\n──────────────────\n• LLM API costs\n  (Anthropic / OpenAI)\n• Engineering team\n  (~50% of burn)\n• Cloud infrastructure\n  (AWS — compute, storage,\n  vector DB, CDN)\n• Sales & Marketing\n• Customer Success\n• Compliance (SOC2,\n  GDPR, CCPA legal)"]

            REV["💰 REVENUE STREAMS\n──────────────────\nSaaS subscription tiers:\n• Starter — up to 5 users\n• Growth — up to 50 users\n• Enterprise — unlimited\n  + SSO + SLA + dedicated CS\n\nAdditional streams:\n• Per-seat pricing for\n  large enterprise orgs\n• Premium AI features add-on\n• API access for integrators\n• Onboarding + PS fees"]
        end
    end
```

---

## 4. Use Cases

The three core use cases map directly to the most critical phases of the ATS lifecycle: job creation and publishing, collaborative application review, and interview-to-hire closing.

---

### 4.1 Use Case 1 — AI-Assisted Job Creation & Multi-Channel Publishing

**Description:** A hiring manager initiates a job requisition. The AI Copilot assists in drafting the job description using the role brief as input. The draft goes through a configurable approval workflow before the recruiter publishes it simultaneously to multiple job boards and the company career page. The system then tracks application volume per channel.

**Primary Actor:** Hiring Manager  
**Supporting Actors:** Recruiter, Approval Authority (HR Director), AI Copilot, External Job Boards

```mermaid
flowchart TD
    HM([👤 Hiring Manager])
    REC([👤 Recruiter])
    AUTH([👤 Approval Authority])
    AI([🤖 AI Copilot])
    EXT([🌐 Job Boards])

    HM --> UC1[Request Job Requisition]
    HM --> UC2[Provide Role Brief\ntitle · level · team · skills]

    UC1 & UC2 --> UC3[AI Generates JD Draft]
    AI -.->|drafts JD| UC3
    AI -.->|suggests compensation range| UC4[Compensation Benchmarking]

    UC3 & UC4 --> UC5[Review & Edit JD]
    HM --> UC5

    UC5 --> UC6[Submit Requisition for Approval]
    AUTH --> UC7[Review & Approve / Reject]
    UC6 --> UC7

    UC7 -->|approved| UC8[Configure Publishing Channels]
    UC7 -->|rejected with comments| UC9[Revise JD]
    UC9 --> UC5

    REC --> UC8
    UC8 --> UC10[Publish to Job Boards]
    UC8 --> UC11[Publish to Career Page]
    UC8 --> UC12[Share on Social Media]

    EXT -.->|receives posting| UC10

    UC10 & UC11 & UC12 --> UC13[Track Applications by Source]

    style HM fill:#6366f1,color:#fff
    style REC fill:#6366f1,color:#fff
    style AUTH fill:#6366f1,color:#fff
    style AI fill:#f59e0b,color:#000
    style EXT fill:#10b981,color:#fff
```

---

### 4.2 Use Case 2 — Collaborative Application Review with AI Screening

**Description:** Applications received from multiple sources are parsed and ingested. The AI Screening Engine scores and ranks candidates against the job's rubric, returning an explainable shortlist with bias flags. Recruiters and hiring managers then collaborate in a shared pipeline view, using structured scorecards and inline discussion to advance, hold, or reject candidates.

**Primary Actor:** Recruiter  
**Supporting Actors:** Candidate, Hiring Manager, AI Screening Engine

```mermaid
flowchart TD
    CAND([👤 Candidate])
    REC([👤 Recruiter])
    HM([👤 Hiring Manager])
    AI([🤖 AI Engine])

    CAND --> UC1[Submit Application\nresume · cover letter · source]
    UC1 --> UC2[Parse & Structure Profile]
    AI -.->|NLP parsing| UC2

    UC2 --> UC3[Generate Candidate Embeddings]
    AI -.->|vector embedding| UC3

    UC3 --> UC4[Score Against Job Rubric]
    AI -.->|multi-criteria scoring| UC4

    UC4 --> UC5[Bias & Fairness Check]
    AI -.->|detect protected proxies| UC5

    UC4 & UC5 --> UC6[Generate Explainable Scorecard\nstrengths · gaps · flags]
    AI -.->|LLM explanation| UC6

    UC6 --> UC7[Recruiter Reviews Shortlist]
    REC --> UC7
    REC --> UC8[Add Tags / Annotations]
    REC --> UC9[Move Stage / Reject]

    UC7 & UC8 --> UC10[Collaborative Pipeline View\nshared real-time kanban]

    HM --> UC10
    HM --> UC11[Rate on Structured Scorecard]
    HM --> UC12[Request More Info from Candidate]

    UC11 --> UC13[Aggregate Team Scores]
    AI -.->|consensus scoring| UC13
    UC13 --> UC14[Final Shortlist Decision]

    UC14 -->|advance| UC15[Move to Assessment / Interview Stage]
    UC14 -->|hold| UC16[Parking Lot Pool]
    UC14 -->|reject| UC17[AI-Drafted Rejection Email + Feedback]
    UC12 --> UC18[Notify Candidate / Recruiter]

    style CAND fill:#ec4899,color:#fff
    style REC fill:#6366f1,color:#fff
    style HM fill:#6366f1,color:#fff
    style AI fill:#f59e0b,color:#000
```

---

### 4.3 Use Case 3 — Assessment, Interview Scheduling & Hire Decision

**Description:** A shortlisted candidate is assigned an online assessment. On passing, the AI Scheduling Engine finds optimal interview slots across all required interviewers. The candidate self-schedules. Each interviewer receives an AI-generated prep packet. After interviews, structured scorecards feed an AI-synthesized hire recommendation. Upon approval, an offer is drafted, routed through an approval workflow, and sent digitally for signature.

**Primary Actor:** Recruiter  
**Supporting Actors:** Candidate, Hiring Manager, Interviewers, AI Copilot, Calendar Systems, E-Signature Provider

```mermaid
flowchart TD
    CAND([👤 Candidate])
    REC([👤 Recruiter])
    HM([👤 Hiring Manager])
    INT([👤 Interviewers])
    AI([🤖 AI Copilot])
    CAL([📅 Calendar Systems])
    SIGN([✍️ E-Signature])

    REC --> UC1[Assign Online Assessment]
    CAND --> UC2[Complete Assessment]
    UC1 --> UC2
    UC2 --> UC3[Ingest & Normalize Results]
    AI -.->|evaluates results| UC3

    UC3 --> UC4{Pass Threshold?}
    UC4 -->|pass| UC5[Trigger Interview Scheduling]
    UC4 -->|fail| UC6[Automated Rejection\n+ Personalised Feedback]
    AI -.->|drafts feedback| UC6

    UC5 --> UC7[AI Finds Optimal Time Slots]
    AI -.->|optimises across time zones| UC7
    CAL -.->|availability data| UC7

    UC7 --> UC8[Candidate Self-Schedules via Portal]
    CAND --> UC8
    UC8 --> UC9[Generate Interview Prep Packets]
    AI -.->|tailored per interviewer| UC9

    UC9 --> UC10[Conduct Interviews]
    INT --> UC10

    UC10 --> UC11[Submit Structured Scorecards]
    INT --> UC11

    UC11 --> UC12[AI Synthesises Feedback]
    AI -.->|aggregate + highlight themes| UC12
    UC12 --> UC13[Hire Recommendation Report]
    AI -.->|generates recommendation| UC13

    HM --> UC14[Review Recommendation]
    UC13 --> UC14

    UC14 -->|hire| UC15[Draft Offer Letter]
    UC14 -->|no hire| UC16[Close Application\n+ Notify Candidate]

    AI -.->|drafts offer with benchmarking| UC15
    UC15 --> UC17[Offer Approval Workflow]
    UC17 -->|approved| UC18[Send Offer to Candidate]
    SIGN -.->|e-signature flow| UC18

    CAND --> UC19{Candidate Decision}
    UC18 --> UC19
    UC19 -->|accept| UC20[Trigger Onboarding Handoff\nto HRIS]
    UC19 -->|decline| UC21[Activate Backup Candidates\nfrom Parking Lot]

    style CAND fill:#ec4899,color:#fff
    style REC fill:#6366f1,color:#fff
    style HM fill:#6366f1,color:#fff
    style INT fill:#6366f1,color:#fff
    style AI fill:#f59e0b,color:#000
    style CAL fill:#10b981,color:#fff
    style SIGN fill:#10b981,color:#fff
```

---

## 5. Data Model

The data model covers all core entities across the LTI ATS lifecycle. The primary relationship chain is: **Company → User → Job → Application → Candidate → Pipeline Stage → Interview → Offer**. Supporting entities handle AI interactions, automation rules, and collaboration artifacts.

```mermaid
erDiagram

    COMPANY {
        uuid id PK
        string name
        string domain
        string industry
        string size_tier
        string subscription_plan
        jsonb settings
        timestamp created_at
    }

    USER {
        uuid id PK
        uuid company_id FK
        string email
        string full_name
        string role
        string[] permissions
        boolean is_active
        timestamp created_at
        timestamp last_login
    }

    JOB {
        uuid id PK
        uuid company_id FK
        uuid created_by FK
        uuid approved_by FK
        string title
        string department
        string location
        string employment_type
        string seniority_level
        text description
        text requirements
        jsonb compensation_range
        string status
        integer headcount
        jsonb scoring_rubric
        timestamp published_at
        timestamp closed_at
        timestamp created_at
    }

    JOB_CHANNEL {
        uuid id PK
        uuid job_id FK
        string channel_name
        string external_job_id
        string status
        timestamp published_at
        timestamp expires_at
        integer applications_received
    }

    CANDIDATE {
        uuid id PK
        string email
        string full_name
        string phone
        string linkedin_url
        string github_url
        string location
        string source
        jsonb parsed_profile
        vector embedding
        boolean gdpr_consent
        timestamp gdpr_consent_at
        timestamp created_at
        timestamp updated_at
    }

    APPLICATION {
        uuid id PK
        uuid job_id FK
        uuid candidate_id FK
        uuid assigned_recruiter FK
        string status
        string source
        float ai_match_score
        jsonb ai_score_breakdown
        text cover_letter
        string resume_url
        boolean duplicate_flag
        timestamp submitted_at
        timestamp updated_at
    }

    PIPELINE_STAGE {
        uuid id PK
        uuid company_id FK
        uuid job_id FK
        string name
        integer order_index
        string stage_type
        jsonb automation_rules
        boolean requires_scorecard
    }

    APPLICATION_STAGE_LOG {
        uuid id PK
        uuid application_id FK
        uuid stage_id FK
        uuid moved_by FK
        string status
        jsonb scorecard_data
        float aggregate_score
        text notes
        timestamp entered_at
        timestamp exited_at
    }

    ASSESSMENT {
        uuid id PK
        uuid application_id FK
        string provider
        string test_type
        string external_test_id
        string status
        float raw_score
        float normalized_score
        jsonb detailed_results
        boolean passed_threshold
        timestamp assigned_at
        timestamp completed_at
    }

    INTERVIEW {
        uuid id PK
        uuid application_id FK
        uuid scheduled_by FK
        string interview_type
        string status
        timestamp scheduled_at
        integer duration_minutes
        string location_or_link
        jsonb prep_packet
        timestamp created_at
    }

    INTERVIEW_PANEL {
        uuid id PK
        uuid interview_id FK
        uuid interviewer_id FK
        string role_in_panel
        boolean confirmed
        jsonb scorecard
        float score
        string recommendation
        text feedback
        boolean bias_flag
        timestamp submitted_at
    }

    OFFER {
        uuid id PK
        uuid application_id FK
        uuid created_by FK
        uuid approved_by FK
        float base_salary
        string currency
        jsonb compensation_details
        string status
        string document_url
        string signing_provider
        string signing_status
        timestamp sent_at
        timestamp responded_at
        timestamp expires_at
        timestamp created_at
    }

    TAG {
        uuid id PK
        uuid company_id FK
        string name
        string color
        string entity_type
    }

    APPLICATION_TAG {
        uuid application_id FK
        uuid tag_id FK
        uuid added_by FK
        timestamp added_at
    }

    COMMENT {
        uuid id PK
        uuid application_id FK
        uuid author_id FK
        text content
        boolean is_internal
        uuid parent_comment_id FK
        timestamp created_at
        timestamp edited_at
    }

    AUTOMATION_RULE {
        uuid id PK
        uuid company_id FK
        uuid job_id FK
        string name
        string trigger_event
        jsonb conditions
        jsonb actions
        boolean is_active
        integer executions_count
        timestamp created_at
    }

    AI_INTERACTION_LOG {
        uuid id PK
        uuid company_id FK
        uuid user_id FK
        uuid entity_id FK
        string entity_type
        string interaction_type
        jsonb input_context
        jsonb ai_output
        float confidence_score
        boolean bias_flag
        timestamp created_at
    }

    COMPANY ||--o{ USER : "has members"
    COMPANY ||--o{ JOB : "posts"
    COMPANY ||--o{ PIPELINE_STAGE : "defines"
    COMPANY ||--o{ TAG : "creates"
    COMPANY ||--o{ AUTOMATION_RULE : "configures"
    USER ||--o{ JOB : "creates / approves"
    JOB ||--o{ JOB_CHANNEL : "published via"
    JOB ||--o{ APPLICATION : "receives"
    JOB ||--o{ PIPELINE_STAGE : "uses"
    CANDIDATE ||--o{ APPLICATION : "submits"
    APPLICATION ||--o{ APPLICATION_STAGE_LOG : "tracked through"
    APPLICATION ||--o{ ASSESSMENT : "assigned"
    APPLICATION ||--o{ INTERVIEW : "scheduled for"
    APPLICATION ||--o{ OFFER : "generates"
    APPLICATION ||--o{ APPLICATION_TAG : "tagged with"
    APPLICATION ||--o{ COMMENT : "annotated with"
    PIPELINE_STAGE ||--o{ APPLICATION_STAGE_LOG : "records"
    INTERVIEW ||--o{ INTERVIEW_PANEL : "includes"
    USER ||--o{ INTERVIEW_PANEL : "participates in"
    TAG ||--o{ APPLICATION_TAG : "applied to"
    USER ||--o{ COMMENT : "writes"
    USER ||--o{ AI_INTERACTION_LOG : "triggers"
```

---

## 6. High-Level System Design

### 6.1 Architectural Overview

LTI follows a **cloud-native, domain-driven microservices architecture** deployed on AWS. A React/TypeScript SPA and progressive mobile web app communicate with backend services through a unified API Gateway. Six core domain services reflect the natural subdomains of the recruitment lifecycle. An AI Services Layer provides screening, copilot, embedding, and automation capabilities as independently scalable services. An event bus (AWS EventBridge) powers asynchronous workflows across all domains.

### 6.2 Key Architectural Decisions

| Decision | Choice | Rationale |
|---|---|---|
| **API surface** | API Gateway (Kong) | Unified auth, rate limiting, and routing across all microservices |
| **Service decomposition** | Domain-driven microservices | Independent scaling; the AI Screening Service requires GPU instances during bulk ingestion |
| **Async workflows** | AWS EventBridge | Decoupled automation triggers; reliable event replay and audit trail |
| **Primary datastore** | PostgreSQL + pgvector | Relational integrity + native vector similarity search for semantic candidate matching |
| **Cache & queue** | Redis | Session management, job queue for async screening tasks, real-time pub/sub |
| **Document storage** | AWS S3 + presigned URLs | Secure, scalable storage for resumes and offer documents |
| **Real-time collaboration** | WebSocket Service | Low-latency pipeline updates, live annotations, @mention notifications |
| **Search** | OpenSearch | Full-text search across candidate profiles, notes, and job history |
| **LLM access** | Abstracted LLM Service | Provider-agnostic; switch between Anthropic, OpenAI, and AWS Bedrock without service changes |

### 6.3 Architecture Diagram

```mermaid
graph TB
    subgraph CLIENT["🖥️ Client Layer"]
        WEB["React / TypeScript SPA"]
        MOB["Mobile PWA"]
    end

    subgraph EDGE["🌐 Edge & Gateway Layer"]
        CDN["CloudFront CDN\n(static assets)"]
        GW["API Gateway — Kong\n(auth · rate limiting · routing)"]
        AUTH["Auth Service\nOAuth2 / JWT / SSO"]
        WSS["WebSocket Service\n(real-time collab)"]
    end

    subgraph CORE["⚙️ Core Domain Services"]
        JS["Job Service\nJob CRUD · Approvals\nTemplates · Publishing"]
        AS["Application Service\nIngestion · Parsing\nDedup · Source Tracking"]
        PS["Pipeline Service\nStages · Scorecards\nCollaboration · Tags"]
        IS["Interview Service\nScheduling · Panels\nPrep Packets · Reminders"]
        OS["Offer Service\nDrafting · Approvals\nSigning · Onboarding"]
        NS["Notification Service\nEmail · In-app · Slack · SMS"]
    end

    subgraph AI_LAYER["🤖 AI Services Layer"]
        SCR["AI Screening Engine\nParsing · Embedding · Scoring\nRanking · Bias Detection"]
        COP["AI Copilot Service\nJD Gen · Summaries\nQ&A · Email Drafting"]
        EMB["Embedding Service\nProfile Vectors\nSemantic Search Index"]
        AUT["Automation Engine\nRule Builder · Triggers\nRecipes · Audit Log"]
    end

    subgraph DATA["🗄️ Data Layer"]
        PG[("PostgreSQL\n+ pgvector\nCore relational data\n+ vector index")]
        RD[("Redis\nCache + Job Queue\n+ Pub/Sub")]
        S3[("AWS S3\nResumes · Documents\nOffer Letters")]
        ES[("OpenSearch\nFull-text search")]
    end

    subgraph INTEGRATIONS["🔗 External Integrations"]
        JB["Job Boards\nLinkedIn · Indeed\nGlassdoor · Wellfound"]
        CAL["Calendars\nGoogle · Outlook\nCal.com"]
        HRIS["HRIS Systems\nWorkday · BambooHR\nRippling"]
        ASSESS["Assessments\nHackerRank · Codility\nPymetrics"]
        SIGN["E-Signature\nDocuSign · HelloSign"]
        LLM["LLM Providers\nAnthropic Claude\nOpenAI · AWS Bedrock"]
    end

    subgraph OBS["📊 Observability"]
        LOG["CloudWatch\nLogs"]
        MET["Datadog\nMetrics + APM"]
        TRC["OpenTelemetry\nDistributed Tracing"]
    end

    WEB & MOB --> CDN
    CDN --> GW
    WEB & MOB <--> WSS

    GW --> AUTH
    GW --> JS & AS & PS & IS & OS & NS

    AS --> SCR
    PS --> COP
    JS --> COP
    IS --> COP
    OS --> COP

    SCR & COP --> EMB
    AUT --> JS & AS & PS & IS & NS

    JS & AS & PS & IS & OS --> PG
    SCR & EMB --> PG
    AS --> S3
    AS & PS --> RD
    AS & PS --> ES

    JS --> JB
    IS --> CAL
    OS --> SIGN
    AS --> ASSESS
    PS --> HRIS

    SCR & COP & EMB --> LLM

    CORE --> LOG & MET & TRC
    AI_LAYER --> LOG & MET & TRC
```

---

## 7. C4 Diagram: AI Screening Engine

The **AI Screening Engine** is LTI's most technically differentiated component. It is responsible for parsing incoming resumes, generating semantic embeddings, scoring candidates against job rubrics, detecting potential bias in scoring rationale, and returning ranked shortlists with explainable scores. We detail this component across C4 levels 1–3.

---

### 7.1 C4 Level 1 — System Context

```mermaid
C4Context
    title AI Screening Engine — System Context

    Person(recruiter, "Recruiter", "Configures screening criteria and reviews AI-generated shortlists")
    Person(hiringMgr, "Hiring Manager", "Defines role requirements; approves ranked shortlist")

    System(lti, "LTI ATS Platform", "Manages full recruitment lifecycle including AI-powered candidate screening")

    System_Ext(llm, "LLM Provider (Anthropic / OpenAI)", "Provides language model capabilities for structured parsing, rubric scoring, bias detection, and explanation generation")
    System_Ext(embApi, "Embedding API (OpenAI / Cohere)", "Generates dense vector representations of candidate profiles and job descriptions")
    System_Ext(jobBoards, "Job Boards & Email Parsers", "Source of inbound application documents and structured profiles")

    Rel(recruiter, lti, "Configures rubric, reviews shortlist, adjusts thresholds", "HTTPS")
    Rel(hiringMgr, lti, "Defines job requirements, views ranked candidates", "HTTPS")
    Rel(lti, llm, "Sends prompts for parsing, scoring, bias checks, and explanations", "HTTPS REST")
    Rel(lti, embApi, "Requests vector embeddings for profiles and JDs", "HTTPS REST")
    Rel(jobBoards, lti, "Pushes applications and resume documents", "Webhook / API")
```

---

### 7.2 C4 Level 2 — Container Diagram

```mermaid
C4Container
    title AI Screening Engine — Container Diagram

    Person(recruiter, "Recruiter")
    Person(hiringMgr, "Hiring Manager")

    System_Boundary(lti, "LTI ATS Platform") {
        Container(spa, "React SPA", "TypeScript / React", "Screening criteria configuration UI and candidate shortlist review views")
        Container(apiGw, "API Gateway", "Kong", "Routes requests, enforces JWT auth and rate limits")
        Container(appSvc, "Application Service", "Node.js / Express / TypeScript", "Receives application submissions, stores raw data, enqueues screening tasks")
        Container(screeningEngine, "AI Screening Engine", "Python / FastAPI", "Core AI service: resume parsing, embedding, multi-criteria scoring, bias detection, ranking, and explanation generation")
        Container(copilotSvc, "AI Copilot Service", "Python / FastAPI", "Conversational assistant service; uses screening output as context for recruiter Q&A")
        Container(db, "Primary Database", "PostgreSQL 15 + pgvector", "Stores applications, candidate profiles, AI scores, and vector embeddings")
        Container(docStore, "Document Store", "AWS S3", "Stores raw resume files, PDFs, and parsed document artefacts")
        Container(cache, "Cache & Task Queue", "Redis 7", "Async screening job queue; score caching; real-time pub/sub for pipeline updates")
        Container(search, "Search Index", "OpenSearch", "Full-text search over candidate profiles, notes, and job data")
    }

    System_Ext(llm, "LLM Provider", "Anthropic Claude / OpenAI GPT-4")
    System_Ext(embApi, "Embedding API", "OpenAI text-embedding-3 / Cohere embed")

    Rel(recruiter, spa, "Configures criteria; reviews shortlist", "HTTPS")
    Rel(hiringMgr, spa, "Reviews ranked candidates", "HTTPS")
    Rel(spa, apiGw, "REST API calls", "HTTPS")
    Rel(apiGw, appSvc, "Routes application events", "HTTP")
    Rel(apiGw, screeningEngine, "Triggers screening; fetches results", "HTTP")
    Rel(appSvc, docStore, "Stores uploaded resume files", "AWS SDK")
    Rel(appSvc, cache, "Enqueues screening tasks", "Redis LPUSH")
    Rel(screeningEngine, cache, "Consumes task queue", "Redis BRPOP")
    Rel(screeningEngine, db, "Reads job rubric; writes scores and embeddings", "SQL + pgvector ANN")
    Rel(screeningEngine, docStore, "Fetches resume files for parsing", "AWS SDK presigned URL")
    Rel(screeningEngine, llm, "Sends parsing, scoring, bias-check, and explanation prompts", "HTTPS")
    Rel(screeningEngine, embApi, "Generates candidate and JD embedding vectors", "HTTPS")
    Rel(screeningEngine, search, "Indexes parsed candidate profiles", "OpenSearch REST")
    Rel(copilotSvc, db, "Reads candidate profiles and score breakdowns for context", "SQL")
    Rel(copilotSvc, llm, "Generates conversational responses with retrieval context", "HTTPS")
```

---

### 7.3 C4 Level 3 — Component Diagram (AI Screening Engine)

```mermaid
C4Component
    title AI Screening Engine — Component Diagram (Python / FastAPI)

    Container_Boundary(screeningEngine, "AI Screening Engine") {
        Component(api, "Screening API", "FastAPI router", "REST endpoints: trigger job, get results, update rubric, get shortlist")
        Component(orchestrator, "Screening Orchestrator", "Celery worker + workflow graph", "Coordinates the 8-step screening pipeline as an async DAG; manages retries, timeouts, and partial results with checkpointing")
        Component(ingestor, "Resume Ingestor", "Python — pypdf2, docx2txt, html2text", "Fetches resume from S3 via presigned URL; extracts raw text from PDF, DOCX, and HTML formats")
        Component(parser, "Profile Parser", "Python + LLM prompt", "Sends raw resume text to LLM with a structured extraction prompt; returns normalised JSON: skills taxonomy, years per domain, education, certifications, and inferred seniority")
        Component(embedder, "Embedding Generator", "Python — numpy, pgvector client", "Calls Embedding API for candidate profile text and JD text; stores resulting vectors in pgvector; updates the ANN index")
        Component(matcher, "Semantic Matcher", "Python — pgvector cosine ANN", "Queries pgvector index for top-N candidates most similar to the JD embedding; returns ranked candidate IDs with similarity scores")
        Component(scorer, "Multi-Criteria Scorer", "Python + LLM prompt chain", "Scores each shortlisted candidate on rubric dimensions defined per job (e.g., skills depth, seniority fit, leadership signals); aggregates dimension scores into a weighted composite")
        Component(biasDetector, "Bias & Fairness Detector", "Python + LLM + rules engine", "Analyses scoring rationale for protected attribute proxies (gender, age, ethnicity signals); applies configurable fairness constraints; emits structured bias flags with severity level")
        Component(ranker, "Ranking & Shortlist Engine", "Python — pandas / scoring module", "Combines semantic similarity, rubric composite score, and bias-adjusted weights to produce a final ranked shortlist; applies configurable shortlist size cap")
        Component(explainer, "Explainability Module", "Python + LLM prompt", "Calls LLM to generate a human-readable score breakdown per candidate: top 3 strengths, key gaps vs JD, and recommended interview focus areas")
        Component(criteriaStore, "Rubric & Criteria Store", "Python — repository pattern", "Reads and caches job-level scoring rubrics, fairness configuration, and threshold settings from PostgreSQL")
    }

    ContainerDb(db, "PostgreSQL + pgvector", "Profiles, scores, embeddings, bias flags, rubrics")
    ContainerDb(docStore, "S3 Document Store", "Raw resume files")
    Container_Ext(llm, "LLM Provider", "Claude / GPT-4o")
    Container_Ext(embApi, "Embedding API", "OpenAI / Cohere")
    Container_Ext(cache, "Redis Queue", "Celery broker + result backend")

    Rel(api, orchestrator, "Submits screening job with application_id + job_id")
    Rel(cache, orchestrator, "Delivers task from queue")
    Rel(orchestrator, criteriaStore, "Step 0: load rubric and thresholds")
    Rel(criteriaStore, db, "Reads rubric config")
    Rel(orchestrator, ingestor, "Step 1: fetch and extract resume text")
    Rel(ingestor, docStore, "GET resume file via presigned URL")
    Rel(orchestrator, parser, "Step 2: structure raw text into normalised profile")
    Rel(parser, llm, "Extraction prompt with schema")
    Rel(parser, db, "Write parsed profile JSON")
    Rel(orchestrator, embedder, "Step 3: vectorise candidate profile")
    Rel(embedder, embApi, "POST text → embedding vector")
    Rel(embedder, db, "Upsert candidate vector into pgvector")
    Rel(orchestrator, matcher, "Step 4: semantic similarity search")
    Rel(matcher, db, "ANN cosine search vs JD vector")
    Rel(orchestrator, scorer, "Step 5: multi-criteria rubric scoring")
    Rel(scorer, llm, "Scoring prompt with rubric and candidate profile")
    Rel(scorer, db, "Write dimension scores")
    Rel(orchestrator, biasDetector, "Step 6: fairness check on scores and rationale")
    Rel(biasDetector, llm, "Bias analysis prompt")
    Rel(biasDetector, db, "Write bias flags and severity")
    Rel(orchestrator, ranker, "Step 7: compute final ranked shortlist")
    Rel(ranker, db, "Write ranked shortlist with composite scores")
    Rel(orchestrator, explainer, "Step 8: generate per-candidate explanations")
    Rel(explainer, llm, "Explanation prompt with scores and rationale")
    Rel(explainer, db, "Write score breakdown and interview focus areas")
```

---

*Document: **LTI-AVW v1.0** — LTI Talent Tracking System Design*  
*Generated: April 2026 | All diagrams rendered with Mermaid*
