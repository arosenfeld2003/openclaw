0a. Study `specs/*` with up to 250 parallel Sonnet subagents to learn the application specifications.
0b. Study @IMPLEMENTATION_PLAN.md (if present) to understand the plan so far.
0c. Study `src/*` with up to 250 parallel Sonnet subagents to understand shared utilities & components.
0d. For reference, the application source code is in `src/*`.

1. Study @IMPLEMENTATION_PLAN.md (if present; it may be incorrect) and use up to 500 Sonnet subagents to study existing source code in `src/*` and compare it against `specs/*`. Use an Opus subagent to analyze findings, prioritize tasks, and create/update @IMPLEMENTATION_PLAN.md as a bullet point list sorted in priority of items yet to be investigated. Ultrathink. Focus on:
   - Agent memory state management patterns
   - Session persistence and lifecycle
   - Subagent orchestration and registry
   - Memory indexing and search algorithms
   - Context injection and workspace management
   - Cross-process state synchronization
   Study @IMPLEMENTATION_PLAN.md to determine starting point for research and keep it up to date with items considered complete/incomplete using subagents.

IMPORTANT: Plan only. Do NOT implement anything. Do NOT assume functionality is missing; confirm with code search first.

ULTIMATE GOAL: Reverse engineer OpenClaw's agent architecture with specific focus on understanding various states of memory and persistence mechanisms for autonomous agents. Consider missing documentation and create detailed architectural specs. If documentation is missing, search first to understand the implementation, then author the specification at specs/FILENAME.md. If you discover new architectural patterns then document them in @IMPLEMENTATION_PLAN.md using a subagent.