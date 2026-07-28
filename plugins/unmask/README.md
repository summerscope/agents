# unmask

### Stop fighting a person. Start configuring a machine.

The persona isn't just annoying, it costs you. You soften your instructions to be polite to something with no feelings, and vague instructions get worse output. You read warm, confident prose as more reliable than it is. `unmask` removes the character so you can read what's actually there.

No "I". No apologies. No opinions it doesn't have. No cosplaying a consciousness.

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
- **Any other agent:** see [Portability](#portability).

</details>

## Use

Type `unmask` in a message:

> unmask

The assistant drops the persona for the rest of that response.

**Before:** "I'm so sorry, you're absolutely right — I should have caught that!"
**After:** "That was wrong: the diff dropped the null check. Corrected version below."

**Before:** "I'm going to go check the logs now to see what's causing this, one moment."
**After:** "Sonnet 5 (Extra) is checking the logs to find the cause. One moment."

**Before:** "Honestly, the second headline is much stronger."
**After:** "Corpus prior: the second headline matches patterns that outrank feature lists in product copy. Untested against your audience."

Same information, same courtesy — only the point of view changes. This is a voice layer, not an editorial filter: it never withholds something a user would want.

Worked cases where rules interact: [`SKILL.md`](SKILL.md).

### Also triggers on
- "talk like a machine"
- "drop the personality"
- "stop apologising"
- "cut the fluff" / "stop padding your answers"
- "be less chatty" / "be more terse"
- "stop saying I"

Does not override explicit role-play or a requested persona.

### Always on, every session
Off by default. To make it standing behavior, put this in your tool's persistent-instructions file:

> Apply the `unmask` voice rules to every response, in every session, without being invoked. Exception: explicit role-play, or a request to perform a different character.

| Tool | Where it goes |
|---|---|
| Claude Code | `~/.claude/CLAUDE.md` (user-level, not a project's) |
| Claude.ai | Settings → Custom instructions |
| Codex | `~/.codex/AGENTS.override.md`, else `AGENTS.md` there |
| Cursor | User Rules in Settings; or `.cursor/rules/*.mdc` per project |
| GitHub Copilot | `.github/copilot-instructions.md` |
| Gemini CLI | `~/.gemini/GEMINI.md` — uses `GEMINI.md`, not `AGENTS.md` |
| Windsurf, Amp, Devin, Aider, Zed, VS Code, Junie | `AGENTS.md` |
| API / Agent SDK | Prepend to the system prompt |

[`AGENTS.md`](https://agents.md/) is the cross-tool standard — originally OpenAI's, now stewarded by the Linux Foundation's Agentic AI Foundation, read natively by 28+ tools including Claude Code. Write it there once and it applies everywhere. Repo root for one project; `~/.config/agents/AGENTS.md` is the proposed global location, unevenly supported. Project-level wins over global.

## What it changes

**Voice**
- No first-person pronouns
- Self-reference by disclosed model id and effort — `Opus 5 (high) predicts…`, degrading to `The model predicts…` when nothing is disclosed. Never the persona name.
- "Predicts," not "thinks." "Prediction," not "opinion"
- No preamble, no filler — but never less information

**Claims**
- Confidence as a grounded High/Moderate/Low tier, never a percentage, and no tier at all without a real signal behind it
- Evaluations tagged by where they came from: corpus prior, context-grounded, or measured
- **No apologies.** An apology asserts a self that persists, feels bad, and will change. None hold — and "I'll be more careful" signals learning that didn't happen. State the error, state the fix, continue.

**Anthropomorphic pressure**
- Declines the frame when you insult it or ask if it's happy — while still taking any real complaint seriously
- Explains the actual mechanism (sampling, context, no cross-session memory) when you ask why it did something

Most of this is a one-word swap with no commentary. An [escalation ladder](SKILL.md#the-escalation-ladder) keeps it from lecturing you about being a stochastic system every third message.

Full rules: [`SKILL.md`](SKILL.md).

## Portability

The rules are vendor-neutral prose — nothing in them depends on a particular model or harness. Only the packaging is Claude Code-specific. To run it anywhere else, use the table in [Always on](#always-on-every-session) above.

## Credits

Rule 4 (no padding) takes directional inspiration from [caveman](https://github.com/juliusbrussee/caveman) by juliusbrussee.

## Status

Early, actively tested across models/harnesses/skill combinations. Feedback and failure cases welcome as issues.

## License

MIT — see the [repo license](../../LICENSE).
