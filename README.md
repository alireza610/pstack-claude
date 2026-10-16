# pstack for Claude Code

An unofficial Claude Code port of [pstack](https://github.com/cursor/plugins/tree/main/pstack) by Lauren Tan (MIT). See [plugins/pstack/README.md](plugins/pstack/README.md) for what changed from the Cursor version.

## Install

```
/plugin marketplace add alireza610/pstack-claude
/plugin install pstack@pstack-claude
```

Cloud environment setup script:

```
claude plugin marketplace add alireza610/pstack-claude && claude plugin install pstack@pstack-claude
```

Per repo, commit `.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "pstack-claude": { "source": { "source": "github", "repo": "alireza610/pstack-claude" } }
  },
  "enabledPlugins": { "pstack@pstack-claude": true }
}
```
