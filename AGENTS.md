# SOVD Security Helper Index

Rust HTTP helper for deriving UDS security keys for SOVD Explorer and simulation workflows.

## Where to look

- `Cargo.toml` — package metadata, axum/tokio/clap/JWT dependencies.
- `src/main.rs` — full service, CLI/env options, routes, key algorithms.
- `config/secrets.toml` — development ECU secret configuration.
- `start.sh`, `stop.sh` — local service lifecycle helpers.

## Essential commands

No component-local `mise` file is present; use Cargo and repo scripts from this submodule root.

```bash
cargo build
cargo test
cargo fmt --all -- --check
cargo clippy --all-targets -- -D warnings
cargo run -- --help
./start.sh
./stop.sh
```

Finding commands:

```bash
rg --files -g 'Cargo.toml' -g 'README*' -g 'config/**' -g '*.sh'
rg -n "derive|seed|key|token|auth|clap|route|secrets" src config Cargo.toml *.sh
```

## Stack

- Rust 2021 binary, axum HTTP server, tokio runtime, clap config/env parsing.
- TOML secrets config; optional JWT/request integration via `jsonwebtoken` and `reqwest`.

## Guardrails

- This is simulation/dev UDS unlock support, not SOVD client authorization; do not confuse it with `sovd-token-helper`.
- Never commit real ECU secrets; `config/secrets.toml` is development data only.
- Keep helper API compatible with SOVD Explorer expectations.

## Gotchas

- No README exists in this checkout; inspect `src/main.rs` before changing behavior.
- Service scripts may assume local ports/config paths from this repo.

## Missing docs/specs to watch

- Add a README/API contract for `/info` and key-calculation endpoints.
- Document accepted secret config schema beyond the example TOML.
