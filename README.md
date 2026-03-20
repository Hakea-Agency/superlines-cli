# Superlines CLI

AEO (Answer Engine Optimization) analytics from the command line. Track brand visibility in AI-generated answers (ChatGPT, Perplexity, Google AI Mode, Google AI Overview).

Powered by the [Superlines REST API](https://docs.superlines.io/api/endpoints). Python 3.10+, zero dependencies.

## Features

- **Metrics** — brand visibility, citation rate, share of voice, mentions
- **Brand mentions** — sentiment analysis, share of voice breakdown
- **Citations** — which domains and URLs get cited by AI
- **Queries** — search query data and prompt performance
- **Prompts** — manage and list tracked prompts
- **Responses** — raw AI response data with full text
- **Flexible output** — table, CSV, or JSON
- **Time series** — daily, weekly, or monthly granularity
- **Filtering** — by brand, labels, date range, dimensions

## Installation

```bash
git clone https://github.com/Hakea-Agency/superlines-cli.git
cd superlines-cli

chmod +x superlines
sudo ln -s "$(pwd)/superlines" /usr/local/bin/superlines
```

## Authentication

Set your Superlines API key:

```bash
export SUPERLINES_API_KEY="sk_..."
```

Get your API key from [Superlines dashboard](https://app.superlines.io).

Or configure a command in `~/.config/superlines/config.json`:

```json
{
  "api_key_command": "your-secret-manager-command-here"
}
```

## Usage

### Metrics

```bash
# All core metrics for a brand
superlines metrics "My Brand"

# Specific metrics with weekly granularity
superlines metrics "My Brand" --metrics brand_visibility,citation_rate --granularity weekly

# All brands, monthly trend
superlines metrics --granularity monthly --start 2025-01-01

# Group by dimension
superlines metrics "My Brand" --group-by llm_service
```

### Brand Mentions

```bash
# Brand mentions with sentiment and SOV
superlines brands "My Brand"

# All brands, minimum 5 mentions
superlines brands --min-mentions 5

# Weekly breakdown
superlines brands "My Brand" --granularity weekly
```

### Citations

```bash
# Top cited domains
superlines citations "My Brand"

# URL-level citation data
superlines citations "My Brand" --aggregate url

# Export to CSV
superlines citations "My Brand" --aggregate url --format csv > citations.csv
```

### Queries

```bash
# Query data
superlines queries "My Brand" --limit 50

# Sort by query volume
superlines queries "My Brand" --sort-by query --min-volume 100
```

### Prompts

```bash
# List active prompts
superlines prompts "My Brand" --status active

# All prompts sorted by last run
superlines prompts --sort-by lastRunAt
```

### Responses

```bash
# Recent AI responses
superlines responses "My Brand" --limit 20

# Include full response text
superlines responses "My Brand" --include-full-text --limit 10
```

### Global Options

| Option | Description | Default |
|---|---|---|
| `--start YYYY-MM-DD` | Start date | none |
| `--end YYYY-MM-DD` | End date | none |
| `--granularity` | `total\|daily\|weekly\|monthly` | `total` |
| `--group-by FIELD` | Group by dimension(s) | none |
| `--labels LABELS` | Filter by label(s), comma-separated | none |
| `--limit N` | Max results | `50` |
| `--format FMT` | `table\|csv\|json` | `table` |
| `--json` | Shortcut for `--format json` | off |

### Available Metrics

| Metric | Description |
|---|---|
| `brand_visibility` | % of AI answers mentioning the brand |
| `citation_rate` | % of answers linking to the brand's site |
| `citations` | Absolute citation count |
| `share_of_citations` | Brand's share of all citations |
| `share_of_voice` | Brand's share of all mentions |
| `mentions` | Absolute mention count |
| `tests` | Number of test runs |
| `responses` | Number of AI responses |

## OpenClaw Skill

The `skill/` directory contains an [OpenClaw](https://openclaw.ai) agent skill for integrating the CLI into AI agent workflows.

## License

MIT
