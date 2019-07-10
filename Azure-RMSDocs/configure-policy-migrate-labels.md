---
title: Eseguire la migrazione delle etichette di Azure Information Protection a Office 365 - AIP
description: Eseguire la migrazione di etichette di Azure Information Protection a etichette di riservatezza di Office 365 per i client e i servizi che supportano le etichette unificate.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/10/2019
ms.topic: article
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: 87d66363531aa29705dedc12ffdace9725fae580
ms.sourcegitcommit: 531feafbabd8874fbeac4bd460e9bef60afabcdc
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/09/2019
ms.locfileid: "67691028"
---
# <a name="how-to-migrate-azure-information-protection-labels-to-office-365-sensitivity-labels"></a>Come eseguire la migrazione di etichette di Azure Information Protection a etichette di riservatezza di Office 365

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
> *Istruzioni per: [Client Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Eseguire la migrazione delle etichette in Azure Information Protection in modo che sia possibile usarle come etichette di riservatezza dal [client e servizi che supportano l'assegnazione di etichette unificata](#clients-and-services-that-support-unified-labeling).

Dopo la migrazione, gestire e pubblicare queste etichette da una delle aree di amministrazione seguenti: Centro sicurezza e conformità di Office 365, Centro sicurezza Microsoft 365 o Centro conformità Microsoft 365. Queste etichette sono utilizzabile dal client Azure Information Protection unified imprevisto delle etichette. Se si continua a usare il client Azure Information Protection (versione classica), il client continua a scaricare le etichette con i criteri di Azure Information Protection dal portale di Azure.

Prima di passare alle istruzioni dettagliate per la migrazione delle etichette può essere utile leggere queste domande frequenti:

- [Qual è la differenza tra le etichette in Azure Information Protection e in Office 365?](faqs.md#whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365)

- [Qual è il momento giusto per la migrazione delle etichette in Office 365?](faqs.md#when-is-the-right-time-to-migrate-my-labels-to-office-365)

- [Dopo la migrazione delle etichette, quale portale di gestione si usa?](faqs.md?#after-ive-migrated-my-labels-which-management-portal-do-i-use )

### <a name="important-information-about-administrative-roles"></a>Informazioni importanti sui ruoli amministrativi

Il [ruolo di Azure AD](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) dei **amministratore di Azure Information Protection** (in precedenza **amministratore di Information Protection**) non è supportata per l'assegnazione di etichette unificato piattaforma. Se questo ruolo amministrativo viene usato nell'organizzazione, prima di migrare le etichette, aggiungere gli utenti che dispongono di questo ruolo per i ruoli di Azure AD del **amministratore di conformità**, **amministratore dei dati di conformità**, oppure **amministratore della sicurezza**. Se serve assistenza con questa procedura, vedere [Concedere agli utenti l'accesso al Centro sicurezza e conformità di Office 365](https://docs.microsoft.com/office365/securitycompliance/grant-access-to-the-security-and-compliance-center). È possibile assegnare questi ruoli anche nel portale di Azure AD, nel Centro sicurezza Microsoft 365 e nel Centro conformità Microsoft 365.

Come alternativa all'uso dei ruoli, nelle interfacce di amministrazione è possibile creare un nuovo gruppo di ruoli per questi utenti e aggiungere il ruolo **Sensitivity Label Administrator** (Amministratore etichette di riservatezza) o **Organization Configuration** (Configurazione organizzazione) a questo gruppo.

Se non si consente l'accesso ai centri di amministrazione a questi utenti usando una di queste configurazioni, gli utenti non potranno configurare Azure Information Protection nel portale di Azure dopo la migrazione delle etichette.

Gli amministratori globali per il tenant possono continuare a gestire le etichette e i criteri sia nel portale di Azure che nei centri di amministrazione dopo la migrazione delle etichette.

## <a name="considerations-for-unified-labels"></a>Considerazioni per le etichette unificate

Prima di eseguire la migrazione delle etichette, prendere nota delle seguenti modifiche e considerazioni:

- Assicurarsi di aver [i client che supportano le etichette unificate](#clients-and-services-that-support-unified-labeling) e se necessario, essere preparata per l'amministrazione del portale di Azure (per i client che non supportano le etichette unificate) sia le interfacce di amministrazione (per i client che supportano etichette unificate).

- I criteri, incluse le impostazioni dei criteri e gli utenti autorizzati all'accesso (criteri con ambito) e tutte le impostazioni client avanzate non vengono sottoposti a migrazione. Opzioni di configurazione di queste impostazioni dopo la migrazione di etichetta includono quanto segue:
    - Il [copiare criteri](#copy-your-policies-and-policy-settings) opzione.
    - L'interfaccia di amministrazione per le etichette di riservatezza.
    - [Sicurezza e Office 365 PowerShell Compliance](https://docs.microsoft.com/powershell/exchange/office-365-scc/office-365-scc-powershell?view=exchange-ps), che è necessario usare per configurare [impostazioni client avanzate](./rms-client/clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell).
    
    Per un'esperienza utente più uniforme è consigliabile pubblicare le stesse etichette negli stessi ambiti nei centri di amministrazione.

- Non tutte le impostazioni di un'etichetta migrata sono supportate dai centri di amministrazione. Usare la tabella nella sezione [Impostazioni delle etichette non supportate nei centri di amministrazione](#label-settings-that-are-not-supported-in-the-admin-centers) per individuare queste impostazioni e le operazioni consigliate.

- Modelli di protezione:
    
    - Anche i modelli che usano una chiave basata sul cloud e fanno parte di una configurazione di etichetta vengono sottoposti a migrazione con l'etichetta. Gli altri modelli di protezione non vengono sottoposti a migrazione. 
    
    - Se sono presenti etichette configurate per un modello predefinito, modificare tali etichette e selezionare l'opzione **Imposta autorizzazioni** per configurare le stesse impostazioni di protezione che erano presenti nel modello. Le etichette con modelli predefiniti non bloccheranno la migrazione delle etichette, ma questa configurazione dell'etichetta non è supportata nei centri di amministrazione.
        
        Suggerimento: Per facilitare la riconfigurazione di queste etichette, può essere utile avere due finestre del browser: una finestra in cui selezionare il pulsante **Modifica modello** per l'etichetta in modo da visualizzare le impostazioni di protezione e l'altra per configurare le stesse impostazioni quando si seleziona **Imposta autorizzazioni**.
    
    - Dopo la migrazione di un'etichetta con le impostazioni di protezione basati sul cloud è stata eseguita, l'ambito risulta del modello di protezione è l'ambito definito nel portale di Azure (o usando il modulo AIPService PowerShell) e l'ambito definito nelle interfacce di amministrazione. 

- Quando si esegue la migrazione delle etichette, i risultati della migrazione visualizzano se un'etichetta è stata **creata**, **aggiornata** o **rinominata** per motivi di duplicazione:

    - Dopo la creazione dell'etichetta, è necessario pubblicarla in uno dei centri di amministrazione per renderla disponibile ad applicazioni e servizi.
    
    - Quando un'etichetta viene rinominata, è necessario modificarla. L'operazione può essere eseguita in uno dei centri di amministrazione o nel portale di Azure.

- Per ogni etichetta il portale di Azure consente di visualizzare solo il nome visualizzato dell'etichetta, che è modificabile. Nei centri di amministrazione vengono mostrati sia il nome visualizzato per un'etichetta che il nome dell'etichetta. Il nome dell'etichetta è il nome iniziale specificato al momento della creazione dell'etichetta. Il servizio back-end usa questa proprietà per l'identificazione.

- Le eventuali stringhe localizzate per le etichette non vengono incluse nella migrazione. Definire nuove stringhe localizzate per le etichette migrate usando Office 365 Security & Compliance PowerShell e il *LocaleSettings* parametro per [Set con etichetta](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps).

- Dopo la migrazione, quando si modifica un'etichetta migrata nel portale di Azure, la stessa modifica si riflette automaticamente nei centri di amministrazione. Tuttavia, quando si modifica un'etichetta migrata in uno dei centri di amministrazione, è necessario tornare al portale di Azure, nel pannello **Azure Information Protection - Etichettatura unificata**, e selezionare **Pubblica**. Questa azione aggiuntiva è necessaria per il client Azure Information Protection (versione classica) per rendere effettive le modifiche dell'etichetta.

### <a name="label-settings-that-are-not-supported-in-the-admin-centers"></a>Impostazioni delle etichette non supportate nei centri di amministrazione

Usare la tabella seguente per identificare le impostazioni di configurazione di un'etichetta migrata non supportate dal Centro sicurezza e conformità di Office 365, dal Centro sicurezza Microsoft 365 o dal Centro conformità Microsoft 365. Se sono presenti etichette con queste impostazioni, una volta completata la migrazione, usare le indicazioni di amministrazione della colonna finale prima di pubblicare le etichette in una delle aree di amministrazione di cui viene fatto riferimento.

In caso di dubbi sulla configurazione delle etichette, visualizzare le relative impostazioni nel portale di Azure. Se serve assistenza con questa procedura, vedere [Configurazione dei criteri di Azure Information Protection](configure-policy.md).

Client Azure Information Protection (versione classico) possono usare tutte le impostazioni di etichetta elencate senza problemi in quanto continuano a scaricare le etichette dal portale di Azure.

|Configurazione dell'etichetta|Supportata dai client di etichettatura unificata| Linee guida per i centri di amministrazione|
|-------------------|---------------------------------------------|-------------------------|
|Stato abilitato o disabilitato<br /><br />Questo stato non viene sincronizzato con le interfacce di amministrazione |Non applicabile|Equivale a se l'etichetta è pubblicata o no. |
|Colore dell'etichetta selezionato dall'elenco o specificato con il codice RGB |Yes|Nessuna opzione di configurazione per i colori dell'etichetta. In alternativa, è possibile configurare i colori di etichetta nel portale di Azure oppure usare [PowerShell](./rms-client/clientv2-admin-guide-customizations.md#specify-a-color-for-the-label).|
|Protezione basata sul cloud o protezione basata su HYOK usando un modello predefinito |No|Nessuna opzione di configurazione per i modelli predefiniti. Non è consigliabile pubblicare un'etichetta con questa configurazione.|
|Protezione basata sul cloud che usa autorizzazioni definite dall'utente in Word, Excel e PowerPoint |No|Le interfacce di amministrazione non sono un'opzione di configurazione per le autorizzazioni definite dall'utente per queste app di Office. A meno che non si usa la versione di anteprima del client di assegnazione di etichette unificata, è consigliabile non che si pubblica un'etichetta con questa configurazione. Se si pubblica un'etichetta con questa configurazione, verificare il risultato ottenuto applicando l'etichetta dal [nella tabella seguente](#comparing-the-behavior-of-protection-settings-for-a-label).|
|Protezione basata su HYOK che usa autorizzazioni definite dall'utente per Outlook (Non inoltrare) |No|Nessuna opzione di configurazione per HYOK. Non è consigliabile pubblicare un'etichetta con questa configurazione. In caso contrario i risultati ottenuti applicando l'etichetta sono elencati nella [tabella seguente](#comparing-the-behavior-of-protection-settings-for-a-label).|
|Rimuovere la protezione |No|Nessuna opzione di configurazione per rimuovere la protezione. Non è consigliabile pubblicare un'etichetta con questa configurazione.<br /><br /> Se si pubblica un'etichetta con questa configurazione, quando viene applicato, sarà possibile rimuovere la protezione se applicata in precedenza da un'etichetta. La protezione verrà mantenuta se in precedenza era stata applicata in modo indipendente da un'etichetta.|
|Tipi di carattere personalizzato e colore del tipo di carattere personalizzato tramite RGB per i contrassegni visivi (intestazione, piè di pagina, filigrana)|Yes|La configurazione per i contrassegni visivi è limitata a un elenco di colori e dimensioni dei caratteri. È possibile pubblicare questa etichetta senza modifiche benché non sia possibile visualizzare i valori configurati nei centri di amministrazione. <br /><br />Per modificare queste opzioni è possibile usare il portale di Azure. Per semplificare l'amministrazione, tuttavia, provare a cambiare il colore impostando una delle opzioni elencate nei centri di amministrazione.|
|Variabili nei contrassegni visivi (intestazione, piè di pagina, filigrana)|No|Se si pubblica questa etichetta senza modifiche, le variabili vengono visualizzate come testo nei client anziché visualizzare i valori dinamici. Prima di pubblicare l'etichetta, modificare le stringhe per rimuovere le variabili.|
|Contrassegni visivi per app|No|Se si pubblica questa etichetta senza modifiche, le variabili delle app vengono visualizzate come testo nei client in tutte le app anziché visualizzare le stringhe di testo in app selezionate. Pubblicare questa etichetta solo se è adatta per tutte le app e modificare le stringhe per rimuovere le variabili delle app.|
|Condizioni e impostazioni associate <br /><br /> include l'assegnazione di etichette automatica e consigliata e le descrizioni comando corrispondenti|Non applicabile|Riconfigurare le condizioni tramite l'applicazione automatica di etichette come configurazione separata dalle impostazioni dell'etichetta.|

### <a name="comparing-the-behavior-of-protection-settings-for-a-label"></a>Confronto del comportamento delle impostazioni di protezione per un'etichetta

Usare la tabella seguente per identificare come la stessa impostazione di protezione per un'etichetta si comporta in modo diverso, a seconda del fatto che venga usato dal client Azure Information Protection (versione classica), il client di assegnazione di etichette Azure Information Protection unified, o per le app di Office con l'assegnazione di etichette predefiniti (noto anche come "nativi di Office 

In caso di dubbi sulla configurazione delle impostazioni di protezione, visualizzare le relative impostazioni nel pannello **Protezione** nel portale di Azure. Se serve assistenza con questa procedura, vedere [Per configurare un'etichetta per le impostazioni di protezione](configure-policy-protection.md#to-configure-a-label-for-protection-settings).

Le impostazioni di protezione con lo stesso comportamento non sono elencate nella tabella, con le eccezioni seguenti:
- Quando si usano le app di Office con l'etichettatura incorporata, le etichette non sono visibili in Esplora file a meno che non si installi anche il client di etichettatura unificata di Azure Information Protection.
- Quando si usano le app di Office con l'etichettatura incorporata, la protezione viene mantenuta se in precedenza era stata applicata in modo indipendente da un'etichetta [[1]](#footnote-1).

|Impostazione di protezione per un'etichetta |Client Azure Information Protection (versione classica) |Client per l'etichettatura unificata di Azure Information Protection| App di Office con etichettatura incorporata
|-------------------|-----------------------------------|-----------------------------------------------------------|---------------
|Azure (chiave cloud) con autorizzazioni definite dall'utente per Word, Excel, PowerPoint ed Esplora file:| Visibile in Word, Excel, PowerPoint ed Esplora file <br /><br /> Quando viene applicata l'etichetta:<br /><br /> - Agli utenti vengono richieste le autorizzazioni personalizzate che vengono quindi applicate come protezione tramite una chiave basata su cloud| Per la versione con disponibilità generale: Non visibile <br /><br />  Per la versione di anteprima: Visibile in Word, Excel, PowerPoint ed Esplora file <br /><br /> Quando viene applicata l'etichetta:<br /><br /> - Agli utenti vengono richieste le autorizzazioni personalizzate che vengono quindi applicate come protezione tramite una chiave basata su cloud|Visibile in Word, Excel, PowerPoint e Outlook: <br /><br /> Quando viene applicata l'etichetta:<br /><br /> - Agli utenti non vengono richieste le autorizzazioni personalizzate e non viene applicata alcuna protezione <br /><br /> - La protezione viene mantenuta se in precedenza era stata applicata in modo indipendente da un'etichetta [[1]](#footnote-1)|
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

È necessario essere un amministratore di conformità, amministratore di conformità dei dati, amministratore della sicurezza o amministratore globale per eseguire la migrazione delle etichette.

> [!NOTE]
> Se si dispone di etichette di conservazione o criteri di prevenzione della perdita dei dati per Office 365, si consiglia di avere il ruolo di amministratore di conformità, ruolo di amministratore di conformità dei dati o il ruolo di amministratore globale per eseguire la migrazione delle etichette.
> 
> Gli amministratori della sicurezza non ha accesso alla conservazione dei dati o le etichette criteri prevenzione della perdita, pertanto, se si dispone di uno di questi elementi e hanno lo stesso nome delle etichette di Azure Information Protection, il processo di migrazione non è possibile completare manualmente finché non si rinomina uno dei duplicati. Tuttavia, se si dispone di uno degli altri ruoli, il processo di migrazione possibile rinominare l'etichetta di Azure Information Protection, in modo da poter completare la migrazione.

1. Se non è già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Quindi passare al pannello **Azure Information Protection**.
    
    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Dal **Manage** opzione di menu, selezionare **unificato l'assegnazione di etichette**.

3. Nel pannello **Azure Information Protection - Etichettatura unificata** selezionare **Attiva** e seguire le istruzioni online.
    
    Se l'opzione di attivazione non è disponibile, controllare l'impostazione di **Stato dell'etichettatura unificata**: se è **Attivato**, il tenant usa già l'archivio di etichette unificate e non è necessario eseguire la migrazione delle etichette.

Le etichette di cui è stata eseguita correttamente la migrazione possono ora essere usate dai [client e servizi che supportano l'etichettatura unificata](#clients-and-services-that-support-unified-labeling). Tuttavia, è prima necessario pubblicare queste etichette in uno dei centri di amministrazione: Centro sicurezza e conformità di Office 365, Centro sicurezza di Microsoft 365 o Centro conformità di Microsoft 365.

> [!IMPORTANT]
> Se si modificano le etichette all'esterno del portale di Azure, per i client di Azure Information Protection (versione classica), tornare a questa **unificata di Azure Information Protection - etichette** pannello e selezionare **Publish**.


#### <a name="copy-your-policies-and-policy-settings"></a>Copiare i criteri e impostazioni dei criteri

> [!NOTE]
> Questa opzione è un'implementazione graduale per i tenant in fase di anteprima e soggetta a modifiche. Se non viene visualizzato il **copiare criteri (anteprima)** opzione, riprovare tra qualche settimana.

Dopo la migrazione delle etichette, è possibile selezionare un'opzione per copiare i criteri. Se si seleziona questa opzione, una copia occasionale dei criteri con loro [le impostazioni dei criteri](configure-policy-settings.md) e qualsiasi [impostazioni client avanzate](./rms-client/client-admin-guide-customizations.md#available-advanced-client-settings) viene inviato all'interfaccia di amministrazione in cui è gestire le etichette: Centro sicurezza e conformità di Office 365, Centro sicurezza di Microsoft 365 o Centro conformità di Microsoft 365.

Prima di selezionare il **copiare criteri (anteprima)** opzione, tenere presente quanto segue:

- È possibile scegliere in modo selettivo criteri e impostazioni da copiare. Tutti i criteri (la **Global** criteri ed eventuali criteri con ambito) vengono copiati e tutte le impostazioni che sono supportate in quanto vengono copiate le impostazioni dei criteri dell'etichetta. Se si dispone già di un criterio di etichetta con lo stesso nome, verrà sovrascritto con le impostazioni dei criteri nel portale di Azure.

- Alcune impostazioni del client avanzato non vengono copiate perché per Azure Information Protection unified client l'assegnazione di etichette, sono supportati come *etichetta impostazioni avanzata* anziché le impostazioni dei criteri. È possibile configurare queste impostazioni di etichetta avanzata con [Office 365 Security & Compliance Center PowerShell](./rms-client/clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell). Le impostazioni del client avanzato che non vengono copiate includono:
    - [LabelbyCustomProperty](./rms-client/client-admin-guide-customizations.md#migrate-labels-from-secure-islands-and-other-labeling-solutions)
    - [LabelToSMIME](./rms-client/client-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)

- Per supportare le proprietà del client avanzato che vengono copiate, è necessario usare la versione di anteprima del client Azure Information Protection unified imprevisto delle etichette.

- A differenza di migrazione di etichetta in cui vengono sincronizzate le successive modifiche alle etichette, l'azione di criteri di copia non sincronizza eventuali modifiche successive per i criteri o impostazioni dei criteri. È possibile ripetere l'azione di copia dei criteri dopo aver apportato le modifiche nel portale di Azure e tutti i criteri esistenti e le relative impostazioni verranno sovrascritto nuovamente. In alternativa, usare il [Set-LabelPolicy](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-labelpolicy?view=exchange-ps) o [Set con etichetta](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps) cmdlet con il *AdvancedSettings* parametro da Office 365 Security & Compliance Center PowerShell.

Per altre informazioni sulla configurazione delle impostazioni dei criteri, avanzate, le impostazioni client e le impostazioni dell'etichetta per Azure Information Protection unified imprevisto delle etichette client, vedere [configurazioni personalizzate per Azure Information Protection unified l'assegnazione di etichette client](./rms-client/clientv2-admin-guide-customizations.md) nella Guida dell'amministratore.

### <a name="clients-and-services-that-support-unified-labeling"></a>Client e servizi che supportano l'etichettatura unificata

Per verificare se i client e i servizi usati dall'utente supportano l'etichettatura unificata, fare riferimento alla relativa documentazione per verificare che sia possibile usare le etichette di riservatezza pubblicate da uno dei centri di amministrazione: Centro sicurezza e conformità di Office 365, Centro sicurezza di Microsoft 365 o Centro conformità di Microsoft 365. 

##### <a name="clients-that-currently-support-unified-labeling-include"></a>I client che attualmente supportano l'etichettatura unificata includono:

- Il [unificata di Azure Information Protection client per l'assegnazione di etichette per Windows](./rms-client/unifiedlabelingclient-version-release-history.md). Per un confronto tra il client con il client Azure Information Protection (versione classica), vedere [confrontare i client](./rms-client/use-client.md#compare-the-clients).

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

Se non già stato fatto, installare il client di assegnazione di etichette unificato di Azure Information Protection. Per informazioni sulla versione di una Guida dell'amministratore e Guida dell'utente, vedere [unificata di Azure Information Protection client per l'assegnazione di etichette per Windows](./rms-client/aip-clientv2.md).
