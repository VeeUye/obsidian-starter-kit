<%*
const personName = await tp.system.prompt("Person name");
const nickname = await tp.system.prompt("Nickname (optional)", "");
await tp.file.rename(personName);
const today = tp.date.now("YYYY-MM-DD");
const taskPattern = nickname
  ? `/\\[\\[${personName}(\\|[^\\]]+)?\\]\\]|\\[\\[${nickname}(\\|[^\\]]+)?\\]\\]/`
  : `/\\[\\[${personName}(\\|[^\\]]+)?\\]\\]/`
-%>
---
aliases: [<% nickname %>]
---
# <% personName %>

**Role**::
**Context**:: 
**Company/Team::**
**Last contact::** <% today %>

## About

*Who are they? How do you know them? What's the context of the relationship?*

## Notes

*Observations, things to remember, relationship context.*

## Meetings

```dataview
LIST
FROM "Meetings" OR "_Personal/Meetings"
WHERE contains(file.outlinks, this.file.link)
SORT file.ctime DESC
```

## Open actions

```tasks
not done
description regex matches <% taskPattern %>
short mode
hide backlink
hide edit button
hide task count
```
