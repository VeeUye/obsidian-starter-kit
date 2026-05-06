<%*
const today = tp.date.now("YYYY-MM-DD");
const yesterday = tp.date.now("YYYY-MM-DD", -1);
const tomorrow = tp.date.now("YYYY-MM-DD", 1);
await tp.file.rename(today);
-%>
# <% tp.date.now("dddd D MMMM YYYY") %>

[[<% yesterday %>|← Yesterday]] | [[Tasks Dashboard]] | [[<% tomorrow %>|Tomorrow →]]

## 🎯 Focus today

*Top 1–3 intentions. Not task copies — what you want to move forward.*

- 
- 

## 🤝 Meetings

*Meetings scheduled for today auto-appear below. Paste live links (Zoom, Meet, calendar invites) in the Quick links area.*

```dataview
LIST
FROM "Meetings"
WHERE dateformat(Date, "yyyy-MM-dd") = dateformat(date(today), "yyyy-MM-dd")
SORT file.ctime ASC
```

**Quick links**
- 

## ⚠️ Still open from earlier

```tasks
not done
path includes Daily
path does not include <% today %>
path does not include Archive
path does not include Templates
path does not include _Personal
short mode
hide backlink
hide edit button
hide task count
```

## 📌 Active project tasks

```tasks
not done
path includes Projects
(due before in 7 days) OR (no due date)
path does not include Archive
path does not include Templates
path does not include _Personal
group by filename
short mode
hide backlink
hide edit button
hide task count
limit 15
```

## ✅ Ad-hoc tasks

*Only things that don't belong to a project. Project tasks go in the project note.*

## 📝 Log

*What happened today — meetings, decisions, wins, blockers.*

- 

## 🧠 Notes & ideas

- 
