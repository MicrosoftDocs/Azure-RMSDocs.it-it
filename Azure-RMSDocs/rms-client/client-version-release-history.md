---
title: 'Client di Azure Information Protection: cronologia delle versioni e criteri per il supporto'
description: Informazioni sugli elementi nuovi o modificati in una versione del client di Azure Information Protection per Windows e sui criteri del ciclo di vita per il supporto.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/14/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 6ebd0ca3-1864-4b3d-bb3e-a168eee5eb1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: d4b9419ee12dfef0db29604dc7a396eedd7225fc
ms.sourcegitcommit: a547dee247e4961e8f7c1f08e39b03dff710a74c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/14/2018
ms.locfileid: "51628072"
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Client di Azure Information Protection: cronologia delle versioni e criteri per il supporto

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Il team di Azure Information Protection aggiorna regolarmente il client di Azure Information Protection con correzioni e nuove funzionalità. 

È possibile scaricare la versione disponibile a livello generale più recente e la versione di anteprima corrente (se disponibile) dall'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018). Questa versione disponibile a livello generale è inclusa anche nel catalogo di Microsoft Update (categoria: **Azure Information Protection**), per poter aggiornare il client tramite WSUS o Configuration Manager o altri meccanismi di distribuzione di software che usano Microsoft Update.

Per altre informazioni, vedere [Aggiornamento e gestione del client Azure Information Protection](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client).

### <a name="servicing-information-and-timelines"></a>Informazioni e tempistiche di manutenzione

Ogni versione con disponibilità generale del client di Azure Information Protection è supportata per un massimo di sei mesi dopo il rilascio della versione con disponibilità generale successiva. Le versioni del client non supportate non sono incluse in questa pagina. Le correzioni e le nuove funzionalità sono sempre valide per l'ultima versione disponibile a livello generale e non verranno applicate alle versioni precedenti.

Le versioni di anteprima non devono essere distribuite agli utenti finali nelle reti di produzione, ma è possibile usare la versione di anteprima più recente per visualizzare e provare le nuove funzionalità e correzioni che saranno disponibili nella prossima versione disponibile a livello generale. Non sono supportate le versioni di anteprima non aggiornate.

### <a name="release-history"></a>Cronologia delle versioni

Usare le informazioni seguenti per scoprire le novità o le modifiche per una versione supportata del client di Azure Information Protection per Windows. La versione più recente è elencata per prima. 

> [!NOTE]
> Dato che le correzioni di minore rilevanza non sono elencate, se si verifica un problema con il client di Azure Information Protection, è consigliabile controllare se tale problema è stato risolto con la versione disponibile a livello generale più recente. Se il problema persiste, verificare la versione di anteprima corrente.
>  
> Per il supporto tecnico, vedere le informazioni riportate in [Opzioni di supporto e risorse per la community](../information-support.md#support-options-and-community-resources). È anche possibile rivolgersi al team di Azure Information Protection nel [sito di Yammer](https://www.yammer.com/askipteam/).

## <a name="versions-later-than-137190"></a>Versioni successive alla versione 1.37.19.0

Se la versione 1 del client usata è successiva alla 1.37.19.0, si tratta di una build di anteprima per scopi di test e valutazione. 

> [!TIP]
> Se si è interessati alla valutazione del client di etichettatura unificato Azure Information Protection perché si pubblicano le etichette dal Centro sicurezza e conformità di Office 365, vedere [Client che supporta l'etichettatura unificata di Azure Information Protection: informazioni di rilascio versione](unifiedlabelingclient-version-release-history.md).

**Data di rilascio**: 20/09/2018

**Nuove funzionalità:**

- Supporto del [reporting centralizzato](../reports-aip.md) per la funzionalità di analisi di Azure Information Protection annunciata in Microsoft Ignite.

**Informazioni aggiuntive:**

Solo per questa versione di anteprima, specifiche per lo scanner:

- Installare lo scanner seguendo questa procedura:
    
    1. Installare la versione GA corrente (1.37.19.0) del client.
    2. Installare e configurare lo scanner.
    3. Avviare lo scanner.
    4. Aggiornare il client Azure Information Protection a questa versione di anteprima.
    5. Avviare lo scanner.

- Problema noto con l'analisi di set di dati grandi:
    
    Con questa versione di anteprima, aumentare gradualmente il numero di file da analizzare e monitorare lo stato di avanzamento. Se lo stato dello scanner segnala che è in esecuzione ma i nuovi file non vengano analizzati, ridurre il numero di file da analizzare e riavviare lo scanner. 

Per istruzioni per l'installazione, la configurazione e l'avvio dello scanner, vedere [Distribuzione dello scanner di Azure Information Protection per classificare e proteggere automaticamente i file](../deploy-aip-scanner.md).

## <a name="version-137190"></a>Versione 1.37.19.0

**Data di rilascio**: 17/09/2018

Questa versione include MSIPC versione 1.0.3592.627 del client RMS.

**Nuove funzionalità**: 

- Supporto dello standard ISO per la crittografia dei file PDF mediante la definizione di una nuova [configurazione del client avanzata](client-admin-guide-customizations.md#protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption). Quando è configurata questa opzione, i documenti PDF protetti mantengono l'estensione pdf (anziché adottare l'estensione ppdf) e possono essere aperti da lettori PDF che supportano questo standard ISO. Attualmente, è necessario indicare agli utenti di aprire questi file PDF protetti manualmente con il Visualizzatore Azure Information Protection. Per consentire agli utenti di eseguire questa operazione, quando aprono uno di questi file PDF protetti, viene visualizzata una pagina con le icone da selezionare per il sistema operativo usato.

- Supporto dei nuovi tipi di informazioni sensibili che consentono di classificare i documenti contenenti informazioni personali. [Altre informazioni](../configure-policy-classification.md#sensitive-information-types-that-require-a-minimum-version-of-the-client) 

- Le etichette che applicano la protezione ora vengono visualizzate nelle app di Office 2016 (versione minima 1805, build 9330.2078) quando all'utente viene assegnata una licenza per Azure Rights Management (noto anche come Azure Information Protection per Office 365).

- Supporto di assegnazione etichette per il formato **Strict Open XML Document** in file di Word, Excel e PowerPoint. Per altre informazioni sui formati Open XML, vedere il post del blog di Office [New file format options in the new Office](https://www.microsoft.com/en-us/microsoft-365/blog/2012/08/13/new-file-format-options-in-the-new-office/) (Nuove opzioni per i formati di file nel nuovo Office). 

- Supporto dei file protetti con Secure Islands e diversi da file PDF e documenti di Office. Ad esempio file di testo e file immagine protetti. Oppure file con estensione pfile. Questo supporto attiva nuovi scenari. Ad esempio lo scanner Azure Information Protection può verificare la presenza di informazioni riservate in questi file e rietichettarli automaticamente per Azure Information Protection. [Altre informazioni](client-admin-guide-customizations.md#support-for-files-protected-by-secure-islands)

- Nuove impostazioni client avanzate per rimuovere le intestazioni e i piè di pagina applicati ai documenti da altre soluzioni di assegnazione etichette. [Altre informazioni](client-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions)

- Per lo scanner di Azure Information Protection:

    - Nuovo cmdlet [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner): deve essere eseguito una sola volta dopo l'aggiornamento dalla versione di disponibilità a livello generale precedente (1.29.5.0) o versioni precedenti.
    
    - Nuovo cmdlet [Get-AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus): ottiene lo stato corrente del servizio per lo scanner.  
    
    - Nuovo cmdlet [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan): richiede allo scanner di avviare un ciclo di analisi unico quando la pianificazione è impostata su manuale.
    
    - SharePoint Server 2010 è supportato per i clienti che dispongono del [supporto "Extended" per la versione corrente di SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).
    
- Supporto del nuovo pannello **Azure Information Protection - Nodi (anteprima)** nel portale di Azure, che consente di gestire gli scanner da una posizione centrale. Le informazioni dagli scanner distribuiti con connettività ad Azure vengono aggiornate ogni cinque minuti. Da questo pannello è possibile avviare lo scanner per una singola analisi, rianalizzare tutti i file, controllare lo stato di uno scanner e visualizzare la velocità di scansione.

**Correzioni**

- Per lo scanner di Azure Information Protection:
    
    - Per i documenti protetti nelle raccolte di SharePoint, se il parametro *DefaultOwner* non viene usato per il repository dei dati, il valore Editor di SharePoint viene ora usato come valore predefinito invece del valore Autore.
    
    - I report dello scanner includono "Autore ultima modifica" per i documenti di Office.
    
    - Ora è possibile proteggere tutti i tipi di file usando il carattere jolly `*` quando si modifica il Registro di sistema come descritto nella sezione [Modifica del Registro di sistema per lo scanner](../deploy-aip-scanner.md#editing-the-registry-for-the-scanner).

- La visualizzazione di messaggi di posta elettronica mediante le icone freccia elemento successivo ed elemento precedente nella barra di accesso rapido visualizza l'etichetta appropriata per ogni messaggio.

- Le autorizzazioni personalizzate supportano gli indirizzi di posta elettronica di destinatari contenenti un apostrofo.

- L'ambiente del computer viene inizializzato correttamente (bootstrap) quando questa operazione viene avviata mediante l'apertura di un documento protetto archiviato in SharePoint Online.

- Quando si fa clic con il pulsante destro del mouse in Esplora file, in PowerShell o nello scanner dal client, l'assegnazione delle etichette è bloccata per i file nei percorsi WebDav poiché si tratta di uno scenario non supportato.

- L'icona Elimina l'etichetta non viene visualizzata nelle app client (Word, Excel, PowerPoint e Outlook) quando si configura l'[impostazione di criteri](../configure-policy-settings.md) di **Tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta**.

**Modifiche aggiuntive**:

- Per [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration):
    
    - I valori del parametro *Schedule* non sono più **OneTime**, **Continuous** e **Never**, ma **Manual** e **Always**.
        
    - Il parametro *Type* è stato rimosso e pertanto viene rimosso anche dall'output quando si esegue [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration). Per impostazione predefinita, solo i file nuovi o modificati vengono controllati dopo il primo ciclo di analisi. Se il parametro *Type* è stato impostato su **Full** in precedenza per ripetere l'analisi di tutti i file, eseguire ora [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan) con il parametro *Reset*. Lo scanner deve essere anche configurato per una pianificazione manuale, che richiede l'impostazione del parametro *Schedule* su **Manual** con [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration).
    
- L'elenco di esclusione predefinito per il client e lo scanner ora include i file con estensione msg, rar e zip. Lo scanner esclude anche i file con estensione rtf. [Altre informazioni](client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection)

- La versione dei criteri è ora la 1.4. L'identificazione del numero di versione è necessaria per la [configurazione dei computer disconnessi](client-admin-guide-customizations.md#support-for-disconnected-computers).

- Il collegamento **Invia commenti e suggerimenti** nella finestra di dialogo **Guida e commenti** è stato rimosso. È stata temporaneamente sostituito dal collegamento **Segnala un problema**, ma ora questo collegamento è disponibile solo nelle versioni di anteprima. Per impostazione predefinita questa opzione invia un messaggio di posta elettronica a Microsoft, ma è possibile modificare l'indirizzo di posta elettronica impostando una stringa HTTP personalizzata. Ad esempio, una pagina Web personalizzata in cui gli utenti possono segnalare i problemi o un indirizzo di posta elettronica che rimanda all'help desk. Per modificare questo indirizzo, usare un'[impostazione del client avanzata](client-admin-guide-customizations.md#modify-the-email-address-for-the-report-an-issue-link).

## <a name="version-12950"></a>Versione 1.29.5.0 

**Data di rilascio**: 26/06/2018

Questa versione include MSIPC versione 1.0.3403.1224 del client RMS.

**Correzioni**:

- Per le versioni di Outlook 16.0.9324.1000 e successive (A portata di clic), la barra di Azure Information Protection supporta le opzioni di visualizzazione dello schermo più recenti per risolvere il problema della barra visualizzata all'esterno dell'applicazione Outlook.

- I contrassegni visivi configurati [per ogni tipo di applicazione di Office](../configure-policy-markings.md#setting-different-visual-markings-for-word-excel-powerpoint-and-outlook) ora sostituiscono un'intestazione o un piè di pagina applicato in precedenza da un'etichetta di Azure Information Protection.

- Quando un file di Excel è già etichettato e l'etichetta applica contrassegni visivi, ora i contrassegni visivi dell'etichetta vengono applicati a un nuovo foglio.

- Quando si usa l'impostazione client avanzata per [etichettare un documento di Office usando una proprietà personalizzata esistente](client-admin-guide-customizations.md#label-an-office-document-by-using-an-existing-custom-property), l'assegnazione automatica dell'etichetta non esegue l'override di quella manuale.

## <a name="version-127480"></a>Versione 1.27.48.0

**Data di rilascio**: 30/05/2018

Questa versione include MSIPC versione 1.0.3403.1224 del client RMS.

**Nuove funzionalità**: 

- Per lo scanner di Azure Information Protection:
    
    - È possibile specificare un elenco di tipi di file da includere o escludere dall'analisi. Per specificare questo elenco, usare [Set-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Set-AIPScannerScannedFileTypes). Dopo aver specificato l'elenco di tipi di file, è possibile aggiungere un nuovo tipo di file all'elenco usando [Add-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Add-AIPScannerScannedFileTypes) e rimuovere un tipo di file dall'elenco usando [Remove-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Remove-AIPScannerScannedFileTypes).
    
    - È possibile applicare un'etichetta ai file senza esaminarne il contenuto applicando un'etichetta predefinita. Usare il cmdlet [Set-AIPScannerRepository](/powershell/module/azureinformationprotection/Set-AIPScannerRepository) e impostare il parametro *MatchPolicy* su **Off**. 
    
    - È possibile individuare i file con i tipi di informazioni riservate senza configurare le etichette per la classificazione automatica. Usare il cmdlet [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) e impostare il parametro *DiscoverInformationTypes* su **All**
    
    - Per impostazione predefinita, sono protetti solo i tipi di documenti di Office. Altri tipi di file possono essere protetti quando li si definisce nel Registro di sistema. Per informazioni, vedere [Configurazione dell'API file](../develop/file-api-configuration.md) nelle linee guida per sviluppatori.
    
    - Per impostazione predefinita, lo scanner viene ora eseguito con un livello di integrità basso per una maggiore sicurezza in caso di esecuzione con un account con privilegi. Quando l'account del servizio che esegue lo scanner ha solo i diritti indicati nei [prerequisiti dello scanner](../deploy-aip-scanner.md#prerequisites-for-the-azure-information-protection-scanner), il livello di integrità basso non è necessario e non è consigliato perché influisce negativamente sulle prestazioni. È possibile usare un'impostazione avanzata del client per disabilitare il livello di integrità basso. [Altre informazioni](client-admin-guide-customizations.md#disable-the-low-integrity-level-for-the-scanner) 
    
- Per [Get-AIPFileStatus](/powershell/module/azureinformationprotection/Get-AIPFileStatus), l'output include ora il proprietario e l'emittente di Rights Management, oltre che la data in cui il contenuto è stato protetto.
 
**Modifiche aggiuntive**:

- Per lo scanner di Azure Information Protection: 
    
    - Se è stata installata una versione precedente dello scanner, eseguire di nuovo il comando di installazione dello scanner con [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner) dopo aver aggiornato il client Azure Information Protection. Verranno mantenute le impostazioni di configurazione per i repository e lo scanner. Reinstallando lo scanner, vengono concesse allo scanner le autorizzazioni di eliminazione account del servizio per il database dello scanner, che saranno necessarie per i report.    
    
    - Il parametro *ScanMode* di [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration) è stato rinominato in **Enforce** e i valori sono Off e On.
    
    - Per usare un'etichetta predefinita, non è più necessario configurare un'etichetta predefinita come impostazione di criteri. È sufficiente specificare l'etichetta predefinita con la configurazione del repository. 

- La pagina iniziale "Congratulazioni" è stata rimossa ed è stata sostituita da una pagina relativa alle novità di Azure Information Protection, visualizzata al primo utilizzo nelle applicazioni di Office.

## <a name="version-12660"></a>Versione 1.26.6.0

**Data di rilascio**: 17/04/2018

Questa versione include MSIPC versione 1.0.3403.1224 del client RMS.

**Nuove funzionalità**:

- Scanner di Azure Information Protection: il modulo di PowerShell incluso nel client offre nuovi cmdlet per installare e configurare lo scanner per l'individuazione, la classificazione e la protezione dei file negli archivi dati locali. Per istruzioni, vedere [Distribuzione dello scanner Azure Information Protection per classificare e proteggere automaticamente i file](../deploy-aip-scanner.md). 
- È ora possibile impostare contrassegni visivi diversi per Word, Excel, PowerPoint e Outlook tramite un'istruzione di variabile "If.App" nella stringa di testo e identificare il tipo di applicazione. [Altre informazioni]configure-policy-markings.md#setting-different-visual-markings-for-word-excel-powerpoint-and-outlook)

- Supporto per l'[impostazione dei criteri](../configure-policy-settings.md): **Visualizza la barra di Information Protection nelle app Office**. Quando questa impostazione è disabilitata, gli utenti selezionano le etichette dal pulsante **Proteggi** sulla barra multifunzione.

- Un nuova impostazione client avanzata (ancora in anteprima) per attivare l'esecuzione continua della classificazione in background. Quando questa impostazione è abilitata, per le app di Office la classificazione automatica e consigliata viene eseguita in modo continuo in background anziché al salvataggio dei documenti. Questa modifica del comportamento consente di applicare la classificazione automatica e consigliata ai documenti archiviati in SharePoint Online. [Altre informazioni](client-admin-guide-customizations.md#turn-on-classification-to-run-continuously-in-the-background)

- Nuova impostazione avanzata del client in base alla quale Outlook non applica l'etichetta predefinita configurata nei criteri di Azure Information Protection. In alternativa, Outlook può applicare un'etichetta predefinita diversa o non applicare alcuna etichetta. [Altre informazioni](client-admin-guide-customizations.md#set-a-different-default-label-for-outlook) 

- Per le app di Office, quando vengono specificate autorizzazioni personalizzate è ora possibile esplorare e selezionare gli utenti da un'icona a forma di rubrica. Questa opzione offre un'esperienza utente simile alla procedura di definizione delle autorizzazioni personalizzate in Esplora file.

- Supporto per un metodo di autenticazione completamente non interattivo per gli account del servizio che usano PowerShell e a cui non è possibile concedere il diritto di **accesso locale**. Questo metodo di autenticazione richiede di usare il nuovo parametro *Token* con [Set-AIPAuthentication](/powershell/module/azureinformationprotection/Set-AIPAuthentication) e di eseguire uno script di PowerShell come attività. [Altre informazioni](client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication)

- Nuovo parametro *IntegratedAuth* per [Set-RMSServerAuthentication](/powershell/module/azureinformationprotection/set-rmsserverauthentication). Questo parametro supporta la modalità server per AD RMS, necessaria affinché Active Directory Rights Management Services supporti Windows Server con Infrastruttura di classificazione file (FCI).


**Correzioni**:

Correzioni per la stabilità e per scenari specifici che includono:

- Per le versioni di Office 16.0.8628.2010 e successive (A portata di clic), la barra di Azure Information Protection supporta le opzioni di visualizzazione dello schermo più recenti per risolvere il problema della barra visualizzata all'esterno delle applicazioni di Office.

- Quando due organizzazioni che usano Azure Information Protection condividono documenti e messaggi di posta elettronica con etichette, le proprie etichette vengono mantenute anziché essere sostituite da quelle dell'altra organizzazione.

- Per Excel:
        
    - Supporto per la modifica dei temi di Office o di Windows che in precedenza non consentivano a Excel di visualizzare dati dopo la modifica del tema.
        
    - Supporto per le celle che contengono riferimenti incrociati che in precedenza causavano un danneggiamento delle celle.
    
    - Supporto per la digitazione di caratteri giapponesi, cinesi e coreani, che in precedenza causava la chiusura di una finestra e l'impossibilità di selezionare questi caratteri.
    
    - Supporto per i commenti, che in precedenza causava la chiusura del commento durante la digitazione.

- Per PowerPoint: supporto per la creazione condivisa, che in precedenza poteva provocare la perdita di dati.

- I file con estensione .xml possono ora essere esaminati per la classificazione automatica o consigliata.

- Il visualizzatore può ora aprire file protetti basati su testo (con estensione .ptxt e .pxml) con dimensioni maggiori di 20 MB. 
- Outlook non si blocca più quando vengono usati i promemoria di Outlook.

- Il bootstrap in Office a 64 bit ha esito positivo, quindi è possibile proteggere documenti e messaggi di posta elettronica.

- È ora possibile configurare un'etichetta per le autorizzazioni definite dall'utente per Word, Excel, PowerPoint ed Esplora file, nonché usare l'impostazione client avanzata per nascondere le opzioni per le autorizzazioni personalizzate. [Altre informazioni](client-admin-guide-customizations.md#make-the-custom-permissions-options-available-or-unavailable-to-users) 

- Fallback al tipo di carattere Calibri se nei criteri di Azure Information Protection sono configurati contrassegni visivi per un tipo di carattere non installato nel client.

- Non si verificano più arresti anomali di Office dopo l'aggiornamento del client Azure Information Protection.

- Per le app di Office, è stato introdotto un miglioramento delle prestazioni e dell'utilizzo della memoria.

- Quando si configura un'etichetta per le autorizzazioni definite dall'utente e la protezione HYOK (AD RMS), la protezione non usa più il servizio Azure Rights Management in modo errato.

- Per un'esperienza di gestione più coerente, le etichette secondarie non ereditano più i contrassegni visivi e le impostazioni di protezione dall'etichetta padre.

**Modifiche aggiuntive**:

- Per la [registrazione dell'utilizzo per il client](client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client ): gli ID evento 102 e 103 vengono sostituiti con l'ID evento 101.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sull'installazione e l'uso del client: 

- Per utenti: [Scaricare e installare il client](install-client-app.md)

- Per amministratori: [Guida per l'amministratore del client di Azure Information Protection](client-admin-guide.md)


