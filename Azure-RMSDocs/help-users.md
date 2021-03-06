---
title: Consentire agli utenti di proteggere i file con Azure RMS - AIP
description: Informazioni per fornire istruzioni a utenti, amministratori e addetti del servizio help desk dopo aver distribuito e configurato il servizio Azure Rights Management di Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/04/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 58f9a6ff-4121-4c8c-9865-1bb290604ad2
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 1a52e867d72b2dabc910bfb4e0378c04ed03a5ab
ms.sourcegitcommit: f6d536b6a3b5e14e24f0b9e58d17a3136810213b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98809500"
---
# <a name="helping-users-to-protect-files-by-using-the-azure-rights-management-service"></a>Consentire agli utenti di proteggere i file mediante il servizio Azure Rights Management

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Rilevante per**: [Client di etichettatura unificata e client classico di AIP](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Dopo aver distribuito e configurato Azure Information Protection per l'organizzazione, è necessario fornire indicazioni e istruzioni agli utenti, agli amministratori e agli addetti del servizio help desk:

-   **Informazioni sull'utente finale**
    
    Gli utenti devono conoscere come e quando proteggere i documenti e i messaggi di posta elettronica che contengono informazioni riservate. Quando possibile, specificare queste informazioni per i flussi di lavoro esistenti per consentire agli utenti di incorporare i passaggi aggiuntivi in un processo già noto anziché introdurre nuovi processi. Assicurarsi di comunicare loro i vantaggi (e i rischi) specifici dell'azienda nonché di fornire le istruzioni per la protezione di file e di messaggi di posta elettronica. 

    Se si dispone del client AIP classico e sono stati configurati [modelli](configure-policy-templates.md), fornire istruzioni su quale selezionare se il nome e la descrizione del modello non sono sufficienti per scegliere quello corretto.
    
    > [!TIP]
    > Video di esempio per gli utenti finali:
    > -   [Microsoft Azure Information Protection](https://youtu.be/ToShAUdlrPo?list=PL8nfc9haGeb6qSm1kLU8n3Zqg398764h5)
    > -   [Revoca e rilevamento dei documenti di Azure RMS](https://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation)

-   **Informazioni amministratore**
    
    In alcune applicazioni la protezione delle informazioni viene automaticamente adottata tramite criteri e impostazioni configurati dagli amministratori. È necessario pertanto fornire istruzioni agli altri amministratori che gestiscono tali applicazioni e servizi. 
    
    Per altre informazioni, vedere [Supporto del servizio Azure Rights Management da parte delle applicazioni](applications-support.md) e [Configurazione di applicazioni per il servizio Azure Rights Management](configure-applications.md).
    
-   **Informazioni sul supporto tecnico**
    
    Se gli utenti dispongono del client Azure Information Protection, gli operatori del supporto tecnico possono chiedere loro di usare l'opzione **Guida e commenti** per informazioni, ad esempio per sapere se l'edizione di Office in uso non è in grado di supportare la protezione e l'account utente attualmente connesso. Questa opzione può essere usata anche per raccogliere i file di log e reimpostare il client. Per altre informazioni, vedere la sezione [Controlli aggiuntivi e risoluzione dei problemi](./rms-client/clientv2-admin-guide.md#installation-checks-and-troubleshooting) della guida dell'amministratore.
    
    Se sono presenti richieste legittime per ottenere diritti completi di accesso ai documenti protetti, verificare che il help desk disponga di processi per richiedere l'accesso tramite la [funzionalità Azure Information Protection utente con privilegi avanzati](configure-super-users.md). Ad esempio, le richieste potrebbero provenire dall'ufficio legale o da un responsabile dopo che un dipendente ha lasciato l'organizzazione.
    
    Inoltre, alcuni dei problemi tipici che gli utenti potrebbero segnalare includono le categorie seguenti:
    
    - **Guida per l'accesso**
        
        Quando il servizio Azure Rights Management deve autenticare un utente e non può usare le credenziali memorizzate nella cache, è possibile che all'utente venga chiesto di immettere le credenziali. Le credenziali richieste sono in genere quelle per l'account aziendale o dell'istituto di istruzione dell'utente e per la password associati al tenant di Office 365 o di Azure Active Directory. Anche se il servizio Azure Rights Management può autenticare account Azure AD, alcune applicazioni possono aprire contenuti protetti anche quando viene usato un account Microsoft per l'autenticazione. [Altre informazioni](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents) 
        
        Fornire agli utenti e agli addetti del servizio help desk istruzioni sugli account da usare nel caso in cui gli utenti debbano immettere le proprie credenziali quando dispongono di applicazioni che usano il servizio Azure Rights Management.
        
    - **Problemi di protezione o utilizzo del contenuto**
        
        Verificare che gli utenti abbiano le istruzioni appropriate per le applicazioni usate e che stiano usando applicazioni e dispositivi supportati dal servizio Azure Rights Management. Per ulteriori informazioni sulle applicazioni e sui dispositivi supportati, vedere [requisiti per Azure Information Protection](requirements.md).
        
        Per verificare se un utente o un gruppo specifico può essere autorizzato da Azure Active Directory a proteggere o utilizzare contenuti protetti, usare i controlli di verifica presentati in [Preparazione di utenti e gruppi per Azure Information Protection](prepare.md).
        
        Se i diritti degli utenti non sono quelli previsti, controllare la relativa descrizione e l'eventuale implementazione specifica dell'applicazione nella [tabella dei diritti di utilizzo](configure-usage-rights.md#usage-rights-and-descriptions).

        **Solo client classico**: se gli utenti segnalano che possono aprire contenuto protetto ma non hanno i diritti necessari, il problema potrebbe essere dovuto al fatto che l'utente non si trova nel gruppo corretto configurato per un modello di Rights Management. oppure che il [modello debba essere riconfigurato](configure-policy-templates.md) per l'utente o il gruppo. 
        
        
Nelle sezioni seguenti sono disponibili informazioni specifiche delle applicazioni che consentono agli utenti di proteggere documenti e messaggi di posta elettronica.

## <a name="using-information-protection-with-the-azure-information-protection-client"></a>Protezione delle informazioni con il client Azure Information Protection

Se gli utenti usano Office 2010, il client Azure Information Protection è necessario per proteggere e utilizzare documenti e messaggi di posta elettronica protetti. Tuttavia, il client Azure Information Protection è consigliabile anche per tutti i computer e dispositivi mobili che supportano questo servizio.

Oltre a rendere più semplice per gli utenti la protezione di documenti e messaggi di posta elettronica, il client Azure Information Protection consente di tenere traccia dei documenti protetti. I documenti rilevati possono anche essere revocati se gli utenti autorizzati in precedenza non devono più avere accesso agli stessi.

Per istruzioni sull'uso di questo client per computer Windows, vedere la [Guida per l'utente del client Azure Information Protection](./rms-client/clientv2-user-guide.md).


## <a name="using-information-protection-with-office-365-office-2019-office-2016-or-office-2013"></a>Uso della protezione delle informazioni con Office 365, Office 2019, Office 2016 o Office 2013

Se si sta usando il servizio Azure Rights Management e il client Azure Information Protection non è stato installato, gli utenti non vedono la barra di Azure Information Protection nelle app desktop di Office, Non è inoltre possibile visualizzare il pulsante **sensitivity** sulla barra multifunzione o **classificare e proteggere** da Esplora file. Queste aggiunte semplificano l'applicazione della protezione a documenti e messaggi di posta elettronica. Tali utenti devono seguire istruzioni simili alle seguenti.

> [!TIP]
> Per trovare indicazioni e istruzioni specifiche dell'applicazione per adottare la protezione delle informazioni in tali applicazioni, cercare **IRM** e il nome e la versione dell'applicazione.

#### <a name="to-protect-a-document-in-word-from-office-365-proplus"></a>Per proteggere un documento in Word da Office 365 ProPlus

1.  Creare un documento in Microsoft Word.

2.  Dal menu **file** : **informazioni**  >  **Proteggi documento**  >   **limita accesso**.

3. Scegliere un modello per applicare rapidamente i diritti di utilizzo appropriati oppure selezionare **Limitazione accesso** e selezionare i diritti manualmente.

    > [!NOTE]
    > Se Rights Management non è mai stato usato nel computer, l'opzione **Limitazione accesso** consente di connettersi al servizio Azure Rights Management e vengono richieste le credenziali per la configurazione del client Office IRM. È quindi possibile scegliere un modello o i diritti di utilizzo.

3.  Salvare il documento.

Quando altri utenti aprono il documento, vengono prima autenticati. Se non sono autorizzati, il documento non viene aperto. Se sono autorizzati ad aprire il documento, si apre con i diritti di [utilizzo](configure-usage-rights.md) limitati specificati per tale utente. 

Un diritto d'uso di sola visualizzazione, ad esempio, non consente all'utente di modificare o di salvare il documento, anche se quest'ultimo viene prima copiato in un percorso diverso. 

I diritti d'uso vengono visualizzati nella parte superiore del documento in un banner di limitazioni, in cui possono essere visualizzate le autorizzazioni applicate al documento o può essere presente un collegamento per visualizzarle.

#### <a name="to-protect-an-email-message-using-outlook-from-office-365-proplus-connecting-to-exchange-online"></a>Per proteggere un messaggio di posta elettronica in Outlook da Office 365 ProPlus, con connessione a Exchange Online

1.  In Outlook creare un messaggio di posta elettronica indirizzato a un destinatario presente nell'organizzazione.

2.  Dalla scheda **Opzioni** : **autorizzazione** > selezionare un'opzione. Ad esempio: non **inviare** né **\<Company Name> -Confidential**, né **\<Company Name> -solo la visualizzazione riservata**.

3.  Inviare il messaggio.

In modo analogo alla visualizzazione di un documento protetto, quando i destinatari aprono il messaggio di posta elettronica protetto vengono prima autenticati. Se sono autorizzati a visualizzare il messaggio di posta elettronica, viene aperto con i [diritti di utilizzo](configure-usage-rights.md) limitati specificati per tale utente. 

Ad esempio, se il messaggio di posta elettronica è stato protetto usando l'opzione **Non inoltrare**, il pulsante Inoltra sulla barra multifunzione non è disponibile.

#### <a name="to-protect-an-email-message-using-outlook-on-the-web"></a>Per proteggere un messaggio di posta elettronica in Outlook sul Web

1. In Outlook sul Web creare un messaggio di posta elettronica indirizzato a un destinatario presente nell'organizzazione.

2. Selezionare **Proteggi**. A meno che l'impostazione predefinita non sia stata modificata da un amministratore, l'opzione **Non inoltrare** viene selezionata automaticamente. Se si desidera modificare il valore predefinito, selezionare **modifica autorizzazioni** e quindi selezionare un'opzione dall'elenco a discesa. Ad esempio: **Encrypt** o **\<Company Name> -Confidential**.

3. Inviare il messaggio.

In modo analogo alla visualizzazione di un documento protetto, quando i destinatari aprono il messaggio di posta elettronica vengono prima autenticati. Se sono autorizzati a visualizzare il messaggio di posta elettronica, viene aperto con i [diritti di utilizzo](configure-usage-rights.md) limitati specificati per tale utente. 

Ad esempio, con l'opzione predefinita **Non inoltrare**, l'opzione **Inoltra** nella finestra di messaggio non è disponibile.
