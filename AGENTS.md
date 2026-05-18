# AGENTS.md

This repository contains the code and related engineering assets for the SYSU ECNC personnel system.

## General Conventions

- Use Conventional Commits by default when creating or suggesting Git commits.
- For small, clear, low-risk requests, AI agents may modify the code directly and run the appropriate checks afterward.
- For larger requests, cross-module changes, unclear requirements, data model changes, or changes that affect critical user flows, use the OpenSpec workflow.
- Subagents may be used in any workflow to improve efficiency. Keep task boundaries clear and avoid having multiple agents modify the same files unless explicitly coordinated.

## Small Request Workflow

When the request is small, clear, and low risk:

1. Read the relevant code and implement the change directly.
2. Run tests, type checks, formatting checks, or other verification appropriate to the scope of the change.
3. Report what changed, what was verified, and anything that remains unverified or incomplete.

## Large Request Workflow

When the request is large or not yet clear enough:

1. Use `grill-me` to ask the user follow-up questions until the goal, scope, acceptance criteria, and key constraints are clear.
2. Use `openspec-propose` to create an OpenSpec change.
3. Use `openspec-apply-change` to implement the requirement.
4. Use a subagent to run `openspec-verify-change` and review whether the implementation from step 3 satisfies the OpenSpec change:
   - If issues are found, return to step 3 and fix the implementation.
   - If no issues are found, continue to step 5.
5. Use `openspec-archive-change` to archive the change.
6. Create a Conventional Commit and push it to the remote.

## OpenSpec Notes

- The design, specs, and task list in an OpenSpec change are the primary source of truth for large-request implementation.
- Keep implementation changes aligned with the OpenSpec change scope. Avoid unrelated refactors.
- During verification, focus on whether the implementation satisfies the specs, whether all tasks are complete, whether tests cover the critical paths, and whether there are obvious regression risks.
