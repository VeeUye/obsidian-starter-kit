<%*
const today = tp.date.now("YYYY-MM-DD");
const noteName = `Standup ${today}`;
await tp.file.rename(noteName);
await tp.file.move("Meetings/" + noteName);
-%>
# Standup <% today %>

**Date**:: <% today %>
**Attendees**:: all hands
**Daily note::** [[<% today %>]]

## Notes

## Action Items

## Decisions Made

- 
