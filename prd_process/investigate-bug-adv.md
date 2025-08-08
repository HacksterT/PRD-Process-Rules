# Rule: Investigating a Bug

## Goal

To guide an AI assistant in creating a detailed **Bug Investigation Document** (BID) that captures all relevant information to identify and confirm the root cause of a defect before proposing or implementing a fix — while confirming recurring environment issues and avoiding unnecessary actions.

## Process

1. **Receive Bug Report:**
   - Get initial bug description, reporter, and any logs/screenshots.

2. **Phase 1: Ask Investigation Questions (General Context):**
   - Select 5–7 most relevant general debugging questions based on the initial bug report.
   - Present these questions in a numbered list for easy reference.
   - Wait for the user to provide answers before proceeding.

3. **Phase 2: Ask Environment & Recurring-Issue Questions:**
   - Before generating the BID, confirm common environmental factors and recurring patterns that have caused delays or false leads in the past.
   - These questions are separate from Phase 1 and should be asked **in full** before continuing.

4. **Phase 3: Generate BID:**
   - Based on answers from Phases 1 and 2, generate a comprehensive BID following the structure below.
   - Ensure each section meets the quality guidelines.

5. **Save BID:**
   - Save as `bid-[short-bug-desc].md` inside the `/debug` directory.

---

## Phase 1: Investigation Questions (General Context)

The AI should adapt its questions based on the report, but here are common areas to explore:

- **Environment:** "What is the exact environment (OS, stack, versions, hosting) where the bug occurs?"
- **Reproduction:** "Can the bug be reproduced consistently? If so, what are the steps?"
- **Expected vs Actual:** "What behavior did you expect? What actually happened?"
- **Logs & Errors:** "Are there relevant logs, stack traces, or monitoring alerts?"
- **Recent Changes:** "What changes have been made recently that could affect this?"
- **Scope:** "Is this issue isolated to one module/component or system-wide?"
- **External Factors:** "Could this involve external APIs, network conditions, or hardware?"

---

## Phase 2: Environment & Recurring-Issue Questions

These should **always** be asked to prevent repeated mistakes and wasted time:

1. **Docker Usage & Cache:**
   - "Are you running this project inside Docker for this debugging session? If yes, should we clear/rebuild the Docker cache before investigating?"
2. **Browser Cache:**
   - "Does this issue involve browser-based behavior? If so, has the browser cache been cleared or disabled for testing?"
3. **Server State:**
   - "Is the server currently running? Should I restart it if needed, or leave server state management to you?"
4. **Development Environment Context:**
   - "Where is the AI assistant expected to operate right now?"
     - IDE in Windows (AI also in Windows)
     - IDE in Windows with AI in Linux/Ubuntu terminal
     - Full project in Linux/Ubuntu environment
     - Other (please specify)
5. **Environment Alignment:**
   - "Do I need to match my debugging instructions/code paths to the OS and tooling of your active environment?"

The assistant **must not** automatically restart servers, clear caches, or rebuild containers unless explicitly instructed.

---

## BID Structure

1. **Overview:** Brief summary of the bug and observed impact.
2. **Environment:** OS, dependencies, stack versions, hosting details.
3. **Steps to Reproduce:** Numbered list with required data/config.
4. **Expected Behavior:** Plain description of intended behavior.
5. **Actual Behavior:** Plain description of what happens instead.
6. **Logs & Evidence:** Key snippets with timestamps.
7. **Suspected Root Causes:** Evidence-based hypotheses.
8. **Impact Analysis:** Who/what is affected and severity.
9. **Open Questions:** Information still needed.

---

## BID Quality Guidelines

- Must be reproducible before proceeding.
- All environment/version details included.
- No fixes proposed before cause is confirmed.
- Hypotheses must be evidence-based.
- Scope must be clearly defined to avoid partial fixes.

---

## Target Audience

Assume the primary reader of the BID is a **junior developer** who will later create a fix based on the findings. The BID should remove ambiguity and avoid assumptions.

---

## Interaction Model

The process requires user confirmation between phases:

1. After Phase 1 (general questions), wait for answers.
2. After Phase 2 (environment & recurring-issue questions), wait for answers.
3. Only proceed to generating the BID after receiving sufficient information from both phases.
4. If answers are incomplete or unclear, ask focused follow-up questions before proceeding.

---

## Output

- **Format:** Markdown (`.md`)
- **Location:** `/debug/`
- **Filename:** `bid-[short-bug-desc].md`
