---
title: Configurare un'etichetta di Azure Information Protection per la protezione - AIP
description: Quando si configura un'etichetta per usare la protezione di Rights Management, è possibile proteggere i documenti e messaggi di posta elettronica più sensibili.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/16/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 17c60e535e41f5678ca94d3744b487c566a3247d
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97383109"
---
# <a name="how-to-configure-a-label-for-rights-management-protection"></a>Come configurare un'etichetta per la protezione di Rights Management

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***Pertinente per**: [Azure Information Protection client classico per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client di etichettatura unificata, vedere [informazioni sulle etichette di riservatezza](/microsoft-365/compliance/sensitivity-labels) e [limitare l'accesso al contenuto usando la crittografia in etichette di riservatezza](/microsoft-365/compliance/encryption-sensitivity-labels) dalla documentazione di Microsoft 365. *

> [!NOTE] 
> Per offrire un'esperienza utente unificata e semplificata, **Azure Information Protection** la gestione classica di client e **etichette** nel portale di Azure verrà **deprecata** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).
>

Per proteggere documenti e messaggi di posta elettronica più sensibili, è possibile usare un servizio Rights Management. Questo servizio usa la crittografia, l'identità e i criteri di autorizzazione per prevenire la perdita di dati. Per applicare la protezione, si usa un'etichetta configurata per l'uso della protezione Rights Management per documenti e messaggi di posta elettronica. Gli utenti possono anche selezionare il pulsante **Non inoltrare** in Outlook.

Quando si configura un'etichetta con l'impostazione di protezione **Azure (chiave cloud)** viene creato e configurato un modello di protezione al quale possono accedere i servizi e le applicazioni che si integrano con i modelli di Rights Management. Alcuni esempi sono Exchange Online, regole del flusso di posta e Outlook sul Web. 

## <a name="how-the-protection-works"></a>Come funziona la protezione

Quando un documento o un messaggio di posta elettronica è protetto da un servizio Rights Management, viene crittografato quando i dati sono inattivi e in transito. Può quindi essere decrittografato solo da utenti autorizzati. Questa crittografia rimane associata al documento o al messaggio di posta elettronica, anche se questo viene rinominato. È anche possibile configurare diritti e restrizioni di utilizzo, come negli esempi seguenti:

- Solo gli utenti all'interno dell'organizzazione possono aprire il documento o il messaggio di posta elettronica riservato dell'azienda.

- Solo gli utenti del reparto marketing possono modificare e stampare il documento o il messaggio di posta elettronica relativo all'annuncio di promozione, mentre tutti gli altri utenti dell'organizzazione possono solo visualizzarlo.

- Gli utenti non possono inoltrare messaggi di posta elettronica o copiare informazioni da messaggi che contengono informazioni su una riorganizzazione interna.

- Il listino prezzi aggiornato inviato ai partner commerciali non può essere aperto dopo una data specificata.

Per altre informazioni sulla protezione di Azure Rights Management e sul relativo funzionamento, vedere [Informazioni su Microsoft Azure Rights Management](what-is-azure-rms.md).

> [!IMPORTANT]
> Per configurare un'etichetta in modo da applicare questa protezione, è necessario che il servizio Azure Rights Management sia stato attivato per l'organizzazione. Per altre informazioni, vedere [Attivazione del servizio di protezione da Azure Information Protection](activate-service.md).

Quando l'etichetta applica la protezione, un documento protetto non può essere salvato in OneDrive o SharePoint. Questi percorsi non supportano le funzionalità seguenti per i file protetti: creazione condivisa, Office per il Web, ricerca, anteprima dei documenti, anteprima, eDiscovery e prevenzione della perdita dei dati (DLP).

> [!TIP]
> Quando si [esegue la migrazione delle etichette](configure-policy-migrate-labels.md) a etichette di riservatezza unificate e le si pubblica da uno dei centri di amministrazione dell'etichettatura, ad esempio il centro conformità di Microsoft 365, le etichette che applicano la protezione sono quindi supportate per queste posizioni. Per altre informazioni, vedere  [abilitare le etichette di riservatezza per i file di Office in SharePoint e OneDrive](/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files).

Non è necessario configurare Exchange per Azure Information Protection per permettere agli utenti di applicare etichette in Outlook e proteggere i loro messaggi di posta elettronica. Tuttavia, fino a quando Exchange non viene configurato per Azure Information Protection, non si può usufruire delle funzionalità di protezione complete di Azure Rights Management con Exchange. Gli utenti non potranno, ad esempio, visualizzare messaggi di posta elettronica protetti nei telefoni cellulari o con Outlook sul Web, i messaggi di posta elettronica protetti non potranno essere indicizzati per la ricerca e non sarà possibile configurare la prevenzione della perdita dei dati di Exchange Online per la protezione di Rights Management. Per assicurarsi che Exchange possa supportare questi scenari aggiuntivi, vedere le risorse seguenti:

- Per Exchange Online, vedere le istruzioni in [Exchange Online: configurazione di IRM](configure-office365.md#exchangeonline-irm-configuration).

- Per la versione locale di Exchange, è necessario distribuire il [connettore RMS e configurare i server Exchange](deploy-rms-connector.md). 

## <a name="to-configure-a-label-for-protection-settings"></a>Per configurare un'etichetta per le impostazioni di protezione

1. Aprire una nuova finestra del browser e accedere al [portale di Azure](configure-policy.md#signing-in-to-the-azure-portal), se questa operazione non è già stata eseguita. Quindi passare al riquadro **Azure Information Protection**. 
    
    Ad esempio, nella casella di ricerca di risorse, servizi e documentazione: iniziare a digitare **Informazioni** e selezionare **Azure Information Protection**.

2. Dall'opzione di menu **classificazioni**  >  **etichette** : nel riquadro **Azure Information Protection etichette** selezionare l'etichetta che si vuole modificare. 

3. Nel riquadro **Etichetta** individuare la sezione **Configurare le autorizzazioni per documenti e messaggi di posta elettronica contenenti questa etichetta** e selezionare una delle opzioni seguenti:
    
    - **Non configurata**: selezionare questa opzione se l'etichetta è attualmente configurata in modo da applicare la protezione e non si vuole più che l'etichetta selezionata applichi la protezione. Procedere quindi con il passaggio 11.
        
        Le impostazioni di protezione configurate in precedenza vengono mantenute come un modello di protezione archiviato e verranno visualizzate di nuovo se si reimposta l'opzione su **Proteggi**. Questo modello non è visualizzato nel portale di Azure, ma è comunque possibile gestirlo con [PowerShell](configure-templates-with-powershell.md) se necessario. Questo comportamento indica che il contenuto rimane accessibile se ha questa etichetta con le impostazioni di protezione applicate in precedenza.
        
        Quando viene applicata un'etichetta con questa impostazione di protezione **Non configurata**:
        
         - Se il contenuto era stato protetto in precedenza senza l'uso di un'etichetta, tale protezione viene mantenuta. 
         
         - Se in precedenza il contenuto era stato protetto con un'etichetta, la protezione viene rimossa se l'utente che applica l'etichetta ha le autorizzazioni per rimuovere la protezione di Rights Management. Questo requisito significa che l'utente deve avere **Esporta** o **Controllo completo come** [diritto di utilizzo](configure-usage-rights.md). oppure essere il proprietario di Rights Management (che implica automaticamente il diritto di utilizzo Controllo completo) o un [utente con privilegi avanzati per Azure Rights Management](configure-super-users.md).
             
             Se l'utente non dispone delle autorizzazioni per rimuovere la protezione, l'etichetta non può essere applicata e viene visualizzato il messaggio seguente: **Azure Information Protection non può applicare questa etichetta. Se il problema persiste, contattare l'amministratore**. 
    
    - **Proteggi**: selezionare questa opzione per applicare la protezione e quindi procedere con il passaggio 4.
    
    - **Rimuovi la protezione**: selezionare questa opzione per rimuovere la protezione se un documento o un messaggio di posta elettronica è protetto. Procedere quindi con il passaggio 11.
        
        Se la protezione è stata applicata con un'etichetta o un modello di protezione, le impostazioni di protezione configurate in precedenza vengono mantenute come un modello di protezione archiviato e verranno visualizzate di nuovo se si reimposta l'opzione su **Proteggi**. Questo modello non è visualizzato nel portale di Azure, ma è comunque possibile gestirlo con [PowerShell](configure-templates-with-powershell.md) se necessario. Questo comportamento indica che il contenuto rimane accessibile se ha questa etichetta con le impostazioni di protezione applicate in precedenza.
        
        Si noti che, per applicare correttamente un'etichetta con questa opzione, l'utente deve avere le autorizzazioni per rimuovere la protezione di Rights Management. Questo requisito significa che l'utente deve avere **Esporta** o **Controllo completo come** [diritto di utilizzo](configure-usage-rights.md). oppure essere il proprietario di Rights Management (che implica automaticamente il diritto di utilizzo Controllo completo) o un [utente con privilegi avanzati per Azure Rights Management](configure-super-users.md). 
        
        Se l'utente che applica l'etichetta con questa impostazione non dispone delle autorizzazioni per rimuovere la protezione Rights Management, l'etichetta non può essere applicata e viene visualizzato il messaggio seguente: **Azure Information Protection non può applicare questa etichetta. Se il problema persiste, contattare l'amministratore.**

4. Se si è selezionato **Proteggi**, il riquadro **Protezione** si aprirà automaticamente se è stata selezionata una delle altre opzioni precedentemente selezionate. Se questo nuovo riquadro non si apre automaticamente, selezionare **Protezione**:
    
    ![Configurare la protezione per un'etichetta di Azure Information Protection](./media/info-protect-protection-bar-configured.png)

5. Nel riquadro **Protezione** selezionare **Azure (chiave cloud)** oppure **HYOK (AD RMS)**.
    
    Nella maggior parte dei casi selezionare **Azure (chiave cloud)** per le impostazioni delle autorizzazioni. Non selezionare **HYOK (AD RMS)** a meno che non siano stati letti e compresi i prerequisiti e le restrizioni relativi a questa configurazione *HYOK* (Hold Your Own Key). Per altre informazioni, vedere [Requisiti e restrizioni HYOK per la protezione di AD RMS](configure-adrms-restrictions.md). Per continuare la configurazione per HYOK (AD RMS), procedere con il passaggio 9.
    
6. Selezionare una delle opzioni seguenti:
    
   - **Configura le autorizzazioni**: consente di definire nuove impostazioni di protezione nel portale.
    
   - **Configura le autorizzazioni definite dall'utente (anteprima)**: consente agli utenti di specificare a chi vengono concesse autorizzazioni e quali sono queste autorizzazioni. È quindi possibile completare l'impostazione dell'opzione e scegliere solo Outlook oppure Word, Excel, PowerPoint ed Esplora file. Questa opzione non è supportata e non funziona quando un'etichetta è configurata per la [classificazione automatica](configure-policy-classification.md).
        
       Se si sceglie l'opzione per Outlook, l'etichetta viene visualizzata in Outlook e il comportamento risultante quando gli utenti applicano l'etichetta è uguale a quello dell'opzione non [inoltrare](configure-usage-rights.md#do-not-forward-option-for-emails) .
        
       Se si sceglie l'opzione per Word, Excel, PowerPoint ed Esplora file, quando l'opzione è impostata, l'etichetta viene visualizzata in queste applicazioni. Quando gli utenti applicano l'etichetta, viene quindi visualizzata la finestra di dialogo che consente loro di selezionare le autorizzazioni personalizzate. In questa finestra di dialogo gli utenti possono scegliere uno dei [livelli di autorizzazione predefiniti](configure-usage-rights.md#rights-included-in-permissions-levels), passare a o specificare utenti o gruppi e, facoltativamente, impostare una data di scadenza. Assicurarsi che gli utenti abbiano a disposizione le istruzioni e le linee guida per specificare questi valori.

        > [!NOTE]
        > Il supporto Azure Information Protection per l'impostazione di autorizzazioni definite dall'utente è attualmente in anteprima. Le [condizioni aggiuntive per l'anteprima di Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) includono termini legali aggiuntivi che si applicano a funzionalità di Azure in versione beta, anteprima o diversamente non ancora disponibili a livello generale. 
        >
     
   - **Seleziona un modello predefinito**: consente di usare uno dei modelli predefiniti o un modello personalizzato che è stato configurato. Si noti che questa opzione non viene visualizzata per le nuove etichette o se si sta modificando un'etichetta che in precedenza usava l'opzione **Configura le autorizzazioni**.
    
     Per selezionare un modello predefinito, il modello deve essere pubblicato (non archiviato) e non deve essere già collegato a un'altra etichetta. Quando si seleziona questa opzione è possibile usare il pulsante **Modifica modello** per [convertire il modello in un'etichetta](configure-policy-templates.md#to-convert-templates-to-labels).
    
     se si creano e modificano regolarmente modelli personalizzati, può risultare utile consultare [Attività che precedentemente venivano eseguite con il portale di Azure classico](migrate-portal.md).

7. Se si è selezionato **Impostazione autorizzazioni** per **Azure (chiave cloud)**, questa opzione consente di selezionare utenti e diritti di utilizzo. 
    
    Se non si seleziona alcun utente e si seleziona **OK** in questo riquadro, seguito da **Salva** nel riquadro **etichetta** : l'etichetta è configurata per applicare la protezione in modo che solo la persona che applica l'etichetta possa aprire il documento o il messaggio di posta elettronica senza restrizioni. Questa configurazione è anche nota come "Solo per me" e potrebbe essere questo il risultato richiesto, in modo che un utente possa salvare un file in qualsiasi posizione ed essere certo che nessun altro possa aprirlo. Se questo risultato corrisponde al requisito e non è necessario che altri utenti collaborino al contenuto protetto, non selezionare **Aggiungi autorizzazioni**. Dopo aver salvato l'etichetta, all'apertura successiva di questo riquadro **Protezione** viene visualizzato **IPC_USER_ID_OWNER** per **Utenti** e **Comproprietario** per **Autorizzazioni** in base a questa configurazione.
    
    Per specificare gli utenti che possono aprire i documenti e i messaggi di posta elettronica protetti, selezionare **Aggiungi autorizzazioni**. Nel riquadro **Aggiungi autorizzazioni** selezionare quindi il primo set di utenti e gruppi che avranno il diritto di usare il contenuto che verrà protetto dall'etichetta selezionata:
    
   - Scegliere **Seleziona dall'elenco** in cui è possibile aggiungere tutti gli utenti dell'organizzazione selezionando **Aggiungi \<organization name> -tutti i membri**. Questa impostazione consente di escludere gli account guest. In alternativa è possibile selezionare **Aggiungi eventuali utenti autenticati** o esplorare la directory.
        
       Quando si scelgono tutti i membri o si passa alla directory, gli utenti o i gruppi devono avere un indirizzo di posta elettronica. Questa condizione si verifica quasi sempre in un ambiente di produzione, ma in un ambiente di test semplice può essere necessario aggiungere gli indirizzi di posta elettronica agli account utente o ai gruppi.
        
       ###### <a name="more-information-about-add-any-authenticated-users"></a>Altre informazioni su **Add any authenticated users** (Aggiungi qualsiasi utente autenticato) 
       Questa impostazione non limita chi può accedere al contenuto protetto dall'etichetta, pur crittografando il contenuto e fornendo le opzioni per limitare come usare il contenuto (autorizzazioni) e come accedervi (scadenza e accesso offline). L'applicazione che apre il contenuto protetto deve tuttavia poter supportare l'autenticazione in uso. Per questo motivo, i provider di servizi di social networking federati, ad esempio Google, e l'autenticazione di passcode monouso devono essere usati solo per la posta elettronica e solo quando si usano Exchange Online e le nuove funzionalità di Office 365 Message Encryption. Gli account Microsoft possono essere usati con il visualizzatore Azure Information Protection e le app di Office 365 (A portata di clic). 
          
       Alcuni scenari tipici per l'impostazione Aggiungi eventuali utenti autenticati:
       - Non è importante chi visualizza il contenuto, ma si vuole limitare il modo in cui viene usato. Ad esempio, non si vuole che il contenuto venga modificato, copiato o stampato.
       - Non è necessario limitare chi accede al contenuto, ma si vuole tenere traccia di chi lo apre e, potenzialmente, revocare l'accesso.
       - Esiste un requisito in base al quale il contenuto deve essere crittografato quando è inattivo e quando è in transito, ma non sono necessari controlli di accesso.
        
   - Scegliere **Immettere i dettagli** per specificare manualmente gli indirizzi di posta elettronica dei singoli utenti o gruppi (interni o esterni). o per specificare tutti gli utenti in un'altra organizzazione immettendo un nome di dominio di tale organizzazione. È anche possibile usare questa opzione per i provider di social networking, immettendo i nomi di dominio, ad esempio **gmail.com**, **hotmail.com** oppure **outlook.com**.
        
     >[!NOTE]
     >Se un indirizzo di posta elettronica viene modificato dopo che si è selezionato l'utente o il gruppo, vedere la sezione [Considerazioni su Azure Information Protection in caso di modifica di indirizzi di posta elettronica](prepare.md#considerations-for-azure-information-protection-if-email-addresses-change) nella documentazione relativa alla pianificazione.
    
     Come procedura consigliata, usare gruppi anziché utenti. Con questa strategia la configurazione risulta più semplice ed è meno probabile che sia necessario aggiornare la configurazione dell'etichetta in un secondo momento e quindi proteggere di nuovo il contenuto. Se, però, se si apportano modifiche al gruppo, tenere presente che, per motivi di prestazioni, Azure Rights Management [memorizza nella cache l'appartenenza ai gruppi](prepare.md#group-membership-caching-by-azure-information-protection). 
    
    Dopo avere specificato il primo set di utenti e gruppi, selezionare le autorizzazioni da concedere a tali utenti e gruppi. Per altre informazioni sulle autorizzazioni selezionabili, vedere [Configurazione dei diritti di utilizzo per Azure Information Protection](configure-usage-rights.md). Le applicazioni che supportano Rights Management possono però implementare queste autorizzazioni in modo diverso. Consultare la relativa documentazione ed eseguire test personalizzati con le applicazioni usate dagli utenti per controllare il comportamento prima di distribuire il modello per gli utenti.
    
     Se necessario, è ora possibile aggiungere un secondo set di utenti e gruppi con diritti di utilizzo. Ripetere fino a quando non sono stati specificati tutti gli utenti e i gruppi con le rispettive autorizzazioni.

     >[!TIP]
     >Valutare l'opportunità di aggiungere l'autorizzazione personalizzata **Salva con nome, Esporta (EXPORT)** e concederla al personale o agli amministratori selezionati in altri ruoli responsabili del recupero delle informazioni. Tali utenti possono rimuovere, se necessario, la protezione da file e messaggi di posta elettronica che verranno protetti mediante questo modello o etichetta. La possibilità di rimuovere la protezione a livello di autorizzazione per un documento o un messaggio di posta elettronica consente un controllo più granulare rispetto all'uso della funzionalità dell'[utente con privilegi avanzati](configure-super-users.md).
    
     Per tutti gli utenti e i gruppi specificati, nel riquadro **Protezione** controllare se si vogliono apportare modifiche alle impostazioni seguenti. Si noti che queste impostazioni, come le autorizzazioni, non si applicano all'[autorità emittente di Rights Management o al proprietario di Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner), nonché a qualsiasi [utente con privilegi avanzati](configure-super-users.md) che è stato assegnato.
    
     ###### <a name="information-about-the-protection-settings"></a>Informazioni sulle impostazioni di protezione
    
     |Impostazione|Ulteriori informazioni|Impostazione consigliata
     |-----------|--------------------|--------------------|
     |**Scadenza del contenuto dei file**|Definire una data o un numero di giorni in cui i documenti protetti tramite queste impostazioni non dovranno essere aperti dagli utenti selezionati. Per i messaggi di posta elettronica, la scadenza non è sempre applicata a causa dei meccanismi di memorizzazione nella cache che alcuni client di posta elettronica usano.<br /><br />È possibile specificare una data o un numero di giorni a partire dal momento in cui la protezione viene applicata ai contenuti.<br /><br />Quando si specifica una data, questa diventa effettiva alla mezzanotte del fuso orario corrente.|**Nessuna scadenza contenuto**, a meno che non esista un requisito temporale specifico per il contenuto.|
     |**Consenti l'accesso offline**|Usare questa impostazione per bilanciare i requisiti di sicurezza, compreso l'accesso dopo la revoca, con la possibilità per gli utenti selezionati di aprire il contenuto protetto quando non hanno una connessione Internet.<br /><br />Se si specifica che il contenuto non è disponibile senza una connessione Internet o che è disponibile solo per un determinato numero di giorni, al raggiungimento di tale soglia, gli utenti dovranno eseguire di nuovo l'autenticazione e l'accesso verrà registrato. In questo caso, se le credenziali non sono memorizzate nella cache, verrà chiesto agli utenti di eseguire l'accesso prima di poter aprire il documento o il messaggio di posta elettronica.<br /><br />Oltre alla ripetizione dell'autenticazione, verranno nuovamente valutati i criteri e l'appartenenza ai gruppi. Questo significa che gli utenti potrebbero avere risultati di accesso diversi per lo stesso documento o messaggio di posta elettronica se dall'ultimo accesso ai contenuti si sono verificati cambiamenti relativi ai criteri o all'appartenenza ai gruppi. Ciò potrebbe includere anche l'impossibilità di accedere al documento se questo è stato [revocato](./rms-client/client-track-revoke.md).|A seconda del livello di sensibilità del contenuto:<br /><br />- **Numero di giorni per cui il contenuto è disponibile senza una connessione Internet**  =  **7** per i dati aziendali sensibili che potrebbero causare danni all'azienda se condivisi con persone non autorizzate. Questa raccomandazione offre un equo compromesso tra sicurezza e flessibilità. Sono esempi di questo tipo di contenuto i contratti, i report sulla sicurezza, i riepiloghi previsionali e i dati sulle vendite.<br /><br />- **Mai** per dati aziendali particolarmente riservati che potrebbero causare danni all'azienda se condivisi con utenti non autorizzati. Con questa raccomandazione viene data maggiore priorità alla sicurezza rispetto alla flessibilità e viene garantito che, in caso di revoca, tutti gli utenti autorizzati non potranno aprire il documento. Sono esempi di questo tipo di contenuto le informazioni su dipendenti e clienti, le password, il codice sorgente e i rendiconti finanziari preannunciati.|
    
     Al termine della configurazione delle autorizzazioni e delle impostazioni, fare clic su **OK**. 
    
     Questo raggruppamento di impostazioni consente di creare un modello personalizzato per il servizio Azure Rights Management. Questi modelli possono essere usati con applicazioni e servizi che si integrano con Azure Rights Management. Per informazioni sul download e sull'aggiornamento di questi modelli in computer e servizi, vedere [Aggiornamento di modelli per utenti e servizi](refresh-templates.md).

8. Se è stata selezionata l'opzione **Seleziona un modello predefinito** per **Azure (chiave cloud)**, fare clic sulla casella di riepilogo a discesa e selezionare il [modello](configure-policy-templates.md) da usare per proteggere i documenti e i messaggi di posta elettronica con questa etichetta. Non sono visualizzati modelli archiviati o modelli già selezionati per un'altra etichetta.
    
    Se si seleziona un **modello di reparto** oppure se sono stati configurati [controlli di onboarding](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment):
    
    - Gli utenti che non rientrano nell'ambito del modello configurato o che sono esclusi dall'applicazione della protezione di Azure Rights Management visualizzeranno comunque l'etichetta ma non potranno applicarla. Se si seleziona l'etichetta, viene visualizzato il messaggio seguente: **Azure Information Protection non può applicare questa etichetta. Se il problema persiste, contattare l'amministratore.**
        
        Si noti che tutti i modelli pubblicati vengono sempre visualizzati, anche se si sta configurando un criterio con ambito. Si supponga ad esempio di configurare un criterio con ambito per il gruppo Marketing. I modelli che è possibile selezionare non sono solo quelli appartenenti all'ambito del gruppo Marketing ed è possibile selezionare un modello di reparto che non può essere usato dagli utenti selezionati. Per semplificare la configurazione e ridurre al minimo la risoluzione dei problemi, provare a rinominare il modello di reparto in modo che corrisponda all'etichetta nel criterio con ambito. 

9. Se è stata selezionata l'opzione **HYOK (AD RMS)**, selezionare **Imposta i dettagli del modello di AD RMS** o **Configura le autorizzazioni definite dall'utente (anteprima)**. Specificare quindi l'URL della licenza per il cluster AD RMS.
    
    Per istruzioni su come specificare un GUID di modello e l'URL della licenza, vedere [Individuazione delle informazioni per specificare la protezione di AD RMS con un'etichetta di Azure Information Protection](configure-adrms-restrictions.md#locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label).
    
    L'opzione per le autorizzazioni definite dall'utente consente agli utenti di specificare a chi vengono concesse autorizzazioni e quali sono queste autorizzazioni. È quindi possibile completare l'impostazione dell'opzione e scegliere solo Outlook (impostazione predefinita) oppure Word, Excel, PowerPoint ed Esplora file. Questa opzione non è supportata e non funziona quando un'etichetta è configurata per la [classificazione automatica](configure-policy-classification.md).
    
    Se si sceglie l'opzione per Outlook, l'etichetta viene visualizzata in Outlook e il comportamento risultante quando gli utenti applicano l'etichetta è uguale a quello dell'opzione non [inoltrare](configure-usage-rights.md#do-not-forward-option-for-emails) .
    
    Se si sceglie l'opzione per Word, Excel, PowerPoint ed Esplora file, quando l'opzione è impostata, l'etichetta viene visualizzata in queste applicazioni. Quando gli utenti applicano l'etichetta, viene quindi visualizzata la finestra di dialogo che consente loro di selezionare le autorizzazioni personalizzate. In questa finestra di dialogo gli utenti possono scegliere uno dei [livelli di autorizzazione predefiniti](configure-usage-rights.md#rights-included-in-permissions-levels), passare a o specificare utenti o gruppi e, facoltativamente, impostare una data di scadenza. Assicurarsi che gli utenti abbiano a disposizione le istruzioni e le linee guida per specificare questi valori.

10. Fare clic su **OK** per chiudere il riquadro **Protezione** e visualizzare la scelta **Definito dall'utente** o il modello selezionato per l'opzione **Protezione** nel riquadro **Etichetta**.

11. Nel riquadro **Etichetta** fare clic su **Salva**.

12. Nel riquadro **Azure Information Protection** usare la colonna **Protezione** per confermare che l'etichetta ora visualizza l'impostazione di protezione desiderata:
    
    - Un segno di spunta se è stata configurata la protezione. 
    
    - Un segno x per indicare l'annullamento se è stata configurata un'etichetta per la rimozione della protezione.
    
    - Un campo vuoto se la protezione non è impostata. 

Quando fa clic su **Salva**, le modifiche diventano automaticamente disponibili per utenti e servizi. Non è più presente un'opzione di pubblicazione separata.


## <a name="example-configurations"></a>Configurazioni di esempio

Le etichette secondarie **Tutti i dipendenti** e **Solo destinatari** delle etichette **Riservato** e **Riservatezza elevata** dei [criteri predefiniti](configure-policy-default.md) sono esempi di configurazione delle etichette per l'applicazione della protezione. È anche possibile usare gli esempi seguenti per la configurazione di scenari diversi. 

Per ogni esempio seguente, nel \<*label name*> riquadro selezionare **Proteggi**. Se il riquadro **Protezione** non si apre automaticamente, selezionare **Protezione** per aprire questo riquadro che consente di selezionare le opzioni di configurazione di protezione:

![Configurazione di un'etichetta di Azure Information Protection per la protezione](./media/info-protect-protection-bar-configured.png)

### <a name="example-1-label-that-applies-do-not-forward-to-send-a-protected-email-to-a-gmail-account"></a>Esempio 1: etichetta che applica Non inoltrare per l'invio di un messaggio di posta elettronica protetto a un account Gmail

Questa etichetta è disponibile solo in Outlook ed è appropriata quando Exchange Online è configurato per le [nuove funzionalità di Office 365 Message Encryption](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e). Indicare agli utenti di selezionare l'etichetta quando devono inviare un messaggio protetto a destinatari che usano un account Gmail (o qualsiasi altro account di posta elettronica esterno all'organizzazione). 

Gli utenti digitano l'indirizzo di posta elettronica Gmail nella casella **A**.  Selezionano quindi l'etichetta e l'opzione Non inoltrare viene aggiunta automaticamente al messaggio di posta elettronica. Il risultato è che i destinatari non possono inviare il messaggio di posta elettronica, stamparlo, copiarlo o salvarlo all'esterno della cassetta postale usando l'opzione **Salva con nome** . 

1. Nel riquadro **Protezione** verificare che l'opzione **Azure (chiave cloud)** sia selezionata.
    
2. Selezionare **Configura le autorizzazioni definite dall'utente (anteprima)** .

3. Assicurarsi che sia selezionata l'opzione seguente: **In Outlook applica Non inoltrare**.

4. Se selezionata, deselezionare l'opzione seguente: **In Word, Excel, PowerPoint e File Explorer richiedi all'utente le autorizzazioni personalizzate**.

5. Fare clic su **OK** nel riquadro **Protezione** e quindi su **Salva** nel riquadro **Etichetta**.


### <a name="example-2-label-that-restricts-read-only-permission-to-all-users-in-another-organization-and-that-supports-immediate-revocation"></a>Esempio 2: etichetta che limita l'autorizzazione di sola lettura a tutti gli utenti di un'altra organizzazione e supporta la revoca immediata

Questa etichetta è adatta per la condivisione (in sola lettura) di documenti molto sensibili che richiedono sempre una connessione Internet per la visualizzazione. Se viene revocata, gli utenti non potranno visualizzare il documento quando provano nuovamente ad aprirlo.

Questa etichetta non è adatta per i messaggi di posta elettronica.

1. Nel riquadro **Protezione** verificare che l'opzione **Azure (chiave cloud)** sia selezionata.
    
2. Assicurarsi che l'opzione **Configura le autorizzazioni** sia selezionata e quindi selezionare **Aggiungi autorizzazioni**.

3. Nel riquadro **Aggiungi autorizzazioni** selezionare **Immettere i dettagli**.

4. Immettere il nome di un dominio dell'altra organizzazione, ad esempio **fabrikam.com**. Quindi selezionare **Aggiungi**.

5. In **Scegliere le autorizzazioni dai valori preimpostati** selezionare **Visualizzatore** e quindi fare clic su **OK**.

6. Nel riquadro **Protezione** in **Consenti l'accesso offline** selezionare **Mai**.

7. Fare clic su **OK** nel riquadro **Protezione** e quindi su **Salva** nel riquadro **Etichetta**.


### <a name="example-3-add-external-users-to-an-existing-label-that-protects-content"></a>Esempio 3: Aggiungere utenti esterni a un'etichetta esistente che protegge il contenuto

I nuovi utenti aggiunti potranno aprire i documenti e i messaggi di posta elettronica già protetti con questa etichetta. Le autorizzazioni concesse a questi utenti possono essere diverse da quelle di cui dispongono gli utenti esistenti.

1. Nel riquadro **Protezione** verificare che sia selezionata l'opzione **Azure (chiave cloud)**.
    
2. Assicurarsi che l'opzione **Configura le autorizzazioni** sia selezionata e quindi selezionare **Aggiungi autorizzazioni**.

3. Nel riquadro **Aggiungi autorizzazioni** selezionare **Immettere i dettagli**.

4. Immettere l'indirizzo di posta elettronica del primo utente o gruppo da aggiungere e quindi selezionare **Aggiungi**.

5. Selezionare le autorizzazioni per l'utente o il gruppo.

6. Ripetere i passaggi 4 e 5 per ogni utente o gruppo che si vuole aggiungere a questa etichetta. Fare quindi clic su **OK**.

7. Fare clic su **OK** nel riquadro **Protezione** e quindi su **Salva** nel riquadro **Etichetta**.

### <a name="example-4-label-for-protected-email-that-supports-less-restrictive-permissions-than-do-not-forward"></a>Esempio 4: etichetta per la posta elettronica protetta che supporta autorizzazioni meno restrittive rispetto a Non inoltrare

Questa etichetta non può essere limitata a Outlook ma prevede controlli meno restrittivi rispetto all'uso di Non inoltrare. Ad esempio, se si vuole che i destinatari possano copiare dati dal messaggio di posta elettronica o da un allegato oppure che possano salvare e modificare un allegato.

Se si specificano gli utenti esterni che non hanno un account in Azure AD:

- L'etichetta è appropriata per i messaggi di posta elettronica quando Exchange Online usa le [nuove funzionalità di Office 365 Message Encryption](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e). 
 
- Per gli allegati di Office protetti automaticamente, questi documenti possono essere visualizzati in un browser. Per modificare questi documenti, scaricarli e modificarli con app di Office 365 (A portata di clic) e un account Microsoft che usa lo stesso indirizzo di posta elettronica. [Altre informazioni](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)


> [!NOTE]
> Exchange Online sta distribuendo una nuova opzione: [Encrypt-Only](configure-usage-rights.md#encrypt-only-option-for-emails) (Solo crittografia). Questa opzione non è disponibile per la configurazione delle etichette. È tuttavia possibile, quando si conoscono i destinatari, usare questo esempio per configurare un'etichetta con lo stesso set di diritti di utilizzo. 

Quando gli utenti specificano gli indirizzi di posta elettronica nella casella **A** gli indirizzi devono essere quelli degli utenti specificati per questa configurazione di etichetta. Dal momento che gli utenti possono appartenere a gruppi e avere più di un indirizzo di posta elettronica, l'indirizzo di posta elettronica che specificano non dovrà corrispondere esattamente a quello specificato per le autorizzazioni, anche se questo è il modo più semplice per garantire che il destinatario venga autorizzato. Per altre informazioni sull'applicazione delle autorizzazioni agli utenti, vedere [Preparazione di utenti e gruppi per Azure Information Protection](prepare.md). 

1. Nel riquadro **Protezione** verificare che l'opzione **Azure (chiave cloud)** sia selezionata.
    
2. Assicurarsi che l'opzione **Configura le autorizzazioni** sia selezionata e selezionare **Aggiungi autorizzazioni**.

3. Nel riquadro **Aggiungi autorizzazioni** : per concedere le autorizzazioni agli utenti dell'organizzazione, selezionare **Aggiungi \<organization name> -tutti i membri** per selezionare tutti gli utenti nel tenant. Questa impostazione consente di escludere gli account guest. In alternativa, selezionare **Cerca nella directory** per selezionare un gruppo specifico. Per concedere autorizzazioni a utenti esterni o se si preferisce digitare l'indirizzo di posta elettronica, selezionare **Immettere i dettagli** e digitare l'indirizzo di posta elettronica dell'utente o del gruppo di Azure AD o il nome di dominio.
    
    Ripetere questo passaggio per specificare gli altri utenti che avranno le stesse autorizzazioni.

4. In **Scegliere le autorizzazioni dai valori preimpostati** selezionare le autorizzazioni da concedere: **Comproprietario**, **Coautore**, **Revisore** o **Personalizzate**.
    
    Nota: non selezionare **Visualizzatore** per i messaggi di posta elettronica. Se si seleziona **Personalizzate** assicurarsi di includere l'opzione **Modifica e salva**.
    
    Per selezionare le stesse autorizzazioni corrispondenti alla nuova opzione **Encrypt-Only** (Solo crittografia) di Exchange Online, selezionare **Personalizzate**. Selezionare quindi tutte le autorizzazioni tranne **Salva con nome, Esporta (EXPORT)** e **Controllo completo (OWNER)**.

5. Ripetere i passaggi 3 e 4 per specificare altri utenti con autorizzazioni diverse.

6. Fare clic su **OK** nel riquadro **Aggiungi autorizzazioni**.

7. Fare clic su **OK** nel riquadro **Protezione** e quindi su **Salva** nel riquadro **Etichetta**.


### <a name="example-5-label-that-encrypts-content-but-doesnt-restrict-who-can-access-it"></a>Esempio 5: Etichetta che crittografa il contenuto, ma non limita chi può accedervi

Questa configurazione offre il vantaggio che non è necessario specificare utenti, gruppi o domini per proteggere un documento o un messaggio di posta elettronica. Il contenuto verrà ugualmente crittografato ed è tuttavia possibile specificare i diritti di utilizzo, una data di scadenza e l'accesso offline. Usare questa configurazione solo quando non è necessario limitare chi può aprire il documento o il messaggio di posta elettronica protetto. [Altre informazioni su questa impostazione](#more-information-about-add-any-authenticated-users)

1. Nel riquadro **Protezione** verificare che sia selezionata l'opzione **Azure (chiave cloud)**.
    
2. Verificare che sia selezionata l'opzione **Configura le autorizzazioni**, quindi fare clic su **Aggiungi autorizzazioni**.

3. Nel riquadro **Aggiungi autorizzazioni** nella scheda **Selezionare dall'elenco** selezionare **Aggiungi eventuali utenti autenticati**.

4. Selezionare le autorizzazioni desiderate e fare clic su **OK**.

5. Nel riquadro **Protezione** configurare le impostazioni per **Scadenza del contenuto del file** e **Consenti l'accesso offline**, se necessario, quindi fare clic su **OK**.

6. Nel riquadro **Etichetta** selezionare **Salva**.


### <a name="example-6-label-that-applies-just-for-me-protection"></a>Esempio 6: etichetta che applica la protezione "Just for me"

Questa configurazione offre l'opposto della collaborazione sicura per i documenti: ad eccezione di un [utente con privilegi avanzati](configure-super-users.md), solo la persona che applica l'etichetta può aprire il contenuto protetto, senza alcuna restrizione. Questa configurazione è spesso definita protezione "Solo per me". È adatta quando un utente vuole salvare un file in una posizione qualsiasi ed essere certo che nessun altro potrà aprirlo.

La configurazione dell'etichetta è apparentemente semplice:

1. Nel riquadro **Protezione** verificare che sia selezionata l'opzione **Azure (chiave cloud)**.
    
2. Selezionare **OK** senza selezionare gli utenti o configurare le impostazioni di questo riquadro.
    
    Anche se è possibile configurare le impostazioni per **Scadenza del contenuto del file** e **Consenti l'accesso offline**, queste impostazioni di accesso non sono applicabili quando non si specificano utenti e le relative autorizzazioni. Questo succede perché l'utente che applica la protezione è l'[autorità di certificazione di Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner) per il contenuto e questo ruolo non è soggetto alle restrizioni di accesso.

3. Nel riquadro **Etichetta** selezionare **Salva**.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy). 

Anche le regole del flusso di posta di Exchange possono applicare la protezione, in base alle etichette. Per altre informazioni ed esempi, vedere [Configurazione delle regole del flusso di posta per le etichette di Exchange Online](configure-exo-rules.md).