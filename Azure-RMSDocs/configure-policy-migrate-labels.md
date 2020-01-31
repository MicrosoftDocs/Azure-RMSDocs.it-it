---
title: Eseguire la migrazione di Azure Information Protection labels a Unified Sensitivity labels-AIP
description: Eseguire la migrazione di Azure Information Protection etichette a etichette di riservatezza unificata per i client e i servizi che supportano Microsoft Information Protection Framework.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/26/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: labelmigrate
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: a62fbe465eda5dec253da938878f343bb00b8173
ms.sourcegitcommit: 200c710a675180cc0488defff299f2cc3c66922f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/29/2020
ms.locfileid: "76812586"
---
# <a name="how-to-migrate-azure-information-protection-labels-to-unified-sensitivity-labels"></a>Come eseguire la migrazione di etichette di Azure Information Protection a etichette di riservatezza unificate

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
> *Istruzioni per: [client di Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*


Eseguire la migrazione di Azure Information Protection etichette alla piattaforma di etichettatura unificata in modo da poterle usare come etichette di riservatezza da parte dei [client e dei servizi che supportano l'assegnazione di etichette unificata](#clients-and-services-that-support-unified-labeling).

> [!NOTE]
> Se il Azure Information Protection sottoscrizione è piuttosto nuovo, potrebbe non essere necessario eseguire la migrazione delle etichette perché il tenant si trova già nella piattaforma di etichettatura unificata. Per ulteriori informazioni, vedere [come è possibile determinare se il tenant si trova nella piattaforma di etichettatura unificata?](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)

Dopo aver eseguito la migrazione delle etichette, non verrà visualizzata alcuna differenza con il client di Azure Information Protection (classico) perché il client continua a scaricare le etichette con i criteri di Azure Information Protection dal portale di Azure. Tuttavia, è ora possibile usare le etichette con la Azure Information Protection client di etichetta unificata e altri client e servizi che usano le etichette di riservatezza.

Prima di leggere le istruzioni per eseguire la migrazione delle etichette, è possibile trovare le seguenti domande frequenti utili:

- [Qual è la differenza tra le etichette in Azure Information Protection e in Office 365?](faqs.md#whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365)

- [Quando è il momento giusto per eseguire la migrazione delle etichette?](faqs.md#when-is-the-right-time-to-migrate-my-labels)

- [Dopo la migrazione delle etichette, quale portale di gestione si usa?](faqs.md?#after-ive-migrated-my-labels-which-management-portal-do-i-use )

### <a name="administrative-roles-that-support-the-unified-labeling-platform"></a>Ruoli amministrativi che supportano la piattaforma di assegnazione di etichette unificata

Se si usano i ruoli di amministratore per l'amministrazione delegata nell'organizzazione, potrebbe essere necessario apportare alcune modifiche alla piattaforma di etichettatura unificata:

Il [ruolo Azure ad](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) di **Azure Information Protection Administrator** (in precedenza **Information Protection Administrator**) non è supportato dalla piattaforma Unified labeling. Se si utilizza questo ruolo amministrativo nell'organizzazione per gestire Azure Information Protection, aggiungere gli utenti che dispongono di questo ruolo ai ruoli Azure AD dell' **amministratore della conformità**, dell' **amministratore dati di conformità**o dell'amministratore della **sicurezza**. Se serve assistenza con questa procedura, vedere [Concedere agli utenti l'accesso al Centro sicurezza e conformità di Office 365](https://docs.microsoft.com/microsoft-365/security/office-365-security/grant-access-to-the-security-and-compliance-center). È possibile assegnare questi ruoli anche nel portale di Azure AD, nel Centro sicurezza Microsoft 365 e nel Centro conformità Microsoft 365.

Come alternativa all'uso dei ruoli, nelle interfacce di amministrazione è possibile creare un nuovo gruppo di ruoli per questi utenti e aggiungere il ruolo **Sensitivity Label Administrator** (Amministratore etichette di riservatezza) o **Organization Configuration** (Configurazione organizzazione) a questo gruppo.

Se non si consente l'accesso ai centri di amministrazione a questi utenti usando una di queste configurazioni, gli utenti non potranno configurare Azure Information Protection nel portale di Azure dopo la migrazione delle etichette.

Gli amministratori globali per il tenant possono continuare a gestire le etichette e i criteri sia nel portale di Azure che nei centri di amministrazione dopo la migrazione delle etichette.

## <a name="before-you-begin"></a>Prima di iniziare

La migrazione delle etichette presenta molti vantaggi, ma è irreversibile, quindi è necessario essere consapevoli delle modifiche e delle considerazioni seguenti:

- Assicurarsi di disporre di [client che supportano le etichette unificate](#clients-and-services-that-support-unified-labeling) e, se necessario, di essere preparati per l'amministrazione in entrambi i portale di Azure (per i client che non supportano le etichette unificate) e i centri di amministrazione (per il client che supportano le etichette unificate).

- I criteri, incluse le impostazioni dei criteri e gli utenti autorizzati all'accesso (criteri con ambito) e tutte le impostazioni client avanzate non vengono sottoposti a migrazione. Le opzioni per la configurazione di queste impostazioni in seguito alla migrazione dell'etichetta includono:
    - Centro di amministrazione per le etichette di riservatezza.
    - [Office 365 sicurezza e conformità PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/office-365-scc-powershell?view=exchange-ps), che è necessario usare per configurare [Impostazioni client avanzate](./rms-client/clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell).
    

- Non tutte le impostazioni di un'etichetta migrata sono supportate dai centri di amministrazione. Usare la tabella nella sezione [Impostazioni delle etichette non supportate nei centri di amministrazione](#label-settings-that-are-not-supported-in-the-admin-centers) per individuare queste impostazioni e le operazioni consigliate.

- Modelli di protezione:
    
    - Anche i modelli che usano una chiave basata sul cloud e fanno parte di una configurazione di etichetta vengono sottoposti a migrazione con l'etichetta. Gli altri modelli di protezione non vengono sottoposti a migrazione. 
    
    - Se sono presenti etichette configurate per un modello predefinito, modificare tali etichette e selezionare l'opzione **Imposta autorizzazioni** per configurare le stesse impostazioni di protezione che erano presenti nel modello. Le etichette con modelli predefiniti non bloccheranno la migrazione delle etichette, ma questa configurazione dell'etichetta non è supportata nei centri di amministrazione.
        
        Suggerimento: per riconfigurare queste etichette, potrebbe risultare utile disporre di due finestre del browser: una finestra in cui è possibile selezionare il pulsante **modifica modello** per l'etichetta per visualizzare le impostazioni di protezione e l'altra finestra per configurare le stesse impostazioni quando si seleziona **Imposta autorizzazioni**.
    
    - Dopo che è stata eseguita la migrazione di un'etichetta con impostazioni di protezione basate su cloud, l'ambito risultante del modello di protezione è l'ambito definito nel portale di Azure (oppure usando il modulo AIPService di PowerShell) e l'ambito definito nei centri di amministrazione. 

- Per ogni etichetta il portale di Azure consente di visualizzare solo il nome visualizzato dell'etichetta, che è modificabile. Gli utenti visualizzano questo nome di etichetta nelle app. Nei centri di amministrazione vengono mostrati sia il nome visualizzato per un'etichetta che il nome dell'etichetta. Il nome dell'etichetta è il nome iniziale specificato quando l'etichetta viene creata per la prima volta e questa proprietà viene usata dal servizio back-end per scopi di identificazione. Quando si esegue la migrazione delle etichette, il nome visualizzato rimane invariato e il nome dell'etichetta viene rinominato nell'ID etichetta della portale di Azure.

- Le eventuali stringhe localizzate per le etichette non vengono incluse nella migrazione. Definire nuove stringhe localizzate per le etichette migrate usando Office 365 Sicurezza e conformità PowerShell e il parametro *LocaleSettings* per [set-label](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps).

- Dopo la migrazione, quando si modifica un'etichetta migrata nel portale di Azure, la stessa modifica si riflette automaticamente nei centri di amministrazione. Tuttavia, quando si modifica un'etichetta migrata in uno dei centri di amministrazione, è necessario tornare al riquadro portale di Azure, **Azure Information Protection-Unified Labeling** e selezionare **pubblica**. Questa azione aggiuntiva è necessaria per i client di Azure Information Protection (classico) per rilevare le modifiche apportate all'etichetta.

### <a name="label-settings-that-are-not-supported-in-the-admin-centers"></a>Impostazioni delle etichette non supportate nei centri di amministrazione

Usare la tabella seguente per identificare le impostazioni di configurazione di un'etichetta migrata non supportate dal Centro sicurezza e conformità di Office 365, dal Centro sicurezza Microsoft 365 o dal Centro conformità Microsoft 365. Se sono presenti etichette con queste impostazioni, al termine della migrazione, usare le linee guida per l'amministrazione nella colonna finale prima di pubblicare le etichette in uno dei centri di amministrazione a cui si fa riferimento.

In caso di dubbi sulla configurazione delle etichette, visualizzare le relative impostazioni nel portale di Azure. Se serve assistenza con questa procedura, vedere [Configurazione dei criteri di Azure Information Protection](configure-policy.md).

Azure Information Protection client (versione classica) possono usare tutte le impostazioni di etichetta elencate senza problemi perché continuano a scaricare le etichette dal portale di Azure.

|Configurazione dell'etichetta|Supportata dai client di etichettatura unificata| Linee guida per i centri di amministrazione|
|-------------------|---------------------------------------------|-------------------------|
|Stato abilitato o disabilitato<br /><br />Questo stato non è sincronizzato con i centri di amministrazione |Not applicable|Equivale a se l'etichetta è pubblicata o no. |
|Colore dell'etichetta selezionato dall'elenco o specificato con il codice RGB |sì|Nessuna opzione di configurazione per i colori dell'etichetta. È invece possibile configurare i colori delle etichette nell'portale di Azure o usare [PowerShell](./rms-client/clientv2-admin-guide-customizations.md#specify-a-color-for-the-label).|
|Protezione basata sul cloud o protezione basata su HYOK usando un modello predefinito |No|Nessuna opzione di configurazione per i modelli predefiniti. Non è consigliabile pubblicare un'etichetta con questa configurazione.|
|Protezione basata sul cloud che usa autorizzazioni definite dall'utente in Word, Excel e PowerPoint |sì|I centri di amministrazione dispongono ora di un'opzione di configurazione per le autorizzazioni definite dall'utente. <br /><br /> Se si pubblica un'etichetta con questa configurazione, verificare i risultati dell'applicazione dell'etichetta nella [tabella seguente](#comparing-the-behavior-of-protection-settings-for-a-label).|
|Protezione basata su HYOK che usa autorizzazioni definite dall'utente per Outlook (Non inoltrare) |No|Nessuna opzione di configurazione per HYOK. Non è consigliabile pubblicare un'etichetta con questa configurazione. In caso contrario i risultati ottenuti applicando l'etichetta sono elencati nella [tabella seguente](#comparing-the-behavior-of-protection-settings-for-a-label).|
|Rimuovere la protezione |No|Nessuna opzione di configurazione per rimuovere la protezione. Non è consigliabile pubblicare un'etichetta con questa configurazione.<br /><br /> Se si pubblica un'etichetta con questa configurazione, quando viene applicata, la protezione viene sempre rimossa, indipendentemente dal fatto che la protezione sia stata precedentemente applicata da un'etichetta o da un'etichetta.|
|Qualsiasi impostazione di protezione utente autenticata |sì|Nessuna opzione di configurazione per selezionare questa impostazione di protezione. Pubblicare un'etichetta con questa configurazione quando è stata eseguita la migrazione di questa impostazione o configurarla nel portale di Azure.|
|Tipi di carattere personalizzato e colore del tipo di carattere personalizzato tramite RGB per i contrassegni visivi (intestazione, piè di pagina, filigrana)|sì|La configurazione per i contrassegni visivi è limitata a un elenco di colori e dimensioni dei caratteri. È possibile pubblicare questa etichetta senza modifiche benché non sia possibile visualizzare i valori configurati nei centri di amministrazione. <br /><br />Per modificare queste opzioni è possibile usare il portale di Azure. Per semplificare l'amministrazione, tuttavia, provare a cambiare il colore impostando una delle opzioni elencate nei centri di amministrazione.|
|Variabili nei contrassegni visivi (intestazione, piè di pagina, filigrana)|No|Se si pubblica questa etichetta senza modifiche, le variabili vengono visualizzate come testo nei client anziché visualizzare i valori dinamici. Prima di pubblicare l'etichetta, modificare le stringhe per rimuovere le variabili.|
|Contrassegni visivi per app|No|Se si pubblica questa etichetta senza modifiche, le variabili delle app vengono visualizzate come testo nei client in tutte le app anziché visualizzare le stringhe di testo in app selezionate. Pubblicare questa etichetta solo se è adatta per tutte le app e modificare le stringhe per rimuovere le variabili delle app.|
|Condizioni e impostazioni associate <br /><br /> include l'assegnazione di etichette automatica e consigliata e le descrizioni comando corrispondenti|Not applicable|Riconfigurare le condizioni tramite l'applicazione automatica di etichette come configurazione separata dalle impostazioni dell'etichetta.|

### <a name="comparing-the-behavior-of-protection-settings-for-a-label"></a>Confronto del comportamento delle impostazioni di protezione per un'etichetta

Usare la tabella seguente per identificare in modo diverso la stessa impostazione di protezione per un'etichetta, a seconda che venga usata dal client di Azure Information Protection (classico), dal client di Azure Information Protection Unified Labeling o dalle app di Office con l'etichetta incorporata (nota anche come "Native Office labeling"). Le differenze nel comportamento delle etichette potrebbero modificare la decisione di pubblicare le etichette, specialmente quando si dispone di una combinazione di client nell'organizzazione.

Se non si è certi del modo in cui vengono configurate le impostazioni di protezione, visualizzare le impostazioni nel riquadro **protezione** , nella portale di Azure. Se serve assistenza con questa procedura, vedere [Per configurare un'etichetta per le impostazioni di protezione](configure-policy-protection.md#to-configure-a-label-for-protection-settings).

Le impostazioni di protezione con lo stesso comportamento non sono elencate nella tabella, con le eccezioni seguenti:
- Quando si usano le app di Office con l'etichettatura incorporata, le etichette non sono visibili in Esplora file a meno che non si installi anche il client di etichettatura unificata di Azure Information Protection.
- Quando si usano le app di Office con l'etichettatura incorporata, la protezione viene mantenuta se in precedenza era stata applicata in modo indipendente da un'etichetta [[1]](#footnote-1).

|Impostazione di protezione per un'etichetta |Client Azure Information Protection (classico) |Client per l'etichettatura unificata di Azure Information Protection| App di Office con etichettatura incorporata
|-------------------|-----------------------------------|-----------------------------------------------------------|---------------
|Azure (chiave cloud) con autorizzazioni definite dall'utente per Word, Excel, PowerPoint ed Esplora file:| Visibile in Word, Excel, PowerPoint ed Esplora file <br /><br /> Quando viene applicata l'etichetta:<br /><br /> - Agli utenti vengono richieste le autorizzazioni personalizzate che vengono quindi applicate come protezione tramite una chiave basata su cloud| Visibile in Word, Excel, PowerPoint ed Esplora file <br /><br /> Quando viene applicata l'etichetta:<br /><br /> - Agli utenti vengono richieste le autorizzazioni personalizzate che vengono quindi applicate come protezione tramite una chiave basata su cloud|Visibile in Word, Excel, PowerPoint e Outlook: <br /><br /> Quando viene applicata l'etichetta:<br /><br /> - Agli utenti non vengono richieste le autorizzazioni personalizzate e non viene applicata alcuna protezione <br /><br /> - La protezione viene mantenuta se in precedenza era stata applicata in modo indipendente da un'etichetta [[1]](#footnote-1)|
|HYOK (AD RMS) con un modello:| Visibile in Word, Excel, PowerPoint, Outlook ed Esplora file<br /><br /> Quando viene applicata questa etichetta: <br /><br />- La protezione HYOK viene applicata a documenti e messaggi di posta elettronica | Visibile in Word, Excel, PowerPoint, Outlook ed Esplora file  <br /><br /> Quando viene applicata questa etichetta: <br /><br />- Non viene applicata alcuna protezione e la protezione viene rimossa [[2]](#footnote-2) se in precedenza era stata applicata da un'etichetta <br /><br />- La protezione viene mantenuta se in precedenza era stata applicata in modo indipendente da un'etichetta |Visibile in Word, Excel, PowerPoint e Outlook <br /><br /> Quando viene applicata questa etichetta: <br /><br />- Non viene applicata alcuna protezione e la protezione viene rimossa [[2]](#footnote-2) se in precedenza era stata applicata da un'etichetta <br /><br />- La protezione viene mantenuta se in precedenza era stata applicata in modo indipendente da un'etichetta [[1]](#footnote-1) |
|HYOK (AD RMS) con autorizzazioni definite dall'utente per Word, Excel, PowerPoint ed Esplora file:| Visibile in Word, Excel, PowerPoint ed Esplora file<br /><br /> Quando viene applicata questa etichetta:<br /><br /> - La protezione HYOK viene applicata a documenti e messaggi di posta elettronica| Visibile in Word, Excel e PowerPoint <br /><br /> Quando viene applicata questa etichetta: <br /><br />- La protezione non viene applicata e viene rimossa [[2]](#footnote-2) se in precedenza era stata applicata da un'etichetta <br /><br />- La protezione viene mantenuta se in precedenza era stata applicata in modo indipendente da un'etichetta|Visibile in Word, Excel e PowerPoint <br /><br /> Quando viene applicata questa etichetta: <br /><br />- La protezione non viene applicata e viene rimossa [[2]](#footnote-2) se in precedenza era stata applicata da un'etichetta <br /><br />- La protezione viene mantenuta se in precedenza era stata applicata in modo indipendente da un'etichetta |
|HYOK (AD RMS) con autorizzazioni definite dall'utente per Outlook:|Visibile in Outlook<br /><br />Quando viene applicata questa etichetta:<br /><br />- Ai messaggi di posta elettronica viene applicato Non inoltrare con la protezione HYOK|Visibile in Outlook<br /><br />Quando viene applicata questa etichetta:<br /><br /> - La protezione non viene applicata e viene rimossa [[2]](#footnote-2) se in precedenza era stata applicata da un'etichetta <br /><br />- La protezione viene mantenuta se in precedenza era stata applicata in modo indipendente da un'etichetta|Visibile in Outlook<br /><br />Quando viene applicata questa etichetta:<br /><br />- La protezione non viene applicata e viene rimossa [[2]](#footnote-2) se in precedenza era stata applicata da un'etichetta <br /><br />- La protezione viene mantenuta se in precedenza era stata applicata in modo indipendente da un'etichetta [[1]](#footnote-1)|

###### <a name="footnote-1"></a>Nota 1

In Outlook, la protezione viene mantenuta con un'unica eccezione: quando un messaggio di posta elettronica è stato protetto con l'opzione di sola crittografia, tale protezione viene rimossa.


###### <a name="footnote-2"></a>Nota 2

La protezione viene rimossa se l'utente ha un diritto di utilizzo o ruolo che supporta questa azione:
- Il [diritto di utilizzo](configure-usage-rights.md#usage-rights-and-descriptions) Esporta o Controllo completo.
- Il ruolo di [emittente di Rights Management o proprietario di Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner) oppure di [utente con privilegi avanzati](configure-super-users.md).

Se l'utente non ha uno di questi diritti di utilizzo o ruoli, l'etichetta non viene applicata e viene mantenuta la protezione originale.


## <a name="to-migrate-azure-information-protection-labels"></a>Per eseguire la migrazione delle etichette di Azure Information Protection

Usare le istruzioni seguenti per eseguire la migrazione del tenant e Azure Information Protection etichette per l'uso dell'archivio di etichette unificato.

Per eseguire la migrazione delle etichette, è necessario essere un amministratore di conformità, un amministratore dei dati di conformità, un amministratore della sicurezza o un amministratore globale.

1. Se non è già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Quindi passare al riquadro **Azure Information Protection**.
    
    Ad esempio, nella casella di ricerca per risorse, servizi e documenti: iniziare a digitare **informazioni** e selezionare **Azure Information Protection**.

2. Dall'opzione di menu **Gestisci** selezionare **etichetta unificata**.

3. Nel riquadro **Azure Information Protection-Unified Labeling** selezionare **Activate (attiva** ) e seguire le istruzioni online.
    
    Se l'opzione per l'attivazione non è disponibile, controllare lo **stato di etichettatura unificata**: se viene visualizzato **attivato**, il tenant usa già l'archivio di etichette unificato e non è necessario eseguire la migrazione delle etichette.

Le etichette di cui è stata eseguita correttamente la migrazione possono ora essere usate dai [client e servizi che supportano l'etichettatura unificata](#clients-and-services-that-support-unified-labeling). Tuttavia, è necessario prima [pubblicare queste etichette](/microsoft-365/compliance/create-sensitivity-labels#publish-sensitivity-labels-by-creating-a-label-policy) in uno dei centri di amministrazione: Office 365 Centro sicurezza e conformità, Microsoft 365 Centro sicurezza o Microsoft 365 Compliance Center.

> [!IMPORTANT]
> Se si modificano le etichette al di fuori dell'portale di Azure, per Azure Information Protection client (versione classica) tornare a questo riquadro **Azure Information Protection-Unified Labeling** e selezionare **pubblica**.

### <a name="copy-policies"></a>Copia criteri

> [!NOTE]
> Questa opzione è in anteprima e soggetta a modifiche.

Dopo aver eseguito la migrazione delle etichette, è possibile selezionare un'opzione per la copia dei criteri. Se si seleziona questa opzione, viene inviata una copia monouso dei criteri con le [impostazioni dei criteri](configure-policy-settings.md) e qualsiasi [impostazione client avanzata](./rms-client/client-admin-guide-customizations.md#available-advanced-client-settings) all'interfaccia di amministrazione in cui si gestiscono le etichette: Office 365 Centro sicurezza e conformità, centro sicurezza Microsoft 365, Microsoft 365 conformità al centro. 

I criteri copiati con le relative impostazioni ed etichette vengono quindi pubblicati automaticamente negli utenti e nei gruppi assegnati ai criteri nel portale di Azure. Si noti che per i criteri globali significa che tutti gli utenti. Se non si è pronti per la pubblicazione delle etichette migrate nei criteri copiati, dopo che i criteri sono stati copiati, è possibile rimuovere le etichette dai criteri delle etichette nel centro di amministrazione delle etichette.

Prima di selezionare l'opzione **Copy Policies (Preview)** nel riquadro **Azure Information Protection-Unified Labeling** , tenere presente quanto segue:

- L'opzione **copia criteri (anteprima)** non è disponibile fino a quando non viene attivata l'etichetta unificata per il tenant.

- Non è possibile scegliere in modo selettivo i criteri e le impostazioni da copiare. Tutti i criteri (i criteri **globali** e tutti i criteri con ambito) vengono selezionati automaticamente per la copia e vengono copiate tutte le impostazioni supportate come impostazioni dei criteri di etichetta. Se si dispone già di un criterio etichetta con lo stesso nome, verrà sovrascritto con le impostazioni dei criteri nel portale di Azure.

- Alcune impostazioni client avanzate non vengono copiate perché per il client Azure Information Protection Unified Labeling sono supportate come *Impostazioni avanzate dell'etichetta* anziché come impostazioni dei criteri. È possibile configurare queste impostazioni avanzate di etichetta con [Office 365 Centro sicurezza e conformità PowerShell](./rms-client/clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell). Impostazioni client avanzate che non vengono copiate:
    - [LabelbyCustomProperty](./rms-client/client-admin-guide-customizations.md#migrate-labels-from-secure-islands-and-other-labeling-solutions)
    - [LabelToSMIME](./rms-client/client-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)

- A differenza della migrazione delle etichette in cui vengono sincronizzate le successive modifiche alle etichette, l'azione **copia criteri** non sincronizza le modifiche successive ai criteri o alle impostazioni dei criteri. È possibile ripetere l'azione di copia dei criteri dopo aver apportato modifiche all'portale di Azure e tutti i criteri esistenti e le relative impostazioni verranno sovrascritti. In alternativa, usare i cmdlet Set-LabelPolicy o set-Label con il parametro *AdvancedSettings* di Office 365 Centro sicurezza e conformità PowerShell.

- L'azione **copia criteri** verifica quanto segue per ogni criterio prima di essere copiato:
    
    - Utenti e gruppi assegnati al criterio sono attualmente in Azure AD. Se uno o più account risultano mancanti, i criteri non vengono copiati. L'appartenenza al gruppo non è selezionata.
    
    - I criteri globali contengono almeno un'etichetta. Poiché i centri di assegnazione di etichette dell'amministratore non supportano i criteri di etichetta senza etichette, i criteri globali senza etichette non vengono copiati.

- Se si copiano i criteri e quindi li si elimina dall'interfaccia utente di amministrazione, attendere almeno due ore prima di utilizzare di nuovo l'azione **copia criteri** per garantire tempo sufficiente per la replica dell'eliminazione.

Per ulteriori informazioni sulla configurazione delle impostazioni dei criteri, le impostazioni client avanzate e le impostazioni delle etichette per il client Azure Information Protection Unified Labeling, vedere [configurazioni personalizzate per il Azure Information Protection client Unified Labeling](./rms-client/clientv2-admin-guide-customizations.md) dalla guida dell'amministratore.

### <a name="clients-and-services-that-support-unified-labeling"></a>Client e servizi che supportano l'etichettatura unificata

Per verificare se i client e i servizi usati supportano l'assegnazione di etichette unificata, fare riferimento alla relativa documentazione per verificare se possono usare le etichette di riservatezza pubblicate da uno dei centri di amministrazione: Office 365 Centro sicurezza e conformità, Microsoft 365 Centro sicurezza o Microsoft 365 centro conformità. 

##### <a name="clients-that-currently-support-unified-labeling-include"></a>I client che attualmente supportano l'etichettatura unificata includono:

- Il [Azure Information Protection client di etichetta unificato per Windows](./rms-client/unifiedlabelingclient-version-release-history.md). Per un confronto di questo client con il client di Azure Information Protection (classico), vedere [confrontare i client di etichettatura per i computer Windows](./rms-client/use-client.md#compare-the-labeling-clients-for-windows-computers).

- App di Office che sono in fasi di disponibilità diverse. Per altre informazioni, vedere [supporto per le funzionalità di etichetta di riservatezza nelle app](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps#support-for-sensitivity-label-capabilities-in-apps) dalla documentazione di Office.
    
- App da fornitori e sviluppatori di software che usano [Microsoft Information Protection SDK](https://docs.microsoft.com/information-protection/develop/overview).

##### <a name="services-that-currently-support-unified-labeling-include"></a>I servizi che attualmente supportano l'etichettatura unificata includono:

- [Power BI (in anteprima)](https://docs.microsoft.com/power-bi/admin/service-security-data-protection-overview)

- Office Online (in anteprima) e Outlook sul Web

- SharePoint Online, OneDrive for business, Microsoft teams e Office 365 groups (in anteprima)
    
    Per altre informazioni, vedere [usare le etichette di riservatezza con Microsoft teams, gruppi di Office 365 e siti di SharePoint (anteprima pubblica)](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-teams-groups-sites) e [abilitare le etichette di riservatezza per i file di Office in SharePoint e OneDrive (anteprima pubblica)](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files).

- Microsoft Defender Advanced Threat Protection

- Microsoft Cloud App Security
    
    Questo servizio supporta le etichette sia prima che dopo la migrazione all'archivio di etichettatura unificata secondo la logica seguente:
    
    - Se i centri di amministrazione hanno etichette di riservatezza, queste etichette vengono recuperate dai centri di amministrazione. Per selezionare tali etichette in Cloud App Security, è necessario pubblicare almeno un'etichetta in almeno un utente.
    
    - Se i centri di amministrazione non hanno etichette di riservatezza, Azure Information Protection le etichette vengono recuperate dalla portale di Azure.

- Servizi da fornitori e sviluppatori di software che usano [Microsoft Information Protection SDK](https://docs.microsoft.com/information-protection/develop/overview).

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori indicazioni e suggerimenti del team dell'esperienza clienti, vedere le risorse seguenti:

- Post di Blog: [informazioni sulla migrazione di etichette unificate](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Understanding-Unified-Labeling-migration/ba-p/783185)

- Webinar: [registrazione con etichetta unificata, mazzo e domande frequenti](https://github.com/nihendle/MIP-Comp/tree/master/MIP/Webinars/Unified%20Labeling%20Migration)

Per altre informazioni sulle etichette migrate che ora possono essere configurate e pubblicate in uno dei centri di amministrazione con etichette, vedere [Panoramica delle etichette di riservatezza](/microsoft-365/compliance/sensitivity-labels) e [creare e configurare etichette di riservatezza e criteri](https://docs.microsoft.com/microsoft-365/compliance/create-sensitivity-labels).

Se non è già stato fatto, installare il client di Azure Information Protection Unified labeling. Per informazioni sulla versione, una guida dell'amministratore e un manuale dell'utente, vedere [Azure Information Protection client di etichetta unificata per Windows](./rms-client/aip-clientv2.md).
