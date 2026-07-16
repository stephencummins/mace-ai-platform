# mace-ai-platform

Umbrella repo for the **Mace AI Service** — the shared platform layer that turns
per-project AI assets (MaceStyle, PDMS, brand generator, etc.) into shared MCP
servers + MAF agents behind thin Copilot Studio agents (A2A/MCP), on Work IQ +
Azure. This repo holds **architecture, policy, governance, and work orders** —
not the runtime code, which lives in the per-service repos (`mace-mcp-style`,
`mace-mcp-pdms`, …).

## Start here

- `HANDOVER-digital-ai-service.md` (repo root) — mission, platform facts, asset
  conversion catalogue, engineering standards. Read this first.
- `docs/bcm/BCM-proposal-AI-Platform-Operations.md` — the proposed BCM capability
  "4.7 AI Platform & Operations" and its eight L3 capabilities.
- `workorders/WORKORDER-architecture-v0.2.md` — instructions to produce the
  Architecture v0.2 doc from the v0.1 baseline.

## Layout

```
docs/
  architecture/   System architecture. v0.1 is read-only (baseline); v0.2 is the
                  working output. Do not edit v0.1 — supersede it in a new file.
  policy/         Routing policy. v1 → v2 progression; keep versions side by side.
  bcm/            Business Continuity Management proposal.
  governance/     Exposure matrix + gate criteria (what ships, what's blocked).
workorders/       Scoped units of work, one file each.
packages/         Shared libs (auth, telemetry) — populated later, not yet.
```

## Conventions

- **Versioned docs are append-only.** A `v0.1` marked read-only stays byte-for-byte
  intact; produce `v0.2` alongside it rather than editing in place. Same for policy
  `v1 → v2`.
- **Governance is the gate.** The exposure matrix and gate criteria in
  `docs/governance/` decide what a service is allowed to expose and when it can
  ship. Architecture and policy changes should trace back to a governance entry.
- **Work orders are the unit of delivery.** New work starts as a file in
  `workorders/`, references the relevant docs, and closes when merged.

## Platform standards (inherited from Mace AI Service)

- **MAF only** for new agents (AutoGen/SK are maintenance-only).
- **Work IQ = delegated auth only.**
- **No hardcoded tenant IDs** — configuration via env/secrets.

## Related

- `mace-mcp-style` — Phase 1, MCP façade over the MaceStyle Function.
- `mace-mcp-pdms` — Phase 2, MCP façade over MaceyBot's SharePoint Site Creation.
