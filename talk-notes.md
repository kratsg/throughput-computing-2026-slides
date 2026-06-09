# LLM Assisted Analysis at the UC AF — front-loaded session notes

Draft entries for the agenda's per-talk template. Paste/adapt into the meeting minutes;
the **Decisions** are what the talk asks the room to settle (record outcomes live).

## Decisions?
Surfaced for the room to settle (the talk's discussion seeds):
- **MCP granularity & identity:** per-service MCPs vs a single facility gateway with delegated
  identity? (FastMCP allows one auth provider/server; PandaMCP delegates auth to PanDA.)
- **Knowledge locus:** does facility-specific knowledge live in the shared USATLAS marketplace
  or ship with the facility (Puppet)? It is in *both* today — pick a primary to stop duplication.
- **Agent authority:** adopt "read-only by default; writes/submits/emails require human approval"
  as a cross-AF norm?
- **Sandboxing baseline:** k8s pod isolation where available; bubblewrap (or equiv) where not?
- **A shared commons:** appetite for one USATLAS marketplace + playbook set across all AFs — and
  who curates/maintains it?

## Milestones?
Delivered at the UChicago AF:
- Managed Claude settings (HEP allow-list + ATLAS env) shipped via Puppet to login01–04 (2026‑05‑19)
- USATLAS marketplace published — `analysis-facilities`, `atlas`, `hep-python-tools`
- `rucio-mcp` + `ami-mcp` (local x509) and **hosted multi-site** `rucio-mcp.af.uchicago.edu`
  (atlas / cms / dune / escape) with an OAuth/OIDC bridge
- Jupyter MCP working on the AF JupyterHub (drive a notebook from any agent, incl. phone)
- OpenWebUI AF assistant live at `af.uchicago.edu/chat`
- HTCondor daily-report agent + human-gated held-job emails

Upcoming:
- `panda-mcp` at the AF (workflow execution) — coordinate with Bockelman
- OIDC across remaining experiments/RSEs (FTS token support)
- Keycloak reverse-proxy for single-token Jupyter routing
- Formalize reasoning-engine / playbook split; the end-to-end "Elwood" loop

## Action Items:
- [ ] (AF) Resolve marketplace-vs-facility knowledge duplication; choose a primary location
- [ ] (AF) Enable OIDC on remaining RSEs; confirm FTS token support
- [ ] (community) Decide MCP granularity + identity model across AFs
- [ ] (community) Agree an agent write-action policy + sandboxing baseline
- [ ] (AF / Bockelman) Stand up HTCondor REST + `panda-mcp` at the AF
- [ ] (community) Scope a shared marketplace/playbook commons + name a curation owner

## Notes:
- **Thesis:** a generic LLM is not enough; value = facility context + ATLAS tools behind agentic
  interfaces. The facility `CLAUDE.md` / managed config is the hero exhibit.
- **Cautionary (real):** cluster agents recommended Lustre/MDS tuning on a **Ceph** filesystem
  with no Ceph context → rule: "no grounded context, stay quiet." Context is what makes agents
  *trustworthy*, not just useful.
- **Architecture:** high-level intent tools (data / transform / batch / inference) over swappable
  backends; reasoning engine (shared) + playbook (per-facility); per-tool skills are
  facility-independent for reuse.
- **Portability proven today:** one `rucio-mcp` serves ATLAS *and* ESCAPE (path-routed).
- **Links:** `github.com/usatlas/marketplace` · `usatlas.github.io/af-docs/ai` · `af.uchicago.edu/chat`
