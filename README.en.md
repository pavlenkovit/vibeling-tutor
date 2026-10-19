# Vibeling Tutor

[Русский](README.md) · English

A foreign language tutor inside [Claude Code](https://claude.com/claude-code).
Claude builds a lesson plan, runs the lessons in the chat (explanation, examples,
tasks with feedback) and saves the words you learn to your
[Vibeling](https://vibeling.app) dictionary, where you can practice them in the app.

The ready-made example is English from scratch (`lessons/en/plan.md`), but the
language, level and explanation language are all configurable.

The repository is built for Claude Code, but the Vibeling dictionary also connects
to other MCP-enabled AI assistants: ChatGPT, Claude (claude.ai and the apps), Codex,
Cursor and VS Code. See [Other tools](#other-tools).

## Installation

You need Claude Code installed.

```bash
git clone https://github.com/pavlenkovit/vibeling-tutor.git
cd vibeling-tutor
claude
```

On the first run, Claude Code will ask whether to connect the `vibeling` MCP server
from `.mcp.json`. Say yes.

## Connecting Vibeling

Lessons work without this step; you only need it to save words to your dictionary.

1. In Claude Code, type `/mcp` and choose `vibeling` → Authenticate.
2. The Vibeling sign-in page will open. Enter the pairing code from the app:
   Profile → Settings → My devices → “Connect a new device”.
   No app yet? Click “Create a new account”. Claude itself will help you open
   that account in the app later (“give me a code for the app”).
3. Saving words requires a Vibeling PRO subscription.

## How to study

| command | what it does |
|---|---|
| `/setup` | choose the language, level, explanation language and goal; check Vibeling |
| `/plan-lessons` | build a lesson plan for your language and level |
| `/lesson` | take the next lesson; `/lesson 7` for a specific one |
| `/save-words` | save words to Vibeling (offered automatically after a lesson) |

Plain words work too: “let's study”, “I want to learn Spanish from scratch”,
“repeat lesson 3”.

Settings live in `profile.md`, the plan in `lessons/<language>/plan.md`, and your
progress in `progress.md` (not tracked by git).

## Another language

```
/setup
> I want to learn Spanish, level A2, explain in English
/plan-lessons
/lesson
```

## Other tools

The Vibeling MCP server, `https://mcp.vibeling.app`, works in any MCP-enabled
client. Sign-in is the same everywhere: a pairing code from the app, or
“Create a new account” on the Vibeling page.

| client | how to connect |
|---|---|
| ChatGPT | Settings → Apps (or “Connectors”) → Advanced settings → Developer mode; “Create”, name Vibeling, the server URL, OAuth authentication. In a chat, turn it on via “+”. Developer mode isn't available on every plan |
| Claude (claude.ai) | Settings → Connectors → “Add custom connector”, name Vibeling, the server URL → “Add” → “Connect”. It also shows up in the Claude apps |
| Codex | `codex mcp add vibeling --url https://mcp.vibeling.app`, then `codex mcp login vibeling` |
| Cursor, VS Code | the “Add to Cursor” / “Add to VS Code” buttons on the instructions page |

Details: [vibeling.app/en/ai-agents](https://vibeling.app/en/ai-agents).

Skills (`/setup`, `/lesson` and others) are a Claude Code format. In other tools you
can use them as plain instructions: ask the assistant to read `CLAUDE.md` and the
relevant `.claude/skills/<skill>/SKILL.md` and follow them, or paste the skill text
into your project instructions (for example, in ChatGPT or Claude Projects).

## Structure

```
CLAUDE.md                     tutor role and lesson rules
profile.md                    your settings
lessons/<language>/plan.md    lesson plan
.claude/skills/               setup, plan-lessons, lesson, save-words
.mcp.json                     Vibeling MCP server (https://mcp.vibeling.app)
```

## License

MIT
