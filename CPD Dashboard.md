# CPD Dashboard

## Planned

```dataviewjs
const pages = dv.pages('"CPD"').where(p => p.status?.trim() === "planned").sort(p => p.file.name, "asc");
dv.table(["Entry", "Type", "Skill", "Source"], pages.map(p => [p.file.link, p.type, p.skill, p.source]));
```

## Last 12 months

```dataviewjs
const cutoff = dv.date("today") - dv.duration("365 days");
const pages = dv.pages('"CPD"').where(p => p.status?.trim() !== "planned" && p.date >= cutoff).sort(p => p.date, "desc");
const rows = pages.map(p => {
  const total = p.file.lists.filter(l => l.hours).map(l => Number(l.hours)).array().reduce((sum, h) => sum + h, 0);
  return [p.file.link, p.type, p.skill, p.status, p.date, total];
});
dv.table(["Entry", "Type", "Skill", "Status", "Date", "Hrs"], rows);
```

## By skill

```dataviewjs
const pages = dv.pages('"CPD"').where(p => p.status?.trim() !== "planned").sort(p => p.date, "desc");
const bySkill = {};
for (const p of pages) {
  const skill = p.skill ?? "Uncategorised";
  const total = p.file.lists.filter(l => l.hours).map(l => Number(l.hours)).array().reduce((sum, h) => sum + h, 0);
  if (!bySkill[skill]) bySkill[skill] = [];
  bySkill[skill].push([p.file.link, p.date, total]);
}
for (const [skill, entries] of Object.entries(bySkill).sort()) {
  dv.header(4, skill);
  dv.table(["Entry", "Date", "Hrs"], entries);
}
```

## By type

```dataviewjs
const pages = dv.pages('"CPD"').where(p => p.status?.trim() !== "planned").sort(p => p.date, "desc");
const byType = {};
for (const p of pages) {
  const type = p.type ?? "Other";
  const total = p.file.lists.filter(l => l.hours).map(l => Number(l.hours)).array().reduce((sum, h) => sum + h, 0);
  if (!byType[type]) byType[type] = [];
  byType[type].push([p.file.link, p.skill, p.date, total]);
}
for (const [type, entries] of Object.entries(byType).sort()) {
  dv.header(4, type);
  dv.table(["Entry", "Skill", "Date", "Hrs"], entries);
}
```

## All time

```dataviewjs
const pages = dv.pages('"CPD"').where(p => p.status?.trim() !== "planned").sort(p => p.date, "desc");
const rows = pages.map(p => {
  const total = p.file.lists.filter(l => l.hours).map(l => Number(l.hours)).array().reduce((sum, h) => sum + h, 0);
  return [p.file.link, p.type, p.skill, p.status, p.date, total];
});
dv.table(["Entry", "Type", "Skill", "Status", "Date", "Hrs"], rows);
```
