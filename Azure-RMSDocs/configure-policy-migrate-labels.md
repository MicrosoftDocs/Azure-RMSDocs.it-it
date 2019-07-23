---
title: Eseguire la migrazione delle etichette di Azure Information Protection a Office 365 - AIP
description: Eseguire la migrazione di etichette di Azure Information Protection a etichette di riservatezza di Office 365 per i client e i servizi che supportano le etichette unificate.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/19/2019
ms.topic: article
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: f1340d42c0f09733bf4517b4d573e75e5d88b68e
ms.sourcegitcommit: ae48f7cea01b4d615052659072305abb8698a7f7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2019
ms.locfileid: "68375416"
---
# <a name="how-to-migrate-azure-information-protection-labels-to-office-365-sensitivity-labels"></a>Come eseguire la migrazione di etichette di Azure Information Protection a etichette di riservatezza di Office 365

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
> *Istruzioni per: [Client Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Eseguire la migrazione delle etichette in Azure Information Protection in modo che sia possibile usarle come etichette di riservatezza dai [client e dai servizi che supportano l'assegnazione](#clients-and-services-that-support-unified-labeling)di etichette unificata.

Queste etichette possono quindi essere usate dal client di Azure Information Protection Unified labeling. Se si continua a usare il client di Azure Information Protection (versione classica), questo client continua a scaricare le etichette con i criteri di Azure Information Protection dal portale di Azure.

Prima di leggere le istruzioni per eseguire la migrazione delle etichette, è possibile trovare le seguenti domande frequenti utili:

- [Qual è la differenza tra le etichette in Azure Information Protection e in Office 365?](faqs.md#whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365)

- [Qual è il momento giusto per la migrazione delle etichette in Office 365?](faqs.md#when-is-the-right-time-to-migrate-my-labels-to-office-365)

- [Dopo la migrazione delle etichette, quale portale di gestione si usa?](faqs.md?#after-ive-migrated-my-labels-which-management-portal-do-i-use )

### <a name="administrative-roles-that-support-the-unified-labeling-platform"></a>Ruoli amministrativi che supportano la piattaforma di assegnazione di etichette unificata

Se si usano i ruoli di amministratore per l'amministrazione delegata nell'organizzazione, potrebbe essere necessario apportare alcune modifiche alla piattaforma di etichettatura unificata:

Il [ruolo Azure ad](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) di **Azure Information Protection Administrator** (in precedenza **Information Protection Administrator**) non è supportato dalla piattaforma Unified labeling. Se si utilizza questo ruolo amministrativo nell'organizzazione, aggiungere gli utenti che dispongono di questo ruolo ai ruoli Azure AD dell'amministratore della **conformità**, dell' **amministratore dei dati di conformità**o dell'amministratore della **sicurezza**. Se serve assistenza con questa procedura, vedere [Concedere agli utenti l'accesso al Centro sicurezza e conformità di Office 365](https://docs.microsoft.com/office365/securitycompliance/grant-access-to-the-security-and-compliance-center). È possibile assegnare questi ruoli anche nel portale di Azure AD, nel Centro sicurezza Microsoft 365 e nel Centro conformità Microsoft 365.

Come alternativa all'uso dei ruoli, nelle interfacce di amministrazione è possibile creare un nuovo gruppo di ruoli per questi utenti e aggiungere il ruolo **Sensitivity Label Administrator** (Amministratore etichette di riservatezza) o **Organization Configuration** (Configurazione organizzazione) a questo gruppo.

Se non si consente l'accesso ai centri di amministrazione a questi utenti usando una di queste configurazioni, gli utenti non potranno configurare Azure Information Protection nel portale di Azure dopo la migrazione delle etichette.

Gli amministratori globali per il tenant possono continuare a gestire le etichette e i criteri sia nel portale di Azure che nei centri di amministrazione dopo la migrazione delle etichette.

## <a name="before-you-begin"></a>Prima di iniziare

Poiché la migrazione delle etichette è irreversibile, assicurarsi di essere a conoscenza delle modifiche e delle considerazioni seguenti:

- Assicurarsi di disporre di [client che supportano le etichette unificate](#clients-and-services-that-support-unified-labeling) e, se necessario, di essere preparati per l'amministrazione in entrambi i portale di Azure (per i client che non supportano le etichette unificate) e i centri di amministrazione (per il client che supportano le etichette unificate).

- I criteri, incluse le impostazioni dei criteri e gli utenti autorizzati all'accesso (criteri con ambito) e tutte le impostazioni client avanzate non vengono sottoposti a migrazione. Le opzioni per la configurazione di queste impostazioni in seguito alla migrazione dell'etichetta includono:
    - Opzione [Copy Policies](#copy-your-policies-and-policy-settings) .
    - Centro di amministrazione per le etichette di riservatezza.
    - [Office 365 sicurezza e conformità PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/office-365-scc-powershell?view=exchange-ps), che è necessario usare per configurare [Impostazioni client avanzate](./rms-client/clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell).
    

- Non tutte le impostazioni di un'etichetta migrata sono supportate dai centri di amministrazione. Usare la tabella nella sezione [Impostazioni delle etichette non supportate nei centri di amministrazione](#label-settings-that-are-not-supported-in-the-admin-centers) per individuare queste impostazioni e le operazioni consigliate.

- Modelli di protezione:
    
    - Anche i modelli che usano una chiave basata sul cloud e fanno parte di una configurazione di etichetta vengono sottoposti a migrazione con l'etichetta. Gli altri modelli di protezione non vengono sottoposti a migrazione. 
    
    - Se sono presenti etichette configurate per un modello predefinito, modificare tali etichette e selezionare l'opzione **Imposta autorizzazioni** per configurare le stesse impostazioni di protezione che erano presenti nel modello. Le etichette con modelli predefiniti non bloccheranno la migrazione delle etichette, ma questa configurazione dell'etichetta non è supportata nei centri di amministrazione.
        
        Suggerimento: Per facilitare la riconfigurazione di queste etichette, può essere utile avere due finestre del browser: una finestra in cui selezionare il pulsante **Modifica modello** per l'etichetta in modo da visualizzare le impostazioni di protezione e l'altra per configurare le stesse impostazioni quando si seleziona **Imposta autorizzazioni**.
    
    - Dopo che è stata eseguita la migrazione di un'etichetta con impostazioni di protezione basate su cloud, l'ambito risultante del modello di protezione è l'ambito definito nel portale di Azure (oppure usando il modulo AIPService di PowerShell) e l'ambito definito nei centri di amministrazione. 

- Quando si esegue la migrazione delle etichette, i risultati della migrazione visualizzano se un'etichetta è stata **creata**, **aggiornata** o **rinominata** per motivi di duplicazione:

    - Dopo la creazione dell'etichetta, è necessario pubblicarla in uno dei centri di amministrazione per renderla disponibile ad applicazioni e servizi.
    
    - Quando un'etichetta viene rinominata, è necessario modificarla. L'operazione può essere eseguita in uno dei centri di amministrazione o nel portale di Azure.

- Per ogni etichetta il portale di Azure consente di visualizzare solo il nome visualizzato dell'etichetta, che è modificabile. Nei centri di amministrazione vengono mostrati sia il nome visualizzato per un'etichetta che il nome dell'etichetta. Il nome dell'etichetta è il nome iniziale specificato al momento della creazione dell'etichetta. Il servizio back-end usa questa proprietà per l'identificazione.

- Le eventuali stringhe localizzate per le etichette non vengono incluse nella migrazione. Definire nuove stringhe localizzate per le etichette migrate usando Office 365 Sicurezza e conformità PowerShell e il parametro *LocaleSettings* per [set-label](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps).

- Dopo la migrazione, quando si modifica un'etichetta migrata nel portale di Azure, la stessa modifica si riflette automaticamente nei centri di amministrazione. Tuttavia, quando si modifica un'etichetta migrata in uno dei centri di amministrazione, è necessario tornare al portale di Azure, nel pannello **Azure Information Protection - Etichettatura unificata**, e selezionare **Pubblica**. Questa azione aggiuntiva è necessaria per i client di Azure Information Protection (classico) per rilevare le modifiche apportate all'etichetta.

### <a name="label-settings-that-are-not-supported-in-the-admin-centers"></a>Impostazioni delle etichette non supportate nei centri di amministrazione

Usare la tabella seguente per identificare le impostazioni di configurazione di un'etichetta migrata non supportate dal Centro sicurezza e conformità di Office 365, dal Centro sicurezza Microsoft 365 o dal Centro conformità Microsoft 365. Se sono presenti etichette con queste impostazioni, al termine della migrazione, usare le linee guida per l'amministrazione nella colonna finale prima di pubblicare le etichette in uno dei centri di amministrazione a cui si fa riferimento.

In caso di dubbi sulla configurazione delle etichette, visualizzare le relative impostazioni nel portale di Azure. Se serve assistenza con questa procedura, vedere [Configurazione dei criteri di Azure Information Protection](configure-policy.md).

Azure Information Protection client (versione classica) possono usare tutte le impostazioni di etichetta elencate senza problemi perché continuano a scaricare le etichette dal portale di Azure.

|Configurazione dell'etichetta|Supportata dai client di etichettatura unificata| Linee guida per i centri di amministrazione|
|-------------------|---------------------------------------------|-------------------------|
|Stato abilitato o disabilitato<br /><br />Questo stato non è sincronizzato con i centri di amministrazione |Non applicabile|Equivale a se l'etichetta è pubblicata o no. |
|Colore dell'etichetta selezionato dall'elenco o specificato con il codice RGB |Sì|Nessuna opzione di configurazione per i colori dell'etichetta. È invece possibile configurare i colori delle etichette nell'portale di Azure o usare [PowerShell](./rms-client/clientv2-admin-guide-customizations.md#specify-a-color-for-the-label).|
|Protezione basata sul cloud o protezione basata su HYOK usando un modello predefinito |No|Nessuna opzione di configurazione per i modelli predefiniti. Non è consigliabile pubblicare un'etichetta con questa configurazione.|
|Protezione basata sul cloud che usa autorizzazioni definite dall'utente in Word, Excel e PowerPoint |Yes|I centri di amministrazione non hanno un'opzione di configurazione per le autorizzazioni definite dall'utente per queste app di Office. Tuttavia, questa impostazione è supportata se si esegue la migrazione di un'etichetta con questa configurazione oppure si configura l'etichetta dopo la migrazione utilizzando il portale di Azure. <br /><br /> Se si pubblica un'etichetta con questa configurazione, verificare i risultati dell'applicazione dell'etichetta nella [tabella seguente](#comparing-the-behavior-of-protection-settings-for-a-label).|
|Protezione basata su HYOK che usa autorizzazioni definite dall'utente per Outlook (Non inoltrare) |No|Nessuna opzione di configurazione per HYOK. Non è consigliabile pubblicare un'etichetta con questa configurazione. In caso contrario i risultati ottenuti applicando l'etichetta sono elencati nella [tabella seguente](#comparing-the-behavior-of-protection-settings-for-a-label).|
|Rimuovere la protezione |No|Nessuna opzione di configurazione per rimuovere la protezione. Non è consigliabile pubblicare un'etichetta con questa configurazione.<br /><br /> Se si pubblica un'etichetta con questa configurazione, quando viene applicata, la protezione verrà rimossa se è stata precedentemente applicata da un'etichetta. La protezione verrà mantenuta se in precedenza era stata applicata in modo indipendente da un'etichetta.|
|Tipi di carattere personalizzato e colore del tipo di carattere personalizzato tramite RGB per i contrassegni visivi (intestazione, piè di pagina, filigrana)|Yes|La configurazione per i contrassegni visivi è limitata a un elenco di colori e dimensioni dei caratteri. È possibile pubblicare questa etichetta senza modifiche benché non sia possibile visualizzare i valori configurati nei centri di amministrazione. <br /><br />Per modificare queste opzioni è possibile usare il portale di Azure. Per semplificare l'amministrazione, tuttavia, provare a cambiare il colore impostando una delle opzioni elencate nei centri di amministrazione.|
|Variabili nei contrassegni visivi (intestazione, piè di pagina, filigrana)|No|Se si pubblica questa etichetta senza modifiche, le variabili vengono visualizzate come testo nei client anziché visualizzare i valori dinamici. Prima di pubblicare l'etichetta, modificare le stringhe per rimuovere le variabili.|
|Contrassegni visivi per app|No|Se si pubblica questa etichetta senza modifiche, le variabili delle app vengono visualizzate come testo nei client in tutte le app anziché visualizzare le stringhe di testo in app selezionate. Pubblicare questa etichetta solo se è adatta per tutte le app e modificare le stringhe per rimuovere le variabili delle app.|
|Condizioni e impostazioni associate <br /><br /> include l'assegnazione di etichette automatica e consigliata e le descrizioni comando corrispondenti|Non applicabile|Riconfigurare le condizioni tramite l'applicazione automatica di etichette come configurazione separata dalle impostazioni dell'etichetta.|

### <a name="comparing-the-behavior-of-protection-settings-for-a-label"></a>Confronto del comportamento delle impostazioni di protezione per un'etichetta

Usare la tabella seguente per identificare in modo diverso la stessa impostazione di protezione per un'etichetta, a seconda che venga usata dal client di Azure Information Protection (classico), dal client di Azure Information Protection Unified Labeling o dalle app di Office con l'etichetta incorporata (nota anche come "Native Office labeling"). Le differenze nel comportamento delle etichette potrebbero modificare la decisione di pubblicare le etichette, specialmente quando si dispone di una combinazione di client nell'organizzazione.

In caso di dubbi sulla configurazione delle impostazioni di protezione, visualizzare le relative impostazioni nel pannello **Protezione** nel portale di Azure. Se serve assistenza con questa procedura, vedere [Per configurare un'etichetta per le impostazioni di protezione](configure-policy-protection.md#to-configure-a-label-for-protection-settings).

Le impostazioni di protezione con lo stesso comportamento non sono elencate nella tabella, con le eccezioni seguenti:
- Quando si usano le app di Office con l'etichettatura incorporata, le etichette non sono visibili in Esplora file a meno che non si installi anche il client di etichettatura unificata di Azure Information Protection.
- Quando si usano le app di Office con l'etichettatura incorporata, la protezione viene mantenuta se in precedenza era stata applicata in modo indipendente da un'etichetta [[1]](#footnote-1).

|Impostazione di protezione per un'etichetta |Client di Azure Information Protection (versione classica) |Client per l'etichettatura unificata di Azure Information Protection| App di Office con etichettatura incorporata
|-------------------|-----------------------------------|-----------------------------------------------------------|---------------
|Azure (chiave cloud) con autorizzazioni definite dall'utente per Word, Excel, PowerPoint ed Esplora file:| Visibile in Word, Excel, PowerPoint ed Esplora file <br /><br /> Quando viene applicata l'etichetta:<br /><br /> - Agli utenti vengono richieste le autorizzazioni personalizzate che vengono quindi applicate come protezione tramite una chiave basata su cloud| Visibile in Word, Excel, PowerPoint ed Esplora file <br /><br /> Quando viene applicata l'etichetta:<br /><br /> - Agli utenti vengono richieste le autorizzazioni personalizzate che vengono quindi applicate come protezione tramite una chiave basata su cloud|Visibile in Word, Excel, PowerPoint e Outlook: <br /><br /> Quando viene applicata l'etichetta:<br /><br /> - Agli utenti non vengono richieste le autorizzazioni personalizzate e non viene applicata alcuna protezione <br /><br /> - La protezione viene mantenuta se in precedenza era stata applicata in modo indipendente da un'etichetta [[1]](#footnote-1)|
|HYOK (AD RMS) con un modello:| Visibile in Word, Excel, PowerPoint, Outlook ed Esplora file<br /><br /> Quando viene applicata questa etichetta: <br /><br />- La protezione HYOK viene applicata a documenti e messaggi di posta elettronica | Visibile in Word, Excel, PowerPoint, Outlook ed Esplora file  <br /><br /> Quando viene applicata questa etichetta: <br /><br />- Non viene applicata alcuna protezione e la protezione viene rimossa [[2]](#footnote-2) se in precedenza era stata applicata da un'etichetta <br /><br />- La protezione viene mantenuta se in precedenza era stata applicata in modo indipendente da un'etichetta |Visibile in Word, Excel, PowerPoint e Outlook <br /><br /> Quando viene applicata questa etichetta: <br /><br />- Non viene applicata alcuna protezione e la protezione viene rimossa [[2]](#footnote-2) se in precedenza era stata applicata da un'etichetta <br /><br />- La protezione viene mantenuta se in precedenza era stata applicata in modo indipendente da un'etichetta [[1]](#footnote-1) |
|HYOK (AD RMS) con autorizzazioni definite dall'utente per Word, Excel, PowerPoint ed Esplora file:| Visibile in Word, Excel, PowerPoint ed Esplora file<br /><br /> Quando viene applicata questa etichetta:<br /><br /> - La protezione HYOK viene applicata a documenti e messaggi di posta elettronica| Visibile in Word, Excel e PowerPoint <br /><br /> Quando viene applicata questa etichetta: <br /><br />- La protezione non viene applicata e viene rimossa [[2]](#footnote-2) se in precedenza era stata applicata da un'etichetta <br /><br />- La protezione viene mantenuta se in precedenza era stata applicata in modo indipendente da un'etichetta|Visibile in Word, Excel e PowerPoint <br /><br /> Quando viene applicata questa etichetta: <br /><br />- La protezione non viene applicata e viene rimossa [[2]](#footnote-2) se in precedenza era stata applicata da un'etichetta <br /><br />- La protezione viene mantenuta se in precedenza era stata applicata in modo indipendente da un'etichetta |
|HYOK (AD RMS) con autorizzazioni definite dall'utente per Outlook:|Visibile in Outlook<br /><br />Quando viene applicata questa etichetta:<br /><br />- Ai messaggi di posta elettronica viene applicato Non inoltrare con la protezione HYOK|Visibile in Outlook<br /><br />Quando viene applicata questa etichetta:<br /><br /> - La protezione non viene applicata e viene rimossa [[2]](#footnote-2) se in precedenza era stata applicata da un'etichetta <br /><br />- La protezione viene mantenuta se in precedenza era stata applicata in modo indipendente da un'etichetta|Visibile in Outlook<br /><br />Quando viene applicata questa etichetta:<br /><br />- La protezione non viene applicata e viene rimossa [[2]](#footnote-2) se in precedenza era stata applicata da un'etichetta <br /><br />- La protezione viene mantenuta se in precedenza era stata applicata in modo indipendente da un'etichetta [[1]](#footnote-1)|

###### <a name="footnote-1"></a>Nota 1

In Outlook per Mac, la protezione viene mantenuta con una sola eccezione: Quando un messaggio di posta elettronica è stato protetto con l'opzione Solo crittografia, la protezione viene rimossa.


###### <a name="footnote-2"></a>Nota 2

La protezione viene rimossa se l'utente ha un diritto di utilizzo o ruolo che supporta questa azione:
- Il [diritto di utilizzo](configure-usage-rights.md#usage-rights-and-descriptions) Esporta o Controllo completo.
- Il ruolo di [emittente di Rights Management o proprietario di Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner) oppure di [utente con privilegi avanzati](configure-super-users.md).

Se l'utente non ha uno di questi diritti di utilizzo o ruoli, l'etichetta non viene applicata e viene mantenuta la protezione originale.


## <a name="to-migrate-azure-information-protection-labels"></a>Per eseguire la migrazione delle etichette di Azure Information Protection

Usare le istruzioni seguenti per eseguire la migrazione del tenant e delle etichette di Azure Information Protection per usare il nuovo archivio di etichettatura unificata.

Per eseguire la migrazione delle etichette, è necessario essere un amministratore di conformità, un amministratore dei dati di conformità, un amministratore della sicurezza o un amministratore globale.

> [!NOTE]
> Se sono presenti etichette di conservazione o criteri di prevenzione della perdita dei dati per Office 365, è consigliabile avere il ruolo di **amministratore della conformità** , il ruolo di **amministratore dei dati di conformità** o il ruolo di **amministratore globale** per eseguire la migrazione delle etichette.
> 
> Gli amministratori della sicurezza non hanno accesso alle etichette di conservazione o ai criteri di prevenzione della perdita dei dati, pertanto se si dispone di uno di questi e hanno lo stesso nome delle etichette di Azure Information Protection, il processo di migrazione non può essere completato fino a quando non si rinomina manualmente uno dei duplicati. Tuttavia, se si dispone di uno degli altri ruoli, il processo di migrazione può rinominare l'etichetta di Azure Information Protection, in modo che la migrazione possa essere completata.

1. Se non è già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Quindi passare al pannello **Azure Information Protection**.
    
    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Dall'opzione  di menu Gestisci selezionare **etichetta unificata**.

3. Nel pannello **Azure Information Protection - Etichettatura unificata** selezionare **Attiva** e seguire le istruzioni online.
    
    Se l'opzione di attivazione non è disponibile, controllare l'impostazione di **Stato dell'etichettatura unificata**: se è **Attivato**, il tenant usa già l'archivio di etichette unificate e non è necessario eseguire la migrazione delle etichette.

Le etichette di cui è stata eseguita correttamente la migrazione possono ora essere usate dai [client e servizi che supportano l'etichettatura unificata](#clients-and-services-that-support-unified-labeling). Tuttavia, è prima necessario pubblicare queste etichette in uno dei centri di amministrazione: Centro sicurezza e conformità di Office 365, Centro sicurezza di Microsoft 365 o Centro conformità di Microsoft 365.

> [!IMPORTANT]
> Se si modificano le etichette al di fuori dell'portale di Azure, per Azure Information Protection client (versione classica) tornare a questo pannello **Azure Information Protection-Unified Labeling** e selezionare **pubblica**.


#### <a name="copy-your-policies-and-policy-settings"></a>Copiare i criteri e le impostazioni dei criteri

Questa opzione viene gradualmente implementata in tenant in anteprima ed è soggetta a modifiche. Se non viene visualizzata l'opzione **copia criteri (anteprima)** , riprovare tra qualche settimana.

Dopo aver eseguito la migrazione delle etichette, è possibile selezionare un'opzione per la copia dei criteri. Se si seleziona questa opzione, viene inviata una copia monouso dei criteri con le [impostazioni dei criteri](configure-policy-settings.md) e tutte [le impostazioni client avanzate](./rms-client/client-admin-guide-customizations.md#available-advanced-client-settings) all'interfaccia di amministrazione in cui si gestiscono le etichette: Centro sicurezza e conformità di Office 365, Centro sicurezza di Microsoft 365 o Centro conformità di Microsoft 365.

Prima di selezionare l'opzione **copia criteri (anteprima)** , tenere presente quanto segue:

- Non è possibile scegliere in modo selettivo i criteri e le impostazioni da copiare. Vengono copiati tutti i criteri (i criteri **globali** e tutti i criteri con ambito) e vengono copiate tutte le impostazioni supportate come impostazioni dei criteri di etichetta. Se si dispone già di un criterio etichetta con lo stesso nome, verrà sovrascritto con le impostazioni dei criteri nel portale di Azure.

- Alcune impostazioni client avanzate non vengono copiate perché per il client Azure Information Protection Unified Labeling sono supportate come *Impostazioni avanzate dell'etichetta* anziché come impostazioni dei criteri. È possibile configurare queste impostazioni avanzate di etichetta con [Office 365 Centro sicurezza e conformità PowerShell](./rms-client/clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell). Le impostazioni client avanzate che non vengono copiate includono:
    - [LabelbyCustomProperty](./rms-client/client-admin-guide-customizations.md#migrate-labels-from-secure-islands-and-other-labeling-solutions)
    - [LabelToSMIME](./rms-client/client-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)

- A differenza della migrazione delle etichette in cui vengono sincronizzate le successive modifiche alle etichette, l'azione copia criteri non sincronizza le modifiche successive ai criteri o alle impostazioni dei criteri. È possibile ripetere l'azione di copia dei criteri dopo aver apportato modifiche all'portale di Azure e tutti i criteri esistenti e le relative impostazioni verranno sovrascritti. In alternativa, usare i cmdlet [set-LabelPolicy](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-labelpolicy?view=exchange-ps) o [set-label](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps) con il parametro *AdvancedSettings* di Office 365 Centro sicurezza e conformità PowerShell.

Per ulteriori informazioni sulla configurazione delle impostazioni dei criteri, delle impostazioni client avanzate e delle impostazioni delle etichette per il client Azure Information Protection Unified Labeling, vedere [configurazioni personalizzate per il client di Azure Information Protection Unified Labeling ](./rms-client/clientv2-admin-guide-customizations.md)dalla guida dell'amministratore.

### <a name="clients-and-services-that-support-unified-labeling"></a>Client e servizi che supportano l'etichettatura unificata

Per verificare se i client e i servizi usati dall'utente supportano l'etichettatura unificata, fare riferimento alla relativa documentazione per verificare che sia possibile usare le etichette di riservatezza pubblicate da uno dei centri di amministrazione: Centro sicurezza e conformità di Office 365, Centro sicurezza di Microsoft 365 o Centro conformità di Microsoft 365. 

##### <a name="clients-that-currently-support-unified-labeling-include"></a>I client che attualmente supportano l'etichettatura unificata includono:

- Il [Azure Information Protection client di etichetta unificato per Windows](./rms-client/unifiedlabelingclient-version-release-history.md). Per un confronto tra il client e il client Azure Information Protection (classico), vedere [confrontare i](./rms-client/use-client.md#compare-the-clients)client.

- App di Office che sono in fasi di disponibilità diverse. Per altre informazioni, vedere la sezione **Oggi dov'è disponibile questa funzionalità?** in [Applicare le etichette di riservatezza per i documenti e la posta elettronica in Office](https://support.office.com/en-us/article/apply-sensitivity-labels-to-your-documents-and-email-within-office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9) nella documentazione di Office.
    
- App da fornitori e sviluppatori di software che usano [Microsoft Information Protection SDK](https://docs.microsoft.com/en-us/information-protection/develop/overview).

##### <a name="services-that-currently-support-unified-labeling-include"></a>I servizi che attualmente supportano l'etichettatura unificata includono:

- Microsoft Defender Advanced Threat Protection

- Microsoft Cloud App Security
    
    Questo servizio supporta le etichette sia prima che dopo la migrazione all'archivio di etichettatura unificata secondo la logica seguente:
    
    - Se i centri di amministrazione hanno le stesse etichette di quelle disponibili nel portale di Azure: le etichette unificate vengono recuperate dai centri di amministrazione. Per selezionare tali etichette in Cloud App Security, è necessario pubblicare almeno un'etichetta in almeno un utente.
    
    - Se i centri di amministrazione non hanno le stesse etichette di quelle disponibili nel portale di Azure: le etichette unificate non vengono usate dai centri di amministrazione, ma vengono recuperate dal portale di Azure.

- Servizi da fornitori e sviluppatori di software che usano [Microsoft Information Protection SDK](https://docs.microsoft.com/en-us/information-protection/develop/overview).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle etichette migrate che possono ora essere configurate e pubblicate in uno dei centri di amministrazione, vedere [Panoramica delle etichette di riservatezza](/Office365/SecurityCompliance/sensitivity-labels).

Se non è già stato fatto, installare il client di Azure Information Protection Unified labeling. Per informazioni sulla versione, una guida dell'amministratore e un manuale dell'utente, vedere [Azure Information Protection Unified Labeling client for Windows](./rms-client/aip-clientv2.md).
