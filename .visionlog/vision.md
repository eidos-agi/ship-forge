---
title: "ship-forge — Ship Software That Stays Shipped"
type: "vision"
date: "2026-03-22"
---

## North Star

ship-forge owns the engineering discipline of getting software from "works on my machine" to "published, deployed, and healthy." Not marketing (foss-forge), not testing (test-forge), not security (security-forge) — the plumbing between code and production.

## The Problem

Eidos AGI has 6 packages on or near PyPI. Every single one has uncommitted changes right now. .gitignore files don't cover the stack. Most have no publish workflow. Pre-commit hooks don't exist. There's no standard for what "ready to ship" means from an engineering standpoint.

The forges are clean because they have no code. The software repos are messy because nobody enforces hygiene.

## What ship-forge Covers

### 1. Code Quality Gates (before commit)
- Pre-commit hooks: ruff (lint + format), mypy (types), pytest (smoke)
- .gitignore that actually covers the project's stack (Python artifacts, IDE files, OS files, build dirs, model files, training artifacts)
- No `.pyc`, `.egg-info`, `dist/`, `__pycache__/` ever committed

### 2. CI/CD Standards (before merge)
- Every repo has a CI workflow that runs on push and PR
- Lint + format check + type check + test matrix
- Build verification: `python -m build` succeeds
- No merge without green CI

### 3. Release Hygiene (before publish)
- Clean working tree (no uncommitted changes)
- Version bumped in pyproject.toml
- CHANGELOG updated
- Tag created and pushed
- Publish via trusted publisher (OIDC), never API tokens
- Verify package installs cleanly from PyPI after publish

### 4. Deployment Standards (after publish)
- Railway deployment checklist
- Environment variables documented
- Health check endpoint exists
- Rollback plan documented
- Deployment logs reviewed

### 5. Repo Hygiene (always)
- .gitignore covers the full stack
- No training artifacts, model files, logs committed
- No build artifacts in git
- Dependencies are minimal and intentional
- Lock files exist for reproducibility

## What ship-forge is NOT

- Not about marketing or community health (foss-forge)
- Not about testing strategy (test-forge)
- Not about security scanning (security-forge)
- Not about demos (demo-forge)

## How It Relates to Other Forges

ship-forge is the last gate before software reaches the world:

```
code → test-forge (does it work?)
     → security-forge (is it safe?)
     → ship-forge (is it clean, built, and deployable?) ← HERE
     → foss-forge (is it well-presented?)
     → demo-forge (does it look good?)
```

## Success Metric

Every Eidos AGI software repo has zero uncommitted changes, a green CI badge, a publish workflow, pre-commit hooks, and a .gitignore that covers its stack. No package ships to PyPI from a dirty tree.

