# Project handoff

Read AGENTS.md first. BUILD/STATE.md and BUILD/TASKS.md remain the authoritative
ledger. This file is a summary, not a replacement ledger.

## Verified on 2026-09-30

- Repository: https://github.com/Vishnu2707/lattence.
- main: 2417e23295cffe4c7c9793b07ae047f35c9cb431.
- dev before this handoff: cc0aea79832dbb20850067cfb8d5786342c52b34.
- Latest follow-up changes are on dev, not main.
- Remote v1.0.1 tag points to the main commit; main package metadata says 1.0.0.
- Local dev tracks origin/dev. core.hooksPath is .githooks.
- The pre-commit hook runs provenance checking only.

## Unverified

The user reports 20,684 attack paths on a clean bundled fixture scan.
The README shows 92 paths, but that number is not a proven acceptance target.
Prior ledger claims about precision, graph counts, dashboard size, chain
reporting, and CI integration must be verified by execution. No scanner tests
or clean scans were performed during this handoff preparation.

## Next action

Execute BUILD/HANDOFF.md. Reproduce and trace the graph explosion before
adding features. Record literal commands, outputs, revision, environment,
fixture hashes, and report sizes. Do not mark the bug fixed from a summary.

## Maintenance

After each completed task, update this summary and the BUILD ledger in the same
commit. Include verified behavior, checks, blockers, next action, and commit
references. Preserve historical claims as historical, not current evidence.
