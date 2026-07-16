# Handover: Mace Digital AI Service — Shared Agent Tooling

**Audience:** Claude Code, working across GitHub repos
**Owner:** Stephen Cummins, Global Lead for AI Applications, Mace Consult
**Milestone:** September 2026 service readiness

---

## 1. Mission

Convert Stephen's existing per-project AI assets into a **shared, reusable capability layer** consumable by any Mace project. The service model:

```
Copilot Studio agents (per project, thin, conversational)
        │  A2A / MCP
        ▼
Shared MAF agents + MCP servers (owned by Digital AI service)  ◄── THIS REPO(S)
        │
        ▼
Work IQ (governed M365 data layer) + Azure services
```

Projects consume; the service builds and governs. New project onboarding should be **configuration, not development**.

## 2. Constraints & platform facts (verified July 2026)

- **A2A is GA in Copilot Studio (May 2026).** MAF-built agents are wire-compatible with Copilot Studio A2A — no custom adapters. Agents built before May 2026 use the old message format and need an A2A compatibility audit.
- **Microsoft Agent Framework (MAF) 1.0 GA April 2026** (Python + .NET). AutoGen and Semantic Kernel are maintenance-only — do not build on them.
- **Work IQ APIs GA June 16, 2026:** A2A, remote MCP server, REST. Entra ID **delegated auth only** (OBO supported, application-only NOT supported). Usage-based Copilot Credits billing — every server we build needs per-invocation cost telemetry.
- **Work IQ MCP design pattern to copy:** small set of generic verb tools (fetch/create/update) against resource paths, not hundreds of bespoke operations.
- **Agent 365** is the governance control plane: admin allow/block of MCP servers, scoped permissions, tool-call tracing via Defender Advanced Hunting. Every server we ship must be registrable/governable there.
- Existing Mace estate: M365 macegroup tenant (maceglobal migration pending — avoid hardcoding tenant IDs), Azure Functions, Power Platform, SharePoint.

## 3. Asset conversion catalogue (priority order)

### Phase 1 — MaceStyle → `mace-mcp-style` (cleanest conversion, do first)
- **Current state:** Azure Function validating documents against 199 style rules; rules in a SharePoint list ("Style Rules"); invoked via Power Automate from Control Centre.
- **Target:** MCP server (TypeScript or Python, official MCP SDK, streamable HTTP transport) wrapping the existing Function.
- **Tools to expose:**
  - `validate_document(file_ref | text, ruleset?) → findings[]`
  - `list_rules(category?) → rules[]`
  - `explain_finding(finding_id) → guidance`
- **Notes:** Keep the Function as-is initially; MCP server is a façade. Rules stay in SharePoint (read via Graph, delegated). Add structured JSON findings output if current output is report-oriented.

### Phase 2 — PDMS site creation → `mace-mcp-pdms` (the reference template)
- **Current state:** Site-creation tooling for project delivery sites.
- **Target:** MCP server exposing `provision_project_site(project_meta) → site_urls`, `get_site_status(project_id)`, plus a **project onboarding recipe** that also registers a pre-wired Copilot Studio agent config consuming the shared tool catalogue.
- **This is the flagship:** "new project = one provisioning call" is the service's pitch.

### Phase 3 — Document QA / search: DO NOT BUILD
- Work IQ MCP (Mail, Calendar, Teams, Copilot search servers) covers cross-M365 retrieval with permission trimming. Consume it; don't replicate Graph plumbing. Only build custom retrieval where Work IQ can't reach (external/non-M365 sources).

### Phase 4 — MaceyBot / ZoeBot refactor (Copilot Studio side, not code-first)
- Stay in Copilot Studio as front doors. Audit for pre-May-2026 A2A message format. Re-point their heavy logic to the Phase 1/2 MCP servers via MCP tool registration (or A2A for task delegation). Track Dev→UAT→Prod pipeline as today.

### Phase 5 (stretch) — Orchestration agents in MAF
- Where a workflow needs >3 conditional branches, checkpointing, code execution, or multi-agent coordination: build as MAF agent (Python), hosted in Foundry Agent Service, invoked via A2A. First candidate: multi-document compliance sweep (batch MaceStyle across a project library with summary report).

## 4. Repo & engineering standards

- **Org structure:** one repo per MCP server (`mace-mcp-style`, `mace-mcp-pdms`) + one `mace-ai-platform` repo for shared libs (auth, telemetry, MCP scaffolding) and docs. Monorepo acceptable if preferred — decide in first session.
- **Language:** TypeScript preferred for MCP servers (SDK maturity); Python for MAF agents.
- **Hosting:** Azure Functions (existing pattern) or Container Apps; streamable HTTP MCP transport.
- **Auth:** Entra ID app registrations, delegated flows; secrets in Key Vault; never in repo.
- **Every server must include:** OpenTelemetry tracing, per-invocation cost/usage logging, health endpoint, a `TOOLS.md` documenting each tool's schema, and a `GOVERNANCE.md` (Agent 365 registration steps, permission scopes requested, data touched).
- **CI:** GitHub Actions — lint, test, deploy-to-dev on merge; manual gate to UAT/Prod (mirrors existing Dev→UAT→Prod discipline).
- **Testing:** contract tests per tool (schema in/out), plus at least one end-to-end test invoking via a real MCP client.

## 5. Suggested first Claude Code session

1. Scaffold `mace-mcp-style`: MCP SDK project, one working tool (`list_rules` stubbed against fixture data), CI pipeline, TOOLS.md, GOVERNANCE.md templates.
2. Wire `validate_document` to the existing Azure Function endpoint (config-driven URL).
3. Add telemetry + cost logging middleware as a shared package.
4. Produce an architecture README with the three-layer diagram for the September deck.

## 6. Definition of done (per server)

- [ ] Deployed to dev, callable from an MCP client (Claude Desktop or Copilot Studio preview)
- [ ] Registered/registrable in Agent 365 with documented scopes
- [ ] Telemetry visible; cost-per-invocation estimable
- [ ] TOOLS.md + GOVERNANCE.md complete
- [ ] Consumed successfully by at least one Copilot Studio agent in dev

## 7. Out of scope

- NHP project work (Stephen no longer involved; NHP timesheets moved to a 3rd-party system).
- Rebuilding M365 retrieval that Work IQ provides.
- Any application-only auth flows against Work IQ (unsupported).
