---
title: 'Client di Azure Information Protection: cronologia delle versioni e criteri per il supporto'
description: Informazioni sugli elementi nuovi o modificati in una versione del client di Azure Information Protection per Windows e sui criteri del ciclo di vita per il supporto.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/28/2018
ms.topic: article
ms.service: information-protection
ms.assetid: 6ebd0ca3-1864-4b3d-bb3e-a168eee5eb1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 945b05a99122b7caf1d9a73ea8b75717a5522660
ms.sourcegitcommit: 8cde6611ab6d95d816e1c80267cacd32443f31cb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2018
ms.locfileid: "43117928"
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

## <a name="versions-later-than-12950"></a>Versioni successive alla versione 1.29.5.0

Se la versione del client usata è successiva alla 1.29.5.0 si tratta di una build di anteprima per scopi di test e valutazione.

Questa versione include MSIPC versione 1.0.3592.627 del client RMS.

**Nuove funzionalità**: 

- Supporto dello standard ISO per la crittografia dei file PDF in modo tale che i documenti protetti mantengano l'estensione pdf per impostazione predefinita e possano essere aperti da lettori PDF che supportano questo standard ISO. Attualmente, è necessario indicare agli utenti di aprire questi file PDF protetti manualmente con il Visualizzatore Azure Information Protection. Per consentire agli utenti di eseguire questa operazione, quando aprono uno di questi file PDF protetti, viene visualizzata una pagina con le icone da selezionare per il sistema operativo usato. Se non si vuole questo comportamento bensì la parità con la versione di disponibilità generale del client Azure Information Protection, è possibile definire una [configurazione del client avanzata](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption).

- Supporto dei nuovi tipi di informazioni sensibili che consentono di classificare i documenti contenenti informazioni personali. [Altre informazioni](../configure-policy-classification.md#sensitive-information-types-that-require-a-minimum-version-of-the-client) 

- Supporto di assegnazione etichette per il formato **Strict Open XML Document** in file di Word, Excel e PowerPoint. Per altre informazioni sui formati Open XML, vedere il post del blog di Office [New file format options in the new Office](https://www.microsoft.com/en-us/microsoft-365/blog/2012/08/13/new-file-format-options-in-the-new-office/) (Nuove opzioni per i formati di file nel nuovo Office). 

- Supporto dei file protetti con Secure Islands e diversi da file PDF e documenti di Office. Ad esempio file di testo e file immagine protetti. Oppure file con estensione pfile. Questo supporto attiva nuovi scenari. Ad esempio lo scanner Azure Information Protection può verificare la presenza di informazioni riservate in questi file e rietichettarli automaticamente per Azure Information Protection. [Altre informazioni](client-admin-guide-customizations.md#support-for-files-protected-by-secure-islands)

- Il collegamento **Invia commenti e suggerimenti** nella finestra di dialogo **Guida e commenti** viene sostituito con **Segnala un problema**, che è possibile personalizzare. Per impostazione predefinita, questa opzione invia un messaggio di posta elettronica a Microsoft. È possibile modificare questo indirizzo di posta elettronica in modo tale che quando gli utenti selezionano questa opzione venga usata una stringa HTTP specificata. Ad esempio, una pagina Web personalizzata in cui gli utenti possono segnalare i problemi o un indirizzo di posta elettronica che rimanda all'help desk. Per modificare questo indirizzo, usare un'[impostazione del client avanzata](client-admin-guide-customizations.md#modify-the-email-address-for-the-report-an-issue-link).

- Per lo scanner di Azure Information Protection:

    - Nuovo cmdlet [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner): deve essere eseguito una sola volta dopo l'aggiornamento dalla versione di disponibilità a livello generale corrente (1.29.5.0) o versioni precedenti.
    
    - Nuovo cmdlet [Get-AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus): ottiene lo stato corrente del servizio per lo scanner.  
    
    - Nuovo cmdlet [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan): richiede allo scanner di avviare un ciclo di analisi unico quando la pianificazione è impostata su manuale.
    
    - SharePoint Server 2010 è supportato per i clienti che dispongono del [supporto "Extended" per la versione corrente di SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).
    
**Correzioni**

- Per lo scanner di Azure Information Protection:
    
    - Per i documenti protetti nelle raccolte di SharePoint, se il parametro *DefaultOwner* non viene usato per il repository dei dati, il valore Editor di SharePoint viene ora usato come valore predefinito invece del valore Autore.
    
    - I report dello scanner includono "Autore ultima modifica" per i documenti di Office.

- Quando si applica la classificazione e la protezione mediante PowerShell o lo scanner, i metadati del documento di Office non vengono rimossi o crittografati.

- La visualizzazione di messaggi di posta elettronica mediante le icone freccia elemento successivo ed elemento precedente nella barra di accesso rapido visualizza l'etichetta appropriata per ogni messaggio.

- Le autorizzazioni personalizzate supportano gli indirizzi di posta elettronica di destinatari contenenti un apostrofo.

- L'ambiente del computer viene inizializzato correttamente (bootstrap) quando questa operazione viene avviata mediante l'apertura di un documento protetto archiviato in SharePoint Online.

- Quando si fa clic con il pulsante destro del mouse in Esplora file, in PowerShell o nello scanner dal client, l'assegnazione delle etichette è bloccata per i file nei percorsi WebDav poiché si tratta di uno scenario non supportato.

- L'icona Elimina l'etichetta non viene visualizzata nelle app client (Word, Excel, PowerPoint e Outlook) quando si configura l'[impostazione di criteri](../configure-policy-settings.md) di **Tutti i documenti e i messaggi di posta elettronica devono avere un'etichetta**.

**Modifiche aggiuntive**:
   
- Per [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration):
    
    - I valori del parametro *Schedule* non sono più **OneTime**, **Continuous** e **Never**, ma **Manual** e **Always**.
        
    - Il parametro *Type* è stato rimosso e pertanto viene rimosso anche dall'output quando si esegue [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration). Per impostazione predefinita, solo i file nuovi o modificati vengono controllati dopo il primo ciclo di analisi. Se il parametro *Type* è stato impostato su **Full** in precedenza per ripetere l'analisi di tutti i file, eseguire ora [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan) con il parametro *Reset*. Lo scanner deve essere anche configurato per una pianificazione manuale, che richiede l'impostazione del parametro *Schedule* su **Manual** con [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration).
    
- Per lo scanner, l'elenco di esclusione predefinito ora include i file con estensione msg, rar, rtf e zip. [Altre informazioni](client-admin-guide-file-types.md#file-types-that-are-excluded-from-classification-and-protection-by-the-azure-information-protection-scanner)

- La versione dei criteri è ora la 1.4. L'identificazione del numero di versione è necessaria per la [configurazione dei computer disconnessi](client-admin-guide-customizations.md#support-for-disconnected-computers).

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

## <a name="version-110560"></a>Versione 1.10.56.0

**Data di rilascio**: 18/09/2017

Questa versione include MSIPC versione 1.0.3219.0619 del client RMS.

**Nuove funzionalità**:

- Supporto per le nuove condizioni di prevenzione della perdita dei dati (DLP) di Office 365 che è possibile configurare per un'etichetta. Per altre informazioni, vedere [Configurare le condizioni per un'etichetta di Azure Information Protection](../configure-policy-classification.md).

- Supporto per le etichette configurate per le azioni definite dall'utente. Per Outlook, questa etichetta si applica automaticamente all'opzione Non inoltrare di Outlook. Per Word, Excel, PowerPoint ed Esplora file, questa etichetta richiede all'utente di specificare autorizzazioni personalizzate. Per altre informazioni, vedere [Configurare un'etichetta di Azure Information Protection per la protezione](../configure-policy-protection.md).

- Le etichette supportano più lingue. A partire da 30 agosto 2017, i [criteri predefiniti](../configure-policy-default.md) includono il supporto per più lingue, visualizzate agli utenti in questa versione del client. Per visualizzare le etichette nella lingua preferita dai criteri predefiniti prima di questa data e per le etichette configurate, vedere [Come configurare etichette per lingue diverse in Azure Information Protection]configure-policy-languages.md).

- Le etichette vengono visualizzate dal pulsante **Proteggi** sulla barra multifunzione di Office, oltre a essere visualizzate sulla barra di Information Protection. 

- Protezione nativa per tipi di file Visio seguenti con estensione vsdm,vsdx, vssm, vssx, vstm e vstx

- Supporto per configurazioni client avanzate che è possibile configurare nel portale di Azure. Le configurazioni comprendono:
    
    - [Nascondere o visualizzare il pulsante Non inoltrare in Outlook](client-admin-guide-customizations.md#hide-or-show-the-do-not-forward-button-in-outlook)
    
    - [Rendere disponibili o non disponibili agli utenti le opzioni relative alle autorizzazioni personalizzate](client-admin-guide-customizations.md#make-the-custom-permissions-options-available-or-unavailable-to-users)
    
    - [Nascondere in modo permanente la barra di Azure Information Protection](client-admin-guide-customizations.md#permanently-hide-the-azure-information-protection-bar)
    
    - [Abilitare la classificazione consigliata in Outlook](client-admin-guide-customizations.md#enable-recommended-classification-in-outlook)

- Per PowerShell, supporto per assegnare un'etichetta ai file in modo non interattivo usando i nuovi cmdlet di PowerShell, [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) e [Clear-AIPAuthentication](/powershell/module/azureinformationprotection/clear-aipauthentication). Per altre informazioni su come usare questi cmdlet, vedere la [sezione relativa a PowerShell](client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) della guida dell'amministratore.

- Per i cmdlet di PowerShell, [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) e [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification), sono disponibili nuovi parametri: **Owner** e **PreserveFileDetails**. Questi parametri consentono di specificare un indirizzo e-mail per la proprietà personalizzata Owner, lasciando invariata la data per i documenti a cui è assegnata un'etichetta.

**Correzioni**:

Correzioni per la stabilità e per scenari specifici che includono:

- Supporto per la protezione generica di file di grandi dimensioni che in precedenza potevano essere causa di danneggiamento se di dimensioni maggiori di 1 GB. Attualmente le dimensioni dei file sono limitate solo dallo spazio disponibile su disco e dalla memoria disponibile. Per altre informazioni sulle limitazioni relative alle dimensioni dei file, vedere [Dimensioni dei file supportati per la protezione](client-admin-guide-file-types.md#file-sizes-supported-for-protection) della guida dell'amministratore.

- Il visualizzatore del client Azure Information Protection consente di aprire file PDF protetti (con estensione ppdf) come file disponibili solo per la visualizzazione.

- Supporto per l'assegnazione di etichette e la protezione dei file archiviati in SharePoint Server.

- Le filigrane supportano ora più righe. Inoltre, i contrassegni visivi vengono ora applicati a un documento [solo al primo salvataggio]configure-policy-markings.md#when-visual-markings-are-applied) anziché ogni volta che un documento viene salvato.

- L'opzione **Esegui diagnostica** nella finestra di dialogo **Guida e commenti** viene sostituita da **Ripristina le impostazioni**. Il comportamento per questa azione è stato modificato in modo da includere la disconnessione dell'utente e l'eliminazione dei criteri di Azure Information Protection. Per altre informazioni, vedere la sezione contenente [altre informazioni sull'opzione Ripristina le impostazioni](..\rms-client\client-admin-guide.md#more-information-about-the-reset-settings-option) della guida dell'amministratore.

- Supporto per l'autenticazione proxy.

Correzioni per una migliore esperienza utente, che includono:

- Convalida e-mail quando gli utenti specificano autorizzazioni personalizzate. Inoltre, è ora possibile specificare più indirizzi e-mail premendo INVIO.

- L'etichetta padre non viene visualizzata quando tutte le relative etichette secondarie sono configurate per la protezione e il client non dispone di un'edizione di Office che supporta la protezione. 

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sull'installazione e l'uso del client: 

- Per utenti: [Scaricare e installare il client](install-client-app.md)

- Per amministratori: [Guida per l'amministratore del client di Azure Information Protection](client-admin-guide.md)


