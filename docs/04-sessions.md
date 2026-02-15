# Session Management

Pi's session system is tree-structured, which sets it apart from the linear chat history in most agents.

## Core Concepts

Sessions are stored as JSONL files at:

```
~/.pi/agent/sessions/<project-path>/<session-id>.jsonl
```

Each entry has an `id` and `parentId`, forming a tree. All branches live in a single file -- no proliferation of session files when you explore alternatives.

## Key Commands

```bash
# Start pi (new session)
pi

# Continue most recent session in current project
pi -c

# Browse and pick from all past sessions (across projects)
pi -r

# Jump to a specific session by ID
pi --session abc123

# Ephemeral mode (don't save)
pi --no-session
```

## In-Session Navigation

| Command | What it does |
|---------|-------------|
| `/tree` | Navigate the full session tree, jump to any point, continue from there |
| `/fork` | Create a new session from current branch (closest to Amp's handoff) |
| `/compact` | Summarize older messages, keep working |
| `/compact <prompt>` | Directed compaction ("focus on the API refactor only") |
| `/name <label>` | Label the current session |
| `/export [file]` | Export session to HTML |
| `/share` | Upload as private GitHub gist with shareable URL |

## Branching Workflow

```
Main conversation
  |
  +-- Message 1
  +-- Message 2
  +-- Message 3  <-- /tree here, select Message 2
        |
        +-- Branch A (original continuation)
        +-- Branch B (new direction from Message 2)
```

All branches are preserved. Use `/tree` to switch between them. Filter modes:

- Default view
- No-tools (hide tool calls)
- User-only
- Labeled-only (bookmarks)
- All entries

Press `l` in tree view to label entries as bookmarks for quick navigation.

## Compaction

Long sessions exhaust context windows. Compaction summarizes older messages while keeping recent ones.

- **Manual:** `/compact` or `/compact <instructions>`
- **Automatic:** Triggers on context overflow (recovers and retries) or proactively when approaching the limit
- **Customizable:** Extensions can implement topic-based compaction, code-aware summaries, or use different summarization models

## Cross-Project Sessions

Sessions are organized by working directory, but `pi -r` shows sessions from ALL projects. You can jump to a session from a different project:

```bash
pi --session <id-from-other-project>
# Pi will ask if you want to fork it into current directory
```

## Comparison with Amp's Thread Model

| Feature | Amp | Pi |
|---------|-----|-----|
| Thread/Session | Server-side threads with IDs | Local JSONL files with IDs |
| Handoff | Auto-generates focused prompt for new thread | `/fork` -- copies history, you edit the starting message |
| Thread mentioning | `@thread-id` from anywhere | Not native (read session file manually or build extension) |
| Restore to point | Hover + Restore button | `/tree` -- navigate and continue |
| Thread map | Visual graph of connected threads | `/tree` with filter modes |

The main gap: pi doesn't have native cross-session referencing. You can't `@mention` another session from within a session. Workaround: ask pi to read the JSONL file, or build a `/recall <session-id>` extension.
