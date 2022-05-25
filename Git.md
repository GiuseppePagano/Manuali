![git-and-version-control-system](C:\Users\UTENTE\Desktop\jquery\git-and-version-control-system.gif)

Git è un **VCS**,  un sistema di controllo versione. È quindi uno strumento che ci da la possibilità di gestire le varie versioni di un documento a prescindere dal suo tipo(possiamo quindi versionare un txt, un doc cosi come un file javascript ). Questa gestione si concretizza nel tenere traccia di chi apporta modifiche ad un documento ma sopratutto alla creazione di uno storico di queste modifiche, funzione fondamentale che tutela dalla perdita dei dati.  Entrando più nello specifico, per capire meglio il workflow di git immaginiamo di avere una versione per lo più funzionante di un software creato da noi. Questa sarà la nostra base, il nostro **tronco** portante da cui partire. Nell'utilizzo di questo software, ci accorgiamo però di un bug che non ne compromette l'utilizzo ma che non lo candida di certo ad essere una versione pronta per la distribuzione. È qui che git si dimostra fondamentale, dandoci la possibilità di creare una "**diramazione**" del nostro codice dove apportare le necessarie modifiche, senza compromettere la versione originale. A modifiche concluse, la diramazione precedentemente creata la faremo riconfluire nel tronco principale, sostituendo quindi il vecchio codice non funzionante con quello nuovo. Con l'aiuto di server remoti quali           https://github.com/ , https://gitlab.com/ o https://bitbucket.org/ più utenti possono accedere allo stesso repository ed interagire sullo stesso codice. 

Al link https://git-scm.com/ è scaricabile il setup. Una volta installato, con un semplice click destro(da qualsiasi path del sistema operativo) si potrà raggiungere la **git bash**, la **CLI**(command line interface) di git. Questa interfaccia è un'emulazione della bash  dei sistemi unix-like, quindi la sintassi dei comandi sarà pressochè la medesima. Iniziamo quindi a creare una cartella con il comando: 

```bash
mkdir <nome_cartella>                                   (esempio mkdir prova )
```

per verificare l'avvenuta creazione, prima di qualsiasi navigazione, tramite il comando 

```bash
ls 
```

vedremo tutte le cartelle ed i file del path sul quale ci troviamo. 

Per accedere alla cartella creata useremo: 

```bash
cd <nome_cartella>  									(esempio cd prova )
```

Adesso è ora di trasformare la cartella in un repository git con il comando:

```bash
git init 
```

Fatto! Adesso il repository git è stato ufficialmente inizializzato, contiene già un branch di default che è il **master**(come si può vedere anche a schermo) ed è pronto per gestire codice. Il passo seguente sarà popolare la cartella con qualche file e senza scomodare editor testuali user enemy come vim, a scopo didattico, possiamo scegliere qualsiasi tipo di documento (meglio se codice) da trascinare nel repository git appena creato. Completata questa operazione inizia il vero e proprio workflow di git, che parte con l'add e finisce con il commit. Quindi tramite il comando 

```bash
git add .
```

aggiungeremo tutti i file presenti all'interno repository nella staging area **NB**: il comando git add seguito dal  punto come già detto aggiunge **TUTTI** i file e le cartelle presenti nel path sul quale ci troviamo, ma possiamo aggiungere puntualmente un file o una cartella specifica semplicemente sostituendo il punto al nome del file o della cartella. IPOTETICO APPROFONDIMENTO SULLA STAGING AREA SI O NO? 

Aggiunti i file è il momento di fare il commit tramite il comando:

```bash
git commit -m "Inserire qui, tra virgolette, un messaggio parlante sulle modifiche appena effettuate"
```

Questa operazione, generando un codice univoco identificativo del commit, ci permette di tenere traccia delle modifiche e ci facilita la lettura dei messaggi di log. Durante il processo di sviluppo potremmo aver bisogno di creare diramazioni del nostro codice, cioè staccare dei **branch**. Le situazioni che richiedono nuovi branch, in ambito lavorativo sono molteplici e la best pratice è quella di avere il branch **master** che contiene il sorgente più funzionante possibile ed il branch **develop**(sviluppo) che contiene il sorgente di testing. Dal develop partiranno tanti sotto branch quanti sono i bugfix da effettuare. 

Per creare un branch il comando è:

```bash
git branch <nome_branch>											(esempio git branch develop)
```

Il nuovo branch sarà una copia 1:1 del branch predefinito in quel momento. Per convenzione si usa master dove si tiene,come già accennato, il codice più pulito e funzionante possibile.

Per cambiare da un branch all'altro invece il comando è:

```bash
git checkout <nome_branch>
```

Per migrare le modifiche effettuate su un branch ad un altro è necessario(dopo aver seguito il workflow di add e commit) fare un merge tra i due posizionadosi sul branch che si vuole modificare. Quindi dopo il checkout il comando sarà

```bash
git merge <nome_branch>
```

Questa operazione conclude il workflow di git a livello locale, quando cioè il repository creato non è collegato a nessun server remoto. Ma la potenza e la versatilità di git si vede quando sono più sviluppatori a dover gestire lo stesso codice. Come già accennato esistono vari server remoti che permettono l'archiviazione e la gestione dei codici con git, uno dei più funzionali è senza dubbio https://github.com/. Registrarsi è gratuito e grazie alla sua GUI (graphical user interface) è semplicissimo creare e gestire repository. Per collegare un repository locale con uno remoto, il primo passo è ovviamente quello di creare quello remoto. Navighiamo quindi all'interno della sezione "i miei repository" che appare cliccando sull'icona del profilo utente. Ed una volta sulla pagina che mostra l'elenco di tutti i nostri repository già esistenti, clicchiamo l'icona verde **new** (o nuovo) e diamo un nome al repository. Concludiamo le operazioni di creazione con il tasto **create repository** in basso. Questa operazione è l'equivalente del git init di una cartella locale. Il passo successivo avviene in locale, precisamente aprendo la git bash con il destro puntando il repository <u>locale</u> precedentemente creato. Una volta avviata la bash il comando da digitare è:

```bash
git remote add origin git@github.com:sammy/my-new-project.git  (Dove sammy è il nostro utente di github e 																my new project il nome del repository remoto)
```

Adesso che abbiamo un supporto remoto è necessario integrare al workflow locale due concetti (e comandi) fondamentali: **push**, **pull**. 

```bash
git push <URL_remoto> <nome_branch>
```

Con questo comando(sempre successivo a tutte le fasi del workflow locale) si *spingono* tutte le modifiche al server remoto

Mentre con:

```bash
git pull <nome_branch> <URL_remoto>
```

ci *tiriamo* tutte le modifiche che stanno sul server remoto caricate da altri(sempre inerenti al repository già in nostro possesso).

Ultimo comando, ma non per importanza, offre la possibilità di scaricare un repository remoto su una macchina locale.

Con

```bash
git clone <URL_remoto>
```

scaricheremo un intero progetto. La url è ottenibile ovviamente, solo dalle interfacce dei server remoti, nel caso di github si troverà all'interno del repository sotto il pulsante verde "code". Da qui è possibile scegliere il protocollo di clone più adatto alle nostre esigenze, copiarlo ed incollarlo.
