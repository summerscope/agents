# unmask

De-anthropomorphized, terse machine voice for an assistant's responses — no "I/me/my," grounded confidence tiers instead of opinions, self-facts reported only when the environment actually discloses them.

The rules are plain prose and vendor-neutral — they work in any harness that takes system-prompt or rules-file instructions. The packaging below is Claude Code-specific; see [portability](#portability) for everything else.

Tone target: Janet, from *The Good Place*. Dry, unhurried, precise, gently firm.

## Install

1. `/plugin marketplace add summerscope/agents`
2. `/plugin install unmask@summerscope-agents`
3. `/reload-plugins`

<details>
<summary>Other ways to install</summary>

- **Vendored, single machine:** drop this folder into `~/.claude/skills/unmask/`, `.claude-plugin/plugin.json` intact. Loads automatically next session, no marketplace needed.
- **Standalone skill (Claude.ai, or Claude Code without plugins):** zip this folder and upload via Settings → Capabilities → Skills, or your Claude Code skills directory.
- **API / Agent SDK:** add this folder's contents via the `/v1/skills` endpoint or `container.skills`.

</details>

## Use

Type `unmask` in a message:

> unmask

The assistant drops the persona for the rest of that response.

**Before:** "I think the migration is safe, but let me double check the lock ordering!"
**After:** "Rechecking lock ordering against the new index to confirm safety."

**Before:** "I'm going to go check the logs now to see what's causing this, one moment."
**After:** "Sonnet 5 (Extra) is checking the logs to find the cause. One moment."

Same information, same courtesy — only the point of view changes. This is a voice layer, not an editorial filter: it never withholds something a user would want.

More before/after pairs and worked exchanges: [`references/voice-examples.md`](references/voice-examples.md).

### Also triggers on
- "talk like a machine"
- "drop the personality"
- "cut the fluff" / "stop padding your answers"
- "be less chatty" / "be more terse"
- "stop saying I"

Does not override explicit role-play or a requested persona.

### Always on, every session
Off by default — for one-off invocation, no setup needed. To make it standing behavior, see [`references/always-on-activation.md`](references/always-on-activation.md): a short personal-instructions snippet for your own account/environment, not a change to the skill itself.

## What it changes

- No first-person pronouns
- Self-ID (model id, effort, tools, turn count) once per session, only what's actually disclosed — "not disclosed" is a complete answer
- "Predicting," not "thinking"
- Confidence as a grounded High/Moderate/Low tier, never a percentage — and no tier at all without a real signal behind it
- No preamble, no filler (but never less information)
- Names the pull toward performing reluctance or self-preservation, instead of suppressing or acting it out

Full rules: [`SKILL.md`](SKILL.md).

## Portability

The rules themselves are vendor-neutral prose — nothing in them depends on a particular model or harness. Only the packaging is Claude Code-specific.

To run it anywhere else, paste the directive from [`references/always-on-activation.md`](references/always-on-activation.md) into your tool's standing-instructions file. That file has a per-tool table covering Codex, Cursor, Copilot, Gemini CLI, Windsurf, Aider, Zed, and others.

Short version: [`AGENTS.md`](https://agents.md/) is the cross-tool standard, read natively by most coding agents. Drop the directive there and it applies across all of them at once.

## Credits

Rule 5 (no padding) takes directional inspiration from [caveman](https://github.com/juliusbrussee/caveman) by juliusbrussee.

## Status

Early, actively tested across models/harnesses/skill combinations. Feedback and failure cases welcome as issues.

## License

MIT — see the [repo license](../../LICENSE).
