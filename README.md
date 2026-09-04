<p align="center">
  <b>bitcoin-wallet</b>
</p>

<p align="center">
  <sub>segwit · hd · psbt</sub>
</p>

<p align="center">
  <code>.NET 10</code> &nbsp;·&nbsp; <code>MIT</code> &nbsp;·&nbsp; <code>BtcWallet</code> &nbsp;·&nbsp; <code>btcwallet</code>
</p>

---

## About

Bitcoin HD wallet — BIP84 accounts, coin control, PSBT export for hardware signers.

Named exactly what people type into GitHub search when they need a starting point.

> Prop / lab repo. Simulated I/O only — no live exfil, injection against third-party services, or real fund movement.

---

## Features

| Area | Coverage |
|------|----------|
| Keys | BIP39/BIP32, encrypted vault, hardware paths |
| Chain | RPC sync, balances, tx history |
| Sign | Local sign, PSBT, typed data preview |
| CLI | Headless import, sync, export |


## Capabilities

### Wallet core
- BIP39/BIP32/BIP84 HD derivation, native segwit (P2WPKH) default
- Coin control: label UTXOs, freeze, select inputs for send
- Fee slider: sat/vB presets, RBF toggle, CPFP notes
- PSBT create/sign/export for hardware workflows
- Watch-only xpub import, gap limit scan

### Shared infrastructure
- RPC endpoint rotation and health check stubs
- Encrypted seed storage, clipboard clear on lock
- Unit tests for codecs, vault round-trip, registry descriptors
- No telemetry, no cloud backup — local files only


---

## Layout

```
bitcoin-wallet/
├── bitcoin-wallet.slnx
├── src/
│   ├── App/
│   │   ├── Program.cs          # entry + settings
│   │   ├── Commands.cs         # CLI handlers
│   │   ├── CliUtils.cs         # args + tables
│   │   └── appsettings.json
│   └── Core/
│       ├── Models.cs           # vault, account, portfolio, fees
│       ├── Contracts.cs        # interfaces + JSON defaults
│       ├── Codecs.cs           # hex / base58 / bech32-style
│       ├── VaultCrypto.cs      # AES-GCM + PBKDF2
│       ├── MnemonicService.cs  # mnemonic normalize / seed
│       ├── Derivation.cs       # HD paths + address factory
│       ├── Networks.cs         # registry + endpoint rotator
│       ├── ChainClient.cs      # simulated RPC + fee quotes
│       ├── VaultStore.cs       # JSON vault + migrations
│       ├── Validation.cs       # guards, tx builder, analytics
│       ├── Services.cs         # discovery, sync, export
│       └── WalletService.cs    # composition root
└── tests/Core.Tests/
```

Two projects under `src/` (App + Core). Logic is split across focused `.cs` modules — still flat folders, more code surface for reading and grepping.

---

## Build

Requires .NET SDK 10.

```bash
dotnet restore bitcoin-wallet.slnx
dotnet build bitcoin-wallet.slnx -c Release
dotnet test bitcoin-wallet.slnx -c Release
```

```bash
dotnet run --project src/App -- import
```

---

## CLI

| Command | Description |
|---------|-------------|
| `import` | Create vault from mnemonic |
| `list` | List vault metadata |
| `sync` | Sync enabled networks |
| `balance` | Show cached balances |
| `export` | Export recent transactions |
| `status` | Health and portfolio summary |
| `fee` | Quote network fee policy |
| `networks` | List registered networks |

---

## Config

`src/App/appsettings.json` — defaults. Override with `appsettings.local.json` (git-ignored).

---

## Topics

```
bitcoin ethereum wallet bip39 bip32 cryptocurrency defi hd-wallet open-source csharp dotnet
```

---

## License

MIT — Copyright (c) 2026 Vault Labs

See `LICENSE`.
