---
title: 'Esercitazione: migrazione dal client classico al client di etichettatura unificata di Azure Information Protection (AIP)'
description: Esercitazione dettagliata per la migrazione dal client classico al client di etichettatura unificata di Azure Information Protection (AIP).
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 10/19/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 746e1a8763c94a3193b7719d5af9326c2d274347
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/29/2020
ms.locfileid: "97805921"
---
# <a name="tutorial-migrating-from-the-azure-information-protection-aip-classic-client-to-unified-labeling-solution"></a>Esercitazione: migrazione dal client classico alla soluzione di etichettatura unificata di Azure Information Protection (AIP)

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> ***Rilevante per**: [Client classico Azure Information Protection per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

> [!NOTE]
> Per offrire un'esperienza per i clienti unificata e semplificata, il client classico di Azure Information Protection e Gestione etichette nel portale di Azure saranno deprecati a partire dal 31 marzo 2021.
> 
> In questo intervallo di tempo tutti i clienti correnti del client classico di Azure Information Protection potranno passare all'etichettatura unificata di AIP che usa la soluzione di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).
>

Questa esercitazione illustra come eseguire la migrazione della distribuzione di Azure Information Protection dell'organizzazione, nonché delle etichette e della gestione dei criteri di etichettatura nel portale di Azure, dal client classico alla soluzione di etichettatura unificata e alle [etichette di riservatezza di Microsoft 365](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels).

**Tempo necessario**: il tempo necessario per completare una migrazione dipende dalla complessità dei criteri e dalle funzionalità AIP usate. È possibile continuare a lavorare con il client classico mentre si esegue la migrazione in background.

Questa esercitazione fornisce una descrizione generale di ogni passaggio, quindi fa riferimento alla sezione pertinente nella documentazione di Microsoft per altri dettagli.

In questa esercitazione si apprenderà come:
> [!div class="checklist"]
> * Informazioni sulla pianificazione della migrazione
> * Eseguire la migrazione delle etichette alla piattaforma di etichettatura unificata
> * Informazioni su come configurare le impostazioni avanzate nella nuova interfaccia di amministrazione dell'etichettatura
> * Copiare i criteri nella piattaforma di etichettatura unificata
> * Distribuire il client di etichettatura unificata

## <a name="why-migrate-to-the-unified-labeling-solution"></a>Perché eseguire la migrazione alla soluzione di etichettatura unificata?

Oltre al fatto che [è prevista la deprecazione del client classico](https://aka.ms/aipclassicsunset), la migrazione alla soluzione di etichettatura unificata consente di proteggere in modo efficace i dati sensibili nelle proprietà digitali. Una volta eseguita la migrazione, usare Microsoft Information Protection (MIP) nei servizi cloud di Microsoft 365, in locale, in applicazioni SaaS di terze parti e altro ancora.

MIP supporta servizi di etichettatura predefiniti per molte funzionalità di protezione delle informazioni di base, consentendo di riservare l'utilizzo del client solo per funzionalità aggiuntive non supportate dalle funzionalità di etichettatura predefinite.

- **Ridurre i costi di manutenzione**, grazie alla possibilità di distribuire e gestire meno software aggiuntivo
- **Aumentare le prestazioni di Office**, senza la necessità di ulteriori componenti aggiuntivi
- **Semplificare la gestione dei criteri di etichettatura e protezione** per AIP, Office 365 e Windows, usando l'interfaccia di amministrazione dell'etichettatura. 

    Le interfacce di amministrazione supportate includono il Centro conformità di Microsoft 365, il Centro sicurezza di Microsoft 365 o il Centro sicurezza e conformità di Microsoft 365.

Per altre informazioni, vedere il post di blog [Understanding unified labeling migration](https://techcommunity.microsoft.com/t5/microsoft-security-and/understanding-unified-labeling-migration/ba-p/783185) (Informazioni sulla migrazione all'etichettatura unificata).

## <a name="planning-your-migration"></a>Pianificazione della migrazione

Sebbene la maggior parte delle funzionalità disponibili per il client classico di AIP sia disponibile anche per il client di etichettatura unificata, alcune funzionalità non sono ancora completamente disponibili e alcune sono configurate in modo diverso per l'etichettatura unificata.

Leggere gli articoli seguenti per comprendere il modo in cui le funzionalità di Information Protection usate possono essere diverse nel client di etichettatura unificata:

- [Informazioni sulle funzionalità di etichettatura predefinite in Microsoft 365](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps)
- [Confrontare le soluzioni di etichettatura per i computer Windows](rms-client/use-client.md#compare-the-labeling-solutions-for-windows-computers)
- [Informazioni su come gestire le impostazioni delle etichette non supportate per impostazione predefinita nelle interfacce di amministrazione dell'etichettatura unificata](configure-policy-migrate-labels.md#label-settings-that-are-not-supported-in-the-admin-centers)

> [!TIP]
> Se sono presenti differenze documentate tra i client con effetti sul comportamento degli utenti finali, è consigliabile comunicare tali modifiche in modo efficace agli utenti prima di distribuire il client di etichettatura unificata e pubblicare i nuovi criteri.

Dopo aver pianificato la migrazione e compreso le modifiche che si verificheranno, continuare con [Migrazione delle etichette alla piattaforma di etichettatura unificata](#migrating-labels-to-the-unified-labeling-platform).

## <a name="migrating-labels-to-the-unified-labeling-platform"></a>Migrazione delle etichette alla piattaforma di etichettatura unificata

Dopo aver pianificato la migrazione e valutato come gestire le differenze nei client, si è pronti per attivare l'etichettatura unificata ed eseguire la migrazione delle etichette.

Durante la migrazione, è possibile continuare a usare il client classico di AIP e i criteri nell'area Azure Information Protection del portale di Azure. I due client possono funzionare affiancati senza alcuna configurazione aggiuntiva.

1. Accedere al [portale di Azure](https://portal.azure.com) come amministratore con uno dei ruoli seguenti:

    - **Amministratore di conformità**
    - **Amministratore dati di conformità**
    - **Amministratore della sicurezza**
    - **Amministratore globale**
    

1. Nell'area Azure Information Protection, in **Gestisci** a sinistra, selezionare **Etichettatura unificata**.

    Nella parte superiore della pagina selezionare :::image type="icon" source="media/qs-tutor/activate.PNG" border="false"::: **Attiva** per attivare l'etichettatura unificata.

    Le etichette vengono copiate da Azure Information Protection alla piattaforma di etichettatura unificata e sono ora archiviate in entrambi i sistemi.

    Aprire l'interfaccia di amministrazione dell'etichettatura per confrontare le etichette visualizzate in tale interfaccia e nell'area Azure Information Protection. I due elenchi devono essere identici. Ad esempio, quando si esegue il confronto con il Centro sicurezza e conformità di Microsoft 365:

    :::image type="content" source="media/qs-tutor/compare-migrated-labels-small.png" alt-text="Confrontare le etichette migrate tra il portale di Azure e il Centro sicurezza e conformità" lightbox="media/qs-tutor/compare-migrated-labels.png":::

    > [!NOTE]
    > Se necessario, continuare a usare le etichette in entrambi i sistemi fino a quando non viene completata la migrazione. Per altre informazioni, vedere [Sincronizzazione delle modifiche alle etichette](#synchronizing-labeling-edits).

Continuare con [Copiare i criteri nella piattaforma di etichettatura unificata](#copy-policies-to-the-unified-labeling-platform).

### <a name="synchronizing-labeling-edits"></a>Sincronizzazione delle modifiche alle etichette

Dopo aver eseguito la migrazione delle etichette nell'interfaccia di amministrazione dell'etichettatura, inclusi il Centro sicurezza di Microsoft 365, il Centro conformità di Microsoft 365 o il Centro sicurezza e conformità di Microsoft 365, le eventuali modifiche apportate alle etichette migrate nel portale di Azure vengono sincronizzate automaticamente con la stessa etichetta nell'interfaccia di amministrazione per l'etichettatura unificata.

Tuttavia, le modifiche apportate alle etichette migrate nell'interfaccia di amministrazione *non* vengono sincronizzate nel portale di Azure. Se si apportano modifiche nell'interfaccia di amministrazione ed è necessario aggiornarle nel portale di Azure, tornare al portale per pubblicare l'aggiornamento.

**Per pubblicare un'etichetta aggiornata nel portale di Azure**:

1. Nell'area Azure Information Protection, in **Gestisci** a sinistra, selezionare **Etichettatura unificata**.

1. Selezionare :::image type="icon" source="media/i-publish.PNG" border="false"::: **Pubblica**. 

> [!NOTE]
> Questo passaggio è necessario solo se sono state apportate modifiche alle etichette migrate nella piattaforma di etichettatura unificata ed è necessario sincronizzarle nel portale di Azure. 

### <a name="migrating-labels-via-powershell"></a>Migrazione di etichette tramite PowerShell

È anche possibile usare PowerShell per eseguire la migrazione delle etichette esistenti, ad esempio per un ambiente GCC High.

Usare il cmdlet [New-Label](/powershell/module/exchange/new-label) per eseguire la migrazione delle etichette di riservatezza esistenti.

Ad esempio, se l'etichetta di riservatezza include la crittografia, è possibile usare il cmdlet **New-Label** come segue:

```PowerShell
New-Label -Name 'aipscopetest' -Tooltip 'aipscopetest' -Comment 'admin notes' -DisplayName 'aipscopetest' -Identity 'b342447b-eab9-ea11-8360-001a7dda7113' -EncryptionEnabled $true -EncryptionProtectionType 'template' -EncryptionTemplateId 'a32027d7-ea77-4ba8-b2a9-7101a4e44d89' -EncryptionAipTemplateScopes "['allcompany@labelaction.onmicrosoft.com','admin@labelaction.onmicrosoft.com']"
```

Per altre informazioni sull'utilizzo degli ambienti GCC, GCC-High e DoD, vedere [Descrizione del servizio Azure Information Protection Premium per enti pubblici](/enterprise-mobility-security/solutions/ems-aip-premium-govt-service-description#label-migration). 

## <a name="copy-policies-to-the-unified-labeling-platform"></a>Copiare i criteri nella piattaforma di etichettatura unificata

Copiare tutti i criteri archiviati nel portale di Azure che si vuole siano disponibili nella piattaforma di etichettatura unificata.

Questa funzionalità è attualmente disponibile in ANTEPRIMA. Le [condizioni aggiuntive per l'anteprima di Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) includono termini legali aggiuntivi che si applicano a funzionalità di Azure in versione beta, anteprima o diversamente non ancora disponibili a livello generale.

> [!NOTE]
> La copia dei criteri presenta alcune limitazioni. È anche possibile iniziare da zero e creare i criteri manualmente nell'interfaccia di amministrazione dell'etichettatura. Per altre informazioni, vedere la [documentazione di Microsoft 365](https://docs.microsoft.com/microsoft-365/compliance/create-sensitivity-labels#publish-sensitivity-labels-by-creating-a-label-policy).
> 

**Per copiare i criteri**: 

1. Valutare le considerazioni seguenti e confermare che si vogliono effettivamente copiare i criteri:

    |Considerazioni  |Descrizione  |
    |---------|---------|
    |**La copia di criteri copia *tutti* i criteri**     |     La copia dei criteri non supporta solo la copia di criteri specifici, ovvero vengono copiati tutti o nessuno.   |
    |**La copia automatica pubblica i criteri**     |  La copia automatica dei criteri nel client di etichettatura unificata li pubblica automaticamente in tutti i client supportati di etichettatura unificata. <br /><br />   **Importante**: non copiare i criteri se non si vuole pubblicarli.     |
    |**La copia sovrascrive i criteri esistenti con lo stesso nome**     |   Se nell'interfaccia di amministrazione sono già presenti criteri con lo stesso nome, la copia dei criteri sovrascriverà le impostazioni definite in tali criteri.   <br /><br />Tutti i criteri copiati dal portale di Azure vengono denominati con la sintassi seguente: `AIP_<policy name>`.    |
    |**Alcune impostazioni client non vengono copiate**     | Alcune impostazioni client non vengono copiate nella piattaforma di etichettatura unificata e devono essere configurate manualmente dopo la migrazione. <br /><br />Per altre informazioni, vedere [Configurazione delle opzioni di etichettatura avanzate](#configuring-advanced-labeling-settings)|
    | | |

1. Accedere al [portale di Azure](https://portal.azure.com) come amministratore con uno dei ruoli seguenti:

    - **Amministratore di conformità**
    - **Amministratore dati di conformità**
    - **Amministratore della sicurezza**
    - **Amministratore globale**


1. Nell'area Azure Information Protection, in **Gestisci** a sinistra, selezionare **Etichettatura unificata**.

1. Selezionare :::image type="icon" source="media/i-copy-policies.PNG" border="false"::: **Copia i criteri (anteprima)** . Tutti i criteri archiviati nel portale di Azure vengono copiati nell'interfaccia di amministrazione.

    Se nell'interfaccia di amministrazione sono già presenti criteri con lo stesso nome, i criteri vengono sovrascritti con le impostazioni del portale di Azure.

    > [!IMPORTANT]
    > Se sono in uso etichette di Microsoft Cloud App Security e Azure Information Protection, verificare di avere pubblicato almeno un criterio con un set minimo di etichette nell'interfaccia di amministrazione dell'etichettatura, anche se il criterio è limitato a un singolo utente. 
    >
    > Questo criterio è necessario per consentire a Microsoft Cloud App Security di identificare tutte le etichette nell'interfaccia di amministrazione dell'etichettatura e visualizzarle nel portale di Microsoft Cloud App Security.

Ora che è stata eseguita la migrazione delle etichette e dei criteri, continuare con [Configurazione delle impostazioni di etichettatura avanzate](#configuring-advanced-labeling-settings) per gestire eventuali configurazioni avanzate di cui non è stata eseguita la migrazione.

## <a name="configuring-advanced-labeling-settings"></a>Configurazione delle impostazioni di etichettatura avanzate

Come spiegato durante la [fase di pianificazione](#planning-your-migration), alcune impostazioni di etichettatura avanzate non vengono incluse automaticamente nella migrazione e devono essere riconfigurate per la piattaforma di etichettatura unificata.

Per altre informazioni, vedere:

- [Configurare le impostazioni di etichettatura avanzate in PowerShell](#configure-advanced-labeling-settings-in-powershell)
- [Definire le condizioni per le etichette nell'interfaccia di amministrazione dell'etichettatura](#define-label-conditions-in-the-labeling-admin-center)

### <a name="configure-advanced-labeling-settings-in-powershell"></a>Configurare le impostazioni di etichettatura avanzate in PowerShell

1. Connettersi al modulo di PowerShell per Centro sicurezza e conformità di Office 365. Per altre informazioni, vedere la [documentazione di PowerShell per il Centro sicurezza e conformità](https://docs.microsoft.com/powershell/exchange/connect-to-scc-powershell).

1. Per definire un'impostazione di etichetta avanzata, usare il cmdlet **Set-Label** specificando il parametro **AdvancedSettings**, l'etichetta a cui si vuole applicare l'impostazione, nonché le coppie chiave/valore per definire l'impostazione.
    
    Usare la sintassi seguente:

    ```PowerShell
    Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{<Key>="<value1>,<value2>"}
    ```

    Dove:
    - **`<LabelGUIDorName>`** identifica l'etichetta usando il nome o il GUID dell'etichetta
    - **`<Key>`** è la chiave o il nome dell'impostazione avanzata che si vuole definire
    - **`<Value>`** è il valore dell'impostazione che si vuole definire. Racchiudere il valore tra virgolette e usare le virgole per separare più valori. Gli spazi vuoti non sono supportati.

1. Per iniziare, configurare le impostazioni avanzate seguenti:

    - [Specificare un colore per l'etichetta](rms-client/clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)
    - [Specificare un'etichetta secondaria predefinita per un'etichetta padre](rms-client/clientv2-admin-guide-customizations.md#specify-a-default-sublabel-for-a-parent-label)
    - [Configurare un'etichetta per applicare la protezione S/MIME in Outlook](rms-client/clientv2-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)
    - [Definire le etichette usando proprietà personalizzate](rms-client/clientv2-admin-guide-customizations.md#migrate-labels-from-secure-islands-and-other-labeling-solutions) 
    - [Definire traduzioni per le etichette](https://docs.microsoft.com/powershell/module/exchange/set-label). 

    Per altre informazioni sulle configurazioni avanzate disponibili, vedere [Guida dell'amministratore: Configurazioni personalizzate per il client di etichettatura unificata di Azure Information Protection](rms-client/clientv2-admin-guide-customizations.md).

> [!NOTE]
> Per sfruttare le impostazioni definite per la piattaforma di etichettatura unificata, gli utenti finali devono avere installato il client di etichettatura unificata nei propri computer. 
>
> Queste impostazioni avanzate non sono disponibili per gli utenti che usano solo la funzionalità di etichettatura predefinita di Office 365.
> 

### <a name="define-label-conditions-in-the-labeling-admin-center"></a>Definire le condizioni per le etichette nell'interfaccia di amministrazione dell'etichettatura

Le condizioni di etichettatura unificata offrono maggiore flessibilità e maggiore accuratezza rispetto alle controparti create nel portale di Azure. 

Per sfruttare la funzionalità per le condizioni di etichettatura unificata, creare manualmente le condizioni di etichettatura nell'interfaccia di amministrazione dell'etichettatura, ovvero in:

- Centro conformità di Microsoft 365
- Centro sicurezza di Microsoft 365
- Centro sicurezza e conformità di Microsoft 365

Per altre informazioni, vedere [Operazioni eseguibili dalle etichette di riservatezza](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels#what-sensitivity-labels-can-do) nella documentazione di Microsoft 365.

> [!TIP]
> Se sono stati creati tipi di informazioni sensibili personalizzati per l'uso con Office 365 DLP o Microsoft Cloud App Security, applicarli senza modifiche all'etichettatura unificata. Per altre informazioni, vedere la [documentazione di Microsoft 365](https://docs.microsoft.com/microsoft-365/compliance/apply-sensitivity-label-automatically).
>  

## <a name="deploy-a-unified-labeling-client"></a>Distribuire un client di etichettatura unificata

Distribuire un client che supporta l'etichettatura unificata nei computer degli utenti per assicurarsi che siano in grado di usare le etichette e i criteri di etichettatura unificata. 

È necessario che gli utenti dispongano di un client supportato in grado di connettersi all'interfaccia di amministrazione dell'etichettatura ed effettuare il pull dei criteri di etichettatura unificata. 

Per altre informazioni, vedere:
- [Piattaforme non Windows](#non-windows-platforms)
- [piattaforme Windows](#windows-platforms)
- [Differenze per gli utenti finali del client classico](#what-changes-for-classic-client-end-users)

### <a name="non-windows-platforms"></a>Piattaforme non Windows

Per gli utenti di piattaforme non Windows, le funzionalità di etichettatura unificata sono integrate direttamente nei client Office e tutte le etichette pubblicate sono utilizzabili immediatamente. 

I client Office con funzionalità integrate per l'etichettatura unificata includono: 

- Client Office per macOS
- Office per il Web (anteprima)
- Outlook Web App
- Outlook per dispositivi mobili

Per altre informazioni sull'etichettatura unificata in queste piattaforme, vedere [Applicare etichette di sensitività ai file e alla posta elettronica in Office](https://support.microsoft.com/office/apply-sensitivity-labels-to-your-files-and-email-in-office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9) nel sito del supporto tecnico Microsoft. 

### <a name="windows-platforms"></a>piattaforme Windows

Per i computer Windows con Microsoft 365 Apps for enterprise, usare il supporto predefinito per l'etichettatura disponibile nelle versioni di Office 1910 e successive oppure installare il client di etichettatura unificata di Azure Information Protection per estendere le funzionalità di AIP a Esplora file o PowerShell.

Per altre informazioni, vedere: 

- [Confrontare le soluzioni di etichettatura per i computer Windows](rms-client/use-client.md#compare-the-labeling-solutions-for-windows-computers)
- [Avvio rapido: Distribuzione del client di etichettatura unificata di Azure Information Protection (AIP)](quickstart-deploy-client.md)

Il client di etichettatura unificata di Azure Information Protection può essere scaricato dall'[Area download Microsoft](https://aka.ms/aipclient). 

Per distribuire il client, assicurarsi di usare il file **AzInfoProtection_UL**. Se nel computer in uso è installato il client classico, l'installazione del client di etichettatura unificata esegue un aggiornamento sul posto.

> [!NOTE]
> Valutare le funzionalità AIP attualmente richieste dall'organizzazione per stabilire quando usare le funzionalità di etichettatura predefinite e quando usare il client di etichettatura unificata. 
>> 

### <a name="what-changes-for-classic-client-end-users"></a>Differenze per gli utenti finali del client classico

La differenza principale e più visibile per gli utenti finali che usano il client classico di Azure Information Protection è che il pulsante **Proteggi** nelle app di Office viene sostituito dal pulsante **Riservatezza**. 

Quando si sfruttano le funzionalità aggiuntive supportate dalle etichette di riservatezza e dall'etichettatura unificata, gli utenti finali visualizzeranno anche queste modifiche nelle app di Office.

Ad esempio:

- **Client classico di Windows AIP**

    :::image type="content" source="media/infoprotect-protectbutton-pulldown.png" alt-text="Pulsante di protezione nel client classico":::

- **Client di etichettatura unificata di Windows AIP**

    :::image type="content" source="media/qs-tutor/sample-aip-client-office.PNG" alt-text="Pulsante di esempio per il client di etichettatura unificata in Microsoft Office":::

> [!TIP]
> Se le etichette sono state pubblicate e i client con supporto incorporato non visualizzano il pulsante **Riservatezza**, vedere la guida alla risoluzione dei problemi appropriata in base alle esigenze.
>
 
## <a name="next-steps"></a>Passaggi successivi

Dopo aver eseguito la migrazione delle etichette, dei criteri e dei client distribuiti in base alle esigenze, continuare [gestendo le etichette e i criteri di etichettatura solo nell'interfaccia di amministrazione dell'etichettatura](https://docs.microsoft.com/microsoft-365/compliance/create-sensitivity-labels), ovvero nel Centro conformità di Microsoft 365, nel Centro sicurezza di Microsoft 365 o nel Centro sicurezza e conformità di Microsoft 365.

Con la piattaforma di etichettatura unificata sarà necessario tornare all'area Azure Information Protection nel portale di Azure per:

- [Usare lo scanner AIP](deploy-aip-scanner.md)
- [Monitorare le attività di etichettatura usando AIP Analytics](reports-aip.md)

Si consiglia agli utenti finali di sfruttare le funzionalità di etichettatura predefinite nelle app di Office più recenti per il Web, Mac, iOS e Android, nonché Microsoft 365 Apps for enterprise. 

Per usare le funzionalità di AIP aggiuntive non ancora supportate dalle funzionalità di etichettatura predefinite, è consigliabile usare il client di etichettatura unificata più recente per Windows.
