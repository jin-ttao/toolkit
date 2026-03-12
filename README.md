# toolkit

A collection of [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skills and tools.

## Skills

| Skill | Description | Requirements |
|-------|-------------|--------------|
| [tab-clean](./skills/tab-clean/) | AI-powered Chrome tab cleanup with interest tracking | macOS, Chrome |

## Install

**Option A: Skills CLI (recommended)**
```bash
npx skills add jin-ttao/toolkit --skill tab-clean
```

**Option B: Manual copy**
```bash
cp skills/tab-clean/SKILL.md .claude/commands/tab-clean.md
```

Then run in Claude Code: `/tab-clean`

## License

MIT
