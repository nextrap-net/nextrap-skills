# Nextrap Skills

**English** | [简体中文](README.zh-CN.md)

Agent Skills for investigating public attack-request intelligence with [Nextrap](https://www.nextrap.net).

The **[nextrap-cli](skills/nextrap-cli/SKILL.md)** skill helps an AI agent start with an IP address, URL, or product name, choose the queries needed to answer your question, and explain the evidence returned by Nextrap CLI.

## Install

```bash
npx skills add nextrap-net/nextrap-skills --skill nextrap-cli
```

Choose your AI tool when prompted. Add `-g` to make the skill available across projects:

```bash
npx skills add nextrap-net/nextrap-skills --skill nextrap-cli -g
```

This installs the skill instructions, not the CLI program. Nextrap CLI must be installed separately and available as `nextrap-cli` on your PATH, or provided to the agent by its executable path.

## Get started

Check the CLI, authenticate, and view your account quota:

```bash
nextrap-cli --version
nextrap-cli auth set --api-key -
nextrap-cli status
```

Create an API key in your Nextrap account settings. The authentication command reads it from standard input; keep the key out of chat messages and command-line arguments.

Then ask your AI agent a question such as:

- “Investigate this source IP over the specified period and show a few representative requests.”
- “Which source IPs account for the most requests to this URL? Show request samples for one usable source.”
- “What requests were observed for this product, and how many distinct source IPs were involved?”
- “Show what happened before and after this log record. Read the full request only if the preview is insufficient.”

## Capabilities

- **IP investigation:** location and network information, activity within a time window, and request samples.
- **URL and product investigation:** matching requests, distinct-source counts, and request distributions.
- **Log analysis:** queryable fields, search, readable full requests, authorized decryption, and neighboring requests.
- **Account and updates:** authentication, remaining quota, and official CLI self-updates.

The skill selects relevant commands rather than running every command. It carries identifiers from the same log record into follow-up queries and distinguishes request counts, distinct-object counts, distribution buckets, and samples.

## Scope and interpretation

Queries cover public intelligence available to your account. Permissions, quota, masking, and truncation can limit what is returned. Aggregations may be approximate, and a sample is not the complete dataset.

An observed attack request does not prove a successful compromise. Decryption may consume quota; credential changes, decryption, and executable updates run only when authorized by your task.

## Skill layout

```text
skills/
└── nextrap-cli/
    ├── SKILL.md
    └── references/
```

Start with the [skill guide](skills/nextrap-cli/SKILL.md), or read a specific workflow:

- [Investigate a source IP](skills/nextrap-cli/references/workflow-ip-investigation.md)
- [Investigate a URL or product](skills/nextrap-cli/references/workflow-url-product-investigation.md)
- [Drill down from a distribution](skills/nextrap-cli/references/workflow-distribution-drilldown.md)

## Releases

[v1.0.0](https://github.com/nextrap-net/nextrap-skills/releases/tag/v1.0.0) is the initial skill release. The skill and CLI program are distributed separately.
