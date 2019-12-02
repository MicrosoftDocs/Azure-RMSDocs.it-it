---
title: Il client per Azure Information Protection-AIP
description: Microsoft Azure Information Protection offre una soluzione client-server che consente di proteggere i dati di un'organizzazione. Il client (di Azure Information Protection o di Rights Management) si integra con le applicazioni che vengono eseguite su computer e dispositivi mobili.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 12/01/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: fdc74c7c1366afe17c6c7b6ac02ec63c973b0bce
ms.sourcegitcommit: 488a941642f82e49503b4c2c4216a003be4db054
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/01/2019
ms.locfileid: "74666838"
---
# <a name="the-client-side-of-azure-information-protection"></a>Lato client di Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, windows server 2019, windows server 2016, windows Server 2012 R2, windows Server 2012, windows Server 2008 R2*

Azure Information Protection offre una soluzione client-server che consente di proteggere i documenti e i messaggi di posta elettronica di un'organizzazione:

- Il client può essere il client di assegnazione di etichette incorporato per Office, il client di Azure Information Protection Unified Labeling per Windows, il client di Azure Information Protection (classico) per Windows o il client di Rights Management.
    
    Questi client sono spesso denominati **client di etichettatura di Office**, il client di **etichettatura unificata**, il **client classico**e il **client RMS**, rispettivamente. Indipendentemente dal client utilizzato, si integra con le applicazioni eseguite su computer e dispositivi mobili.

- Il servizio risiede nel cloud o in locale. Il servizio cloud è Azure Information Protection, che usa il servizio Rights Management di Azure per la protezione dei dati. Il servizio locale è Active Directory Rights Management Services, più comunemente noto come AD RMS. 

Tutti questi client si integrano con le applicazioni di Office, ma il client Unified Labeling e il client classico devono essere installati separatamente e supportare funzionalità e componenti aggiuntivi. Ad esempio, questi client includono il supporto per Esplora file, pertanto è possibile classificare e proteggere i file all'esterno di Office. I componenti aggiuntivi includono un visualizzatore per documenti PDF protetti e immagini protette e uno scanner per gli archivi dati locali.

Il client RMS fornisce solo la protezione. Questo client viene installato automaticamente con alcune applicazioni, ad esempio le applicazioni di Office, i client di Azure Information Protection e le applicazioni abilitate per RMS dei fornitori di software. Tuttavia può essere anche [installato da solo](https://www.microsoft.com/en-us/download/details.aspx?id=38396), per supportare la [sincronizzazione dei file tra le librerie protette da IRM e OneDrive for Business](https://support.office.com/article/Deploy-the-new-OneDrive-sync-client-in-an-enterprise-environment-3f3a511c-30c6-404a-98bf-76f95c519668) e per gli sviluppatori che vogliono integrare la protezione di Rights Management nelle applicazioni line-of-business.

## <a name="choose-which-labeling-client-to-use-for-windows-computers"></a>Scegliere il client di assegnazione di etichette da usare per i computer Windows

Laddove possibile, usare uno dei client di assegnazione di etichette perché le etichette astraggono la complessità dell'applicazione della protezione per gli utenti, mentre le etichette forniscono anche la classificazione, in modo che sia possibile tenere traccia e gestire i dati.

La scelta di etichettare il client per i computer Windows potrebbe essere influenzata dal portale di gestione usato:

- Il client di assegnazione di etichette predefinito di Office e le impostazioni dei criteri e delle etichette di Azure Information Protection per il download dei client con etichetta unificata dai centri di amministrazione seguenti: 
    - Office 365 Centro sicurezza e conformità
    - Centro sicurezza Microsoft 365
    - Centro conformità Microsoft 365

- Il client di Azure Information Protection (versione classica) Scarica le impostazioni dell'etichetta e dei criteri dal portale di Azure.

Poiché il client di etichettatura unificata e il client classico richiedono un'installazione separata in Office, è necessario scaricare e installare questi client dall' [area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 

Quale client utilizzare?

- Usare il **client di assegnazione di etichette incorporato in Office** per i computer Windows quando si dispone di app di Office 365 con una versione minima 1910, si vogliono usare le stesse etichette e le stesse impostazioni dei criteri che possono essere usate anche da MacOS, iOS e Android e non sono necessarie funzionalità nelle app di Office che richiedono il client di etichetta unificato o il client classico. Queste funzionalità includono la barra Information Protection sotto la barra multifunzione per semplificare la selezione e la visibilità delle etichette. Questo client supporta il cambio di account e, poiché non usa un componente aggiuntivo di Office, offre prestazioni migliori nelle app di Office rispetto all'uso di uno dei client Azure Information Protection.

- Usare la **Azure Information Protection client di assegnazione di etichette unificata** nei computer Windows per le etichette e le impostazioni dei criteri che possono essere usate anche da MacOS, iOS e Android, si vuole etichettare i file in modo indipendente dalle app di Office 365 e non sono necessarie funzionalità che sono supportate solo dal client classico. Queste funzionalità includono attualmente la protezione del contenuto con una chiave locale (HYOK) e una versione di disponibilità generale dello scanner per gli archivi dati locali.

- Installare il **client di Azure Information Protection (classico)** nei computer Windows se è necessaria una versione del client con funzionalità che non sono ancora disponibili con il client di etichettatura unificata. Sebbene questo client possa usare le stesse etichette usate da MacOS, iOS e Android, presenta impostazioni di criteri diverse. Quindi, il compromesso è l'amministrazione usando un altro portale di gestione e un'esperienza utente diversa per gli utenti.

La versione più recente del client Unified Labeling consente di chiudere la parità nelle funzionalità con il client classico. Quando questo gap si chiude, è possibile aspettarsi che vengano aggiunte nuove funzionalità solo al client di etichettatura unificata. Per questo motivo, è consigliabile distribuire il client di etichettatura unificata se il set di funzionalità e le funzionalità correnti soddisfano i requisiti aziendali. In caso contrario, o se sono state configurate etichette nel portale di Azure di cui non è ancora stata [eseguita la migrazione nell'archivio Unified Labeling](../configure-policy-migrate-labels.md), usare il client classico.

È possibile utilizzare client diversi nello stesso ambiente per supportare requisiti aziendali diversi, come illustrato nel seguente esempio di distribuzione. In un ambiente client misto è consigliabile usare le etichette unificate in modo che i client condividano lo stesso set di etichette per semplificare l'amministrazione. Per impostazione predefinita, i nuovi clienti hanno etichette unificate, perché i tenant si trovano nella piattaforma di etichettatura unificata. Per ulteriori informazioni, vedere [come è possibile determinare se il tenant si trova nella piattaforma di etichettatura unificata?](../faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)

Quando si dispone di un computer Windows che esegue le app di Office 365 che corrispondono alla versione minima 1910 e uno dei client di Azure Information Protection è installato, per impostazione predefinita il client di assegnazione di etichette incorporato è disabilitato nelle app di Office. Tuttavia, è possibile modificare questo comportamento per usare il client di assegnazione di etichette incorporato solo per le app di Office. Con questa configurazione, il client di Azure Information Protection (classica o unificata) rimane disponibile per l'assegnazione di etichette in Esplora file, PowerShell e lo scanner. Per istruzioni su come disabilitare il client Azure Information Protection nelle app di Office 365, vedere la sezione le [etichette di riservatezza vengono eseguite insieme al client di Azure Information Protection in Office per Windows?](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps#can-sensitivity-labels-run-alongside-the-azure-information-protection-client-in-office-for-windows) dalla documentazione di Office.

##### <a name="example-deployment-strategy"></a>Strategia di distribuzione di esempio:

- Per la maggior parte degli utenti, si distribuisce il Azure Information Protection client Unified Labeling perché questo client soddisfa le esigenze aziendali per questi utenti. 
    
    Per questi utenti, la loro esperienza di etichettatura è molto simile in Windows, Mac, iOS e Android, perché hanno le stesse etichette pubblicate e le stesse impostazioni dei criteri. In qualità di amministratore, le etichette e le impostazioni dei criteri vengono gestite nello stesso centro di gestione.

- Si installa anche il client di assegnazione di etichette unificato per testare la versione di anteprima dello scanner Azure Information Protection.

- Per un subset di utenti, si distribuisce il client classico perché questi utenti richiedono etichette che applicano la protezione HYOK (Holding your own key).
    
    Per questi utenti hanno un'esperienza di etichettatura leggermente diversa quando usano questo client. Ad esempio, viene visualizzato un pulsante **Proteggi** anziché un pulsante di **riservatezza** nelle app di Office. In qualità di amministratore, è necessario gestire le etichette per le impostazioni di HYOK e le impostazioni dei criteri in un centro di gestione diverso per le etichette e le impostazioni per le altre piattaforme client.

- Sono presenti archivi dati locali con documenti che devono essere analizzati per ottenere informazioni riservate oppure classificati e protetti. Per l'uso in produzione, si distribuisce il client classico nei server per eseguire lo scanner Azure Information Protection.

## <a name="compare-the-labeling-clients-for-windows-computers"></a>Confrontare i client di etichettatura per i computer Windows

Usare la tabella seguente per confrontare le funzionalità supportate dai tre client di etichettatura per i computer Windows.

Per confrontare le funzionalità di riservatezza predefinite di Office per le diverse piattaforme del sistema operativo (Windows, MacOS, iOS e Android) e per il Web, vedere la documentazione di Office, [quali funzionalità dell'etichetta di riservatezza sono supportate in Office oggi?](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps#what-sensitivity-label-capabilities-are-supported-in-office-today)

|Funzionalità|Classic client|Unified labeling client|Client di assegnazione di etichette incorporato di Office|
|:------|:------------:|:---------------------:|:-----------------------------:|
|Etichettatura manuale:| **Sì** | **Sì** |**Sì** |
|Etichetta predefinita:| **Sì** | **Sì** | **Sì** |
|Etichettatura consigliata o automatica:| **Sì** | **Sì** | No |
|Etichettatura obbligatoria:| **Sì** | **Sì** | No |
|Autorizzazioni definite dall'utente per un'etichetta:<br />-Non trasmettere per i messaggi di posta elettronica<br />-Autorizzazioni personalizzate per Word, Excel, PowerPoint, Esplora file| **Sì** | **Sì** | No |
|Supporto multilingue per le etichette:| **Sì** | **Sì** |**Sì** |
|Ereditarietà delle etichette dagli allegati di posta elettronica:| **Sì** | **Sì**  |No |
|Personalizzazioni che includono:<br />- Etichetta predefinita per la posta elettronica<br />-Messaggi popup in Outlook <br />- Supporto S/MIME<br />- Opzione Segnala un problema| **Sì** <sup>1</sup> | **Sì** <sup>2</sup> | No |
|Scanner per gli archivi dati locali:| **Sì** | **Sì <br />(anteprima)** | No |
|Creazione di report centrale (analisi):| **Sì** | **Sì** | No |
|Autorizzazioni personalizzate impostate in modo indipendente da un'etichetta:| **Sì** | **Sì** <sup>3</sup>| No |
|Barra di Information Protection nelle app Office:| **Sì** | **Sì**| No |
|Contrassegni visivi come azione etichetta (intestazione, piè di pagina, filigrana):| **Sì** | **Sì** | **Sì**|
|Contrassegni visivi per app:| **Sì** | No | No |
|Contrassegni visivi dinamici con variabili:| **Sì** | No | No |
|Etichetta con Esplora file:| **Sì** | **Sì** | No |
|Un visualizzatore per i file protetti (testo, immagini, PDF, Pfile):| **Sì** | **Sì** | No|
|Supporto di PPDF per l'applicazione di etichette:| **Sì** | No | No |
|Cmdlet per l'assegnazione di etichette di PowerShell:| **Sì** | **Sì** <sup>4</sup> | No |
|Supporto offline per le azioni di protezione:| **Sì** | **Sì** <sup>5</sup> | **Sì** |
|Gestione manuale dei file di criteri per i computer disconnessi:| **Sì** |**Sì** <sup>6</sup>| No |
|Supporto HYOK:| **Sì** | No | No |
|Registrazione dell'utilizzo in Visualizzatore eventi:| **Sì** | No |No |
|Visualizzare il pulsante non trasmettere in Outlook:| **Sì** | No | No |
|Traccia documentata protetta:| **Sì** | **Sì** <sup>7</sup> | No |
|Revocare i documenti protetti:| **Sì** | No | No |
|Modalità di sola protezione (nessuna etichetta):| **Sì** | No | No |
|Supporto per il cambio di account:| No | No | **Sì** |
|Supporto per AD RMS:| **Sì** | Nessun <sup>8</sup> | No |

Note a piè di pagina:

<sup>1</sup> queste impostazioni e molte altre sono supportate come [Impostazioni client avanzate che è possibile configurare nel portale di Azure](client-admin-guide-customizations.md#how-to-configure-advanced-client-configuration-settings-in-the-portal).

<sup>2</sup> queste impostazioni e molte altre sono supportate come [Impostazioni avanzate configurate con PowerShell](clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell).

<sup>3</sup> supportato da Esplora file e PowerShell. In Office apps, users can select **File Info** > **Protect Document** > **Restrict Access**.

<sup>4</sup> No support to remove protection from container files (zip, .rar, .7z, .msg, and .pst).

<sup>5</sup> For File Explorer and PowerShell commands, the user must be connected to the internet to protect files.

<sup>6</sup> Supported for labeling with File Explorer, PowerShell, and the scanner. Not supported for labeling in Office apps.

<sup>7</sup> The document tracking site that's supported by the classic client isn't supported by the unified labeling client. However, without the need to first register the document for tracking, administrators can use [central reporting](../reports-aip.md) to identify whether protected documented are accessed from Windows computers, and whether access was granted or denied. 

<sup>8</sup> Labeling and protection actions aren't supported. However, for an AD RMS deployment, the viewer can open protected documents when you use the [Active Directory Rights Management Services Mobile Device Extension](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\)).


### <a name="detailed-comparisons-for-the-azure-information-protection-clients"></a>Detailed comparisons for the Azure Information Protection clients

When the Azure Information Protection client (classic) and the Azure Information Protection unified labeling client both support the same feature, use the following table to help identify some functional differences between the two clients.

|Funzionalità |Classic client|Unified labeling client|
|--------------|-----------------------------------|-----------------------------------------------------------|
|Configurazione:| Opzione per installare i criteri demo locali | Nessun criterio demo locale|
|Selezione e visualizzazione di etichette se applicate nelle app Office:|Dal pulsante **Proteggi** nella barra multifunzione <br /><br /> Dalla barra di Information Protection (barra orizzontale sotto la barra multifunzione)|Dal pulsante **Riservatezza** sulla barra multifunzione<br /><br /> Dalla barra di Information Protection (barra orizzontale sotto la barra multifunzione)|
|Gestione della barra di Information Protection nelle app Office:|Per gli utenti: <br /><br />- Opzione per visualizzare o nascondere la barra dal pulsante **Proteggi** sulla barra multifunzione<br /><br />- Quando un utente seleziona l'opzione per nascondere la barra, per impostazione predefinita, la barra viene nascosta in tale app, ma continua a essere automaticamente visualizzata nelle app appena aperte <br /><br /> Per gli amministratori: <br /><br />- Impostazioni dei criteri per visualizzare o nascondere automaticamente la barra quando un'app viene aperta per la prima volta e per controllare se la barra rimane automaticamente nascosta per le app appena aperte dopo che un utente ha selezionato l'opzione per nascondere la barra|Per gli utenti: <br /><br />- Opzione per visualizzare o nascondere la barra dal pulsante **Riservatezza** sulla barra multifunzione<br /><br />- Quando un utente seleziona l'opzione per nascondere la barra, la barra viene nascosta in tale app e anche nelle app appena aperte <br /><br />Per gli amministratori: <br /><br />- PowerShell setting to manage the bar |
|Colore dell'etichetta: | Configurazione nel portale di Azure | Retained after label migration and configurable with [PowerShell](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)|
|Labels support different languages:| Configurazione nel portale di Azure | Configure by using Office 365 Security & Compliance PowerShell and the *LocaleSettings* parameter for [New-Label](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/new-label?view=exchange-ps) and [Set-Label](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps)|
|Aggiornamento criteri: | Quando si apre un'app Office <br /><br /> Quando si fa clic con il pulsante destro del mouse per classificare e proteggere un file o una cartella <br /><br />Quando si eseguono i cmdlet di PowerShell per l'assegnazione di etichette e la protezione<br /><br />Ogni 24 ore <br /><br />For the scanner: Every hour and when the service starts and the policy is older than one hour| Quando si apre un'app Office <br /><br /> Quando si fa clic con il pulsante destro del mouse per classificare e proteggere un file o una cartella <br /><br />Quando si eseguono i cmdlet di PowerShell per l'assegnazione di etichette e la protezione<br /><br />Ogni 4 ore <br /><br />For the scanner: Every 4 hours|
|Formati supportati per PDF:| Protezione: <br /><br /> - Standard ISO per la crittografia dei file PDF (impostazione predefinita) <br /><br /> - Estensione ppdf <br /><br /> Consumo: <br /><br /> - Standard ISO per la crittografia dei file PDF <br /><br />- Estensione ppdf<br /><br />- Protezione IRM SharePoint| Protezione: <br /><br /> - Standard ISO per la crittografia dei file PDF <br /><br /> <br /><br /> Consumo: <br /><br /> - Standard ISO per la crittografia dei file PDF <br /><br />- Estensione ppdf<br /><br />- Protezione IRM SharePoint|
|Generically protected files (.pfile) opened with the viewer:| File opens in the original app where it can then be viewed, modified, and saved without protection | File opens in the original app where it can then be viewed and modified, but not saved|
|Cmdlet supportati:| Cmdlets for labeling and cmdlets for protection-only | Cmdlets for labeling:<br /><br /> Set-AIPFileClassification and Set-AIPFileLabel don't support the *Owner* parameter <br /><br /> È inoltre presente un singolo commento "No label to apply" per tutti gli scenari in cui non viene applicata un'etichetta <br /><br /> Set-AIPFileClassification supports the *WhatIf* parameter, so it can be run in discovery mode <br /><br /> Set-AIPFileLabel non supporta il parametro *EnableTracking* <br /><br /> Get-AIPFileStatus non restituisce informazioni sulle etichette da altri tenant e non visualizza il parametro *RMSIssuedTime*<br /><br />In addition, the *LabelingMethod* parameter for Get-AIPFileStatus displays **Privileged** or **Standard** instead of **Manual** or **Automatic**. Per altre informazioni, vedere la [documentazione online](/powershell/module/azureinformationprotection/get-aipfilestatus).|
|Richieste di giustificazione (se configurate) per ogni azione in Office: | Frequency: Per file <br /><br /> Riduzione del livello di riservatezza <br /><br /> Rimozione di un'etichetta<br /><br /> Rimozione della protezione | Frequency: Per session <br /><br /> Riduzione del livello di riservatezza<br /><br /> Rimozione di un'etichetta|
|Azioni di rimozione di etichette applicate: | Viene chiesta conferma all'utente <br /><br />L'etichetta predefinita o l'etichetta automatica (se configurata) non viene applicata automaticamente alla successiva apertura del file nell'app Office  <br /><br />| Non viene chiesta conferma all'utente<br /><br /> L'etichetta predefinita o l'etichetta automatica (se configurata) viene applicata automaticamente alla successiva apertura del file nell'app Office|
|Automatic and recommended labels: | Configurata come [condizioni per le etichette](../configure-policy-classification.md) nel portale di Azure con i tipi di informazioni predefiniti e le condizioni personalizzate che usano frasi o espressioni regolari <br /><br />Le opzioni di configurazione possibili sono: <br /><br />- Conteggio univoco/non univoco <br /><br /> - Conteggio minimo| Configurata nei centri di amministrazione con i tipi di informazioni riservate predefiniti e i [tipi di informazioni personalizzati](https://docs.microsoft.com/microsoft-365/compliance/create-a-custom-sensitive-information-type)<br /><br />Le opzioni di configurazione possibili sono:  <br /><br />- Solo conteggio univoco <br /><br />- Conteggio minimo e massimo <br /><br />- Supporto di AND e OR con i tipi di informazioni <br /><br />- Dizionario di parole chiave<br /><br />- Livello di attendibilità e prossimità dei caratteri personalizzabili|
|Customizable policy tip for automatic and recommended labels: | Yes <br /><br />Use the Azure portal to replace the default message to users | No <br /><br /> Although the admin centers have an option to supply a customized policy tip, this option is not currently supported by the unified labeling client|
|Order support for sublabels on attachments: | Enabled with an [advanced client setting](client-admin-guide-customizations.md##enable-order-support-for-sublabels-on-attachments) | Enabled by default, no configuration required|
|Change the default protection behavior for file types: | You can use [registry edits](client-admin-guide-file-types.md#changing-the-default-protection-level-of-files) to override the defaults of native and generic protection | You can use [PowerShell](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect) to change which file types get protected|

For a detailed comparison of behavior differences for specific protection settings, see [Comparing the behavior of protection settings for a label](../configure-policy-migrate-labels.md#comparing-the-behavior-of-protection-settings-for-a-label).

### <a name="features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client"></a>Features not planned to be in the Azure Information Protection unified labeling client

Although the Azure Information Protection unified labeling client is still under development, the following features and behavior differences from the classic client are not currently planned to be available in future releases for the unified labeling client: 

- Support Office apps for disconnected computers with manual policy file management

- Custom permissions as a separate option that users can select in Office apps: Word, Excel, and PowerPoint

- Rilevamento e revoca da app di Office ed Esplora file

- Titolo e descrizione comando della barra di Information Protection

- Protection-only mode (no labels) using templates

- Protezione del documento PDF come formato ppdf

- Visualizzazione del pulsante Non inoltrare in Outlook

- Criteri demo

- Giustificazione per la rimozione della protezione

- Confirmation prompt **Do you want to delete this label?** for users when you don't use the policy setting for justification

- Separazione dei cmdlet PowerShell per la connessione a un servizio Rights Management


### <a name="parent-labels-and-their-sublabels"></a>Etichette padre ed etichette secondarie 

The Azure Information Protection client (classic) doesn't support configurations that specify a parent label that has sublabels. Queste configurazioni includono la specifica di un'etichetta predefinita e un'etichetta per la classificazione consigliata o automatica. Quando un'etichetta ha etichette secondarie, è possibile specificare una delle etichette secondarie, ma non l'etichetta padre.

Per motivi di parità, nemmeno il client per l'etichettatura unificata di Azure Information Protection supporta l'applicazione di etichette padre con etichette secondarie, anche se è possibile selezionare queste etichette nei centri di amministrazione. In questo scenario il client di etichettatura unificata Azure Information Protection non applicherà l'etichetta padre.

## <a name="next-steps"></a>Passaggi successivi

To install and configure the Azure Information Protection clients, use the following documentation:

- [Client di Azure Information Protection](AIP-client.md)

- [Client per l'etichettatura unificata Azure Information Protection](unifiedlabelingclient-version-release-history.md)

For more information about using the built-in labeling client for Office 365 apps, see [Sensitivity labels in Office apps](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps).
