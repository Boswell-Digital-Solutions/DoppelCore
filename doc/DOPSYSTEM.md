        # DoppelCore - Compiled System Reference

        **Designation:** DOP
        **Document role:** Canonical compiled technical reference for the DoppelCore Rust contract library
        **Source:** `doc/system/`
        **Build command:** `bash doc/system/BUILD.sh`
        **Document version:** 2.0 (2026-06-22) - canonical compliance migration
        **Protocol:** BDS Documentation Protocol v2.0; BDS Repo Documentation System Canonical Compliance Standard

        > **Generated artifact warning:** `doc/DOPSYSTEM.md` is assembled output. Edit
        > the source modules under `doc/system/` and rebuild. Hand edits to the
        > compiled artifact are overwritten by the next build.

        Assembly contract:

        - Command: `bash doc/system/BUILD.sh`
        - Validation: `bash doc/system/validate_snapshots.sh` runs during assembly
        - Primary output: `doc/DOPSYSTEM.md`

        This `doc/system/` tree is the canonical source of truth for DoppelCore. It uses
        explicit **truth classes**: canonical facts define repo role, authority
        boundaries, contract behavior, runtime behavior, and verification doctrine;
        snapshot facts are dated, audit-derived counts and current implementation
        inventory that may drift between audits.

        | Part | File | Contents |
        | --- | --- | --- |
        | §1 | `01-overview.md` | 01 Overview |
| §2 | `02-contract-surface.md` | 02 Contract Surface |
| §3 | `03-runtime-boundary.md` | 03 Runtime Boundary |
| §4 | `04-dependencies.md` | 04 Dependencies |
| §5 | `05-governance.md` | 05 Governance |
| §6 | `06-verification.md` | 06 Verification |
| §7 | `90-appendices.md` | 90 Appendices |

        ## Quick Assembly

        ```bash
        bash doc/system/BUILD.sh
        ```

---

            # Overview

            **Document version:** 2.0 (2026-06-22) - canonical compliance migration

            DoppelCore is a standalone Rust library repo for the portable truth-core contract surface that was extracted from Forge_Command.

The current slice establishes the repo as an internal ecosystem component without pulling in UI ownership, registry orchestration, Self-Healing command ownership, LocalDb ownership, or execution-lane behavior.

This documentation tree is a canonical starting point for repo-local system truth. It does not replace the authored planning material under `docs/doppelcore_canvas_set/`.

---

            # Contract Surface

            **Document version:** 2.0 (2026-06-22) - canonical compliance migration

            The repo-owned contract surface lives in `src/` and is organized around contracts, records, correction, comparison, and error types.

The current boundary is library-contract publication. DoppelCore may expose portable types and validation helpers, but this document does not admit database adapters, Tauri commands, registry orchestration, or correction-fabric handoff behavior.

---

            # Runtime Boundary

            **Document version:** 2.0 (2026-06-22) - canonical compliance migration

            DoppelCore is not a standalone runtime in the current slice. It has no direct execution lane and no service process documented by this source tree.

Runtime claims must be introduced only after executable proof lands in the repository and the system chapters are rebuilt from source.

---

            # Dependencies

            **Document version:** 2.0 (2026-06-22) - canonical compliance migration

            The repository is a Rust library crate. Dependency truth is owned by `Cargo.toml` and `Cargo.lock`.

Any dependency inventory in generated system docs is a snapshot fact and must be refreshed from the manifests before release claims are made.

---

            # Governance

            **Document version:** 2.0 (2026-06-22) - canonical compliance migration

            The slice boundary is intentionally narrow: establish a standalone library and avoid first-slice cross-repo coupling.

The repo must remain free of UI, registry, Self-Healing, LocalDb, and execution ownership until a later governed extraction slice admits those responsibilities.

---

            # Verification

            **Document version:** 2.0 (2026-06-22) - canonical compliance migration

            The README names the first proof gate as:

```bash
cargo test
cargo check
```

Run these commands from the repository root before claiming the library is ready for the next extraction slice.

## Which CI runs for which change

A change that touches only documentation runs the Documentation CI and no code CI.
A change that touches any other file runs the code CI.
A change that touches both runs both.
If the scope is unknown, the code CI runs.

The code CI is `.github/workflows/ci.yml`.
It runs formatting, clippy and tests.
It has a workflow-level `paths-ignore` filter on `push` and `pull_request`.
The filter ignores `docs/**`, `doc/**` and `**/*.md`.
A change to `.github/workflows/**` is code and runs the code CI.

No re-include exists.
No source file, test or build script reads a documentation file.
`Cargo.toml` names `LICENSE` only, and `LICENSE` is not Markdown.
If code starts to read a documentation file, the filter must re-include that path.
Then the filter must use `paths` with `!` patterns, because `paths-ignore` cannot re-include.

The Documentation CI is `.github/workflows/documentation.yml`.
It runs on changes to `docs/**`, `doc/**`, `**/*.md` and its own file.
It runs `bash doc/system/BUILD.sh`.
It fails if `git diff --exit-code -- doc` shows a difference.
The assembled `doc/DOPSYSTEM.md` must be built from its parts and committed.

No scheduled run exists.
No secret scan or other security scan exists in this repository.
If a scan is added, it must run on every change, documentation included.

Do not add a required check on a path-filtered workflow.
A workflow that does not start leaves the check pending, and the pending check blocks the merge.

---

            # Appendices

            **Document version:** 2.0 (2026-06-22) - canonical compliance migration

            Supporting authored material lives in:

- `APPLY.md`
- `VERIFY.md`
- `docs/doppelcore_canvas_set/`

Those files remain source evidence. This compiled system reference summarizes the current canonical repo boundary.
