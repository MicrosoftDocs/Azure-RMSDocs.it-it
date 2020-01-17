---
title: 'Tipi di file supportati: Azure Information Protection Unified Labeling client'
description: Dettagli tecnici sui tipi di file supportati, le estensioni dei nomi di file e i livelli di protezione per gli amministratori che sono responsabili del Azure Information Protection client unificato per Windows.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/13/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 46a9ce17efc40242f78506cf59c842d3b7721b98
ms.sourcegitcommit: ad3e55f8dfccf1bc263364990c1420459c78423b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/16/2020
ms.locfileid: "76117681"
---
# <a name="admin-guide-file-types-supported-by-the-azure-information-protection-unified-labeling-client"></a>Guida dell'amministratore: tipi di file supportati dal client di Azure Information Protection Unified Labeling

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, windows Server 2012*>
>
> *Istruzioni per: [Azure Information Protection client di etichetta unificata per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Il client Azure Information Protection Unified Labeling può applicare quanto segue ai documenti e ai messaggi di posta elettronica:

- Solo classificazione

- Classificazione e protezione

- Solo protezione

Il client di etichettatura unificata Azure Information Protection può anche esaminare il contenuto di alcuni tipi di file usando i tipi di informazioni riservate note o le espressioni regolari definite dall'utente.

Usare le informazioni seguenti per verificare quali tipi di file sono supportati dal client Azure Information Protection Unified Labeling, comprendere i diversi livelli di protezione e come modificare il livello di protezione predefinito e identificare i file automaticamente escluso (ignorato) dalla classificazione e dalla protezione.

Per i tipi di file elencati, i percorsi WebDav non sono supportati.

## <a name="file-types-supported-for-classification-only"></a>Tipi di file supportati solo per la classificazione

I tipi di file seguenti possono essere classificati anche se non sono protetti.

- **Adobe Portable Document Format**: .pdf

- **Microsoft Project**: .mpp, .mpt

- **Microsoft Publisher**: .pub

- **Microsoft XPS**: .xps .oxps

- **Immagini**: con estensione jpg, jpe, jpeg, jif, jfif, jfi, png, tif e tiff

- **Autodesk Design Review 2013**: .dwfx

- **Adobe Photoshop**: .psd

- **Digital Negative**: .dng

- **Microsoft Office**: i tipi di file nella tabella seguente.

    I formati di file supportati per questi tipi di file sono i formati 97-2003 e Office Open XML per i programmi di Office seguenti: Word, Excel e PowerPoint.

    |Tipo di file Office|Tipo di file Office|
    |----------------------------------|----------------------------------|
    |.doc<br /><br />.docm<br /><br />.docx<br /><br />dot<br /><br />.dotm<br /><br />.dotx<br /><br />potm<br /><br />.potx<br /><br />pps<br /><br />ppsm<br /><br />ppsx<br /><br />.ppt<br /><br />.pptm<br /><br />.pptx<br /><br />.vdw<br /><br />.vsd|.vsdm<br /><br /> .vsdx<br /><br />.vss<br /><br />.vssm<br /><br />.vst<br /><br />.vstm<br /><br />.vssx<br /><br />.vstx<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />xltm<br /><br />.xltx|

Tipi di file aggiuntivi supportano la classificazione anche quando sono protetti. Per altre informazioni su questi file, vedere la sezione [Tipi di file supportati per la classificazione e la protezione](#supported-file-types-for-classification-and-protection).

Di seguito sono riportati alcuni esempi.

- Se l'etichetta di riservatezza **generale** applica la classificazione e non applica la protezione: è possibile applicare l'etichetta **generale** a un file denominato Sales. pdf, ma non è possibile applicare questa etichetta a un file denominato Sales. txt. 

- Se l'etichetta **riservata \ tutti i dipendenti** applica la classificazione e la protezione: è possibile applicare questa etichetta a un file denominato Sales. pdf e a un file denominato Sales. txt. È possibile applicare solo la protezione a questi file, senza applicare la classificazione.

## <a name="file-types-supported-for-protection"></a>Tipi di file supportati per la protezione

Il Azure Information Protection client di etichetta unificata supporta la protezione a due livelli diversi, come descritto nella tabella seguente.

|Tipo di protezione|Nativa|Generica|
|----------------------|----------|-----------|
|Description|Per file di testo e immagine, file di Microsoft Office (Word, Excel e PowerPoint), file con estensione pdf e altri tipi di file di applicazione che supportano un servizio Rights Management, la protezione nativa offre un forte livello di protezione che include crittografia e applicazione di diritti (autorizzazioni).|Per tutte le altre applicazioni e gli altri tipi di file, la protezione generica offre un livello di protezione che include funzionalità di incapsulamento dei file, usando il tipo di file pfile, e di autenticazione per verificare se un utente è autorizzato ad aprire il file.|
|Protection|La protezione dei file viene applicata nei modi seguenti:<br /><br />- Prima di eseguire il rendering del contenuto protetto, è necessario che venga eseguita l'autenticazione per coloro che ricevono il file tramite posta elettronica o a cui viene concesso l'accesso al file tramite autorizzazioni di file o condivisione.<br /><br />- Vengono anche applicati tutti i diritti di utilizzo e i criteri impostati dal proprietario del contenuto al momento dell'applicazione della protezione ai file quando viene eseguito il rendering del contenuto nel visualizzatore Azure Information Protection (per i file di testo e immagine protetti) o nell'applicazione associata (per tutti gli altri tipi di file supportati).|La protezione dei file viene applicata nei modi seguenti:<br /><br />- Prima di eseguire il rendering del contenuto protetto, è necessario che venga eseguita l'autenticazione per coloro che sono autorizzati ad aprire il file e a cui viene concesso l'accesso al file. Se l'autorizzazione non riesce, il file non viene aperto.<br /><br />- Vengono visualizzati i diritti di utilizzo e i criteri impostati dal proprietario del contenuto per comunicare agli utenti autorizzati i criteri di utilizzo previsti.<br /><br />- Viene effettuata la registrazione di controllo dell'apertura di file e dell'accesso a questi da parte di utenti autorizzati. I diritti di utilizzo, tuttavia, non vengono applicati.|
|Livello predefinito per tipi di file|Questo è il livello predefinito di protezione per i tipi di file seguenti:<br /><br />- File di testo e immagine<br /><br />- File di Microsoft Office (Word, Excel, PowerPoint)<br /><br />- Formato di documento portatile (.pdf)<br /><br />Per altre informazioni, vedere la sezione che segue, [Tipi di file supportati per la classificazione e la protezione](#supported-file-types-for-classification-and-protection).|Questa è la protezione predefinita per tutti gli altri tipi di file (ad esempio i file con estensione vsdx, rtf e così via) che non sono supportati dalla protezione nativa.|

Non è possibile modificare il livello di protezione predefinito a cui si applica il client di etichetta unificato Azure Information Protection o lo scanner. Tuttavia, è possibile modificare i tipi di file protetti. Per ulteriori informazioni, vedere [modificare i tipi di file da proteggere](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect).

La protezione può essere applicata automaticamente quando un utente seleziona un'etichetta di riservatezza configurata da un amministratore oppure gli utenti possono specificare le proprie impostazioni di protezione personalizzate usando i [livelli di autorizzazione](../configure-usage-rights.md#rights-included-in-permissions-levels). 

### <a name="file-sizes-supported-for-protection"></a>Dimensioni dei file supportati per la protezione

Sono disponibili dimensioni massime per i file che la Azure Information Protection client Unified Labeling supporta per la protezione.

- **Per i file di Office:**


  |                                                     Applicazione di Office                                                      |                                                Dimensione massima del file supportata                                                 |
  |-----------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
  |             Word 2010<br /><br />Word 2013<br /><br />Word 2016             |                                          32 bit: 512 MB<br /><br />64 bit: 512 MB                                          |
  |           Excel 2010<br /><br />Excel 2013<br /><br />Excel 2016           |                      32 bit: 2 GB<br /><br />64 bit: limitato solo dalla memoria e dallo spazio disponibile su disco                       |
  | PowerPoint 2010<br /><br />PowerPoint 2013<br /><br />PowerPoint 2016 | 32 bit: limitato solo dalla memoria e dallo spazio disponibile su disco<br /><br />64 bit: limitato solo dalla memoria e dallo spazio disponibile su disco |


- **Per tutti gli altri file**: 

  - Per proteggere altri tipi di file e aprire questi tipi di file nel visualizzatore Azure Information Protection: le dimensioni massime dei file sono limitate solo dalla memoria e dallo spazio su disco disponibili.

  - Per rimuovere la protezione dai file tramite il cmdlet [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile): le dimensioni massime del file supportate per i file con estensione pst sono 5 GB. Gli altri tipi di file sono limitati solo dalla memoria e dallo spazio disponibile su disco.

    Suggerimento: se occorre cercare o recuperare elementi protetti in file PST di grandi dimensioni, vedere [Linee guida per l'uso di Unprotect-RMSFile per eDiscovery](../configure-super-users.md#guidance-for-using-unprotect-rmsfile-for-ediscovery).

### <a name="supported-file-types-for-classification-and-protection"></a>Tipi di file supportati per la classificazione e la protezione

La tabella seguente elenca un subset di tipi di file che supportano la protezione nativa dal client Azure Information Protection Unified Labeling e che possono anche essere classificati. 

Questi tipi di file vengono identificati separatamente perché quando sono protetti in modo nativo l'estensione del nome file originale viene modificata e i file diventano di sola lettura. Si noti che se i file sono protetti in modo generico, l'estensione del nome file originale viene sempre modificata in pfile.

> [!WARNING]
> Se si dispone di firewall, proxy Web o software di protezione che esaminano e agiscono in base alle estensioni di file, potrebbe essere necessario riconfigurare tali software e dispositivi di rete per supportare queste nuove estensioni.

|Estensione del file originale|Estensione dei file protetti|
|--------------------------------|-------------------------------------|
|txt|ptxt|
|.xml|pxml|
|.jpg|pjpg|
|jpeg|pjpeg|
|.png|ppng|
|.tif|.ptif|
|tiff|ptiff|
|bmp|pbmp|
|.gif|pgif|
|jpe|pjpe|
|jfif|pjfif|
|jt|pjt|

Nella tabella seguente sono elencati i tipi di file rimanenti che supportano la protezione nativa dal client Azure Information Protection Unified Labeling e che possono anche essere classificati. Questi sono riconoscibili come tipi di file delle app di Microsoft Office. I formati di file supportati per questi tipi di file sono i formati 97-2003 e Office Open XML per i programmi di Office seguenti: Word, Excel e PowerPoint.

Per questi file, l'estensione del nome di file rimane invariata dopo che il file è stato protetto da un servizio Rights Management.

|Tipi di file supportati da Office|Tipi di file supportati da Office|
|----------------------------------|----------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />dot<br /><br />.dotm<br /><br />.dotx<br /><br />potm<br /><br />.potx<br /><br />pps<br /><br />ppsm<br /><br />ppsx<br /><br />.ppt<br /><br />.pptm<br /><br />.pptx<br /><br />.vsdm|.vsdx<br /><br />.vssm<br /><br />.vssx<br /><br />.vstm<br /><br />.vstx<br /><br />xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />xltm<br /><br />.xltx<br /><br />.xps|


## <a name="file-types-that-are-excluded-from-classification-and-protection"></a>Tipi di file esclusi dalla classificazione e dalla protezione

Per impedire agli utenti di modificare file critici per il funzionamento del computer, alcuni tipi di file e cartelle vengono automaticamente esclusi dalla classificazione e dalla protezione. Se gli utenti provano a classificare o proteggere questi file usando il client Azure Information Protection Unified Labeling, visualizzano un messaggio che ne è escluso.

- **Tipi di file esclusi**: INK, EXE, COM, CMD, BAT, DLL, INI, PST, SCA, DRM, SYS, CPL, INF, DRV, DAT, TMP, MSP, MSI, PDB, JAR
    
    > [!NOTE]
    > Diversamente dal client classico, i file con estensione msg non vengono esclusi. Attualmente, non è possibile aprire correttamente i file con estensione msg classificati e protetti. Per questi file, rimuovere l'etichetta per aprire il file.

- **Cartelle escluse**: 
    - Windows
    - Programmi (\Programmi e \Programmi (x86))
    - ProgramData 
    - \AppData (per tutti gli utenti)

### <a name="file-types-that-are-excluded-from-classification-and-protection-by-the-azure-information-protection-scanner"></a>Tipi di file esclusi dalla classificazione e dalla protezione dallo scanner di Azure Information Protection

Per impostazione predefinita, lo scanner esclude anche gli stessi tipi di file del client di Azure Information Protection Unified Labeling con le eccezioni seguenti:

- sono esclusi anche i messaggi di errore, RTF e rar.

È possibile modificare i tipi di file inclusi o esclusi per l'analisi dei file eseguita dallo scanner:

- Configurare **Tipi di file da analizzare** nel profilo dello scanner [usando il portale di Azure](../deploy-aip-scanner.md#configure-the-scanner-in-the-azure-portal).
    
    > [!NOTE]
    > A causa del problema noto per i file con estensione msg descritti in dettaglio nella sezione precedente, è consigliabile che i file con estensione msg siano esclusi.
    > 
    > Se si includono nell'analisi i file con estensione rtf, monitorare attentamente lo scanner. Alcuni file con estensione rtf non possono essere controllati dallo scanner: per questi file l'ispezione non viene completata ed è necessario riavviare il servizio. 

Per impostazione predefinita lo scanner protegge solo i tipi di file di Office e i file PDF se questi sono protetti usando lo standard ISO per la crittografia dei file PDF. Per modificare questo comportamento per lo scanner, usare l'impostazione avanzata di PowerShell, **PFileSupportedExtensions**. Per altre informazioni, vedere [configurazione di PowerShell per modificare i tipi di file protetti](../deploy-aip-scanner.md#scanner-from-the-unified-labeling-client-use-powershell-to-change-which-file-types-are-protected) dalle istruzioni per la distribuzione dello scanner.

### <a name="files-that-cannot-be-protected-by-default"></a>File che non possono essere protetti per impostazione predefinita

Qualsiasi file protetto da password non può essere protetto in modo nativo dal client Azure Information Protection Unified Labeling, a meno che il file non sia attualmente aperto nell'applicazione che applica la protezione. Spesso sono i file con estensione pdf ad essere protetti da password, ma anche altre applicazioni, come ad esempio le app di Office,offrono questa funzionalità.

### <a name="limitations-for-container-files-such-as-zip-files"></a>Limitazioni per i file contenitore (ad esempio, file con estensione zip)

I file contenitore sono file che contengono altri file, ad esempio i file con estensione zip che contengono file compressi. Altri esempi includono file con estensione rar, 7z e msg e documenti PDF che includono allegati.

È possibile classificare e proteggere i file contenitore, ma la classificazione e la protezione non vengono applicate ai singoli file all'interno del contenitore.

Se è presente un file contenitore che include file classificati e protetti, è necessario estrarre i file per modificarne le impostazioni di classificazione o protezione.

Il visualizzatore di Azure Information Protection non supporta l'apertura di allegati in un documento PDF protetto. In questo scenario, quando il documento viene aperto nel visualizzatore, gli allegati non sono visibili.

## <a name="file-types-supported-for-inspection"></a>Tipi di file supportati per il controllo

Senza alcuna configurazione aggiuntiva, il client Azure Information Protection Unified labeling usa il filtro IFilter di Windows per esaminare il contenuto dei documenti. Windows IFilter viene usato da Windows Search per l'indicizzazione. Di conseguenza, è possibile controllare i tipi di file seguenti quando si usa il comando di PowerShell [set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification) .

|Tipo di applicazione|Tipo file|
|--------------------------------|-------------------------------------|
|Word|doc docx;. docm;. dot;. dotm;. dotx|
|Excel|.xls; .xlt; .xlsx; .xltx; .xltm; .xlsm; .xlsb|
|PowerPoint|.ppt; .pps; .pot; .pptx; .ppsx; .pptm; .ppsm; .potx; .potm|
|PDF |.pdf|
|Testo|.txt; .xml; .csv|

Con impostazioni di configurazione aggiuntive è possibile esaminare anche altri tipi di file. Ad esempio, è possibile [registrare un'estensione di file personalizzata per usare il gestore di filtro di Windows esistente per i file di testo](https://docs.microsoft.com/windows/desktop/search/-search-ifilter-registering-filters), ed è anche possibile installare filtri aggiuntivi di produttori di software.

Per verificare quali filtri sono installati, vedere la sezione [Finding a Filter Handler for a Given File Extension](https://docs.microsoft.com/windows/desktop/search/-search-ifilter-registering-filters#finding-a-filter-handler-for-a-given-file-extension) (Come trovare un gestore filtri per un'estensione di file data) nella Guida sviluppatori di Windows Search.

Le sezioni seguenti includono istruzioni di configurazione per il controllo dei file con estensione zip e tiff.

### <a name="to-inspect-zip-files"></a>Per esaminare i file con estensione zip

Lo scanner di Azure Information Protection e il comando di PowerShell [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification) consentono di esaminare i file con estensione zip se si seguono queste istruzioni:

1. Per il computer che esegue lo scanner o la sessione di PowerShell, installare [Office 2010 Filter Pack SP2](https://support.microsoft.com/en-us/help/2687447/description-of-office-2010-filter-pack-sp2).

2. Per lo scanner: dopo aver individuato le informazioni riservate, se il file zip deve essere classificato e protetto con un'etichetta, specificare l'estensione zip con l'impostazione avanzata di PowerShell, **PFileSupportedExtensions**, come descritto in [configurazione di PowerShell per modificare i tipi di file protetti](../deploy-aip-scanner.md#scanner-from-the-unified-labeling-client-use-powershell-to-change-which-file-types-are-protected) dalle istruzioni per la distribuzione dello scanner.


Scenario di esempio dopo avere eseguito questi passaggi: 

Un file denominato **accounts.zip** contiene fogli di calcolo di Excel con i numeri di carta di credito. Si dispone di un'etichetta di **riservatezza denominata Confidential \ Finance**, configurata per individuare i numeri di carta di credito e applicare automaticamente l'etichetta con la protezione che limita l'accesso al gruppo Finance. 

Dopo aver esaminato il file, il client Unified Labeling dalla sessione di PowerShell classifica il file come **Confidential \ Finance**, applica la protezione generica al file in modo che solo i membri dei gruppi finance possano decomprimerlo e rinominare il file **accounts. zip. Pfile**.

### <a name="to-inspect-tiff-files-by-using-ocr"></a>Per esaminare i file con estensione tiff tramite OCR

Il comando di PowerShell [set-AIPFileClassiciation](/powershell/module/azureinformationprotection/set-aipfileclassification) può usare il riconoscimento ottico dei caratteri (OCR) per controllare le immagini TIFF con estensione TIFF quando si installa la funzionalità IFilter TIFF di Windows e quindi configurare le [impostazioni di IFilter TIFF di Windows](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/dd744701%28v%3dws.10%29) nel computer che esegue la sessione di PowerShell.

Per lo scanner: dopo aver individuato le informazioni riservate, se il file con estensione TIFF deve essere classificato e protetto con un'etichetta, specificare questa estensione di file con l'impostazione avanzata di PowerShell, **PFileSupportedExtensions**, come descritto in [configurazione di PowerShell per modificare i tipi di file protetti](../deploy-aip-scanner.md#scanner-from-the-unified-labeling-client-use-powershell-to-change-which-file-types-are-protected) dalle istruzioni per la distribuzione dello scanner.

## <a name="next-steps"></a>Passaggi successivi
Ora che sono stati identificati i tipi di file supportati dal client Azure Information Protection Unified Labeling, vedere le risorse seguenti per altre informazioni che potrebbero essere necessarie per supportare questo client:

- [Personalizzazioni](clientv2-admin-guide-customizations.md)

- [File del client e registrazione dell'utilizzo](clientv2-admin-guide-files-and-logging.md)

- [Comandi di PowerShell](clientv2-admin-guide-powershell.md)

