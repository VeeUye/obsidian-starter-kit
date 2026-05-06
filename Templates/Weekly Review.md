<%*
const defaultMonday = moment().startOf('isoWeek').format("YYYY-MM-DD");
const weekStart = await tp.system.prompt("Week starting (Monday, YYYY-MM-DD)", defaultMonday);
const weekEnd = moment(weekStart).add(6, 'days').format("YYYY-MM-DD");
const dayBeforeStart = moment(weekStart).subtract(1, 'days').format("YYYY-MM-DD");
const dayAfterEnd = moment(weekStart).add(7, 'days').format("YYYY-MM-DD");
const nextWeekEnd = moment(weekStart).add(13, 'days').format("YYYY-MM-DD");
const dayAfterNextWeekEnd = moment(weekStart).add(14, 'days').format("YYYY-MM-DD");
const twoWeeksBeforeEnd = moment(weekStart).subtract(8, 'days').format("YYYY-MM-DD");
const reviewName = `Weekly Review - ${weekStart}`;
await tp.file.rename(reviewName);
-%>
# Weekly Review: <% weekStart %> → <% weekEnd %>

## ✅ Completed this week

```tasks
done after <% dayBeforeStart %>
done before <% dayAfterEnd %>
path does not include Archive
path does not include Templates
path does not include _Personal
description regex matches /\S/
group by filename
sort by done
short mode
hide backlink
hide edit button
hide task count
```

## 🤝 Meetings this week

```dataview
LIST
FROM "Meetings"
WHERE file.ctime >= date("<% weekStart %>") AND file.ctime <= date("<% weekEnd %>")
SORT file.ctime DESC
```

## 🗂️ Active projects

```dataview 
TABLE 
	status, 
	started, 
	length(filter(file.tasks, (t) => !t.completed)) AS "Open",
	length(filter(file.tasks, (t) => t.completed AND t.completion >= date("<% weekStart %>") AND t.completion <= date("<% weekEnd %>"))) AS "Done this week" 
FROM "Projects" 
WHERE contains(lower(string(status)), "active") 
SORT file.name ASC 
```

## ⏭️ Carrying forward

```tasks
not done
due before <% dayAfterNextWeekEnd %>
path does not include Archive
path does not include Templates
path does not include _Personal
description regex matches /\S/
group by due
sort by due
short mode
hide backlink
hide edit button
hide task count
```

---

## 🤝 Relationships

*Anyone you haven't connected with in a while? Anything to follow up on?*

```dataview
TABLE last-contact
FROM "People"
WHERE context = "work" AND last-contact < date("<% twoWeeksBeforeEnd %>")
SORT last-contact ASC
```

## 📚 CPD this week

```dataviewjs
const weekStart = dv.date("<% weekStart %>");
const weekEnd = dv.date("<% dayAfterEnd %>");
let weekTotal = 0;
const rows = [];
for (const p of dv.pages('"CPD"')) {
  const sessions = p.file.lists
    .filter(l => l.hours)
    .filter(l => {
      const match = l.text.match(/^(\d{4}-\d{2}-\d{2})/);
      if (!match) return false;
      const d = dv.date(match[1]);
      return d >= weekStart && d < weekEnd;
    })
    .array();
  if (sessions.length === 0) continue;
  const hrs = sessions.reduce((sum, l) => sum + Number(l.hours), 0);
  weekTotal += hrs;
  rows.push([p.file.link, p.skill, hrs]);
}
if (rows.length === 0) {
  dv.span("_No CPD logged this week._");
} else {
  dv.table(["Entry", "Skill", "Hrs"], rows);
  dv.paragraph("**Total: " + weekTotal + "h**");
}
```

## 🌟 Highlights & wins

*What went well? What are you proud of? What did you learn?*

- 

## 🧠 Reflection

*What didn't work? What felt draining? Any patterns you want to change?*

- 

## 🎯 Priorities next week (<% dayAfterEnd %> → <% nextWeekEnd %>)

*Top 3 things you want to move forward. Keep it realistic.*

1. 
2. 
3. 

## 🧹 Prune & close

*Any projects to archive? Tasks no longer relevant? Commitments to drop?*

- 
