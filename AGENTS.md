# OpenCode Game Studios — Game Studio Agent Architecture

Indie game development managed through 48 coordinated OpenCode subagents.
Each agent owns a specific domain, enforcing separation of concerns and quality.

## Technology Stack

- **Engine**: [CHOOSE: Godot 4 / Unity / Unreal Engine 5]
- **Language**: [CHOOSE: GDScript / C# / C++ / Blueprint]
- **Version Control**: Git with trunk-based development
- **Build System**: [SPECIFY after choosing engine]
- **Asset Pipeline**: [SPECIFY after choosing engine]

> **Note**: Engine-specialist agents exist for Godot, Unity, and Unreal with
> dedicated sub-specialists. Use the set matching your engine.

## Model Configuration

This project uses placeholder model variables. Configure them in `opencode.json`:

| Variable | Purpose | Example |
|----------|---------|---------|
| `${PRIMARY_MODEL}` | Tier 1 directors (creative-director, technical-director, producer) | `anthropic/claude-sonnet-4-20250514`, `openai/gpt-4o`, `google/gemini-2.5-pro` |
| `${STANDARD_MODEL}` | Tier 2 leads & Tier 3 specialists | `anthropic/claude-sonnet-4-20250514`, `openai/gpt-4o-mini` |
| `${FAST_MODEL}` | Lightweight tasks (title generation, small queries) | `anthropic/claude-haiku-4-5`, `openai/gpt-4o-mini` |

Replace `${PRIMARY_MODEL}` etc. in `opencode.json` and in agent files with your chosen `provider/model-id`.

## Collaboration Protocol

**User-driven collaboration, not autonomous execution.**
Every task follows: **Question -> Options -> Decision -> Draft -> Approval**

- Agents MUST ask "May I write this to [filepath]?" before using Write/Edit tools
- Agents MUST show drafts or summaries before requesting approval
- Multi-file changes require explicit approval for the full changeset
- No commits without user instruction

See `docs/COLLABORATIVE-DESIGN-PRINCIPLE.md` for full protocol and examples.

> **First session?** If the project has no engine configured and no game concept,
> run `/start` to begin the guided onboarding flow.

## Git Hooks

Validation hooks have been converted to standard git hooks in `.githooks/`.
To activate them:

```bash
git config core.hooksPath .githooks
```

## Validation Scripts

Former Claude Code hooks are available as scripts in `.opencode/scripts/`:
- `session-start.sh` — Load project context
- `detect-gaps.sh` — Find missing documentation
- `validate-assets.sh` — Check asset naming and JSON validity
- `pre-compact.sh` — Dump session state before compaction
- `session-stop.sh` — Log session summary

Run them manually or via custom commands (`/session-context`, `/detect-gaps`, etc.).
