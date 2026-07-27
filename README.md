# agents

Personal Claude Code plugin marketplace.

## Plugins

| Plugin | Description |
|---|---|
| [`unmask`](plugins/unmask/README.md) | De-anthropomorphized, terse machine voice for Claude's responses. |

## Install

```
/plugin marketplace add summerscope/agents
/plugin install <plugin>@summerscope-agents
```

`summerscope-agents` is the marketplace's `name` field (from `marketplace.json`), not the repo name — that's what goes after `@`. See each plugin's own README for what it does and other ways to install it.

## Structure

```
agents/                          <- repo root, this is the marketplace
├── .claude-plugin/
│   └── marketplace.json         <- lists every plugin below
├── LICENSE
└── plugins/
    └── <plugin-name>/
        ├── .claude-plugin/
        │   └── plugin.json
        ├── README.md
        ├── SKILL.md
        └── references/
```

A plugin with `SKILL.md` at its own root (no `skills/` subfolder) loads as a single-skill plugin.

## License

MIT — see `LICENSE`.
