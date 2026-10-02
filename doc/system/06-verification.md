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
