<%*
const managerName = await tp.system.prompt("Manager's name");
const today = tp.date.now("YYYY-MM-DD");
const noteName = `1-1 ${managerName} ${today}`;
await tp.file.rename(noteName);
await tp.file.move("Meetings/" + noteName);

const managerFile = app.vault.getAbstractFileByPath(`People/${managerName}.md`);
if (managerFile) {
  let content = await app.vault.read(managerFile);
  content = content.replace(/\*\*Last contact::\*\* .*/, `**Last contact::** ${today}`);
  await app.vault.modify(managerFile, content);
}
-%>
# 1:1 [[<% managerName %>]] — <% today %>

**Date**:: <% today %>
**Daily note::** [[<% today %>]]

## Previous 1:1s

```dataview
LIST
FROM "Meetings"
WHERE contains(file.name, "1:1 <% managerName %>")
AND file.name != this.file.name
SORT file.ctime DESC
LIMIT 5
```

## Open actions

```tasks
not done
description includes [[<% managerName %>]]
short mode
hide backlink
hide edit button
hide task count
```

## 🏆 Wins to share

*What's gone well since last time? Shipped, unblocked, learned.*

- 

## 🚧 Current work & blockers

*What am I working on? Anything I need help with or visibility on?*

- 

## 🎯 Topics to raise

*My agenda — questions, concerns, things I want input on.*

- 

## 📈 Career & growth

*Feedback, development conversations, goals progress. Leave blank if not relevant this week.*

- 

## 📝 Notes

## ✅ Actions from this meeting

- 
