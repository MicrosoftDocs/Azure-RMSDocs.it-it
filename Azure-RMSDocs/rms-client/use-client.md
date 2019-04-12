---
title: Client per Azure Information Protection
description: Microsoft Azure Information Protection offre una soluzione client-server che consente di proteggere i dati di un'organizzazione. Il client (di Azure Information Protection o di Rights Management) si integra con le applicazioni che vengono eseguite su computer e dispositivi mobili.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/05/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a6fa85be-f92a-4e00-9efc-9dbfd4dfbfcb
ms.suite: ems
ms.openlocfilehash: 0762edb3e7960c5700ac8a28d7ae1b62455efbe0
ms.sourcegitcommit: 729b12e1219c6dbf1bb2a6cfa7239f24d1d13cc5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/09/2019
ms.locfileid: "59364607"
---
# <a name="the-client-side-of-azure-information-protection"></a>Lato client di Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Azure Information Protection offre una soluzione client-server che consente di proteggere i documenti e i messaggi di posta elettronica di un'organizzazione:

- Il client, che può essere di Azure Information Protection o di Rights Management, si integra con le applicazioni che vengono eseguite su computer e dispositivi mobili. 

- Il servizio risiede nel cloud (Azure Information Protection, che usa il servizio Azure Rights Management per la protezione dei dati) o in locale (Active Directory Rights Management Services, più comunemente noto come AD RMS). 

Il client Azure Information Protection supporta funzionalità di classificazione e protezione con assegnazione di etichette, oltre alla protezione senza assegnazione di etichette. Questo client si integra con le applicazioni di Office e deve essere installato separatamente.

Il client Rights Management (RMS) viene installato automaticamente con alcune applicazioni, ad esempio le applicazioni di Office, il client Azure Information Protection e applicazioni RMS a cura di fornitori software. Tuttavia può essere anche [installato da solo](https://www.microsoft.com/en-us/download/details.aspx?id=38396), per supportare la [sincronizzazione dei file tra le librerie protette da IRM e OneDrive for Business](https://support.office.com/article/Deploy-the-new-OneDrive-sync-client-in-an-enterprise-environment-3f3a511c-30c6-404a-98bf-76f95c519668) e per gli sviluppatori che vogliono integrare la protezione di Rights Management nelle applicazioni line-of-business.

## <a name="choose-which-azure-information-protection-client-to-use"></a>Scegliere il client Azure Information Protection da usare

Il **client Azure Information Protection** che scarica le etichette e le impostazioni dei criteri dal portale di Azure è disponibile a livello generale e ha una versione di anteprima per il test delle nuove funzionalità e correzioni. Per altre informazioni su queste versioni del client, vedere [Client Azure Information Protection: Cronologia delle versioni e criteri per il supporto](client-version-release-history.md). 

Il **client per l'etichettatura unificata Azure Information Protection** scarica le etichette e le impostazioni dei criteri dai centri di amministrazione: Centro sicurezza e conformità di Office 365, Centro sicurezza Microsoft 365 e Centro conformità Microsoft 365. Questo client è attualmente in anteprima per i test. Per altre informazioni su questa versione del client, vedere [Client per l'etichettatura unificata Azure Information Protection: informazioni di rilascio versione](unifiedlabelingclient-version-release-history.md).

Quale client è opportuno installare?

- Se si esegue la distribuzione nell'ambiente di produzione, usare il client Azure Information Protection disponibile a livello generale.

- Se è in corso la fase di test e valutazione, usare uno dei client di anteprima.
    
    Le versioni di anteprima del client Azure Information Protection e del client di etichettatura unificata Azure Information Protection non offrono attualmente pari funzionalità. Il divario, tuttavia, verrà colmato e verranno aggiunte nuove funzionalità solo al client per l'etichettatura unificata Azure Information Protection. Per questo motivo, è consigliabile eseguire i test con il client per l'etichettatura unificata Azure Information Protection se le funzionalità e il set di funzioni correnti soddisfano i requisiti aziendali. In caso contrario o se nel portale di Azure sono state configurate etichette di cui non è ancora stata eseguita la [migrazione all'archivio etichette unificato](../configure-policy-migrate-labels.md), usare il client Azure Information Protection.

### <a name="feature-comparisons-for-the-clients"></a>Confronto delle funzionalità dei client

Per poter confrontare le funzionalità supportate dalle due versioni di anteprima correnti, usare la tabella seguente.

|Funzionalità|Client Azure Information Protection|Azure Information Protection<br /> Client per l'etichettatura unificata|
|-------|-----------------------------------|----------------------------------------------------|
|Azioni di assegnazione di etichette: manuali, consigliate, automatiche| Sì | Sì |
|Creazione di report centrale (analisi):| Sì | Sì |
|Reimpostazione delle impostazioni ed esportazione dei log:| Sì | Sì |
|Autorizzazioni definite dall'utente:| Sì | Solo per Outlook (Non inoltrare) |
|Autorizzazioni personalizzate:| Sì | Solo Esplora file <br /><br /> In alternativa, nelle app Office gli utenti possono selezionare **Info sul file** > **Proteggi documento** > **Limita accesso** |
|Barra di Information Protection nelle app Office:| Sì | Sì, con limitazioni:<br /><br /> - Nessun titolo o descrizione comando personalizzabile<br /><br /> - Colore dell'etichetta non visualizzato per l'etichetta applicata|
|Le etichette permettono di applicare contrassegni visivi (intestazione, piè di pagina, filigrana):| Sì | Sì, con limitazioni:<br /><br /> - Le intestazioni e i piè di pagina non supportano le variabili per i valori dinamici <br /><br /> - Nessun supporto per l’impostazione di contrassegni visivi diversi per Word, Excel, PowerPoint e Outlook|
|Esplora file, azioni con il pulsante destro del mouse:| Sì | Sì, con limitazioni:<br /><br /> - Non è possibile proteggere i documenti PDF in formato ppdf <br /><br />  - Nessun supporto per la modalità di sola protezione|
|Visualizzatore per i file protetti:| Sì | Sì, con limitazioni:<br /><br /> - Per i file protetti in modo generico (con estensione pfile), a differenza del visualizzatore del client Azure Information Protection, non è possibile salvare le modifiche apportate al file aperto originariamente.|
|Comandi di PowerShell:| Sì | Sì, con limitazioni:<br /><br />- Cmdlet inclusi: [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus), [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification), [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel), [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) <br /><br />- Non sono inclusi i cmdlet che si connettono direttamente a un servizio di protezione|
|Supporto offline per le azioni di protezione:| Sì | Sì, con limitazioni: <br /><br />- Per i comandi di Esplora File e PowerShell, l'utente deve essere connesso a Internet per proteggere i file. |
|Supporto per i computer disconnessi con gestione manuale dei file di criteri:| Sì |No |
|Supporto HYOK:| Sì | No<br /><br /> Le etichette di cui si esegue la migrazione dal portale di Azure e che sono configurate per la protezione HYOK vengono visualizzate dal client per l'etichettatura unificata Azure Information Protection, ma non applicano la protezione. |
|Registrazione dell'utilizzo nel Visualizzatore eventi:| Sì | No|
|Ereditarietà delle etichette dagli allegati di posta elettronica:| Sì | No |
|Visualizzare il pulsante Non inoltrare in Outlook| Sì | No |
|[Personalizzazioni](client-admin-guide-customizations.md#available-advanced-client-settings) che includono:<br />- Etichetta predefinita per la posta elettronica<br />- Abilitazione delle autorizzazioni personalizzate <br />- Supporto S/MIME<br />- Opzione Segnala un problema| Sì | No |
|Scanner per gli archivi dati locali:| Sì | No |
|Tenere traccia e revocare:| Sì | No |
|Modalità di sola protezione (nessuna etichetta):| Sì | No |
|Pulsante Non inoltrare in Outlook:| Sì | No |
|Supporto multilingue:| Sì | No |
|Supporto per AD RMS:| Sì | È supportata solo l'azione seguente:<br /><br /> - Il visualizzatore può aprire i documenti protetti se si distribuisce l'[estensione per dispositivi mobili di Active Directory Rights Management Services](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\))|

#### <a name="functional-comparison-for-the-clients"></a>Confronto funzionale dei client

Quando entrambi i client supportano la stessa funzionalità, usare la tabella seguente per identificare alcune differenze funzionali tra le due versioni di anteprima correnti.

|Funzionalità |Client Azure Information Protection|Azure Information Protection<br /> Client per l'etichettatura unificata|
|--------------|-----------------------------------|-----------------------------------------------------------|
|Configurazione:| Opzione per installare i criteri demo locali | Nessun criterio demo locale|
|Selezione e visualizzazione di etichette se applicate nelle app Office:|Dal pulsante **Proteggi** nella barra multifunzione <br /><br /> Dalla barra di Information Protection (barra orizzontale sotto la barra multifunzione)|Dal pulsante **Riservatezza** sulla barra multifunzione<br /><br /> Dalla barra di Information Protection (barra orizzontale sotto la barra multifunzione)|
|Gestione della barra di Information Protection nelle app Office:|Per gli utenti: <br /><br />- Opzione per visualizzare o nascondere la barra dal pulsante **Proteggi** sulla barra multifunzione<br /><br />- Quando un utente seleziona l'opzione per nascondere la barra, per impostazione predefinita, la barra viene nascosta in tale app, ma continua a essere automaticamente visualizzata nelle app appena aperte <br /><br /> Per gli amministratori: <br /><br />- Impostazioni dei criteri per visualizzare o nascondere automaticamente la barra quando un'app viene aperta per la prima volta e per controllare se la barra rimane automaticamente nascosta per le app appena aperte dopo che un utente ha selezionato l'opzione per nascondere la barra|Per gli utenti: <br /><br />- Opzione per visualizzare o nascondere la barra dal pulsante **Riservatezza** sulla barra multifunzione<br /><br />- Quando un utente seleziona l'opzione per nascondere la barra, la barra viene nascosta in tale app e anche nelle app appena aperte <br /><br />Per gli amministratori: <br /><br />- Nessuna impostazione dei criteri per gestire la barra|
|Colore dell'etichetta: | Configurazione nel portale di Azure | Mantenuto dopo la migrazione delle etichette a Office 365 <br /><br /> Le nuove etichette create nei centri di amministrazione non hanno un colore|
|Aggiornamento criteri: | Quando si apre un'app Office <br /><br /> Quando si fa clic con il pulsante destro del mouse per classificare e proteggere un file o una cartella <br /><br />Quando si eseguono i cmdlet di PowerShell per l'assegnazione di etichette e la protezione<br /><br />Ogni 24 ore | Quando si apre un'app Office <br /><br /> Quando si fa clic con il pulsante destro del mouse per classificare e proteggere un file o una cartella <br /><br />Quando si eseguono i cmdlet di PowerShell per l'assegnazione di etichette e la protezione<br /><br />Ogni 4 ore|
|Formati supportati per PDF:| Protezione: <br /><br /> - Standard ISO per la crittografia dei file PDF (impostazione predefinita) <br /><br /> - Estensione ppdf <br /><br /> Consumo: <br /><br /> - Standard ISO per la crittografia dei file PDF <br /><br />- Estensione ppdf<br /><br />- Protezione IRM SharePoint| Protezione: <br /><br /> - Standard ISO per la crittografia dei file PDF <br /><br /> <br /><br /> Consumo: <br /><br /> - Standard ISO per la crittografia dei file PDF <br /><br />- Estensione ppdf<br /><br />- Protezione IRM SharePoint|
|Cmdlet supportati:| Tutti i cmdlet documentati per [AzureInformatioProtection](/powershell/module/azureinformationprotection) | Set-AIPFileClassification e Set-AIPFileLabel non supportano il parametro *Owner* o le librerie di SharePoint Server <br /><br /> È inoltre presente un singolo commento "No label to apply" per tutti gli scenari in cui non viene applicata un'etichetta <br /><br /> Set-AIPFileLabel non supporta il parametro *EnableTracking* <br /><br /> Get-AIPFileStatus non restituisce informazioni sulle etichette da altri tenant e non visualizza il parametro *RMSIssuedTime*<br /><br />Inoltre, il parametro *LabelingMethod* per Get-AIPFileStatus visualizza **Privileged**, **Standard** o **Auto** invece di **Manual** o **Automatic**. Per altre informazioni, vedere la [documentazione online](/powershell/module/azureinformationprotection/get-aipfilestatus).|
|Richieste di giustificazione (se configurate) per ogni azione in Office: | Frequenza: per ogni file <br /><br /> Riduzione del livello di riservatezza <br /><br /> Rimozione di un'etichetta<br /><br /> Rimozione della protezione | Frequenza: per ogni sessione <br /><br /> Riduzione del livello di riservatezza<br /><br /> Rimozione di un'etichetta|
|Azioni di rimozione di etichette applicate: | Viene chiesta conferma all'utente <br /><br />L'etichetta predefinita o l'etichetta automatica (se configurata) non viene applicata automaticamente alla successiva apertura del file nell'app Office  <br /><br />| Non viene chiesta conferma all'utente<br /><br /> L'etichetta predefinita o l'etichetta automatica (se configurata) viene applicata automaticamente alla successiva apertura del file nell'app Office|
|Classificazione automatica e consigliata: | Configurata come [condizioni per le etichette](../configure-policy-classification.md) nel portale di Azure con i tipi di informazioni predefiniti e le condizioni personalizzate che usano frasi o espressioni regolari <br /><br />Le opzioni di configurazione possibili sono: <br /><br />- Conteggio univoco/non univoco <br /><br /> - Conteggio minimo| Configurata nei centri di amministrazione con i tipi di informazioni riservate predefiniti e i [tipi di informazioni personalizzati](https://docs.microsoft.com/office365/securitycompliance/create-a-custom-sensitive-information-type)<br /><br />Le opzioni di configurazione possibili sono:  <br /><br />- Solo conteggio univoco <br /><br />- Conteggio minimo e massimo <br /><br />- Supporto di AND e OR con i tipi di informazioni <br /><br />- Dizionario di parole chiave<br /><br />- Livello di attendibilità e prossimità dei caratteri personalizzabili|

Per un confronto più dettagliato delle differenze di comportamento per impostazioni di protezione specifiche, vedere [Confronto del comportamento delle impostazioni di protezione per un'etichetta](../configure-policy-migrate-labels.md#comparing-the-behavior-of-protection-settings-for-a-label).

#### <a name="features-that-will-not-be-in-the-azure-information-protection-unified-labeling-client"></a>Funzionalità che non saranno disponibili nel client per l'etichettatura unificata di Azure Information Protection

Sebbene il client per l'etichettatura unificata di Azure Information Protection sia ancora in fase di sviluppo, non è previsto che le funzionalità seguenti e le differenze di comportamento del client di Azure Information Protection saranno disponibili nelle versioni future del client per l'etichettatura unificata di Azure Information Protection: 

- Autorizzazioni personalizzate nelle app di Office: Word, Excel e PowerPoint

- Rilevamento e revoca da app di Office ed Esplora file

- Titolo e descrizione comando della barra di Information Protection

- Modalità di sola protezione (nessuna etichetta)

- Protezione del documento PDF come formato ppdf

- Visualizzazione del pulsante Non inoltrare in Outlook

- Criteri demo

- Giustificazione per la rimozione della protezione

- Richiesta di conferma prima dell'eliminazione di un'etichetta applicata

- Segnalazione del collegamento di un problema nella finestra di dialogo Guida e commenti

- Assegnazione di un'etichetta a un documento di Office tramite una proprietà personalizzata esistente (impostazioni client avanzate SyncPropertyName e SyncPropertyState)

- Separazione dei cmdlet PowerShell per la connessione a un servizio Rights Management


#### <a name="parent-labels-and-their-sublabels"></a>Etichette padre ed etichette secondarie 

Il client Azure Information Protection non supporta le configurazioni che specificano un'etichetta padre con etichette secondarie. Queste configurazioni includono la specifica di un'etichetta predefinita e un'etichetta per la classificazione consigliata o automatica. Quando un'etichetta ha etichette secondarie, è possibile specificare una delle etichette secondarie, ma non l'etichetta padre.

Per motivi di parità, nemmeno il client per l'etichettatura unificata di Azure Information Protection supporta l'applicazione di etichette padre con etichette secondarie, anche se è possibile selezionare queste etichette nei centri di amministrazione. In questo scenario il client di etichettatura unificata Azure Information Protection non applicherà l'etichetta padre.

## <a name="see-also"></a>Vedere anche
Quando sono necessarie altre informazioni su come distribuire e usare questi client, usare la documentazione seguente:

- [Client di Azure Information Protection](AIP-client.md)

- [Client per l'etichettatura unificata Azure Information Protection](unifiedlabelingclient-version-release-history.md)

- [Note sulla distribuzione del client RMS](client-deployment-notes.md)

Anche se può essere usato con AD RMS, il client Azure Information Protection si integra al meglio con i servizi di Azure, Azure Information Protection e il relativo servizio di protezione dei dati, Azure Rights Management. Per un confronto del lato servizio per Azure Information Protection, vedere [Confronto tra Azure Information Protection e AD RMS](../compare-on-premise.md).
