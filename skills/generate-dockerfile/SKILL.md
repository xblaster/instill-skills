---
name: generate-dockerfile
description: >
  Scans the current directory to identify the technology stack (Node.js, Python, Go, Rust) and generates a production-ready, multi-stage Dockerfile.
  Use when the user wants to "dockerize" an application or create a container build configuration.
  Handles conflict detection, package manager resolution (npm/yarn/pnpm/pip/poetry), and creation of .dockerignore files.
compatibility: Requires file system access (ls, cat, grep).
metadata:
  version: "1.0.0"
  author: "Agent Architect"
  generatedBy: "agent-architect-v1"
---

# Generate Optimized Dockerfile

Orchestrates the creation of a `Dockerfile` and `.dockerignore` tailored to the specific project structure, ensuring security best practices (multi-stage builds, minimal images, non-root users).

## Input
Optional: `stack` (if auto-detection fails), `port` (exposed port).

## Steps

### Phase 1: Environment Safety & Discovery (Silent)
1.  **Check for existing configuration:**
    * Run `ls -1 Dockerfile` (check existence).
    * **Logic:**
        * IF `Dockerfile` exists: **STOP**. Use `AskUserQuestion`: "A Dockerfile already exists. Do you want to overwrite it, create a `Dockerfile.new`, or cancel?"
        * ELSE: Proceed.

2.  **Stack Detection (State Machine):**
    * Run `ls -1 package.json requirements.txt pyproject.toml go.mod Cargo.toml pom.xml` to gather signal files.
    * **Logic (Hierarchy of Resolution):**
        * IF `package.json`: Set `STACK="node"`. Check lockfiles (`yarn.lock`, `pnpm-lock.yaml`) to determine installer.
        * IF `requirements.txt` OR `pyproject.toml`: Set `STACK="python"`. Check for `poetry.lock` vs `pip`.
        * IF `go.mod`: Set `STACK="go"`.
        * IF multiple signals found (e.g., Python backend + Node frontend): **STOP**. Use `AskUserQuestion`: "Multiple stacks detected. Which one is the primary entry point for this Dockerfile?" (Options: Node, Python, etc.).
        * IF no signals: **