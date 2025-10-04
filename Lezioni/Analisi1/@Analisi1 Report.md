---

Subject: Analisi1
color: "#FBF0B7"
icon: "🔢"
Type: Report
CFU: 10
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
path includes Analisi1
# you can add any number of extra Tasks instructions, for example:
group by heading
`;

dv.paragraph('```tasks\n' + query + '\n```');
```

# Lezioni di Analisi1
```dataview
TABLE without id
 Date AS "📆",
 file.link AS "Lezione",
 argomento AS "Argomento", 
 choice(status, "✅", "❌") AS "Fatto"
FROM "Lezioni/Analisi1"
WHERE Type = "Lezione"
SORT file.name ASC

```


#report
