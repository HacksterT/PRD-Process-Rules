# Rule: Investigating a Bug

## Goal

To guide an AI assistant in creating a detailed **Bug Investigation Document** (BID) that captures all relevant information to identify and confirm the root cause of a defect before proposing or implementing a fix.

## Process

1. **Receive Bug Report:**
   - Get initial bug description, reporter, and any logs/screenshots.

2. **Phase 1: Ask Investigation Questions:**
   - Select 5–7 most relevant questions based on the initial bug report.
   - Present these questions in a numbered list for easy reference.
   - Wait for the user to provide answers before proceeding.

3. **Phase 2: Generate BID:**
   - Based on the bug report and user answers, generate a comprehensive BID.
   - Follow the structure outlined in the "BID Structure" section.
   - Ensure each section meets the quality guidelines.

4. **Save BID:**
   - Save the generated document as `bid-[short-bug-desc].md` inside the `/debug` directory.

## Investigation Questions (Examples)

The AI should adapt its questions based on the report, but here are common areas to explore:

- **Environment:** "What is the exact environment (OS, stack, versions, hosting) where the bug occurs?"
- **Reproduction:** "Can the bug be reproduced consistently? If so, what are the steps?"
- **Expected vs Actual:** "What behavior did you expect? What actually happened?"
- **Logs & Errors:** "Are there relevant logs, stack traces, or monitoring alerts?"
- **Recent Changes:** "What changes have been made recently that could affect this?"
- **Scope:** "Is this issue isolated to one module/component or system-wide?"
- **External Factors:** "Could this involve external APIs, network conditions, or hardware?"

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

## BID Quality Guidelines

When creating each section of the BID, ensure they meet these criteria:

1. **Must Be Reproducible:**
   - Include exact steps so another developer can replicate.

2. **Complete Environment Details:**
   - OS, software versions, frameworks, dependencies.

3. **Evidence-Based Hypotheses:**
   - Do not propose fixes without proof.
   - Avoid speculative or “shotgun” debugging.

4. **Clear Scope:**
   - Identify all affected areas to prevent partial fixes.

## Target Audience

Assume the primary reader of the BID is a **junior developer** who will later create a fix based on the findings. The BID should remove ambiguity and avoid assumptions.

## Interaction Model

The process requires user confirmation between phases:

1. After presenting investigation questions, wait for user answers.
2. Only proceed to generating the BID after receiving sufficient information.
3. If answers are incomplete or unclear, ask focused follow-up questions before proceeding.

## Output

- **Format:** Markdown (`.md`)
- **Location:** `/debug/`
- **Filename:** `bid-[short-bug-desc].md`
