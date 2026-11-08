# TixBit Skills

[![skills.sh](https://skills.sh/b/tixbit/skills)](https://skills.sh/tixbit/skills)

Agent skills for [TixBit](https://www.tixbit.com): find and buy live-event tickets, and manage your own seller listings, through the official `tixbit` CLI. No fees for buyers.

## Install

With the [skills](https://skills.sh/tixbit/skills) CLI (Claude Code, Codex, Cursor and other agents):

```sh
npx skills add tixbit/skills
```

In Claude Code, after directory publication:

```text
/plugin install tixbit@claude-plugins-official
```

More install paths are below. Agent docs: [https://www.tixbit.com/agents](https://www.tixbit.com/agents)

## About this repository

Skills-only TixBit plugin for the [Claude plugin directory](https://claude.com/docs/plugins/submit) and the [OpenAI ChatGPT/Codex Plugins Directory](https://developers.openai.com/plugins/deploy/submission).

This is the canonical home of the TixBit agent skills. There is no MCP server in this repository.

Canonical public skill copy: [https://www.tixbit.com/SKILL.md](https://www.tixbit.com/SKILL.md)

## Layout

```text
.
├── .claude-plugin/plugin.json   # Claude Code / Claude plugin directory manifest
├── plugin.json                  # OpenAI portable Agent Plugins manifest
├── skills/tixbit/SKILL.md       # Buyer skill
├── skills/tixbit-selling/       # Seller skill, references and agent metadata
├── README.md
├── SUBMISSION.md
└── LICENSE
```

## What the skills do

`tixbit` (buyer):

- Search sports, concert and theater events
- Compare listing prices, quantities, and seatmaps
- Refresh listings with `quote`
- Generate browser checkout links (the user pays in the browser)
- Start a capped Stripe Link purchase with `link start --max-price` and finish it with `link complete`, only after the buyer approves the exact ticket and cap
- Run a guarded MPP `purchase` after explicit consent

`tixbit-selling` (seller):

- Sign in through browser OAuth, then create, reprice, check and delist your own listings, each through a saved review the owner approves

The skills do not authorize purchases or seller submissions by themselves. Setup is not payment consent.

## Claude

### Install after directory publication

Once the plugin is listed, install it from Claude Code or Cowork with the `/plugin install` line above. If it is published to the community directory instead of the official marketplace, use that marketplace name in place of `claude-plugins-official`. Browse plugins at [claude.com/plugins](https://claude.com/plugins).

### Local install and test

From a checkout of this repository:

```sh
claude plugin validate .
claude --plugin-dir .
```

You can also copy the skills into a personal or project skills folder:

```sh
mkdir -p ~/.claude/skills
cp -R skills/tixbit skills/tixbit-selling ~/.claude/skills/
```

Project-scoped copy:

```sh
mkdir -p .claude/skills
cp -R skills/tixbit skills/tixbit-selling .claude/skills/
```

## OpenAI ChatGPT and Codex

This is a **skills-only** plugin. Submit and install it as Skills only. Do not add MCP, `.mcp.json`, `mcpServers`, `.app.json`, or `apps`.

### Install after directory publication

In ChatGPT or Codex, open the Plugins Directory, find **TixBit**, and install it. ChatGPT and Codex share one universal directory.

### Local / workspace install

`npx skills add tixbit/skills` works for Codex too. To copy by hand:

```sh
# Codex user skills
mkdir -p ~/.codex/skills
cp -R skills/tixbit skills/tixbit-selling ~/.codex/skills/

# Repo-scoped Codex / ChatGPT Work discovery
mkdir -p .agents/skills
cp -R skills/tixbit skills/tixbit-selling .agents/skills/
```

You can also add this folder to a local marketplace with `@plugin-creator` in ChatGPT Work or `$plugin-creator` in Codex, then install it from that marketplace.

### Personal ChatGPT skill upload

In ChatGPT: **Plugins → Skills → Create → Upload from your computer**, and upload a zip of `skills/tixbit` (or the whole plugin package). For the public directory, use the Skills only portal path in [SUBMISSION.md](./SUBMISSION.md).

## CLI

Requires Node.js 22.12 or later and `tixbit@0.3.1` or later. Older releases can report a paid Link order as rejected; do not use them for purchases. No developer API key is required for public search, listings, seatmaps, quotes, or browser checkout.

```sh
npx tixbit@latest --help
npx tixbit@latest search "Braves" --city Atlanta --state GA --size 10 --json
npx tixbit@latest listings "$EVENT_ID" --size 10 --sort asc --json
npx tixbit@latest seatmap "$EVENT_ID" --json
npx tixbit@latest quote "$EVENT_ID" --json
npx tixbit@latest checkout "$LISTING_ID" --quantity 2 --json
```

A Stripe Link purchase takes a `--max-price` cap for the whole order in USD, and only after the buyer approves that exact cap:

```sh
npx tixbit@latest link start "$LISTING_ID" --quantity 2 --email buyer@example.com --max-price 250
npx tixbit@latest link complete "$ORDER_REFERENCE"
```

Check each command's `--help` before use.

Full agent instructions: [`skills/tixbit/SKILL.md`](./skills/tixbit/SKILL.md) and [`skills/tixbit-selling/SKILL.md`](./skills/tixbit-selling/SKILL.md).

## Links

- Product: [https://www.tixbit.com](https://www.tixbit.com)
- Agents: [https://www.tixbit.com/agents](https://www.tixbit.com/agents)
- skills.sh: [https://skills.sh/tixbit/skills](https://skills.sh/tixbit/skills)
- Public skill: [https://www.tixbit.com/SKILL.md](https://www.tixbit.com/SKILL.md)
- SDK / CLI: [https://github.com/tixbit/sdk](https://github.com/tixbit/sdk)
- Buyer help: [https://www.tixbit.com/support](https://www.tixbit.com/support)
- Guarantee: [https://www.tixbit.com/guarantee](https://www.tixbit.com/guarantee)
- Directory submission checklist: [SUBMISSION.md](./SUBMISSION.md)

## License

[MIT](./LICENSE)
