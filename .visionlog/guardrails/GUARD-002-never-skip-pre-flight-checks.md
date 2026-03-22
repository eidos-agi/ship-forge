---
id: "GUARD-002"
type: "guardrail"
title: "Never skip pre-flight checks"
status: "active"
date: "2026-03-22"
---

## Rule
ship-forge skills must never offer a "skip checks" or "force" option. If a pre-flight check fails, the release is blocked until it's fixed.

## Why
Every shortcut taken during shipping becomes technical debt. "Just this once" is how broken packages reach PyPI.

## Violation Examples
- Adding a --force flag to /ship-check
- Allowing release from a dirty tree with a warning instead of a block
- Skipping CI verification before publish
