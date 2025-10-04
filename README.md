# PoliTracker (Ita)
[Obsidian](https://obsidian.md/) Set-Up to track Engineering Lessons (built for PoliMI)

## Cos'è?
Politracker è un progetto basato su Obsidian per tracciare le lezioni universitarie e lo studio, tramite un sistema di **task**, **indicizzazione** e **calendarizzazione**. 

A partire dalla corretta **registrazione** delle attività svolte, in un momento prossimo alla lezione, si prevede una **semplificazione** dello studio, subito mirato e pianificato correttamente.

## Cosa fa?
- costituisce un **database** ordinato per materia di lezioni, classificate tramite metadati specifici
- crea un **Report** per ogni materia per avere traccia delle lezioni e dello studio
- Gestisce delle **task** associate ad ogni lezione, con possibilità di impostarne una scadenza
- Crea una **bacheca** con un'overview sui corsi, tramite vista *calendario* delle lezioni e delle task
- Tramite **pulsanti** e **template** semplifica l'inserimento delle lezioni, in modelli di nota pronti all'uso

## Set-up
1. **Importare** la cartella "Template" nel Vault e il file "Bacheca"
2. Installare i Plugin
3. Configurare i **Template**
4. Prendere confidenza con i **comandi**
5. **Personalizzare**
6. Sincronizzare in **cloud** le note [[Risorse|Vedi risorse]]

### Plugin
Per una guida su come installare i **plugin** consultare [la guida ufficiale](https://help.obsidian.md/Extending+Obsidian/Community+plugins)
Installare i seguenti plugin nell'ordine in cui indicati, avendo cura di impostarli correttamente.
#### 1. Dataview
- necessario per associazione di *metadati* ad ogni nota e classificazione in tabelle/calendari/liste
- I **metadati** sono contenuti all'inizio di ogni nota, preceduti e seguiti da `---`
- Alcune tabelle, che fanno uso di Dataview, sono già state inserite nei template. Per avere una maggiore comprensione del funzionamento, consultare la [Documentazione](https://obsidian.rocks/dataview-in-obsidian-a-beginners-guide/).
- **Impostazioni**: 
	- in General Setting di Dataview abilitare: "Enable Inline Queries", "Enable Javascript Queries"
	- *opzionale*: Modificare il formato di data
#### 2. Tasks
- Necessario per pianificazione delle **task**
- Per la vista calendario collegata alle task è necessario configurare alcuni file. Fare riferimento a [questo progetto su GitHub](https://github.com/702573N/Obsidian-Tasks-Calendar)
- NB: La vista calendario consente di impostare un'**emoji** e un **colore** correlato a dei metadati. L'impostazione di tali metadati è automatica, tramite templater.
#### 3. Templater
- Necessario per la creazione **automatica** di file. 
- **Impostazioni**: Impostare la *directory* dei Template in *Template folder location*
- La **sintassi** di Templater permette di avere in modo automatico metadati, titolo del file, composizione e posizione. I template sono personalizzabili e le modifiche sono applicate sui nuovi file. 
- Per maggiori informazioni sulla sintassi fare riferimento alla [documentazione](https://silentvoid13.github.io/Templater/introduction.html)
- Per comprendere i template importati consultare i **commenti**.
- La **shortcut** per creare una nuova nota da template è **alt+N**, questa è modificabile nelle impostazioni di Obsidian.
#### 4. Buttons
- Necessaria per **pulsanti** in report

### Capire e configurare
#### Template "Lezione"
Dopo la creazione di un nuovo file tramite templater (**alt+N**) e aver selezionato Lezione (tasto invio) comparirà un menù pop up per selezionare subito la materia (e la relativa directory del file). 
Il file è composto da:
- **metadati** utili 
- sezione **contenuto** per segnare eventuali appunti/link a materiali
- sezione **studio**, per tracciare il relativo studio ed eventuali problemi
- tag lezione
##### Set-up Lezione
Affinchè tutto funzioni al meglio, sulla base delle proprie esigenze è necessario impostare alcuni parametri nel file "Lezione".
1. inserire **materie** e alias materie
*esempio:*
`tp.system.suggester(["Analisi 1", "Informatica", "Geometria e Algebra Lineare"], ["Analisi1", "Informatica", "Geometria"], false, "Scegli la materia:")`
nella prima quadra inserire i nomi delle materie, nella seconda gli alias per il menù di scelta
2. impostare i cicli **if** secondo le emoji e la materia (utile per la vista calendario Task) 
3. impostare la **struttura** del file secondo le proprie esigenze
4. impostare la **directory** se diversa da /Lezioni/NomeMateria
5. è possibile modificare il **titolo** automatico in diversi formati
N.B. più file con lo stesso titolo andranno in conflitto, per questo nella fase di testing è consigliabile mantenere anche l'ora e il minuto di creazione nel nome del file. L'opzione è sempre *modificabile*.
*esempio:*
`let newTitle if(tp.file.title.toLowerCase().includes('untitled')) {newTitle = ${Subject} + " " + tp.date.now("YYYY-MM-DD-HHmm")await tp.file.rename(newTitle)}`
*in questo esempio il titolo è composto dal nome della materia + spazio+2023-07-21-1055*

Il file lezione presenta alcuni **metadati** utili per la corretta indicizzazione e analisi con dataview. In particolare
- Argomento: NC 
*di default NC, successivamente inserire gli argomenti in modo sintetico*
- Status: false
*variabile booleana (true/false) che viene converita in emoji (✅, ❌) nella tabella in report, può risultare utile per tracciare l'avvenuto studio della lezione*. 

#### Template "Report"
I file **report** sono costruiti come overview della materia, per questo il titolo è preceduto da **"@",** per farli apparire per primi all'interno della directory. 
La creazione del file report avverrà solo **1 volta** per materia, grazie a *dataview* il file sarà sempre aggiornato con gli ultimi inserimenti. In ogni file lezione è presente un **collegamento** al relativo report.
Il meccanismo di creazione è lo stesso della lezione, e la sintassi di personalizzazione è la stessa. 
Il file è composto da 
- **metadati** utili, tra cui "CFU"
- **pulsante** per la creazione di una nuova lezione (tramite plugin *Buttons*)
- sezione **task** (automatica in base alla materia)
- **tabella** riassuntiva delle lezioni del corso (gestita da *dataview*)
##### Set-up Report
- impostare le **materie** (vedi setup lezione) e gli if
- impostare la **directory** se diversa da /Lezioni/NomeMateria
##### Spunti
Il report potrebbe diventare un efficace *planning* dell'esame, con maggiori informazioni a riguardo, scadenze, link di risorse...
#### Bacheca
Il file Bacheca presenta tutte le lezioni in poche ed efficienti schermate.
E' composto da 
- **tabella** riassuntiva delle lezioni
- vista **calendario** delle lezioni inserite
- vista **calendario** delle **Task**
- vista **di tutte le lezioni**, ordinate secondo data (ordine modificabile)
### Lavorare con le Task
Il sistema di Task si basa sul plugin **tasks**, integrato con lo snippet del calendario.
- Di default tramite la shortcut **ctrl+L** si crea una task, di cui impostare priorità, data di inizio e data di scadenza.
- Per visualizzare il menù completo di inserimento si può ricorrere al comando *Tasks: create or edit task* (accessibile tramite ctrl+p)
- Le task sono poi ordinate e filtrate nei **report** e in **bacheca**. 
-  è importante impostare, di ogni task, la **data di scadenza** (*Due date*), che permetterà la visualizzazione nel calendario
### Shortcut utili
- **alt+N** creazione file da template
- **ctrl+P** accedere a comandi di Obsidian (shortcut da abilitare)
- **ctrl+L** crea nuova task

## Perchè?
Il metodo di studio e la pianificazione delle attività sono estremamente personali. Nell'analisi dello studio universitario ho identificato alcuni elementi:
- importanza delle **lezioni**
- **intensità** elevata
- molteplicità di **risorse**
- estrema **autonomia** nello studio
#### Ita

Politracker costituisce uno strumento per far fronte alle **problematiche** legate all'accumularsi di studio, lezioni da rivedere e appunti vari. In particolare:
- inserimento **immediato** delle lezioni
	Il processo di **scrittura** e **catalogazione** della lezione, con note didattiche sulla propria *ricezione* è di per sè *importante*. Se questo avviene a distanza di qualche ora, magari quando si rientra a casa, diventa essere estremamente **efficace**. Politracker **semplifica** questo processo: sfruttando l'archiviazione in cloud si riesce facilmente ad inserire l'attività di catalogazione nella propria *routine*.
- **pianificazione**
	Come prepararsi per gli esami? In che **ordine** studiare le materie? Da dove prendere i materiali? Sono domande utilissime per affrontare in modo sicuro lo studio, e, se non soddisfatti subito questi dubbi rischiano di sopraffare lo studente. I **report** di Politracker sono pensati per questa esigenza. Ripetere seguendo l'ordine delle lezioni, con i materiali già classificati, può risolvere molti di questi problemi per affrontare il ripasso con la *serenità* necessaria.
- dal **vago** al **particolare**
Il sistema delle **task** aiuta ad orientare lo studio verso dei piccoli obiettivi *concreti*, *raggiungibili*. La consapevolezza di dover "Studiare Analisi" si trasformerà in "Imparare dimostrazione dei teoremi fondamentali", semplificando lo studio.
-  **personalizzazione**
Politracker è basato su **Obsidian**: vuole infatti essere un prodotto estremamente fluido, "*open*" e legato alle **proprie** esigenze di studio. Questo modello costituisce solo una **guida**, un raccoglitore di diverse funzionalità orientate verso un unico obiettivo. 

Spero con questa guida di avere ispirato riguardo gli obiettivi, le potenzialità e le modalità di utilizzo. Politracker è un'**idea**, sta a te personalizzarlo e integrarlo nella tua vita da studente.
Buono studio! Buon Poli!

Chiara Santovito
chiara1.santovito@mail.polimi.it

# PoliTracker (Eng)

## What is it?

**Politracker** is a project based on **Obsidian** designed to track university lectures and study sessions through a system of **tasks**, **indexing**, and **scheduling**.

By correctly **logging** the activities carried out shortly after each lecture, it aims to **simplify** studying—making it immediately focused and well-planned.

## What does it do?

* Builds an organized **database** of lectures for each subject, classified through specific metadata
* Creates a **Report** for each subject to keep track of lectures and study progress
* Manages **tasks** associated with each lecture, with the ability to set deadlines
* Creates a **Dashboard** providing an overview of all courses, using a *calendar view* for both lectures and tasks
* Simplifies lecture entry through **buttons** and **templates**—ready-to-use note models

## Set-up

1. **Import** the “Template” folder into your Vault and the “Bacheca” (Dashboard) file
2. Install the necessary **Plugins**
3. Configure the **Templates**
4. Get familiar with the **commands**
5. **Customize**
6. Sync your notes to the **cloud** [[Resources|See resources]]

### Plugins

For a guide on how to install **plugins**, see the [official documentation](https://help.obsidian.md/Extending+Obsidian/Community+plugins).
Install the following plugins in the order listed and make sure to configure them properly.

#### 1. Dataview

* Required for associating *metadata* with each note and classifying them in tables/calendars/lists
* **Metadata** are placed at the beginning of each note, enclosed between `---`
* Some tables using Dataview are already included in the templates. To better understand how it works, see the [Documentation](https://obsidian.rocks/dataview-in-obsidian-a-beginners-guide/).
* **Settings:**

  * In Dataview General Settings, enable: “Enable Inline Queries” and “Enable Javascript Queries”
  * *Optional:* Modify the date format

#### 2. Tasks

* Required for planning and managing **tasks**
* For the calendar view linked to tasks, some files must be configured. Refer to [this GitHub project](https://github.com/702573N/Obsidian-Tasks-Calendar).
* **Note:** The calendar view allows you to set an **emoji** and **color** related to metadata. These are automatically assigned via Templater.

#### 3. Templater

* Required for **automatically** creating files.
* **Settings:** Set the *Template folder location* under Templater settings.
* The **Templater syntax** allows for automatic metadata, file title, composition, and location. Templates are customizable, and changes apply to newly created files.
* For syntax details, refer to the [documentation](https://silentvoid13.github.io/Templater/introduction.html).
* To understand the imported templates, read the **comments** within them.
* The **shortcut** to create a new note from a template is **Alt+N**, modifiable in Obsidian’s settings.

#### 4. Buttons

* Required for adding **buttons** inside reports

### Understanding and Configuring

#### “Lezione” (Lecture) Template

After creating a new file with Templater (**Alt+N**) and selecting *Lezione* (press Enter), a pop-up will appear to select the subject (and corresponding directory).
The file includes:

* Useful **metadata**
* A **content** section for notes or links to materials
* A **study** section to track study progress or issues
* A lecture **tag**

##### Lecture Template Set-up

To ensure everything works properly, you’ll need to configure some parameters in the “Lezione” file:

1. Add your **subjects** and subject aliases
   *Example:*

   ```js
   tp.system.suggester(["Calculus 1", "Computer Science", "Geometry and Linear Algebra"], ["Calculus1", "CS", "Geometry"], false, "Choose the subject:")
   ```

   The first array contains subject names, the second contains aliases shown in the selection menu.
2. Configure **if** statements for emojis and subjects (useful for the Task Calendar view).
3. Customize the **file structure** as needed.
4. Set the **directory** if different from `/Lectures/SubjectName`.
5. You can modify the **automatic title** format.
   *Note:* Multiple files with the same title will conflict. During testing, it’s recommended to include the creation time in the file name (e.g., `2023-07-21-1055`).
   *Example:*

   ```js
   let newTitle
   if(tp.file.title.toLowerCase().includes('untitled')) {
       newTitle = ${Subject} + " " + tp.date.now("YYYY-MM-DD-HHmm")
       await tp.file.rename(newTitle)
   }
   ```

   This creates a title with *Subject + Date + Time*.

The lecture file contains useful **metadata** for Dataview indexing and analysis, including:

* `Topic: NC` *(default NC, later replaced with a brief topic description)*
* `Status: false` *(a boolean variable converted into an emoji ✅/❌ in the report table—useful for tracking whether the lecture has been studied)*

#### “Report” Template

**Report files** serve as overviews of each subject and are titled with a leading “@” so they appear first in their folder.
A report is created only **once per subject**—thanks to Dataview, it auto-updates with new entries. Each lecture note includes a **link** to its report.

Like the lecture template, it can be customized similarly.
Each report includes:

* Useful **metadata**, such as “CFU” (credit units)
* A **button** to create a new lecture (via the Buttons plugin)
* A **task** section (auto-generated based on the subject)
* A **summary table** of course lectures (via Dataview)

##### Report Set-up

* Configure **subjects** and **if** conditions (same as lecture setup)
* Set the **directory** if different from `/Lectures/SubjectName`

##### Suggestions

The report can also become an effective **exam planner**, including more details, deadlines, and resource links.

#### Dashboard (“Bacheca”)

The Dashboard file provides a compact and efficient overview of all lectures.
It includes:

* A **summary table** of lectures
* A **calendar view** of all lectures
* A **calendar view** of all **tasks**
* A **list view** of all lectures, ordered by date (modifiable)

### Working with Tasks

The task system is based on the **Tasks** plugin, integrated with the calendar snippet.

* By default, the shortcut **Ctrl+L** creates a new task, where you can set priority, start date, and due date.
* To open the full task creation menu, use *Tasks: create or edit task* (via **Ctrl+P**).
* Tasks are displayed and filtered within **reports** and the **dashboard**.
* It’s important to set a **Due date** for each task so it appears in the calendar view.

### Useful Shortcuts

* **Alt+N** → Create a file from a template
* **Ctrl+P** → Access Obsidian commands (must be enabled)
* **Ctrl+L** → Create a new task

## Why?

Study methods and activity planning are highly personal.
In analyzing university study habits, I identified several key factors:

* The importance of **lectures**
* High **intensity**
* A variety of **resources**
* Great **autonomy** in studying

**Politracker** is a tool designed to address problems like the accumulation of study material, unreviewed lectures, and scattered notes. Specifically:

* **Immediate lecture entry**
  Writing and cataloging a lecture—with reflections on one’s understanding—is inherently **valuable**.
  Doing so within a few hours (e.g., after returning home) can be **highly effective**.
  Politracker **simplifies** this process: with cloud syncing, integrating this cataloging step into your daily *routine* becomes easy.

* **Planning**
  How should I prepare for exams? In what **order** should I study subjects? Where do I find materials?
  These questions, if left unanswered, can overwhelm students.
  Politracker’s **reports** are designed for this: reviewing in lecture order, with pre-organized materials, reduces confusion and allows for calmer, more effective study sessions.

* **From vague to specific**
  The **task system** helps turn large goals into smaller, *concrete*, *achievable* objectives.
  “Study Calculus” becomes “Learn the proof of the Fundamental Theorems,” making study more approachable.

* **Personalization**
  Built on **Obsidian**, Politracker is intended to be **flexible**, **open**, and adaptable to your personal study needs.
  This model serves as a **guide**, a collection of useful features centered on a single goal.

I hope this guide inspires you regarding the goals, potential, and ways to use this tool.
Politracker is an **idea** it’s up to you to customize and integrate it into your student life.

**Happy studying! Go Poli!**

*Chiara Santovito*
📧 [chiara1.santovito@mail.polimi.it](mailto:chiara1.santovito@mail.polimi.it)