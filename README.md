# Minimum OpenCode AGENTS System For Research

A lightweight AGENTS.md for reliable, transparent vibe coding/research in opencode for small-scale experimental projects. Karpathy/Linux/Hermes Hybrid.

## Overview

This system provides a structured yet simple method for AI agents to assist with coding and data work. It combines a clear set of coding guidelines with mechanisms to retain project memory across sessions. The aim is to support consistency, make the development process auditable, and allow for steady progress even when work spans multiple sessions or involves different people.

Inspired by principles from prominent developers and systems (Karpathy-style clarity, Linux robustness, Hermes adaptability), it enforces best practices that mitigate common pitfalls in AI-driven development such as assumption errors, hidden bugs, and loss of context between sessions.

## Strengths and Benefits

The framework focuses on several practical areas:

- **General Coding Guidance**: A complete and enforceable set of rules is provided in `coding_guide.md`. These address key practices such as making assumptions explicit, allowing errors to propagate for proper debugging rather than suppressing them, preserving backward compatibility, limiting changes to the smallest viable set, and establishing verifiable objectives before implementation begins.

- **Transparent Development**: Decisions, assumptions, and progress are documented explicitly. All code and outputs are produced by scripts that write results to files. This makes the entire process auditable and reproducible. The emphasis is on delivering working code and verifiable outputs rather than lengthy explanations alone.

- **Letting Errors Surface**: A deliberate choice is made to let errors occur and propagate instead of wrapping large sections of code in try/except blocks that provide fallbacks or silent recoveries. This approach is especially beneficial for research-focused projects for the following reasons:
1. Research code often explores new ideas, algorithms. Masking errors can hide important information about why something failed or produced incorrect results.
2. By seeing the actual exception or failure, developers can trace the exact point of breakdown, examine inputs and state at that moment, and address root causes directly. This mirrors the iterative, evidence-based nature of scientific inquiry.
3. It discourages "defensive" coding that assumes too much about what might go wrong.
4. In the long run, it builds more reliable code because problems are confronted by solving the root cause, rather than papered over.

**Cross-Session Memory System and Evolve**: A concise `PROJECT_PROGRESS.md` serves as the single source of truth for the current project status. Previous states are automatically preserved in `archive/project_archive_log.md`. This supports seamless handoff between sessions or contributors without losing important context. The `TROUBLESHOOTING.md` file captures knowledge about issues that have been encountered and resolved. The AI can be self-evolved by maintaining the memory of key truths, key decisions, key problem-solving. 


## How to use

Directly copy the AGENTS.md and coding_guide.md files to your project root folder. If needed, free to append your own project info (project introduction, structure, aim) to the AGENTS.md.

## Remind
For the long context session, LLM may forget about this guideline (like consistantly update the memory). In some long context cased, need to manually remind the AI to re-read the AGENTS.md or ask for update the memory.

## License

This guidance system is provided as an open methodology for the benefit of the development community. Feel free to adapt it to your projects while preserving attribution to the core principles.
