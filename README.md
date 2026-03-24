# ssa-devteam marketplace

Claude Code plugin marketplace containing the `ssa-devteam` plugin.

## Installation

Add to your `~/.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "ssa-devteam": {
      "source": {
        "source": "github",
        "repo": "mderganc/ssa-devteam"
      }
    }
  },
  "enabledPlugins": {
    "ssa-devteam@ssa-devteam": true
  },
  "env": {
    "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1"
  }
}
```

Then restart Claude Code.

## Usage

```
/ssa-devteam Add user authentication with OAuth2
```

See [plugins/ssa-devteam/README.md](plugins/ssa-devteam/README.md) for full documentation.
