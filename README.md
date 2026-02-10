# 🧠 Instill Skills: Cognitive Modules for AI Agents

> **Turn your AI assistant into a proactive Senior Engineer.**

This repository is not just a collection of "docs"—it is a library of **Active Cognitive Skills** designed to give your AI agent (Cursor, Windsurf, Claude Code, Gemini) the ability to *reason, plan, and execute* complex engineering tasks autonomously.

When you install these skills, you aren't just giving your AI context; you are giving it a **Role**.

---

## 🚀 Available Skills

### 🛡️ Security & Stability
* **[Dependency Sentinel](skills/dependency-sentinel.md)** (`dependency-sentinel`)
  * *The Guardian.* Safely audits and remediates vulnerabilities. It doesn't just "report" issues—it uses a state machine to verify that updates don't break your build before committing them.
* **[Security Audit](skills/security-audit.md)** (`security-audit`)
  * *The White Hat.* Performs comprehensive security scans using tools like Semgrep or Snyk, creating prioritized remediation plans and ensuring your codebase is fortress-ready.

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

---

## 📦 Installation

Integrate these skills into your workflow in seconds using [Instill](https://github.com/xblaster/instill):

```bash
# 1. Add this repo as a remote source
instill sources add https://github.com/xblaster/instill-skills

# 2. Install the skills you need
instill install dependency-sentinel git-master
```

## 🤝 Contributing

Got an idea for a new "Cognitive Module"? 
1. Create a markdown file in `skills/`.
2. Define the `input`, `steps` (the "thought process"), and `output`.
3. Open a PR!

---

*Part of the [Instill Ecosystem](https://github.com/xblaster/instill) - Empowering Agentic Workflows.*
