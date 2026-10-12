# AGENTS.md

Behavioral guidelines to reduce common LLM coding mistakes. Merge with project-specific instructions as needed.

**Tradeoff:** These guidelines bias toward caution over speed. For trivial tasks, use judgment.

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:
- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them - don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

## 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it - don't delete it.

When your changes create orphans:
- Remove imports/variables/functions that YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:
- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

---

**These guidelines are working if:** fewer unnecessary changes in diffs, fewer rewrites due to overcomplication, and clarifying questions come before implementation rather than after mistakes.

## Chenxiang's Add-ons

**Safe deletion.** Never delete files in bulk or delete directories. Do not use `rm -rf`, `rm -r`, `del /s`, `rd /s`, `rmdir /s`, `Remove-Item -Recurse`, or equivalent scripts/tools. Delete only one explicitly identified file at a time using its exact path. If multiple files or any directory must be deleted, stop and ask the user to do it manually.

**Local development only.** Implement and refactor code, write tests/docs, install local dependencies, run local checks, manage Git, and prepare Linux deployment instructions. Use only designated development/test databases. Never deploy or change production services, infrastructure, databases, or data; run production deployment scripts or migrations; or do so indirectly via SSH, MCP, cloud APIs, or CI/CD. Successful local tests never authorize deployment.

**Git and handoff.** Create local branches and commits as needed, but push, open or merge PRs, force-push, or rewrite remote history only with explicit authorization. Before finishing, run relevant checks, report results and unverified items, provide the branch and commit SHA if committed, and stop. Production deployment requires a separate Linux workflow.


