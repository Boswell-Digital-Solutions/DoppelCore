# Known issues

## 2026-10-02: `CLAUDE.md` says CI runs on every push and pull request

- What is wrong: `CLAUDE.md` says CI runs fmt, clippy and tests "on every push and pull request". A documentation-only change now skips the code CI.
- Root cause: the path filter added in the documentation-only CI change. The sentence predates it.
- Fix: not made. Reword the sentence to name the filter and `documentation.yml`.
- Status: open.
