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
Purpose: Text truth audit release baseline
Upstream: https://github.com/sulkasormi/frogcomposband
Fork:
Local path: sources/frogcomposband-7.1.salmiak
Baseline release/tag: v7.1.salmiak
Baseline SHA: 36ae9d549a6196243a2be84f8e07f8cb7ce574aa
Hosted/nightly source:
Hosted/nightly SHA or identifier:
Work branch pattern: angdocs/frog-<domain>
Notes: Live GitHub checkout matches AngbandArchive/frogcomposband/7.1.salmiak with no file-tree differences, excluding .git.
```

```text
Variant: FrogComposband
Purpose: Text truth audit nightly delta
Upstream: https://github.com/sulkasormi/frogcomposband
Fork:
Local path: sources/frogcomposband-nightly
Baseline release/tag: master
Baseline SHA: 3d28f6b1d28a0246a1c4923414455eb669ea34b8
Hosted/nightly source: AngbandArchive/frogcomposband/nightly_7.1.salmiak_63-g3d28f6b1
Hosted/nightly SHA or identifier: nightly_7.1.salmiak_63-g3d28f6b1
Work branch pattern: angdocs/frog-nightly-<domain>
Notes: Live GitHub master matches the archived nightly with no file-tree differences, excluding .git.
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
Notes: Live GitHub checkout differs from AngbandArchive/angband/4.2.5 in 10 file-tree entries, all apparently packaging/generated or repository-support files (.github, .gitignore, .travis.yml, autogen.sh, aclocal.m4, configure, src/autoconf.h.in, Windows DLLs, version). Treat source/data/docs text audit work as aligned unless a later focused diff shows content-relevant changes.
```

```text
Variant: Angband
Purpose: Text truth audit official-nightly delta
Upstream: https://github.com/angband/angband
Fork:
Local path: sources/angband-nightly
Baseline release/tag: master
Baseline SHA: 3ea683599894ba5786e56bb22f0c2a9b47809c6e
Hosted/nightly source: AngbandArchive/angband/nightly_4.2.6_44-g6ded57739
Hosted/nightly SHA or identifier: nightly_4.2.6_44-g6ded57739
Work branch pattern: angdocs/angband-nightly-<domain>
Notes: Live official master differs from the archived nightly in 136 file-tree entries, including docs, gamedata, build files, borg files, and core source files. Treat this as an intentional official-nightly versus hosted/archive delta, not as a duplicate baseline.
```

## Archive Comparison Notes

- Comparison command shape: `diff -qr --exclude=.git <live-checkout> <archive-copy>`.
- FrogComposband release and nightly are exact file-tree matches against the local archive.
- Angband 4.2.5 has only packaging/generated/repository-support differences in the first comparison pass.
- Angband official nightly has materially moved beyond the archived nightly, so player-facing findings against `sources/angband-nightly` may need a hosted-nightly applicability check before sending patches or recommendations for angband.live.
