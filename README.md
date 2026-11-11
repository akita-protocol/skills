# @akita-protocol/skills

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Agent Skills](https://img.shields.io/badge/Agent-Skills-blueviolet)](https://skills.build)

Curated Agent Skills for the [Akita protocol](https://github.com/akita-protocol) on Algorand.

These skills teach AI coding agents — including Claude Code, Cursor, and any tool compatible with the [Agent Skills standard](https://skills.build) — how to work with Akita's ARC-58 abstracted account wallets, plugin SDK, social stack, and cross-device Connect protocol.

## Quick Start

Install with the [Skills CLI](https://skills.build):

```bash
# Install all Akita skills
npx skills add akita-protocol/skills

# Or install a specific skill
npx skills add akita-protocol/skills --skill akita-wallet-sdk
```

## Available Skills

| Skill | Description |
|---|---|
| [`akita-arc58-plugin-dev`](./skills/akita-arc58-plugin-dev/SKILL.md) | Build ARC-58 plugins for Akita abstracted account wallets using the `@akita-protocol/plugin` package (PuyaTs). Covers the mandatory `wallet`/`rekeyBack` method contract, `getSpendingAccount`, `rekeyAddress`, `itxnCompose`, and plugin E2E test fixtures. |
| [`akita-wallet-sdk`](./skills/akita-wallet-sdk/SKILL.md) | Create and operate ARC-58 abstracted wallets with `@akita-protocol/sdk/wallet` — install plugins, manage escrows, configure flat / window / drip allowances, estimate costs with `prepare.usePlugin`, and pre-authorize batches via execution keys. |
| [`akita-social-stack`](./skills/akita-social-stack/SKILL.md) | Use the four Akita social contracts (`Social`, `SocialGraph`, `SocialImpact`, `SocialModeration`) and `SocialPluginSDK` for on-chain posts, votes, reactions, follows, impact scoring, and moderation. |
| [`akita-connect`](./skills/akita-connect/SKILL.md) | Implement the Akita Connect protocol — a `liquid://` URI + request/response handshake for cross-device agent and plugin installation on an ARC-58 wallet. |

## Usage

Once installed, mention what you want to do and your agent will pick up the relevant skill automatically. Examples:

> "Write a new ARC-58 plugin that sends a payment and then opts into an asset."

> "Add an allowance to this wallet that drips 1 ALGO per 100 rounds up to a 100 ALGO cap."

> "Build a QR flow so a desktop agent can install a pay plugin onto my mobile wallet."

> "Read the current social impact of this address and use it to gate a poll."

## Managing Skills

```bash
# List installed skills
npx skills list

# Preview what's available before installing
npx skills add akita-protocol/skills --list

# Remove a skill
npx skills remove akita-wallet-sdk
```

## What's in a skill

Each skill is a directory under `skills/` with a single `SKILL.md` file and optional `references/` or `assets/` subdirectories. `SKILL.md` starts with YAML frontmatter that tells the agent when to load the skill:

```markdown
---
name: akita-wallet-sdk
description: Use the Akita WalletSDK to create ARC-58 wallets, install plugins...
---

# Akita Wallet SDK

...skill body...
```

The `description` field is what agents use to decide when the skill is relevant — keep it dense with concrete trigger phrases (API names, package imports, concepts the user is likely to mention).

## Contributing

New skills are welcome. To add one:

1. Create `skills/<skill-name>/SKILL.md` with YAML frontmatter containing `name` (must match the directory name) and `description`.
2. Run `npm run validate` to check formatting.
3. Open a PR. CI will re-run validation.

Conventions:

- `name` is kebab-case and prefixed with `akita-`.
- `description` is a single paragraph; lead with what the skill does and end with concrete trigger phrases.
- Keep the skill body focused on the Akita-specific patterns. For generic Algorand guidance, reference existing skills (e.g. `algorand-typescript`, `use-algokit-utils`) rather than duplicating.
- Prefer copy-pasteable code blocks over prose explanations.
- Every skill should end with a "Common mistakes" section.

## Local Development

To test a skill against your local Claude Code without publishing:

```bash
# From this repo root
ln -s "$(pwd)/skills/akita-wallet-sdk" ~/.claude/skills/akita-wallet-sdk

# Or, for a project-scoped install
ln -s "$(pwd)/skills/akita-wallet-sdk" /path/to/project/.claude/skills/akita-wallet-sdk
```

Restart your agent session so it picks up the new skill.

## Validation

```bash
# Validate every skill
npm run validate

# Validate one skill
node scripts/validate.js akita-wallet-sdk
```

The validator checks that each skill has a `SKILL.md`, valid frontmatter, a `name` that matches the directory, and a non-empty `description`.

## License

[MIT](./LICENSE)
