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

Each plugin's `SKILL.md` sits at its own root, not under a nested `skills/` subfolder — that's enough for Claude Code to load it as a single-skill plugin.

## License

MIT — see `LICENSE`.
