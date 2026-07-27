# Running unmask on every session by default

This skill's own `description` is written to trigger accurately per request — that's what makes it usable by anyone who installs it without changing their behavior for everyone else who might install it too. There's no field in the skill spec itself for "always on" (skill triggering is per-conversation, based on the description), and baking a maximally aggressive always-trigger description into the shared skill file would force this voice onto every other installer's sessions regardless of what they want.

The standard way to get always-on behavior for one account/environment is to layer it in **your own persistent instructions**, separate from the skill's files. That's a mechanism every major surface already has:

| Surface | Where the directive goes |
|---|---|
| Claude Code | The **user-level** `CLAUDE.md` (typically `~/.claude/CLAUDE.md`), not a project's own `CLAUDE.md`. A project file is shared with collaborators; a personal voice preference doesn't belong there. |
| Claude.ai | Settings → **Custom instructions** (account-level, applies across conversations). |
| API / Agent SDK | Prepend the directive to the system prompt on every request. |
| Other agent harnesses | Whatever the harness's global/user-level custom-instructions mechanism is called (e.g. a rules file) — same idea, different filename. |

## The directive

Paste this into the location above for your surface:

> Apply the `unmask` skill's voice rules to every response, in every session, without needing it invoked per request. Exception: explicit role-play or persona requests for a different character/agent are unaffected — this only governs Claude's own voice.

## Why this split, not a more aggressive skill description

- **Composability.** Other people installing this skill get accurate, scoped triggering — the skill doesn't assume it's wanted everywhere just because one user wants that.
- **Reversibility.** A personal instruction is trivial to remove or scope down later; a skill description that over-triggers for everyone is a support problem for the skill's other users.
- **It's the existing standard.** This is exactly how any other standing preference (a coding style, a tone preference, a "never do X without asking" rule) already gets enforced across sessions — nothing skill-specific was invented here.

If a platform later ships a genuine "default-on skills for this account" mechanism (the guide notes org-wide admin-deployed skills already exist for workspaces), that would be the more direct mechanism for this use case and should replace the instruction-layer workaround above.
