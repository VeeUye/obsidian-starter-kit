# Obsidian Starter Kit — Setup Guide

A personal knowledge system built around one idea: **write once, surface everywhere**. Tasks live in exactly one note; dashboards and templates do the surfacing. No copy-forward, no duplication, one source of truth per thing.

---

## What's in the box

### Community plugins

| Plugin | Version | Purpose |
|---|---|---|
| **Templater** | 2.19.0 | Smart templates with prompts, auto-rename, date substitution, folder auto-assignment |
| **Dataview** | 0.5.68 | Query-driven dashboards — tables and lists pulled from note metadata |
| **Tasks** | 7.23.1 | Task management with due dates, done dates, custom statuses, and vault-wide queries |

### Core plugins in use

Daily Notes, Backlinks (inline), Properties, Graph, Bookmarks, File Explorer, Global Search, Quick Switcher, Outline, Word Count, Canvas, Bases, Sync, Note Composer, File Recovery.

Core **Templates** plugin is **disabled** — Templater replaces it and they conflict.

### Folder structure

```
Daily/             ← one note per workday (YYYY-MM-DD), auto-created on startup
Meetings/          ← one note per meeting, auto-populated from templates
Projects/          ← one note per project, tasks + context together
People/            ← one note per person, auto-links to meetings and open actions
Reviews/           ← weekly reviews, one note per week
CPD/               ← continuing professional development log entries
Reads/
  Fiction/
  Non-Fiction/
Templates/         ← all Templater templates — do not rename this folder
Archive/           ← dormant notes and old imports — excluded from all queries
_Personal/         ← personal mirror (Daily, Meetings, Projects, Reviews, Fitness)
```

### Templates

| Template | Trigger | What it does |
|---|---|---|
| `Daily Note` | Folder template for `Daily/` | Auto-renames to today's date, shows today's meetings, overdue tasks, active project tasks |
| `Meeting Note` | Hotkey / manual | Prompts for name and date, links back to that day's daily note |
| `Standup` | Hotkey | Auto-renames, auto-moves to `Meetings/` — sections for each team area |
| `1-1 Meeting` | Hotkey | Prompts for person name, moves to `Meetings/`, updates Last contact in their People note |
| `Project Template` | Folder template for `Projects/` | Prompts for name, sets status and start date, sections for context, current focus, tasks, open questions, log |
| `Weekly Review` | Folder template for `Reviews/` | Prompts for week start, auto-populates completed tasks, meetings, active project status, CPD, carrying forward |
| `Person` | Folder template for `People/` | Prompts for name and optional nickname, shows linked meetings and open actions via queries |
| `CPD Entry` | Folder template for `CPD/` | Prompts for title, calculates total hours from session log |
| `Read` | Folder template for `Reads/` | Prompts for title and Fiction/Non-Fiction, moves to the right subfolder |
| `Transcript Summary` | Manual | AI prompt template — fill in context and paste a transcript |
| `Startup` | Runs on Obsidian open | Auto-creates today's work and personal daily notes if they don't exist yet |
| `Personal Daily Note` | Created by Startup | Personal mirror of the work daily note |

### Dashboards

- **Tasks Dashboard** (`Tasks Dashboard.md`) — Overdue, Today, This Week, High Priority (no date), Inbox (no due date), Upcoming (30 days), Completed This Week
- **CPD Dashboard** (`CPD Dashboard.md`) — Planned CPD, last 12 months, by skill, by type, all-time log

---

## One-time setup

### 1. Install the community plugins

Settings → Community plugins → turn off Restricted mode → Browse → install and enable:

- **Templater** (by SilentVoid)
- **Dataview** (by Michael Brenan)
- **Tasks** (by Clare Macrae and Ilyas Landikov)

### 2. Disable the core Templates plugin

Settings → Core plugins → find **Templates** → turn it **off**.

(Leave Daily Notes and Backlinks turned **on**.)

### 3. Configure Templater

Settings → Templater:

- **Template folder location**: `Templates`
- **Trigger Templater on new file creation**: ON
- **Auto jump to cursor**: OFF

**Folder Templates** — add one row per line below:

| Folder | Template |
|---|---|
| `Projects` | `Templates/Project Template` |
| `Daily` | `Templates/Daily Note` |
| `Reviews` | `Templates/Weekly Review` |
| `People` | `Templates/Person` |
| `CPD` | `Templates/CPD Entry` |
| `Reads` | `Templates/Read` |
| `_Personal/Meetings` | `Templates/Personal Meeting Note` |
| `_Personal/Projects` | `Templates/Personal Project` |
| `_Personal/Reviews` | `Templates/Personal Weekly Review` |

**Startup Templates** — add one row:
- `Templates/Startup`

**Enabled Templates Hotkeys** — add four rows in this order (you'll bind hotkeys to them):
1. `Templates/1-1 Meeting`
2. `Templates/Manager 1-1`
3. `Templates/Standup`
4. `Templates/Meeting Note`

### 4. Configure Daily Notes

Settings → Daily Notes:

- **Date format**: `YYYY-MM-DD` (don't change — ISO format is required for queries)
- **New file location**: `Daily`
- **Template file location**: `Templates/Daily Note`

### 5. Configure Tasks

Settings → Tasks:

- **Task format**: Tasks emoji format
- **Set done date on every completed task**: ON
- **Set cancelled date**: ON
- **Auto-suggest**: ON

**Custom statuses** — add these in Tasks settings under Status:

| Symbol | Name | Next symbol | Type |
|---|---|---|---|
| `/` | In Progress | `x` | IN_PROGRESS |
| `-` | Cancelled | ` ` | CANCELLED |

### 6. Configure Dataview

Settings → Dataview:

- **Enable JavaScript queries**: ON
- **Enable inline Dataview**: ON
- **Enable inline JavaScript queries**: ON
- **Render null as**: `\-`

### 7. Configure Backlinks

Settings → Core Plugins → Backlinks → **Backlinks in document**: ON

### 8. Bind hotkeys (optional but worth it)

Settings → Hotkeys:

| Search for | Suggested binding |
|---|---|
| `Daily notes: Open today's daily note` | `Cmd/Ctrl+D` |
| `Templater: Create new note from template` (1-1 Meeting) | your choice |
| `Templater: Create new note from template` (Standup) | your choice |

---

## Day-to-day workflow

### Every morning (2 minutes)

1. Open Obsidian — Startup template auto-creates today's work and personal daily notes.
2. Open **Task Dashboard**. Scan Overdue and Today.
3. Jot 1–3 intentions in today's daily note Focus section.

### Creating things during the day

**A new project** → right-click `Projects/` → New note → type the name when prompted. Template fires automatically.

**A meeting** → use the Meeting Note hotkey, or right-click `Meetings/` → New note. For standups, use the Standup hotkey — it renames and moves itself automatically.

**A 1:1** → use the 1-1 Meeting hotkey → type the person's name. It moves to `Meetings/` and updates the Last contact field in their People note automatically.

**A task**:
- Belongs to a project → open that project note, add `- [ ]` under Tasks → Active
- Doesn't belong anywhere → drop it in today's daily note under Ad-hoc tasks
- Meeting action item → write it as `- [ ]` in the meeting note — it surfaces in the dashboard automatically

**A new person** → right-click `People/` → New note → type name (and optional nickname). Their note auto-queries all meetings that link to them and all open tasks that mention them.

**CPD entry** → right-click `CPD/` → New note → type the course/resource name. Log sessions using the `Sessions` list format. Hours auto-total via Dataview.

**A book or article** → right-click `Reads/` → New note → prompted for title and category, auto-files to Fiction or Non-Fiction.

### Every Friday (15 minutes)

1. Right-click `Reviews/` → New note. Template prompts for the week start date and auto-populates everything.
2. Read the generated sections: completed tasks, meetings, active project status, CPD, what's carrying forward.
3. Fill in the prose sections: highlights, reflection, priorities for next week.
4. Use the **Prune & close** section — archive stalled projects, drop tasks no longer relevant. This step is the most important. Without it the system accumulates cruft.

---

## The three rules

1. **Every task lives in exactly one place.** Project note, daily note, or meeting note. Never copy forward. The dashboard finds everything.

2. **Daily notes are for capture, not for keeping.** Write once. If a task needs to persist, move it to a project note. If it doesn't, let it stay where it was born.

3. **When in doubt, delete rather than add.** Template field you never fill in? Remove it. Dashboard section too noisy? Delete it. The best setups are invisible.

---

## The `_Personal` split

Everything under `_Personal/` is a personal mirror of the work vault — same structure, separate queries. The Startup template creates both a work daily note (`Daily/YYYY-MM-DD.md`) and a personal one (`_Personal/Daily/YYYY-MM-DD-personal.md`) every morning.

All Tasks and Dataview queries in work notes include `path does not include _Personal` to keep them separate.

---

## Troubleshooting

**Template `<% %>` tags show as literal text in new notes**
- Settings → Templater → "Trigger Templater on new file creation" is ON
- Folder name in Folder Templates matches exactly (case-sensitive, no trailing slash)
- Core Templates plugin is disabled

**Daily note saves as "Untitled" instead of today's date**
- Use the Daily Notes command/hotkey, not right-click → New note
- Or rely on the Startup template — it creates both notes automatically on open

**Meetings don't appear in today's daily note**
- The daily note query matches files in `Meetings/` where the `Date` inline field equals today
- Check the meeting note has `**Date**:: YYYY-MM-DD` set correctly
- Folder must be named exactly `Meetings`

**Tasks plugin queries return nothing**
- Every Tasks query block needs its own `path does not include Archive` and `path does not include Templates` lines — filters don't carry between blocks

**Dataview tables show `\-` instead of a value**
- That's expected — it means the field isn't set on that note. Fill it in or remove the column from the query.

**1:1 template doesn't update Last contact in the person's note**
- The People note must exist at `People/<name>.md` with the exact same name you type in the prompt
- The `**Last contact::**` field must be present and formatted exactly as written in the Person template

---

## What's intentionally not included

- Monthly/quarterly reviews (add Periodic Notes plugin if you want them)
- Kanban boards (add Kanban plugin if you need visual pipelines)
- Time tracking, Pomodoro, habit tracker
- Tags as an organisational system (use folders + links instead)

Start with what's here. Add one thing at a time, only when you feel a specific friction. Most "improvements" made in the first week get reverted by week three.
