# 🧠 Instill Skills: Cognitive Modules for AI Agents

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)](package.json)
[![Instill](https://img.shields.io/badge/Powered%20by-Instill-blueviolet)](https://github.com/xblaster/instill)

> **Turn your AI assistant into a proactive Senior Engineer.**

This repository is not just a collection of "docs"—it is a library of **Active Cognitive Skills** designed to give your AI agent (Cursor, Windsurf, Claude Code, Gemini) the ability to *reason, plan, and execute* complex engineering tasks autonomously.

When you install these skills, you aren't just giving your AI context; you are giving it a **Role**.

---

## ⚡ Quick Start

```bash
# 1. Add this repo as a remote source
instill sources add https://github.com/xblaster/instill-skills

# 2. Install the skills you need
instill install dependency-sentinel git-master
```

---

## 🚀 Available Skills

### 🛡️ Security & Stability
* **[Dependency Sentinel](skills/dependency-sentinel.md)** (`dependency-sentinel`)
  * *The Guardian.* Safely audits and remediates vulnerabilities. It doesn't just "report" issues—it uses a state machine to verify that updates don't break your build before committing them.
* **[Security Audit](skills/security-audit.md)** (`security-audit`)
  * *The White Hat.* Performs comprehensive security scans using tools like Semgrep or Snyk, creating prioritized remediation plans and ensuring your codebase is fortress-ready.

### 🔍 Diagnostic & Debugging
* **[Debug Stacktrace Resolver](skills/debug-stacktrace-resolver.md)** (`debug-stacktrace-resolver`)
  * *The Fixer.* Analyze, research, and resolve complex software errors and stack traces. It performs environment discovery, structured web research, and proposes deterministic fixes after verifying context.

### 🏗️ Architectural Intelligence
* **[Architect Vision Audit](skills/architect-vision-audit.md)** (`architect-vision-audit`)
  * *The CTO.* Ensures your code aligns with the project's long-term vision. It detects "drift" between your documentation and your actual implementation, preventing scope creep and architectural decay.
* **[Tech Debt Loan Officer](skills/tech-debt-loan-officer.md)** (`tech-debt-loan-officer`)
  * *The Auditor.* Treats code complexity as financial liability. Before you merge that "quick fix," this skill calculates the interest rate on your technical debt and advises on whether you can afford the loan.

### ⚙️ DevOps & Workflow High-Performance
* **[Git Master](skills/git-master.md)** (`git-master`)
  * *The Release Manager.* Orchestrates the perfect commit. Handling everything from conventional commit messages to resolving complex merge conflicts and crafting descriptive Pull Requests.
* **[Generate Dockerfile](skills/generate-dockerfile.md)** (`generate-dockerfile`)
  * *The Ops Expert.* Instantly detects your tech stack (Node, Python, Go, Rust) and generates a production-hardened, multi-stage `Dockerfile` faster than you can say "containerize."

### 📝 Documentation Auto-Pilot
* **[Auto-Doc Manager](skills/auto-doc-manager.md)** (`auto-doc-manager`)
  * *The Librarian.* Banish "usage rot" forever. This skill automatically synchronizes your code changes with your documentation, ensuring your READMEs, JSDoc, and OpenAPI specs are always up to date.

### 🧠 Strategic & Creative Intelligence
* **[Improbable Recruiter](skills/improbable-recruiter.md)** (`improbable-recruiter`)
  * *The Talent Scout.* Identifies the "Black Swan" hire. It analyzes your codebase's "Technical DNA" to generate a job description for an atypical profile (e.g., an Ethnobotanist for a database project) who would bring disruptive innovation.

### 🚀 Growth & Community

* **[OSS Community Catalyst](skills/oss-community-catalyst.md)** (`oss-community-catalyst`)
  * *The Evangelist.* Audit your repo for "social proof" and generate high-engagement technical content. It identifies friction in your onboarding flow and creates a launch plan to amplify your project's reach.

---

## 🧩 Skill Architecture

Each skill in this repository follows a structured, state-machine approach to ensure reliability and safety:

1.  **Input Handling & Resolution**: Context discovery and proactive ambiguity resolution (asking questions instead of hallucinating).
2.  **Pre-flight & Discovery**: Silent verification of the local environment, dependencies, and tool availability.
3.  **Execution**: Running deterministic commands (preferring `--json` output) to gather ground-truth data.
4.  **Reporting & UX**: Structured Markdown output with clear summaries and actionable next steps.
5.  **Guardrails**: Explicit safety constraints to protect your codebase, secrets, and data integrity.

---

## 📂 Project Structure

```text
skills/
├── architect-vision-audit.md       # Architectural alignment & CTO-level oversight
├── auto-doc-manager.md             # Documentation synchronization
├── debug-stacktrace-resolver.md    # Error analysis & resolution
├── dependency-sentinel.md          # Vulnerability auditing & remediation
├── generate-dockerfile.md          # Tech stack detection & Dockerization
├── git-master.md                   # Advanced Git workflows & PR management
├── improbable-recruiter.md         # Strategic hiring & cognitive diversity analysis
├── oss-community-catalyst.md       # Community engagement & OSS growth
├── security-audit.md               # Comprehensive security scanning
└── tech-debt-loan-officer.md       # Technical debt & complexity analysis
```

---



## 🤝 Contributing

Got an idea for a new "Cognitive Module"? 
1. Create a markdown file in `skills/`. (Use our [Template Skill](.instill/library/template-skill.md) as a starting point).
2. Define the `input`, `steps` (the "thought process"), and `output`.
3. Open a PR!

---

*Part of the [Instill Ecosystem](https://github.com/xblaster/instill) - Empowering Agentic Workflows.*
