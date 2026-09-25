# Contributing to mux-contracts

Thanks for contributing to Mux Protocol's Soroban contracts. This guide covers the
basics; for deeper protocol context see the canonical docs linked below.

## Canonical documentation

- [`README.md`](./README.md) — repo overview, build/test instructions, and layout.
- [`SECURITY.md`](./SECURITY.md) — vulnerability disclosure and security policy.
- [`CONTRACT_IDS.md`](./CONTRACT_IDS.md) — deployed contract IDs per network.
- [`Somzilla.md`](./Somzilla.md) — status/audit notes for the Somzilla review.
  This file is a status document only; where it disagrees with `README.md`,
  `SECURITY.md`, or `CONTRACT_IDS.md`, those canonical docs win.

## Getting started

1. Fork and clone the repository.
2. Install the Rust toolchain and `soroban-cli` per `README.md`.
3. Build and run the test suite as described in `README.md`.

## CI: wasm size budget and artifacts

The CI workflow (`.github/workflows/ci.yml`) enforces a **wasm size budget** on
every compiled contract. The build fails closed if any `*.wasm` exceeds the
configured limit, so oversized contracts cannot land unnoticed.

- The budget is defined by the `WASM_SIZE_BUDGET_BYTES` environment variable in
the workflow (default `65536` bytes / 64 KiB per contract).
- To adjust the budget, change that value in `.github/workflows/ci.yml` and
explain the rationale in your PR description.
- Built wasm artifacts are uploaded from each CI run as the `wasm-artifacts`
artifact, so contributors and reviewers can download and inspect them directly
from the workflow run page.

If a contract legitimately needs more space, raise the budget in the same PR
that grows the contract and note the reason; do not bypass the check.

## Pull requests

- Keep changes scoped to a single issue; avoid unrelated refactors.
- Include tests for new behavior and authz/idempotency negatives where relevant.
- Update docs (`README.md`, `SECURITY.md`, `CONTRACT_IDS.md`, `Somzilla.md`)
  when behavior or status changes so they stay consistent.
- Do not commit secrets, keys, JWTs, or webhook secrets.

## Reporting security issues

Do not open public issues for vulnerabilities. Follow the process in
[`SECURITY.md`](./SECURITY.md).
