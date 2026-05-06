# Reads

## Currently reading

```dataview
TABLE author, started
FROM "Reads"
WHERE status = "reading"
SORT started ASC
```

## Want to read

```dataview
TABLE author, type
FROM "Reads"
WHERE status = "want to read"
SORT file.name ASC
```

## Done

```dataview
TABLE author, finished, rating
FROM "Reads"
WHERE status = "done"
SORT finished DESC
```
