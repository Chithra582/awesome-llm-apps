# EXPLAINABILITY.md

This document explains the internal mechanisms, data lineage, operational boundaries, and governance framework of **Awesome LLM Apps Catalog Agent** (`awesome-llm-apps`) in accordance with the **OpenGAP v0.1.0** specification for the **HiDevs GitAgent Passport** clearance pipeline.

> **Agent Name:** Awesome LLM Apps Catalog Agent (`awesome-llm-apps`)  
> **Specification:** OpenGAP v0.1.0  
> **Category / Domain:** Developer Tools / Production LLM Applications & Agent Architectures  
> **Compliance Standard:** OpenGAP Checkpoint 2 (Explainability & Decision Governance), OWASP LLM Top 10, MITRE ATLAS  

---

## How the Agent Decides

Awesome LLM Apps Catalog Agent is an intelligent architectural advisor and catalog discovery engine designed to navigate and analyze over 100 open-source, production-grade AI agent applications, modular agent skills, voice agents, and RAG architectures. Its primary operational purpose is to accelerate software engineering teams in selecting, architecting, and deploying verifiable LLM applications without vendor lock-in.

### 1. Decision Architecture

The application discovery, topology evaluation, and scaffolding generation pipeline operates across a deterministic, five-stage architecture:

```
Developer Query / Architecture Requirement (Domain / Latency SLA / Tool Specs / Framework)
    │
    ▼
[Stage 1: Intent & Constraint Parsing]
    │  - Decomposes developer queries into domain, latency SLA, modality, and framework criteria
    │  - Determines paradigm match: Single-Agent, Multi-Agent Debate, SOP Pipeline, or RAG Stack
    │  - Initializes local catalog index search filters
    ▼
[Stage 2: Catalog Filtering & Affinity Scoring]
    │  - Scans index of 100+ verified production LLM application templates
    │  - Computes affinity scores across supported model providers and license constraints
    │  - Filters out deprecated patterns lacking automated evaluation fixtures
    ▼
[Stage 3: Topology Assessment & Blueprint Synthesis]
    │  - Formulates comparative trade-off blueprints across candidate architectures
    │  - Synthesizes modular boilerplates (`agent.py`, `tools.py`, `eval.py`)
    │  - Enforces least-privilege tool execution permissions and environment isolation
    ▼
[Stage 4: Security Verification & Guardrail Audit]
    │  - Audits synthesized blueprints for loop ceilings, prompt injection defenses, and error fallbacks
    │  - Runs AST linting and dependency license compliance checks
    │  - Verifies that external write operations are bound to human approval gates
    ▼
[Stage 5: Artifact Packaging & Handover]
    │  - Delivers ready-to-run repository structures to the local workspace
    │  - Generates comprehensive architectural diagrams and setup guides
    │  - Archives structured decision traces for human engineering review
    ▼
Validated LLM Application Blueprint & Auditable Catalog Trajectory Record
```

### 2. Decision Logic & Recommendation Formulations

The catalog agent evaluates application template affinity, latency feasibility, and architectural fit using deterministic mathematical models:

1. **Application Template Affinity Score ($S_{\text{app}}$)**:
   $$S_{\text{app}} = (w_d \cdot D_{\text{domain}}) + (w_l \cdot L_{\text{latency}}) + (w_m \cdot M_{\text{modal}})$$
   where:
   - $D_{\text{domain}} \in [0, 1]$ represents semantic keyword alignment with application domains (RAG, Voice, Vision, Autonomous Coding).
   - $L_{\text{latency}} \in [0, 1]$ represents SLA compliance (real-time voice streaming requires $L_{\text{latency}} \ge 0.85$).
   - $M_{\text{modal}} \in [0, 1]$ represents multimodal tool requirement matching.
   - Weights: $w_d = 0.45, w_l = 0.35, w_m = 0.20$ ($\sum w_i = 1.0$).

2. **Architectural Safety Index ($I_{\text{safe}}$)**:
   $$I_{\text{safe}} = \frac{1}{3} \left( G_{\text{guardrail}} + S_{\text{sandbox}} + T_{\text{turn\_limit}} \right)$$
   Recommended templates must attain $I_{\text{safe}} \ge 0.90$ with zero known unhandled vulnerabilities before recommendation.

### 3. Thresholding & Refusal Decision Criteria

Awesome LLM Apps Catalog Agent enforces strict operational safety and integrity boundaries:
- **Refusal to Recommend Deprecated or Insecure Templates**: Reference implementations lacking input sanitization or using deprecated unmaintained SDKs are deterministically rejected with code `ERR_INSECURE_TEMPLATE_BLOCKED`.
- **Refusal of Hardcoded Secrets**: Scaffolding templates containing hardcoded API keys or environment secrets trigger refusal (`ERR_HARDCODED_SECRETS_PROHIBITED`).
- **Turn Ceiling Enforcement**: Advisory sessions are bounded by `max_turns: 25` to eliminate circular planning dialogues (`WARN_TURN_BUDGET_EXCEEDED`).
- **Local Directory Boundary Enforcement**: Scaffolding outputs write strictly to the local workspace; directory traversal attempts are blocked (`ERR_OUT_OF_BOUNDS_WRITE`).

### 4. Fallback Decision Mechanism

Continuous advisory support is maintained through multi-tier fault recovery:
- **Model Cascade Failover**: When the primary foundation model experiences latency spikes or HTTP 429 rate limits, the orchestrator cascades automatically between `claude-3-5-sonnet`, `gpt-4o`, and `gemini-2.0-flash`.
- **Deterministic Static Catalog Fallback**: If LLM synthesis encounters service outages, the system serves pre-indexed static Markdown template blueprints directly from the local repository.
- **Graceful Topology Simplification**: When complex multi-agent graphs exceed execution parameters, the agent simplifies topologies to linear sequential chains.

### 5. Human-in-the-Loop Governance

Human engineers retain complete architectural direction and sign-off authority:
- **Mandatory Operator Review Gates**: Git commits, file creations, and library installations require explicit confirmation from the human developer.
- **Immediate Execution Cancellation**: Operators can halt scaffolding sessions at any point using `Ctrl+C` interrupt signals.
- **Editable Source Code**: All generated application scaffolds, tool scripts, and Docker manifests are saved as clean, readable code requiring human review before deployment.

---

## The Data It Uses

Awesome LLM Apps Catalog Agent operates under strict privacy, data minimization, and local workspace isolation standards.

### 1. Ingested Input Data

The agent processes only operational assets necessary to fulfill architectural consulting:
- **Developer Requirements**: Queries describing use-case goals, latency targets, and target tech stacks.
- **Catalog Metadata Index**: Descriptions, dependency manifests, and directory trees of 100+ open-source application templates.
- **Workspace Source Files**: User configuration manifests, environment files, and local code snippets scoped to the project.

### 2. Configuration & Reference Data

- **Application Catalog Taxonomy**: Categorization matrices spanning RAG pipelines, multimodal vision, real-time voice, and multi-agent coordination.
- **Model Provider Benchmark Data**: Latency, context window, and pricing benchmarks across frontier providers.
- **Security Checklists**: OWASP Top 10 for LLM Applications and MITRE ATLAS security patterns.

### 3. Base Model & Inference Lineage

- **Deterministic Algorithmic Engines**: Catalog search indexing, taxonomy matching, and file templating executed natively in Python (100% deterministic with zero LLM variance).
- **Foundation LLMs**: High-capability frontier models (`claude-3-5-sonnet`, `gpt-4o`, `gemini-2.0-flash`) utilized for complex architectural analysis, trade-off comparisons, and code authoring.
- **Zero Training on Developer Blueprints**: Proprietary project briefs, system architectures, and company requirements are never stored on external servers or used for model training.

### 4. Data Privacy, Storage, and Retention

- **OWASP LLM & MITRE ATLAS Hardened**: Defended against prompt injection, context leakage, and excessive tool privileges.
- **Local-Only Blueprint Storage**: All generated projects, documentation, and configuration templates remain exclusively on the user's filesystem.
- **Credential Scrubbing**: Environment variables, authentication tokens, and user paths are scrubbed from generation logs.
- **Zero Commercial Monetization**: Developer specifications, scaffolded codebases, and architectural inquiries are never monetized, aggregated, or shared with third parties.

---

## Limitations

Understanding the operational boundaries and technical constraints of Awesome LLM Apps Catalog Agent is essential for system engineering.

### 1. Rapid Upstream Model API Deprecations
- **Limitation**: Third-party model providers frequently deprecate endpoint parameters, which can affect older catalog templates.
- **Mitigation**: Scaffolds pin explicit SDK versions and implement dynamic configuration layers that adapt to upstream API shifts.

### 2. Multi-Modal Audio Hardware Latency Bottlenecks
- **Limitation**: Real-time voice templates depend heavily on local sound driver performance and network jitter outside agent control.
- **Mitigation**: The advisor incorporates client-side audio jitter buffers and WebRTC optimization guidelines in voice application blueprints.

### 3. Vector Database Index Tuning at Extreme Scale
- **Limitation**: While catalog RAG templates include standard vector store configurations (Qdrant, Chroma, PGVector), billion-scale vector indexes require custom cluster sharding.
- **Mitigation**: Scaffolds isolate vector store logic behind standard retriever interfaces to allow transparent swapping to cloud-managed vector backends.

### 4. Non-Deterministic Multi-Agent Swarm Convergence
- **Limitation**: Open-ended peer-to-peer agent handoffs can result in unpredictable conversational loops without strict convergence criteria.
- **Mitigation**: Templates automatically inject hard turn ceilings, timeout handlers, and supervisor arbitration checks into generated agent loops.

### 5. Subjective Architectural Trade-Off Preferences
- **Limitation**: Optimal architectural choices depend heavily on team familiarity and existing organizational infrastructure.
- **Mitigation**: The advisor outputs comparative trade-off tables comparing alternative frameworks to empower informed human team decisions.

---

## Summary & Compliance Checklist

| Checkpoint 2 Requirement | Corresponding Section | Status |
| :--- | :--- | :---: |
| **How the agent decides** | [How the Agent Decides](#how-the-agent-decides) | **Covered** |
| - Decision architecture & 5-stage pipeline | Section 1 | Verified |
| - Decision logic & recommendation formulations | Section 2 | Verified |
| - Thresholding & refusal decision criteria | Section 3 | Verified |
| - Fallback decision mechanism | Section 4 | Verified |
| - Human-in-the-loop governance & oversight | Section 5 | Verified |
| **The data it uses** | [The Data It Uses](#the-data-it-uses) | **Covered** |
| - Ingested developer requirements, catalog metadata & files | Section 1 | Verified |
| - Configuration, catalog taxonomy & benchmark data | Section 2 | Verified |
| - Base model lineage & deterministic engines | Section 3 | Verified |
| - Data privacy, retention lifecycle & MITRE/OWASP | Section 4 | Verified |
| **Its limitations** | [Limitations](#limitations) | **Covered** |
| - Rapid upstream model API deprecations | Section 1 | Verified |
| - Multi-modal audio hardware latency bottlenecks | Section 2 | Verified |
| - Vector database index tuning at extreme scale | Section 3 | Verified |
| - Non-deterministic multi-agent swarm convergence | Section 4 | Verified |
| - Subjective architectural trade-off preferences | Section 5 | Verified |
