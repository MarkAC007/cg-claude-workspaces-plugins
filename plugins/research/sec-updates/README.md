# SEC Updates Plugin

Aggregate security news from tldrsec, Krebs on Security, Schneier, The Hacker News, and other sources into ranked updates across three categories: Breaches & Incidents, Security Research, and Security Ideas. Maximum 32 items per run, ordered by impact and recency.

## Commands

| Command | Description |
|---------|-------------|
| `/sec-updates:update` | Fetch and rank the latest security news from all sources |

## Prerequisites

No external API keys required. Uses public web sources.

## Install

```bash
claude plugin add ~/GitHub/cg-claude-workspaces-plugins/plugins/research/sec-updates
```
