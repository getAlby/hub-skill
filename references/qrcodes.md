# QR Codes

Long strings like lightning invoices and NWC connection URLs are easier to use when displayed as a QR code. On Linux, use `qrencode`:

```bash
echo -n "<string>" | qrencode -t UTF8
```

Install if needed: `sudo apt-get install -y qrencode`

## When to offer a QR code

Always **ask the user** before generating one. Common cases:

- **`make-invoice`** — display the BOLT11 invoice as a QR code for a wallet to scan
- **`request-lsp-order`** — display the LSP payment invoice as a QR code
- **`create-app`** — display the `nostrWalletConnectUrl` as a QR code for easy pairing with a NWC-compatible app
