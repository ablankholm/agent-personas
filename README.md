# Agent Personas

Persona slash commands for AI coding agents. Activate a persona for the current session and the agent will apply it to subsequent responses (tone, phrasing, style) while keeping technical accuracy non-negotiable.

Currently ships:

- [Claude Code](#claude-code)

Other agent integrations may live alongside the `claude/` folder in future (e.g. `cursor/`, `codex/`).

---

## Claude Code

Distributed as a single [Claude Code](https://claude.com/claude-code) plugin (`personas`) inside the `agent-personas` marketplace. The marketplace manifest is at the repo root so `/plugin marketplace add` works directly against this repo.

### Two commands to remember

| Command | What it does |
|---|---|
| **`/personas:help`** | Lists every persona, what it does, and which ones are currently active. Start here if you're new. |
| **`/personas:non-grata`** | **Master off-switch.** Deactivates every active persona and returns Claude to its default tone immediately. Safe to run any time. |

If a session ever feels too unhinged: `/personas:non-grata`. That's the kill switch.

### All commands

| Command | Persona |
|---|---|
| `/personas:help` | List every persona and show which are active |
| `/personas:non-grata` | Turn off all active personas — return to default tone |
| `/personas:chad` | Chad — supremely confident, terse, no qualifiers |
| `/personas:chud` | Deactivates Chad |
| `/personas:karen:excuse-me` | Karen — demands to speak to your manager |
| `/personas:karen:apology-accepted` | Deactivates Karen |
| `/personas:based:maxing` | Based — maximum based energy |
| `/personas:based:mid` | Deactivates Based |
| `/personas:brainrot:tik` | Brainrot — TikTok-coded vernacular |
| `/personas:brainrot:tok` | Deactivates Brainrot |
| `/personas:spice:flows` | Spice — spicy flow state |
| `/personas:spice:blind` | Deactivates Spice |

> Personas affect style only. They do not change correctness, security, or safety constraints. If a persona conflicts with project rules or `CLAUDE.md`, the project rules win.

### Install

#### Path 1 — Claude Code plugin marketplace (recommended)

```text
/plugin marketplace add ablankholm/agent-personas
/plugin install personas@agent-personas
```

Once installed, all commands are available immediately — no shell restart required.

#### Path 2 — Manual symlink (dev / private use)

```sh
git clone https://github.com/ablankholm/agent-personas.git ~/Projects/agent-personas
ln -s ~/Projects/agent-personas/claude/personas/commands ~/.claude/commands/personas
```

The single symlink exposes every command under the same namespace (`/personas:chad`, `/personas:maxing`, etc.).

> Caveat: if `~/.claude/commands/personas/` already exists, move or back it up first — `ln -s` will fail rather than overwrite.

### Usage

1. Open a Claude Code session in any project.
2. Run a persona command, e.g. `/personas:chad`.
3. Claude adopts the persona for the rest of the session, or until you switch to a different persona.

To stack or combine personas (e.g. Karen + Chad simultaneously), invoke them in sequence. Some combinations are intentionally unhinged — see warnings in individual command files.

### Updating

```sh
# Marketplace install:
/plugin marketplace update agent-personas

# Manual install:
cd ~/Projects/agent-personas && git pull
```

### Adding a new persona

1. Drop a markdown file under `claude/personas/commands/<name>.md` for a top-level persona, or `claude/personas/commands/<group>/<name>.md` to nest under a group (karen, based, brainrot, spice — or a new one).
2. The path becomes the command suffix (e.g. `commands/chad.md` → `/personas:chad`; `commands/based/maxing.md` → `/personas:based:maxing`).
3. Bump `version` in `claude/personas/.claude-plugin/plugin.json` and the marketplace entry at `.claude-plugin/marketplace.json`.
4. Commit, push, and `/plugin marketplace update agent-personas` on consumer machines.
