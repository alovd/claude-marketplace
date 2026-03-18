# Claude Marketplace

Skills, agents, and MCP tools for the team.

## Setup (one time)

```bash
/plugin marketplace add alovd/claude-marketplace
```

## Available Plugins

| Plugin             | Description                                    | Install                                            |
| ------------------ | ---------------------------------------------- | -------------------------------------------------- |
| **design-auditor** | Audit UI designs against 17 professional rules | `/plugin install design-auditor@alovd-marketplace` |

## Usage

After adding the marketplace, install any plugin:

```bash
/plugin install design-auditor@alovd-marketplace
```

Plugins update automatically when new versions are pushed.

## Repo structure

```
claude-marketplace/
├── .claude-plugin/
│   └── marketplace.json       ← registry (team subscribes to this)
└── plugins/
    ├── design-auditor/        ← each plugin is a folder
    │   ├── .claude-plugin/
    │   │   └── plugin.json
    │   └── .claude/
    │       └── skills/...
    ├── next-plugin/           ← just add a folder + marketplace entry
    └── ...
```

## Adding a new plugin

1. Create `plugins/<name>/` with `.claude-plugin/plugin.json` and skill/agent/MCP files
2. Add an entry to `.claude-plugin/marketplace.json`
3. Push — team gets it on next update
