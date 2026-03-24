# ssa-devteam marketplace

Claude Code plugin marketplace containing the `ssa-devteam` plugin.

## Installation

### CLI (recommended)

```bash
# Add the marketplace
claude plugin marketplace add mderganc/ssa-devteam

# Install the plugin
claude plugin install ssa-devteam@ssa-devteam
```

Then enable agent teams by adding to `~/.claude/settings.json`:
```json
{
  "env": {
    "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1"
  }
}
```

Restart Claude Code.

### Manual (settings.json)

Add all three blocks to `~/.claude/settings.json`:

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

Restart Claude Code.

## Usage

```
/ssa-devteam Add user authentication with OAuth2
```

See [plugins/ssa-devteam/README.md](plugins/ssa-devteam/README.md) for full documentation.
