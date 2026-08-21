---
name: concise-coding
description: Guides concise, minimal code changes with sparse comments, readable formatting, scoped edits, temporary unit tests, and clear handoff notes. Use whenever modifying, implementing, fixing, or refactoring code.
---

# Concise Coding

## Original requirements

1. keep the modification concise, and try to make minimal changes to the codebase
2. reduce the comment usages, only include comments when the code is really hard to understand
3. avoid writing hard to understand codes, unless it provides major performance boost
4. do not touch the parts where you werent asked to make a change
5. avoid multi-line lists, for example:

```
a_list = ["1",
    "2",
    "3",
    ]
```

or 

```
def func(
    arg1,
    arg2,
):
```

6. do unit test on the code you wrote, but remove the testing files and artifacts afterwards
7. when you are finished, clearly states which parts you modified, the consequences, how to run it, and what are the current concerns

## Detailed instructions

### Keep changes minimal

- Make the smallest change that fully satisfies the request.
- Read the relevant code before editing and follow its existing conventions.
- Do not refactor nearby code, rename unrelated symbols, reorder imports unnecessarily, reformat untouched sections, add dependencies, or change configuration unless the requested work requires it.
- Prefer editing an existing function or file over introducing a new abstraction when both approaches are equally clear.
- Keep the resulting change easy to review. Avoid generated file churn and unrelated whitespace changes.

### Use comments sparingly

- Prefer clear names and straightforward control flow over explanatory comments.
- Add a comment only when a careful reader could not reasonably infer why the code exists, when a non-obvious constraint must be preserved, or when an unusual performance choice needs justification.
- Comments should explain the reason or constraint. Do not narrate what the next line already says.
- Keep existing comments unless the change makes them inaccurate. Update or remove only comments affected by the requested modification.
- Do not add section banners, commented-out code, change logs, or restatements of the user request inside source files.

### Prefer readable code

- Use simple expressions, descriptive names, early returns, and direct control flow.
- Avoid compressed one-liners, clever language tricks, deep nesting, hidden side effects, and abstractions that make a small change harder to follow.
- Add a helper only when it clearly improves readability, removes meaningful duplication, or isolates behavior that needs focused testing.
- Use a harder-to-read implementation for performance only when the expected improvement is major and relevant to the request. Verify the improvement with a benchmark or other concrete evidence when practical, and explain the tradeoff in the final report.

### Stay within the requested scope

- Do not clean up, modernize, optimize, or fix unrelated code discovered during the task.
- Do not overwrite or revert existing user changes.
- Make an adjacent change only when the requested implementation cannot work correctly without it. State why that additional change was necessary in the final report.
- Report unrelated problems instead of fixing them unless the user expands the scope.

### Keep short structures on one line

- Keep function signatures, calls, imports, list literals, tuple literals, dictionary literals, and similar structures on one line when they remain reasonably readable.
- Do not expand short structures across multiple lines merely because each item could occupy its own line.
- Follow the repository's required formatter when it enforces multi-line formatting. Allow multiple lines when a single line would exceed the project's line-length limit or materially reduce readability.

Preferred:

```python
a_list = ["1", "2", "3"]
def func(arg1, arg2):
    return arg1
```

Avoid:

```python
a_list = [
    "1",
    "2",
    "3",
]

def func(
    arg1,
    arg2,
):
    return arg1
```

### Test the changed behavior

- Run the smallest relevant existing unit tests after making the change.
- When existing tests do not cover the behavior, create a focused temporary unit test or verification script, run it, and remove it before finishing.
- Remove only files and artifacts created during the current task. Never remove existing tests, user-owned files, or artifacts that existed before the task.
- Clean up temporary test files, generated coverage reports, temporary outputs, and cache directories created by the verification when it is safe to identify them.
- Do not claim that tests passed unless they were actually run. If testing is impossible, state the exact reason and the remaining risk.

### Give a complete final report

State each of the following clearly:

1. Describe which files, functions, or behaviors were modified.
2. Explain the user-visible and technical consequences, including compatibility or performance effects.
3. Provide the exact command or steps needed to run the changed code.
4. List current concerns, untested cases, assumptions, and known limitations. State that there are no known concerns when none remain.

## Completion checklist

- The requested behavior is implemented with the smallest practical change.
- Unrelated code remains untouched.
- New code is straightforward and comments are limited to necessary explanations.
- Relative paths and symbolic links were inspected and verified when applicable.
- Short structures remain on one line where practical.
- Relevant unit tests were run.
- Temporary tests and artifacts created during the task were removed.
- The final report covers modifications, consequences, run instructions, and current concerns.
