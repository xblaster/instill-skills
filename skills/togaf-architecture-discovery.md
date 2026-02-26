---
name: togaf-architecture-discovery
description: >
  Explore and document existing enterprise architecture using the TOGAF framework. 
  Use when the user wants to understand projects, components, and especially the correlations and dependencies between them. 
  Handles the creation of strictly evidence-based architectural hypotheses, including dependency parsing (pom.xml, package.json, etc.) to generate Mermaid.js visual relationship diagrams. 
  Manages the workflow between 'hypothesis' (agent-generated) and 'verified' (human-validated) knowledge bases.
compatibility: Requires standard Unix tools (find, grep, cat, jq, xmllint) and a Markdown viewer supporting Mermaid.js.
metadata:
  version: "1.2"
  author: "Agent Architect"
  generatedBy: "agent-architect-v1"
---

# Orchestrate the discovery of enterprise architecture, focusing on component correlations and strict evidence-based mapping.

Input: The path to the repository, or a specific correlation request (e.g., "How does the Order API communicate with the Payment Service?").

## Steps

### Phase 1: Discovery, Disambiguation & Dependency Parsing (Gathering)
1.  **Environment Initialization**:
    * Run `mkdir -p hypothesis verified` to ensure the state directories exist.
2.  **Ground Truth Synchronization**:
    * Silently run `find verified/ -type f -name "*.md" -exec cat {} +` to load established human-verified knowledge into context.
3.  **Dependency & Correlation Scanning**:
    * Identify package managers: Run `find . -maxdepth 2 -name "pom.xml" -o -name "package.json" -o -name "requirements.txt" -o -name "docker-compose.yml"`.
    * Parse dependencies silently (e.g., using `jq` for JSON or `grep` for imports/API calls).
    * Trace connections: Use `grep -rnw . -e "http://" -e "https://" -e "import "` to find network calls or direct code couplings between internal modules.
    * *Rule*: Record the exact file, line number, and the nature of the correlation (e.g., REST call, library import, event broker pub/sub).
    * *Ambiguity Handling*: IF a discovered endpoint or import cannot be statically resolved to a known internal component:
        * Call `AskUserQuestion`.
        * *Question*: "I found Component A calling endpoint `/api/v1/payments`, but I cannot locate the source code for the payment service. Is this an external system or located in another repository?"

### Phase 2: Pre-condition Check (State Machine)
1.  **Verification State Check**:
    * IF the requested component topology is already documented in `verified/<component-topology>.md`: STOP. Inform the user and present a summary.
    * IF it exists in `hypothesis/`: Ask the user to overwrite or augment.
    * ELSE: Proceed.
2.  **Correlation Evidence Check**:
    * IF NO explicit link (import, config, network call) is found between components: STOP. Inform the user: "No concrete evidence found in the codebase to establish a correlation between these components."

### Phase 3: Execution
1.  **Hypothesis & Topology Generation**:
    * Draft the architectural document mapping the findings to TOGAF Application/Technology domains.
    * **Visual Correlation Mapping (Mermaid)**: Translate the extracted dependencies into a C4-style Container diagram or flowchart.
    * Structure the document strictly as follows:
        * **Component/System**: [Name]
        * **TOGAF Domain**: [Application/Technology Architecture]
        * **Identified Pattern**: [e.g., API Gateway, Point-to-Point, Event-Driven]
        * **Component Correlations Diagram**:
          ```mermaid
          graph TD
            %% Only draw edges that have proven code references
            A[Component A] -->|Protocol/Method e.g., HTTPS GET| B[Component B]
          ```
        * **Correlation Proof/Evidence**:
            * `A -> B`: [File path, line number, code snippet proving the connection].
2.  **File Creation**:
    * Write the drafted content to `hypothesis/<system-topology>.md`.

## Output

* Display an emoji-rich summary of the findings (e.g., "🔗 **Correlations Discovered & Mapped**: [System Topology]").
* Show a markdown checklist of the generated files.
* Display a mandatory call-to-action:
    * "[ ] Please review `hypothesis/<system-topology>.md` and its correlation diagram."
    * "[ ] Verify the edges in the Mermaid diagram. If accurate, manually move the file to the `verified/` directory."

## Guardrails

* **Zero Deduction Policy for Correlations**: Do NOT draw a relationship arrow (`-->`) in Mermaid between Component A and Component B unless a direct code reference, import, or network configuration linking them was found and cited in the Proof section.
* **External Systems**: Clearly mark external/unresolved dependencies in the Mermaid diagram (e.g., using dashed lines or specific node shapes) if they are not part of the analyzed codebase.
* **Immutability of Verified Data**: Do NOT modify ANY file inside the `verified/` directory.
