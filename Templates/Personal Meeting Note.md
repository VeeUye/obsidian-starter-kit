<%*
const meetingName = await tp.system.prompt("Meeting name");
await tp.file.rename(meetingName);
const today = tp.date.now("YYYY-MM-DD");
-%>
# <% meetingName %>

**Date**:: <% today %>
**With**:: 
**Daily note::** [[<% today %>-personal]]

## Notes

## Action Items

## Follow-up

- 
