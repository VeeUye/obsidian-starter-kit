<%*
const title = await tp.system.prompt("Title");
const category = await tp.system.suggester(["Fiction", "Non-Fiction"], ["Fiction", "Non-Fiction"], true, "Category");
await tp.file.move(`Reads/${category}/${title}`);
const today = tp.date.now("YYYY-MM-DD");
-%>
# <% title %>

**Author**::
**Category**:: <% category %>
**Type**:: book | article | other
**Status**:: want to read | reading | done | abandoned
**Started**::
**Finished**::
**Rating**:: /5

## Key takeaways

- 

## Notes

