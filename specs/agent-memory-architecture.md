# Agent Memory Architecture

## Overview

OpenClaw's agent memory system implements a sophisticated multi-tier architecture that manages agent state, conversation history, and long-term knowledge across multiple persistence layers.

## Requirements

### Core Memory Tiers

1. **Session Memory** (Short-term)
   - Conversation history within a session
   - Token count tracking and budget enforcement
   - Session-specific context and state
   - Auto-reset based on policies (daily, idle, manual)

2. **Working Memory** (Medium-term)
   - Daily append-only logs (`memory/YYYY-MM-DD.md`)
   - Topical memory files (`memory/<topic>.md`)
   - Recent context retrieval
   - Temporal decay for relevance

3. **Long-term Memory** (Persistent)
   - Curated knowledge in `MEMORY.md`
   - Vector-indexed for semantic search
   - SQLite-backed embedding storage
   - Hybrid search (BM25 + vector similarity)

### State Persistence Layers

1. **File System**
   ```
   ~/.openclaw/agents/<agentId>/
   ├── sessions/
   │   ├── sessions.json                    # Registry
   │   ├── <SessionId>.jsonl               # Transcripts
   │   └── <SessionId>-topic-<threadId>.jsonl
   └── <workspace>/
       ├── MEMORY.md                        # Long-term
       └── memory/
           ├── YYYY-MM-DD.md               # Daily logs
           └── <topic>.md                  # Topical
   ```

2. **SQLite Database**
   - Embedding cache with provider/model keys
   - File and chunk indexing
   - Vector similarity search support
   - Batch processing for large corpora

3. **In-Memory Caches**
   - Active session state
   - Subagent registry
   - Recent embeddings
   - Configuration overrides

## Memory Operations

### Write Paths

1. **Session Updates**
   - Append to JSONL transcript
   - Update session metadata
   - Increment token counts
   - Maintain routing information

2. **Memory Persistence**
   - Daily log appends (atomic writes)
   - Topical memory updates
   - Long-term memory curation
   - Vector index updates

### Read Paths

1. **Context Loading**
   - Bootstrap file injection
   - Recent memory retrieval
   - Semantic search over indexed content
   - MMR re-ranking for diversity

2. **Session Restoration**
   - Load session metadata
   - Reconstruct conversation history
   - Apply token budget limits
   - Restore agent configuration

## Lifecycle Management

### Session Lifecycle

1. **Creation**
   - Generate unique session key
   - Initialize metadata
   - Set reset policies
   - Configure token budgets

2. **Active Use**
   - Append messages to transcript
   - Update token counts
   - Maintain topic threads
   - Handle attachments

3. **Reset/Archive**
   - Policy-based resets (4 AM daily default)
   - Idle timeout triggers
   - Manual reset commands
   - Archive to cold storage

### Memory Maintenance

1. **Indexing**
   - Incremental chunk updates
   - Embedding generation
   - Cache management
   - Garbage collection

2. **Compaction**
   - Prune old daily logs
   - Consolidate topical memory
   - Update long-term memory
   - Optimize vector index

## Acceptance Criteria

### Functional Requirements

- [ ] Sessions persist across gateway restarts
- [ ] Memory search returns relevant context
- [ ] Token budgets are enforced accurately
- [ ] Session resets follow configured policies
- [ ] Vector search performs within 100ms for typical queries
- [ ] Memory files are atomic and crash-safe

### Performance Requirements

- [ ] Session load time < 50ms
- [ ] Memory indexing < 1s for 1000 chunks
- [ ] Vector search < 100ms for 10k embeddings
- [ ] Session write latency < 10ms
- [ ] Memory compaction runs without blocking

### Reliability Requirements

- [ ] No data loss on process crash
- [ ] Graceful degradation without vector index
- [ ] Automatic orphan cleanup
- [ ] Cross-process state consistency
- [ ] Idempotent memory operations

## Implementation Notes

### Key Design Decisions

1. **JSONL for Sessions**: Append-only format ensures crash safety
2. **SQLite for Vectors**: Local, embedded, no external dependencies
3. **File-based Memory**: Human-readable, version-controllable
4. **Hybrid Search**: Combines keyword and semantic matching
5. **Per-Agent Isolation**: Security and multi-tenancy support

### Extension Points

1. **Memory Providers**: Pluggable backends (QMD, custom)
2. **Embedding Models**: Support multiple providers (OpenAI, Gemini, local)
3. **Search Algorithms**: Configurable ranking and re-ranking
4. **Reset Policies**: Custom triggers and schedules
5. **Archive Strategies**: Cold storage and compression options