# CLAUDE.md — ship-forge

> Shipping standards for agentic software — CI/CD, QA, code quality, deployment, and release hygiene.

## What This Is

ship-forge owns the engineering discipline of getting software from "works on my machine" to "published, deployed, and healthy." The last gate before software reaches the world.

```
code → test-forge (does it work?)
     → security-forge (is it safe?)
     → ship-forge (is it clean, built, and deployable?) ← HERE
     → foss-forge (is it well-presented?)
     → demo-forge (does it look good?)
```

## Skills

| Skill | What It Does |
|-------|-------------|
| `/ship-full-audit` | Run ALL forges against a project: foss-check → sec-audit → ship-check → ship-qa → forge-enforce |
| `/ship-detect` | Auto-detect which preflight checks a project needs from config, CI, and history (L0→L1) |
| `/ship-check` | Pre-ship audit: runs `/ship-detect` first, then clean tree, build verification, install-test artifacts |
| `/ship-init` | Scaffold shipping infrastructure: pre-commit hooks, CI workflows, .gitignore |
| `/ship-release` | End-to-end release: preflight → build → verify → tag → publish → smoke test |
| `/ship-deploy` | Railway deployment checklist: health checks, SIGTERM, env vars, rollback plan |
| `/ship-qa` | MCP server QA: schema validation, tool descriptions, error standards, behavior testing |
| `/ship-dev` | Local development workflow: editable installs, branch testing, pre-release lifecycle |

## Templates

| Template | Generates |
|----------|-----------|
| `pre-commit-config.yaml.tmpl` | Pre-commit hooks (ruff, codespell, pre-commit-hooks) |
| `ci-full.yml.tmpl` | CI workflow with lint, test matrix, and build verification |
| `publish-verified.yml.tmpl` | Publish workflow with pre-publish artifact verification |
| `gitignore-python-ml.tmpl` | .gitignore for Python + ML artifacts |

## Guardrails

1. **No software.** Skills and templates only.
2. **Never skip pre-flight checks.** No --force, no shortcuts. If it fails, fix it.

## Related Forges

- **ml-forge** — intelligence patterns: ship-detect uses ml-forge's L0→L1 hybrid pattern
- **foss-forge** — open-source standards and marketing
- **security-forge** — security auditing and agentic threat modeling
- **demo-forge** — AI-generated demo content
- **test-forge** — testing standards and test generation
- **forge-forge** — meta-forge for creating and managing forges
