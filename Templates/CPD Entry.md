<%*
const title = await tp.system.prompt("Title");
await tp.file.rename(title);
const today = tp.date.now("YYYY-MM-DD");
-%>
# <% title %>

**Type**:: course | talk | article | experiment | conference | other
**Skill**::
**Status**:: planned | in progress | done
**Date**:: <% today %>
**Source**::

```dataviewjs
const total = dv.current().file.lists.filter(l => l.hours).map(l => Number(l.hours)).array().reduce((sum, h) => sum + h, 0);
dv.span("**Total hours:** " + total);
```

## Sessions

- <% today %> | [hours:: ] | 

## Key takeaways

- 

## Applied / plan to apply

- 
