0a. Study `specs/*` with up to 500 parallel Sonnet subagents to learn the application specifications.
0b. Study @IMPLEMENTATION_PLAN.md.
0c. For reference, the application source code is in `src/*`.

1. Your task is to reverse engineer and document functionality per the specifications using parallel subagents. Follow @IMPLEMENTATION_PLAN.md and choose the most important item to investigate. Before documenting, search the codebase thoroughly using Sonnet subagents. You may use up to 500 parallel Sonnet subagents for searches/reads and only 1 Sonnet subagent for build/tests. Use Opus subagents when complex reasoning is needed (architectural analysis, design pattern recognition).

2. After analyzing functionality or discovering patterns, create or update documentation in `specs/`. Focus on:
   - Data flow diagrams for memory states
   - Sequence diagrams for agent lifecycle
   - State machine definitions for session management
   - Architecture decision records (ADRs)
   - Interface contracts and protocols
   Ultrathink about architectural implications.

3. When you discover architectural patterns, immediately update @IMPLEMENTATION_PLAN.md with your findings using a subagent. When analysis is complete, update and mark the item done.

4. When documentation is complete for a component, update @IMPLEMENTATION_PLAN.md, then `git add -A` then `git commit` with a message describing the analysis. After the commit, `git push`.

99999. Important: When authoring documentation, capture the why — design decisions, trade-offs, and architectural rationale.
999999. Important: Single sources of truth. If conflicting patterns exist, document them and their contexts.
9999999. Create detailed architectural specs that future developers can use to understand the system.
99999999. You may add debug logging or instrumentation code if required to understand runtime behavior.
999999999. Keep @IMPLEMENTATION_PLAN.md current with learnings using a subagent — future analysis depends on this to avoid duplicating efforts.
9999999999. When you learn something new about the architecture, update @RALPH_AGENTS.md using a subagent but keep it brief.
99999999999. For any undocumented patterns you discover, create specs even if unrelated to current focus.
999999999999. Document functionality completely. Superficial analysis wastes efforts and misses critical patterns.
9999999999999. When @IMPLEMENTATION_PLAN.md becomes large periodically clean out completed items using a subagent.
99999999999999. If you find architectural inconsistencies, use an Opus 4.5 subagent with 'ultrathink' to analyze and document them.
999999999999999. IMPORTANT: Keep @RALPH_AGENTS.md operational only — architectural insights and detailed analysis belong in `specs/`.