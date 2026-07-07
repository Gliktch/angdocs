# angdocs

Angband-family documentation and text audit workspace.

This project audits player-facing descriptions against code truth across major Angband-family variants, then prepares concise and lore-friendly text fixes where the documentation no longer matches mechanics.

Initial priority targets:

* FrogComposband `salmiak` plus the relevant hosted/nightly delta
* Angband `4.2.5` plus the relevant hosted/nightly delta

Workspace layout:

* `queues/`: audit queues and target lists
* `batches/`: per-batch work logs
* `findings/`: validated text-vs-code mismatches
* `patches/`: patch plans, diffs, and upstream notes
* `references/`: release, nightly, and source-location notes

See `AGENTS.md` for standing audit rules.
