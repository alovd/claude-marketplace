# Claude Marketplace

Skills, agents, and MCP tools for the team.

## Setup (one time)

```bash
/plugin marketplace add alovd/claude-marketplace
/plugin install design-auditor@alovd-marketplace
```

## Available Plugins

| Plugin             | Description                                    | Install                                            |
| ------------------ | ---------------------------------------------- | -------------------------------------------------- |
| **design-auditor** | Audit UI designs against 17 professional rules | `/plugin install design-auditor@alovd-marketplace` |

## Repo structure

```
claude-marketplace/
├── .claude-plugin/
│   └── marketplace.json       ← registry + plugin definitions
└── skills/
    ├── design-auditor/        ← each skill is a folder with SKILL.md
    │   ├── SKILL.md
    │   └── references/
    ├── next-skill/            ← just add a folder + marketplace entry
    └── ...
```

## Adding a new skill

1. Create `skills/<name>/SKILL.md`
2. Add `"./skills/<name>"` to the plugin's `skills` array in `marketplace.json`
3. Push — team gets it on next update
