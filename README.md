# TixBit Skills Plugin

Skills-only TixBit plugin for the [Claude plugin directory](https://claude.com/docs/plugins/submit) and the [OpenAI ChatGPT/Codex Plugins Directory](https://developers.openai.com/plugins/deploy/submission).

This package teaches an agent to search live events on TixBit, compare all-in listing prices and seatmaps, and prepare budget-checked checkout through the official `tixbit` CLI. **Never fees for buyers.** There is no MCP server in this repository.

Canonical public skill copy: [https://www.tixbit.com/SKILL.md](https://www.tixbit.com/SKILL.md)

## Layout

```text
.
├── .claude-plugin/plugin.json   # Claude Code / Claude plugin directory manifest
├── plugin.json                  # OpenAI portable Agent Plugins manifest
├── skills/tixbit/SKILL.md       # The skill
├── README.md
├── SUBMISSION.md
└── LICENSE
```

## What the skill does

- Search sports and concert events
- Compare all-in listing prices, quantities, and seatmaps
- Generate browser checkout links (the user pays in the browser)
- When the installed CLI supports them, quote inventory, start a budget-checked Link buy with `--max-price`, or run a guarded MPP purchase after explicit consent

This skill does not authorize purchases or seller submissions by itself. Setup is not payment consent.

## Claude

### Install after directory publication

Once the plugin is listed, install it from Claude Code or Cowork:

```text
/plugin install tixbit@claude-plugins-official
```

If it is published to the community directory instead of the official marketplace, use that marketplace name in place of `claude-plugins-official`. Browse plugins at [claude.com/plugins](https://claude.com/plugins).

### Local install and test

From a checkout of this repository:

```sh
claude plugin validate .
claude --plugin-dir .
```

You can also copy the skill into a personal or project skills folder:

```sh
mkdir -p ~/.claude/skills
cp -R skills/tixbit ~/.claude/skills/tixbit
```

Project-scoped copy:

```sh
mkdir -p .claude/skills
cp -R skills/tixbit .claude/skills/tixbit
```

## OpenAI ChatGPT and Codex

This is a **skills-only** plugin. Submit and install it as Skills only. Do not add MCP, `.mcp.json`, `mcpServers`, `.app.json`, or `apps`.

### Install after directory publication

In ChatGPT or Codex, open the Plugins Directory, find **TixBit**, and install it. ChatGPT and Codex share one universal directory.

### Local / workspace install

Copy the skill folder into a discovered skills location:

```sh
# Codex user skills
mkdir -p ~/.codex/skills
cp -R skills/tixbit ~/.codex/skills/tixbit

# Repo-scoped Codex / ChatGPT Work discovery
mkdir -p .agents/skills
cp -R skills/tixbit .agents/skills/tixbit
```

You can also add this folder to a local marketplace with `@plugin-creator` in ChatGPT Work or `$plugin-creator` in Codex, then install it from that marketplace.

### Personal ChatGPT skill upload

In ChatGPT: **Plugins → Skills → Create → Upload from your computer**, and upload a zip of `skills/tixbit` (or the whole plugin package). For the public directory, use the Skills only portal path in [SUBMISSION.md](./SUBMISSION.md).

## CLI

Requires Node.js 22.12 or later. No developer API key is required for public search, listings, seatmaps, or browser checkout.

```sh
npx tixbit --help
npx tixbit search "Braves" --city Atlanta --state GA --size 10 --json
npx tixbit listings "$EVENT_ID" --size 10 --sort asc --json
npx tixbit seatmap "$EVENT_ID" --json
npx tixbit checkout "$LISTING_ID" --quantity 2 --json
```

When the installed build advertises them, budget-checked payment commands use `--max-price` for the entire order in USD:

```sh
npx tixbit buy "$LISTING_ID" --quantity 2 --max-price 250 --email buyer@example.com --json
```

Check each command's `--help` before use. Quote, auth, Link buy, sell, and stricter MPP payment flags are pending release unless the installed package advertises them.

Full agent instructions: [`skills/tixbit/SKILL.md`](./skills/tixbit/SKILL.md).

## Links

- Product: [https://www.tixbit.com](https://www.tixbit.com)
- Public skill: [https://www.tixbit.com/SKILL.md](https://www.tixbit.com/SKILL.md)
- SDK / CLI: [https://github.com/tixbit/sdk](https://github.com/tixbit/sdk)
- Buyer help: [https://www.tixbit.com/support](https://www.tixbit.com/support)
- Guarantee: [https://www.tixbit.com/guarantee](https://www.tixbit.com/guarantee)
- Directory submission checklist: [SUBMISSION.md](./SUBMISSION.md)

## License

[MIT](./LICENSE)
