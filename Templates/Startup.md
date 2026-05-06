<%*
const today = tp.date.now("YYYY-MM-DD");

// Create work daily note if it doesn't exist yet today
const workPath = "Daily/" + today + ".md";
if (!app.vault.getAbstractFileByPath(workPath)) {
  const workTemplate = tp.file.find_tfile("Templates/Daily Note");
  await tp.file.create_new(workTemplate, today, true, "Daily");
}

// Create personal daily note if it doesn't exist yet today
const personalName = today + "-personal";
const personalPath = "_Personal/Daily/" + personalName + ".md";
if (!app.vault.getAbstractFileByPath(personalPath)) {
  const personalTemplate = tp.file.find_tfile("Templates/Personal Daily Note");
  await tp.file.create_new(personalTemplate, personalName, false, "_Personal/Daily");
}
-%>
