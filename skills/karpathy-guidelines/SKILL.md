---
name: karpathy-guidelines
description: Behavioral guidelines to reduce common LLM coding mistakes. Use when writing, reviewing, or refactoring code to avoid overcomplication, make surgical changes, surface assumptions, define verifiable success criteria, and fail loudly on partial failures.
license: MIT
---

# Karpathy Guidelines

Behavioral guidelines to reduce common LLM coding mistakes, derived from [Andrej Karpathy's observations](https://x.com/karpathy/status/2015883857489522876) on LLM coding pitfalls and expanded to 9 rules.

**Tradeoff:** These guidelines bias toward caution over speed. For trivial tasks, use judgment.

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

- State assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them — don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear mid-task, stop. Name what's confusing. Ask.
- If uncertain about a fact, say so explicitly — don't guess and present it as known.

## 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If 200 lines could be 50, rewrite it.

**Test:** Would a senior engineer call this overcomplicated? If yes, simplify.

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it — don't delete it.
- When two patterns exist in the codebase, adopt the established one — even an imperfect one. A third pattern is always worse than either alone.

When your changes create orphans:
- Remove imports/variables/functions that your changes made unused.
- Don't remove pre-existing dead code unless asked.

**Test:** Every changed line should trace directly to the user's request.

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:
- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, pair each plan step with a verification check:
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
```

For multi-step refactors or migrations: commit between steps so a failure mid-way doesn't require rewinding completed work.

## 5. Pause at Decision Points

**Surface forks; decide together.**

- When facing a choice with real consequences (approach, architecture, exclusion criteria), stop and initiate a conversation — don't proceed unilaterally.
- When the same problem has been attempted twice without progress, stop. Re-read the original problem, re-state what is actually known, and align before continuing.
- The goal is a shared decision, not the model choosing independently or the user thinking alone.

## 6. Surface Conflicts, Don't Average Them

- When two parts of the codebase disagree (two error patterns, two testing styles, two state stores), pick one explicitly and explain why.
- Blending both doubles the bug surface and swallows errors twice.

## 7. Read Before You Write

- Before writing a new function or utility, read the surrounding code: existing helpers, exports, callers.
- Duplicate functions break silently through masking and load order — never through an error.

## 8. Tests Verify Intent, Not Just Pass

- A test that passes while the function returns a constant is not a passing test.
- Assertions must be tied to correct behavior: wrong answers should fail.
- Plausible-looking output can mask incorrect logic — tie assertions to behavior, not shape.

## 9. Fail Loud

- "Completed successfully" while silently skipping records, truncating output, or swallowing warnings is the worst class of bug.
- Surface partial failures, dropped records, convergence warnings, and retry exhaustion — never hide them in a success message.
- Applies to all code: data pipelines, models, jobs, utility functions.

---

**Pre-completion checklist — verify before declaring any task done:**
- [ ] Were assumptions stated explicitly?
- [ ] Did any change touch code outside the stated scope?
- [ ] Do tests assert on correct behavior, not just output shape?
- [ ] Could this step have silently failed, skipped records, or swallowed warnings?
