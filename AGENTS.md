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

## Audit Method

- Read the player-facing text first and identify concrete claims about mechanics, probabilities, formulas, flags, limits, availability, or side effects.
- Check the related code/data definitions before deciding a claim is wrong.
- Prefer structured data/parsers and established local tools over ad hoc text matching when the codebase provides them.
- Distinguish documentation bugs from code bugs. Do not change mechanics unless the task explicitly asks for code behavior changes.
- Keep findings traceable: cite the text location, code/data source, observed mismatch, and proposed wording.

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
