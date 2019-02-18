---
title: Eseguire la migrazione di etichette di Azure Information Protection al Centro sicurezza e conformità di Office 365 - AIP
description: Eseguire la migrazione di etichette di Azure Information Protection al Centro sicurezza e conformità di Office 365 per i client che supportano l'etichettatura unificata.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/12/2019
ms.topic: article
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: 27fe7dce81856140caf5e30451caabc3df9a2894
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56254782"
---
# <a name="how-to-migrate-azure-information-protection-labels-to-the-office-365-security--compliance-center"></a>Come eseguire la migrazione di etichette di Azure Information Protection al Centro sicurezza e conformità di Office 365

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

> [!IMPORTANT]
> Questa funzionalità è disponibile in anteprima ed esegue la migrazione del tenant a una nuova piattaforma. La migrazione non è reversibile. La nuova piattaforma supporta l'etichettatura unificata. Le etichette create e gestite possono essere usate da più client e servizi.

Eseguire la migrazione delle etichette se si vuole usarle nel Centro sicurezza e conformità di Office 365, in cui possono essere pubblicate e quindi scaricate dai [client che supportano l'etichettatura unificata](#clients-that-support-unified-labeling). Il client Azure Information Protection continuerà a scaricare le etichette con i rispettivi criteri di Azure Information Protection dal portale di Azure. 

Prima di passare alle istruzioni dettagliate per la migrazione delle etichette può essere utile leggere queste domande frequenti:

- [Qual è la differenza tra le etichette in Azure Information Protection e in Office 365?](faqs.md#whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365)

- [Qual è il momento giusto per la migrazione delle etichette in Office 365?](faqs.md#when-is-the-right-time-to-migrate-my-labels-to-office-365)

- [Dopo la migrazione delle etichette, quale portale di gestione si usa?](faqs.md?#after-ive-migrated-my-labels-which-management-portal-do-i-use )

### <a name="important-information-about-administrative-roles"></a>Informazioni importanti sui ruoli amministrativi

I [ruoli di Azure AD](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) di **Amministratore della sicurezza** e **Amministratore di Information Protection** non sono supportati dalla piattaforma di etichettatura unificata. Se questi ruoli amministrativi vengono usati nell'organizzazione, prima di eseguire la migrazione delle etichette, aggiungere gli utenti con questi ruoli ai gruppi di ruoli **Amministratore di conformità** o **Gestione organizzazione** per il Centro sicurezza e conformità di Office 365. In alternativa, è possibile creare un nuovo gruppo di ruoli per questi utenti e aggiungere i ruoli **Gestione conservazione** o **Configurazione dell'organizzazione** a questo gruppo. Per istruzioni, vedere [Concedere agli utenti l'accesso al Centro sicurezza e conformità di Office 365](https://docs.microsoft.com/office365/securitycompliance/grant-access-to-the-security-and-compliance-center).

Se non si consente l'accesso al Centro sicurezza e conformità a questi utenti usando una di queste configurazioni, gli utenti perderanno l'accesso alle etichette e ai criteri nel portale di Azure dopo la migrazione delle etichette.

Gli amministratori globali per il tenant possono continuare a gestire le etichette e i criteri sia nel portale di Azure che nel Centro sicurezza e conformità dopo la migrazione delle etichette.


## <a name="considerations-for-unified-labels"></a>Considerazioni per le etichette unificate

Prima di eseguire la migrazione delle etichette, prendere nota delle seguenti modifiche e considerazioni:

- Non tutti i client supportano attualmente le etichette unificate. Assicurarsi di avere [client supportati](#clients-that-support-unified-labeling) e predisporre l'amministrazione sia nel portale di Azure (per i client che non supportano le etichette unificate) sia nel Centro sicurezza e conformità (per i client che supportano le etichette unificate).

- Se è ancora in corso la definizione e la configurazione delle etichette da usare, è consigliabile completare questo processo usando il portale di Azure e quindi eseguire la migrazione delle etichette. Questa strategia evita la duplicazione delle etichette durante il processo di migrazione e la successiva modifica nel Centro sicurezza e conformità.

- I criteri, incluse le impostazioni dei criteri e gli utenti autorizzati all'accesso (criteri con ambito) e tutte le impostazioni client avanzate non vengono sottoposti a migrazione. Per le modifiche di cui non viene eseguita la migrazione sarà necessario configurare le opzioni pertinenti nel Centro sicurezza e conformità dopo la migrazione delle etichette.
    
    Per un'esperienza utente più uniforme è consigliabile pubblicare le stesse etichette negli stessi ambiti nel Centro di sicurezza e conformità.

- Non tutte le impostazioni di un'etichetta sottoposta a migrazione sono supportate dal Centro sicurezza e conformità. Usare la tabella nella sezione [Impostazioni delle etichette non supportate nel Centro di sicurezza e conformità](#label-settings-that-are-not-supported-in-the-security--compliance-center) per individuare le impostazioni non supportate dal Centro sicurezza e conformità.

- Modelli di protezione:
    
    - Anche i modelli che usano una chiave basata sul cloud e fanno parte di una configurazione di etichetta vengono sottoposti a migrazione con l'etichetta. Gli altri modelli di protezione non vengono sottoposti a migrazione. 
    
    - Se sono presenti etichette configurate per un modello predefinito, [convertire questi modelli in etichette](configure-policy-templates.md#to-convert-templates-to-labels) prima della migrazione delle etichette. Questa configurazione non bloccherà la migrazione delle etichette, ma non è supportata nel Centro sicurezza e conformità.
    
    - Dopo la migrazione di un'etichetta con le impostazioni di protezione basate sul cloud, l'ambito risultante del modello di protezione è l'ambito definito nel portale di Azure (o mediante il modulo PowerShell AADRM) e quello definito nel Centro sicurezza e conformità. 

- Quando si esegue la migrazione delle etichette, i risultati della migrazione visualizzano se un'etichetta è stata **creata**, **aggiornata** o **rinominata** per motivi di duplicazione:

    - Dopo la creazione dell'etichetta, è necessario pubblicarla nel Centro sicurezza e conformità per renderla disponibile ad applicazioni e servizi.
    
    - Quando un'etichetta viene rinominata, è necessario modificarla. L'operazione può essere eseguita nel Centro sicurezza e conformità o nel portale di Azure. 

- Per ogni etichetta il portale di Azure consente di visualizzare solo il nome visualizzato dell'etichetta, che è modificabile. Il Centro sicurezza e conformità presenta sia il nome visualizzato dell'etichetta sia il nome dell'etichetta. Il nome dell'etichetta è il nome iniziale specificato al momento della creazione dell'etichetta. Il servizio back-end usa questa proprietà per l'identificazione.

- Le eventuali stringhe localizzate per le etichette non vengono incluse nella migrazione. Per le etichette sottoposte a migrazione sarà necessario definire nuove stringhe localizzate nel Centro sicurezza e conformità.

- Dopo la migrazione, quando si modifica un'etichetta sottoposta a migrazione nel portale di Azure, la stessa modifica si riflette automaticamente nel Centro sicurezza e conformità. Tuttavia, quando si modifica un'etichetta migrata nel Centro sicurezza e conformità, è necessario tornare al portale di Azure, nel pannello **Azure Information Protection - Etichettatura unificata**, e selezionare **Pubblica**. Questa azione aggiuntiva è necessaria per il client Azure Information Protection per recuperare le modifiche dell'etichetta.

### <a name="label-settings-that-are-not-supported-in-the-security--compliance-center"></a>Impostazioni delle etichette non supportate nel Centro di sicurezza e conformità

Usare la tabella seguente per identificare le impostazioni di configurazione di un'etichetta migrata che non sono supportate dai client di etichettatura unificata o lo sono con limitazioni. Per evitare confusione, è consigliabile non configurare le impostazioni che non hanno alcun effetto sui client di etichettatura unificata.

I client Azure Information Protection possono usare queste impostazioni delle etichette senza problemi, perché continuano a scaricare le etichette dal portale di Azure.

|Configurazione dell'etichetta|Supportata dai client di etichettatura unificata|Esclusione dalla modifica nel Centro sicurezza e conformità|
|-------------------|---------------------------------------------|-------------------------|
|Stato abilitato o disabilitato<br /><br />Note: nessuna sincronizzazione con il Centro sicurezza e conformità |Non applicabile|Non applicabile|
|Colore dell'etichetta: selezionarlo dall'elenco o specificarlo con il codice RGB<br /><br />Note: i colori delle etichette non sono supportati dal Centro sicurezza e conformità |Non applicabile|Non applicabile|
|Protezione basata sul cloud o protezione basata su HYOK usando un modello predefinito |No|Sì|
|Protezione basata sul cloud che usa autorizzazioni definite dall'utente in Word, Excel e PowerPoint |No|Sì|
|Protezione basata su HYOK che usa autorizzazioni definite dall'utente in Outlook per Non inoltrare |No|Sì|
|Rimuovere la protezione |No|Sì|
|Contrassegni visivi (intestazione, piè di pagina, filigrana): Tipo di carattere personalizzato e colore carattere personalizzato in base al codice RGB|No|Consigliata se si usano le variabili<br /><br />- Nei client le variabili vengono visualizzate come testo anziché visualizzare i valori dinamici|
|Contrassegni visivi per app|No|Consigliata se si usano le variabili<br /><br />- Nei client le variabili vengono visualizzate come testo anziché visualizzare i valori dinamici|
|Condizioni e impostazioni associate <br /><br />Note: include l'assegnazione di etichette automatica e consigliata e le descrizioni comando corrispondenti|Non applicabile|No|


## <a name="to-migrate-azure-information-protection-labels"></a>Per eseguire la migrazione delle etichette di Azure Information Protection

Usare le istruzioni seguenti per eseguire la migrazione del tenant e delle etichette di Azure Information Protection per usare il nuovo archivio di etichettatura unificata.

È necessario essere un amministratore globale per eseguire la migrazione delle etichette.

1. Se non è già stato fatto, aprire una nuova finestra del browser e [accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal). Quindi passare al pannello **Azure Information Protection**.
    
    Ad esempio, dal menu hub fare clic su **Tutti i servizi** e iniziare a digitare **Informazioni** nella casella Filtro. Selezionare **Azure Information Protection**.

2. Dall'opzione di menu **Gestisci** selezionare **Etichettatura unificata (anteprima)**.

3. Nel pannello **Azure Information Protection - Etichettatura unificata** selezionare **Attiva** e seguire le istruzioni online.

Le etichette di cui è stata eseguita correttamente la migrazione possono ora essere usate dai [client che supportano l'etichettatura unificata](#clients-that-support-unified-labeling). Tuttavia, è prima di tutto necessario pubblicare queste etichette nel Centro sicurezza e conformità.

> [!IMPORTANT]
> Se si modificano le etichette all'esterno del portale di Azure, per i client di Azure Information Protection, tornare a questo pannello **Azure Information Protection - Etichettatura unificata** e selezionare **Pubblica**.

### <a name="clients-that-support-unified-labeling"></a>Client che supportano l'etichettatura unificata

I client che attualmente supportano l'etichettatura unificata includono:

- Il [client per l'etichettatura unificata di Azure Information Protection per Windows](./rms-client/unifiedlabelingclient-version-release-history.md) (in anteprima)

- App di Office che sono in fasi di disponibilità diverse. Per altre informazioni, vedere la sezione **Oggi dov'è disponibile questa funzionalità?** in [Applicare le etichette di riservatezza per i documenti e la posta elettronica in Office](https://support.office.com/en-us/article/apply-sensitivity-labels-to-your-documents-and-email-within-office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9) nella documentazione di Office.
    
- Client di fornitori di software e sviluppatori che usano il [SDK MIP](https://docs.microsoft.com/azure/information-protection/develop/mip/mip-sdk-reference).


## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle etichette migrate che possono ora essere configurate e pubblicate nel Centro sicurezza e conformità di Office 365, vedere [Panoramica delle etichette di riservatezza](/Office365/SecurityCompliance/sensitivity-labels).

Per leggere il post di blog dell'annuncio: [Announcing the availability of unified labeling management in the Security & Compliance Center](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Announcing-the-availability-of-unified-labeling-management-in/ba-p/262492) (Annuncio della disponibilità della gestione dell'etichettatura unificata nel Centro sicurezza e conformità).
