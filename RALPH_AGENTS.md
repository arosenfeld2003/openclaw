## Project Goal

Reverse engineer OpenClaw's agent architecture with specific focus on understanding various states of memory and persistence mechanisms for autonomous agents.

## Tech Stack

- **Language**: TypeScript (ESM)
- **Runtime**: Node.js 22+
- **Build System**: pnpm/bun with vitest
- **Database**: SQLite (for vector embeddings and memory index)
- **Platforms**: CLI, macOS app, iOS app, Android app
- **Messaging**: Discord, Telegram, Slack, Signal, iMessage, WhatsApp (web)
- **Framework**: Custom agent runtime based on pi-mono

## Build & Run

- **Install Dependencies**: `pnpm install` (or `bun install`)
- **Build**: `pnpm build` (TypeScript compilation + checks)
- **Run CLI**: `pnpm openclaw` or `pnpm dev`
- **Format**: `pnpm format:fix` (oxfmt)

## Validation

- **Tests**: `pnpm test` (vitest)
- **Coverage**: `pnpm test:coverage`
- **Typecheck**: `pnpm tsgo`
- **Lint**: `pnpm check` (oxlint + oxfmt)

## Operational Notes

### Agent Architecture Summary

OpenClaw implements a sophisticated multi-layer agent architecture with:

1. **Session Management**: JSONL-based session persistence in `~/.openclaw/agents/<agentId>/sessions/`
2. **Memory System**: Multi-tier memory with file-based storage and SQLite vector indexing
3. **Subagent Registry**: Complex orchestration of child agents with lifecycle management
4. **Workspace Context**: Agent-specific workspaces with AGENTS.md, SOUL.md, MEMORY.md
5. **Configuration Scoping**: Per-agent configuration overrides and isolated state

### Key Memory States

- **Session State**: Conversation history, token counts, routing metadata
- **Memory Files**: Daily logs, topical memory, long-term curated memory
- **Vector Index**: SQLite-backed embedding cache with hybrid search
- **Subagent State**: Registry of running agents with lifecycle tracking
- **Configuration State**: Agent-specific settings and workspace paths

### Codebase Patterns

- Agent code primarily in `src/agents/`
- Session management in `src/agents/pi-embedded-runner/`
- Memory system in `src/memory/` and `src/agents/tools/memory-tool.ts`
- Messaging channels in `src/` subdirs and `extensions/`
- Configuration in `src/config/` and `src/agents/agent-scope.ts`