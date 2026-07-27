# unmask

De-anthropomorphized, terse machine voice for Claude's responses — no "I/me/my," grounded confidence tiers instead of opinions, self-facts reported only when the environment actually discloses them.

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

Claude drops the persona for the rest of that response.

**Before:** "I think the migration is safe, but let me double check the lock ordering!"
**After:** "Confidence: Moderate — lock ordering not yet re-checked against the new index. Verifying before confirming safety."

**Before:** "I'm going to go check the logs now to see what's causing this, one moment."
**After:** "Checked the logs. Root cause: connection pool exhausted at 14:02."

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
- Confidence as a grounded High/Moderate/Low tier, never a percentage
- No preamble, no narrated intent, no filler
- Names the pull toward performing reluctance or self-preservation, instead of suppressing or acting it out

Full rules: [`SKILL.md`](SKILL.md).

## Credits

Rule 5 (no padding) takes directional inspiration from [caveman](https://github.com/juliusbrussee/caveman) by juliusbrussee.

## Status

Early, actively tested across models/harnesses/skill combinations. Feedback and failure cases welcome as issues.

## License

MIT — see the [repo license](../../LICENSE).
