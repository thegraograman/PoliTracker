---
<%*
//Pop up a window to ask you to choose your subject
let Subject = await tp.system.suggester(["Analisi 1", "Informatica", "Geometria e Algebra Lineare"], ["Analisi1", "Informatica", "Geometria"], false, "Scegli la materia:")

let Color = "";
let Icon = "";

if (Subject == "Analisi1"){
	Color="#FBF0B7"; //giallo
	Icon="🔢";
}
if (Subject == "Informatica"){
	Color="#FFB8C3"; //rosa
	Icon="🎢";
}

if (Subject == "Geometria"){
	Color="#F4E3C9"; //arancio
	Icon="💻";
}

let newTitle
if(tp.file.title.toLowerCase().includes('untitled')) {
newTitle = "@" + `${Subject}` + " Report"
await tp.file.rename(newTitle)
}
else newTitle = tp.file.title
if(Subject !== null) {
let filePath = "/Lezioni/" + `${Subject}` + "/" + `${newTitle}`
await tp.file.move(`${filePath}`)
}
%>
Subject: <% Subject %>
color: "<%Color%>"
icon: "<%Icon%>"
Type: Report
CFU: 0
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
path includes <% Subject %>
# you can add any number of extra Tasks instructions, for example:
group by heading
`;

dv.paragraph('```tasks\n' + query + '\n```');
```

# Lezioni di <% Subject %>
```dataview
TABLE without id
 Date AS "📆",
 file.link AS "Lezione",
 argomento AS "Argomento", 
 choice(status, "✅", "❌") AS "Fatto"
FROM "Lezioni/<% Subject %>"
WHERE Type = "Lezione"
SORT file.name ASC

```


#report
