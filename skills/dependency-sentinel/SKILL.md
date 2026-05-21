---
name: dependency-sentinel
description: >
  Safely audit and remediate dependency vulnerabilities (npm/pip). 
  Performs state-check before updates, parses JSON-only reports, 
  and ensures zero-breaking changes by validating SemVer and running tests.
  Use when the user wants to "fix security issues" or "update packages safely".
compatibility: Requires npm CLI or pip-audit CLI.
metadata:
  version: "1.1.0"
  author: "Agent Architect"
  generatedBy: "agent-architect-v1"
---

# Dependency Sentinel

Active protection and automated remediation of project vulnerabilities with state-machine verification.

## Input Handling & Resolution
1. **Contextual Detection:** Check for `package-lock.json` (Node.js) or `requirements.txt`/`pyproject.toml` (Python).
2. **Preference Order:**
   - Use user-specified package if provided.
   - If ambiguous (multiple environments), call `AskUserQuestion` to define the target ecosystem.
3. **Hierarchy:** Explicit arguments > Manifest detection > User prompt.

## Steps

### Phase 1: Discovery & State Verification (Silent)
1.  **Integrity Check:** Ensure the environment is "clean" (e.g., `git status` check to avoid working on dirty trees).
2.  **Telemetry Gathering:**
    - **NPM:** `npm audit --json`
    - **Python:** `pip-audit --format json`
3.  **State Mapping:** Parse JSON to create a "Risk Map" separating:
    - **Safe-Path:** Patch/Minor updates.
    - **Risk-Path:** Major updates or those without direct fixes.

### Phase 2: Strategic Proposal (Verbose)
1.  **Visual Audit:** Display a formatted table of vulnerabilities categorized by severity.
2.  **Ambiguity Handling:**
    - If multiple resolution paths exist, call `AskUserQuestion`.
    - **Question:** "Multiple upgrade paths found. How should Sentinel proceed?"
    - **Options:** `[Apply Patch/Minor Fixes Only (Safe)]`, `[Full Audit Fix (Potential Breaking)]`, `[Selective Package Update]`.

### Phase 3: Controlled Execution
1.  **Pre-flight:** IF a test script exists, run it *before* making changes to establish a baseline.
2.  **Execution:** Apply the selected fixes using precise version flags (e.g., `npm install <pkg>@<version>`).
3.  **Post-flight & SMAG Validation:**
    - Run `npm test` or `pytest`.
    - **Logic:** - IF exit code != 0: Trigger **Rollback** (e.g., `git checkout .`) and report the failure.
      - IF exit code == 0: Confirm success.

## Output Formatting
- **Executive Summary:**
| Component | Risk Level | Status | Action Taken |
| :--- | :--- | :--- | :--- |
| `engine-io` | 🔴 Critical | Fixed | Upgraded to v6.5.4 |
- **Verification Checklist:**
  - [x] Environment Baseline established
  - [x] Vulnerability JSON parsed
  - [x] Non-breaking versions identified
  - [x] Post-update regression tests passed ✓

## Guardrails
- **No Force:** Never use `--force` or `--legacy-peer-deps` without explicit user override.
- **Scope Lock:** Do not modify `.env` files or source code logic; only dependency manifests.
- **Transparency:** Every command executed must be logged in the session for auditability.
- **Rollback Guarantee:** Must be able to revert changes instantly if the state machine detects a regression.