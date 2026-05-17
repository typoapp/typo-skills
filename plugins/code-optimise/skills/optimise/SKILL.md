---
description: Optimise the developer's unstaged code changes for clarity, performance, and conciseness without changing any behaviour. Use when the user runs /code-optimise:optimise or asks to clean up, optimise, or improve their uncommitted code.
---

# Code Optimiser

Optimise unstaged code changes in place. Behaviour must be identical before and after — this is a safe refactor only.

## Steps

1. Get the list of files with unstaged changes:

```
git diff --name-only
```

If there are no unstaged changes, stop and tell the user there is nothing to optimise.

2. For each changed file, get the exact unstaged diff to understand what the developer wrote:

```
git diff -- <file>
```

3. Read the full content of each changed file.

4. Apply the following optimisations directly to each file — edit them in place:

**Simplify expressions**
- Remove redundant boolean comparisons (`=== true`, `=== false`)
- Collapse negated conditions where a positive form is clearer
- Replace verbose ternaries with simpler expressions when safe

**Remove redundancy**
- Remove unused variables, imports, and assignments that are never read
- Collapse intermediate variables that are assigned once and immediately returned
- Remove unnecessary else blocks after an early return

**Improve loops and iteration**
- Replace manual index loops with idiomatic equivalents (`map`, `filter`, `reduce`, `for...of`) where the language supports it and the intent is clearer
- Remove redundant array copies when the original is not reused

**Naming and structure**
- Only rename a variable if the new name is unambiguously clearer — do not rename for style preference alone
- Flatten unnecessary nesting (early returns, guard clauses) where it reduces cognitive load

**Performance (safe only)**
- Move invariant expressions out of loops if they provably do not depend on loop state
- Replace repeated property lookups with a local variable if accessed 3+ times

5. After editing all files, run:

```
git diff
```

to produce the final diff of what changed.

6. Print a summary in this format:

**Optimised: `<filename>`**
- [one line per change, plain English, explaining what was simplified and why]

Repeat for each file. Keep each bullet under 15 words.

## Hard rules — never break these

- Do not change function signatures, parameter names, or return types
- Do not change what a function returns or the side effects it produces
- Do not reorder or remove logic branches that affect observable behaviour
- Do not touch files that were not in the original `git diff --name-only` output
- Do not optimise staged files — only unstaged changes are in scope
- If a change would require re-testing business logic, skip it and note it as out of scope
- If $ARGUMENTS specifies a filename or pattern (e.g. `src/utils.ts`), restrict optimisations to matching files only
