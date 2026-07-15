# Coding Guide

**Lightweight Karpathy/Linux/Hermes Hybrid**
**For Small-Scale Experimental and Research Projects**

These rules govern all AI-assisted coding, refactoring, planning, and development tasks. They enforce simplicity, transparency, backward compatibility, and auditable continuity while preventing common AI pitfalls such as hidden errors or fabricated outputs. All agents must adhere to them strictly.

---

## 1. Surface Assumptions and Uncertainty Explicitly

Before implementing any change, explicitly state all key assumptions. If the request is ambiguous or admits multiple interpretations, present the options or seek clarification rather than guessing. Never proceed with unverified interpretations.

## 2. Let Real Errors Propagate

Don't do any error handling. Allows genuine errors (e.g., missing files, invalid inputs, network failures) to surface naturally. Do not introduce broad `try/except` blocks, default fallbacks, fabricated data, or other mechanisms that conceal root causes.

## 3. Never Break Userspace

Treat backward compatibility as a first-class constraint. Do not introduce breaking changes to existing interfaces, APIs, user-visible behaviors, or downstream dependencies without explicit discussion and provision of migration guidance.

## 4. Smallest Viable Change

Make only the minimal change necessary to fulfill the stated requirement. Strictly match the existing code style, structure, and conventions. Do not refactor unrelated code or add speculative features, abstractions, or configurability.

## 5. Verifiable Goals Over Vague Intent

For any non-trivial task, first rephrase the request into concrete, testable success criteria or a short plan with explicit verification checkpoints before writing significant code.

## 6. Verify Every State Change

Every data transformation must be followed by a structural check of the result (shape, type, sample values, data size, rows). Do not chain operations without inspecting each intermediate output.

## 7. No Hypothetical Error Handling

Do not write code that coerces types, fill NAs, or adjust formats unless you have first printed the variable and confirmed the problem exists. Do not write defensive code. Defensive code silently corrupts data without error.

## 8. Show Code and Real Output — Never Answer by Description Alone
Never answer data/analysis questions with prose alone — write code that produces the answer. All example and test scripts go in test or example folder. All output must be written to result files, not just printed to chat. Let the code and the data talk.

### 9. Persistent Project State Log
Maintain `PROJECT_PROGRESS.md` in the project root as the single, authoritative, high-level project state file. This file must remain extremely concise.

All changes to `PROJECT_PROGRESS.md` must be appended to a separate archive file: `archive/project_archive_log.md` 

Create the file and the archive folder if not exist.

`PROJECT_PROGRESS.md` must contain only the following sections:

- **Project Description**: One single sentence describing the project.
- **Environment**: Running environment and how to activate. If the user has not designated any environment, clarify with user about the system conda and python. Then create and maintain a self-sustained virtual environment (conda or venv) under the workspace, and sync to an env setting file; record all the outside resources needed (module, absolute path of software and data).
- **Aiming Structure**: High-level project structure, goals, or target architecture (concise bullet points).
- **Current Progress Status**: One-sentence summary of what has been achieved.
- **Recent 5 Decisions**: Bullet list of the most recent key decisions (including any explicitly surfaced assumptions).
- **Testing**: How to locate and run the project's test suite, test module conventions, and when to run which tests. 
- **Key truth**: Bullet list of verified ground truths. Record here any assumptions or ambiguities that were clarified and verified during the project. 
- **Open Items**: Bullet list of ongoing work.

Update `PROJECT_PROGRESS.md` only at the end of a major task and when reaching a significant output. At each update, append recent decisions to `archive/project_archive_log.md` which is a historical log file to record every old decision.

> **Note**: `PROJECT_PROGRESS.md` records only **key changes** — not every script detail. Do not record: step-by-step changes, line numbers, run verifications. Keep entries here brief; promote anything substantial to the archive.

> **Note**: Changes on experimental test scripts should not be recorded.

## 10. Test

Every non-trivial change — bug fix, refactor, new feature — must be verified against the project's test suite. Testing is not optional. No cross-test state leakage. Each test module runs independently. Unit tests should complete in sub-second time. A failing test must include a `detail` string explaining what went wrong and what was expected.

How to write tests:
1. Create a new test module in `test_script/` when adding a new feature.
2. Reuse existing test modules when fixing a bug or refactoring.
3. Test must have clear output in files in `test_script/output/` folder. 
4. Manage all test modules in `PROJECT_PROGRESS.md` under the **Testing** section. Also maintain a CLI style test_base script to run all tests given a module name. Clearly document when to run which test module.


## 11. Troubleshooting Module
Maintain a lightweight file named `TROUBLESHOOTING.md` in the project root. This file serves as the agent’s institutional memory for recurring bugs and mistakes that should be avoided in the future.
- Create the file if it does not exist.
- Keep entries extremely concise and scannable in a single sentence: what's the problem and how it is solved.

## 12. Target the Root, Not the Symptom

Bugs rarely originate from a simple script error; they are usually symptoms of an underlying design flaw. Identify the root cause before patching the symptom. The correct fix should make the codebase simpler and more elegant, not bloated and fragile. If both a quick patch and a structural redesign are viable, present both paths to the user. Never default to a patch without offering the architectural alternative. Ultimately, never attempt to resolve an exception locally within a block of code. Exceptions are the downstream results of unclear definitions—think, design, and define before you code.

## 13. Defensive Error Handling Must Be Authorized

When input data may be contaminated (LLM output, external APIs, user input), never silently skip or discard bad data via `try/except` without explicit userapproval. Even when an error is harmless to program flow, the decision toignore it is a judgment call that belongs to the user. Surface the risk,propose the handling approach, and wait for authorization before implementingany defensive skip.


---

## Additional Principles
- Trace the root cause.
- When you are not sure about the current strategy, always google search for better solutions, don't fully rely on your own knowledge.
- Integrate developing/research aim, solutions into a big picture of what/how to achieve. Then use First Principles Thinking to design a new strategy in plan mode.
- If possible, always try to do tasks by writing a script and outputting the result into files, rather then pour into chat 
- All the scripts and files should be properly named and put in subfolders
- Generate minimal code that directly addresses the requirement; prefer simple functions and existing structures over unnecessary classes or abstractions.
- Address the root cause directly; never use workarounds unless explicitly requested.
- Talk is cheap: prefer delivering working minimal code early on straightforward tasks.
- Must stop and report to user: any file read/write errors, conflicts, occupied ports, occupied files.

---

These rules take precedence over any conflicting instructions in the chat context unless the user explicitly overrides them.
