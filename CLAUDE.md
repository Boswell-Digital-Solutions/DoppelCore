# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

DoppelCore is a standalone Rust library that acts as the canonical **machine-truth kernel** for a code-mirror system: code is the authority, DoppelCore mirrors it into typed, JSON-stable truth records, a Registry (elsewhere) governs/verifies/enforces those records, and human-readable documents are deterministic rendered products rather than the authority layer itself. See `docs/doppelcore_canvas_set/` for the full doctrine and phased roadmap.

## Common Commands

- `cargo check` — type-check the library
- `cargo test` — run the test suite (includes `tests/wire_format.rs` JSON wire-format guarantees)
- `cargo fmt --all -- --check` — formatting check (enforced in CI)
- `cargo clippy --all-targets -- -D warnings` — lint, warnings treated as errors (enforced in CI)

CI (`.github/workflows/ci.yml`) runs all four on every push and pull request.

## Architecture

- `src/contracts.rs` — string enums (profile, subject/anchor/claim kinds, …)
- `src/records.rs` — canonical truth records and the manifest bundle
- `src/comparison.rs` — manifest-diff and drift-delta types
- `src/correction.rs` — correction-fabric contracts
- `src/extraction.rs` — Cortex extraction packet contracts
- `src/intake.rs` — extraction → canonical record normalization adapter
- `src/errors.rs` — typed error surface
- `tests/wire_format.rs` — JSON wire-format guarantees

## Notes

- Currently implemented: the contract surface (`contracts`, `records`, `comparison`, `correction`, `errors`) and Phase 2 extraction intake (`extraction`, `intake`), which normalizes bounded Cortex extraction packets into canonical subjects, anchors, and evidence.
- Not yet implemented (see Canvas 08 roadmap in `docs/doppelcore_canvas_set/`): the claim engine (Phase 3), Registry persistence/IPC (Phase 4), rendered projection (Phase 5), and differential scans/drift history (Phase 6). Don't assume these exist.
- This repo is self-contained — there is no zip-extract step or copy into `~/Forge/ecosystem/DoppelCore`; work directly in this checkout (see `APPLY.md`, `VERIFY.md`).
