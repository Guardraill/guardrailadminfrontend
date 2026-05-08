# Guardrail Admin Backend

Rust/Axum API backing Guardrail’s admin flows for asset issuance, compliance, treasury, oracle
pricing, markets, and faucet operations.

## Features

- Admin and auth endpoints
- Asset catalog and issuance workflows
- Compliance registry and rules
- Oracle pricing and valuation sync
- Treasury and market endpoints
- Faucet utilities for test environments
- Monad chain and account abstraction integrations

## Tech Stack

- Rust 1.94 (edition 2024)
- Axum + Tokio
- PostgreSQL + SQLx
- Ethers-rs + Reqwest

## Getting Started

### Prerequisites

- Rust 1.94+ (see `rust-version` in `Cargo.toml`)
- PostgreSQL 13+
- Access to the target chain RPC and contract addresses (see `.env.example`)

### Setup

1. Copy the environment template:
   ```bash
   cp .env.example .env
   ```
2. Update required values in `.env`.
3. Ensure the database exists (the app runs migrations on startup).

### Run

```bash
cargo run
```

The server listens on `HOST:PORT` (defaults to `0.0.0.0:8080`) and runs SQLx migrations
from `./migrations` on startup.

## Configuration

All environment variables are documented in `.env.example`. Key required settings include:

- **Server**: `HOST`, `PORT`, `CORS_ALLOWED_ORIGINS`
- **Database**: `DATABASE_URL`
- **Auth**: `GOOGLE_CLIENT_ID`, `JWT_SECRET`, `JWT_TTL_HOURS`, `ADMIN_WALLET_ADDRESSES`
- **Chain + AA**: `MONAD_RPC_URL` or `MONAD_RPC_URLS`, `AA_BUNDLER_RPC_URL`,
  `AA_ENTRY_POINT_ADDRESS`, `AA_SIMPLE_ACCOUNT_FACTORY_ADDRESS`,
  `AA_OWNER_ENCRYPTION_KEY`
- **Contracts**: `ACCESS_CONTROL_ADDRESS`, `ASSET_FACTORY_ADDRESS`,
  `COMPLIANCE_REGISTRY_ADDRESS`, `TREASURY_ADDRESS`, `ORACLE_DATA_BRIDGE_ADDRESS`,
  `PAYMENT_TOKEN_ADDRESS` (or `MOCK_USDC_ADDRESS`)

Optional Filebase/IPFS settings are available via the `FILEBASE_*` variables.

## API Overview

- `GET /health` for basic health checks.
- Admin routes are grouped under `/admin`.
- Auth routes are under `/auth`.
- Public and user routes include assets, compliance, markets, oracle, and treasury modules.

For admin asset creation payloads and seed data, see
[`docs/rwa-admin-asset-seeds.md`](docs/rwa-admin-asset-seeds.md).

## Utilities

Account-abstraction smoke test:

```bash
cargo run --bin aa_smoke
```

Requires the AA and contract env vars to be configured.

## Testing

```bash
cargo test
```

## Linting & Formatting

```bash
cargo fmt -- --check
cargo clippy --all-targets --all-features
```

## Contributing

1. Create a feature branch.
2. Run tests and linting before submitting a PR.
3. Include clear context in your PR description.

## License

No license file is currently provided. Please confirm licensing before reuse.
