# Literature Review (EU PPP)

Agent skill for rigorous, defensible literature reviews in EU plant protection product (PPP) regulatory work.

## Install

**Cursor** — clone into your skills directory, or symlink this folder:

```text
.cursor/skills/ppp-literature-review/
```

**Claude Code** — clone into your Claude skills path and ensure `SKILL.md` is discoverable by the agent.

The skill entry point is [`SKILL.md`](SKILL.md).

## Contents

| Path | Purpose |
|------|---------|
| `SKILL.md` | Workflow, phases, chemwise integration, writing rules |
| `lit-rev-models.txt` | Full / Condensed / Adapted review depth matrix |
| `references/` | Source hierarchy, citations, quality appraisal, EU framework |
| `assets/` | PRISMA/scope templates, EU regulation index, OECD TG index |

## Triggers

Examples: `lit review`, `PPP review`, `evidence synthesis`, `data gap analysis`, `WoE for`, `/lit-review`, `/ppp-review`.

## Requirements

- **chemwise** MCP for regulatory anchor (substance status, EFSA conclusions, MRLs, etc.)
- Optional: `anthropic-skills:docx` for Word output

## Author

Dylan Grimes Larkin — Regulatory Scientist @ Life Scientific

## License

All rights reserved unless otherwise stated by the repository owner.
