# ship-forge

Ship software that stays shipped. CI/CD, QA, and release hygiene for agentic software.

## Why?

We audited 6 Python packages and found every single one had uncommitted changes. .gitignore files didn't cover the stack. Most had no publish workflow. Pre-commit hooks didn't exist. The tools worked — they just weren't shippable.

ship-forge fixes the gap between "code works" and "software is in production and healthy."

## Skills

| Skill | What |
|-------|------|
| `/ship-check` | Pre-ship audit: clean tree, build verification, install-test artifacts, .gitignore |
| `/ship-init` | Scaffold: pre-commit hooks, CI workflows, .gitignore for your stack |
| `/ship-release` | End-to-end release: preflight → build → verify → tag → publish → smoke test |
| `/ship-deploy` | Railway deployment: health checks, graceful shutdown, env vars, rollback plan |
| `/ship-qa` | MCP server QA: schemas, tool descriptions, error quality, behavior testing |

## The Key Insight

**Test what you ship, not what's in your working tree.**

Build the wheel. Install it in a clean venv. Run smoke tests against the installed package. Most teams skip this and discover broken sdists after publishing.

ship-forge's `/ship-check` and `/ship-release` enforce this by running build verification before every release.

## The Dev-to-PyPI Lifecycle

How professional Python developers get from "I'm editing source" to "it's on PyPI and it works":

```
Phase 1: LOCAL          pip install -e .           Edit → test → instant feedback
Phase 2: INTEGRATION    pip install git+branch     Downstream project tests your branch
Phase 3: PRE-RELEASE    pip install --pre          v1.5.0a1 on PyPI, invisible to normal install
Phase 4: RELEASE        pip install package        v1.5.0 — the real deal
```

**Nobody assumes it will work online.** Confidence is earned at each layer.

### Quick Reference

| Situation | Command |
|-----------|---------|
| Developing locally | `pip install -e .` in the package repo |
| Testing in another project | `pip install git+https://github.com/you/pkg.git@branch` |
| Publishing pre-release | Tag `v1.5.0a1`, CI publishes. Users opt in with `--pre` |
| Publishing release | Tag `v1.5.0`, CI publishes. Now it's the default |
| Protecting downstream | Pin `==1.4.0` in apps, `>=1.4,<2` in libraries |

### Version Tags

| Tag | Meaning | Who gets it |
|-----|---------|-------------|
| `1.5.0a1` | Alpha — unstable, APIs may change | Only `--pre` users |
| `1.5.0b1` | Beta — feature-complete, bugs expected | Only `--pre` users |
| `1.5.0rc1` | Release candidate — believed stable | Only `--pre` users |
| `1.5.0` | Release | Everyone |

See `findings/0009-python-package-dev-to-pypi-lifecycle.md` for the full research.

## Templates

| Template | What |
|----------|------|
| `.pre-commit-config.yaml` | ruff + codespell + pre-commit-hooks |
| `ci-full.yml` | Lint, test matrix, build verification with install-test |
| `publish-verified.yml` | PyPI publish with pre-publish artifact verification (trusted publisher) |
| `.gitignore` (Python + ML) | Covers Python artifacts, ML models/data, experiment tracking |

## Usage

```bash
git clone https://github.com/eidos-agi/ship-forge.git ~/repos-eidos-agi/ship-forge
cp ~/repos-eidos-agi/ship-forge/.claude/skills/ship-*.md .claude/skills/
```

## Part of the Forge Ecosystem

- [forge-forge](https://github.com/eidos-agi/forge-forge) — the meta-forge
- [foss-forge](https://github.com/eidos-agi/foss-forge) — FOSS standards and marketing
- [ship-forge](https://github.com/eidos-agi/ship-forge) — this repo
- [security-forge](https://github.com/eidos-agi/security-forge) — security auditing
- [demo-forge](https://github.com/eidos-agi/demo-forge) — AI-generated demos

## License

MIT — [Eidos AGI](https://github.com/eidos-agi)
