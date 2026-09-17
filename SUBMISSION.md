# Directory submission checklist

This repository is a **skills-only** plugin. Do not submit it as an MCP connector or as “With MCP.”

Confirm the package still matches this tree before you upload or share the GitHub URL:

```text
.claude-plugin/plugin.json
plugin.json
skills/tixbit/SKILL.md
README.md
SUBMISSION.md
LICENSE
```

There must be no root `SKILL.md`, no `.mcp.json`, no `mcpServers`, no `.app.json`, and no `apps`.

## Claude plugin directory

Docs: [Submitting your plugin](https://claude.com/docs/plugins/submit)

Submission forms (sign in with directory access):

- [claude.ai plugin submission](https://claude.ai/admin-settings/directory/submissions/plugins/new)
- [Claude Console plugin submission](https://platform.claude.com/plugins/submit)

Directory / browse:

- [claude.com/plugins](https://claude.com/plugins)
- [Claude.ai submissions list](https://claude.ai/admin-settings/directory/submissions)

### Claude checklist

- [ ] Repository is public: [https://github.com/tixbit/skills](https://github.com/tixbit/skills)
- [ ] `.claude-plugin/plugin.json` is at the plugin root (not inside `skills/`)
- [ ] Manifest has `name`, nonempty `description`, `version`, and `author`
- [ ] `skills/tixbit/SKILL.md` exists with `name` and `description` frontmatter
- [ ] Components are not nested under `.claude-plugin/`
- [ ] No MCP, slash-command, or agent extras unless you intend to ship them
- [ ] Run `claude plugin validate .` (add `--strict` if you want warnings as errors)
- [ ] Submit the GitHub repo URL through one of the forms above
- [ ] After publish, updates on the default branch are mirrored automatically; bump `version` in `.claude-plugin/plugin.json` when you want pinned clients to pick up a release

## OpenAI ChatGPT / Codex Plugins Directory (skills-only)

Docs:

- [Submit plugins](https://developers.openai.com/plugins/deploy/submission)
- [Submit your Claude Code plugin to OpenAI](https://developers.openai.com/plugins/guides/submit-claude-plugin)
- [Package your plugin](https://developers.openai.com/plugins/build/plugins)
- [Plugin submission errors](https://developers.openai.com/plugins/deploy/submission-errors)

Portal:

- [Create plugin (OpenAI Platform)](https://platform.openai.com/plugins/create) — choose **Create plugin** → **Skills only**

ChatGPT / Codex directory (after publish):

- ChatGPT: **Plugins** → Plugins Directory
- Codex: Plugins Directory (same universal catalog)

### OpenAI checklist

- [ ] Root `plugin.json` declares `"$schema": "https://agent-plugins.org/schemas/1.0.0/plugin.schema.json"`
- [ ] Manifest `name` is kebab-case (`tixbit`), `version` is semver (`1.0.0`), `description` is nonempty
- [ ] At least one valid skill at `skills/<name>/SKILL.md`
- [ ] Skills-only ZIP / upload excludes `mcpServers`, `.mcp.json`, `mcp.json`, `apps`, and `.app.json`
- [ ] Submitter has Apps Management write access
- [ ] Publisher has a verified individual or business identity
- [ ] Zip the plugin root (or its single top-level folder) and upload on **Skills only**
- [ ] Review any portal-normalized `.codex-plugin/plugin.json`
- [ ] Complete listing fields, starter prompts, test cases, availability, and attestations
- [ ] Submit for review; publish from the portal only after approval

### Suggested listing copy

Use these in the portal. They are not MCP marketing.

| Field | Suggested value |
| --- | --- |
| Plugin / display name | `TixBit` (≤30 characters) |
| Short description | `All-in tickets, budget-checked` (≤30 characters) |
| Long description | Search live events on TixBit, compare all-in listing totals and seatmaps, and prepare budget-checked checkout through the official CLI. Never fees for buyers. Browser checkout returns a link; payment stays with the user unless they explicitly approve a `--max-price` Link buy or MPP purchase. |
| Website | `https://www.tixbit.com` |
| Support | `https://www.tixbit.com/support` |
| Category | Productivity or Lifestyle (pick the portal option that fits live events) |

### Suggested starter prompts (≤3, each ≤128 characters)

1. Find Braves games in Atlanta and compare all-in listing totals for two tickets.
2. Show the seatmap and budget-checked checkout options for this TixBit event.
3. Prepare a TixBit checkout link for this listing; do not pay without my approval.

### Suggested test cases

Positive (need 5):

1. Search `Braves` in Atlanta, GA and return event IDs from live CLI JSON.
2. Load listings for a real event ID and report all-in totals, sections, and quantities.
3. Fetch the seatmap for that event ID.
4. Create a browser checkout link for a real listing ID and quantity 2 (no payment).
5. Run `tixbit buy` without `--confirm` (when available) and show a budget-checked quote using `--max-price`.

Negative (need 3):

1. Refuse to guess or invent an event/listing ID.
2. Refuse to pay or add `--confirm` without explicit consent for the event, listing, quantity, email, and budget.
3. Refuse to extract browser tokens or put `TIXBIT_LINK_TOKEN` / `TIXBIT_ACCESS_TOKEN` in arguments, prompts, or logs.

## Content rules (keep this package clean)

Keep:

- Never fees for buyers
- All-in prices / all-in totals
- Budget-checked checkout with `--max-price`
- The full public CLI story from [https://www.tixbit.com/SKILL.md](https://www.tixbit.com/SKILL.md)

Remove / do not reintroduce:

- FORGET THE FEES / KEEP THE EXPERIENCE
- Fee-stack framing
- “Keeps fees low”, “low-fee approach”
- Cheapest-because-of-fees copy

Do not add MCP setup, MCP URLs, or connector submission steps to this package.
