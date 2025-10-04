---
<%*
//Pop up a window to ask you to choose your subject
let Subject = await tp.system.suggester(["Analisi 1", "Informatica", "Geometria e Algebra Lineare"], ["Analisi1", "Informatica", "Geometria"], false, "Scegli la materia:")

//Impostazione colore e icona per calendario task
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

/*if (Subject == "Elettr1"){
	Color="#B6DBE1"; //celestino
	Icon="📱";
}
*/

//Rename your note, add condition just in case you accidentally delete the note
let newTitle
if(tp.file.title.toLowerCase().includes('untitled')) {
newTitle = `${Subject}` + " " + tp.date.now("YYYY-MM-DD-HHmm")
await tp.file.rename(newTitle)
}
else newTitle = tp.file.title
//Move the note to the right directory
if(Subject !== null) {
let filePath = "/Lezioni/" + `${Subject}` + "/" + `${newTitle}`
await tp.file.move(`${filePath}`)
} %>
color: "<%Color%>"
icon: "<%Icon%>"
Subject: <%Subject%>
Date: <%tp.date.now("YYYY-MM-DD")%>
Type: Lezione
Argomento: NC
Status: false
---
[[@<%Subject%> Report|Vedi il report completo]]

---
# Contenuto
## Argomenti


## Link

---
# Studio
## Task


## Problemi

---
#lezione