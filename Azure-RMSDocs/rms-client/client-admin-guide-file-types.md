---
title: Tipi di file supportati-client Azure Information Protection
description: Dettagli tecnici sui tipi di file supportati, le estensioni di file e i livelli di protezione per gli amministratori che sono responsabili del client Azure Information Protection per Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/26/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ''
ms.subservice: v1client
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 350f687a61899046346f26b5beb2944b9f3caf13
ms.sourcegitcommit: 3464f9224b34dc54ad6fc1b7bc4dc11ad1ab8d59
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/28/2019
ms.locfileid: "72984882"
---
# <a name="admin-guide-file-types-supported-by-the-azure-information-protection-client"></a>Guida dell'amministratore: Tipi di file supportati dal client Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, windows server 2019, windows server 2016, windows Server 2012 R2, windows Server 2012, windows Server 2008 R2*
>
> *Istruzioni per: [client di Azure Information Protection per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Il client Azure Information Protection permette di applicare quanto segue a documenti e messaggi di posta elettronica:

- Solo classificazione

- Classificazione e protezione

- Solo protezione

Il client Azure Information Protection può anche esaminare il contenuto di alcuni tipi di file che usano tipi di informazioni riservate noti o espressioni regolari definite dall'utente.

Usare le informazioni seguenti per verificare quali tipi di file sono supportati dal client di Azure Information Protection, comprendere i diversi livelli di protezione e come modificare il livello di protezione predefinito e individuare quali file vengono automaticamente esclusi (ignorati) dalla classificazione e dalla protezione.

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

Ad esempio, nei [criteri predefiniti](../configure-policy-default.md) correnti l'etichetta **Generale** si applica alla classificazione e non alla protezione. È possibile applicare l'etichetta **Generale** a un file denominato sales.pdf, ma non a un file denominato sales.txt. 

Anche nei criteri predefiniti correnti l'etichetta **Riservato \ Tutti i dipendenti** si applica a classificazione e protezione. È possibile applicare questa etichetta a un file denominato sales.pdf, ma non a un file denominato sales.txt. È possibile applicare solo la protezione a questi file, senza applicare la classificazione.

## <a name="file-types-supported-for-protection"></a>Tipi di file supportati per la protezione

Il client Azure Information Protection supporta la protezione a due livelli diversi, come descritto nella tabella seguente.

|Tipo di protezione|Nativo|Generica|
|----------------------|----------|-----------|
|Description|Per file di testo e immagine, file di Microsoft Office (Word, Excel e PowerPoint), file con estensione pdf e altri tipi di file di applicazione che supportano un servizio Rights Management, la protezione nativa offre un forte livello di protezione che include crittografia e applicazione di diritti (autorizzazioni).|Per tutte le altre applicazioni e gli altri tipi di file, la protezione generica offre un livello di protezione che include funzionalità di incapsulamento dei file, usando il tipo di file pfile, e di autenticazione per verificare se un utente è autorizzato ad aprire il file.|
|Protection|La protezione dei file viene applicata nei modi seguenti:<br /><br />- Prima di eseguire il rendering del contenuto protetto, è necessario che venga eseguita l'autenticazione per coloro che ricevono il file tramite posta elettronica o a cui viene concesso l'accesso al file tramite autorizzazioni di file o condivisione.<br /><br />- Vengono anche applicati tutti i diritti di utilizzo e i criteri impostati dal proprietario del contenuto al momento dell'applicazione della protezione ai file quando viene eseguito il rendering del contenuto nel visualizzatore Azure Information Protection (per i file di testo e immagine protetti) o nell'applicazione associata (per tutti gli altri tipi di file supportati).|La protezione dei file viene applicata nei modi seguenti:<br /><br />- Prima di eseguire il rendering del contenuto protetto, è necessario che venga eseguita l'autenticazione per coloro che sono autorizzati ad aprire il file e a cui viene concesso l'accesso al file. Se l'autorizzazione non riesce, il file non viene aperto.<br /><br />- Vengono visualizzati i diritti di utilizzo e i criteri impostati dal proprietario del contenuto per comunicare agli utenti autorizzati i criteri di utilizzo previsti.<br /><br />- Viene effettuata la registrazione di controllo dell'apertura di file e dell'accesso a questi da parte di utenti autorizzati. I diritti di utilizzo, tuttavia, non vengono applicati.|
|Livello predefinito per tipi di file|Questo è il livello predefinito di protezione per i tipi di file seguenti:<br /><br />- File di testo e immagine<br /><br />- File di Microsoft Office (Word, Excel, PowerPoint)<br /><br />- Formato di documento portatile (.pdf)<br /><br />Per altre informazioni, vedere la sezione che segue, [Tipi di file supportati per la classificazione e la protezione](#supported-file-types-for-classification-and-protection).|Questa è la protezione predefinita per tutti gli altri tipi di file (ad esempio i file con estensione vsdx, rtf e così via) che non sono supportati dalla protezione nativa.|

È possibile modificare il livello di protezione predefinito applicato dal client Azure Information Protection. È possibile modificare il livello predefinito da nativo a generico, da generico a nativo e anche impedire al client Azure Information Protection di applicare la protezione. Per altre informazioni, vedere la sezione [Modifica del livello di protezione predefinito dei file](#changing-the-default-protection-level-of-files) in questo articolo.

La protezione dei dati può essere applicata automaticamente quando un utente seleziona un'etichetta configurata da un amministratore oppure gli utenti possono specificare impostazioni di protezione personalizzate tramite [livelli di autorizzazione](../configure-usage-rights.md#rights-included-in-permissions-levels). 

### <a name="file-sizes-supported-for-protection"></a>Dimensioni dei file supportati per la protezione

Esistono dimensioni massime dei file supportati dal client Azure Information Protection per la protezione.

- **Per i file di Office:**


  |                                                     Applicazione di Office                                                      |                                                Dimensione massima del file supportata                                                 |
  |-----------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
  |             Word 2007 (supportato solo da AD RMS)<br /><br />Word 2010<br /><br />Word 2013<br /><br />Word 2016             |                                          32 bit: 512 MB<br /><br />64 bit: 512 MB                                          |
  |           Excel 2007 (supportato solo da AD RMS)<br /><br />Excel 2010<br /><br />Excel 2013<br /><br />Excel 2016           |                      32 bit: 2 GB<br /><br />64 bit: limitato solo dalla memoria e dallo spazio disponibile su disco                       |
  | PowerPoint 2007 (supportato solo da AD RMS)<br /><br />PowerPoint 2010<br /><br />PowerPoint 2013<br /><br />PowerPoint 2016 | 32 bit: limitato solo dalla memoria e dallo spazio disponibile su disco<br /><br />64 bit: limitato solo dalla memoria e dallo spazio disponibile su disco |


- **Per tutti gli altri file**: 

  - Per proteggere altri tipi di file e aprire questi tipi di file nel visualizzatore Azure Information Protection: le dimensioni massime dei file sono limitate solo dalla memoria e dallo spazio su disco disponibili.

  - Per rimuovere la protezione dai file tramite il cmdlet [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile): le dimensioni massime del file supportate per i file con estensione pst sono 5 GB. Gli altri tipi di file sono limitati solo dalla memoria e dallo spazio disponibile su disco.

    Suggerimento: se occorre cercare o recuperare elementi protetti in file PST di grandi dimensioni, vedere [Linee guida per l'uso di Unprotect-RMSFile per eDiscovery](../configure-super-users.md#guidance-for-using-unprotect-rmsfile-for-ediscovery).

### <a name="supported-file-types-for-classification-and-protection"></a>Tipi di file supportati per la classificazione e la protezione

La tabella seguente elenca un subset di tipi di file che supportano la protezione nativa in base al client di Azure Information Protection e che possono anche essere classificati. 

Questi tipi di file vengono identificati separatamente perché quando sono protetti in modo nativo l'estensione del nome file originale viene modificata e i file diventano di sola lettura. Si noti che se i file sono protetti in modo generico, l'estensione del nome file originale viene sempre modificata in pfile.

> [!WARNING]
> Se si dispone di firewall, proxy Web o software di protezione che esaminano e agiscono in base alle estensioni di file, potrebbe essere necessario riconfigurare tali software e dispositivi di rete per supportare queste nuove estensioni.

|Estensione del file originale|Estensione dei file protetti|
|--------------------------------|-------------------------------------|
|.txt|ptxt|
|.xml|pxml|
|.jpg|pjpg|
|jpeg|pjpeg|
|.pdf|.ppdf [[1]](#footnote-1)|
|.png|ppng|
|.tif|.ptif|
|tiff|ptiff|
|bmp|pbmp|
|.gif|pgif|
|jpe|pjpe|
|jfif|pjfif|
|jt|pjt|

###### <a name="footnote-1"></a>Nota 1
Con l'ultima versione del client Azure Information Protection, [per impostazione predefinita](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption) l'estensione del documento PDF protetto rimane pdf.

La tabella successiva elenca i rimanenti tipi di file che supportano la protezione nativa in base al client di Azure Information Protection e che possono anche essere classificati. Questi sono riconoscibili come tipi di file delle app di Microsoft Office. I formati di file supportati per questi tipi di file sono i formati 97-2003 e Office Open XML per i programmi di Office seguenti: Word, Excel e PowerPoint.

Per questi file, l'estensione del nome di file rimane invariata dopo che il file è stato protetto da un servizio Rights Management.

|Tipi di file supportati da Office|Tipi di file supportati da Office|
|----------------------------------|----------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />dot<br /><br />.dotm<br /><br />.dotx<br /><br />potm<br /><br />.potx<br /><br />pps<br /><br />ppsm<br /><br />ppsx<br /><br />.ppt<br /><br />.pptm<br /><br />.pptx<br /><br />.vsdm|.vsdx<br /><br />.vssm<br /><br />.vssx<br /><br />.vstm<br /><br />.vstx<br /><br />xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />xltm<br /><br />.xltx<br /><br />.xps|

### <a name="changing-the-default-protection-level-of-files"></a>Cambiare il livello di protezione predefinito dei file
È possibile modificare il modo in cui il client Azure Information Protection protegge i file modificando il Registro di sistema. Ad esempio, è possibile forzare la protezione generica da parte del client Azure Information Protection per i file che supportano la protezione nativa.

Ecco i motivi per cui si potrebbe scegliere questa opzione:

- Per assicurarsi che tutti gli utenti possano aprire il file se non hanno un'applicazione che supporta la protezione nativa.

- Per supportare sistemi di sicurezza che agiscono sui file in base alla relativa estensione e che possono essere riconfigurati per supportare l'estensione pfile ma non diverse estensioni di file per la protezione nativa.

Analogamente, è possibile forzare il client Azure Information Protection ad applicare la protezione nativa ai file ai quali, per impostazione predefinita, viene applicata la protezione generica. Questa azione potrebbe essere appropriata se si ha un'applicazione che supporta le API RMS, ad esempio, un'applicazione line-of-business scritta da sviluppatori interni oppure acquistata da un fornitore di software indipendente (ISV).

È anche possibile forzare il client Azure Information Protection a bloccare la protezione dei file, ovvero a non applicare la protezione nativa o quella generica. Ad esempio, questa azione potrebbe essere necessaria se si ha un'applicazione automatica o un servizio che deve essere in grado di aprire un file specifico per elaborare il relativo contenuto. Quando si blocca la protezione per un tipo di file, gli utenti non possono usare il client Azure Information Protection per proteggere un file del tipo specificato. Se ci provano, visualizzano un messaggio che indica che l'amministratore ha impedito la protezione e devono quindi annullare l'azione di protezione del file.

Per configurare il client Azure Information Protection per l'applicazione della protezione generica a tutti i file per impostazione predefinita, apportare le modifiche seguenti al Registro di sistema. Se la chiave FileProtection non esiste, è necessario crearla manualmente.

1. Creare una nuova chiave denominata * per il percorso del Registro di sistema seguente, che indica i file con qualsiasi estensione del nome file:

    - Per la versione a 32 bit di Windows: **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection**

    - Per la versione a 64 bit di Windows: **HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\FileProtection** e **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection**

2. Nella nuova chiave aggiunta (ad esempio HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\\\*), creare un nuovo valore stringa (REG_SZ) denominato **Encryption** con valore dati **Pfile**.

    Questa impostazione ha come risultato l'applicazione della protezione generica da parte del client Azure Information Protection.

Queste due impostazioni hanno come risultato l'applicazione della protezione generica da parte del client Azure Information Protection a tutti i file dotati di estensione. Se è questo l'obiettivo, non è necessario eseguire altre configurazioni. È tuttavia possibile definire eccezioni per specifici tipi di file, in modo che vengano comunque protetti in modo nativo. A tale scopo, è necessario apportare 3 (per Windows a 32 bit) o 6 (per Windows a 64 bit) modifiche aggiuntive del Registro di sistema per ogni tipo di file:

1. Per **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection** e **HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\FileProtection** (se applicabile): aggiungere una nuova chiave con il nome dell'estensione di file (senza il periodo precedente).

    Ad esempio, i file con estensione del nome di file .docx, creano una chiave denominata **DOCX**.

2. nella nuova chiave aggiunta per il tipo di file, ad esempio **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX**, creare un nuovo valore DWORD denominato **AllowPFILEEncryption** con valore **0**.

3. Nella nuova chiave aggiunta per il tipo di file, ad esempio **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RmsSharingApp\FileProtection\DOCX**, creare un nuovo valore stringa denominato **Encryption** con valore **Native**.

In seguito a queste impostazioni, tutti i file sono protetti in modo generico ad eccezione dei file con estensione docx, che sono protetti in modo nativo dal client di Azure Information Protection.

Ripetere questi tre passaggi per altri tipi di file da definire come eccezioni, in quanto supportano la protezione nativa e non si vuole vengano protetti in modo generico dal client Azure Information Protection.

È possibile apportare modifiche di registro di sistema simile per altri scenari modificando il valore della stringa **Crittografia** che supporta i seguenti valori:

- **Pfile**: Protezione generica

- **Nativo**: Protezione nativa

- **Off**: Protezione di blocco

Dopo aver apportato queste modifiche del Registro di sistema, non è necessario riavviare il computer. Tuttavia, se si usano i comandi di PowerShell per proteggere i file, è necessario avviare una nuova sessione di PowerShell per rendere effettive le modifiche.

Per altre informazioni sulla modifica del Registro di sistema per modificare il livello di protezione predefinito dei file, vedere [Configurazione dell'API file](../develop/file-api-configuration.md) nelle linee guida per sviluppatori. Per fare riferimento alla protezione generica, questa documentazione per sviluppatori usa il termine "PFile".

## <a name="file-types-that-are-excluded-from-classification-and-protection"></a>Tipi di file esclusi dalla classificazione e dalla protezione

Per impedire agli utenti di modificare file critici per il funzionamento del computer, alcuni tipi di file e cartelle vengono automaticamente esclusi dalla classificazione e dalla protezione. Se gli utenti provano a classificare o proteggere questi file usando il client Azure Information Protection, viene visualizzato un messaggio per segnalare che sono esclusi.

- **Tipi di file esclusi**: lnk, exe, com, cmd, bat, dll, ini, pst, sca, drm, sys, cpl, inf, drv, dat, tmp, msg, msp, msi, pdb, jar


- **Cartelle escluse**: 
    - Windows
    - Programmi (\Programmi e \Programmi (x86))
    - ProgramData 
    - \AppData (per tutti gli utenti)

### <a name="file-types-that-are-excluded-from-classification-and-protection-by-the-azure-information-protection-scanner"></a>Tipi di file esclusi dalla classificazione e dalla protezione dallo scanner di Azure Information Protection

Per impostazione predefinita lo scanner esclude anche gli stessi tipi di file del client Azure Information Protection, con le eccezioni seguenti:

- Sono esclusi anche i file con estensione RTF e RAR

È possibile modificare i tipi di file inclusi o esclusi per l'analisi dei file eseguita dallo scanner:

- Configurare **Tipi di file da analizzare** nel profilo dello scanner [usando il portale di Azure](../deploy-aip-scanner.md#configure-the-scanner-in-the-azure-portal).

> [!NOTE]
> Se si includono nell'analisi i file con estensione rtf, monitorare attentamente lo scanner. Alcuni file con estensione rtf non possono essere controllati dallo scanner: per questi file l'ispezione non viene completata ed è necessario riavviare il servizio. 

Per impostazione predefinita lo scanner protegge solo i tipi di file di Office e i file PDF se questi sono protetti usando lo standard ISO per la crittografia dei file PDF. Per modificare questo comportamento per lo scanner, modificare il Registro di sistema e specificare i tipi di file aggiuntivi da proteggere. Per istruzioni, vedere [modifiche al registro di sistema per modificare i tipi di file protetti](../deploy-aip-scanner.md#scanner-from-the-classic-client-use-the-registry-to-change-which-file-types-are-protected) dalle istruzioni per la distribuzione dello scanner.

### <a name="files-that-cannot-be-protected-by-default"></a>File che non possono essere protetti per impostazione predefinita

Un file protetto da password non può essere protetto in modo nativo dal client Azure Information Protection a meno che il file non sia attualmente aperto nell'applicazione che applica la protezione. Spesso sono i file con estensione pdf ad essere protetti da password, ma anche altre applicazioni, come ad esempio le app di Office,offrono questa funzionalità.

Se si modifica il [comportamento predefinito](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption) del client Azure Information Protection in modo che protegga i file PDF con un'estensione di file ppdf, il client non può proteggere in modo nativo o rimuovere la protezione per i file PDF in una della situazioni seguenti:

- File PDF basato su modulo.

- File PDF protetto con estensione pdf.

    Il client di Azure Information Protection può proteggere un file PDF non protetto e può rimuovere la protezione di un file PDF protetto, o riproteggerlo, se il nome file ha estensione ppdf.

### <a name="limitations-for-container-files-such-as-zip-files"></a>Limitazioni per i file contenitore (ad esempio, file con estensione zip)

I file contenitore sono file che contengono altri file, ad esempio i file con estensione zip che contengono file compressi. Altri esempi includono file con estensione rar, 7z e msg e documenti PDF che includono allegati.

È possibile classificare e proteggere i file contenitore, ma la classificazione e la protezione non vengono applicate ai singoli file all'interno del contenitore.

Se è presente un file contenitore che include file classificati e protetti, è necessario estrarre i file per modificarne le impostazioni di classificazione o protezione. È possibile tuttavia rimuovere la protezione per tutti i file contenuti nei file contenitore supportati usando il cmdlet [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile).

Il visualizzatore di Azure Information Protection non supporta l'apertura di allegati in un documento PDF protetto. In questo scenario, quando il documento viene aperto nel visualizzatore, gli allegati non sono visibili.

## <a name="file-types-supported-for-inspection"></a>Tipi di file supportati per il controllo

Senza alcuna configurazione aggiuntiva, il client Azure Information Protection usa Windows IFilter per esaminare il contenuto dei documenti. Windows IFilter viene usato da Windows Search per l'indicizzazione. Di conseguenza è possibile esaminare i tipi di file seguenti quando si usa lo [scanner di Azure Information Protection](../deploy-aip-scanner.md) o il comando di PowerShell [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification).

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

2. Per lo scanner: dopo aver individuato le informazioni riservate, se il file zip deve essere classificato e protetto con un'etichetta, aggiungere una voce del registro di sistema per questa estensione di file per la protezione generica (Pfile), come descritto in [modifiche del registro di sistema per modificare i tipi di file sono protette](../deploy-aip-scanner.md#scanner-from-the-classic-client-use-the-registry-to-change-which-file-types-are-protected) dalle istruzioni per la distribuzione dello scanner.

Scenario di esempio dopo avere eseguito questi passaggi: 

Un file denominato **accounts.zip** contiene fogli di calcolo di Excel con i numeri di carta di credito. I criteri di Azure Information Protection includono un'etichetta denominata **Confidential \ Finance**, che è configurata per individuare i numeri di carta di credito e applicare automaticamente l'etichetta con una protezione che limita l'accesso al gruppo Finance. 

Dopo aver controllato il file, lo scanner lo classifica come **Confidential \ Finance**, applica la protezione generica al file in modo che solo i membri dei gruppi Finance possano decomprimerlo e lo rinomina **accounts.zip.pfile**.

### <a name="to-inspect-tiff-files-by-using-ocr"></a>Per esaminare i file con estensione tiff tramite OCR

Lo scanner Azure Information Protection e il comando di PowerShell [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification) possono anche usare una soluzione OCR (Optical Character Recognition) per esaminare immagini TIFF con estensione di file tiff quando si installa la funzionalità IFilter TIFF di Windows e quindi si configurano le [impostazioni IFilter TIFF di Windows](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/dd744701%28v%3dws.10%29) nel computer che esegue lo scanner o la sessione di PowerShell.

Per lo scanner: dopo aver individuato le informazioni riservate, se il file con estensione TIFF deve essere classificato e protetto con un'etichetta, aggiungere una voce del registro di sistema per questa estensione di file in modo che disponga della protezione nativa, come descritto in [modifiche del registro di sistema per modificare i tipi di file protetto](../deploy-aip-scanner.md#scanner-from-the-classic-client-use-the-registry-to-change-which-file-types-are-protected) dalle istruzioni per la distribuzione dello scanner.

## <a name="next-steps"></a>Passaggi successivi
Dopo aver identificato i tipi di file supportati dal client di Azure Information Protection, vedere le risorse seguenti per altre informazioni che potrebbero essere necessarie per supportare il client:

- [Personalizzazioni](client-admin-guide-customizations.md)

- [File del client e registrazione dell'utilizzo](client-admin-guide-files-and-logging.md)

- [Rilevamento dei documenti](client-admin-guide-document-tracking.md)

- [Comandi di PowerShell](client-admin-guide-powershell.md)

