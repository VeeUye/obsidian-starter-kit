<%*
const defaultMonday = moment().startOf('isoWeek').format("YYYY-MM-DD");
const weekStart = await tp.system.prompt("Week starting (Monday, YYYY-MM-DD)", defaultMonday);
const weekEnd = moment(weekStart).add(6, 'days').format("YYYY-MM-DD");
const dayBeforeStart = moment(weekStart).subtract(1, 'days').format("YYYY-MM-DD");
const dayAfterEnd = moment(weekStart).add(7, 'days').format("YYYY-MM-DD");
const nextWeekEnd = moment(weekStart).add(13, 'days').format("YYYY-MM-DD");
const dayAfterNextWeekEnd = moment(weekStart).add(14, 'days').format("YYYY-MM-DD");
const twoWeeksBeforeEnd = moment(weekStart).subtract(8, 'days').format("YYYY-MM-DD");
const reviewName = `Personal Weekly Review - ${weekStart}`;
await tp.file.rename(reviewName);
-%>
# Personal Weekly Review: <% weekStart %> → <% weekEnd %>

## ✅ Completed this week

```tasks
done after <% dayBeforeStart %>
done before <% dayAfterEnd %>
path includes _Personal
description regex matches /\S/
group by filename
sort by done
short mode
hide backlink
hide edit button
hide task count
```

## 🗓️ Events & appointments this week

```dataview
LIST
FROM "_Personal/Meetings"
WHERE file.ctime >= date("<% weekStart %>") AND file.ctime <= date("<% weekEnd %>")
SORT file.ctime DESC
```

## 🗂️ Active personal projects

```dataview
TABLE
	status,
	started,
	length(filter(file.tasks, (t) => !t.completed)) AS "Open",
	length(filter(file.tasks, (t) => t.completed AND t.completion >= date("<% weekStart %>") AND t.completion <= date("<% weekEnd %>"))) AS "Done this week"
FROM "_Personal/Projects"
WHERE contains(lower(string(status)), "active")
SORT file.name ASC
```

## ⏭️ Carrying forward

```tasks
not done
due before <% dayAfterNextWeekEnd %>
path includes _Personal
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

*Anyone you haven't been in touch with? Anyone to reach out to?*

```dataview
TABLE last-contact
FROM "People"
WHERE context = "personal" AND last-contact < date("<% twoWeeksBeforeEnd %>")
SORT last-contact ASC
```

## 🏃 Fitness this week

*How did training go? Any patterns or progress worth noting?*

- 

## 🌟 Highlights & wins

*What went well? What are you proud of?*

- 

## 🧠 Reflection

*What didn't work? What felt draining? Any patterns you want to change?*

- 

## 🎯 Priorities next week (<% dayAfterEnd %> → <% nextWeekEnd %>)

1. 
2. 
3. 

## 🧹 Prune & close

*Any projects to archive? Commitments to drop?*

- 
