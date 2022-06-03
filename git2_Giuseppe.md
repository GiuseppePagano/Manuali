Approfondiamo il concetto di GIT, come si crea una branch? Come si uniscono i rami di sviluppo? Inoltre, come funziona Git Kraken?

**Sto dividendo in un secondo documento per facilità di lettura, ad approvazione ottenuta farò il merge dei due.**

Non esiste un metodo assoluto e predefinito di unione dei rami di sviluppo, di gestione del versionamento e di nomeclatura. Possiamo però provare ad esporre quello che, secondo me, può essere l'how to use più efficace. 

Come abbiamo già visto un branch si crea tramite il comando: 

```bash
git branch <nome_branch>											(esempio git branch develop)
```

Fin qui nulla di nuovo, ma la gestione di un flow git diventa più intricata quando più sviluppatori lavorano in contemporanea. Fin quando ogni modifica(che sia al codice o alla gestione dei branch) è fatta in locale, ogni sviluppatore ha la totale libertà, quando però le modifiche devono arrivare al server remoto, è cruciale evitare ogni tipo di conflitto tra i codici o quanto meno saperli gestire al meglio. Mettiamo caso che due sviluppatori stiano lavorando in contemporanea sullo stesso branch, lo sviluppatore A scrive codice e segue il normale workflow fino alla push sul server remoto, cambiando quindi il sorgente per tutti e lasciando "indietro" chi sta ancora lavorando su branch non aggiornati. Di buona norma, lo sviluppatore B (che agisce non solo sullo stesso branch, ma sulle stesse **righe** di codice) dovrebbe fare una pull prima di ogni commit, così prendere le modifiche ancora prima che il conflitto possa presentarsi. Se ciò non accade i conflitti si possono gestire tramite alcuni comandi da CLI.

Se al tentato merge dei commit abbiamo dei conflitti, git diff ci offre una comparazione visiva delle differenze tra i due sorgenti (quello locale e quello remoto), offrendo la possibilità di editare quello locale e finalmente di mergiare e pushare.

```bash
git diff
```

Questo comando invece annulla il merge in corso e ci riporta allo stato precedente, prima che il conflitto tra sorgenti si presentasse. 

```bash
git merge --abort
```

Git reset è un comando da usare quando ci si trova in conflitto, offre l'opportunità di resettare il file locale che è in conflitto con la sua copia che si trova nel server remoto

```bash
git reset


```

Viene da se che gestire anche solo concettualmente questo flusso di dati da riga di comando risulta intricato. É vero che tramite il comando 

```bash
git log --all --decorate --oneline --graph
```

Possiamo raffigurare in maniera rudimentale l'intero workflow (quindi avere una sorta di grafico che rappresenta i branch, come e quando vengono mergiati e le loro commit di riferimento)

```bash
|
|\
| * 60dab315 Fixing a few typos
| |* 3e8f67bc Another round of edits
|/
| * 67a15c15 Adding more specific JSON serailization examples
|
```

Ma grazie all'aiuto di GUI possiamo efficacemente gestire ogni aspetto del flow di git. Una delle GUI più utilizzate e potenti è git kraken, la cui peculiarità principale è la gestione grafica dei branch.

All'avvio troveremo una login con la scelta dell'avatar(nota doverosa, sono tanti e tutti originali) . Git kraken è uno strumento con licenza, usato più comunemente nelle aziende e non da singoli sviluppatori. Supporta tutti i maggiori servizi di hosting git. Una volta scelto il nostro preferito ed aver importato almeno un repository, quello che ci troviamo davanti sarà più o meno questo.

![](C:\Users\UTENTE\Desktop\Tesina git\gitkrakenpic.jpg)

Per quanto possa spiazzare all'inizio, la gestione in gui rende elementare praticamente ogni azione che prima veniva fatta da git bash. A destra c'è l'area di commit divisa per file che sono nella stage area (**Staged File**) e file che non lo sono  (**Unstataged File**) e commit con tanto di message e bottone per l'invio. In alto abbiamo i tasti per pull e push creazione di branch. Tutte operazioni guidate e rese semplicissime dall'interfaccia grafica. A sinistra invece c'è la gestione dei branch remote e local ed la lista dei commit che ci permette di tenere traccia di tutte le modifiche, locali e remote. Ma la parte fondamentale è quella al centro, quella grafica. L'intricata alberatura dei branch da senso al nostro percorso. Da qui possiamo vedere quando, quanto e come uno sviluppatore (l'avatar tondo) ha contribuito al progetto, dove si sono uniti i rami di sviluppo e quali fix sono state lavorate. 
