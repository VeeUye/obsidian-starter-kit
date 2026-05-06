<%*
const today = tp.date.now("YYYY-MM-DD");
const yesterday = tp.date.now("YYYY-MM-DD", -1);
const tomorrow = tp.date.now("YYYY-MM-DD", 1);
await tp.file.rename(today + "-personal");
-%>
# Personal: <% tp.date.now("dddd D MMMM YYYY") %>

[[<% yesterday %>-personal|← Yesterday]] | [[<% tomorrow %>-personal|Tomorrow →]]

## 🎯 Focus today

*Top 1–3 personal intentions.*

- 

## 🗓️ Events & appointments

```dataview
LIST
FROM "_Personal/Meetings"
WHERE dateformat(file.ctime, "yyyy-MM-dd") = dateformat(date(today), "yyyy-MM-dd")
SORT file.ctime ASC
```

## ⚠️ Still open from earlier

```tasks
not done
path includes _Personal/Daily
happens before today
short mode
hide backlink
hide edit button
hide task count
```

## 📌 Personal project tasks

```tasks
not done
path includes _Personal/Projects
(due before in 7 days) OR (no due date)
group by filename
short mode
hide backlink
hide edit button
hide task count
limit 15
```

## ✅ Ad-hoc tasks

*Quick personal to-dos that don't belong to a project.*

## 🏃 Fitness

*Log any workout, run, or movement here.*

- 

## 📝 Log

*What happened today.*

- 

## 🧠 Notes & ideas

- 
