# Notion board migration: where things stand (Oct 15, 2026)

Read this first, then use the `anthropic-skills:leo-notion-system` skill for Leo's rules
(never delete anything, keep his words exactly, never mark anything done/dropped).
Some IDs in that skill are out of date; the ones below are current.

**Approval prompts:** Leo hates clicking "Allow once" hundreds of times. Those prompts come
from the Notion connector's own tool permissions on claude.ai, not from Claude Code, so
`.claude/settings.json` and Auto mode don't stop them. If a Notion write asks for approval,
stop and tell Leo to set that tool to "Always allow" at https://claude.ai/customize/connectors
(Notion → tool permissions) before doing any bulk work.

## The goal

Leo wants every database shown as a **board** using his special **Board Template**
(an old Notion board layout: compact small cards that show the page content).
A new board view can't reproduce that layout (the API can't set "cover = page content"
or the compact card mode), so the method is: Leo duplicates the Board Template once per
database, and Claude moves all pages from the old database into the copy.

- Board Template: database https://app.notion.com/p/3e230e5e46f9803487befad583763611
  (data source `f1830e5e-46f9-83f1-a64f-0733b0f703f8`), in the "Extras" page.
- **Never delete or recreate the board view** in a copy, and don't change its grouping.

## Done

| Database | New (board) data source | New database | Old data source (now empty) |
|---|---|---|---|
| Notes (247 pages) | `collection://7f630e5e-46f9-83c9-9856-07a8163e2bb6` | https://app.notion.com/p/3fa30e5e46f9800f9985c0b313f8f42a | `a96648f5-173c-4cf0-b785-3b96ff16e2d2` |
| Tasks (175 pages) | `collection://05330e5e-46f9-82d4-91fb-8759c2c55cdb` | https://app.notion.com/p/3fa30e5e46f98092a4d4f4bcdf467aba | `3eb30e5e-46f9-8036-a972-000bfa87308c` |
| Atomic (318 pages) | `collection://e1c30e5e-46f9-8332-9633-8766ed4e4f48` | https://app.notion.com/p/3fa30e5e46f9807f8d6af86089c196c6 (was "Board Template (1)") | `cbb37999-b611-429c-b09a-c7454523c16e` |
| Resources (145 pages) | `collection://4fb30e5e-46f9-833c-aa62-8788dd9c354b` | https://app.notion.com/p/3fa30e5e46f980628b41da580ddb4448 (was "Board Template (2)") | `0315e595-76a7-47d9-9e5d-51e8303563f3` |
| Projects (46 pages) | `collection://47330e5e-46f9-822c-a444-8712a8226466` | https://app.notion.com/p/3fa30e5e46f980479777f4023f2a6eac (was "Board Template (3)") | `232b68d1-6d29-40c0-a4f6-3a73ba96a377` |
| Goals (160 pages) | `collection://3df30e5e-46f9-824a-a7d6-07e6cd262afb` | https://app.notion.com/p/3fa30e5e46f980418e38c55e8890b1f1 (was "Board Template (4)") | `3a4a0fae-d643-4bb4-96f1-406bba5947bb` |
| Reminders (98 pages) | `collection://f1830e5e-46f9-83f1-a64f-0733b0f703f8` | https://app.notion.com/p/3e230e5e46f9803487befad583763611 (was the original "Board Template") | `bf2f65b2-b0a0-48fd-9065-048e7041d40d` |

Old databases were left in place, empty. Nothing was deleted.

Not carried over for Tasks (Leo has to do these by hand in Notion):
- the formulas **Written** and **Active project** (the API can't read formula code),
- the default **"New task"** template (Type = Task, Status = To-do).

Column renames made in the other databases (renamed, never removed; the "(old)" columns
still hold the old links):
- Notes move: Atomic/Ideas/Resources `From` → `From (old Notes)`;
  Tasks/Projects/Goals/Reminders `Notes` → `Notes (old)`. New `From` / `Notes` columns
  point to the new Notes database.
- Tasks move: Notes/Atomic/Resources/Projects `Tasks` → `Tasks (old)`;
  Goals/Reminders `Old project` → `Old project (old)`. New `Tasks` / `Old project`
  columns point to the new Tasks database.
- Template leftover columns in the copies were renamed `Template …` (e.g. `Template tasks`,
  `Template Status`) where they clashed with real names. A leftover status column gives
  every moved page "Not started"; ignore it.

## Five more moved (Oct 15)

Leo said the 5 templates in Extras were for the 5 remaining databases (Ideas aside), so they were
used in this order: Board Template (1) Atomic, (2) Resources, (3) Projects, (4) Goals, and the
original **Board Template** for Reminders. **There is no unused Board Template left**; for Ideas,
Leo needs to duplicate one of the board databases (or make a new template) first.
The new databases are named like the old ones, and both still sit side by side (the old ones are
empty, in their old places; the new ones are in "Extras"). Icons were not copied (the API can't).

- Backups (all properties and links, taken before the move): `backup-atomic.json`,
  `backup-atomic-late8.json`, `backup-resources.json`, `backup-projects.json`, `backup-goals.json`,
  `backup-reminders.json`. Link plan used for the restore: `restore-plan-5dbs.json`.
- Verified after the restore: page counts and every link total match the backups; old databases empty.
- 8 Atomic pages written Oct 14 were missing from the first backup (added by another session
  while this ran); they were backed up, moved and relinked separately. If anything still writes to
  the old data sources (e.g. the scheduled routines), it will land in the old empty databases.
- Column renames this time (renamed, never removed; "(old)" columns hold the old links):
  Notes `Atomic/Goals/Projects/Reminders/Resources` → `… (old)`; Tasks
  `Atomic/Goals/Projects/Reminders/Resources` → `… (old)`. New columns with the original names
  point to the new databases. In the copies, clashing template columns became `Template …`
  (`Template Tasks`, `Template Topic`, `Template Type`, `Template Kind`, `Template Notes`,
  `Template Status`, `Template Status 1`, `Template State`). The board views still group by the
  template's empty "Notes"/"Template Notes" select (unchanged).
- Not carried over: the leftover "(old)" link columns (`From (old Notes)`, `Tasks (old)`,
  `Notes (old)`, `Old project (old)`) — their links are in the backups.
- **Ideas links**: 77 links from 35 pages (Atomic, Goals) to Ideas couldn't be restored while Ideas
  is in the trash: `ideas-links-pending-5dbs.json`.
- 8 "On this topic" links and 8 Goals→Atomic / 1 Reminders→Atomic links in the backups pointed to
  pages that weren't in Atomic at backup time (the 8 late pages); those pages now carry the links
  themselves.

## Still to move

| Database | Database URL | Data source |
|---|---|---|
| Ideas | https://app.notion.com/p/e427dc10920c4bf094433b8eb3a40e82 | `dfcccef9-dae7-4ee6-be1a-9288fbec27ca` — **in Notion's trash**; ask Leo before doing anything with it |

## The method that works

1. **Back up** every page: all property values and every relation link, saved to a file
   in this repo folder (scratchpad folders are lost when a session ends).
   `query-data-sources` has a workspace usage limit; when it runs out, use search + fetch.
2. **Prepare the copy** with `notion-update-data-source` DDL: rename the title to the
   old title name; rename template columns whose names clash to `Template <name>`;
   add every non-relation property with the **same name, type and options** (values
   carry over on move only when name and type match).
3. **Relations:** moving a page drops its relation values. For each two-way relation,
   rename the reverse column in the other database to `<name> (old)`, then add the
   relation on the copy with `RELATION('<bare uuid>', DUAL '<original reverse name>')`
   (bare UUID, not `collection://…`) so other databases keep their column names.
4. **Test one page** with many links: `notion-move-pages` to the new data source id,
   fetch it, restore its relations from the backup, check the reverse side.
5. **Move the rest** (100 per call), then **restore every relation** from the backup
   (`update_properties`, one call per page; subagents in parallel work well).
6. **Verify**: old database empty, link totals match the backup, spot-check pages.

## Done: bold title lines removed (Oct 15)

Leo asked to undo the bold title line that had been inserted at the top of some Notes pages.
Every page in `bold-title-pages.txt` (41) was fetched. Where the first line was exactly
`**<page title>**`, only that line was removed (`update_content`) and the page re-fetched to
confirm it now starts with its original text. Titles were not touched.

- **Removed (19):** 3f930e5e46f981f9af32dd9c2a6300a4, 3f930e5e46f98103becee83dd6551003,
  3f930e5e46f98105949beaa26e0a3c1a, 3f930e5e46f9810ab098d6dadc3fe83f,
  3f930e5e46f981108481ca6db2fededa, 3f930e5e46f98121a7dafd20aff9bec4,
  3f930e5e46f981529b19ddf6396f3fa1, 3f930e5e46f981559079fa723b5e63a6,
  3f930e5e46f9815abc0ad9d2fccaf614, 3f930e5e46f98165a9bffb191d5142d3,
  3f930e5e46f98166a9b2cb1cd6405b8d, 3f930e5e46f98173ab81c63396738652,
  3f930e5e46f981759412f8aea38c5d64, 3f930e5e46f981a88a38c76906a085ee,
  3f930e5e46f981b18fe3f33bbea547cf, 3f930e5e46f981b3aeafeacde4878e86,
  3f930e5e46f981b6af33e3f0ab15066d, 3f930e5e46f981b9adc1d648a995f918,
  3f930e5e46f981dfbac5c197fcb29a91.
- **Left alone (22), first line was not the bold title** (no bold line was ever inserted, or
  it was declined): 3f930e5e46f981239714efe10646d3b7 ("Motivation I didn't have before",
  starts with his text), 3fa30e5e46f9817dbab6dab767fbcaa7 (starts `## Staying by the beach`),
  and all 20 other session B pages (they start with a `##`/`###` heading, a gray "Pasted"
  callout, or a code block).

## Other open items

- **Ideas links**: 28 Notes pages had links to Ideas that couldn't be restored while Ideas is
  in the trash. They're in `notes-ideas-links-pending.json` (Notes page id → Ideas page ids).
- **Notes link backup** (from before the move) is in `notes-links-backup.txt`.
- **When every database is moved, write Leo a new skill** to replace the out-of-date
  `leo-notion-system` one (he'll add it himself; don't ask him to hand-edit the old one).
  Start from the old skill's text (load `anthropic-skills:leo-notion-system`), keep all its
  rules, and update: every data source ID to the new board databases (see the Done table above), the relation column names after the
  renames above (the "(old)" columns are leftovers to ignore), the Template-leftover columns
  to ignore, and the board-view rule (never delete or recreate a board view). Save it as a
  `SKILL.md` in this folder (use the `anthropic-skills:skill-creator` skill) and tell Leo how
  to add it.
- Scheduled routines (only editable from their own thread, or switched off in Routines):
  - **"Go through yesterday's notes"** still reads the old, empty Notes data source.
    Leo said he doesn't need it right now, so he can switch it off.
  - **"Daily habit refresh"** still reads the old, empty Tasks data source; it needs
    `collection://05330e5e-46f9-82d4-91fb-8759c2c55cdb`, or switching off.
