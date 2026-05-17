# typo-skills

A collection of Claude Code plugins built by [Typo](https://github.com/typoapp). Install any plugin individually or browse the collection to find skills that fit your workflow.

## Plugins

| Plugin | Description | Install |
|--------|-------------|---------|
| [daily-standup](plugins/daily-standup/) | Generate a daily standup summary from the last 24 hours of git activity | `/plugin install github:typoapp/typo-skills?path=plugins/daily-standup` |
| [code-optimise](plugins/code-optimise/) | Optimise unstaged hand-written code for clarity and performance without changing behaviour | `/plugin install github:typoapp/typo-skills?path=plugins/code-optimise` |

## Usage

Each plugin is independently installable. Navigate to a plugin's directory for its own README and usage instructions.

**Quick example — daily standup:**

```
/plugin install github:typoapp/typo-skills?path=plugins/daily-standup
/claude-daily-standup:standup
/claude-daily-standup:standup 48h
```

## Contributing

Each plugin lives in `plugins/<name>/` and follows the standard Claude Code plugin layout:

```
plugins/<name>/
├── .claude-plugin/
│   └── plugin.json
└── skills/
    └── <skill-name>/
        └── SKILL.md
```

## License

MIT — see [LICENSE](LICENSE)
