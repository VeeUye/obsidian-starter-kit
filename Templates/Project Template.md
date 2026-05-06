<%*
const projectName = await tp.system.prompt("Project name");
await tp.file.rename(projectName);
-%>
# <% projectName %>

**Type**:: project
**Status**:: active
**Started**:: <% tp.date.now("YYYY-MM-DD") %>
**Target**:: 
**Highlight**:: 
**Impact**:: 

## Context

*What is this project? Why does it matter?*

## Current Focus

*Where things stand right now. Update as the project moves.*

## Tasks

### Active

### Done

## Open Questions

*Unresolved questions for the team — add owner and date when known.*

## Log

*Dated notes, decisions, discoveries — newest at top.*

### <% tp.date.now("YYYY-MM-DD") %>

## Links
