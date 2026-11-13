# Copilot Instructions

This repository contains user-level VS Code agents. When adding, renaming, or
changing an agent, follow the Naming Convention and Agent Checklist in
`README.md`.

## Scope and Safety

- Make requested agent and skill changes only within this repository. Update
  supporting files here when required by the Agent Checklist or validation.
- Never create, edit, delete, or otherwise mutate files in an external
  repository, including one open in the workspace or referenced by the request.
  If a task requires such a change, leave that repository untouched and explain
  the limitation. External repositories may be inspected only when needed for
  context; inspection does not authorize changes there.
- Keep shared agents, skills, scenarios, reports, and documentation generic.
  Do not include personal information, account or organization identities,
  source-project names, repository inventories or URLs, activity or session
  identifiers, private hosts, credentials, or absolute user paths. Use
  synthetic examples and repository-relative paths; acquire task-specific
  context only when needed.
- Do not commit, push, or change unrelated agent permissions without
  authorization.

## Agent Naming and Documentation

- Use PascalCase ASCII names with the owning domain's `Code`, `Infra`, `Gov`,
  or `Business` prefix and a descriptive role suffix. Name the file
  `<Name>.agent.md` and make its frontmatter `name` match exactly. Advisors
  must end in `Advisor`. Do not invent unprefixed names or silently expand
  documented exceptions.
- In the same change, update the README Agent Index, Domain Organization
  diagram, Domain Map, and any affected tool or workflow documentation.
  Document changed behavior, including CLI preferences and fallback paths, not
  just the agent name.
- Keep Orchestrator's agents allowlist, Embedded Routing Index, Embedded
  Ownership, and the owning advisor's selection cues synchronized. Make
  routing self-contained in the agent definition; do not add external runtime
  routing files. Remove obsolete operational references when renaming and
  record the old and new names in Name Migration.
- Preserve role boundaries: only Orchestrator delegates, and advisors remain
  tool-free. For each new worker, add a suitable `tool_profile` in
  `tools/agent-roster-validator.py`.

## Runtime Workflows

- Embed required workflows in their owning agent definitions so they remain
  usable in Remote SSH sessions. Do not require local skills, workflow files,
  personal directory junctions, or client-profile searches at runtime.
- Keep Orchestrator's selection index compact; only the selected worker should
  receive its full procedures.
- Treat missing runtime tools or task evidence as blockers; do not imply a
  workflow succeeded when required capabilities or evidence are unavailable.

## Validation

- After roster changes, run:
  - `python tools/agent-roster-validator.py`
  - `python -m unittest discover -s tests -v`
- Add focused regression coverage for new validation rules. Report existing
  failures separately; do not weaken rules or claim the roster checks passed
  when they fail.
