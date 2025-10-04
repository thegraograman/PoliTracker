---

Subject: Geometria
color: "#F4E3C9"
icon: "💻"
Type: Report
CFU: 8
---

```button
name Aggiungi una lezione
type note(UntitledNN) template
action Lezione
color blue
```

# Tasks
```dataviewjs
const query = `
path includes Geometria
# you can add any number of extra Tasks instructions, for example:
group by heading
`;

dv.paragraph('```tasks\n' + query + '\n```');
```

# Lezioni di Geometria
```dataview
TABLE without id
 Date AS "📆",
 file.link AS "Lezione",
 argomento AS "Argomento", 
 choice(status, "✅", "❌") AS "Fatto"
FROM "Lezioni/Geometria"
WHERE Type = "Lezione"
SORT file.name ASC

```


#report
