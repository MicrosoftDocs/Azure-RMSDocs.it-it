---
title: Configurare un'etichetta di Azure Information Protection per la protezione
description: È possibile proteggere i documenti e i messaggi di posta elettronica più sensibili configurando un'etichetta per l'uso della protezione di Rights Management.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/02/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
ms.openlocfilehash: a1e480f8a071e8c5582169193a8e17ea2ec38e6f
ms.sourcegitcommit: 949bf02d5d12bef8e26d89ad5d6a0d5cc7826135
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/02/2018
ms.locfileid: "39474138"
---
# <a name="how-to-configure-a-label-for-rights-management-protection"></a>Come configurare un'etichetta per la protezione di Rights Management

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Non è possibile proteggere i documenti e i messaggi di posta elettronica più sensibili usando un servizio Rights Management. Questo servizio usa la crittografia, l'identità e i criteri di autorizzazione per prevenire la perdita di dati. Questa protezione viene applicata con un'etichetta configurata per l'uso della protezione Rights Management per documenti e messaggi di posta elettronica. Gli utenti possono anche selezionare il pulsante **Non inoltrare** in Outlook.

Quando si configura un'etichetta con l'impostazione di protezione **Azure (chiave cloud)** viene creato e configurato un modello di protezione al quale possono accedere i servizi e le applicazioni che si integrano con i modelli di Rights Management. Alcuni esempi sono Exchange Online, regole del flusso di posta e Outlook sul Web. 

## <a name="how-the-protection-works"></a>Come funziona la protezione

Quando un documento o un messaggio di posta elettronica è protetto da un servizio Rights Management, viene crittografato quando i dati sono inattivi e in transito. Può quindi essere decrittografato solo da utenti autorizzati. Questa crittografia rimane associata al documento o messaggio di posta elettronica, anche se viene rinominato. È anche possibile configurare diritti di utilizzo e restrizioni, come negli esempi seguenti:

- Solo gli utenti all'interno dell'organizzazione possono aprire il documento o il messaggio di posta elettronica riservato dell'azienda.

- Solo gli utenti del reparto marketing possono modificare e stampare il documento o il messaggio di posta elettronica relativo all'annuncio di promozione, mentre tutti gli altri utenti dell'organizzazione possono solo visualizzarlo.

- Gli utenti non possono inoltrare messaggi di posta elettronica o copiare informazioni da messaggi che contengono informazioni su una riorganizzazione interna.

- Il listino prezzi aggiornato inviato ai partner commerciali non può essere aperto dopo una certa data.

Per altre informazioni sulla tecnologia di protezione Azure Rights Management e sul suo funzionamento, vedere [Informazioni su Microsoft Azure Rights Management](../what-is-azure-rms.md).

> [!IMPORTANT]
> Per configurare un'etichetta in modo da applicare questa protezione, è necessario che il servizio Azure Rights Management sia attivo per l'organizzazione. Per ulteriori informazioni, vedere l'articolo relativo all'[attivazione di Azure Rights Management](../deploy-use/activate-service.md).

Quando l'etichetta applica la protezione, un documento protetto non è adatto per essere salvato in OneDrive o SharePoint. Questi percorsi non supportano le funzionalità seguenti per i file protetti: Creazione condivisa, Office Online, ricerca, anteprima di documenti, anteprima di video, eDiscovery e prevenzione della perdita di dati (DLP). 

Non è necessario configurare Exchange per Azure Information Protection per permettere agli utenti di applicare etichette in Outlook e proteggere i loro messaggi di posta elettronica. Tuttavia, fino a quando Exchange non viene configurato per Azure Information Protection, non si può usufruire delle funzionalità di protezione complete di Azure Rights Management con Exchange. Ad esempio, gli utenti non possono visualizzare messaggi di posta elettronica protetti nei telefoni cellulari o con Outlook dal Web, i messaggi di posta elettronica protetti non possono essere indicizzati per la ricerca e non è possibile configurare la prevenzione della perdita dei dati di Exchange Online con la protezione di Rights Management. Per assicurarsi che Exchange possa supportare questi scenari aggiuntivi, vedere le risorse seguenti:

- Per Exchange Online: vedere le istruzioni per [Exchange Online: configurazione di IRM](../deploy-use/configure-office365.md#exchange-online-irm-configuration).

- Per Exchange locale, è necessario distribuire il [connettore RMS e configurare i server Exchange](../deploy-use/deploy-rms-connector.md). 

## <a name="to-configure-a-label-for-protection-settings"></a>Per configurare un'etichetta per le impostazioni di protezione

1. Se non è già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Quindi passare al pannello **Azure Information Protection**. 
    
    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Dall'opzione di menu **CLASSIFICAZIONI** > **Etichette**: nel pannello **Azure Information Protection - Etichette** selezionare l'etichetta che si vuole modificare. 

3. Nel pannello **Etichetta** individuare la sezione **Configurare le autorizzazioni per documenti e messaggi di posta elettronica contenenti questa etichetta** e selezionare una delle opzioni seguenti:
    
    - **Non configurata**: selezionare questa opzione se l'etichetta è attualmente configurata in modo da applicare la protezione e non si vuole più che l'etichetta selezionata applichi la protezione. Procedere quindi con il passaggio 11.
        
        Le impostazioni di protezione configurate in precedenza vengono mantenute come un modello di protezione archiviato e verranno visualizzate di nuovo se si reimposta l'opzione su **Proteggi**. Questo modello non è visualizzato nel portale di Azure, ma è comunque possibile gestirlo con [PowerShell](configure-templates-with-powershell.md) se necessario. Questo comportamento indica che il contenuto rimane accessibile se ha questa etichetta con le impostazioni di protezione applicate in precedenza.
    
    - **Proteggi**: selezionare questa opzione per applicare la protezione e quindi procedere con il passaggio 5 per configurare le impostazioni di protezione.
    
    Nota: in questa fase è possibile salvare una nuova etichetta senza ulteriore configurazione. In tal caso, l'etichetta viene configurata per applicare la protezione in modo che solo la persona che applica l'etichetta possa aprire il documento o il messaggio di posta elettronica senza restrizioni di utilizzo. In alcuni casi, potrebbe essere questo il risultato richiesto, in modo che un utente possa salvare un file in qualsiasi posizione ed essere certo che nessun altro possa aprirlo. Se questo risultato corrisponde al requisito e non è necessario che altri utenti collaborino al contenuto protetto, andare direttamente al passaggio 12 invece che al 5.
    
    - **Rimuovi la protezione**: selezionare questa opzione per rimuovere la protezione se un documento o un messaggio di posta elettronica è protetto. Procedere quindi con il passaggio 11.
        
        Le impostazioni di protezione configurate in precedenza vengono mantenute come un modello di protezione archiviato e verranno visualizzate di nuovo se si reimposta l'opzione su **Proteggi**. Questo modello non è visualizzato nel portale di Azure, ma è comunque possibile gestirlo con [PowerShell](configure-templates-with-powershell.md) se necessario. Questo comportamento indica che il contenuto rimane accessibile se ha questa etichetta con le impostazioni di protezione applicate in precedenza.
        
        Si noti che, per applicare un'etichetta con questa opzione, gli utenti devono avere le autorizzazioni per rimuovere la protezione di Rights Management. Questo requisito significa che gli utenti devono disporre di **Esportazione** o **Controllo completo** come [diritto d'uso](../deploy-use/configure-usage-rights.md). oppure essere proprietari di Rights Management (che implica automaticamente il diritto di utilizzo Controllo completo) o essere [utenti con privilegi avanzati per Azure Rights Management](../deploy-use/configure-super-users.md). I modelli predefiniti di Azure Rights Management non includono i diritti di utilizzo che consentono agli utenti di rimuovere la protezione. 
        
        Se gli utenti non hanno le autorizzazioni per rimuovere la protezione di Rights Management e selezionano un'etichetta configurata con l'opzione **Rimuovi protezione**, viene visualizzato il messaggio seguente: **Azure Information Protection non può applicare questa etichetta. Se il problema persiste, contattare l'amministratore.**

4. Se si è selezionata l'opzione **Proteggi**, selezionare ora **Protezione** per aprire il pannello **Protezione**:
    
    ![Configurare la protezione per un'etichetta di Azure Information Protection](../media/info-protect-protection-bar-configured.png)

5. Nel pannello **Protezione** selezionare **Azure (cloud key)** (Azure - Chiave cloud) oppure **HYOK (AD RMS)**.
    
    Nella maggior parte dei casi è necessario selezionare **Azure (cloud key)** (Azure - Chiave cloud) per le impostazioni delle autorizzazioni. Non selezionare **HYOK (AD RMS)** a meno che non siano stati letti e compresi i prerequisiti e le restrizioni relativi a questa configurazione *HYOK* (Hold Your Own Key). Per altre informazioni, vedere [Requisiti e restrizioni HYOK per la protezione di AD RMS](configure-adrms-restrictions.md). Per continuare la configurazione per HYOK (AD RMS), procedere con il passaggio 9.
    
6. Selezionare una delle opzioni seguenti:
    
    - **Configura le autorizzazioni**: consente di definire nuove impostazioni di protezione nel portale.
    
    - **Configura le autorizzazioni definite dall'utente (anteprima)**: consente agli utenti di specificare a chi vengono concesse autorizzazioni e quali sono queste autorizzazioni. È quindi possibile completare l'impostazione dell'opzione e scegliere solo Outlook oppure Word, Excel, PowerPoint e File Explorer. Questa opzione non è supportata e non funziona quando viene configurata un'etichetta per la [classificazione automatica](configure-policy-classification.md).
        
        Se si sceglie l'opzione per Outlook l'etichetta viene visualizzata in Outlook e il comportamento quando gli utenti applicano l'etichetta è uguale a quello generato dall'opzione Non inoltrare.
        
        Se si sceglie l'opzione per Word, Excel, PowerPoint e File Explorer, quando l'opzione è impostata l'etichetta viene visualizzata in queste applicazioni. Quando gli utenti applicano l'etichetta viene visualizzata la finestra di dialogo che consente loro di selezionare le autorizzazioni personalizzate. Nella finestra di dialogo gli utenti devono specificare gli utenti o i gruppi, le autorizzazioni e una data di scadenza. Verificare che gli utenti dispongano di istruzioni e linee guida per specificare questi valori.
    
    - **Seleziona un modello predefinito**: per usare uno dei modelli predefiniti o un modello personalizzato che è stato configurato. Si noti che questa opzione non viene visualizzata per le nuove etichette o se si sta modificando un'etichetta che in precedenza usava l'opzione **Configura le autorizzazioni**.
    
    Per selezionare un modello predefinito, il modello deve essere pubblicato (non archiviato) e non deve essere già collegato a un'altra etichetta. Quando si seleziona questa opzione è possibile usare il pulsante **Modifica modello** per [convertire il modello in un'etichetta](configure-policy-templates.md#to-convert-templates-to-labels).
    
    Suggerimento: se si creano e usano regolarmente modelli personalizzati, può risultare utile consultare [Attività che precedentemente venivano eseguite con il portale di Azure classico](migrate-portal.md).

7. Se è stata selezionata l'opzione **Imposta autorizzazioni** per **Azure (cloud key)** (Azure - Chiave cloud), questa opzione consente di configurare le stesse impostazioni configurabili in un modello. 
    
    Selezionare **Aggiungere autorizzazioni**, quindi, nel pannello **Aggiungere autorizzazioni**, selezionare il primo set di utenti e gruppi che avranno il diritto di usare il contenuto che verrà protetto per l'etichetta selezionata:
    
    - Scegliere **Selezionare dall'elenco** in cui è possibile aggiungere tutti gli utenti dell'organizzazione selezionando **Aggiungi \<nome organizzazione> - Tutti i membri**. Questa impostazione consente di escludere gli account guest. In alternativa è possibile selezionare **Add any authenticated users (Preview)** (Aggiungi qualsiasi utente autenticato - Anteprima) o passare alla directory.
        
        Quando si scelgono tutti i membri o si passa alla directory, gli utenti o i gruppi devono avere un indirizzo di posta elettronica. In un ambiente di produzione, utenti e gruppi quasi mai hanno un indirizzo di posta elettronica, ma in un ambiente di test semplice può essere necessario aggiungere gli indirizzi di posta elettronica agli account utente o ai gruppi.
        
        ###### <a name="more-information-about-add-any-authenticated-users"></a>Altre informazioni su **Add any authenticated users** (Aggiungi qualsiasi utente autenticato) 
        Questa impostazione non limita chi può accedere al contenuto protetto dall'etichetta, pur crittografando il contenuto e fornendo le opzioni per limitare come usare il contenuto (autorizzazioni) e come accedervi (scadenza e accesso offline). L'applicazione che apre il contenuto protetto deve tuttavia poter supportare l'autenticazione in uso. Per questo motivo, i provider di servizi di social networking federati, ad esempio Google, e l'autenticazione di passcode monouso devono essere usati solo per la posta elettronica e solo quando si usano Exchange Online e le nuove funzionalità di Office 365 Message Encryption. Gli account Microsoft possono essere usati con il visualizzatore Azure Information Protection e Office 2016 A portata di clic. 
        
        Alcuni scenari tipici per l'impostazione relativa agli utenti autenticati: - Non è importante chi visualizza il contenuto, ma si vuole limitare il modo in cui viene usato. Ad esempio, non si vuole che il contenuto venga modificato, copiato o stampato.
            - Non è necessario limitare chi accede al contenuto, ma si vuole tenere traccia di chi lo apre e, potenzialmente, lo revoca.
            - Esiste un requisito in base al quale il contenuto deve essere crittografato quando è inattivo e quando è in transito, ma non sono necessari controlli di accesso.     
        
    - Scegliere **Immettere i dettagli** per specificare manualmente gli indirizzi di posta elettronica dei singoli utenti o gruppi (interni o esterni) o per specificare tutti gli utenti in un'altra organizzazione immettendo un nome di dominio di tale organizzazione. È anche possibile usare questa opzione per i provider di social networking, immettendo i nomi di dominio, ad esempio **gmail.com**, **hotmail.com** oppure **outlook.com**.
        
    >[!NOTE]
    >Se un indirizzo di posta elettronica viene modificato dopo che si è selezionato l'utente o il gruppo, vedere la sezione [Considerazioni in caso di modifica degli indirizzi di posta elettronica](../plan-design/prepare.md#considerations-for-azure-information-protection-if-email-addresses-change) della documentazione relativa alla pianificazione.
    
    Come procedura consigliata, usare gruppi anziché utenti. Questo strategia mantiene la configurazione più semplice e rende meno probabile la necessità di aggiornare la configurazione dell'etichetta in un secondo momento e quindi di proteggere nuovamente il contenuto. Tuttavia, se si apportano modifiche al gruppo, tenere presente che, per motivi di prestazioni, Azure Rights Management [memorizza nella cache l'appartenenza ai gruppi](../plan-design/prepare.md#group-membership-caching-by-azure-information-protection). 
    
    Dopo avere specificato il primo set di utenti e gruppi, selezionare le autorizzazioni da concedere a tali utenti e gruppi. Per altre informazioni sulle autorizzazioni selezionabili, vedere [Configurazione dei diritti di utilizzo per Azure Rights Management](configure-usage-rights.md). Tuttavia, le applicazioni che supportano Rights Management possono implementare queste autorizzazioni in modo diverso. Consultare la relativa documentazione ed eseguire test personalizzati con le applicazioni usate dagli utenti per controllare il comportamento prima di distribuire il modello per gli utenti.
    
    Se necessario, è ora possibile aggiungere un secondo set di utenti e gruppi con diritti di utilizzo. Ripetere fino a quando non sono stati specificati tutti gli utenti e i gruppi con le rispettive autorizzazioni.

    >[!TIP]
    >Valutare l'opportunità di aggiungere l'autorizzazione personalizzata **Salva con nome, Esporta (EXPORT)** e concederla al personale o agli amministratori selezionati in altri ruoli responsabili del recupero delle informazioni. Tali utenti possono rimuovere, se necessario, la protezione da file e messaggi di posta elettronica che verranno protetti mediante questo modello o etichetta. La possibilità di rimuovere la protezione a livello di autorizzazione per un documento o un messaggio di posta elettronica consente un controllo più accurato rispetto all'uso della [funzionalità dell'utente con privilegi avanzati](configure-super-users.md).
    
    Per tutti gli utenti e i gruppi specificati, nel pannello **Protezione** controllare se si desidera apportare modifiche alle seguenti impostazioni. Si noti che queste impostazioni, come le autorizzazioni, non si applicano all'[emittente di Rights Management e proprietario di Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner), o a qualsiasi [utente con privilegi avanzati](configure-super-users.md) che è stato assegnato.
    
    ###### <a name="information-about-the-protection-settings"></a>Informazioni sulle impostazioni di protezione
    
    |Impostazione|Altre informazioni|Impostazione consigliata
    |-----------|--------------------|--------------------|
    |**scadenza contenuto**|Definire una data o un numero di giorni in cui i documenti o i messaggi di posta elettronica protetti tramite queste impostazioni non devono essere aperti da alcuni utenti selezionati. È possibile specificare una data o un numero di giorni a partire dal momento in cui la protezione viene applicata ai contenuti.<br /><br />Quando si specifica una data, diventa effettiva alla mezzanotte del fuso orario corrente.|**Nessuna scadenza contenuto**, a meno che non esista un requisito temporale specifico per il contenuto.|
    |**Consenti l'accesso offline**|Usare questa impostazione per bilanciare i requisiti di sicurezza, compreso l'accesso dopo la revoca, con la possibilità per gli utenti selezionati di aprire il contenuto protetto quando non hanno una connessione Internet.<br /><br />Se si specifica che il contenuto non è disponibile senza una connessione Internet o che è disponibile solo per un determinato numero di giorni, al raggiungimento di tale soglia, gli utenti dovranno eseguire di nuovo l'autenticazione e l'accesso verrà registrato. In questo caso, se le credenziali non sono memorizzate nella cache, verrà chiesto agli utenti di eseguire l'accesso prima di poter aprire il documento o il messaggio di posta elettronica.<br /><br />Oltre alla riesecuzione dell'autenticazione, viene nuovamente valutata l'appartenenza degli utenti ai criteri e ai gruppi. Questo significa che gli utenti potrebbero avere risultati di accesso diversi per lo stesso documento o messaggio di posta elettronica se dall'ultimo accesso ai contenuti si sono verificati cambiamenti relativi all'appartenenza ai criteri o ai gruppi. Ciò potrebbe includere anche l'impossibilità di accedere al documento se questo è stato [revocato](../rms-client/client-track-revoke.md).|A seconda della sensibilità del contenuto:<br /><br />- **Numero di giorni per cui il contenuto è disponibile senza una connessione a Internet** = **7** per i dati aziendali sensibili che potrebbero causare danni all'azienda in caso di condivisione con persone non autorizzate. Questa raccomandazione offre un equo compromesso tra sicurezza e flessibilità. Sono esempi di questo tipo di contenuto i contratti, i report sulla sicurezza, i riepiloghi previsionali e i dati sulle vendite.<br /><br />- **Mai** per dati aziendali particolarmente riservati che potrebbero causare danni all'azienda se condivisi con utenti non autorizzati. Questa indicazione assegna maggiore priorità alla sicurezza che alla flessibilità e garantisce che, se il documento viene revocato, per tutti gli utenti autorizzati sarà immediatamente impossibile aprirlo. Sono esempi di questo tipo di contenuto le informazioni su dipendenti e clienti, le password, il codice sorgente e i rendiconti finanziari preannunciati.|
    
    Al termine della configurazione delle autorizzazioni e delle impostazioni, fare clic su **OK**. 
    
    Questo raggruppamento di impostazioni consente di creare un modello personalizzato per il servizio Azure Rights Management. I modelli possono essere usati con applicazioni e servizi che si integrano con Azure Rights Management. Per informazioni sul download e l'aggiornamento dei modelli nei computer e nei servizi, vedere [Aggiornamento dei modelli per gli utenti](refresh-templates.md).

8. Se è stata selezionata l'opzione **Seleziona un modello predefinito** per **Azure (cloud key)** (Azure - Chiave cloud), fare clic sulla casella di riepilogo a discesa e selezionare il [modello](../deploy-use/configure-policy-templates.md) da usare per proteggere i documenti e i messaggi di posta elettronica con questa etichetta. Non sono visualizzati modelli archiviati o modelli già selezionati per un'altra etichetta.
    
    Se si seleziona un **modello di reparto** oppure se sono stati configurati [controlli di selezione](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment):
    
    - Gli utenti che non rientrano nell'ambito del modello configurato o che sono esclusi dall'applicazione della protezione di Azure Rights Management visualizzano comunque l'etichetta ma non possono applicarla. Se si seleziona l'etichetta, viene visualizzato un messaggio che indica che **Azure Information Protection non può applicare l'etichetta. Se il problema persiste, contattare l'amministratore.**
        
        Si noti che vengono visualizzati sempre tutti i modelli pubblicati, anche se si sta configurando un criterio con ambito. Si supponga ad esempio di configurare un criterio con ambito per il gruppo Marketing. I modelli che è possibile selezionare non sono solo quelli appartenenti all'ambito del gruppo Marketing ed è possibile selezionare un modello di reparto che non può essere usato dagli utenti selezionati. Per semplificare la configurazione e per ridurre al minimo la risoluzione dei problemi, provare a ridenominare il modello di reparto in modo da corrispondere all'etichetta nel criterio con ambito. 

9. Se è stato selezionato **HYOK (AD RMS)**, selezionare **Imposta i dettagli del modello di AD RMS** o **Configura le autorizzazioni definite dall'utente (anteprima)**. Specificare quindi l'URL della licenza per il cluster AD RMS.
    
    Per istruzioni su come specificare un GUID di modello e l'URL della licenza, vedere [Individuazione delle informazioni per specificare la protezione di AD RMS con un'etichetta di Azure Information Protection](configure-adrms-restrictions.md#locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label).
    
    L'opzione per le autorizzazioni definite dall'utente consente agli utenti di specificare a chi vengono concesse autorizzazioni e quali sono queste autorizzazioni. È quindi possibile completare l'impostazione dell'opzione e scegliere solo Outlook (impostazione predefinita) oppure Word, Excel, PowerPoint e File Explorer. Questa opzione non è supportata e non funziona quando viene configurata un'etichetta per la [classificazione automatica](configure-policy-classification.md).
    
    Se si sceglie l'opzione per Outlook l'etichetta viene visualizzata in Outlook e il comportamento quando gli utenti applicano l'etichetta è uguale a quello generato dall'opzione Non inoltrare.
    
    Se si sceglie l'opzione per Word, Excel, PowerPoint e File Explorer l'etichetta viene visualizzata in queste applicazioni. Quando gli utenti applicano l'etichetta viene visualizzata la finestra di dialogo che consente loro di selezionare le autorizzazioni personalizzate. Nella finestra di dialogo gli utenti devono specificare gli utenti o i gruppi, le autorizzazioni e una data di scadenza. Verificare che gli utenti dispongano di istruzioni e linee guida per specificare questi valori.

10. Fare clic su **OK** per chiudere il pannello **Protezione** e visualizzare la scelta **Definito dall'utente** o il modello selezionato per l'opzione **Protezione** nel pannello **Etichetta**.

11. Nel pannello **Etichetta** fare clic su **Salva**.

12. Nel pannello **Azure Information Protection** usare la colonna **Protezione** per confermare che l'etichetta ora visualizza l'impostazione di protezione desiderata:
    
    - Un segno di spunta se è stata configurata la protezione. 
    
    - Un segno x per indicare l'annullamento se è stata configurata un'etichetta per la rimozione della protezione.
    
    - Un campo vuoto se la protezione non è impostata. 

Quando fa clic su **Salva**, le modifiche diventano automaticamente disponibili per utenti e servizi. Non è più presente un'opzione di pubblicazione separata.


## <a name="example-configurations"></a>Configurazioni di esempio

Le etichette secondarie **Tutti i dipendenti** e **Solo destinatari** delle etichette **Riservato** e **Riservatezza elevata** dei [criteri predefiniti](configure-policy-default.md) sono esempi di configurazione delle etichette per l'applicazione della protezione. È anche possibile usare gli esempi seguenti per la configurazione di diversi scenari. 

Per ognuno degli esempi seguenti, nel pannello \<*nome etichetta*> selezionare **Proteggi** e quindi **Protezione** per aprire il pannello **Protezione**.

### <a name="example-1-label-that-applies-do-not-forward-to-send-a-protected-email-to-a-gmail-account"></a>Esempio 1: etichetta che applica Non inoltrare per l'invio di un messaggio di posta elettronica protetto a un account Gmail

Questa etichetta è disponibile solo in Outlook ed è appropriata quando Exchange Online è configurato per le [nuove funzionalità di Office 365 Message Encryption](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e). Indicare agli utenti di selezionare l'etichetta quando devono inviare un messaggio protetto a destinatari che usano un account Gmail (o qualsiasi altro account di posta elettronica esterno all'organizzazione). 

Gli utenti digitano l'indirizzo di posta elettronica Gmail nella casella **A**.  Gli utenti selezionano quindi l'etichetta e l'opzione Non inoltrare viene aggiunta automaticamente al messaggio di posta elettronica. Il risultato è che i destinatari non possono inoltrare il messaggio di posta elettronica, stamparlo, copiarne il contenuto, salvare gli allegati o salvare il messaggio di posta elettronica con un nome diverso. 

1. Nel pannello **Protezione** verificare che sia selezionata l'opzione **Azure (cloud key)** (Azure - Chiave cloud).
    
2. Selezionare **Configura le autorizzazioni definite dall'utente (anteprima)**.

3. Verificare che sia selezionata l'opzione **In Outlook applica Non inoltrare**.

4. Se è selezionata, deselezionare l'opzione **In Word, Excel, PowerPoint e File Explorer richiedi all'utente le autorizzazioni personalizzate**.

5. Fare clic su **OK** nel pannello **Protezione** e quindi fare clic su **Salva** nel pannello **Etichetta**.


### <a name="example-2-label-that-restricts-read-only-permission-to-all-users-in-another-organization-and-that-supports-immediate-revocation"></a>Esempio 2: etichetta che limita l'autorizzazione di sola lettura a tutti gli utenti di un'altra organizzazione e supporta la revoca immediata

Questa etichetta è adatta per la condivisione (in sola lettura) di documenti molto sensibili che richiedono sempre una connessione Internet per la visualizzazione. Se viene revocata, gli utenti non potranno visualizzare il documento quando provano nuovamente ad aprirlo.

Questa etichetta non è adatta per i messaggi di posta elettronica.

1. Nel pannello **Protezione** verificare che sia selezionata l'opzione **Azure (cloud key)** (Azure - Chiave cloud).
    
2. Verificare che sia selezionata l'opzione **Configura le autorizzazioni** e quindi fare clic su **Aggiungi autorizzazioni**.

3. Nel pannello **Aggiungi autorizzazioni** selezionare **Immettere i dettagli**.

4. Immettere il nome di un dominio dell'altra organizzazione, ad esempio **fabrikam.com**. Selezionare **Aggiungi**.

5. In **Scegliere le autorizzazioni dai valori preimpostati** selezionare **Visualizzatore**, quindi scegliere **OK**.

6. Nel pannello **Protezione** in **Consenti l'accesso offline** selezionare **Mai**.

7. Fare clic su **OK** nel pannello **Protezione** e quindi fare clic su **Salva** nel pannello **Etichetta**.


### <a name="example-3-add-external-users-to-an-existing-label"></a>Esempio 3: aggiungere utenti esterni a un'etichetta esistente

I nuovi utenti aggiunti potranno aprire i documenti e i messaggi di posta elettronica già protetti con questa etichetta. Le autorizzazioni concesse a questi utenti possono essere diverse da quelle di cui dispongono gli utenti esistenti.

1. Nel pannello **Protezione** verificare che sia selezionata l'opzione **Azure (chiave cloud)**.
    
2. Verificare che sia selezionata l'opzione **Configura le autorizzazioni**, quindi fare clic su **Aggiungi autorizzazioni**.

3. Nel pannello **Aggiungi autorizzazioni** selezionare **Immettere i dettagli**.

4. Immettere l'indirizzo di posta elettronica del primo utente o gruppo da aggiungere e selezionare **Aggiungi**.

5. Selezionare le autorizzazioni per l'utente o il gruppo.

6. Ripetere i passaggi 4 e 5 per ogni utente o gruppo che si vuole aggiungere a questa etichetta. Fare quindi clic su **OK**.

7. Fare clic su **OK** nel pannello **Protezione** e quindi fare clic su **Salva** nel pannello **Etichetta**.

### <a name="example-4-label-for-protected-email-that-supports-less-restrictive-permissions-than-do-not-forward"></a>Esempio 4: etichetta per la posta elettronica protetta che supporta autorizzazioni meno restrittive rispetto a Non inoltrare

Questa etichetta non può essere limitata a Outlook ma fornisce controlli meno restrittivi rispetto all'uso di Non inoltrare. Ad esempio, se si vuole che i destinatari possano copiare dati dal messaggio di posta elettronica o da un allegato oppure che possano salvare e modificare un allegato.

Se si specificano gli utenti esterni che non hanno un account in Azure AD:

- L'etichetta è appropriata per i messaggi di posta elettronica quando Exchange Online usa le [nuove funzionalità di Office 365 Message Encryption](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e). 
 
- Per gli allegati di Office protetti automaticamente, questi documenti possono essere visualizzati in un browser. Per modificare questi documenti, scaricarli e modificarli con Office 2016 A portata di clic e un account Microsoft che usa lo stesso indirizzo di posta elettronica. [Altre informazioni](../secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)


> [!NOTE]
> Exchange Online sta distribuendo una nuova opzione: [Encrypt-Only](configure-usage-rights.md#encrypt-only-option-for-emails) (Solo crittografia). Questa opzione non è disponibile per la configurazione delle etichette. È tuttavia possibile, quando si conoscono i destinatari, usare questo esempio per configurare un'etichetta con lo stesso set di diritti di utilizzo. 

Quando gli utenti specificano gli indirizzi di posta elettronica nella casella **A** gli indirizzi devono essere quelli degli utenti specificati per questa configurazione di etichetta. Dato che gli utenti possono appartenere a gruppi e avere più di un indirizzo di posta elettronica, l'indirizzo di posta elettronica che specificano non deve corrispondere esattamente a quello specificato per le autorizzazioni, anche se questo è il modo più semplice per garantire che il destinatario venga autorizzato. Per altre informazioni sull'applicazione delle autorizzazioni agli utenti, vedere [Preparazione di utenti e gruppi per Azure Information Protection](../plan-design/prepare.md). 

1. Nel pannello **Protezione** verificare che sia selezionata l'opzione **Azure (cloud key)** (Azure - Chiave cloud).
    
2. Verificare che sia selezionata l'opzione **Configura le autorizzazioni** e fare clic su **Aggiungi autorizzazioni**.

3. Nel pannello **Aggiungi autorizzazioni** per concedere le autorizzazioni agli utenti dell'organizzazione selezionare **Aggiungi \<nome organizzazione> - Tutti i membri** per selezionare tutti gli utenti del tenant. Questa impostazione consente di escludere gli account guest. In alternativa, selezionare **Cerca nella directory** per selezionare un gruppo specifico. Per concedere autorizzazioni a utenti esterni o se si preferisce digitare l'indirizzo di posta elettronica, selezionare **Immettere i dettagli** e digitare l'indirizzo di posta elettronica dell'utente o del gruppo di Azure AD o il nome di dominio.
    
    Ripetere questo passaggio per specificare gli altri utenti che avranno le stesse autorizzazioni.

4. In **Scegliere le autorizzazioni dai valori preimpostati** selezionare le autorizzazioni da concedere: **Comproprietario**, **Coautore**, **Revisore** o **Personalizzate**.
    
    Nota: non selezionare **Visualizzatore** per i messaggi di posta elettronica. Se si seleziona **Personalizzate** verificare di includere l'opzione **Modifica e salva**.
    
    Per selezionare le stesse autorizzazioni corrispondenti alla nuova opzione **Encrypt-Only** (Solo crittografia) di Exchange Online, selezionare **Personalizzate**. Selezionare quindi tutte le autorizzazioni tranne **Salva con nome, Esporta (EXPORT)** e **Controllo completo (OWNER)**.

5. Ripetere i passaggi 3 e 4 per specificare altri utenti con autorizzazioni diverse.

6. Fare clic su **OK** nel pannello **Aggiungi autorizzazioni**.

7. Fare clic su **OK** nel pannello **Protezione** e quindi fare clic su **Salva** nel pannello **Etichetta**.


### <a name="example-5-label-that-encrypts-content-but-doesnt-restrict-who-can-access-it"></a>Esempio 5: Etichetta che crittografa il contenuto, ma non limita chi può accedervi

Questa configurazione offre il vantaggio che non è necessario specificare utenti, gruppi o domini per proteggere un documento o un messaggio di posta elettronica. Il contenuto verrà ugualmente crittografato ed è tuttavia possibile specificare i diritti di utilizzo, una data di scadenza e l'accesso offline. Usare questa configurazione solo quando non è necessario limitare chi può aprire il documento o il messaggio di posta elettronica protetto. [Altre informazioni su questa impostazione](#more-information-about-add-any-authenticated-users)

1. Nel pannello **Protezione** verificare che sia selezionata l'opzione **Azure (chiave cloud)**.
    
2. Verificare che sia selezionata l'opzione **Configura le autorizzazioni**, quindi fare clic su **Aggiungi autorizzazioni**.

3. Nel pannello **Aggiungi autorizzazioni** nella scheda **Selezionare dall'elenco** selezionare **Add any authenticated users (Preview)** (Aggiungi qualsiasi utente autenticato - Anteprima).

4. Selezionare le autorizzazioni desiderate e fare clic su **OK**.

5. Nel pannello **Protezione** configurare le impostazioni per **Scadenza del contenuto** e **Consenti l'accesso offline**, se necessario, e quindi fare clic su **OK**.

6. Nel pannello **Etichetta** selezionare **Salva**.


## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy). 

Anche le regole del flusso di posta di Exchange possono applicare la protezione, in base alle etichette. Per altre informazioni ed esempi, vedere [Configurazione delle regole del flusso di posta per le etichette di Exchange Online](configure-exo-rules.md).  
