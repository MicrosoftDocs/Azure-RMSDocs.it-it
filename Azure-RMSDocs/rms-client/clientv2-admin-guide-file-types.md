---
title: File types supported - Azure Information Protection unified labeling client
description: Technical details about supported file types, file name extensions, and levels of protection for admins who are are responsible for the Azure Information Protection unified labeling client for Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/21/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: bf386685847f10ecead59ac59c44620f03372d6d
ms.sourcegitcommit: fed1df1858f8316f7dd45e751c6910b444651a87
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/25/2019
ms.locfileid: "74474246"
---
# <a name="admin-guide-file-types-supported-by-the-azure-information-protection-unified-labeling-client"></a>Admin Guide: File types supported by the Azure Information Protection unified labeling client

>*Applies to: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 with SP1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*>
>
> *Instructions for: [Azure Information Protection unified labeling client for Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

The Azure Information Protection unified labeling client can apply the following to documents and emails:

- Solo classificazione

- Classificazione e protezione

- Solo protezione

The Azure Information Protection unified labeling client can also inspect the content of some file types using well-known sensitive information types or regular expressions that you define.

Use the following information to check which file types the Azure Information Protection unified labeling client supports, understand the different levels of protection and how to change the default protection level, and to identify which files are automatically excluded (skipped) from classification and protection.

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

- If the **General** sensitivity label applies classification and does not apply protection: You could apply the **General** label to a file named sales.pdf but you could not apply this label to a file named sales.txt. 

- If the **Confidential \ All Employees** sensitivity label applies classification and protection: You could apply this label to a file named sales.pdf and a file named sales.txt. È possibile applicare solo la protezione a questi file, senza applicare la classificazione.

## <a name="file-types-supported-for-protection"></a>Tipi di file supportati per la protezione

The Azure Information Protection unified labeling client supports protection at two different levels, as described in the following table.

|Tipo di protezione|Nativo|Generica|
|----------------------|----------|-----------|
|Description|Per file di testo e immagine, file di Microsoft Office (Word, Excel e PowerPoint), file con estensione pdf e altri tipi di file di applicazione che supportano un servizio Rights Management, la protezione nativa offre un forte livello di protezione che include crittografia e applicazione di diritti (autorizzazioni).|Per tutte le altre applicazioni e gli altri tipi di file, la protezione generica offre un livello di protezione che include funzionalità di incapsulamento dei file, usando il tipo di file pfile, e di autenticazione per verificare se un utente è autorizzato ad aprire il file.|
|Protection|La protezione dei file viene applicata nei modi seguenti:<br /><br />- Prima di eseguire il rendering del contenuto protetto, è necessario che venga eseguita l'autenticazione per coloro che ricevono il file tramite posta elettronica o a cui viene concesso l'accesso al file tramite autorizzazioni di file o condivisione.<br /><br />- Vengono anche applicati tutti i diritti di utilizzo e i criteri impostati dal proprietario del contenuto al momento dell'applicazione della protezione ai file quando viene eseguito il rendering del contenuto nel visualizzatore Azure Information Protection (per i file di testo e immagine protetti) o nell'applicazione associata (per tutti gli altri tipi di file supportati).|La protezione dei file viene applicata nei modi seguenti:<br /><br />- Prima di eseguire il rendering del contenuto protetto, è necessario che venga eseguita l'autenticazione per coloro che sono autorizzati ad aprire il file e a cui viene concesso l'accesso al file. Se l'autorizzazione non riesce, il file non viene aperto.<br /><br />- Vengono visualizzati i diritti di utilizzo e i criteri impostati dal proprietario del contenuto per comunicare agli utenti autorizzati i criteri di utilizzo previsti.<br /><br />- Viene effettuata la registrazione di controllo dell'apertura di file e dell'accesso a questi da parte di utenti autorizzati. I diritti di utilizzo, tuttavia, non vengono applicati.|
|Livello predefinito per tipi di file|Questo è il livello predefinito di protezione per i tipi di file seguenti:<br /><br />- File di testo e immagine<br /><br />- File di Microsoft Office (Word, Excel, PowerPoint)<br /><br />- Formato di documento portatile (.pdf)<br /><br />Per altre informazioni, vedere la sezione che segue, [Tipi di file supportati per la classificazione e la protezione](#supported-file-types-for-classification-and-protection).|Questa è la protezione predefinita per tutti gli altri tipi di file (ad esempio i file con estensione vsdx, rtf e così via) che non sono supportati dalla protezione nativa.|

You cannot change the default protection level that the Azure Information Protection unified labeling client or the scanner applies. However, you can change which file types are protected. For more information, see [Change which file types to protect](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect).

The protection can be applied automatically when a user selects a sensitivity label that an administrator has configured, or users can specify their own custom protection settings by using [permission levels](../configure-usage-rights.md#rights-included-in-permissions-levels). 

### <a name="file-sizes-supported-for-protection"></a>Dimensioni dei file supportati per la protezione

There are maximum file sizes that the Azure Information Protection unified labeling client supports for protection.

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

The following table lists a subset of file types that support native protection by the Azure Information Protection unified labeling client, and that can also be classified. 

Questi tipi di file vengono identificati separatamente perché quando sono protetti in modo nativo l'estensione del nome file originale viene modificata e i file diventano di sola lettura. Si noti che se i file sono protetti in modo generico, l'estensione del nome file originale viene sempre modificata in pfile.

> [!WARNING]
> Se si dispone di firewall, proxy Web o software di protezione che esaminano e agiscono in base alle estensioni di file, potrebbe essere necessario riconfigurare tali software e dispositivi di rete per supportare queste nuove estensioni.

|Estensione del file originale|Estensione dei file protetti|
|--------------------------------|-------------------------------------|
|.txt|ptxt|
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

The next table lists the remaining file types that support native protection by the Azure Information Protection unified labeling client, and that can also be classified. Questi sono riconoscibili come tipi di file delle app di Microsoft Office. I formati di file supportati per questi tipi di file sono i formati 97-2003 e Office Open XML per i programmi di Office seguenti: Word, Excel e PowerPoint.

Per questi file, l'estensione del nome di file rimane invariata dopo che il file è stato protetto da un servizio Rights Management.

|Tipi di file supportati da Office|Tipi di file supportati da Office|
|----------------------------------|----------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />dot<br /><br />.dotm<br /><br />.dotx<br /><br />potm<br /><br />.potx<br /><br />pps<br /><br />ppsm<br /><br />ppsx<br /><br />.ppt<br /><br />.pptm<br /><br />.pptx<br /><br />.vsdm|.vsdx<br /><br />.vssm<br /><br />.vssx<br /><br />.vstm<br /><br />.vstx<br /><br />xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />xltm<br /><br />.xltx<br /><br />.xps|


## <a name="file-types-that-are-excluded-from-classification-and-protection"></a>Tipi di file esclusi dalla classificazione e dalla protezione

Per impedire agli utenti di modificare file critici per il funzionamento del computer, alcuni tipi di file e cartelle vengono automaticamente esclusi dalla classificazione e dalla protezione. If users try to classify or protect these files by using the Azure Information Protection unified labeling client, they see a message that they are excluded.

- **Tipi di file esclusi**: INK, EXE, COM, CMD, BAT, DLL, INI, PST, SCA, DRM, SYS, CPL, INF, DRV, DAT, TMP, MSP, MSI, PDB, JAR
    
    > [!NOTE]
    > Unlike the classic client, .msg files are not excluded. Currently, there is a known issue with .msg files that are classified and protected as ".msg.pfile" and you cannot open these files. For these files, remove the label to open the file.

- **Cartelle escluse**: 
    - Windows
    - Programmi (\Programmi e \Programmi (x86))
    - ProgramData 
    - \AppData (per tutti gli utenti)

### <a name="file-types-that-are-excluded-from-classification-and-protection-by-the-azure-information-protection-scanner"></a>Tipi di file esclusi dalla classificazione e dalla protezione dallo scanner di Azure Information Protection

By default, the scanner also excludes the same file types as the Azure Information Protection unified labeling client with the following exceptions:

- .msg, .rtf, and .rar, are also excluded

È possibile modificare i tipi di file inclusi o esclusi per l'analisi dei file eseguita dallo scanner:

- Configurare **Tipi di file da analizzare** nel profilo dello scanner [usando il portale di Azure](../deploy-aip-scanner.md#configure-the-scanner-in-the-azure-portal).
    
    > [!NOTE]
    > Because of the known issue for .msg files detailed in the previous section, we recommend you keep .msg files as excluded.
    > 
    > Se si includono nell'analisi i file con estensione rtf, monitorare attentamente lo scanner. Alcuni file con estensione rtf non possono essere controllati dallo scanner: per questi file l'ispezione non viene completata ed è necessario riavviare il servizio. 

Per impostazione predefinita lo scanner protegge solo i tipi di file di Office e i file PDF se questi sono protetti usando lo standard ISO per la crittografia dei file PDF. To change this behavior for the scanner, use the PowerShell advanced setting, **PFileSupportedExtensions**. For more information, see [PowerShell configuration to change which file types are protected](../deploy-aip-scanner.md#scanner-from-the-unified-labeling-client-use-powershell-to-change-which-file-types-are-protected) from the scanner deployment instructions.

### <a name="files-that-cannot-be-protected-by-default"></a>File che non possono essere protetti per impostazione predefinita

Any file that is password-protected cannot be natively protected by the Azure Information Protection unified labeling client unless the file is currently open in the application that applies the protection. Spesso sono i file con estensione pdf ad essere protetti da password, ma anche altre applicazioni, come ad esempio le app di Office,offrono questa funzionalità.

### <a name="limitations-for-container-files-such-as-zip-files"></a>Limitazioni per i file contenitore (ad esempio, file con estensione zip)

I file contenitore sono file che contengono altri file, ad esempio i file con estensione zip che contengono file compressi. Altri esempi includono file con estensione rar, 7z e msg e documenti PDF che includono allegati.

È possibile classificare e proteggere i file contenitore, ma la classificazione e la protezione non vengono applicate ai singoli file all'interno del contenitore.

Se è presente un file contenitore che include file classificati e protetti, è necessario estrarre i file per modificarne le impostazioni di classificazione o protezione.

Il visualizzatore di Azure Information Protection non supporta l'apertura di allegati in un documento PDF protetto. In questo scenario, quando il documento viene aperto nel visualizzatore, gli allegati non sono visibili.

## <a name="file-types-supported-for-inspection"></a>Tipi di file supportati per il controllo

Without any additional configuration, the Azure Information Protection unified labeling client uses Windows IFilter to inspect the contents of documents. Windows IFilter viene usato da Windows Search per l'indicizzazione. As a result, the following file types can be inspected when you use the [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification) PowerShell command.

|Tipo di applicazione|Tipo file|
|--------------------------------|-------------------------------------|
|Word|.doc; docx; .docm; .dot; .dotm; .dotx|
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

2. For the scanner: After finding sensitive information, if the .zip file should be classified and protected with a label, specify the .zip file name extension with the PowerShell advanced setting, **PFileSupportedExtensions**, as described in [PowerShell configuration to change which file types are protected](../deploy-aip-scanner.md#scanner-from-the-unified-labeling-client-use-powershell-to-change-which-file-types-are-protected) from the scanner deployment instructions.


Scenario di esempio dopo avere eseguito questi passaggi: 

Un file denominato **accounts.zip** contiene fogli di calcolo di Excel con i numeri di carta di credito. You have a sensitivity label named **Confidential \ Finance**, which is configured to discover credit card numbers and automatically apply the label with protection that restricts access to the Finance group. 

After inspecting the file, the unified labeling client from your PowerShell session classifies this file as **Confidential \ Finance**, applies generic protection to the file so that only members of the Finance groups can unzip it, and renames the file **accounts.zip.pfile**.

### <a name="to-inspect-tiff-files-by-using-ocr"></a>Per esaminare i file con estensione tiff tramite OCR

The [Set-AIPFileClassiciation](/powershell/module/azureinformationprotection/set-aipfileclassification) PowerShell command can use optical character recognition (OCR) to inspect TIFF images with a .tiff file name extension when you install the Windows TIFF IFilter feature, and then configure [Windows TIFF IFilter Settings](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/dd744701%28v%3dws.10%29) on the computer running the PowerShell session.

For the scanner: After finding sensitive information, if the .tiff file should be classified and protected with a label, specify this file name extension with the PowerShell advanced setting, **PFileSupportedExtensions**, as described in [PowerShell configuration to change which file types are protected](../deploy-aip-scanner.md#scanner-from-the-unified-labeling-client-use-powershell-to-change-which-file-types-are-protected) from the scanner deployment instructions.

## <a name="next-steps"></a>Passaggi successivi
Now that you've identified the file types supported by the Azure Information Protection unified labeling client, see the following resources for additional information that you might need to support this client:

- [Personalizzazioni](clientv2-admin-guide-customizations.md)

- [File del client e registrazione dell'utilizzo](clientv2-admin-guide-files-and-logging.md)

- [Comandi di PowerShell](clientv2-admin-guide-powershell.md)

