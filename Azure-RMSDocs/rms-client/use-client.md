---
title: Il client per Azure Information Protection-AIP
description: Microsoft Azure Information Protection offre una soluzione client-server che consente di proteggere i dati di un'organizzazione. Il client (di Azure Information Protection o di Rights Management) si integra con le applicazioni che vengono eseguite su computer e dispositivi mobili.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 02/20/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 96a1af247d9c65077be3dc7706cc1976850540fd
ms.sourcegitcommit: 2abde0336bffda66ba7c629bfb5f0525264c3730
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77494877"
---
# <a name="the-client-side-of-azure-information-protection"></a>Lato client di Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, windows server 2019, windows server 2016, windows Server 2012 R2, windows Server 2012*


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

- Usare il **client di assegnazione di etichette incorporato in Office** per i computer Windows quando si dispone di app di Office 365 con una versione minima 1910, si vogliono usare le stesse etichette e le stesse impostazioni dei criteri che possono essere usate anche da MacOS, iOS e Android e non sono necessarie funzionalità nelle app di Office che richiedono il client di etichetta unificato o il client classico. Queste funzionalità includono la barra Information Protection sotto la barra multifunzione per semplificare la selezione e la visibilità delle etichette. 
    
    Questo client supporta il cambio di account e, poiché non usa un componente aggiuntivo di Office, offre prestazioni migliori nelle app di Office rispetto all'uso di uno dei client Azure Information Protection. Poiché l'assegnazione di etichette è incorporata in Office, non è prevista alcuna installazione e manutenzione separate per questo client di assegnazione di etichette. Inoltre, diversamente da un componente aggiuntivo di Office, non può essere disabilitato.

- Usare la **Azure Information Protection client di assegnazione di etichette unificata** nei computer Windows per le etichette e le impostazioni dei criteri che possono essere usate anche da MacOS, iOS e Android, si vuole etichettare i file in modo indipendente dalle app di Office 365 e non sono necessarie funzionalità che sono supportate solo dal client classico. Queste funzionalità includono attualmente la protezione del contenuto con una chiave locale (HYOK) e una versione di disponibilità generale dello scanner per gli archivi dati locali.

- Installare il **client di Azure Information Protection (classico)** nei computer Windows se è necessaria una versione del client con funzionalità che non sono ancora disponibili con il client di etichettatura unificata. Sebbene questo client possa usare le stesse etichette usate da MacOS, iOS e Android, presenta impostazioni di criteri diverse. Quindi, il compromesso è l'amministrazione usando un altro portale di gestione e un'esperienza utente diversa per gli utenti.

La versione più recente del client Unified Labeling consente di chiudere la parità nelle funzionalità con il client classico. Quando questo gap si chiude, è possibile aspettarsi che vengano aggiunte nuove funzionalità solo al client di etichettatura unificata. Per questo motivo, è consigliabile distribuire il client di etichettatura unificata se il set di funzionalità e le funzionalità correnti soddisfano i requisiti aziendali. In caso contrario, o se sono state configurate etichette nel portale di Azure di cui non è ancora stata [eseguita la migrazione nell'archivio Unified Labeling](../configure-policy-migrate-labels.md), usare il client classico.

È possibile utilizzare client diversi nello stesso ambiente per supportare requisiti aziendali diversi, come illustrato nel seguente esempio di distribuzione. In un ambiente client misto è consigliabile usare le etichette unificate in modo che i client condividano lo stesso set di etichette per semplificare l'amministrazione. Per impostazione predefinita, i nuovi clienti hanno etichette unificate, perché i tenant si trovano nella piattaforma di etichettatura unificata. Per ulteriori informazioni, vedere [come è possibile determinare se il tenant si trova nella piattaforma di etichettatura unificata?](../faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)

Quando si dispone di un computer Windows che esegue le app di Office 365 che corrispondono alla versione minima 1910 e uno dei client di Azure Information Protection è installato, per impostazione predefinita il client di assegnazione di etichette incorporato è disabilitato nelle app di Office. Tuttavia, è possibile modificare questo comportamento per usare il client di assegnazione di etichette incorporato solo per le app di Office. Con questa configurazione, il client di Azure Information Protection (classica o unificata) rimane disponibile per l'assegnazione di etichette in Esplora file, PowerShell e lo scanner. Per istruzioni su come disabilitare il client Azure Information Protection nelle app di Office 365, vedere la sezione [Office built-in etichettating client and the Azure Information Protection client](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps#office-built-in-labeling-client-and-the-azure-information-protection-client) dalla documentazione di Microsoft 365 Compliance.

##### <a name="example-deployment-strategy"></a>Strategia di distribuzione di esempio:

- Per la maggior parte degli utenti, si distribuisce il Azure Information Protection client Unified Labeling perché questo client soddisfa le esigenze aziendali per questi utenti. 
    
    Per questi utenti, la loro esperienza di etichettatura è molto simile in Windows, Mac, iOS e Android, perché hanno le stesse etichette pubblicate e le stesse impostazioni dei criteri. In qualità di amministratore, le etichette e le impostazioni dei criteri vengono gestite nello stesso centro di gestione.

- Si installa anche il client di assegnazione di etichette unificato per testare la versione di anteprima dello scanner Azure Information Protection.

- Per un subset di utenti, si distribuisce il client classico perché questi utenti richiedono etichette che applicano la protezione HYOK (Holding your own key).
    
    Per questi utenti hanno un'esperienza di etichettatura leggermente diversa quando usano questo client. Ad esempio, viene visualizzato un pulsante **Proteggi** anziché un pulsante di **riservatezza** nelle app di Office. In qualità di amministratore, è necessario gestire le etichette per le impostazioni di HYOK e le impostazioni dei criteri in un centro di gestione diverso per le etichette e le impostazioni per le altre piattaforme client.

- Sono presenti archivi dati locali con documenti che devono essere analizzati per ottenere informazioni riservate oppure classificati e protetti. Per l'uso in produzione, si distribuisce il client classico nei server per eseguire lo scanner Azure Information Protection.

## <a name="compare-the-labeling-clients-for-windows-computers"></a>Confrontare i client di etichettatura per i computer Windows

Usare la tabella seguente per confrontare le funzionalità supportate dai tre client di etichettatura per i computer Windows.

Per confrontare le funzionalità di riservatezza predefinite di Office in diverse piattaforme del sistema operativo (Windows, MacOS, iOS e Android) e per il Web, vedere la documentazione relativa alla conformità del Microsoft 365, [supporto per le funzionalità di etichetta di riservatezza nelle app](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps#support-for-sensitivity-label-capabilities-in-apps). Questa documentazione include anche i numeri di build di Office o le informazioni sul canale di aggiornamento di Office per le funzionalità supportate.

|Funzionalità|Client classico|Client di etichetta unificato|Client di assegnazione di etichette incorporato di Office|
|:------|:------------:|:---------------------:|:-----------------------------:|
|Etichettatura manuale:| **Sì** | **Sì** |**Sì** |
|Etichetta predefinita:| **Sì** | **Sì** | **Sì** |
|Etichettatura consigliata o automatica: <br />-Per Word, Excel, PowerPoint| **Sì** | **Sì** | **Sì** |
|Etichettatura consigliata o automatica:<br />-Per Outlook| **Sì** | **Sì** | No |
|Etichettatura obbligatoria:| **Sì** | **Sì** | No |
|Autorizzazioni definite dall'utente per un'etichetta: <br />-Non trasmettere per i messaggi di posta elettronica| **Sì** | **Sì** | **Sì** |
|Autorizzazioni definite dall'utente per un'etichetta: <br />-Autorizzazioni personalizzate per Word, Excel, PowerPoint, Esplora file| **Sì** | **Sì** | No |
|Supporto multilingue per le etichette:| **Sì** | **Sì** |**Sì** |
|Ereditarietà delle etichette dagli allegati di posta elettronica:| **Sì** | **Sì**  |No |
|Personalizzazioni che includono:<br />- Etichetta predefinita per la posta elettronica<br />-Messaggi popup in Outlook <br />- Supporto S/MIME<br />- Opzione Segnala un problema| **Sì** <sup>1</sup> | **Sì** <sup>2</sup> | No |
|Scanner per gli archivi dati locali:| **Sì** | **Sì <br />(anteprima)** | No |
|Creazione di report centrale (analisi):| **Sì** | **Sì** | No |
|Autorizzazioni personalizzate impostate in modo indipendente da un'etichetta:| **Sì** | **Sì** <sup>3</sup>| No |
|Barra di Information Protection nelle app Office:| **Sì** | **Sì**| No |
|Contrassegni visivi come azione etichetta (intestazione, piè di pagina, filigrana):| **Sì** | **Sì** | **Sì**|
|Contrassegni visivi per app:| **Sì** | **Sì* | No |
|Contrassegni visivi dinamici con variabili:| **Sì** | **Sì** (anteprima) | No |
|Etichetta con Esplora file:| **Sì** | **Sì** | No |
|Un visualizzatore per i file protetti (testo, immagini, PDF, Pfile):| **Sì** | **Sì** | No|
|Supporto di PPDF per l'applicazione di etichette:| **Sì** | No | No |
|Cmdlet per l'assegnazione di etichette di PowerShell:| **Sì** | **Sì** <sup>4</sup> | No |
|Supporto offline per le azioni di protezione:| **Sì** | **Sì** <sup>5</sup> | **Sì** |
|Gestione manuale dei file di criteri per i computer disconnessi:| **Sì** |**Sì**| No |
|Supporto HYOK:| **Sì** | No | No |
|Registrazione dell'utilizzo in Visualizzatore eventi:| **Sì** | No |No |
|Visualizzare il pulsante non trasmettere in Outlook:| **Sì** | No | No |
|Traccia documentata protetta:| **Sì** | **Sì** <sup>6</sup> | No |
|Revocare i documenti protetti:| **Sì** | No | No |
|Modalità di sola protezione (nessuna etichetta):| **Sì** | No | No |
|Supporto per il cambio di account:| No | No | **Sì** |
|Supporto per Servizi Desktop remoto:| **Sì** | **Sì** | **Sì** |
|Supporto per AD RMS:| **Sì** | N. <sup>7</sup> | No |

Note a piè di pagina:

<sup>1</sup> queste impostazioni e molte altre sono supportate come [Impostazioni client avanzate che è possibile configurare nel portale di Azure](client-admin-guide-customizations.md#how-to-configure-advanced-client-configuration-settings-in-the-portal).

<sup>2</sup> queste impostazioni e molte altre sono supportate come [Impostazioni avanzate configurate con PowerShell](clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell).

<sup>3</sup> supportato da Esplora file e PowerShell. Nelle app di Office gli utenti possono selezionare **informazioni sul File** > proteggere il **documento** > **limitare l'accesso**.

<sup>4</sup> nessun supporto per rimuovere la protezione dai file contenitore (zip).

<sup>5</sup> per i comandi di Esplora file e PowerShell, l'utente deve essere connesso a Internet per proteggere i file.

<sup>6</sup> il sito di rilevamento dei documenti supportato dal client classico non è supportato dal client di etichettatura unificata. Tuttavia, senza la necessità di registrare il documento per il rilevamento, gli amministratori possono utilizzare la funzionalità di [creazione di rapporti centrale](../reports-aip.md) per identificare se l'accesso a documenti protetti viene eseguito da computer Windows e se l'accesso è stato concesso o negato. 

<sup>7</sup> le azioni di assegnazione di etichette e protezione non sono supportate. Tuttavia, per una distribuzione AD RMS, il visualizzatore può aprire i documenti protetti quando si usa l' [estensione Active Directory Rights Management Services Mobile Device](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\)).


### <a name="detailed-comparisons-for-the-azure-information-protection-clients"></a>Confronti dettagliati per i client di Azure Information Protection

Quando il client di Azure Information Protection (classico) e il Azure Information Protection client di etichetta unificata supportano entrambe la stessa funzionalità, usare la tabella seguente per identificare alcune differenze funzionali tra i due client.

|Funzionalità |Client classico|Client di etichetta unificato|
|--------------|-----------------------------------|-----------------------------------------------------------|
|Configurazione:| Opzione per installare i criteri demo locali | Nessun criterio demo locale|
|Selezione e visualizzazione di etichette se applicate nelle app Office:|Dal pulsante **Proteggi** nella barra multifunzione <br /><br /> Dalla barra di Information Protection (barra orizzontale sotto la barra multifunzione)|Dal pulsante **Riservatezza** sulla barra multifunzione<br /><br /> Dalla barra di Information Protection (barra orizzontale sotto la barra multifunzione)|
|Gestione della barra di Information Protection nelle app Office:|Per gli utenti: <br /><br />- Opzione per visualizzare o nascondere la barra dal pulsante **Proteggi** sulla barra multifunzione<br /><br />- Quando un utente seleziona l'opzione per nascondere la barra, per impostazione predefinita, la barra viene nascosta in tale app, ma continua a essere automaticamente visualizzata nelle app appena aperte <br /><br /> Per gli amministratori: <br /><br />- Impostazioni dei criteri per visualizzare o nascondere automaticamente la barra quando un'app viene aperta per la prima volta e per controllare se la barra rimane automaticamente nascosta per le app appena aperte dopo che un utente ha selezionato l'opzione per nascondere la barra|Per gli utenti: <br /><br />- Opzione per visualizzare o nascondere la barra dal pulsante **Riservatezza** sulla barra multifunzione<br /><br />- Quando un utente seleziona l'opzione per nascondere la barra, la barra viene nascosta in tale app e anche nelle app appena aperte <br /><br />Per gli amministratori: <br /><br />-Impostazione di PowerShell per gestire la barra |
|Colore dell'etichetta: | Configurazione nel portale di Azure | Conservati dopo la migrazione delle etichette e configurabili con [PowerShell](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)|
|Le etichette supportano lingue diverse:| Configurazione nel portale di Azure | Configurare usando [Office 365 sicurezza e conformità PowerShell](/microsoft-365/compliance/create-sensitivity-labels#additional-label-settings-with-office-365-security--compliance-center-powershell)|
|Aggiornamento criteri: | Quando si apre un'app Office <br /><br /> Quando si fa clic con il pulsante destro del mouse per classificare e proteggere un file o una cartella <br /><br />Quando si eseguono i cmdlet di PowerShell per l'assegnazione di etichette e la protezione<br /><br />Ogni 24 ore <br /><br />Per lo scanner: ogni ora e quando il servizio viene avviato e il criterio è più vecchio di un'ora| Quando si apre un'app Office <br /><br /> Quando si fa clic con il pulsante destro del mouse per classificare e proteggere un file o una cartella <br /><br />Quando si eseguono i cmdlet di PowerShell per l'assegnazione di etichette e la protezione<br /><br />Ogni 4 ore <br /><br />Per lo scanner: ogni 4 ore|
|Formati supportati per PDF:| Protezione: <br /><br /> - Standard ISO per la crittografia dei file PDF (impostazione predefinita) <br /><br /> - Estensione ppdf <br /><br /> Consumo: <br /><br /> - Standard ISO per la crittografia dei file PDF <br /><br />- Estensione ppdf<br /><br />- Protezione IRM SharePoint| Protezione: <br /><br /> - Standard ISO per la crittografia dei file PDF <br /><br /> <br /><br /> Consumo: <br /><br /> - Standard ISO per la crittografia dei file PDF <br /><br />- Estensione ppdf<br /><br />- Protezione IRM SharePoint|
|File protetti in modo generico (con estensione Pfile) aperti con il Visualizzatore:| Il file viene aperto nell'app originale, dove può essere visualizzato, modificato e salvato senza protezione | Il file viene aperto nell'app originale, dove può essere visualizzato e modificato, ma non salvato|
|Cmdlet supportati:| Cmdlet per l'assegnazione di etichette e i cmdlet per la sola protezione | Cmdlet per l'assegnazione di etichette:<br /><br /> Set-AIPFileClassification e set-AIPFileLabel non supportano il parametro *owner* <br /><br /> È inoltre presente un singolo commento "No label to apply" per tutti gli scenari in cui non viene applicata un'etichetta <br /><br /> Set-AIPFileClassification supporta il parametro *whatIf* , in modo che possa essere eseguito in modalità di individuazione <br /><br /> Set-AIPFileLabel non supporta il parametro *EnableTracking* <br /><br /> Get-AIPFileStatus non restituisce informazioni sulle etichette da altri tenant e non visualizza il parametro *RMSIssuedTime*<br /><br />Inoltre, il parametro *LabelingMethod* per Get-AIPFileStatus Visualizza **Privileged** o **standard** anziché **Manual** o **Automatic**. Per altre informazioni, vedere la [documentazione online](/powershell/module/azureinformationprotection/get-aipfilestatus).|
|Richieste di giustificazione (se configurate) per ogni azione in Office: | Frequenza: per file <br /><br /> Riduzione del livello di riservatezza <br /><br /> Rimozione di un'etichetta<br /><br /> Rimozione della protezione | Frequenza: per sessione <br /><br /> Riduzione del livello di riservatezza<br /><br /> Rimozione di un'etichetta|
|Azioni di rimozione di etichette applicate: | Viene chiesta conferma all'utente <br /><br />L'etichetta predefinita o l'etichetta automatica (se configurata) non viene applicata automaticamente alla successiva apertura del file nell'app Office  <br /><br />| Non viene chiesta conferma all'utente<br /><br /> L'etichetta predefinita o l'etichetta automatica (se configurata) viene applicata automaticamente alla successiva apertura del file nell'app Office|
|Etichette automatiche e consigliate: | Configurata come [condizioni per le etichette](../configure-policy-classification.md) nel portale di Azure con i tipi di informazioni predefiniti e le condizioni personalizzate che usano frasi o espressioni regolari <br /><br />Le opzioni di configurazione possibili sono: <br /><br />- Conteggio univoco/non univoco <br /><br /> - Conteggio minimo| Configurata nei centri di amministrazione con i tipi di informazioni riservate predefiniti e i [tipi di informazioni personalizzati](https://docs.microsoft.com/microsoft-365/compliance/create-a-custom-sensitive-information-type)<br /><br />Le opzioni di configurazione possibili sono:  <br /><br />- Solo conteggio univoco <br /><br />- Conteggio minimo e massimo <br /><br />- Supporto di AND e OR con i tipi di informazioni <br /><br />- Dizionario di parole chiave<br /><br />- Livello di attendibilità e prossimità dei caratteri personalizzabili|
|Supporto degli ordini per le etichette secondarie sugli allegati: | Abilitato con un' [impostazione client avanzata](client-admin-guide-customizations.md#enable-order-support-for-sublabels-on-attachments) | Abilitata per impostazione predefinita, nessuna configurazione richiesta|
|Modificare il comportamento di protezione predefinito per i tipi di file: | È possibile utilizzare le [modifiche del registro di sistema](client-admin-guide-file-types.md#changing-the-default-protection-level-of-files) per eseguire l'override delle impostazioni predefinite di protezione nativa e generica | È possibile usare [PowerShell](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect) per modificare i tipi di file che vengono protetti|

Per un confronto dettagliato delle differenze di comportamento per specifiche impostazioni di protezione, vedere [confronto tra il comportamento delle impostazioni di protezione per un'etichetta](../configure-policy-migrate-labels.md#comparing-the-behavior-of-protection-settings-for-a-label).

### <a name="features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client"></a>Funzionalità non previste nel client di Azure Information Protection Unified Labeling

Anche se il Azure Information Protection client di assegnazione unificata di etichette è ancora in fase di sviluppo, le seguenti funzionalità e differenze di comportamento rispetto al client classico non sono attualmente pianificate per essere disponibili nelle versioni future per il client Unified Labeling: 

- Autorizzazioni personalizzate come [opzione separata che gli utenti possono selezionare nelle app di Office: Word, Excel e PowerPoint](client-classify-protect.md#set-custom-permissions-for-a-document)

- [Rilevare e revocare le](client-track-revoke.md) opzioni dalle app di Office e da Esplora file

- Titolo e descrizione comando della barra di Information Protection

- [Modalità di sola protezione](client-protection-only-mode.md) (nessuna etichetta) tramite i modelli

- Proteggi documento PDF come file con [estensione Ppdf (formato precedente)](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)

- Visualizzazione del pulsante Non inoltrare in Outlook

- Criteri demo

- Giustificazione per la rimozione della protezione

- Richiesta **di conferma eliminare questa etichetta?** per gli utenti se non si usa l'impostazione dei criteri per la giustificazione

- Separazione dei cmdlet PowerShell per la connessione a un servizio Rights Management


### <a name="parent-labels-and-their-sublabels"></a>Etichette padre ed etichette secondarie 

Il client Azure Information Protection (classico) non supporta le configurazioni che specificano un'etichetta padre con etichette secondarie. Queste configurazioni includono la specifica di un'etichetta predefinita e un'etichetta per la classificazione consigliata o automatica. Quando un'etichetta ha etichette secondarie, è possibile specificare una delle etichette secondarie, ma non l'etichetta padre.

Per motivi di parità, nemmeno il client per l'etichettatura unificata di Azure Information Protection supporta l'applicazione di etichette padre con etichette secondarie, anche se è possibile selezionare queste etichette nei centri di amministrazione. In questo scenario il client di etichettatura unificata Azure Information Protection non applicherà l'etichetta padre.

## <a name="next-steps"></a>Passaggi successivi

Per installare e configurare i client di Azure Information Protection, utilizzare la seguente documentazione:

- [Client di Azure Information Protection](AIP-client.md)

- [Client per l'etichettatura unificata Azure Information Protection](unifiedlabelingclient-version-release-history.md)

Per altre informazioni sull'uso del client di assegnazione di etichette incorporato per le app di Office 365, vedere [etichette di riservatezza nelle app di Office](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps).
