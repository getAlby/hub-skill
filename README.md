# Alby Hub Skill

An agent skill that teaches Claude how to use [`@getalby/hub-cli`](https://github.com/getAlby/hub-cli) to manage an [Alby Hub](https://github.com/getAlby/hub) self-custodial lightning node.

## Installation

### 🚀 Install with single command

```bash
npx skills add getAlby/hub-skill
```

### 🦞 OpenClaw

Tell your agent to install the skill:

```txt
Install this skill as a custom skill: https://getalby.com/hub/SKILL.md
```

## Example Agent Prompts

- "Set up my Alby Hub."
- "Check my hub's lightning and on-chain balances."
- "Open an inbound lightning channel."
- "Create a new NWC app connection called 'My Store' with a monthly budget of 50,000 sats."
- "Show me all recent payments."

## Reference

- [Overview](./references/overview.md)
- [Backends](./references/backends.md)
- [Initial Setup](./references/initial-setup.md)
- [Authentication](./references/authentication.md)
- [Hub Management](./references/hub-management.md)
- [Channels](./references/channels.md)
- [Payments](./references/payments.md)
- [Apps](./references/apps.md)
- [LSP](./references/lsp.md)
- [Mutinynet](./references/mutinynet.md)
