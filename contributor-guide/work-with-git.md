<properties pageTitle="Comandi GIT per la creazione di un nuovo articolo o l'aggiornamento di un articolo esistente" description="Procedura per usare i repository GitHub di contenuti tecnici di Azure." metaKeywords="" services="" solutions="" documentationCenter="" authors="v-jocgar" videoId="" scriptId="" manager="robmazz" />

<tags ms.service="contributor-guide" ms.devlang="" ms.topic="article" ms.tgt_pltfrm="" ms.workload="" ms.date="02/24/2016" ms.author="v-jocgar" />

# Uso di GIT

Procedura:
- [ ] N.22 Sostituire l'URL dei Servizi di gestione emergenze per gli articoli completati (vedere la fine delle istruzioni)

## Processo standard (da un ramo)
Seguire i passaggi descritti in questo articolo per creare un ramo di lavoro locale nel computer in modo da creare un nuovo articolo per la sezione di documentazione tecnica di Microsoft.com/ems o aggiornare un articolo esistente.

1. Avviare Git Bash. 

2. Passare al repository `emdocs`:

        cd emdocs
        
3. Creare un nuovo ramo di lavoro:

        git checkout <branchname>

4. Creare un nuovo ramo di lavoro locale:

        git pull origin master:<branchname>

5. Creare un nuovo articolo o apportare modifiche a un articolo esistente. Usare Atom (http://atom.io), o un altro editor di preferenza, come editor Markdown per creare e aprire i nuovi file Markdown. Dopo aver creato o modificato l'articolo e le immagini, andare al passaggio successivo.

6. Aggiungere i file creati ed eseguirne il commit:

        git add <path-to-file>
        git commit –m "<comment>"
        
   In alternativa, per eseguire il commit solo di alcuni file modificati:

        git commit -a –m "<comment>"

7. Informare l'origine che è stato creato il ramo di lavoro locale:

        git push origin <branchname>

8. Eseguire il push delle modifiche nel ramo in GitHub:

        git push origin <branchname>

9. Quando si è pronti per inviare il contenuto al ramo master per la gestione temporanea, la convalida, e/o la pubblicazione nell'interfaccia utente di GitHub, creare una richiesta pull dal ramo locale al ramo master.

10. Il destinatario della richiesta pull esamina la richiesta, genera un feedback e/o accetta la richiesta pull. 

11. Facoltativamente, è possibile verificare le modifiche apportate o l'articolo pubblicato all'indirizzo
<span style="color:red;">È necessario l'URL corretto per la visualizzazione degli articoli pubblicati.</span>
 http://docs.microsoft.com/ems/articles/nome-articolo-senza-estensione-MD


<!--HONumber=Mar16_HO1-->


