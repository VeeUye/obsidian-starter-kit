<%*
const meetingName = await tp.system.prompt("Meeting name");
await tp.file.rename(meetingName);
const meetingDate = await tp.system.prompt("Meeting date (YYYY-MM-DD)", tp.date.now("YYYY-MM-DD"));
-%>
# <% meetingName %>

**Date**:: <% meetingDate %>
**Attendees**:: 
**Project**:: 
**Daily note::** [[<% meetingDate %>]]

## Agenda

1. 

## Notes

## Action Items

## Decisions Made

- 
