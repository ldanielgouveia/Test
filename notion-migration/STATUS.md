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

## Still to move

| Database | Database URL | Data source |
|---|---|---|
| Atomic | https://app.notion.com/p/4dbcffe7d9a441beba09d43882827ea1 | `cbb37999-b611-429c-b09a-c7454523c16e` |
| Resources | https://app.notion.com/p/83987c80c97a4fa1a51d88bb21c3c18c | `0315e595-76a7-47d9-9e5d-51e8303563f3` |
| Projects | https://app.notion.com/p/e15ed6dccc38488385f77972006c6338 | `232b68d1-6d29-40c0-a4f6-3a73ba96a377` |
| Goals | https://app.notion.com/p/60f30a0ef01c44268b69cadace3f177b | `3a4a0fae-d643-4bb4-96f1-406bba5947bb` |
| Reminders | https://app.notion.com/p/23213f908e734a63a273e568851fd25b | `bf2f65b2-b0a0-48fd-9065-048e7041d40d` |
| Ideas | https://app.notion.com/p/e427dc10920c4bf094433b8eb3a40e82 | `dfcccef9-dae7-4ee6-be1a-9288fbec27ca` — **in Notion's trash**; ask Leo before doing anything with it |

For each one, Leo duplicates the Board Template first and tells you which copy is for which database.

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

## Unfinished: remove the bold title lines (Leo asked for this to be undone)

Earlier, a bold line with the page's title was inserted at the very top of some Notes pages.
Leo changed his mind: **remove only that inserted line** and keep page titles as they are.

Rule: only for the pages listed in `bold-title-pages.txt`. For each, fetch the page; if the
very first line of the content is exactly `**<page title>**`, remove just that line
(`notion-update-page`, `update_content`, old_str = that line plus the following newline,
new_str = ""), then fetch again to confirm the page now starts with its original text. If the
first line isn't exactly that, leave the page alone and list it. (The insert was only ever
attempted on pages whose text did NOT already start with the title, so a matching first line
on a listed page is always the inserted one.)

## Other open items

- **Ideas links**: 28 Notes pages had links to Ideas that couldn't be restored while Ideas is
  in the trash. They're in `notes-ideas-links-pending.json` (Notes page id → Ideas page ids).
- **Notes link backup** (from before the move) is in `notes-links-backup.txt`.
- Leo must update his **leo-notion-system skill** (claude.ai → Settings → Skills): Notes data
  source → `collection://7f630e5e-46f9-83c9-9856-07a8163e2bb6`, Tasks data source →
  `collection://05330e5e-46f9-82d4-91fb-8759c2c55cdb`.
- Scheduled routines (only editable from their own thread, or switched off in Routines):
  - **"Go through yesterday's notes"** still reads the old, empty Notes data source.
    Leo said he doesn't need it right now, so he can switch it off.
  - **"Daily habit refresh"** still reads the old, empty Tasks data source; it needs
    `collection://05330e5e-46f9-82d4-91fb-8759c2c55cdb`, or switching off.
