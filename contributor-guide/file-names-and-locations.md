<properties pageTitle="Nomi di file e percorsi per gli articoli tecnici di EMS" description="Viene illustrata la struttura di file per gli articoli e le convenzioni di denominazione da seguire quando si crea un nuovo articolo." metaKeywords="" services="" solutions="" documentationCenter="" authors="tysonn" videoId="" scriptId="" manager="required" />

<tags ms.service="contributor-guide" ms.devlang="" ms.topic="article" ms.tgt_pltfrm=""  ms.workload="" ms.date="02/25/2016" ms.author="v-jocgar" />

# Nomi di file e percorsi per gli articoli tecnici di EMS
Procedura: 
- [ ] N.7 Trascinare i campi dati dinamici dei servizi per gli esempi
- [ ] N.8 Confermare il modello di denominazione dei file
- [ ] N. 9 Specificare esempi di sostituzione di modelli di denominazione dei file
- [ ] N. 10 Assicurarsi che tutti i collegamenti, soprattutto gli ancoraggi, funzionino correttamente

Nel repository dei contenuti tecnici viene usata un'unica cartella, la cartella **articoli**, per tutti gli articoli. Non esiste alcuna gerarchia di cartelle, tutti gli articoli risiedono nella struttura di file flat. Se si creano cartelle contenenti articoli, questi non possono essere pubblicati.

Anziché usare una struttura di file come principio di organizzazione, viene usata una convenzione di denominazione dei file piuttosto rigida che identifica in modo chiaro gli argomenti e che facilita l'individuazione nel Web.

Ecco cosa è necessario tenere presente:

+ [Regole per la denominazione dei file]
+ [Modelli di nome file]
+ [Esempi]
+ [Approvazione dei nomi file]

## Regole per la denominazione dei file

- Niente spazi o caratteri di punteggiatura. Usare il segno meno per separare le parole nel nome del file.
- Usare solo lettere minuscole
- Non più di 80 caratteri. Il limite è dettato dal sistema di pubblicazione
- Usare verbi di azione specifici, ad esempio sviluppare, acquistare, compilare, risolvere. Non usare verbi al gerundio.
- Non includere parole molto brevi come preposizioni, articoli e così via.
- Tutti i file devono essere Markdown e avere estensione md.

## Modelli di nome file

Il modello di denominazione generale è il seguente:

<span style="color:red;">È necessaria la conferma di questo modello di denominazione di file.</span>
 **servizio-piattaforma-lingua-contenuto-prodotto-versione.md**

Usare le parti del modello applicabili e controllare l'elenco di articoli nel repository per avere un'idea dei nomi esistenti. 

## Esempi
<span style="color:red;"> **Sono necessari esempi di sostituzione per questa sezione da docs.microsoft.com/ems**  </span>

Di seguito vengono illustrati alcuni esempi di nomi validi che seguono il modello:

- servizi-cloud-dotnet-recapito-continuo.md
- servizi-mobile-ios-introduzione.md
- documentdb-gestione-account.md
- servizi-mobile-dotnet-backend-introduzione-impostazioni-sincronizzazione.md
- active-directory-java-autenticazione-utenti-controllo-accesso-eclipse.md
- macchine-virtuali-installazione-windows-server-2008r2.md

## Approvazione dei nomi file

Il gruppo di revisori delle richieste pull si occupa di controllare i nomi file quando un nuovo file viene inviato per la prima volta al repository. I revisori delle richieste pull devono esaminare il nome file e generare un feedback se sono necessarie modifiche. Il nome file deve essere corretto prima che venga accettata la richiesta pull. I collaboratori hanno la possibilità di sollecitare l'aggiornamento della richiesta pull in sospeso tramite una procedura molto semplice.

## Torna alla pagina iniziale

- [Articolo di panoramica](./../README.md)
- [Indice degli articoli sul materiale sussidiario](./contributor-guide-index.md)


<!--Anchors-->
[Rules for naming files]: #rules
[File name patterns]: #pattern
[Examples]: #standard-examples
[File name approval]: #file-name-approval


<!--HONumber=Mar16_HO1-->


