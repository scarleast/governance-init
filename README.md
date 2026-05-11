# Governance Init

Bootstrap skill and templates for installing a skills-style engineering governance model into new or existing repositories.

The repository is intentionally split into four parts:

- `skills/project-governance-init/`: the bootstrap skill used by an agent to analyze, recommend, and apply governance.
- `templates/`: reusable governance contracts, work item templates, governance skills, and runtime entrypoint templates.
- `scripts/audit_project.py`: read-only project structure audit.
- `scripts/init_governance.py`: deterministic scaffold helper for confirmed plans.
- `scripts/check_sync.py`: runtime/canonical skill consistency checker.

## Quick Start With Codex

Copy the bootstrap skill into a target project runtime directory:

```bash
mkdir -p .codex/skills
cp -R skills/project-governance-init .codex/skills/
```

Then ask Codex:

```text
Use project-governance-init. This is an existing project. First run discover and recommend only; do not change files until I confirm.
```

For a new project:

```text
Use project-governance-init. Initialize strict governance for a new Python + uv project with Codex and Claude runtime entrypoints.
```

## Existing Project Safety

Existing projects should follow:

```text
/discover -> /recommend -> /confirm -> /apply -> /verify
```

Do not overwrite existing `AGENTS.md`, `CLAUDE.md`, ADRs, CI, or task records without explicit user confirmation.

## Template Model

Initialized target projects should maintain project-local facts under a governance directory such as:

```text
project/governance/contracts/
project/governance/templates/
project/governance/skills/
project/work/
```

Runtime entrypoints such as `.codex/skills/**` and `.claude/commands/**` should point back to the project-local canonical governance files.

## Scripts

Read-only audit:

```bash
python3 scripts/audit_project.py /path/to/project
```

Scaffold from a manifest:

```bash
python3 scripts/init_governance.py /path/to/project --mode standard --runtime codex --runtime claude
```

Check canonical/runtime skill sync:

```bash
python3 scripts/check_sync.py /path/to/project
```
