<%*
const personName = await tp.system.prompt("Person name");
const today = tp.date.now("YYYY-MM-DD");
const noteName = `1-1 ${personName} ${today}`;
await tp.file.rename(noteName);
await tp.file.move("Meetings/" + noteName);

const personFile = app.vault.getAbstractFileByPath(`People/${personName}.md`);
if (personFile) {
  let content = await app.vault.read(personFile);
  content = content.replace(/\*\*Last contact::\*\* .*/, `**Last contact::** ${today}`);
  await app.vault.modify(personFile, content);
}
-%>
# 1:1 [[<% personName %>]] — <% today %>

**Date**:: <% today %>
**Daily note::** [[<% today %>]]

## Previous 1:1s

```dataview
LIST
FROM "Meetings"
WHERE contains(file.name, "1:1 <% personName %>")
AND file.name != this.file.name
SORT file.ctime DESC
LIMIT 5
```

## Open actions

```tasks
not done
description includes [[<% personName %>]]
short mode
hide backlink
hide edit button
hide task count
```

## Topics to raise

- 

## Notes

## Actions from this meeting

- 
