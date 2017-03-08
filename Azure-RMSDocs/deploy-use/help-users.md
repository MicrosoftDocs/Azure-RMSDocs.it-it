---
title: Consentire agli utenti di proteggere i file con Azure RMS - AIP
description: Informazioni per fornire istruzioni a utenti, amministratori e addetti del servizio help desk dopo aver distribuito e configurato il servizio Azure Rights Management di Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/02/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 58f9a6ff-4121-4c8c-9865-1bb290604ad2
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 1300b0abb3cb59ad09075418ab8c911466740a2c
ms.openlocfilehash: f1d2db08951c1d017ea4f011855d99423fa9d577
ms.lasthandoff: 03/03/2017


---

# <a name="helping-users-to-protect-files-by-using-the-azure-rights-management-service"></a>Consentire agli utenti di proteggere i file mediante il servizio Azure Rights Management

>*Si applica a: Azure Information Protection, Office 365*

Dopo aver distribuito e configurato Azure Information Protection per l'organizzazione, è necessario fornire indicazioni e istruzioni agli utenti, agli amministratori e agli addetti del servizio help desk:

-   **Informazioni per l'utente finale:**

    Gli utenti devono conoscere come e quando proteggere i documenti e i messaggi di posta elettronica che contengono informazioni riservate. Quando possibile, è necessario fornire queste informazioni per i flussi di lavoro esistenti per consentire di incorporare i passaggi aggiuntivi in un processo già noto anziché introdurre processi completamente nuovi. Assicurarsi di comunicare loro i vantaggi (e i rischi) specifici dell'azienda nonché di fornire le istruzioni per la protezione di file e di messaggi di posta elettronica. Se sono stati configurati [modelli personalizzati](configure-custom-templates.md), specificare le istruzioni su come selezionarne uno qualora il nome e la descrizione del modello non siano sufficienti per scegliere quello corretto.

    > [!TIP]
    > Video di esempio per gli utenti finali:
    >
    > -   [Esperienza utente di Azure RMS](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-user-experience)
    > -   [Revoca e rilevamento dei documenti di Azure RMS](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation)

-   **Informazioni per gli amministratori:**

    In alcune applicazioni la protezione delle informazioni viene automaticamente adottata tramite criteri e impostazioni configurati dagli amministratori. È necessario pertanto fornire istruzioni agli altri amministratori che gestiscono tali applicazioni e servizi. Per altre informazioni, vedere [Supporto del servizio Azure Rights Management da parte delle applicazioni](../understand-explore/applications-support.md) e [Configurazione di applicazioni per il servizio Azure Rights Management](configure-applications.md).

-   **Informazioni per il supporto tecnico:**

    Uno degli strumenti più utili per il supporto tecnico è [RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437). Gli operatori del supporto tecnico possono eseguirlo con l'opzione di amministratore di Azure RMS e possono richiedere agli utenti di eseguirlo con l'opzione utente di Azure RMS. Questo strumento consente non solo di identificare eventuali problemi, ma anche di risolvere quelli individuati e, se non risolti, di registrare log di traccia.
    
    Se gli utenti eseguono il client Azure Information Protection, gli operatori del supporto tecnico possono chiedere loro di usare l'opzione **Guida e commenti**, **Esegui diagnostica** e successivamente reimpostare il client. Tuttavia, a differenza di quanto avviene per RMS Analyzer, la reimpostazione non determina la disconnessione dell'utente o la ripetizione del bootstrap del client e non è prevista alcuna correzione automatica.

    Se sono presenti richieste legittime per ottenere diritti completi di accesso a documenti protetti, ad esempio una richiesta da parte del reparto legale o di un responsabile dopo che un dipendente ha lasciato l'organizzazione, verificare che il supporto tecnico abbia definito le procedure per richiederlo usando la [funzionalità per utenti con privilegi avanzati](configure-super-users.md) di Azure Rights Management.

    Inoltre, di seguito sono riportati alcuni dei problemi tipici che potrebbero segnalare gli utenti:

    -   **Guida per l'accesso:**

        Quando il servizio Azure Rights Management deve autenticare un utente e non può usare le credenziali memorizzate nella cache, è possibile che all'utente venga chiesto di immettere le credenziali. Tali credenziali sono costituite dal nome dell'account e dalla password aziendali o dell'istituto di istruzione associati al tenant di Office 365 o di Azure Active Directory. L'account non è un account Microsoft (in precedenza Microsoft Live ID) né un account di posta elettronica personale, perché tali account non sono attualmente supportati dal servizio Azure Rights Management. Fornire agli utenti e agli addetti del servizio help desk istruzioni sugli account da usare nel caso in cui gli utenti debbano immettere le proprie credenziali quando usano tali applicazioni con il servizio Azure Rights Management.

    -   **Problemi di protezione o fruizione dei contenuti:**

        Verificare che gli utenti abbiano le istruzioni appropriate per le applicazioni usate e che stiano usando applicazioni e dispositivi supportati dal servizio Azure Rights Management. Per altre informazioni sui dispositivi e le applicazioni supportate, vedere [Requisiti per Azure Rights Management](../get-started/requirements-azure-rms.md).

        Se viene visualizzato un errore durante il tentativo di protezione o fruizione del contenuto, chiedere loro di eseguire [RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437) come un utente di Azure RMS.

        Se gli utenti segnalano che possono aprire contenuti protetti ma che non dispongono dei diritti di cui hanno bisogno, chiedere loro di eseguire [RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437) come un utente di Azure RMS, quindi scaricare e visualizzare i modelli. In questo modo, si verificherà che gli utenti abbiano correttamente scaricato i modelli e i relativi diritti forniti. Il problema potrebbe essere dovuto al fatto che l'utente non sia presente nel gruppo corretto configurato per il modello o che il modello debba essere riconfigurato per l'utente.

Nelle sezioni seguenti sono disponibili informazioni specifiche delle applicazioni che consentono agli utenti di proteggere documenti e messaggi di posta elettronica riservati.

## <a name="using-information-protection-with-the-azure-information-protection-client"></a>Protezione delle informazioni con il client Azure Information Protection
Il client Azure Information Protection potrebbe essere necessario per consentire agli utenti di proteggere e di utilizzare messaggi di posta elettronica e documenti protetti quando usano Office 2010, ma è anche consigliato per tutti i computer e i dispositivi mobili.

Oltre a rendere più semplice per gli utenti la protezione di documenti importanti, il client Azure Information Protection consente di tenere traccia dei documenti protetti e, se necessario, di revocarne l'accesso.

Per istruzioni sull'uso di questo client per computer Windows, vedere la [Guida per l'utente del client Azure Information Protection](../rms-client/client-user-guide.md).


## <a name="using-information-protection-with-office-365-office-2016-or-office-2013"></a>Uso della protezione delle informazioni con Office 365 oppure Office 2016 o Office 2013
Se si sta usando il servizio Azure Rights Management e il client Azure Information Protection non è stato installato, gli utenti non vedranno la barra di Azure Information Protection nelle app desktop di Office, il pulsante **Proteggi** sulla barra multifunzione o il comando **Classifica e proteggi** in Esplora file, che semplifica l'applicazione della protezione ai file. Tali utenti devono seguire istruzioni simili alle seguenti.

> [!TIP]
> Per trovare indicazioni e istruzioni specifiche dell'applicazione per l'uso della protezione delle informazioni in tali applicazioni, cercare **IRM** e il nome e la versione dell'applicazione.

#### <a name="to-protect-a-document-in-word-2013"></a>Per proteggere un documento in Word 2013

1.  In Microsoft Word creare un nuovo documento.

2.  Nel menu **File** , fare clic su **Info**, **Proteggi documento**, **Limita l'accesso**, quindi scegliere un modello per applicare rapidamente i diritti d'utilizzo corretti oppure selezionare **Limita l'accesso** e selezionare manualmente i diritti di utilizzo.

    > [!NOTE]
    > Se è la prima volta che si usa Rights Management, si verrà messi in contatto con il servizio [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] e verranno richieste le credenziali per configurare il client Office IRM.

3.  Salvare il documento.

Quando altri utenti aprono il documento, vengono prima autenticati. Se non sono autorizzati, il documento non viene aperto. Se invece sono autorizzati, il documento viene aperto con i diritti d'uso limitati indicati per l'utente specifico. Un diritto d'uso di sola visualizzazione, ad esempio, non consente all'utente di modificare o di salvare il documento, anche se quest'ultimo viene prima copiato in un percorso diverso. I diritti d'uso vengono visualizzati nella parte superiore del documento in un banner di limitazioni, in cui possono essere visualizzate le autorizzazioni applicate al documento o può essere presente un collegamento per visualizzarle.

#### <a name="to-protect-an-email-message-using-outlook-2013-and-exchange-online"></a>Per proteggere un messaggio di posta elettronica in Outlook 2013 e in Exchange Online

1.  In Outlook creare un nuovo messaggio di posta elettronica indirizzato a un destinatario presente nell'organizzazione.

2.  Nella scheda **OPZIONI** fare clic su **Autorizzazione**, quindi selezionare un'opzione. Ad esempio: **Non inoltrare**, **&lt;Nome società&gt; - Riservato** o **&lt;Nome società&gt; - Solo visualizzazione riservata**.

3.  Inviare il messaggio.

In modo analogo alla visualizzazione di un documento protetto, quando i destinatari ricevono il messaggio di posta elettronica vengono prima autenticati. Se sono autorizzati a visualizzare il messaggio di posta elettronica, quest'ultimo viene aperto con i diritti d'uso limitati indicati per l'utente specifico. Se ad esempio è stata selezionata l'opzione **Non inoltrare**, il pulsante Inoltra sulla barra multifunzione non è disponibile.

#### <a name="to-protect-an-email-message-using-the-outlook-web-app"></a>Per proteggere un messaggio di posta elettronica in Outlook Web App

1.  In Outlook Web App creare un nuovo messaggio di posta elettronica indirizzato a un destinatario presente nell'organizzazione.

2.  Fare clic su  **…**, fare clic su **Imposta autorizzazione**, quindi selezionare un'opzione. Ad esempio: **Non inoltrare**, **Non rispondere a tutti**, **&lt;Nome società&gt; - Riservato** o **&lt;Nome società&gt; - Solo visualizzazione riservata**.

3.  Inviare il messaggio.

In modo analogo alla visualizzazione di un documento protetto, quando i destinatari ricevono il messaggio di posta elettronica vengono prima autenticati. Se sono autorizzati a visualizzare il messaggio di posta elettronica, quest'ultimo viene aperto con i diritti d'uso limitati indicati per l'utente specifico. Se ad esempio è stata selezionata l'opzione **Non rispondere a tutti**, l'opzione **RISPONDI A TUTTI** nella finestra del messaggio non è disponibile.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


