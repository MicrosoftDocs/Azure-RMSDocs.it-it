---
title: Configurare un'etichetta di Azure Information Protection per la protezione
description: "È possibile proteggere i documenti e i messaggi di posta elettronica più sensibili configurando un'etichetta per l'uso della protezione di Rights Management."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/21/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
ms.openlocfilehash: dccd5f86dd75cf053336426df161e927b4cd9e5b
ms.sourcegitcommit: 76bf1f93b02fd75bead8ccdaaf34da1a6aad571f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/22/2017
---
# <a name="how-to-configure-a-label-for-rights-management-protection"></a>Come configurare un'etichetta per la protezione di Rights Management

>*Si applica a: Azure Information Protection*

Non è possibile proteggere i documenti e i messaggi di posta elettronica più sensibili usando un servizio Rights Management. Questo servizio usa la crittografia, l'identità e i criteri di autorizzazione per prevenire la perdita di dati. Questa protezione viene applicata con un'etichetta configurata per l'uso della protezione Rights Management per documenti e messaggi di posta elettronica. Gli utenti possono anche selezionare il pulsante **Non inoltrare** in Outlook. 

## <a name="how-the-protection-works"></a>Come funziona la protezione

Quando un documento o un messaggio di posta elettronica è protetto da un servizio Rights Management, viene crittografato quando i dati sono inattivi e in transito. Può quindi essere decrittografato solo da utenti autorizzati. Questa crittografia rimane associata al documento o messaggio di posta elettronica, anche se viene rinominato. È anche possibile configurare diritti di utilizzo e restrizioni, come negli esempi seguenti:

- Solo gli utenti all'interno dell'organizzazione possono aprire il documento o il messaggio di posta elettronica riservato dell'azienda.

- Solo gli utenti del reparto marketing possono modificare e stampare il documento o il messaggio di posta elettronica relativo all'annuncio di promozione, mentre tutti gli altri utenti dell'organizzazione possono solo visualizzarlo.

- Gli utenti non possono inoltrare messaggi di posta elettronica o copiare informazioni da messaggi che contengono informazioni su una riorganizzazione interna.

- Il listino prezzi aggiornato inviato ai partner commerciali non può essere aperto dopo una certa data.

Per altre informazioni sulla tecnologia di protezione Azure Rights Management e sul suo funzionamento, vedere [Informazioni su Microsoft Azure Rights Management](../understand-explore/what-is-azure-rms.md).

> [!IMPORTANT]
> Per configurare un'etichetta in modo da applicare questa protezione, è necessario che il servizio Azure Rights Management sia attivo per l'organizzazione. Se non è ancora stato fatto, vedere [Attivazione di Azure Rights Management](../deploy-use/activate-service.md).

Quando l'etichetta applica la protezione, un documento protetto non è adatto per essere salvato in OneDrive o SharePoint. Questi percorsi non supportano le operazioni seguenti per i file protetti: Creazione condivisa, Office Online, ricerca, anteprima di documenti, anteprima di video, eDiscovery e prevenzione della perdita di dati (DLP). 

Non è necessario configurare Exchange per Information Rights Management (IRM) per permettere agli utenti di applicare etichette in Outlook e proteggere i loro messaggi di posta elettronica. Tuttavia, fino a quando Exchange non sarà configurato per IRM, non si potrà usufruire della funzionalità completa della protezione di Rights Management di Azure con Exchange. Ad esempio, gli utenti non potranno visualizzare messaggi di posta elettronica protetti nei telefoni cellulari o con Outlook dal Web, i messaggi di posta elettronica protetti non potranno essere indicizzati per la ricerca e non sarà possibile configurare la prevenzione della perdita dei dati di Exchange Online con la protezione di Rights Management. Per configurare Exchange in modo da supportare questi scenari aggiuntivi, vedere le risorse seguenti:

- Per Exchange Online: vedere le istruzioni per [Exchange Online: configurazione di IRM](../deploy-use/configure-office365.md#exchange-online-irm-configuration).

- Per Exchange locale, è necessario distribuire il [connettore RMS e configurare i server Exchange](../deploy-use/deploy-rms-connector.md). 

## <a name="to-configure-a-label-for-rights-management-protection"></a>Per configurare un'etichetta per la protezione di Rights Management

1. Se non è già stato fatto, aprire una nuova finestra del browser e accedere al [portale di Azure](https://portal.azure.com) come amministratore globale o della sicurezza. Quindi passare al pannello **Azure Information Protection**. 
    
    Ad esempio, dal menu principale fare clic su **Altri servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Se l'etichetta da configurare viene applicata a tutti gli utenti, restare nel pannello **Azure Information Protection - Criteri globali**. Se tuttavia l'etichetta da configurare si trova in [criteri con ambito](configure-policy-scope.md) per essere applicata solo agli utenti selezionati, nel menu **CRITERI** selezionare **Criteri con ambito**. Selezionare quindi i criteri con ambito nel pannello **Azure Information Protection - Criteri con ambito**.

3. Selezionare l'etichetta da configurare. Verrà aperto il pannello **Etichetta**. 

4. Nel pannello **Etichetta** individuare la sezione **Set permissions for documents and emails containing this label** (Impostare le autorizzazioni per documenti e messaggi di posta elettronica contenenti questa etichetta) e selezionare una delle opzioni seguenti:
    
    - **Non configurata**: selezionare questa opzione se l'etichetta è attualmente configurata in modo da applicare la protezione e non si vuole più che l'etichetta selezionata applichi la protezione. Procedere quindi con il passaggio 11.
    
    - **Proteggi**: selezionare questa opzione per applicare la protezione e quindi procedere con il passaggio 5.
    
    - **Rimuovi la protezione**: selezionare questa opzione per rimuovere la protezione se un documento o un messaggio di posta elettronica è protetto. Procedere quindi con il passaggio 11.
        
        Si noti che, per applicare un'etichetta con questa opzione, gli utenti devono avere le autorizzazioni per rimuovere la protezione di Rights Management. Questo requisito significa che gli utenti devono disporre di **Esportazione** o **Controllo completo** come [diritto d'uso](../deploy-use/configure-usage-rights.md). oppure essere proprietari di Rights Management (che implica automaticamente il diritto di utilizzo Controllo completo) o essere [utenti con privilegi avanzati per Azure Rights Management](../deploy-use/configure-super-users.md). I modelli predefiniti di Azure Rights Management non includono i diritti di utilizzo che consentono agli utenti di rimuovere la protezione. 
        
        Se gli utenti non hanno le autorizzazioni per rimuovere la protezione di Rights Management e selezionano un'etichetta configurata con l'opzione **Rimuovi protezione**, viene visualizzato il messaggio seguente: **Azure Information Protection non può applicare questa etichetta. Se il problema persiste, contattare l'amministratore.**

5. Se si è selezionata l'opzione **Proteggi**, selezionare ora **Protezione** per aprire il pannello **Protezione**:
    
    ![Configurare la protezione per un'etichetta di Azure Information Protection](../media/info-protect-protection-bar-configured.png)

6. Nel pannello **Protezione** selezionare **Azure (cloud key)** (Azure - Chiave cloud) oppure **HYOK (AD RMS)**.
    
    Nella maggior parte dei casi è necessario selezionare **Azure (cloud key)** (Azure - Chiave cloud) per le impostazioni delle autorizzazioni. Non selezionare **HYOK (AD RMS)** a meno che non siano stati letti e compresi i prerequisiti e le restrizioni relativi a questa configurazione *HYOK* (Hold Your Own Key). Per altre informazioni, vedere [Requisiti e restrizioni HYOK per la protezione di AD RMS](configure-adrms-restrictions.md). Per continuare la configurazione per HYOK (AD RMS), procedere con il passaggio 10.
    
7. Selezionare una delle opzioni seguenti:
    
    - **Seleziona un modello predefinito**: per usare uno dei modelli predefiniti o un modello personalizzato che è stato configurato. Questo modello deve essere pubblicato (non archiviato) e non deve essere già collegato a un'altra etichetta. Quando si seleziona questa opzione è possibile usare il pulsante **Modifica modello** per [convertire il modello in un'etichetta](configure-policy-templates.md#to-convert-templates-to-labels).
    
    Suggerimento: se si usa il pulsante **Modifica modello** può risultare utile consultare [Tasks that you used to do with the Azure classic portal](migrate-portal.md) (Attività che si eseguivano con il portale di Azure classico).
    
    - **Configura le autorizzazioni**: consente di definire nuove impostazioni di protezione nel portale.
    
    - **Configura le autorizzazioni definite dall'utente (anteprima)**: consente agli utenti di specificare a chi vengono concesse autorizzazioni e quali sono queste autorizzazioni. È quindi possibile completare l'impostazione dell'opzione e scegliere solo Outlook (impostazione predefinita) oppure Word, Excel, PowerPoint e File Explorer. 
        
        Se si sceglie l'opzione per Outlook l'etichetta viene visualizzata in Outlook e il comportamento quando gli utenti applicano l'etichetta è uguale a quello generato dall'opzione Non inoltrare.
        
        Se si sceglie l'opzione per Word, Excel, PowerPoint e File Explorer, quando l'opzione è impostata l'etichetta viene visualizzata in queste applicazioni. Quando gli utenti applicano l'etichetta viene visualizzata la finestra di dialogo che consente loro di selezionare le autorizzazioni personalizzate. Nella finestra di dialogo gli utenti devono specificare gli utenti o i gruppi, le autorizzazioni e una data di scadenza. Verificare che gli utenti dispongano di istruzioni e linee guida per specificare questi valori.

8. Se è stata selezionata l'opzione **Seleziona un modello predefinito** per **Azure (cloud key)** (Azure - Chiave cloud), fare clic sulla casella di riepilogo a discesa e selezionare il [modello](../deploy-use/configure-policy-templates.md) da usare per proteggere i documenti e i messaggi di posta elettronica con questa etichetta. Non sono visualizzati modelli archiviati o modelli già selezionati per un'altra etichetta.
    
    Se si seleziona un **modello di reparto** oppure se sono stati configurati [controlli di selezione](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment):
    
    - Gli utenti che non rientrano nell'ambito del modello configurato o che sono esclusi dall'applicazione della protezione di Azure Rights Management visualizzeranno comunque l'etichetta ma non potranno applicarla. Se si seleziona l'etichetta, viene visualizzato un messaggio che indica che **Azure Information Protection non può applicare l'etichetta. Se il problema persiste, contattare l'amministratore.**
        
        Si noti che vengono visualizzati sempre tutti i modelli pubblicati, anche se si sta configurando un criterio con ambito. Si supponga ad esempio di configurare un criterio con ambito per il gruppo Marketing. I modelli che è possibile selezionare non sono solo quelli appartenenti all'ambito del gruppo Marketing ed è possibile selezionare un modello di reparto che non può essere usato dagli utenti selezionati. Per semplificare la configurazione e per ridurre al minimo la risoluzione dei problemi, provare a ridenominare il modello di reparto in modo da corrispondere all'etichetta nel criterio con ambito. 
            
9. Se è stata selezionata l'opzione **Imposta autorizzazioni** per **Azure (cloud key)** (Azure - Chiave cloud), questa opzione consente di configurare le stesse impostazioni configurabili in un modello. 
    
    Selezionare **Aggiungere autorizzazioni**, quindi, nel pannello **Aggiungere autorizzazioni**, selezionare il primo set di utenti e gruppi che avranno il diritto di usare il contenuto che verrà protetto per l'etichetta selezionata:
    
    - Scegliere **Selezionare dall'elenco** per aggiungere tutti gli utenti dell'organizzazione o passare alla directory.
        
        Gli utenti o i gruppi selezionati devono disporre di un indirizzo di posta elettronica. Questa condizione si verifica quasi sempre in un ambiente di produzione, ma in un ambiente di test semplice può essere necessario aggiungere gli indirizzi di posta elettronica agli account utente o ai gruppi.
        
    - Scegliere **Immettere i dettagli** per specificare manualmente gli indirizzi di posta elettronica dei singoli utenti o gruppi (interni o esterni) o per specificare tutti gli utenti in un'altra organizzazione immettendo un nome di dominio di tale organizzazione. 
        
    >[!NOTE]
    >Se un indirizzo di posta elettronica viene modificato dopo che si è selezionato l'utente o il gruppo, vedere la sezione [Considerazioni in caso di modifica degli indirizzi di posta elettronica](../plan-design/prepare.md#considerations-for-azure-information-protection-if-email-addresses-change) della documentazione relativa alla pianificazione.
    
    Come procedura consigliata, usare gruppi anziché utenti. Questo strategia mantiene la configurazione più semplice e rende meno probabile la necessità di aggiornare la configurazione dell'etichetta in un secondo momento e quindi di proteggere nuovamente il contenuto. Tuttavia, se si apportano modifiche al gruppo, tenere presente che, per motivi di prestazioni, Azure Rights Management [memorizza nella cache l'appartenenza ai gruppi](../plan-design/prepare.md#group-membership-caching-by-azure-rights-management ). 
    
    Dopo avere specificato il primo set di utenti e gruppi, selezionare le autorizzazioni da concedere a tali utenti e gruppi. Per altre informazioni sulle autorizzazioni selezionabili, vedere [Configurazione dei diritti di utilizzo per Azure Rights Management](configure-usage-rights.md). Tuttavia, le applicazioni che supportano Rights Management possono implementare queste autorizzazioni in modo diverso. Consultare la relativa documentazione ed eseguire test personalizzati con le applicazioni usate dagli utenti per controllare il comportamento prima di distribuire il modello per gli utenti.
    
    Se necessario, è ora possibile aggiungere un secondo set di utenti e gruppi con diritti di utilizzo. Ripetere fino a quando non sono stati specificati tutti gli utenti e i gruppi con le rispettive autorizzazioni.

    >[!TIP]
    >Valutare l'opportunità di aggiungere l'autorizzazione personalizzata **Copia ed estrai contenuto** e concederla al personale o agli amministratori selezionati in altri ruoli responsabili del recupero di informazioni. Tali utenti possono rimuovere, se necessario, la protezione da file e messaggi di posta elettronica che verranno protetti mediante questo modello o etichetta. La possibilità di rimuovere la protezione a livello di autorizzazione per un documento o un messaggio di posta elettronica consente un controllo più accurato rispetto all'uso della [funzionalità dell'utente con privilegi avanzati](configure-super-users.md).
    
    Per tutti gli utenti e i gruppi specificati, nel pannello **Protezione** controllare se si desidera apportare modifiche alle seguenti impostazioni. Si noti che queste impostazioni, come le autorizzazioni, non si applicano all'[emittente di Rights Management e proprietario di Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner), o a qualsiasi [utente con privilegi avanzati](configure-super-users.md) che è stato assegnato.
    
    |Impostazioni|Altre informazioni|Impostazione consigliata
    |-----------|--------------------|--------------------|
    |**scadenza contenuto**|Definire una data o un numero di giorni in cui i documenti o i messaggi di posta elettronica protetti tramite il modello non devono essere aperti da alcuni utenti selezionati. È possibile specificare una data o un numero di giorni a partire dal momento in cui la protezione viene applicata ai contenuti.<br /><br />Quando si specifica una data, diventa effettiva alla mezzanotte del fuso orario corrente.|**Nessuna scadenza contenuto**, a meno che non esista un requisito temporale specifico per il contenuto.|
    |**Consenti l'accesso offline**|Usare questa impostazione per bilanciare i requisiti di sicurezza, compreso l'accesso dopo la revoca, con la possibilità per gli utenti selezionati di aprire il contenuto protetto quando non hanno una connessione Internet.<br /><br />Se si specifica che il contenuto non è disponibile senza una connessione Internet o che è disponibile solo per un determinato numero di giorni, al raggiungimento di tale soglia, gli utenti dovranno eseguire di nuovo l'autenticazione e l'accesso verrà registrato. In questo caso, se le credenziali non sono memorizzate nella cache, verrà chiesto agli utenti di eseguire l'accesso prima di poter aprire il documento o il messaggio di posta elettronica.<br /><br />Oltre alla riesecuzione dell'autenticazione, verrà nuovamente valutata l'appartenenza degli utenti ai criteri e ai gruppi. Questo significa che gli utenti potrebbero avere risultati di accesso diversi per lo stesso documento o messaggio di posta elettronica se dall'ultimo accesso ai contenuti si sono verificati cambiamenti relativi all'appartenenza ai criteri o ai gruppi. Ciò potrebbe includere anche l'impossibilità di accedere al documento se questo è stato [revocato](../rms-client/client-track-revoke.md).|A seconda della sensibilità del contenuto:<br /><br />- **Numero di giorni per cui il contenuto è disponibile senza una connessione a Internet** = **7** per i dati aziendali sensibili che potrebbero causare danni all'azienda in caso di condivisione con persone non autorizzate. Questa raccomandazione offre un equo compromesso tra sicurezza e flessibilità. Sono esempi di questo tipo di contenuto i contratti, i report sulla sicurezza, i riepiloghi previsionali e i dati sulle vendite.<br /><br />- **Mai** per dati aziendali particolarmente riservati che potrebbero causare danni all'azienda se condivisi con utenti non autorizzati. Questa indicazione assegna maggiore priorità alla sicurezza che alla flessibilità e garantisce che, se il documento viene revocato, per tutti gli utenti autorizzati sarà immediatamente impossibile aprirlo. Sono esempi di questo tipo di contenuto le informazioni su dipendenti e clienti, le password, il codice sorgente e i rendiconti finanziari preannunciati.|
    
    Al termine della configurazione delle autorizzazioni, fare clic su **OK**. 
    
    Questo raggruppamento di impostazioni consente di creare un modello personalizzato per il servizio Azure Rights Management. I modelli possono essere usati con applicazioni e servizi che si integrano con Azure Rights Management. Per informazioni sul download e l'aggiornamento dei modelli nei computer e nei servizi, vedere [Aggiornamento dei modelli per gli utenti](refresh-templates.md).

10. Se è stato selezionato **HYOK (AD RMS)**, selezionare **Imposta i dettagli del modello di AD RMS** o **Configura le autorizzazioni definite dall'utente (anteprima)** e specificare l'URL della licenza per il cluster AD RMS.
    
    Per istruzioni su come specificare un GUID di modello e l'URL della licenza, vedere [Individuazione delle informazioni per specificare la protezione di AD RMS con un'etichetta di Azure Information Protection](configure-adrms-restrictions.md#locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label).
    
    L'opzione per le autorizzazioni definite dall'utente consente agli utenti di specificare a chi vengono concesse autorizzazioni e quali sono queste autorizzazioni. È quindi possibile completare l'impostazione dell'opzione e scegliere solo Outlook (impostazione predefinita) oppure Word, Excel, PowerPoint e File Explorer. 
    
    Se si sceglie l'opzione per Outlook l'etichetta viene visualizzata in Outlook e il comportamento quando gli utenti applicano l'etichetta è uguale a quello generato dall'opzione Non inoltrare.
    
    Se si sceglie l'opzione per Word, Excel, PowerPoint e File Explorer l'etichetta viene visualizzata in queste applicazioni. Quando gli utenti applicano l'etichetta viene visualizzata la finestra di dialogo che consente loro di selezionare le autorizzazioni personalizzate. Nella finestra di dialogo gli utenti devono specificare gli utenti o i gruppi, le autorizzazioni e una data di scadenza. Verificare che gli utenti dispongano di istruzioni e linee guida per specificare questi valori. Si noti che se non si dispone della versione di anteprima del client, questa opzione per Esplora File usa sempre la protezione di Azure RMS anziché la protezione HYOK (AD RMS).

11. Fare clic su **OK** per chiudere il pannello **Protezione** e visualizzare la scelta **Definito dall'utente** o il modello selezionato per l'opzione **Protezione** nel pannello **Etichetta**.

12. Nel pannello **Etichetta** fare clic su **Salva**.

13. Nel pannello **Azure Information Protection** usare la colonna **Protezione** per confermare che l'etichetta ora visualizza l'impostazione di protezione desiderata:
    
    - Un segno di spunta se è stata configurata la protezione. 
    
    - Un segno x per indicare l'annullamento se è stata configurata un'etichetta per la rimozione della protezione.
    
    - Un campo vuoto se la protezione non è impostata. 

13. Per mettere le modifiche a disposizione degli utenti, fare clic su **Publish** (Pubblica).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla configurazione dei criteri di Azure Information Protection, usare i collegamenti nella sezione [Configurazione dei criteri dell'organizzazione](configure-policy.md#configuring-your-organizations-policy).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]