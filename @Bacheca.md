# Corsi
```dataview
LIST without ID link(file.link, Subject)
FROM "Lezioni" where Type = "Report"
SORT file.folder

```
```dataview
TABLE without ID 
icon AS "",
link(file.link, Subject) AS "Materie",
CFU AS "CFU"
FROM "Lezioni"
WHERE Type = "Report"
SORT file.folder

```

# Task
```dataviewjs
const query = `
not done
path includes Lezioni
# you can add any number of extra Tasks instructions, for example:
group by heading
`;

dv.paragraph('```tasks\n' + query + '\n```');
```

```dataviewjs
await dv.view("tasksCalendar", {pages: "",
view: "Month",
firstDayOfWeek: "1",
options: "style1 noCellNameEvent",
})
```

# Tutte le lezioni

```dataview
TABLE
	Date AS "Data",
	argomento AS "Argomenti",
	choice(status, "✅", "❌") AS "Fatto"
FROM "Lezioni"
WHERE Type = "Lezione"
SORT Date DESC
```

# Calendario delle lezioni
```dataview
CALENDAR file.ctime
from #lezione 
```

