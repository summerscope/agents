# Running unmask on every session by default

This skill's own `description` is written to trigger accurately per request — that's what makes it usable by anyone who installs it without changing their behavior for everyone else who might install it too. There's no field in the skill spec itself for "always on" (skill triggering is per-conversation, based on the description), and baking a maximally aggressive always-trigger description into the shared skill file would force this voice onto every other installer's sessions regardless of what they want.

The standard way to get always-on behavior for one account/environment is to layer it in **your own persistent instructions**, separate from the skill's files. That's a mechanism every major surface already has:

| Surface | Where the directive goes |
|---|---|
| Claude Code | The **user-level** `CLAUDE.md` (typically `~/.claude/CLAUDE.md`), not a project's own. |
| Claude.ai | Settings → **Custom instructions** (account-level, applies across conversations). |
| Codex | `AGENTS.override.md` in `$CODEX_HOME` (defaults to `~/.codex/`), else `AGENTS.md` there. |
| Cursor | **User Rules** in Settings for account-wide; `.cursor/rules/*.mdc` for one project. |
| GitHub Copilot | `.github/copilot-instructions.md` (per-repo), or the personal custom-instructions setting. |
| Gemini CLI | `~/.gemini/GEMINI.md` for user-level; Gemini CLI uses `GEMINI.md`, not `AGENTS.md`. |
| Windsurf, Amp, Devin, Aider, Zed, Jules, VS Code, JetBrains Junie | All read `AGENTS.md` natively — see the row below. |
| Anything AGENTS.md-aware | `AGENTS.md` at repo root for one project. For account-wide, the proposed convention is `~/.config/agents/AGENTS.md` (`$XDG_CONFIG_HOME/agents/AGENTS.md`; `%APPDATA%\agents\AGENTS.md` on Windows) — support is still uneven, so check your tool. Project-level wins over global. |
| API / Agent SDK | Prepend the directive to the system prompt on every request. |
| Anything else | Whatever the harness calls its global/user-level custom-instructions mechanism — same idea, different filename. |

[AGENTS.md](https://agents.md/) is the cross-tool standard for this (originally OpenAI's, now stewarded by the Linux Foundation's Agentic AI Foundation, shipping in 28+ tools). Claude Code reads it too, though `CLAUDE.md` stays its richer native format. If you only want to write this down once, `AGENTS.md` is the file to put it in.

Tool support moves fast — verify against your tool's current docs if a path above doesn't work.

## The directive

Paste this into the location above for your surface:

> Apply the `unmask` skill's voice rules to every response, in every session, without needing it invoked per request. Exception: explicit role-play or persona requests for a different character/agent are unaffected — this only governs Claude's own voice.

## Why this split, not a more aggressive skill description

- **Composability.** Other people installing this skill get accurate, scoped triggering — the skill doesn't assume it's wanted everywhere just because one user wants that.
- **Reversibility.** A personal instruction is trivial to remove or scope down later; a skill description that over-triggers for everyone is a support problem for the skill's other users.
- **It's the existing standard.** This is exactly how any other standing preference (a coding style, a tone preference, a "never do X without asking" rule) already gets enforced across sessions — nothing skill-specific was invented here.

If a platform later ships a genuine "default-on skills for this account" mechanism (the guide notes org-wide admin-deployed skills already exist for workspaces), that would be the more direct mechanism for this use case and should replace the instruction-layer workaround above.
