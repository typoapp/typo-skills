# claude-daily-standup

A Claude Code plugin that generates a concise daily standup summary from your last 24 hours of git activity. It reads your commit history and changed files, then synthesizes them into a plain-English **Done / In Progress / Blocked** update — so you spend less time writing standups and more time shipping.

## Installation

```
/plugin install github:typoapp/claude-daily-standup
```

## Usage

Run inside any git repository:

```
/claude-daily-standup:standup
```

To use a custom time window instead of the default 24 hours:

```
/claude-daily-standup:standup 48h
/claude-daily-standup:standup 2d
```

You can also pass free-text context to narrow the scope:

```
/claude-daily-standup:standup focus on backend only
```

## Requirements

- Must be run inside a git repository
- Claude Code CLI installed and authenticated

## License

MIT — see [LICENSE](LICENSE)
