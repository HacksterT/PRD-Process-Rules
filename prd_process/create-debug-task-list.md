# Rule: Creating a Debug Task List

## Goal

To guide an AI assistant in producing a **Bug Fix Task List** in Markdown based on a completed Bug Investigation Document (BID). The task list should be actionable for a junior developer to implement safely and with minimal risk of regression.

## Output

- **Format:** Markdown (`.md`)
- **Location:** `/debug/`
- **Filename:** `tasks-[bid-file-name].md` (e.g., `tasks-bid-login-timeout.md`)

## Process

1. **Receive BID Reference:**
   - The user points the AI to a specific BID file.

2. **Analyze BID:**
   - Review confirmed root cause, scope, and environment from the BID.

3. **Assess Current State:**
   - Review the existing codebase to understand:
     - Existing infrastructure and architectural patterns.
     - Components or utilities that may be affected.
     - Related test coverage and logging.

4. **Phase 1: Generate Parent Tasks ONLY:**
   - Based on BID analysis and current state, create 5–8 high-level parent tasks required to fix the bug.
   - Do **NOT** include any subtasks at this stage.
   - Present these parent tasks to the user in the specified format.
   - Inform the user: "I have generated the high-level fix tasks based on the BID. Ready to generate the sub-tasks? Respond with 'Go' to proceed."

5. **Wait for Confirmation:**
   - Pause and wait for the user to respond with "Go".

6. **Phase 2: Generate Subtasks in Batches:**
   - Once the user confirms, break down parent tasks into smaller, actionable subtasks in batches of 2 parent tasks at a time.
   - For each parent task in the current batch:
     - Create 5–15 detailed subtasks that logically follow from the parent task.
     - Include environment-aware implementation details (function names, file paths, etc.).
     - Reference patterns, naming conventions, and dependencies from the existing codebase.
     - Include safeguards such as tests, logging, and rollback.

7. **Identify Relevant Files:**
   - Based on the BID and tasks, list potential files that will need to be created or modified.
   - Include associated test files.

8. **Generate Final Output:**
   - Combine parent tasks, subtasks, relevant files, and notes into the final Markdown structure.

9. **Save Task List:**
   - Save the generated document in the `/debug/` directory with the filename `tasks-[bid-file-name].md`.

## Subtask Quality Guidelines

When creating subtasks in Phase 2, ensure they meet these quality criteria:

1. **Specific and Actionable:**
   - Include concrete file paths, function names, and parameters.
   - Specify configuration, dependencies, or API calls.

2. **Environment-Aware:**
   - Use versions, OS, and stack constraints from the BID.

3. **Logically Sequenced:**
   - Fix in smallest testable increments.
   - Ensure dependencies are resolved in the correct order.

4. **Include Safeguards:**
   - Write unit and integration tests.
   - Implement logging and error handling.
   - Plan for rollback or feature flags.

5. **Evidence-Based:**
   - Only address code confirmed to be related to the root cause.

## Output Format

The generated task list **must** follow this structure:

```markdown
## Relevant Files

- `path/to/file1.ts` - Contains logic identified in BID as root cause.
- `path/to/file1.test.ts` - Unit tests for `file1.ts`.
- `src/config/envLoader.ts` - Environment variable loader impacted by bug.
- `src/config/envLoader.test.ts` - Unit tests for `envLoader.ts`.

### Notes

- Tests should typically be placed alongside their code files.
- Use `npx jest [optional/path]` or equivalent to run tests.

## Tasks

- [ ] 1.0 Parent Fix Task Title
  - [ ] 1.1 Implement targeted code change per BID findings in `file1.ts`
  - [ ] 1.2 Add unit tests to reproduce and confirm fix
  - [ ] 1.3 Update relevant configuration documentation
- [ ] 2.0 Parent Fix Task Title
  - [ ] 2.1 Remove unused variable as identified in BID
  - [ ] 2.2 Validate no regression in dependent modules
