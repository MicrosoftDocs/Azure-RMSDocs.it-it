---
title: Guida alla distribuzione rapida di Rights Management di Azure | Azure RMS
description: "Una guida che consente di distribuire e usare più rapidamente Azure Rights Management (Azure RMS) per proteggere i dati dell'organizzazione. Iniziare scegliendo da un elenco di scenari specifici da implementare."
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: get-started-article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c994d616-cff6-4930-9228-a7f7d198a160
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 81426cf43f31625c6e83d443fa925f6426eb89da
ms.openlocfilehash: 715290d2417df3b386d8e5b8a784e964355d4e15


---

# Guida alla distribuzione rapida di Rights Management di Azure

>*Si applica a: Azure Rights Management, Office 365*

Usare questa Guida, oltre alle informazioni di configurazione presenti nella sezione **Distribuire e usare**, che consentono di distribuire e usare Azure Rights Management (Azure RMS) più rapidamente, scegliendo da un elenco di scenari specifici da implementare.

Questi scenari contengono sia istruzioni per l'amministratore sia documentazione di accompagnamento per gli utenti finali. Prima di distribuire la documentazione (istruzioni o annunci) agli utenti finali, è opportuno personalizzarla in base agli specifici requisiti aziendali e ai flussi di lavoro esistenti. Un set di istruzioni o un annuncio di esempio mostrano il potenziale aspetto della documentazione finale dell'utente finale.

Ciascuno scenario include un elenco di requisiti, con collegamento a eventuali informazioni aggiuntive necessarie, affinché sia possibile implementare tali soluzioni in modo indipendente e in qualsiasi ordine.

Gli scenari elencati di seguito sono un esempio di quelli più diffusi. Poiché Azure RMS può essere usato per proteggere le informazioni in un numero elevato di scenari all'interno dell'organizzazione e tra organizzazioni diverse, è possibile definire gli scenari personali e distribuirli nell'ambiente e agli utenti tramite lo stesso modello. Concentrando l'attenzione su scenari specifici, la distribuzione di Azure RMS si allineerà in maniera più precisa agli obiettivi aziendali. Inoltre, l'esperienza ci insegna che gli utenti tendono a seguire le istruzioni specifiche di uno scenario n maniera molto più precisa e sistematica rispetto a linee guida di carattere generale, come "proteggere i documenti riservati".

Prima di distribuire queste soluzioni, si può valutare di inviare un annuncio di ampio respiro agli utenti finali per informarli del fatto che sono previste alcune modifiche per proteggere i dati aziendali e che potrebbero essere richieste alcune modifiche. Dopo la tabella seguente è riportata una comunicazione di esempio.

> [!NOTE]
> Per eventuali domande e commenti inerenti a questa Guida, usare i meccanismi di commenti e suggerimenti in questa pagina, sfruttare i meccanismi di feedback o inviare un messaggio di posta elettronica all'indirizzo [AskIPTeam@Microsoft.com](mailto:%20askipteam@microsoft.com?subject=Rapid%20Deployment%20Guide%20feedback).

## Scenari per Azure RMS
Per distribuire più rapidamente Azure RMS per risolvere problemi aziendali specifici, scegliere gli scenari che meglio soddisfano gli obiettivi aziendali e adattarli ove necessario.



**Inviare un file di Office tramite posta elettronica in modo sicuro a utenti di un'altra organizzazione, con la possibilità di verificare l'accesso al file inviato (collaborazione business-to-business).**

Esempi:

- Invio di un listino prezzi, una guida di orientamento o piani di rilascio a un cliente.

- Invio di un ordine di lavoro o di specifiche marketing a un fornitore.

- Invio di un'offerta o di una richiesta di offerta a un partner.

Vedere: [Scenario - Condividere un file di Office con utenti in un'altra organizzazione](scenario-share-office-file-externally.md)

**Assicurare che i documenti archiviati in una raccolta di SharePoint rimangano sotto il proprio controllo**

Esempi:

- Fogli di calcolo e report dei reparti.

- Collaborazione tra team per documenti di progettazione o altri risultati finali

Vedere: [Scenario - Mantenere il controllo dei documenti archiviati in SharePoint](scenario-sharepoint.md)

**I dirigenti possono scambiare informazioni riservate tramite email in totale sicurezza**

Esempi:

- Condivisione di piani di acquisizione.

- Discussione o diffusione di problematiche legali.

- Informazioni su potenziali licenziamenti o altri argomenti delicati.

Vedere: [Scenario - Scambiarsi informazioni con privilegi tra dirigenti](scenario-executives-email.md)

**Proteggere automaticamente tutti i file in un server di file**

Esempi:

- Documenti CAD che devono essere mantenuti internamente per evitare la perdita della proprietà intellettuale

- I piani promozionali di marketing e le date da non rendere note al pubblico per mantenere un vantaggio competitivo

Vedere: [Scenario - Proteggere i file in una condivisione di file server](scenario-fci.md)

**Proteggere con molta attenzione i documenti più riservati, ad alto impatto ambientale**

Esempi:

- Informazioni sulla ricetta o la formula univoche per l'azienda

- Acquisizione o piani di fusione altamente classificati

- Dati di esplorazione delle risorse naturali

Vedere: [Scenario - Proteggere i file più importanti &#40;few&#41;](scenario-secure-most-valuable-files.md)

**Inviare in modo sicuro messaggi di posta elettronica e allegati aziendali riservati**

Esempi:

- Dichiarazione degli obiettivi aziendali

- Organigrammi, notizie di riorganizzazione o annunci di promozioni

- Informazioni sui criteri aziendali

Vedere: [Scenario - Invio di messaggi di posta elettronica aziendali riservati](scenario-company-confidential-email.md)

**Applicare protezione permanente per i file di Office nelle cartelle di lavoro**

Esempi:

- Documenti di Word modificati a livello locale per un progetto aziendale riservato

- Fogli di calcolo che contengono dati sensibili o ad alto impatto creati a livello locale

- Presentazioni di PowerPoint non definitive, memorizzate a livello locale, che non devono essere comunicate o accidentalmente condivise con utenti esterni all'organizzazione fino a quando la presentazione non è definitiva

Vedere: [Scenario - Configurare le cartelle per una protezione permanente](scenario-work-folders.md)




## Annuncio per gli utenti prima dell'implementazione
È possibile usare il seguente messaggio di comunicazione di esempio per informare gli utenti che la distribuzione di Azure RMS comporta l'arrivo di alcune modifiche. Copiare e incollare il testo seguente, da inviare tramite posta elettronica a tutti gli utenti dal team di leadership dell'organizzazione, preferibilmente l'amministratore delegato. È consigliabile apportare modifiche al testo che renderanno il messaggio più pertinente per gli utenti e l'organizzazione.

![Esempio di banner della documentazione dell'utente per la distribuzione rapida di Azure RMS](../media/AzRMS_ExampleBanner.png)

### Modifiche apportate per la protezione dei dati
Si è mai desiderato di bloccare l'accesso a un documento inviato ai partner per errore? Ci si è mai chiesti se esiste un modo per sapere quali clienti hanno letto le ultime novità sul prodotto inviate? È necessario condividere informazioni riservate senza preoccuparsi che potrebbero essere inviate a persone che non dovrebbero visualizzarle?

Presto sarà possibile eseguire queste operazioni perché il reparto IT sta apportando alcune modifiche che implementano Microsoft Azure Rights Management (Azure RMS) come soluzione di protezione dei dati. Molte di queste soluzioni applicheranno automaticamente la protezione necessaria, senza dover eseguire operazioni particolari. Tuttavia, alcune modifiche potrebbero richiedere l'esecuzione di operazioni in modo diverso e in questo caso, il reparto IT invierà le informazioni e le istruzioni, con il supporto dell'help desk in caso di domande o problemi.

Ad esempio, per tenere traccia (e se necessario, revocare) i documenti condivisi, sarà possibile usare il sito di rilevamento dei documenti:

![Screenshot del rilevamento dei documenti di Azure RMS](../media/AzRMS_Tutorial_5_Screenshots.png)

Per provare il funzionamento, è possibile guardare questo video di 2 minuti: [Revoca e rilevamento dei documenti di Azure RMS](https://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation)

Uno dei beni più preziosi dell'organizzazione sono i suoi dati, i dati generati, archiviati e usati su base giornaliera. Offrono il vantaggio competitivo e contribuiscono al successo. Ecco perché è così importante il controllo dei dati continuo e assicurarsi che gli utenti che non devono accedere, non possano accedervi.

Le soluzioni implementare risulteranno utili per proteggere i dati preziosi e offrono gli strumenti per mantenere il controllo dei dati. Grazie per la collaborazione mentre è in corso l'implementazione di tali modifiche.




<!--HONumber=Aug16_HO4-->


