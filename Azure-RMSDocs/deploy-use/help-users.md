---
# required metadata

title: Consentire agli utenti di proteggere i file tramite Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 58f9a6ff-4121-4c8c-9865-1bb290604ad2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Consentire agli utenti di proteggere i file tramite Azure Rights Management

*Si applica a: Azure Rights Management, Office 365*

Dopo aver distribuito e configurato Azure Rights Management (RMS) per l'organizzazione, è necessario fornire indicazioni e istruzioni agli utenti, agli amministratori e agli addetti del servizio help desk:

-   **Informazioni per l'utente finale**

    Gli utenti devono conoscere come e quando proteggere i documenti e i messaggi di posta elettronica che contengono informazioni riservate. Quando possibile, è necessario fornire queste informazioni per i flussi di lavoro esistenti per poter incorporare i passaggi aggiuntivi in un processo già noto anziché introdurre processi completamente nuovi. Assicurarsi di comunicare loro i vantaggi (e i rischi) specifici dell'azienda nonché di fornire le istruzioni per la protezione di file e di messaggi di posta elettronica. Se sono stati configurati [modelli personalizzati](configure-custom-templates.md), specificare le istruzioni su come selezionarne uno qualora il nome e la descrizione del modello non siano sufficienti per scegliere quello corretto.

    > [!TIP]
    > Video di esempio per gli utenti finali:
    >
    > -   [Esperienza utente di Azure RMS](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-user-experience)
    > -   [Revoca e rilevamento dei documenti di Azure RMS](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation)

-   **Informazioni per gli amministratori**

    In alcune applicazioni la protezione delle informazioni viene automaticamente adottata tramite criteri e impostazioni configurati dagli amministratori. È necessario pertanto fornire istruzioni agli altri amministratori che gestiscono tali applicazioni e servizi. Per altre informazioni, vedere [Supporto di Microsoft Azure Rights Management da parte delle applicazioni](../understand-explore/applications-support.md) e [Configurazione di applicazioni per Azure Rights Management](configure-applications.md).

-   **Informazioni sul supporto tecnico:**

    Uno degli strumenti più utili per il supporto tecnico è [RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437). Gli operatori del supporto tecnico possono eseguirlo con l'opzione di amministratore di Azure RMS e possono richiedere agli utenti di eseguirlo con l'opzione utente di Azure RMS. Questo strumento consente non solo di identificare eventuali problemi, ma anche di risolvere quelli individuati e, se non risolti, di registrare log di traccia.

    Se sono presenti richieste legittime per ottenere diritti completi di accesso a documenti protetti, ad esempio una richiesta da parte dell'ufficio legale o di un responsabile dopo che un dipendente ha lasciato l'organizzazione, verificare che il supporto tecnico abbia le procedure per richiederli usando la [funzionalità per utenti con privilegi avanzati](configure-super-users.md) di Azure RMS.

    Inoltre, di seguito sono riportati alcuni dei problemi tipici che potrebbero segnalare gli utenti:

    -   **Guida per l'accesso**

        Quando Azure RMS deve autenticare un utente e non può usare le credenziali memorizzate nella cache, agli utenti può venire richiesto di immettere le credenziali. Tali credenziali sono costituite dal nome dell'account e dalla password aziendali o dell'istituto di istruzione associati al tenant di Office 365 o di Azure Active Directory. L'account non è un account Microsoft (in precedenza Microsoft Live ID) né un account di posta elettronica personale, perché tali account non sono attualmente supportati da Azure RMS. Fornire agli utenti e agli addetti del servizio help desk istruzioni sugli account da usare quando agli utenti viene richiesto di immettere le proprie credenziali quando usano tali applicazioni con Azure RMS.

    -   **Problemi di protezione o fruizione di contenuto:**

        Verificare che gli utenti abbiano le istruzioni appropriate per le applicazioni usate e che stiano usando applicazioni e dispositivi supportati da Azure RMS. Per altre informazioni sulle applicazioni e i dispositivi supportati, vedere [Requisiti per Azure Rights Management](../get-started/requirements-azure-rms.md).

        Se viene visualizzato un errore durante il tentativo di protezione o fruizione del contenuto, chiedere loro di eseguire [RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437) come un utente di Azure RMS.

        Se gli utenti segnalano che possono aprire contenuti protetti ma che non dispongono dei diritti di cui hanno bisogno, chiedere loro di eseguire [RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437) come un utente di Azure RMS, quindi scaricare e visualizzare i modelli. In questo modo, si verificherà che gli utenti abbiano correttamente scaricato i modelli e i relativi diritti forniti. Il problema potrebbe essere dovuto al fatto che l'utente non sia presente nel gruppo corretto configurato per il modello o che il modello debba essere riconfigurato per l'utente.

Nelle sezioni seguenti sono disponibili informazioni specifiche delle applicazioni che consentono agli utenti di proteggere documenti e messaggi di posta elettronica riservati.

## Uso della protezione delle informazioni con l'applicazione di condivisione Rights Management
L'applicazione di condivisione Rights Management (RMS) è necessaria perché gli utenti proteggano e usino contenuto protetto con Office 2010, ma è anche consigliata per tutti i computer e i dispositivi mobili che supportano Azure RMS.

Oltre a rendere più semplice per gli utenti la protezione di documenti importanti, l'applicazione RMS sharing consente agli utenti di registrare i documenti protetti e, se necessario, revocarne l'accesso.

Per istruzioni sull'uso di questa applicazione per computer Windows, vedere [Guida dell'utente dell'applicazione di condivisione Rights Management](../rms-client/sharing-app-user-guide.md).

Per i dispositivi mobili, vedere [Domande frequenti sull'applicazione di condivisione Microsoft Rights Management per piattaforme mobili](http://technet.microsoft.com/dn451248).

> [!TIP]
> Per uno scenario di esempio generale con screenshot, vedere la pagina relativa alla [condivisione sicura di allegati con utenti mobili] (../understand-explore/what-admins-users-see.md#users-safely-share-attachments-with-mobile-users.

## Uso della protezione delle informazioni con Office 365 oppure Office 2016 o Office 2013
Se si usa Azure RMS e l'applicazione Rights Management sharing non è installata, gli utenti non visualizzeranno il pulsante **Condividi file protetto** sulla barra multifunzione o il pulsante **Proteggi sul posto** in Esplora file che semplifica la protezione dei file. Tali utenti devono seguire istruzioni simili alle seguenti.

> [!TIP]
> Per trovare indicazioni e istruzioni specifiche dell'applicazione per l'uso della protezione delle informazioni in tali applicazioni, cercare **IRM** e il nome e la versione dell'applicazione.

#### Per proteggere un documento in Word 2013

1.  In Microsoft Word creare un nuovo documento.

2.  Nel menu **File** , fare clic su **Info**, **Proteggi documento**, **Limita l'accesso**, quindi scegliere un modello per applicare rapidamente i diritti d'utilizzo corretti oppure selezionare **Limita l'accesso** e selezionare manualmente i diritti di utilizzo.

    > [!NOTE]
    > Se è la prima volta che si usa Rights Management, si verrà messi in contatto con il servizio [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] e verranno richieste le credenziali per configurare il client Office IRM.

3.  Salvare il documento.

Quando altri utenti aprono il documento, vengono prima autenticati. Se non sono autorizzati, il documento non viene aperto. Se invece sono autorizzati, il documento viene aperto con i diritti d'uso limitati indicati per l'utente specifico. Un diritto d'uso di sola visualizzazione, ad esempio, non consente all'utente di modificare o di salvare il documento, anche se quest'ultimo viene prima copiato in un percorso diverso. I diritti d'uso vengono visualizzati nella parte superiore del documento in un banner di limitazioni, in cui possono essere visualizzate le autorizzazioni applicate al documento o può essere presente un collegamento per visualizzarle.

#### Per proteggere un messaggio di posta elettronica in Outlook 2013 e in Exchange Online

1.  In Outlook creare un nuovo messaggio di posta elettronica indirizzato a un destinatario presente nell'organizzazione.

2.  Nella scheda **OPZIONI** fare clic su **Autorizzazione**, quindi selezionare un'opzione. Ad esempio: **Non inoltrare**, **&lt;Nome società&gt; - Riservato** o **&lt;Nome società&gt; - Solo visualizzazione riservata**.

3.  Inviare il messaggio.

In modo analogo alla visualizzazione di un documento protetto, quando i destinatari ricevono il messaggio di posta elettronica vengono prima autenticati. Se sono autorizzati a visualizzare il messaggio di posta elettronica, quest'ultimo viene aperto con i diritti d'uso limitati indicati per l'utente specifico. Se ad esempio è stata selezionata l'opzione **Non inoltrare**, il pulsante Inoltra sulla barra multifunzione non è disponibile.

#### Per proteggere un messaggio di posta elettronica in Outlook Web App

1.  In Outlook Web App creare un nuovo messaggio di posta elettronica indirizzato a un destinatario presente nell'organizzazione.

2.  Fare clic su  **…**, fare clic su **Imposta autorizzazione**, quindi selezionare un'opzione. Ad esempio: **Non inoltrare**, **Non rispondere a tutti**, **&lt;Nome società&gt; - Riservato** o **&lt;Nome società&gt; - Solo visualizzazione riservata**.

3.  Inviare il messaggio.

In modo analogo alla visualizzazione di un documento protetto, quando i destinatari ricevono il messaggio di posta elettronica vengono prima autenticati. Se sono autorizzati a visualizzare il messaggio di posta elettronica, quest'ultimo viene aperto con i diritti d'uso limitati indicati per l'utente specifico. Se ad esempio è stata selezionata l'opzione **Non rispondere a tutti**, l'opzione **RISPONDI A TUTTI** nella finestra del messaggio non è disponibile.




<!--HONumber=Apr16_HO4-->


