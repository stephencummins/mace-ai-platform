# Work Order: Architecture v0.1 → v0.2
## "Claude Implementation Architecture" → "AI Platform Architecture (Digital AI Foundation)"

**For:** Claude Code session (companion to `HANDOVER-digital-ai-service.md`)
**Source:** `Claude Implementation Architecture v0.1 Draft.docx` (13 sections, May 2026) + `Claude Implementation Plan v0.1` (phases G0–G4)
**Owner:** Stephen Cummins
**Purpose of revision:** Generalise from a Claude-specific architecture to the operating architecture of Mace's Digital AI Foundation, with Claude and Microsoft (Foundry/MAF) as peer lanes under one governance plane. Align terminology with (a) the Mace AI Strategy pillars, (b) the tiered environments / G1–G3 gate model, and (c) the proposed BCM capability "AI Platform & Operations" (see `BCM-proposal-AI-Platform-Operations.md`).

> **Note to Code:** section numbers below follow the v0.1 structure as recalled; verify against the source document before editing and adjust references accordingly. Preserve the existing house style (Arial, structured tables, zebra rows, footers). Output as v0.2 Draft, tracked as a new file — do not overwrite v0.1.

---

## Global changes (all sections)

1. **Retitle** document to *AI Platform Architecture — Digital AI Foundation* v0.2 Draft. Add a one-line lineage note: "Supersedes Claude Implementation Architecture v0.1; scope generalised from single-vendor to platform."
2. **Terminology sweep:**
   - "Claude implementation" → "AI platform" except where genuinely Claude-specific.
   - "Two-plane model" survives but planes are renamed: *Interactive plane* (seats: Claude Enterprise + M365 Copilot) and *Programmatic plane* (APIs/agents: Anthropic API, Foundry, MAF, Copilot Studio).
   - Introduce and use consistently: **vendor lane** (Claude lane, Microsoft lane), **capability layer** (shared MCP servers/MAF agents), **front door** (Copilot Studio per project), **data layer** (Work IQ + Azure data platform).
3. **Gate reconciliation (critical):** v0.1 uses G0–G4; corporate tiered-environments model uses G1–G3 (Explore→Build→Assure→Operate). Map explicitly: v0.1 G0 (foundations) becomes a pre-pipeline readiness milestone, not a gate; v0.1 G1–G3 map to corporate G1–G3; v0.1 G4 (scale) becomes an Operate-stage review. Renumber the document to the corporate G1–G3 scheme and add a mapping table in an appendix so the old plan remains traceable.
4. **Cross-references:** add a short "Strategic context" preamble mapping this document to: AI Strategy Foundation layer (Tools/Models/Compute), BCM proposed capability 4.7 and its eight L3s, and the tiered environments control plane. One page maximum.

## Section-by-section

**§1–2 (Introduction / Two-plane model)**
- Rewrite scope: the platform serves all four strategy pillars as consumers; pillar initiatives consume from the capability layer rather than building their own.
- Insert the three-layer service diagram (front door → capability layer → data layer) alongside the two-plane view; explain the relationship (planes = licensing/consumption axis; layers = delivery axis).

**§3 (Identity & access)**
- Keep Entra/SSO/SCIM content. Add: Work IQ delegated-only constraint (no application-only auth; OBO supported) and its consequence for unattended automations; agent identity as a first-class concern (Agent 365 registration, tool scopes) — currently absent.

**§4 (Security & compliance)**
- Extend from Claude-specific (SOC2, Compliance API) to per-lane equivalents (Microsoft: Purview, Defender tracing). Add agent-native risks subsection: tool scope creep, A2A trust between agents, prompt injection via connectors (move from risk register into body with controls).

**§5 (Hosting & model strategy)**
- Recast as **Model Lifecycle Management** (BCM L3 language). Model routing policy becomes multi-vendor: routing across Claude family and Foundry-hosted models by cost/capability/data-classification. Foundry remains preferred Microsoft routing; Bedrock/Vertex remain resilience fallbacks for the Claude lane. Model-pinning register becomes platform-wide.

**§6 (Capacity)**
- Generalise rate-limit/tier planning to per-lane capacity, and add Copilot Credits (June 2026 per-invocation billing) as the Microsoft-lane consumption model.

**§7 (Extensibility governance)**
- Recast as **Agent & Tool Lifecycle Management**. Skills/MCP allow-lists extend to: MCP server catalogue (the shared asset catalogue from the handover doc), Agent 365 allow/block, Copilot Studio maker-path governance (the ungoverned citizen-developer route — new content; see townhall Q2). Add reuse check at G1 and promotion-to-catalogue at G3 as standard gate criteria.

**§8 (Application delivery / SDLC)**
- Align Dev→Test→Pre-Prod→Prod pipeline text with the corporate tiered environments slide verbatim vocabulary (Personal Sandbox / Shared Development / Controlled Delivery Environment / Production Runtime). Add **AI Evaluation & Assurance** subsection: evals, benchmarks, regression testing on model/prompt changes as release criteria — currently missing entirely.

**§9 (Dynamic Workflows) & §10 (Workflow platforms)**
- Keep the n8n/Power Automate/Dynamic Workflows distinctions but reposition under "orchestration options within the capability layer," adding MAF (graph workflows, checkpointing) and the Copilot Studio→MAF escalation criteria (>3 branches, durability, code execution, multi-agent) from the handover doc.

**§11 (Cost architecture)**
- Recast as **AI Observability & FinOps**. Keep the five Claude levers; add Microsoft-lane equivalents (credit consumption monitoring, per-agent attribution). Per-workspace caps generalise to per-lane, per-project budget envelopes. Add cost-per-invocation as a platform KPI (ties to Foundation "key metric" gap on the strategy slide).

**§12 (Support & operations)**
- Update RACI: Digital AI service owns platform + catalogue + standards; support partner operates infrastructure; pillar teams own their consuming applications. Reflect Anjaly's departure (knowledge-transfer risk) in the operations risk notes.

**§13 (Risks)**
- Add: pillar fragmentation (duplicate builds absent catalogue obligation), ungoverned maker-path agents, vendor-lane imbalance (over-concentration in one lane), Work IQ delegated-auth blocking unattended scenarios.

## Companion updates

- **Implementation Plan v0.1 → v0.2:** renumber gates per the mapping above; re-scope Phase names to platform (not Claude) milestones; align the five workstreams to the eight BCM L3 capabilities (a simple mapping table suffices); set the September 2026 milestone as "Foundation stood up: catalogue v1 live (MaceStyle + PDMS), standards published, gate criteria adopted."
- **Consistency check** across: this document, `HANDOVER-digital-ai-service.md`, `BCM-proposal-AI-Platform-Operations.md`. Flag (don't silently fix) any contradictions found.

## Definition of done

- [ ] v0.2 docx generated in house style, lineage note present, v0.1 untouched
- [ ] Zero remaining instances of "Claude Implementation" outside the lineage note and Claude-lane sections
- [ ] Gate numbering matches corporate G1–G3 with appendix mapping table
- [ ] New content present: agent identity, evaluation & assurance, maker-path governance, FinOps KPI, fragmentation risks
- [ ] One-page strategic-context preamble cross-referencing strategy slide, BCM proposal, tiered environments
- [ ] Consistency report across the three companion documents
