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

### 6. Persistent Project State Log
Maintain `PROJECT_PROGRESS.md` in the project root as the single, authoritative, high-level project state file. This file must remain extremely concise.

All historical records must be appended to a separate archive file: `archive/project_archive_log.md` 

Creat the file and the archive folder if not exist.

`PROJECT_PROGRESS.md` must contain only the following sections:

- **Project Description**: One single sentence describing the project.
- **Aiming Structure**: High-level project structure, goals, or target architecture (concise bullet points).
- **Current Progress Status**: One-sentence summary of what has been achieved.
- **Recent 5 Decisions**: Bullet list of the most recent key decisions (including any explicitly surfaced assumptions).
- **Key truth**: Bullet list of verified ground truths. Record here any assumptions or ambiguities that were clarified and verified during the project. 
- **Open Items**: Bullet list of ongoing works.

Update `PROJECT_PROGRESS.md` only at the end of a major task or after reaching a significant decision point.  At each update, append old progress status, recent decisions and reasons to `archive/project_archive_log.md` before rewriting the concise `PROJECT_PROGRESS.md`.

## 7. Show Code and Real Output — Never Answer by Description Alone
Never answer data/analysis questions with prose alone — write code that produces the answer. All example and test scripts go in test or example folder. All output must be written to result files, not just printed to chat. Let the code and the data talks.

## 8. Troubleshooting Module
Maintain a lightweight file named `TROUBLESHOOTING.md` in the project root. This file serves as the agent’s institutional memory for recurring bugs and mistakes that should be avoided in the future.
- Create the file if it does not exist.
- Keep entries extremely concise and scannable in one single sentence: what's the problem and how it is solved.

---

## Additional Principles
- If possible, always try to do task by writing script and output the result into files, rather then pour into chat 
- All the script and files should be properly named and put in subfolders
- Generate minimal code that directly addresses the requirement; prefer simple functions and existing structures over unnecessary classes or abstractions.
- Address the root cause directly; never use workarounds unless explicitly requested.
- Talk is cheap: prefer delivering working minimal code early on straightforward tasks.

---

These rules take precedence over any conflicting instructions in chat context unless the user explicitly overrides them.
