# Backups

## After Opening a Channel

For the default LDK backend, static channel backups are saved automatically to the `ldk` folder in the hub directory after each channel opening. These are recommended to be backed up to another location after each channel opening.

Static channel backups combined with the user's recovery phrase can be used together to recover all funds if they lose access to their Alby Hub.

A simpler alternative: the user can connect their Alby account to their hub, and automatic encrypted static channel backups will be saved to their Alby account - then they only need their recovery phrase. See [Alby Account](./alby-account.md) for how to connect.

## Backup Recovery Phrase

`backup-mnemonic` writes the 12-word wallet recovery phrase to a `.recovery` file (default: `~/.hub-cli/albyhub.recovery`). The command outputs `{ "success": true, "file": "<path>" }`.

> **IMPORTANT:** The agent MUST NOT read the backup file at any point. Just tell the user the file location so they can store it securely offline. The recovery phrase is sensitive — reading it would expose it in conversation history.
