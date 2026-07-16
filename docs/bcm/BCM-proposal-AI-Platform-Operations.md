# Proposed addition to the Mace Business Capability Model
## 4.7 AI Platform & Operations

**Draft for discussion — Stephen Cummins, July 2026**
**Responding to:** Business Capability Map (Draft, Jun 2026, Suketu Mehta) — "are there some capabilities that are missing?"

---

### The gap

The current model treats technology as applications we deploy and secure (4.4) and AI as something we pilot (4.5 "Emerging Tech & AI Strategy"). AI-era capabilities are different in kind: they are **services we operate continuously** — with lifecycles, evaluation loops, per-invocation economics, and software that acts rather than software that runs. The AI Strategy names this layer (the "Digital AI Foundation" — Tools / Models / Compute) but the capability map has no home for it. Two of the four strategy pillars (Commercial AI, Spatial AI) similarly map to no capability. Without a named capability there is no investment line, no owner, and no way to align the strategy and technology views the model exists to connect.

### Proposed L2 capability

| Capability Name | Business Definition |
|---|---|
| **AI Platform & Operations** | Building, cataloguing, governing and operating reusable AI tools, agents, models and standards consumed across client programmes and internal functions. |

### Proposed L3 capabilities

| Capability Name | Business Definition |
|---|---|
| Model Lifecycle Management | Selecting, routing, versioning and retiring AI models against approved use cases, cost and capability profiles. |
| Agent Lifecycle Management | Governing agents as managed actors — identity, permissions, tool scopes, ownership, monitoring and retirement. |
| Shared AI Asset Catalogue | Cataloguing reusable tools, agents and templates; enforcing reuse checks at intake and promotion of project assets into shared stock. |
| AI Evaluation & Assurance | Testing non-deterministic systems through evaluations, benchmarks and regression checks across model and prompt changes. |
| AI Observability & FinOps | Tracing agent activity, detecting drift, and managing per-invocation cost and consumption across projects and functions. |
| Prompt & Context Asset Management | Versioning and governing prompts, skills and grounding content as firm IP (links to 4.6 Knowledge & Knowhow). |
| AI Risk, Safety & Responsible AI | Managing hallucination risk, human-in-the-loop design, red-teaming, client disclosure and regulatory classification (e.g. EU AI Act). |
| Data Readiness for AI | Curating retrieval, grounding and knowledge-base infrastructure so agents act on governed, permission-trimmed data. |

### How it fits

- **Strategy alignment:** this L2 *is* the Digital AI Foundation from the AI Strategy, expressed in capability language. Pillar initiatives (AI for Colleagues, Commercial AI, Spatial AI) become consumers of it.
- **Governance alignment:** the tiered environment model (Explore→Build→Assure→Operate) is the delivery pipeline; this capability owns the standards applied at its gates (reuse check at G1, promotion to catalogue at G3, agent-specific controls at G2).
- **Boundary with 4.4/4.5:** 4.4 keeps enterprise platforms and infrastructure; 4.5 keeps data governance, BI and early-stage innovation scanning. Productised AI assets graduate from 4.5 incubation into 4.7 operation.
- **Existing proof points:** MaceStyle (production), PDMS template (flagship reusable deployment), MaceyBot/ZoeBot (UAT), AI Model Routing Policy and model exposure matrix — the capability already exists in embryo; the model should name it.

### Secondary feedback (offered separately)

Minor errata in the June draft: 3.4's definition table duplicates 3.2's content; repeated rows in 3.3/3.5/3.6; naming drift between map and definition pages (Design vs Digital Engineering; Data, Analytics and AI vs & Innovation; Knowledge & Knowhow vs & Intellectual Capital).
