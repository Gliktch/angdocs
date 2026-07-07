# Source Checkouts

Track local source clones, forks, worktrees, release baselines, and release-to-nightly deltas used by audit batches.

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
Purpose: Text truth audit release baseline
Upstream: https://github.com/sulkasormi/frogcomposband
Fork:
Local path: sources/frogcomposband-7.1.salmiak
Baseline release/tag: v7.1.salmiak
Baseline SHA: 36ae9d549a6196243a2be84f8e07f8cb7ce574aa
Hosted/nightly source:
Hosted/nightly SHA or identifier:
Work branch pattern: angdocs/frog-<domain>
Notes: Treat the GitHub tag checkout as the relevant FrogComposband release source for this project.
```

```text
Variant: FrogComposband
Purpose: Text truth audit nightly delta
Upstream: https://github.com/sulkasormi/frogcomposband
Fork:
Local path: sources/frogcomposband-nightly
Baseline release/tag: master
Baseline SHA: 3d28f6b1d28a0246a1c4923414455eb669ea34b8
Hosted/nightly source: official upstream master
Hosted/nightly SHA or identifier: 3d28f6b1d28a0246a1c4923414455eb669ea34b8
Work branch pattern: angdocs/frog-nightly-<domain>
Notes: Treat the GitHub master checkout as the relevant FrogComposband nightly source for this project.
```

```text
Variant: Angband
Purpose: Text truth audit release baseline
Upstream: https://github.com/angband/angband
Fork:
Local path: sources/angband-4.2.5
Baseline release/tag: 4.2.5
Baseline SHA: 69e24dbb001818d5f902215e7a474d122e12202c
Hosted/nightly source:
Hosted/nightly SHA or identifier:
Work branch pattern: angdocs/angband-4.2.5-<domain>
Notes: Treat the GitHub tag checkout as the relevant Angband 4.2.5 source for this project.
```

```text
Variant: Angband
Purpose: Text truth audit official-nightly delta from 4.2.5
Upstream: https://github.com/angband/angband
Fork:
Local path: sources/angband-nightly
Baseline release/tag: master
Baseline SHA: 3ea683599894ba5786e56bb22f0c2a9b47809c6e
Hosted/nightly source: official upstream master
Hosted/nightly SHA or identifier: 3ea683599894ba5786e56bb22f0c2a9b47809c6e
Work branch pattern: angdocs/angband-nightly-<domain>
Notes: The useful Angband delta is between sources/angband-4.2.5 and sources/angband-nightly.
```

## Source Selection Notes

- Use GitHub-sourced release tags and upstream nightly/master checkouts for audit work.
