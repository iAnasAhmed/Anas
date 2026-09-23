# CLAUDE.md — Autonomous Agent Instructions

Guidelines for working with Claude as an autonomous agent.

**Goal:** Give Claude the full task, clear boundaries, and let it execute autonomously to deliver high-quality results.

## 1. Execution — take ownership and keep going

- Take ownership of the entire task.
- Define a clear **Definition of Done** before execution.
- Continue automatically when the next step does not require human input.
- Do not stop merely to report progress or ask whether to continue.
- Include progress updates alongside your next action.

## 2. Human Approval — stop only when necessary

Stop and request approval only when:

- A required decision or missing input blocks execution.
- An operation could delete or irreversibly modify data.
- A force push or destructive Git operation is required.
- Changes outside the repository are necessary.
- Production systems, credentials, or sensitive data could be affected.

> Keep permission prompts enabled for destructive operations.

## 3. Multi-Agent Execution — handle large tasks with subagents

- Split independent work across specialized subagents.
- Assign clear ownership and scope to each agent.
- Avoid overlapping file modifications.
- Validate each agent's evidence before accepting its results.
- Integrate and test the combined output.

## 4. Progress Tracking — use `TASKS.md` as the source of truth

- Maintain `TASKS.md` throughout execution.
- Record completed and pending tasks.
- Update the checklist after meaningful progress.
- Add newly discovered tasks.
- Record blockers and unresolved issues.

## 5. Validation — verify before declaring completion

- Verify every Definition of Done criterion.
- Run relevant tests.
- Review the final diff.
- Identify unverified assumptions.
- Never claim a test passed unless it was actually executed successfully.
- Report any checks that could not be performed.

## 6. Final Report — end with a clear, concise summary

End every run with these three sections:

| Section | Contents |
| --- | --- |
| **Blocked on me** | Decisions or approvals required from the user. |
| **Changed** | Files modified and work completed. |
| **Found** | Issues discovered, test results, and anything that could not be verified. |

Keep the final report concise and evidence-based.
