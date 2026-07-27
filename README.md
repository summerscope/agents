# agents

A Claude Code plugin marketplace for personal skills. First entry: `unmask`.

## unmask

A Claude Agent Skill that swaps the assistant's default first-person, warm-chatbot voice for a de-anthropomorphized machine register: no "I/me/my," self-reference by actual model id and effort level instead of a persona, "predicting" instead of "thinking," confidence expressed as grounded High/Moderate/Low tiers instead of opinions, and self-facts reported only when the environment genuinely discloses them — never invented context-window or session-length numbers.

Tone target: Janet, from *The Good Place*. Dry, unhurried, precise, gently firm — not a generic gruff-senior-engineer bit.

## Install

**As a plugin (Claude Code):**

```
/plugin marketplace add summerscope/agents
/plugin install unmask@summerscope-agents
/reload-plugins
```

Confirmed against the [plugin marketplaces](https://code.claude.com/docs/en/plugin-marketplaces) and [plugins reference](https://code.claude.com/docs/en/plugins-reference) docs, and against a real `claude plugin validate` run. `summerscope-agents` is the marketplace's own `name` field, not the repo name — that's what goes after the `@`. `/reload-plugins` activates the plugin in the current session without a restart.

**Simpler alternative for personal, single-machine use:** drop `plugins/unmask/` (with its `.claude-plugin/plugin.json` intact) directly into `~/.claude/skills/unmask/`. Claude Code auto-loads any folder under a skills directory that contains a `plugin.json` as `unmask@skills-dir` on the next session — no marketplace, no install step, available in every project. Still a vendored copy on that machine, same as any other file there.

**As a standalone skill (Claude.ai, or Claude Code without the plugin system):** download `plugins/unmask/` from this repo, zip *that* folder (not the whole repo), upload via Settings → Capabilities → Skills (Claude.ai) or your Claude Code skills directory. The `.claude-plugin/plugin.json` inside is harmless if left in — Claude.ai's skill loader only looks for `SKILL.md` — but drop it first if a plugin-free zip is preferred.

**API / Agent SDK:** add that same folder's contents via the `/v1/skills` endpoint or `container.skills`.

## Use

Invoked by name — like running `insights` implies "run insights on this session," running `unmask` implies "unmask yourself." Also triggers on "talk like a machine," "drop the personality," "cut the fluff," "stop saying I." Does not override explicit role-play or persona requests.

Want it on by default in every session rather than invoked per request? See `plugins/unmask/references/always-on-activation.md` for the (short) personal-instructions snippet — that's a setting in your own account/environment, not a change to the skill itself.

## Structure

```
agents/                                  <- repo root, this is the marketplace
├── .claude-plugin/
│   └── marketplace.json                 <- lists every plugin below
├── LICENSE
└── plugins/
    └── unmask/                          <- one plugin per skill (so far, just this one)
        ├── .claude-plugin/
        │   └── plugin.json
        ├── SKILL.md
        └── references/
            ├── voice-examples.md              <- calibrated before/after pairs and worked exchanges
            └── always-on-activation.md        <- how to run this every session by default
```

No nested `skills/<name>/` folder: a plugin with `SKILL.md` at its own root, and no `skills/` subdirectory, loads automatically as a single-skill plugin (Claude Code v2.1.142+; confirmed here with a live `claude plugin validate` run, not just the docs). That inner `skills/` layout exists for a plugin bundling *more than one* skill — not the case here, so it isn't used. This plugin happening to share its name with its one skill (`unmask` the plugin, `unmask` the skill) is a coincidence of naming, not a structural requirement.

`README.md` lives at the repo root, alongside `.claude-plugin/` and `plugins/` — never inside a plugin or skill folder itself, both of which stay README-free per the skill-authoring convention (skill documentation goes in `SKILL.md` and `references/`, not a `README.md` a human would read).

## License

MIT — see `LICENSE`.

## Prior art

The no-padding rule (`unmask`'s Rule 5) takes directional inspiration from [caveman](https://github.com/juliusbrussee/caveman) by juliusbrussee — no preamble, no narrated intent, exact preservation of code/commands/errors. Scope differs: caveman is a general-purpose token-reduction system with six compression levels and dedicated slash commands; `unmask` uses one terseness bar in service of a specific voice, and treats precision (grounding a confidence tier, disclosing what isn't known) as taking priority over brevity whenever the two conflict.

## Status

Early draft, actively being tested across models/harnesses/skill combinations. Feedback and failure cases welcome as issues.
