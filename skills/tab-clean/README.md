# tab-clean

AI-powered Chrome tab cleanup for [Claude Code](https://docs.anthropic.com/en/docs/claude-code).

> Not just a tab manager — it tracks your **interest signals** from browser behavior.

## What it does

1. **Reads** all Chrome tabs across all windows
2. **Classifies** each tab: KEEP / SAVE / CLOSE
3. **Discusses context** with you per group ("why did you have these open?")
4. **Saves** important tabs with context to a markdown file
5. **Extracts interest signals** from your Google searches
6. **Closes** confirmed tabs via AppleScript

## Example output

```
Tab cleanup complete:
- KEEP: 6 tabs kept
- SAVE: 21 tabs → saved to tabs-2026-03-11.md, then closed
- CLOSE: 9 tabs closed
- Interest Signals: 4 search queries captured
```

Saved file (`tabs-2026-03-11.md`):
```markdown
## Interest Signals (from Google searches)
- **harness engineering** — AI agent era engineering org practices
- **context engineering** — effective context design for AI agents

## Saved Tabs

### Tech Articles (5)
- [Anthropic: Effective context engineering](https://...) — AI agent context design guide
- [OpenAI: Harness engineering](https://...) — Codex usage in agent-first world
...
```

## Requirements

- **macOS** (uses AppleScript via `osascript`)
- **Google Chrome**
- **Claude Code**

## Install

```bash
# Copy the skill file to your project
cp tab-clean.md .claude/commands/tab-clean.md
```

Then run in Claude Code:
```
/tab-clean
```

## Customize

Open `.claude/commands/tab-clean.md` and edit:

- **KEEP domains** — Add sites you always want to keep open (e.g., `github.com/{username}`)
- **Save path** — Change `./tabs-{date}.md` to your preferred location (e.g., `inbox/tabs-{date}.md`)
- **Interest Signal topics** — Adjust which search categories are tracked

## How it works

```
Chrome tabs (all windows)
       │
       ▼
  ┌─────────┐
  │ Collect  │  osascript reads title + URL
  └────┬─────┘
       ▼
  ┌─────────┐
  │Classify  │  KEEP (hardcoded domains) / SAVE / CLOSE (AI judgment)
  └────┬─────┘
       ▼
  ┌─────────┐
  │ Discuss  │  Groups similar tabs, asks "why did you have these open?"
  └────┬─────┘
       ▼
  ┌─────────┐
  │ Confirm  │  Shows final classification, waits for approval
  └────┬─────┘
       ▼
  ┌─────────┐
  │ Execute  │  Saves to .md → closes tabs (reverse index order, all windows)
  └─────────┘
```

## Limitations

- macOS only (AppleScript dependency)
- Google Chrome only (no Firefox/Safari/Arc support)
- Requires Claude Code to run the skill
