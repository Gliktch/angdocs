# Source Checkouts

Track local source clones, forks, worktrees, release baselines, and hosted-nightly deltas used by audit batches.

## Fields

Use this shape for each checkout:

```text
Variant:
Purpose:
Upstream:
Fork:
Local path:
Baseline release/tag:
Baseline SHA:
Hosted/nightly source:
Hosted/nightly SHA or identifier:
Work branch pattern:
Notes:
```

## Initial Targets

```text
Variant: FrogComposband
Purpose: Text truth audit baseline plus hosted/nightly delta
Upstream:
Fork:
Local path: sources/frogcomposband-salmiak
Baseline release/tag: salmiak
Baseline SHA:
Hosted/nightly source:
Hosted/nightly SHA or identifier:
Work branch pattern: angdocs/frog-<domain>
Notes:
```

```text
Variant: Angband
Purpose: Text truth audit baseline plus hosted/nightly delta
Upstream:
Fork:
Local path: sources/angband-4.2.5
Baseline release/tag: 4.2.5
Baseline SHA:
Hosted/nightly source:
Hosted/nightly SHA or identifier:
Work branch pattern: angdocs/angband-4.2.5-<domain>
Notes:
```
