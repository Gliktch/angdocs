# Angband 4.2.5 Quest Text Audit

Status: active
Batch ID: angband-4.2.5-quests
Variant: Angband
Baseline: 4.2.5
Baseline source: `sources/angband-4.2.5`
Nightly delta source: `sources/angband-nightly`

## Goal

Audit vanilla Angband quest-related player-facing text against code/data truth, using 4.2.5 as the baseline and official upstream master/nightly only as a release-to-nightly delta check.

## First Pass

Model: `gpt-5.4-mini`
Purpose: economical inventory, claim extraction, and likely source mapping.

Tasks:

* Inventory quest-related player-facing text in Angband 4.2.5.
* Extract concrete claims about quest levels, quest monsters, stair/recall behavior, quest artifacts, and related player-visible mechanics.
* Map each claim to likely verification sources in code or gamedata.
* Compare the same quest-related files or claims against official master/nightly only enough to identify obvious delta areas.
* Do not adjudicate hard mechanics unless the answer is directly obvious from the mapped sources.
* Do not patch source files in this pass.

## Expected Output

Add first-pass notes below with:

* text locations
* extracted claims
* likely verification files/functions/data records
* baseline-to-nightly delta notes
* open questions for a later adjudication pass

## Source Hints

Baseline files already identified:

* `sources/angband-4.2.5/lib/gamedata/quest.txt`
* `sources/angband-4.2.5/src/player-quest.c`
* `sources/angband-4.2.5/src/player-quest.h`
* `sources/angband-4.2.5/docs/option.rst`
* `sources/angband-4.2.5/docs/command.rst`
* `sources/angband-4.2.5/docs/hacking/modifying.rst`
* `sources/angband-4.2.5/lib/gamedata/monster.txt`
* `sources/angband-4.2.5/lib/gamedata/object.txt`
* `sources/angband-4.2.5/lib/gamedata/artifact.txt`

Nightly counterpart files:

* `sources/angband-nightly/lib/gamedata/quest.txt`
* `sources/angband-nightly/src/player-quest.c`
* `sources/angband-nightly/src/player-quest.h`
* `sources/angband-nightly/docs/option.rst`
* `sources/angband-nightly/docs/command.rst`
* `sources/angband-nightly/docs/hacking/modifying.rst`
* `sources/angband-nightly/lib/gamedata/monster.txt`
* `sources/angband-nightly/lib/gamedata/object.txt`
* `sources/angband-nightly/lib/gamedata/artifact.txt`

## First-Pass Notes

### Text locations

* `lib/gamedata/quest.txt:3-18` - fixed quest definitions for Sauron and Morgoth.
* `src/player-quest.c:186-251` - quest completion, magical staircase spawn, and victory/retire message.
* `docs/option.rst:156-166` - force-descent text mentioning quest-level recall blocking and warning before entry.
* `docs/command.rst:130-135` - down-stair command text noting quest levels have no down stairs until the quest monster dies.
* `docs/hacking/modifying.rst:121-124` - quest.txt overview and hard-coded quest caveat.

### Extracted claims

* There are only two fixed vanilla quests, copied into player state at birth.
* Completing a quest zeroes that quest's stored level in the player quest history.
* Sauron is the level 99 quest and Morgoth is the level 100 quest; each has `number:1`.
* Quest levels block recall until the quest is complete, and the player is warned before descending into one.
* Quest levels have no down stairs until the quest monster is killed.
* Killing a quest monster can create a magical staircase and may end the game once all quests are complete.
* The post-win retirement prompt is part of the player-facing quest flow.

### Likely verification sources

* `src/player-quest.c`
  * `parse_quest_*` for quest data ingestion.
  * `player_quests_reset()` / `player_quests_free()` for birth-time copying and cleanup.
  * `is_quest()` for quest-level detection.
  * `build_quest_stairs()` for staircase creation.
  * `quest_check()` for completion, victory, and message text.
* `src/player-quest.h` for the quest API surface.
* `lib/gamedata/quest.txt` for the fixed quest records.
* `lib/gamedata/monster.txt:14640-14777` for Sauron/Morgoth questor records and depth/flags.
* `lib/gamedata/artifact.txt:2404-2434` and `lib/gamedata/object.txt` quest-artifact sections for late-game quest-linked item text/data.

### Baseline-to-nightly delta

* `lib/gamedata/quest.txt` appears unchanged between 4.2.5 and official nightly.
* `src/player-quest.c` changed in `quest_check()`:
  * nightly matches quest completion by current depth plus monster race, instead of only `RF_QUESTOR`/monster depth.
  * nightly only spawns the magical staircase after an actual completion event.
  * nightly changes the win/retire message from `commit suicide` to `key is shift-q`.
* The inspected quest-facing docs paragraphs did not show a quest-specific wording change; nearby nightly command/option diffs appear to be unrelated staircase/autoexplore documentation churn.

### Open questions

* Does the nightly `quest_check()` change alter behavior for any future multi-kill or non-unique quest definitions, or is it just a cleanup for the current fixed quests?
* Are there any other quest-linked player-facing strings outside the files listed here, especially in UI messages or help text not covered by the initial grep set?
* Should the quest artifact area be treated as part of this batch's final adjudication, or only as supporting late-game content context?

## Next Step

Run `gpt-5.5` with medium reasoning for adjudication of the mapped quest claims and the official master/nightly `quest_check()` delta. Produce validated findings or note that no text change is needed.
