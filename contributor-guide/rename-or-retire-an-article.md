<properties pageTitle="Passaggi da eseguire quando si ritira o si modifica il nome di un articolo tecnico EMS" description="I passaggi da eseguire quando si ritira o si modifica il nome di un articolo tecnico EMS." metaKeywords="" services="" solutions="" documentationCenter="" authors="v-jocgar" videoId="" scriptId="" manager="robmazz" />

<tags ms.service="contributor-guide" ms.devlang="" ms.topic="article" ms.tgt_pltfrm="" ms.workload="" ms.date="02/26/2016" ms.author="v-jocgar" />

# Passaggi da eseguire quando si rinomina o si ritira un articolo tecnico EMS

Attività:
- [ ] #57 Verificare che questa sia la modalità di rimozione del contenuto per EMS. Ha l'aspetto di una serie di procedure a solo uso interno. 
- [ ] #58 Verificare che gli scrittori esterni possano eseguire uno strumento di analisi Web nel contenuto Microsoft. 
- [ ] #59 Testare la procedura per individuare collegamenti incrociati nel repository.
- [ ] #60 Verificare l'URL dei documenti EMS.  
- [ ] #61 Verificare che la rimozione dei collegamenti incrociati sia possibile per gli scrittori esterni. 
- [ ] #62 Verificare che gli scrittori esterni possano creare un reindirizzamento.
- [ ] #63 Verificare che gli scrittori esterni possano eliminare un articolo dal repository.
- [ ] #64 Verificare che gli scrittori esterni possano richiedere la rimozione di contenuto Microsoft dai motori di ricerca.


<span style="color:red;">Verificare che questa sia la modalità di rimozione del contenuto per EMS. Ha l'aspetto di una serie di procedure a solo uso interno. </span>
Queste indicazioni sono indirizzate agli esperti di dominio indicati come autori di un articolo che deve essere ritirato dalla sezione della documentazione tecnica di http://docs.microsoft.com/ems. La procedura si applica anche per la ridenominazione di un file.

Gli autori esperti di dominio devono eseguire diversi passaggi per ritirare il contenuto dal sito in modo che gli utenti del sito Web non abbiano un'esperienza negativa. L'eliminazione o la ridenominazione di un articolo va evitata il più possibile.

Se si è membri della community EMS e si ritiene che un articolo debba essere ritirato per qualsiasi motivo, lasciare un commento per l'articolo per informare l'autore che si è verificato un problema con l'articolo.

## Passaggio 1: Gestire i collegamenti in ingresso

Determinare se sono presenti collegamenti in ingresso non Microsoft al contenuto. Molto spesso blog, forum e altri contenuti sul Web si collegano agli articoli. È spesso possibile collaborare con i proprietari dei blog per modificare i collegamenti e rimuovere o aggiornare i collegamenti dei post dei forum. <span style="color:red;">Verificare che gli scrittori esterni siano in grado di eseguire un'analisi Web nel contenuto Microsoft. </span>Gli strumenti di analisi Web possono individuare la presenza di collegamenti in ingresso a traffico elevato che è possibile gestire.

## Passaggio 2: Rimuovere tutti i collegamenti incrociati all'articolo dal repository dei contenuti tecnici
<span style="color:red;">Testare la procedura per individuare collegamenti incrociati nel repository.</span>
1. Assicurarsi di lavorare in un ramo locale aggiornato. Eseguire `git pull origin master` o la variante appropriata di questo comando.

2.  <span style="color:red;">Verificare i percorsi nel repository.</span> Cercare nelle cartelle \EMDocs\Solutions e \EMDocs\Token articoli e token collegati all'articolo che si vuole ritirare e rimuovere i collegamenti incrociati o sostituirli con nuovi collegamenti incrociati appropriati. Se installata, è possibile usare un'utilità di ricerca e sostituzione per la ricerca dei collegamenti incrociati. In caso contrario, è possibile usare Windows PowerShell gratuitamente. Di seguito viene illustrato come usare PowerShell per trovare i collegamenti incrociati:

 a. Avviare Windows PowerShell.

 b. Al prompt di PowerShell passare alla cartella \EMDocs\Solutions:

 `cd \EMDocs\Solutions`

 c. Digitare il comando seguente che consente di visualizzare un elenco di tutti i file contenenti un riferimento all'articolo da eliminare:

 `Get-ChildItem -Recurse -Include *.md* | Select-String "<the name of the topic you are deleting>" | group path | select name`

  Se si preferisce inviare l'elenco dei nomi di file in un file di testo, denominato in questo caso psoutput.txt, è possibile:

  `Get-ChildItem -Recurse -Include *.md* | Select-String "<the name of the topic you are deleting>" | group path | select name | Out-File C:\Users\<your account>\psoutput.txt`

3. Aggiungere ed eseguire il commit di tutte le modifiche, effettuare il push all'origine e creare una richiesta pull per spostare le modifiche dall'origine al ramo master del repository principale.

## Passaggio 3: Rimuovere tutti i collegamenti incrociati 
<span style="color:red;">Verificare che la rimozione dei collegamenti incrociati sia possibile per gli scrittori esterni. </span>
Se sono presenti collegamenti all'articolo da altre pagine in <span style="color:red;">Verificare l'URL dei documenti EMS </span> http://docs.microsoft.com/ems, rimuoverli e creare un reindirizzamento per la pagina ritirata, se necessario. È necessario collaborare con la persona che gestisce e aggiorna la pagina di destinazione della documentazione del servizio relativa a questa parte. Contattare il proprio partner del team dei contenuti se non si conosce tale persona. La persona che gestisce e aggiorna la pagina di destinazione della documentazione dovrà eseguire due operazioni:

1. In Visual Studio, cercare nell'**intera** soluzione Web EMS i riferimenti incrociati al file da ritirare. Rimuovere i riferimenti incrociati o sostituirli con un riferimento incrociato aggiornato. Sarà necessario rimuovere i collegamenti HTML e le stringhe di risorse correlate per i collegamenti HTML. 

2. <span style="color:red;">Verificare che gli scrittori esterni possano creare un reindirizzamento.</span>Se è disponibile un articolo sostitutivo, creare un reindirizzamento all'articolo. 

3. Controllare le modifiche nel repository.

## Passaggio 4: Ritirare l'articolo
<span style="color:red;">Verificare che gli scrittori esterni possano eliminare un articolo dal repository.</span>
Dopo aver completato i tre passaggi precedenti e reso effettive le modifiche, è possibile eliminare l'articolo dal repository.

## Passaggio 5: Rimuovere le pagine memorizzate nella cache dai motori di ricerca
<span style="color:red;">Verificare che gli scrittori esterni possano richiedere la rimozione di contenuto Microsoft dai motori di ricerca.</span>
Eseguire questa operazione SOLO se il contenuto deve essere rimosso rapidamente a causa di problemi legali o gravi problemi con i clienti. Le eliminazioni delle pagine con priorità standard verranno gestite dai processi dei motori di ricerca. Passare alle pagine Web seguenti per rimuovere le pagine Web memorizzate nella cache dai motori di ricerca:

[Bing](https://www.bing.com/webmaster/tools/content-removal?rflid=1)
[Google](https://www.google.com/webmasters/tools/removals?pli=1)


### Torna alla pagina iniziale

- [Articolo di panoramica](./../README.md)
- [Indice degli articoli del materiale sussidiario](./contributor-guide-index.md)


<!--HONumber=Mar16_HO1-->


