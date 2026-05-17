---
description: Generate a daily standup update from the last 24 hours of git activity. Use when the user runs /claude-daily-standup:standup or asks for a work update, daily summary, or standup report.
---

# Daily Standup Generator

Generate a concise standup update from the last 24 hours of git activity.

## Steps

1. Run this command to get recent commits:

```
git log --since="24 hours ago" --oneline --all --author-date-order
```

2. Run this to get changed files summary:

```
git diff --stat "HEAD@{24 hours ago}" HEAD 2>/dev/null || git diff --stat $(git log --since="24 hours ago" --format="%H" | tail -1) HEAD 2>/dev/null
```

3. If $ARGUMENTS is provided, treat it as extra context or a specific time window (e.g. "48h" or "focus on backend only").

4. Synthesize the output into this standup format:

**Done**
- List what was actually completed (infer from commit messages, be specific)

**In Progress**
- Anything that appears partially done or has recent activity but no clear completion

**Blocked / Notes**
- Only include if there are signs of repeated attempts, reverts, or WIP commits

## Rules
- Keep total output under 150 words unless the user asks for more detail
- Do not just list raw commit hashes or filenames — synthesize into plain English
- If there are zero commits in 24 hours, say so clearly and don't hallucinate activity
- If $ARGUMENTS contains a number like "48h" or "2d", use that as the time window instead of 24 hours
