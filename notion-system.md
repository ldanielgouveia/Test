# Leo's Notion System: Context for Claude

This file explains how Leo's Notion workspace is set up and how to work in it. It was checked against the live workspace on 2026-10-19.

## How to use this file (for Leo)

- Attach this file, or paste it, at the start of a new chat.
- If Notion and this file disagree, Notion wins. Ask Claude to check and update the file.
- Leo thinks the main structure is in place for now. A lot is still unfinished, and he is going to try to figure out the more specific structure of each page next, so expect this file to change.
- Tasks can live either in the Tasks database or inside a project or topic page's own database (Inbox = Tasks). Both are valid.
- Quotes from Leo come from his description in chat on 2026-10-19 unless marked otherwise.

## Read this first (for Claude)

- **Words Leo uses.** "Project" means only a flag-icon page made from the project template under Notebooks (*"when i say projects i just mean the template under notebooks that uses the flag icon instead of the notebook icon."*). "Notebook" in his phrase "projects/notebooks" means a notebook-icon topic page. "Notebooks" (capital N) is the database. The numbered rows (1.1 to 9.5) are left over from the old Projects database. They are not projects in his sense.
- **Only two levels: tasks and projects.** Leo (2026-10-19): *"goals have turned into projects for me. there is either tasks or projects, nothing else. if there is something more longterm it goes under timeline in reminders."* So a goal is a project (a flag page in Notebooks), and anything long-term goes in Reminders with Template Notes = **Timeline**. Don't create goals anywhere.
- Six databases are in use. They sit at the top of the sidebar in this order: **Notes, Reminders, Tasks, Notebooks, Thoughts, Resources**. Older databases sit in the trash. Do not use them.
- Two databases were renamed, but the relations that point to them still use the old names:
  - Any relation called **Atomic** points to **Thoughts**.
  - Any relation called **Goals** points to **Notebooks**. The title property of Notebooks is still called **Goal**.
- Every view in every database is named "Notes". Find a database by its URL or data source id (see the appendix), not by its view name.
- Most databases have many empty leftover columns. Use only the properties named in each section below. See "Ignore these".
- Pages Leo types himself often have no title, so they show up as "New page" or "Untitled". Searching by title will not find them.
- The skill `leo-notion-system` still describes the older layout, where Atomic, Ideas, Projects and Goals were separate databases. This file is newer.
- If rows-mode or SQL queries hit Notion's usage limit, view-mode queries and page fetches still work.
- Follow the Rules on every task.

## Rules

1. **Keep his words exactly.** Never summarize, reword, fix typos or delete his text. A new page title is a phrase copied word for word from his text.
2. **Never delete anything in Notion.** Notes pages are never deleted. They are only marked Processed.
3. **His text stays plain.** Text he did not write (AI answers, pasted articles) goes in a **gray callout** whose first line is bold: `Pasted · <source> · <date>`. Something someone else wrote, pasted in as is, counts as pasted. What he types in his own words about someone's tip is his text and stays plain. Claude's own notes on his pages go in a **blue callout**. Never fold a callout, and never use toggles.
4. **Never mark anything dropped, done or reached.** Only he does that.
5. **Keep insights about him apart from general ones.** In Thoughts, use About = Me or General.
6. **He only writes and asks.** Never give him fields to fill or review queues. If he does not answer a question, go with your proposal and say that you did.
7. **Keep it simple.** Do not create pages, databases, views or properties he did not ask for. Do not invent tasks from wants.
8. **Do not write as "I" meaning him, and never name a page "My ...".** (The old rule against using the word "notebook" is retired: he named a database Notebooks himself.)
9. **Keep repeats.** Do not merge them unless he asks.
10. **Never delete or recreate a board view, and do not change its grouping.**
11. **His old Obsidian vault (vault-main) is read-only.** Never open or copy anything in its `08 Resources` folder (it holds credentials).
12. **When answering a question, search in this order:**
    1. His own words: Notes and Thoughts. Reminders, goal-row bullets and entries in project or topic pages also hold his words, except text in a gray Pasted callout, rows tagged Pasted from AI, and Inbox = Resources entries. Treat those as Resources.
    2. Resources.
    3. Outside knowledge.

    Quote him with the date and a link. Label outside knowledge and your own inferences as such.

## The big picture

**Notes is the inbox.** Everything that comes to mind goes there first. In his words: *"the notes page is for everything that comes to mind and then I plan with your help process it/save it for potential future reference of what things I have said or thought of."*

**He processes notes with Claude's help.** Each piece of a note is copied word for word into the database where it fits, and linked back to the note. The Notes page itself stays unchanged as the record of what he said, and Processed gets ticked.

**Reminders hold what he must keep remembering.** In his words: *"they update over time, and the notes that are no longer needed as reminders usually end up in one of the other pages depending which it fits best, and usually it fits best goals"*. Goals have since turned into projects, so "goals" here now means project pages in Notebooks. Long-term things stay in Reminders under Timeline.

```
              anything that comes to mind
                          |
                          v
                  +---------------+
                  |     NOTES     |   inbox; his raw words stay here for good
                  +-------+-------+
                          |  processing with Claude:
                          |  copy pieces word for word, link back, tick Processed
     +-----------+--------+---+-----------+------------+
     v           v            v           v            v
 NOTEBOOKS    THOUGHTS      TASKS     REMINDERS    RESOURCES
 projects +   ideas with    things    ideas, goals pasted info,
 topics, each no project    to do     etc. to keep kept separate
 with its own or topic                remembering  (some lives in
 database                                          project/topic
                                                   pages)
     ^                                    |
     +----- reminders no longer needed ---+
            -> wherever fits best, usually a project (goals are projects now)

 Venting with nothing to file stays in Notes (still ticked Processed).
```

## Where does it go?

Use this table when filing one piece of a Notes page.

| The piece is... | Put it in | Notes |
|---|---|---|
| A thought about a project or topic that has its **own database** (new-style page) | That page's database, Inbox = **Notes** | On the Notes page, add the project or topic page to its **Goals** relation. |
| A thought about an **old numbered row or goal row** (no database inside) | **Thoughts**, linked to that row through **Goals** | This is how filing has worked until now. |
| A thought with no project or topic | **Thoughts** | Fill Type, About (insights only), Topic, Area, Written, Voice note, From, and Topic page if a hub fits. |
| Pasted info (AI answer, article) | **Resources** by default (*"usually all the pasted information I try to keep separate"*). Use a project or topic page's database (Inbox = **Resources**) only when the paste is only about that one page (*"some of this info may live in projects/notebooks"*). | Put it in a gray "Pasted" callout. The Notes page keeps the raw paste. |
| Something he says to do | **Tasks**. If it belongs to one project or topic page, use that page's database instead, with Inbox = **Tasks**. | Only things he says to do. Never turn a want into a task. |
| Something to keep remembering | **Reminders**. If it only matters for one project or topic page, use that page's database instead, with Inbox = **Reminders**. | Entries there don't appear in the Reminders database. |
| A reminder he says is no longer needed as a reminder | Wherever it fits best, usually the matching project page in Notebooks (its database) | Copy word for word and link through Goals. The Reminders row stays. |
| A decision about a project or topic | That page's database, Inbox = **Decisions** | No decision fields exist yet. Store just his words. |
| A decision with no project | **Thoughts**, Type = Decision | This is how it has been done so far. |
| How to do something | A **guide** in the project or topic page's database (Inbox = **Guides**) | One complete page per subject, built from his words copied exactly (rule 1). Pasted how-to text goes in a gray Pasted callout, and any structure or summary Claude adds goes in a blue callout. If a guide for that subject exists, add to it and keep repeats (rule 9). If no project or topic page fits, file it in Thoughts and suggest a page. Never delete the source notes. |
| A goal | It is a project: the matching **project page** in Notebooks. If no project fits, propose one and ask before creating it | Goals are projects now. There are only tasks and projects. |
| Something long-term | **Reminders**, Template Notes = **Timeline** | Leo's rule for long-term things. |
| Venting, or a piece that fits no other database | It **stays in Notes**, which already keeps it for future reference | Still tick Processed. |

### How to process a note

1. Find the Notes rows where **Processed** is unticked.
2. Read the body and split it into pieces by meaning. Do not change the note.
3. File each piece using the table above. Copy his words exactly, and make the title a phrase copied from them.
4. Link back to the note. In Thoughts and Resources, set the **From** relation. In Tasks, Reminders and Notebooks rows, set the **Notes** relation. The matching relation on the Notes page fills itself. Entries in a project or topic page's own database cannot link back, so add the project or topic page to the note's **Goals** relation instead.
5. Tick **Processed**.
6. Tell him what went where, with links. Ask any questions, and if he does not answer, go with your proposal.

---

## Notes

**Purpose:** *"everything that comes to mind"*. It is the inbox and the permanent record of what he said. It holds about 265 rows, most of which were moved in from Obsidian on 2026-10-14. Notes are written in English and Spanish.

**What goes in:** anything he writes or dictates, and things he pastes. **What does not:** nothing is filed here by Claude. Processed pieces go to the other databases.

| Property | Type | Use |
|---|---|---|
| Note | title | Notes he types himself are untitled ("New page"). Pasted AI answers are titled `Pasted: <first words>…`. |
| Processed | checkbox | The inbox flag. Its description reads: *"Ticked once Claude has filed what is in this note. The note itself is never changed or deleted"*. |
| Written | date | When he wrote it. Some older rows have only the day. It is empty on notes he types directly, so use Created time for those. |
| Created time | created time | The real date for new notes. For the rows moved in on 2026-10-14, this is the move date, not the writing date. |
| Atomic | relation → Thoughts | Thoughts made from this note. The reverse is Thoughts.From. |
| Goals | relation → Notebooks | Project and topic pages, and old goal and numbered rows, that this note fed. Set on almost every note processed since 2026-10-15. |
| Tasks | relation → Tasks | The reverse is Tasks.Notes. |
| Reminders | relation → Reminders | The reverse is Reminders.Notes. |
| Resources | relation → Resources | The reverse is Resources.From. Mostly used on "Pasted:" notes. |

**Views and templates:**
- There is one board view. It is grouped by an empty select, so every card sits in one column, sorted newest first.
- Its cards show leftover columns, not the live relations.
- There are no templates.

**Page bodies:** the note itself is in the body. Properties are only used for linking. There are four layouts:
1. **Typed by him:** no title, one to a few plain paragraphs.
2. **Old journal entries:** long first-person paragraphs, sometimes opening with a bold date line such as `**Oct 6**`.
3. **Pasted AI answers:** the whole paste sits inside a gray 📋 callout, and the note is linked to a Resources page, which holds the filed copy.
4. **Longer voice-style dumps:** a sentence title, a date-only Written value, and the speech split into short `##` sections. These were created in batches, apparently by Claude.

The body never contains links. All connections are made through relations.

## Reminders

**Purpose:** *"making sure that I constantly remember the ideas, goals, etc that I should be reminding myself of. they update over time"*. It holds about 100 rows.

**What goes in:** rules to re-read, ideas, goals and motivation he wants in front of him. **What does not:** things to do, which go to Tasks, and ideas he doesn't need reminding of. Those go to the project or topic page they belong to, or to Thoughts if they have none.

| Property | Type | Use |
|---|---|---|
| Reminder | title | A phrase copied word for word from his text, usually the first sentence. |
| Area | select | The 9 areas (see Shared values). |
| Tags | multi-select | Options: Very important, Rule, Just start, Do the hard things, Keep it simple, People, Motivation, Helping others, Confidence, Mindset, Structure, Meaning & faith, Pasted from AI. The description says: *"Very important means you marked it so yourself. Rule is a note from your Rules to re-read. Pasted from AI is text you pasted from an AI chat, not your words."* Rows usually have 1–2 tags. Only he sets Very important. |
| Written | date | When he wrote it, if known. |
| Date is approximate | checkbox | Ticked when the source date had a "~". |
| How often | select | Options: Daily, Every 3 days, Weekly, Monthly, Yearly. Meant as the re-read cadence, but only 4 rows have a value (all Daily). |
| Template Notes | select | Options: Timeline, Important. The view groups by it. **Timeline** is where long-term things go (Leo, 2026-10-19). Important: not described yet. |
| Notes | relation → Notes | The source note. |
| Atomic | relation → Thoughts | |
| Goals | relation → Notebooks | |
| Tasks | relation → Tasks | Rarely used. |
| From | text | Where the row sat in Obsidian before the move. This is a record only. New rows use the Notes relation instead. |

**Views and templates:**
- There is one board view, grouped by Template Notes. No card properties are shown.
- There are no templates.

**Page bodies:** short, in his own words, verbatim. The layouts are:
- **"Rules to re-read" rows:** open with a short `##` heading, followed by the transcript.
- **Rows from old Obsidian notes:** plain paragraphs, often with a bold lead line.
- **Pasted AI rows:** a gray callout headed `**Pasted · AI**`, tagged Pasted from AI.

The body has no links.

**Lifecycle:** reminders *"update over time"*: new ones come in from Notes, and *"the notes that are no longer needed as reminders usually end up in one of the other pages depending which it fits best, and usually it fits best goals"*. When he says a reminder is no longer needed as a reminder, copy it word for word to where it fits best (usually its project page, linked through the reminder's Goals relation) and tell him where it went. Never decide by yourself that a reminder is no longer needed. Never delete it (rule 2) and never reword it (rule 1). Nothing marks a reminder as moved yet, so the row stays in Reminders. Tell him that, and don't add a property unless he asks (rule 7).

## Tasks

**Purpose:** *"tasks.. well usually pretty self explanatory"*. It holds about 790 rows. About 600 of them were imported from Obsidian vault-main on 2026-10-12 and are marked Origin = Old pending.

| Property | Type | Use |
|---|---|---|
| Task name | title | A phrase copied word for word from his text (rule 1). |
| Status | status | Options: To-do, Doing, Block, Soon, Done✔. Two quirks: Done✔ sits in Notion's To-do group, so Notion counts nothing as complete. Block appears to be the default for new pages, so Block does not reliably mean "blocked". |
| Someday | checkbox | *"Not necessary or urgent right now. Shown in the Someday view."* |
| Area | select | The 9 areas. |
| Template Notes | select | Options: Money, Urgent. Despite its name it is in use as a category, and both views group by it. |
| Type | select | Options: Task, Habit. |
| Do on | date | The day he plans to do it. |
| How often / Last done | select / date | Used on habits only. How often options: Daily, Weekly. |
| Parent item / Sub-item | self relation | Nests sub-tasks under the numbered parent tasks, for example "9.3 Sorting out my car and transportation". |
| Goals | relation → Notebooks | |
| Atomic | relation → Thoughts | |
| Notes | relation → Notes | The source note. |
| Resources | relation → Resources | |
| Reminders | relation → Reminders | Rarely used. |
| Why | text | One line on why it matters. Set on 2 rows. |
| AI reason | text | Notes from an earlier AI review about duplicates and overlaps. |

**Views:**
- **Pending** shows rows where Someday is unticked.
- **Someday** shows rows where Someday is ticked.
- Both are boards grouped by Template Notes, sorted newest first, with sub-items nested. Neither filters on Status.

**Templates:** none. A Task type property (Simple/Complex) was planned but never used.

**Habits:** a habit is a row with Type = Habit and uses How often, Do on and Last done. There are 3 habit rows.

**Page bodies:** the layout depends on where the row came from.
- Sub-tasks are to-do checkboxes.
- Pages Claude cleaned up have a `## Sub-tasks` section with priority `###` headings (such as `### 🔴 Now`), his original words indented under each to-do, then `---` and `## Notes`.
- The numbered parent tasks have blank bodies.
- Some imported bodies still contain Obsidian `[[wikilinks]]` as plain text.

**Old numbered rows living here:** 14 numbered parent tasks from the old setup were never moved and still sit in Tasks: 1.3, 2.3, 2.4, 3.3, 3.5, 4.1, 4.2, 4.3, 5.3, 8.1, 8.2, 9.2, 9.3 and 9.5.

## Notebooks

**Purpose, in his words:** *"this one has projects and then my topics of curiosity/expertise/interest. the projects will use a different icon than the topic pages"* / *"inside of each page is its own database with different tags depending on the type of note i write, it can have its own tasks, reminders, decisions, which is info about what decisions have i made related to that project, and guides which is like complete pages that let me know how to do something instead of a separate note, the rest is pretty self explanatory"*

He also said: *"when i say projects i just mean the template under notebooks that uses the flag icon instead of the notebook icon."*

### What is in the database today

| Kind of row | How to recognise it | Count |
|---|---|---|
| **New project page** | Flag icon (custom emoji `goal--4-`). The body is the page's own database. | 2: "Organizing The Notion System" and "Elizabeth April Knowledge" |
| **New topic page** | Notebook icon (custom emoji `book--2-`). The body is the page's own database. | 0 so far |
| Old numbered row (from the old Projects database) | No icon. Title in the form `N.M Name`, for example "2.1 Finding a job I can sustain". Has a Status. Goal rows are nested under it. | 32 |
| Old goal row | No icon. A sentence title. Has State, Times written, and First/Last written dates. The body is bullets of his quotes. | 160 |

**The icon is the only thing that separates a project from a topic.** No property records it. "Elizabeth April Knowledge" has the flag icon, so by his definition it is a project. Don't change its icon.

### Making a new page

Create a project or topic page only when he asks for one (rule 7). If a piece of a note has no home, file it in Thoughts and suggest a new page in your reply.

| For a new... | Use the template | Icon | Template id |
|---|---|---|---|
| Project | "New page" (the default) | flag `goal--4-` | `3fd30e5e-46f9-80ad-9ed1-c103e5a53542` |
| Topic of curiosity, expertise or interest | "New page" | notebook `book--2-` | `3fe30e5e-46f9-8014-a279-d20d6720102a` |

How the templates work:
- Both templates are untitled.
- Each template's body is a single inline database and nothing else.
- Every page made from a template gets its **own fresh copy** of that database, with its own data source. It is not a linked view of a shared database.
- The copy is named `(Database) Organizing The Notion System (1)`. It is a copy of the database on the "Organizing The Notion System" page, and nobody has renamed it on the new pages.

### The page's own database

| Property | Type | Values |
|---|---|---|
| Name | title | Existing entries are untitled. New entries get a phrase copied from his text (rule 1). |
| **Inbox** | select | Tasks, Resources, Notes, Reminders, Decisions, Guides, Roadmap. This is the kind of entry, one per entry. |
| Status | status | To-do group: Hold, Later, To-do, Now, Soon, Whenever, Potential, Dropped. In progress group: In progress. Complete group: Done. |
| Date, Due date | date | |
| Parent item / Sub-item | self relation | For nesting entries. |

What the Inbox tags mean:
- **Tasks:** things to do for this project or topic.
- **Reminders:** things to keep remembering about it.
- **Decisions:** *"info about what decisions have i made related to that project"*. His planning note (an entry in the [Organizing The Notion System database](https://app.notion.com/p/3fa30e5e46f9800a8cd1ec0832354a3d); see Existing entries below) asks for when the decision was made, what type it is, and any conflicts, all kept as properties. Those properties do not exist yet. Don't add them unless he asks (rule 7).
- **Guides:** *"complete pages that let me know how to do something instead of a separate note"*. His planning note describes one combined page per subject, for example hair loss.
- **Notes:** plain thoughts about the project or topic. This is inferred: he said *"the rest is pretty self explanatory"*.
- **Resources:** pasted info that belongs to this project or topic (inferred, one of "the rest").
- **Roadmap:** he didn't name it, so it is one of the tags covered by *"the rest is pretty self explanatory"*. His planning note describes a roadmap as direction by month, year and decade.

**View:** one board named "Notes", grouped by Inbox. Cards show Name and Status. Do not change its grouping.

**No links out:** this database has no relations to the six main databases. An entry here does not appear in Tasks or Reminders, and it cannot link back to its Notes page through a property.

**How to add an entry:**
1. Fetch the project or topic page and find its inline database (its data source id).
2. Create a page in that database. The body is his words, exactly. Pasted text goes in a gray callout.
3. Set the title to a phrase copied word for word from his text, and set **Inbox** to the kind of entry.
4. Leave Status alone unless his words give one. Never set Done or Dropped.
5. On the source Notes page, add the project or topic page to the **Goals** relation, then tick Processed.

**Existing entries:**
- "Organizing The Notion System" has 4 entries, all Inbox = Tasks. They are his plans for this system, so read them before changing any structure.
- "Elizabeth April Knowledge" has 1 entry with no Inbox tag.

### Old goal rows and old numbered rows

Notebooks used to be the Goals database and was renamed, which is why its title property is "Goal". The old Projects database was moved into it and is now in the trash.

**Old numbered rows (32, from the old Projects database):**
- They are numbered by Area number plus an index, from 1.1 to 9.4.
- 30 are Paused and 2 are Active: "2.1 Finding a job I can sustain" and "2.2 Getting out of debt and reducing expenses". Both Active rows have Why and Start (2026-10-13) set.
- They have no icon and no database inside, and most bodies are blank.
- Properties: Status (Active, Paused, Someday, Done), Why (*"One line: why this matters right now"*), Start.

**Old goal rows (160):**
- 104 of them are nested under an old numbered row through Parent item.
- Properties:
  - **State:** Likely still active, Quiet since before September, Changed, or Maybe reached or let go (not confirmed). The value depends on when he last wrote about the goal.
  - **Times written:** a number.
  - **First written / Last written:** dates.
  - **Date is approximate:** checkbox.
  - **Obsidian project:** text, a record from the move.
- Body: a bulleted list of his own words in curly quotes. Each bullet is followed by gray text giving the date or the title of the source note.

**Goals have turned into projects** (Leo, 2026-10-19). The old goal rows are leftovers from before: read them for his words, but don't add new goal rows. A new goal is a project page; something long-term goes in Reminders under Timeline. Never change State or Status to reached, done or let go (rule 4).

**Shared properties:**
- Area: set on the old rows, empty on the new pages.
- Atomic → Thoughts, Notes → Notes, Reminders → Reminders, Tasks → Tasks.
- Parent item / Sub-item.

**View:** one table, unfiltered, with sub-items nested. New rows default to the project template.

## Thoughts

**Purpose:** *"a page with all my processed notes that don't have a project/notebook to live in, usually separate ideas or something like that. or what others call atomic notes."* It holds about 350 rows. It used to be called "Atomic".

Rows by Type:
- **Atomic thoughts** (about 285): Insight, Want, Decision, Problem, Question, Experience.
- **Topic page** (42): hub pages. These are long pages carried over from Obsidian project notes, with `# Clarity`, `# Epiphanies` and `# Reminders` sections. Thoughts link to them through "Topic page".
- **Page** (25): long-form pages built around a group of tasks (for example "Side hustles and reselling"), plus "Vision".

Only the atomic rows match his description of Thoughts. Hubs and Pages were carried over from Obsidian.

| Property | Type | Use |
|---|---|---|
| Note | title | On atomic rows, a sentence lifted word for word from the body. |
| Type | select | See the list above. |
| About | select | Me, General. Description: *"For insights: about you, or about life in general"*. Set on every Insight. |
| Topic | select | Business, Habits, Health, Mindset, Money, People, Places, Self, Spirituality, Work. |
| Area | multi-select | The 9 areas. Usually 1–2 values. |
| Written | date | Date only. |
| Voice note | checkbox | Ticked when the thought was transcribed from speech. |
| From | relation → Notes | Exactly one source note per atomic row. |
| Topic page | self relation | Links to one or more hub rows. The reverse is "On this topic". |
| Goals | relation → Notebooks | |
| Tasks | relation → Tasks | |
| Reminders | relation → Reminders | |
| Resources | relation → Resources | Used on hubs only. |
| Private | checkbox | Ticked on 1 row. Meaning unclear. |

**Views and templates:**
- There is one board view, grouped by an empty select, so all cards sit in one column with no properties shown.
- There are no templates.

**Page bodies:**
- **Atomic thoughts:** one short paragraph of his words. Typed ones sometimes have the key sentence in bold. Voice-note ones open with a short `##` heading, followed by the transcript. There are no links in the body.
- **Hubs:** entries under `##` or `###` headings with italic date lines such as `*2026-08-25*`. Spanish sections are flagged by a blue 🤖 callout headed `**Claude · note from an earlier import**`. Lines like `↳ Tasks moved to Notion: …` link to Tasks.

**Overlap with Notebooks:** the hubs repeat old numbered rows that now sit in Notebooks. For example, the hub "Finding where I want to live longterm" holds about 45k characters, while the old numbered Notebooks row "9.4 Finding where I want to live longterm" is blank.

## Resources

**Purpose:** *"usually all the pasted information I try to keep separate but some of this info may live in projects/notebooks"*. It holds about 147 rows, most of them saved AI answers.

| Property | Type | Use |
|---|---|---|
| Resource | title | Existing rows have descriptive titles. Consolidated pages end in " - Insights" or " - Protocols". A new row's title follows rule 1, a phrase copied word for word from his text. If he wrote nothing with the paste, use `Pasted: <first words>…` as on Notes. |
| Kind | select | AI answer, Claude research, Page from Tasks. There is no option yet for text from a person or a website. |
| Saved | date | *"When you saved it"*. |
| Area | multi-select | The 9 areas. Always exactly one value. |
| Topic | select | The same 10 options as in Thoughts. |
| Atomic | relation → Thoughts | Every row links to exactly one Topic page hub. |
| From | relation → Notes | The source note (newer rows). |
| Tasks | relation → Tasks | |

Resources has **no relation** to Notebooks or Reminders.

**Views and templates:**
- There is one board view, grouped by an empty select, so all cards sit in one column.
- There are no templates.

**Page bodies:** the callout style tells you where the text came from.
- **Pasted text:** a gray callout with a 📋 icon. The first line is bold, for example `**Pasted · AI · Aug 10**`. Variants include `Pasted · Claude` and `Pasted · source not given · Oct 16`.
- **Claude's notes:** a blue callout with a 🤖 icon. The first line is bold: `**Claude · Oct 17**` or `**Claude · note from an earlier import**`.
- **His own writing:** plain paragraphs outside any callout.
- **Consolidated pages:** numbered `#` sections (such as `# 1. Medication`), a `##` heading per question, an italic date line, and then the callout. A `---` divider separates unrelated pastes.

---

## Shared values in use

**Area** is used in Reminders and Tasks (select), Notebooks (select, old rows only), Thoughts (multi-select) and Resources (multi-select, one value). It is not used in Notes or in the project and topic page databases. Its values:

- 1 Direction
- 2 Money & Job
- 3 Businesses
- 4 Health & Looks
- 5 Identity
- 6 Relations
- 7 Habits & Routine
- 8 Mundanes
- 9 Environment

**Topic** is used in Thoughts and Resources. Its values are Business, Habits, Health, Mindset, Money, People, Places, Self, Spirituality, Work. A second Topic list ("Work · Money in", "Place · Base", and so on) exists in other databases but is empty. Ignore it.

## Ignore these

Do not fill these columns, do not rely on them, and do not delete them. Cleanup is Leo's call.

| Where | Leftover columns |
|---|---|
| All six databases | Claim, Original Notes, Layer, Reviewed, Select, Time, Source, Task type, Task type 1, Date, Due date, Template Tasks, Status 1 (called "Template Status 1" in Tasks; always "Not started"), Projects (moved), and every relation whose name ends in "(old)" |
| Notes | Kind, State, Status, Type, Topic, the empty "Notes" select, Parent item, Sub-item |
| Reminders | Kind, State, Status, Type, Topic, Parent item, Sub-item. From is a record only. |
| Tasks | Kind, State, Topic, Area 1, Written 1, Voice note, Template Status, Template Topic, Template Type, Assignee. Description, Origin, Last written and Journal date are import records only. |
| Notebooks | Kind, Type, Topic, Target, Template Notes. Obsidian project is a record only. |
| Thoughts | Kind, State, Status, the empty "Notes" select, Parent item, Sub-item. Note: 8 rows link to a project **only** through Projects (moved), so keep that column. |
| Resources | State, Status, Type, the empty "Notes" select, Parent item, Sub-item |
| Project and topic page databases | the "Tasks" select (Now/Soon/Later/Maybe), State, Type, Kind, Layer, Topic, Time, Source, Reviewed, Select, Task type, Task type 1, Claim, Original Notes |

**Legacy databases.** All of these are in the trash and empty. Do not restore them or use them.

| Name | Data source id |
|---|---|
| Projects (emptied after the move) | `collection://47330e5e-46f9-822c-a444-8712a8226466` |
| Atomic (old) | `collection://cbb37999-b611-429c-b09a-c7454523c16e` |
| Ideas (old) | `collection://dfcccef9-dae7-4ee6-be1a-9288fbec27ca` |
| Resources (old) | `collection://0315e595-76a7-47d9-9e5d-51e8303563f3` |
| Tasks (old) | `collection://3eb30e5e-46f9-8036-a972-000bfa87308c` |
| Projects (old) | `collection://232b68d1-6d29-40c0-a4f6-3a73ba96a377` |
| Goals (old) | `collection://3a4a0fae-d643-4bb4-96f1-406bba5947bb` |
| Reminders (old) | `collection://bf2f65b2-b0a0-48fd-9065-048e7041d40d` |
| Notes (first generation) | `collection://a96648f5-173c-4cf0-b785-3b96ff16e2d2` |

## Still being built

This is a list of what is unfinished, not a to-do list. Don't fix, rename, regroup, merge, move, retitle or create anything listed here unless Leo asks (rules 1, 7, 9, 10), and don't turn any of it into tasks. He said he will try to figure out the more specific structure of each page next.

**What Leo said:** he thinks the main structure is in place for now, and a lot is still unfinished.

**Notebooks:**
- No topic (notebook icon) pages exist yet.
- The templates are untitled, and every page database is still named `(Database) Organizing The Notion System`.
- Entries are untitled.
- The page databases do not link to the main databases.
- Decisions have no fields yet.
- His planning note also mentions an "Introspection" page (everything about him) and Areas pages, each with its own database. Neither exists. Don't create them unless he asks.

**Goals:** goals are projects now, but the 160 old goal rows still sit in Notebooks next to 32 old numbered rows. They haven't been turned into project pages yet.

**Content from the old numbered projects is split across three places (none of it is a project in Leo's sense yet):**
- 32 old numbered rows are in Notebooks.
- 14 are still parent tasks in Tasks.
- 42 Thoughts hubs hold most of the content.

**Relation names are out of date:**
- "Atomic" means Thoughts.
- "Goals" means Notebooks.
- "Projects (moved)" points to a trashed database.

**Views:** every view is named "Notes". Notes, Thoughts and Resources group by an empty select, so they show one column. Most cards show leftover columns.

**Tasks:**
- Done✔ sits in the To-do group, and Block appears to be the default status.
- 34 idea rows from 2026-10-14 (for example "I have a backup plan") use Thoughts fields and look like thoughts filed as tasks.
- The statuses of the Old pending imports were not carried over consistently.
- Recent captures hold raw text in the title, and some are untitled.

**Reminders:**
- How often is almost never set.
- There is no way to mark a reminder as retired or moved.
- 5 untitled rows (2026-10-14 to 10-16) were typed straight into Reminders and are not processed.

**Thoughts vs Notebooks:** Leo's description settles where new content goes. Thoughts is for *"processed notes that don't have a project/notebook to live in"*, so anything about a project or topic page goes in that page's database. The 42 Topic page hubs and 25 Page rows in Thoughts come from the old setup and don't match his description. Leave them where they are, and don't move, copy or split their content unless he asks.

**Resources:**
- Kind has no option for non-AI pastes.
- There are near-duplicates (kept under rule 9).
- The Saved date is missing on 23 rows.

**Taxonomies do not match:**
- There are two Topic lists.
- Area is a multi-select in Thoughts and Resources, but a single select elsewhere.

**Scheduled Claude tasks:** Leo will redo them later. Ignore the existing ones.

---

## Appendix: IDs

| Database | URL | Data source | Title property |
|---|---|---|---|
| Notes | https://app.notion.com/p/3fa30e5e46f9800f9985c0b313f8f42a | `collection://7f630e5e-46f9-83c9-9856-07a8163e2bb6` | Note |
| Reminders | https://app.notion.com/p/3e230e5e46f9803487befad583763611 | `collection://f1830e5e-46f9-83f1-a64f-0733b0f703f8` | Reminder |
| Tasks | https://app.notion.com/p/3fa30e5e46f98092a4d4f4bcdf467aba | `collection://05330e5e-46f9-82d4-91fb-8759c2c55cdb` | Task name |
| Notebooks | https://app.notion.com/p/3fa30e5e46f980418e38c55e8890b1f1 | `collection://3df30e5e-46f9-824a-a7d6-07e6cd262afb` | Goal |
| Thoughts | https://app.notion.com/p/3fa30e5e46f9807f8d6af86089c196c6 | `collection://e1c30e5e-46f9-8332-9633-8766ed4e4f48` | Note |
| Resources | https://app.notion.com/p/3fa30e5e46f980628b41da580ddb4448 | `collection://4fb30e5e-46f9-833c-aa62-8788dd9c354b` | Resource |

**Views:**

| Database | View | View id |
|---|---|---|
| Notes | board | `view://cc130e5e-46f9-835c-9758-08e6f866b881` |
| Reminders | board | `view://02f30e5e-46f9-830d-9839-8834617d0bf9` |
| Tasks | Pending | `view://7ac30e5e-46f9-83ac-b2ca-887ae3646a14` |
| Tasks | Someday | `view://3fa30e5e-46f9-8017-8492-000c1ad7736b` |
| Notebooks | table | `view://fc930e5e-46f9-82dd-bbf8-8844be8aecf1` |
| Thoughts | board | `view://e3730e5e-46f9-8390-97b7-88e7032442b1` |
| Resources | board | `view://bcc30e5e-46f9-8259-8c97-886dbeb6d5d8` |

**Notebooks templates and page databases:**

| Item | Page | Its own database | Data source |
|---|---|---|---|
| Project template (default, flag `goal--4-`, emoji id 19f30e5e-46f9-80fc-8eca-007a6f014866) | https://app.notion.com/p/3fd30e5e46f980ad9ed1c103e5a53542 | https://app.notion.com/p/3fd30e5e46f9806f8279c3689d4700e1 | `collection://c9730e5e-46f9-8211-8497-875df56651cd` |
| Topic template (notebook `book--2-`, emoji id 2b130e5e-46f9-80fd-83ba-007a6efcef79) | https://app.notion.com/p/3fe30e5e46f98014a279d20d6720102a | https://app.notion.com/p/21a30e5e46f9822c84aa812e2c55c089 | `collection://29d30e5e-46f9-83d8-ac51-077e0eba5aaa` |
| Organizing The Notion System (project) | https://app.notion.com/p/3fa30e5e46f9807f8068ca9eea2574b0 | https://app.notion.com/p/3fa30e5e46f9800a8cd1ec0832354a3d | `collection://03130e5e-46f9-82ab-8ff5-87d3d8857812` |
| Elizabeth April Knowledge (flag icon) | https://app.notion.com/p/fa230e5e46f98254bfa4815af1ba73de | https://app.notion.com/p/8ad30e5e46f9834b8d2d81bbddb32aa0 | `collection://f7330e5e-46f9-83af-ac41-073ea7e6ee4e` |

