# PRD & Debugging Process Rules

A lightweight, opinionated set of **Markdown rule docs** for building software with AI assistants in a controlled, auditable way.  
This repo includes rules for **feature PRDs**, **task creation**, and **investigation-first debugging**.

## What’s inside

- `prd_process/create-feature-prd.md` – Rule for generating a feature-specific PRD from a prompt
- `prd_process/create-overview-prd.md` – Rule for generating a project overview PRD
- `prd_process/create-task-from-prd.md` – Rule for generating task lists from a PRD (parent tasks → subtasks)
- `prd_process/task-management.md` – Guidance for task hygiene and workflow
- `prd_process/investigate-bug.md` – Investigation-first debugging rule (Phase 1 & 2 questions → Phase 3 BID)
- `prd_process/create-debug-task-list.md` – Rule for turning a completed investigation into a fix task list

## Why this exists

AI can be brilliant *and* impulsive. These rules:

- Force **clarifying questions** before output
- Keep fixes **root-cause driven** (no “rewrite until it works”)
- Produce artifacts a **junior dev** can follow
- Reduce regressions through **explicit scope & tests**

## How to use

1. **Pick the rule** that matches your need:
   - New feature → `create-feature-prd.md`
   - Project overview → `create-overview-prd.md`
   - Turn PRD into tasks → `create-task-from-prd.md`
   - Investigate a bug → `investigate-bug.md`
   - Turn investigation into fix tasks → `create-debug-task-list.md`

2. **Paste the rule** into your AI assistant as system/context instructions.

3. **Follow the phases** exactly:
   - PRDs: Questions → PRD (save as `prd-[feature].md`)
   - Debugging: Phase 1 (general) → Phase 2 (env/recurring issues) → Phase 3 (BID)
   - Tasking: Parent tasks → “Go” → Subtasks in batches of 2 parents

4. **Save outputs** in your project repo under `/tasks` or `/debug` as directed by each rule.

## Conventions

- Output format: **Markdown**
- Audience: **Junior developer**
- Style: **Specific, testable, codebase-aware**
- Do not auto-start servers, clear caches, or rebuild containers without explicit approval.

## Example prompts

- **Feature PRD**
  > “Using the `create-feature-prd` rule, generate a PRD for adding Google SSO to our web app. Wait for my answers to your questions before drafting.”

- **Debug Investigation**
  > “Using the `investigate-bug` rule, investigate intermittent 502s on the API. Ask Phase 1 and Phase 2 questions first; do not propose fixes.”

- **Create Tasks from PRD**
  > “Using `create-task-from-prd`, read `/tasks/prd-google-sso.md` and produce parent tasks only. Wait for ‘Go’ before subtasks.”

## Roadmap

- Templates for RCAs/postmortems
- Optional checklists for CI gates (lint, tests, contracts)
- Rule variants for frontend/backend/data/infra

## Contributing

PRs welcome! Keep rules:
- Concise but complete
- Reproducible and audit-friendly
- Bias toward **questions first**, **evidence-driven fixes**

## License

MIT — see `LICENSE`.
