---
name: ai-content-reviewer
description: >
  Review, detect, and humanize AI-generated text. Use when the user wants to remove AI tropes, robotic phrasing, predictable structures, and "slop" to make the content credible and human-written. Handles file reading, structural analysis, style rewriting, diff generation, and safe file writing.
compatibility: Requires file system read/write capabilities (e.g., standard agent tools).
metadata:
  version: "1.0"
  author: "Agent Architect"
  generatedBy: "agent-architect-v1"
---

# Orchestrate the Review and Humanization of AI-Generated Content

**Input:** A file path containing the text to review, or a direct string of text. If omitted, the agent must ask for it.

## Steps

### Phase 1: Discovery & Disambiguation
1. **Identify the Source:**
   - If the user provides a file name, verify its existence using `ls` or standard file-checking tools.
   - *Logic:* - IF file does not exist or multiple similar files exist: STOP. Use `AskUserQuestion`.
       - *Question:* "I couldn't find the exact file. Which of these files should I review?"
       - *Options:* [List of matched files] or [Ask for correct path].
     - IF no input is provided at all: Use `AskUserQuestion`.
       - *Question:* "Please provide the path to the text file you want me to humanize."

2. **Read State:**
   - Read the content of the file silently. Do NOT output the raw text to the user.

### Phase 2: Pre-condition Check & Analysis (State Machine)
1. **Cognitive Detection Phase (Silent):** Analyze the text for common AI generation flaws:
   - *Vocabulary Tropes:* "It is important to note", "In conclusion", "Furthermore", "Delve", "Tapestry", "Crucial", "Navigating the landscape".
   - *Structural Flaws:* Perfectly symmetrical paragraph lengths, bullet-point overload, repetitive sentence structures (Subject-Verb-Object continuously).
   - *Tone Flaws:* Overly preachy/moralizing tone, lack of strong stance, excessive neutrality, absence of human idioms or varied cadence (burstiness).
   
2. **Compile Flaw Inventory:** Map out the exact locations of these flaws in your internal state.

3. **Present the Audit:**
   - Show the user a summary table of the detected flaws before making any changes.
   - *Format:*
     | ⚠ AI Pattern Detected | 📍 Context/Quote | 💡 Proposed Humanization Strategy |
     | :--- | :--- | :--- |
     | [Pattern] | "[Short quote]" | [How to fix it] |

### Phase 3: Execution & Disambiguation
1. **Drafting the Humanized Version (Internal State):**
   - Rewrite the text to eliminate the detected flaws. 
   - Increase text *perplexity* and *burstiness* (mix very short sentences with longer, complex ones).
   - Inject a natural, credible tone appropriate for the context.
   - **Crucial:** Maintain the exact original language of the source text (e.g., if French, output perfect, idiomatic French).

2. **Approval Gate:**
   - Present a short excerpt or a high-level summary of the changes.
   - Use `AskUserQuestion` to determine the save destination.
   - *Question:* "Review complete. How would you like to save the humanized content?"
   - *Options:* 1. Overwrite the original file.
     2. Save as `<original_filename>_humanized.<ext>`.
     3. Just print it to the console.

3. **Execution:**
   - Execute the file write operation based on the user's choice using the appropriate write tool/command.

## Output
- Display a success message with a green checkmark (✓).
- Show a checklist of improvements made:
  - [x] Removed predictable AI vocabulary.
  - [x] Varied sentence length and structure (burstiness).
  - [x] Adjusted tone for human credibility and natural flow.
  - [x] Preserved core meaning and factual accuracy.

## Guardrails
- **Strict Adherence to Meaning:** Do NOT hallucinate new facts, arguments, or data not present in the original text.
- **No AI Meta-Talk:** Do NOT include phrases like "As an AI...", "Here is the revised version", or "I have humanized the text." Write only the final content in the file.
- **Safe Writing:** NEVER overwrite the original file without explicit user confirmation (Approval Gate).
- **Style Constraints:** Avoid overly flowery language. A "normal human being" writes clearly, sometimes bluntly, and with varying rhythm.
