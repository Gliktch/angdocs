# Angdocs Agent Instructions

`angdocs` is the workspace for Angband-family documentation truth audits.

## Mission

- Audit player-facing descriptive text against code truth across targeted Angband-family variants.
- Cover help text, item descriptions, spell/prayer/ability descriptions, class/race/personality text, monster and ego/artifact descriptions, UI help, and similar user-facing documentation.
- When text does not match mechanics or data behavior, produce concise, effective, lore-friendly updates that preserve the variant's voice.

## Version Targeting

- Use the latest official release as the baseline for each targeted variant.
- At the start of each variant audit, verify the latest official release from upstream sources rather than relying on memory.
- If `angband.live` hosts a nightly/development build for that variant, audit the official release first, then inspect the latest-official-to-hosted-nightly delta.
- Treat hosted nightlies as supplemental patch targets, not separate full audits. Avoid duplicating stable-release work unless the nightly delta changes the relevant code or text.
- Record the exact variant, upstream URL, release/tag, commit SHA, and any hosted-nightly SHA or identifier used for each audit batch.

## Primary Targets

- Start with FrogComposband `salmiak` plus its relevant nightly/hosted delta.
- Start with Angband `4.2.5` plus its relevant nightly/hosted delta.
- For these initial targets, treat the named release/version as the baseline even when a newer official release exists, unless the user updates the target.

## Audit Method

- Read the player-facing text first and identify concrete claims about mechanics, probabilities, formulas, flags, limits, availability, or side effects.
- Check the related code/data definitions before deciding a claim is wrong.
- Prefer structured data/parsers and established local tools over ad hoc text matching when the codebase provides them.
- Distinguish documentation bugs from code bugs. Do not change mechanics unless the task explicitly asks for code behavior changes.
- Keep findings traceable: cite the text location, code/data source, observed mismatch, and proposed wording.

## Model Strategy

- Use `gpt-5.4-mini` for economical bulk passes: text inventory, claim extraction, likely code/data source mapping, and first-pass notes.
- Use `gpt-5.5` with medium reasoning for primary adjudication: deciding whether text is wrong, tracing mechanics across files, and drafting final wording or patches.
- Escalate to `gpt-5.5` with xhigh reasoning only for hard cases: tangled formulas, inherited flags/effects, ambiguous proc chains, or conflicting stable/nightly behavior.
- Prefer multiple focused passes over one broad expensive pass. Keep each worker batch narrow enough that references, decisions, and proposed patches can be reviewed.
- Record model/escalation level in batch notes when it affects confidence or cost.

## Patch Style

- Make the smallest text change that makes the description true and useful.
- Preserve upstream formatting, line wrapping, terminology, spelling style, and file organization.
- Prefer clear player-facing language over implementation jargon.
- Keep lore-friendly flavor when the original text is flavor-forward, but never at the cost of mechanical truth.
- When stable and hosted-nightly patches differ, keep the stable patch primary and record the nightly-only supplemental patch separately.

## Task Shape

- Use small audit batches, such as one variant plus one text domain: `frogcomposband spells`, `angband object descriptions`, or `sil-q help files`.
- Store durable notes, queues, findings, and patch plans in this repo.
- Jarvis tracks scheduling and task state; this repo stores the audit substance.

## Repository Layout

- `queues/`: standing queues and target lists for variants, text domains, and nightly deltas.
- `batches/`: per-batch work logs with scope, sources, commands, model/escalation level, and outcome.
- `findings/`: validated documentation mismatches, one file per finding or tight group of related findings.
- `patches/`: patch plans, generated diffs, upstream PR notes, and stable-vs-nightly supplemental patch records.
- `references/`: durable source notes about release tags, hosted nightly SHAs, upstream URLs, and local checkout locations.
- `sources/`: ignored local clones or mirrors of target codebases. Do not commit upstream source trees here.
- `worktrees/`: ignored local worktrees or per-batch patch branches. Do not commit upstream source trees here.

Use stable filenames such as `<variant>-<version>-<domain>.md` for batch files and `<variant>-<short-topic>.md` for findings.

## Source Checkout Boundaries

- Keep target game codebases inside ignored `sources/` or `worktrees/` subfolders so Jarvis treats them as implementation detail of `angdocs`, not separate top-level managed projects.
- Track checkout metadata in `references/checkouts.md`: upstream URL, fork URL if any, local path, release tag/SHA, hosted-nightly SHA or identifier, and intended branch naming.
- For upstream contributions, make edits in a fork/branch that belongs to the target repo's fork network. Use `angdocs` to store findings and patch notes, not as the PR source repository.
- Prefer branch names prefixed with `angdocs/`, such as `angdocs/frog-salmiak-spells` or `angdocs/angband-4.2.5-help`.
- If a local source checkout has uncommitted changes, record whether they are audit scratch, generated artifacts, or intended patch work before switching tasks.
