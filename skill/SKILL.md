---
name: superlines
description: >
  Superlines AEO analytics CLI — brand visibility, citation rate, share of
  voice, sentiment, and query data in AI-generated answers. Use when analyzing
  AI search visibility, checking brand performance in ChatGPT/Perplexity/Gemini.
---

# Superlines AEO Analytics CLI

Superlines data via REST API. Tracks brand visibility in AI answers.

## CLI

```bash
superlines <command> [brand] [options]
```

## Commands

```bash
# Core metrics (visibility, citation rate, SOV)
superlines metrics "My Brand"
superlines metrics "My Brand" --granularity weekly --start 2025-01-01

# Brand mentions + sentiment
superlines brands "My Brand"
superlines brands --min-mentions 5

# Citations (which domains/URLs get cited)
superlines citations "My Brand" --aggregate url

# Query data
superlines queries "My Brand" --limit 50

# Tracked prompts
superlines prompts "My Brand" --status active

# Raw AI responses
superlines responses "My Brand" --include-full-text --limit 10
```

## Global Options

- `--start YYYY-MM-DD` — Start date
- `--end YYYY-MM-DD` — End date
- `--granularity` — total | daily | weekly | monthly
- `--group-by FIELD` — Group by dimension(s)
- `--labels LABELS` — Filter by label(s)
- `--limit N` — Max results (default: 50)
- `--format` — table | csv | json
- `--json` — Shortcut for --format json

## Available Metrics

`brand_visibility`, `citation_rate`, `citations`, `share_of_citations`,
`share_of_voice`, `mentions`, `tests`, `responses`

## Authentication

Set `SUPERLINES_API_KEY` env var, or configure in `~/.config/superlines/config.json`:

```json
{
  "api_key_command": "your-command-to-get-key"
}
```

## Typical AEO Analysis

```bash
# 1. Overview
superlines metrics "My Brand" --granularity weekly

# 2. Competitor landscape
superlines brands --min-mentions 3

# 3. Citation sources
superlines citations "My Brand" --aggregate url

# 4. Query insights
superlines queries "My Brand" --limit 50

# 5. Export for reporting
superlines metrics "My Brand" --granularity monthly --format csv > metrics.csv
```
