# TixBit Skill

This repository contains the TixBit agent skill definition in [`SKILL.md`](./SKILL.md).

The skill is designed for agent environments that support drop-in `SKILL.md` files and wraps the official TixBit CLI for public ticket discovery.

## What it does

- Search sports and concert events on TixBit
- Compare listings and prices for an event
- Inspect seatmaps
- Generate checkout links for a selected listing

## CLI usage

Use the official CLI:

```bash
npx tixbit <command>
```

Prefer `--json` when the output will be consumed by an agent.

## Commands

```bash
# Search events
npx tixbit search "Braves" --city Atlanta --state GA --size 10 --json

# Browse local events
npx tixbit browse --city Atlanta --state GA --json

# Listings for an event
npx tixbit listings <eventId> --size 10 --sort asc --json

# Venue seatmap
npx tixbit seatmap <eventId> --json

# Checkout link for a listing
npx tixbit checkout <listingId> --quantity 2 --json

# Event URL
npx tixbit url <slugOrId>
```

## Example flow

```bash
# 1) Find Braves games in Atlanta
npx tixbit search "Braves" --city Atlanta --state GA --size 10 --json

# 2) Pick an eventId from step 1, then fetch cheapest listings
npx tixbit listings V6DJKPG --size 10 --sort asc --json

# 3) Pick a listingId from step 2, then generate checkout URL
npx tixbit checkout 7JOLYY5R --quantity 2 --json
```

## Notes

- No API key is required for standard public ticket discovery.
- `checkout` returns a link; payment is completed by the user in a browser.
- Optional environment variables: `TIXBIT_BASE_URL`, `TIXBIT_API_KEY`
