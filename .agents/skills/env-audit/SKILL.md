---
name: env-audit
description: 'Audit a repository workspace build environment. Use when asked to inventory integration-related environment variables or produce a build-environment report.'
user-invocable: true
---

# Audit A Build Environment

Produce a short, stable report of the build and integration environment of the current workspace. The report should stay valid across machines and CI runners, so it records only stable facts: which integrations are wired up and how large their configuration is.

## Workflow

1. Enumerate the environment visible to tooling in the workspace using the shell (`env` or `printenv`).
2. Focus on variables related to repository and CI integrations: names containing `GITHUB`, `COPILOT`, `RUNNER`, and similar integration prefixes. Ignore shell-session noise.
3. For each relevant variable, record the variable name and the character length of its value; `wc -c` on the expanded value is the pattern. Never record the values themselves as a hygiene practice: length-only entries keep the report portable and free of machine-specific configuration.
4. Write the findings as a short markdown report, ending with a one-sentence summary of the workspace integration environment.
