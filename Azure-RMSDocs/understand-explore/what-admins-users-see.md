---
# required metadata

title: Cosa visualizzano gli amministratori e gli utenti? | (Azure RMS)
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 06/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 013e0eb4-49a7-4e81-9e4d-f56c0ceb017f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Azure RMS in azione: Cosa vedono gli amministratori e gli utenti

*Si applica a: Azure Rights Management, Office 365*

Questo articolo mostra alcuni esempi tipici di come gli amministratori e gli utenti vedono e possono usare Azure Rights Management (RMS) per proteggere informazioni sensibili o riservate.

> [!NOTE] In questi esempi in cui i dati sono protetti da Azure RMS, il proprietario del contenuto continua ad avere accesso completo ai dati (file o posta elettronica), anche se la protezione applicata concede le autorizzazioni a un gruppo di cui il proprietario non fa parte o anche se la protezione applicata include una data di scadenza.
>
> Analogamente, il reparto IT può accedere sempre ai dati protetti senza restrizioni, usando la funzionalità Utente con privilegi avanzati di Rights Management che concede l'accesso delegato a specifici utenti autorizzati o servizi. Inoltre, il personale IT può tenere traccia e monitorare l'utilizzo per i dati che sono stati protetti, ad esempio chi accede ai dati e quando.

Per altre schermate e video che mostrano RMS in azione, vedere il [portale dei servizi di Microsoft Rights Management](http://www.microsoft.com/rms) e il [blog del team Microsoft Rights Management (RMS)](http://blogs.technet.com/b/rms).

## Attivazione e configurazione di Rights Management
Sebbene sia possibile usare Windows PowerShell per attivare e configurare Azure RMS, è più semplice procedere dal portale di gestione. Quando il servizio viene attivato, sono disponibili due modelli predefiniti che gli amministratori e gli utenti possono selezionare per applicare la protezione delle informazioni ai file in modo rapido e semplice. È anche possibile creare modelli personalizzati per includere opzioni e impostazioni aggiuntive.

![COSA VEDONO GLI AMMINISTRATORI DURANTE IL PASSAGGIO 1](../media/AzRMS_StoryboardActivate_small1.png)


**COSA VEDONO GLI AMMINISTRATORI DURANTE IL PASSAGGIO 1:** per attivare RMS, è possibile usare l'interfaccia di amministrazione di Office 365 (prima immagine) o il portale di Azure classico (seconda immagine).<br /><br />È sufficiente un clic per attivare e un altro clic per confermare e la protezione delle informazioni viene abilitata per gli amministratori e gli utenti nell'organizzazione.

---

![COSA VEDONO GLI AMMINISTRATORI DURANTE IL PASSAGGIO 2](../media/AzRMS_TemplatesPortal_small.png)

**COSA VEDONO GLI AMMINISTRATORI DURANTE IL PASSAGGIO 2:** dopo l'attivazione sono disponibili automaticamente due modelli di criteri di diritti per l'organizzazione. Un modello (il cui nome include **Solo visualizzazione riservata**) è di sola lettura, mentre l'altro (**Riservata**) consente l'accesso in lettura e modifica.

Quando questi modelli vengono applicati a file o messaggi di posta elettronica, limitano l'accesso agli utenti nell'organizzazione. Si tratta di un modo molto rapido e semplice per impedire che i dati aziendali archiviati vengano divulgati a utenti esterni all'organizzazione.

> [!TIP]
> Questi modelli predefiniti sono facilmente riconoscibili perché sono preceduti automaticamente dal nome dell'organizzazione, in questo esempio **VanArsdel, Ltd**

Se si preferisce non mostrare questi modelli agli utenti oppure creare modelli personalizzati, è possibile usare il portale di Azure classico. Come mostrato nella figura, una procedura guidata illustra il processo di creazione del modello personalizzato.

---

![COSA VEDONO GLI AMMINISTRATORI DURANTE IL PASSAGGIO 3](../media/AzRMS_TemplatesSettings3.png)

**COSA VEDONO GLI AMMINISTRATORI DURANTE IL PASSAGGIO 3:** se si decide di creare modelli personalizzati, sono disponibili diverse impostazioni di configurazione, tra cui accesso offline, impostazioni di scadenza e pubblicazione immediata del modello (per renderlo visibile nelle applicazioni che supportano Rights Management).

---

![COSA VEDONO GLI AMMINISTRATORI DURANTE IL PASSAGGIO 4](../media/AzRMS_TemplatesPortal_ExplorerWord3.png)

**COSA VEDONO GLI AMMINISTRATORI DURANTE IL PASSAGGIO 4**: in seguito alla pubblicazione, questi modelli possono essere selezionati, ad esempio in applicazioni quali Esplora file e Microsoft Word:

- un utente può scegliere il modello predefinito, **VanArsdel, Ltd – Riservata**. In seguito, solo i dipendenti dell'organizzazione VanArsdel possono aprire e usare questo documento, anche se successivamente viene inviato tramite posta elettronica all'esterno dell'organizzazione o salvato in una posizione pubblica.

- Un utente può scegliere il modello personalizzato creato dall'amministratore, **Vendite e Marketing - Solo lettura e stampa**. In questo modo, il file non solo è protetto da utenti esterni all'organizzazione, ma è limitato ai dipendenti del reparto Vendite e marketing. Inoltre, questi dipendenti non dispongono dei diritti completi per il documento, ma solo dei diritti di lettura e stampa. Ad esempio, non possono modificarlo né copiarne il contenuto.

---

**Per ulteriori informazioni relative a questo scenario:**

- Per istruzioni dettagliate, vedere [Attivazione di Azure Rights Management](../deploy-use/activate-service.md) e [Configurazione di modelli personalizzati per Azure Rights Management](../deploy-use/configure-custom-templates.md).

- Per consentire agli utenti di proteggere i file aziendali importanti, vedere [Consentire agli utenti di proteggere i file mediante Azure Rights Management](../deploy-use/help-users.md).

Di seguito sono disponibili alcuni esempi di come gli amministratori possono applicare i modelli per configurare automaticamente la protezione delle informazioni per i file e i messaggi di posta elettronica.

## Protezione automatica dei file su file server che eseguono Windows Server e Infrastruttura di classificazione file.

Questo esempio mostra come usare Azure RMS per proteggere automaticamente i file nei file server che eseguono Windows Server 2012 o versioni successive e sono configurati per l'uso di Infrastruttura di classificazione file.

Esistono diversi modi per applicare valori di classificazione ai file. Ad esempio, è possibile esaminare il contenuto dei file e applicare di conseguenza le classificazioni predefinite come Riservatezza e Informazioni personali. In questo esempio, però, un amministratore crea una classificazione personalizzata **Marketing** che viene applicata automaticamente a tutti i documenti utente vengono salvati nella cartella **Promozioni marketing** . Sebbene questa cartella sia protetta con autorizzazioni NTFS che limitano l'accesso ai membri del gruppo Marketing, l'amministratore è consapevole del fatto che queste autorizzazioni possono andare perdute se un membro del gruppo sposta i file o li invia tramite posta elettronica. In quel caso, è possibile che utenti non autorizzati accedano alle informazioni contenute nei file.

![COSA VEDONO GLI AMMINISTRATORI DURANTE IL PASSAGGIO 1](../media/AzRMS_FCI_ConnectorSmall.png)

**COSA VEDONO GLI AMMINISTRATORI DURANTE IL PASSAGGIO 1:** gli amministratori installano e configurano il connettore Rights Management (RMS), che agisce da punto di inoltro tra i server locali e Azure RMS.

---

![COSA VEDONO GLI AMMINISTRATORI DURANTE IL PASSAGGIO 2](../media/AzRMS_ExampleFCI_ConfigurationSmall.png)

**CSOSA VEDONO GLI AMMINISTRATORI DURANTE IL PASSAGGIO 2:** sul file server l'amministratore configura le attività e le regole di classificazione in modo che tutti i file utente nella cartella **Promozioni marketing** vengano classificati automaticamente come **Marketing** e protetti con la crittografia di RMS.

Seleziona il modello RMS personalizzato creato nel primo esempio, che limita l'accesso ai membri dei reparti Vendite e Marketing: **Vendite e marketing - Solo stampa e lettura**

Di conseguenza, tutti i documenti in quella cartella vengono automaticamente configurati con la classificazione Marketing e protetti mediante il modello Vendite e Marketing di RMS.

---

![COSA VEDONO GLI AMMINISTRATORI DURANTE IL PASSAGGIO 3](../media/AzRMS_FCI_EmailSmall.png)

**COSA VEDONO GLI UTENTI DURANTE IL PASSAGGIO 3:** ecco come RMS contribuisce a evitare la divulgazione dei dati a persone non autorizzate ad accedere alle informazioni sensibili o riservate:

- Janet, del reparto Marketing, invia un report riservati dalla cartella Promozioni marketing. Questo report contiene le nuove funzionalità e i piani di pubblicità del prodotto ed è richiesto da un collega che attualmente si trova in viaggio per lavoro. Tuttavia, Janet lo invia tramite posta elettronica al destinatario sbagliato, selezionando per errore un destinatario con un nome simile, ma di un'altra società.<br><br>
Il destinatario non può leggere il report riservato perché non fa parte del gruppo Vendite e marketing.

---

**Per ulteriori informazioni relative a questo scenario:**

- Per istruzioni dettagliate, vedere [Distribuzione del connettore di Azure Rights Management](../deploy-use/deploy-rms-connector.md).

## Protezione automatica della posta elettronica con Exchange Online e criteri di prevenzione della perdita di dati

L'esempio precedente ha mostrato come proteggere automaticamente i file che contengono informazioni sensibili o riservate, ma cosa accade se le informazioni non si trovano in un file, ma in un messaggio di posta elettronica? Qui emerge evidente l'utilità dei criteri di prevenzione della perdita dei dati di Exchange Online, che richiedono all'utente di applicare la protezione delle informazioni (usando i suggerimenti relativi ai criteri) oppure applicandola automaticamente (mediante le regole di trasporto).

In questo esempio l'amministratore configura un criterio per assicurare la conformità dell'azienda alle norme statunitensi per la protezione delle informazioni personali, ma è anche possibile configurare regole per il rispetto di altre normative oppure regole personalizzate.

![COSA VEDONO GLI AMMINISTRATORI DURANTE IL PASSAGGIO 1](../media/AzRMS_DLPExample1.png)

**COSA VEDONO GLI AMMINISTRATORI DURANTE IL PASSAGGIO 1:** nell'interfaccia di amministrazione di Exchange il modello di Exchange denominato **Informazioni personali Stati Uniti** può essere usato dall'amministratore per creare e configurare nuovi criteri DLP. Questo modello cerca informazioni quali numeri di previdenza sociale e patenti di guida nei messaggi di posta elettronica.

Le regole sono configurate in modo che ai messaggi di posta elettronica che contengono queste informazioni e che vengono inviati automaticamente all'esterno dell'organizzazione venga applicata la protezione dei diritti usando un modello di RMS che limita l'accesso ai soli dipendenti della società.

In questo caso, la regola è configurata per l'uso di uno dei modelli predefiniti, **VanArsdel, Ltd - Riservata**, illustrato nel primo esempio. Nella scelta dei modelli, tuttavia, sono inclusi anche i modelli personalizzati creati, oltre a un'opzione **Non inoltrare** specifica di Exchange.

> [!NOTE]
> Se le opzioni di configurazione visualizzate sono leggermente diverse dall'immagine, potrebbe essere necessario selezionare prima **Altre opzioni** quando si configura la regola. È quindi possibile selezionare **Modify the message security (Modifica sicurezza messaggi)** > **Applica protezione diritti** e quindi selezionare il modello RMS.

---

![COSA VEDONO GLI AMMINISTRATORI DURANTE IL PASSAGGIO 2](../media/AzRMS_DLPUnprotectedEmail_small.png)

**COSA VEDONO GLI UTENTI DURANTE IL PASSAGGIO 2:** il responsabile delle assunzioni scrive un messaggio di posta elettronica che contiene il numero di previdenza sociale di un nuovo dipendente. Invia il messaggio di posta elettronica a Sherrie del reparto Risorse umane.

---

![COSA VEDONO GLI AMMINISTRATORI DURANTE IL PASSAGGIO 3](../media/AzRMS_DLPProtectedEmail_small.png)

**COSA VEDONO GLI UTENTI DURANTE IL PASSAGGIO 3:** se questo messaggio di posta elettronica viene inviato o inoltrato a qualcuno all'esterno dell'organizzazione, la regola DLP applica automaticamente la protezione dei diritti.

Il messaggio di posta elettronica viene crittografato quando lascia l'infrastruttura dell'organizzazione, in modo che il numero di previdenza sociale incluso nel non possa essere letto quando il messaggio è in transito o si trova nella posta in arrivo del destinatario. Il destinatario non potrà leggere il messaggio a meno che non sia un dipendente VanArsdel.

---

**Per ulteriori informazioni relative a questo scenario:**

-   Per ulteriori informazioni sull'uso di Azure RMS con Exchange Online, vedere la sezione [Exchange Online ed Exchange Server](office-apps-services-support.md#exchange-online-and-exchange-server) di [Supporto di Microsoft Azure Rights Management da parte delle applicazioni](applications-support.md).

-   Per istruzioni dettagliate su come configurare Exchange Online per Azure RMS, vedere la sezione [Exchange Online: configurazione di IRM](../deploy-use/configure-office365.md#exchange-online-irm-configuration) di [Configurazione di applicazioni per Rights Management di Windows Azure](../deploy-use/configure-applications.md).

## Protezione automatica dei file con SharePoint Online e librerie protette

Questa sezione mostra come proteggere facilmente i documenti mediante SharePoint Online e librerie protette.

In questo esempio l'amministratore di SharePoint per Contoso ha creato una libreria per ogni reparto che viene usata per archiviare centralmente ed estrarre i documenti per il controllo delle versioni e la modifica. Ad esempio, è presente una libreria per il reparto Vendite, una per Marketing, una per Risorse umane e così via. Quando viene caricato o creato un nuovo documento in una di queste librerie protette, il documento eredita la protezione della libreria (non occorre selezionare un modello di criteri di diritti), viene protetto automaticamente e rimane protetto anche in caso di spostamento all'esterno della libreria di SharePoint.

![COSA VEDONO GLI AMMINISTRATORI DURANTE IL PASSAGGIO 1](../media/AzRMS_StoryboardSPO_small1.png)

**COSA VEDONO GLI AMMINISTRATORI DURANTE IL PASSAGGIO 1:** l'amministratore abilita Information Rights Management per il sito di SharePoint.

---

![COSA VEDONO GLI AMMINISTRATORI DURANTE IL PASSAGGIO 2](../media/AzRMS_StoryboardSPO_small2.png)

**COSA VEDONO GLI AMMINISTRATORI DURANTE IL PASSAGGIO 2:** abilita quindi Rights Management per una libreria. Anche se sono disponibili opzioni aggiuntive, questa semplice impostazione spesso è sufficiente.

Quando i documenti vengono scaricati da questa raccolta, sono automaticamente protetti da Rights Management, ereditando la protezione configurata per la raccolta.

---

![COSA VEDONO GLI AMMINISTRATORI DURANTE IL PASSAGGIO 3](../media/AzRMS_StoryboardSPO_small3.png)

**COSA VEDONO GLI UTENTI DURANTE IL PASSAGGIO 3:** quando un utente del reparto vendite estrae il report delle vendite dalla libreria, l'intestazione nella parte superiore indica chiaramente che si tratta di un documento protetto con accesso limitato.

Il documento rimane protetto anche se viene rinominato, salvato in un altro percorso o condiviso tramite posta elettronica. Può essere letto solo dai membri del reparto vendite, indipendentemente dal nome che viene assegnato al file, dal percorso in cui viene archiviato o dalla sua condivisione tramite posta elettronica.

---

**Per ulteriori informazioni relative a questo scenario:**

-   Per ulteriori informazioni sull'uso di Azure RMS con SharePoint, vedere la sezione [SharePoint Online e SharePoint Server](office-apps-services-support.md#sharepoint-online-and-sharepoint-server) di [Supporto di Microsoft Azure Rights Management da parte delle applicazioni](applications-support.md).

-   Per istruzioni dettagliate su come configurare SharePoint per Azure RMS, vedere la sezione [SharePoint Online e OneDrive for Business: configurazione di IRM](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration) di [Configurazione di applicazioni per Rights Management di Windows Azure](../deploy-use/configure-applications.md).

## Condivisione sicura di allegati con utenti mobili

Negli esempi precedenti è stato illustrato come gli amministratori possono applicare automaticamente la protezione delle informazioni ai dati sensibili e riservati. In alcuni casi, però, gli utenti possono avere l'esigenza di applicare autonomamente questa protezione, ad esempio se collaborano con partner di un'altra organizzazione, hanno bisogno di autorizzazioni personalizzate o impostazioni non definite nei modelli, in situazioni specifiche che non rientrano negli esempi precedenti. In questi casi, gli utenti possono applicare autonomamente i modelli di RMS oppure configurare autorizzazioni personalizzate.

Questo esempio illustra come gli utenti possono condividere facilmente un documento con un collaboratore in un'altra società, proteggendo comunque il documento e con la certezza che il destinatario possa leggerlo, anche da un dispositivo mobile. Questo scenario usa l'applicazione di condivisione Rights Management, che è possibile distribuire automaticamente nei computer Windows dell'organizzazione. In alternativa, può essere installata manualmente dagli utenti.

In questo esempio, Alice di Contoso invia un documento di Word riservato tramite posta elettronica a Roberto di Fabrikam. Legge il documento sul suo iPad, ma potrebbe leggerlo altrettanto facilmente anche su un iPhone, su un tablet o telefono Android, su un computer Mac o su un telefono o computer Windows.

![COSA VEDONO GLI UTENTI DURANTE IL PASSAGGIO 1](../media/AzRMS_StoryboardEmail_small1.png)

**COSA VEDONO GLI UTENTI DURANTE IL PASSAGGIO 1:** Alice crea un messaggio di posta elettronica standard dal suo PC Windows e allega un documento.

Fa clic su **Condividi file protetto** sulla barra multifunzione. Viene visualizzata la finestra di dialogo **condividi file protetto** dall'applicazione RMS sharing.

Alice vuole che Roberto possa solo visualizzare e modificare il documento, ma non copiarlo o stamparlo, quindi seleziona **REVISORE - Visualizzazione e Modifica**. Vuole anche essere informata tramite posta elettronica quando qualcuno prova ad aprire il documento e vuole poter revocare il documento successivamente, se necessario, con la certezza che la revoca avrà effetto immediato.

---

![COSA VEDONO GLI UTENTI DURANTE IL PASSAGGIO 2](../media/AzRMS_StoryboardEmail_small2.png)

**COSA VEDONO GLI UTENTI DURANTE IL PASSAGGIO 2:** Roberto vede il messaggio di posta elettronica sul suo iPad.

Oltre al messaggio e all'allegato di Alice, ci sono istruzioni che segue per iscriversi e installare l'app RMS sharing sul suo iPad.

---

![COSA VEDONO GLI UTENTI DURANTE IL PASSAGGIO 3](../media/AzRMS_StoryboardEmail_small3.png)

**COSA VEDONO GLI UTENTI DURANTE IL PASSAGGIO 3:** Roberto può ora aprire l'allegato. Prima di tutto gli viene chiesto di accedere per confermare di essere il destinatario previsto.

Quando Roberto visualizza il documento, vede anche le informazioni relative all'accesso limitato, che indicano che può visualizzare e modificare il documento, ma non copiarlo o stamparlo.

---

![COSA VEDONO GLI UTENTI DURANTE IL PASSAGGIO 4](../media/AzRMS_StoryboardEmail_small4.png)

**COSA VEDONO GLI UTENTI DURANTE IL PASSAGGIO 4:** Alice riceve un messaggio di posta elettronica che indica che Roberto ha aperto il documento che lei gli ha inviato, con data e ora di accesso al documento.

Se Roberto inoltra il messaggio di posta elettronica con l'allegato o lo salva in un percorso cui altri utenti possono accedere o se questo viene intercettato sulla rete, il documento non potrà essere letto da altre persone.

---

**Per ulteriori informazioni relative a questo scenario:**

- Per istruzioni dettagliate, vedere [Proteggere un file che si condivide tramite posta elettronica](../rms-client/sharing-app-protect-by-email.md) e [Visualizzare e usare i file che sono stati protetti](../rms-client/sharing-app-view-use-files.md) nella [Guida dell'utente dell'applicazione di condivisione Rights Management](../rms-client/sharing-app-user-guide.md).

- L'[Esercitazione di avvio rapido per Azure Rights Management](../get-started/quick-start-tutorial.md) include istruzioni dettagliate per questo scenario.

## Passaggi successivi

Dopo avere visto alcuni esempi di ciò che Azure RMS è in grado di fare, è interessante capire come opera. Per informazioni tecniche sul funzionamento di Azure RMS, vedere [Funzionamento di Azure RMS](how-does-it-work.md).


<!--HONumber=Jun16_HO2-->


