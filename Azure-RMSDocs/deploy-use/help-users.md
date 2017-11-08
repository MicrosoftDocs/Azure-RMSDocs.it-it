---
title: Consentire agli utenti di proteggere i file con Azure RMS - AIP
description: Informazioni per fornire istruzioni a utenti, amministratori e addetti del servizio help desk dopo aver distribuito e configurato il servizio Azure Rights Management di Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/20/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 58f9a6ff-4121-4c8c-9865-1bb290604ad2
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 29a85bf1bf216c785a1b9cd6511069fe688327db
ms.sourcegitcommit: 73973986ae7086e6f30cab579187241fd98bef61
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/21/2017
---
# <a name="helping-users-to-protect-files-by-using-the-azure-rights-management-service"></a>Consentire agli utenti di proteggere i file mediante il servizio Azure Rights Management

>*Si applica a: Azure Information Protection, Office 365*

Dopo aver distribuito e configurato Azure Information Protection per l'organizzazione, è necessario fornire indicazioni e istruzioni agli utenti, agli amministratori e agli addetti del servizio help desk:

-   **Informazioni per l'utente finale**
    
    Gli utenti devono conoscere come e quando proteggere i documenti e i messaggi di posta elettronica che contengono informazioni riservate. Quando possibile, specificare queste informazioni per i flussi di lavoro esistenti per consentire agli utenti di incorporare i passaggi aggiuntivi in un processo già noto anziché introdurre nuovi processi. Assicurarsi di comunicare loro i vantaggi (e i rischi) specifici dell'azienda nonché di fornire le istruzioni per la protezione di file e di messaggi di posta elettronica. Se sono stati configurati dei [modelli](configure-policy-templates.md), specificare le istruzioni su come selezionarne uno qualora il nome e la descrizione del modello non siano sufficienti per scegliere quello corretto.
    
    > [!TIP]
    > Video di esempio per gli utenti finali:
    > -   [Microsoft Azure Information Protection](https://youtu.be/ToShAUdlrPo?list=PL8nfc9haGeb6qSm1kLU8n3Zqg398764h5)
    > -   [Revoca e rilevamento dei documenti di Azure RMS](http://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation)

-   **Informazioni per gli amministratori**
    
    In alcune applicazioni la protezione delle informazioni viene automaticamente adottata tramite criteri e impostazioni configurati dagli amministratori. È necessario pertanto fornire istruzioni agli altri amministratori che gestiscono tali applicazioni e servizi. 
    
    Per altre informazioni, vedere [Supporto del servizio Azure Rights Management da parte delle applicazioni](../understand-explore/applications-support.md) e [Configurazione di applicazioni per il servizio Azure Rights Management](configure-applications.md).
    
-   **Informazioni per il supporto tecnico**
    
    Se gli utenti dispongono del client Azure Information Protection, gli operatori del supporto tecnico possono chiedere loro di usare l'opzione **Guida e commenti** per informazioni, ad esempio per sapere se l'edizione di Office in uso non è in grado di supportare la protezione e l'account utente attualmente connesso. Questa opzione può essere usata anche per raccogliere i file di log e reimpostare il client. Per altre informazioni, vedere la sezione [Controlli aggiuntivi e risoluzione dei problemi](../rms-client/client-admin-guide.md#installation-checks-and-troubleshooting) della guida dell'amministratore.
    
    Se sono presenti richieste legittime per ottenere diritti completi di accesso a documenti protetti, verificare che l'help desk abbia definito le procedure per richiederlo usando la [funzionalità per utenti con privilegi avanzati](configure-super-users.md) di Azure Rights Management. Ad esempio, le richieste potrebbero provenire dall'ufficio legale o da un responsabile dopo che un dipendente ha lasciato l'organizzazione.
    
    Inoltre, alcuni dei problemi tipici che gli utenti potrebbero segnalare includono le categorie seguenti:
    
    - **Guida per l'accesso**
        
        Quando il servizio Azure Rights Management deve autenticare un utente e non può usare le credenziali memorizzate nella cache, è possibile che all'utente venga chiesto di immettere le credenziali. Le credenziali richieste sono costituite dal nome dell'account aziendale o dell'istituto di istruzione e dalla password associata al tenant di Office 365 o di Azure Active Directory. Le credenziali richieste non sono relative a un account Microsoft (in precedenza Microsoft Live ID) né a un account di posta elettronica personale, perché tali account non sono attualmente supportati dal servizio Azure Rights Management. 
        
        Fornire agli utenti e agli addetti del servizio help desk istruzioni sugli account da usare nel caso in cui gli utenti debbano immettere le proprie credenziali quando dispongono di applicazioni che usano il servizio Azure Rights Management.
        
    - **Problemi di protezione o fruizione dei contenuti**
        
        Verificare che gli utenti abbiano le istruzioni appropriate per le applicazioni usate e che stiano usando applicazioni e dispositivi supportati dal servizio Azure Rights Management. Per altre informazioni sui dispositivi e le applicazioni supportate, vedere [Requisiti per Azure Rights Management](../get-started/requirements-azure-rms.md).
        
        L'autenticazione e l'autorizzazione si basano su account e gruppi di Azure Active Directory. Per verificare se un utente o un gruppo specifico può essere autorizzato a consumare contenuto protetto, usare i controlli di verifica in [Preparazione di utenti e gruppi per Azure Information Protection](../plan-design/prepare.md).
        
        Se un utente indica che è in grado di aprire il contenuto protetto ma non ha i diritti necessari, il problema può essere dovuto al fatto che l'utente non è incluso nel gruppo corretto configurato per un modello di Rights Management, oppure che il [modello debba essere riconfigurato](configure-policy-templates.md) per l'utente o il gruppo. 
        
        Se i diritti degli utenti non sono quelli previsti, controllare la relativa descrizione e l'eventuale implementazione specifica dell'applicazione nella [tabella dei diritti di utilizzo](../deploy-use/configure-usage-rights.md#usage-rights-and-descriptions).

Nelle sezioni seguenti sono disponibili informazioni specifiche delle applicazioni che consentono agli utenti di proteggere documenti e messaggi di posta elettronica.

## <a name="using-information-protection-with-the-azure-information-protection-client"></a>Protezione delle informazioni con il client Azure Information Protection

Se gli utenti usano Office 2010, il client Azure Information Protection, o l'applicazione RMS sharing in uso in precedenza, deve proteggere e usare documenti e messaggi di posta elettronica protetti. Tuttavia, il client Azure Information Protection è consigliabile anche per tutti i computer e dispositivi mobili che supportano questo servizio.

Oltre a rendere più semplice per gli utenti la protezione di documenti e messaggi di posta elettronica, il client Azure Information Protection consente di tenere traccia dei documenti protetti. I documenti rilevati possono anche essere revocati se gli utenti autorizzati in precedenza non devono più avere accesso agli stessi.

Per istruzioni sull'uso di questo client per computer Windows, vedere la [Guida per l'utente del client Azure Information Protection](../rms-client/client-user-guide.md).


## <a name="using-information-protection-with-office-365-office-2016-or-office-2013"></a>Uso della protezione delle informazioni con Office 365 oppure Office 2016 o Office 2013
Se si sta usando il servizio Azure Rights Management e il client Azure Information Protection non è stato installato, gli utenti non vedono la barra di Azure Information Protection nelle app desktop di Office, il pulsante **Proteggi** sulla barra multifunzione o il comando **Classifica e proteggi** in Esplora file. Queste aggiunte semplificano l'applicazione della protezione a documenti e messaggi di posta elettronica. Tali utenti devono seguire istruzioni simili alle seguenti.

> [!TIP]
> Per trovare indicazioni e istruzioni specifiche dell'applicazione per l'uso della protezione delle informazioni in tali applicazioni, cercare **IRM** e il nome e la versione dell'applicazione.

#### <a name="to-protect-a-document-in-word-2013"></a>Per proteggere un documento in Word 2013

1.  Creare un documento in Microsoft Word.

2.  Dal menu **File** fare clic su **Info**, su **Proteggi documento** e quindi su **Limitazione accesso**.

3. Scegliere un modello per applicare rapidamente i diritti di utilizzo appropriati oppure selezionare **Limitazione accesso** e selezionare i diritti manualmente.

    > [!NOTE]
    > Se Rights Management non è mai stato usato nel computer, l'opzione **Limitazione accesso** consente di connettersi al servizio [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] e vengono richieste le credenziali per la configurazione del client Office IRM. È quindi possibile scegliere un modello o i diritti di utilizzo.

3.  Salvare il documento.

Quando altri utenti aprono il documento, vengono prima autenticati. Se non sono autorizzati, il documento non viene aperto. Se invece sono autorizzati, il documento viene aperto con i [diritti di utilizzo](../deploy-use/configure-usage-rights.md) limitati indicati per l'utente specifico. 

Un diritto d'uso di sola visualizzazione, ad esempio, non consente all'utente di modificare o di salvare il documento, anche se quest'ultimo viene prima copiato in un percorso diverso. 

I diritti d'uso vengono visualizzati nella parte superiore del documento in un banner di limitazioni, in cui possono essere visualizzate le autorizzazioni applicate al documento o può essere presente un collegamento per visualizzarle.

#### <a name="to-protect-an-email-message-using-outlook-2013-and-exchange-online"></a>Per proteggere un messaggio di posta elettronica in Outlook 2013 e in Exchange Online

1.  In Outlook creare un messaggio di posta elettronica indirizzato a un destinatario presente nell'organizzazione.

2.  Nella scheda **OPZIONI** fare clic su **Autorizzazione**, quindi selezionare un'opzione. Ad esempio: **Non inoltrare** o **\<Nome società>- Riservato** o **\<Nome società> - Solo visualizzazione riservata**.

3.  Inviare il messaggio.

In modo analogo alla visualizzazione di un documento protetto, quando i destinatari aprono il messaggio di posta elettronica protetto vengono prima autenticati. Se sono autorizzati a visualizzare il messaggio di posta elettronica, quest'ultimo viene aperto con i [diritti di utilizzo](../deploy-use/configure-usage-rights.md) limitati indicati per l'utente specifico. 

Ad esempio, se il messaggio di posta elettronica è stato protetto usando l'opzione **Non inoltrare**, il pulsante Inoltra sulla barra multifunzione non è disponibile.

#### <a name="to-protect-an-email-message-using-outlook-on-the-web"></a>Per proteggere un messaggio di posta elettronica in Outlook sul Web

1.  In Outlook sul Web creare un messaggio di posta elettronica indirizzato a un destinatario presente nell'organizzazione.

2.  Fare clic su  **…**, fare clic su **Imposta autorizzazione**, quindi selezionare un'opzione. Ad esempio: **Non inoltrare** o **Non rispondere a tutti**. O **\<Nome società> - Riservato** o **\<Nome società> - Solo visualizzazione riservata**.

3.  Inviare il messaggio.

In modo analogo alla visualizzazione di un documento protetto, quando i destinatari aprono il messaggio di posta elettronica vengono prima autenticati. Se sono autorizzati a visualizzare il messaggio di posta elettronica, quest'ultimo viene aperto con i [diritti di utilizzo](../deploy-use/configure-usage-rights.md) limitati indicati per l'utente specifico. 

Se ad esempio è stata selezionata l'opzione **Non rispondere a tutti**, l'opzione **RISPONDI A TUTTI** nella finestra del messaggio non è disponibile.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

