---
title: Tipi di file supportati dal Azure Information Protection (AIP) Unified Labeling client
description: Informazioni sui tipi di file e le dimensioni supportati per il client Unified Labeling Azure Information Protection (AIP) per Windows.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/07/2021
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 22a30abf5ea3bf63e5a352bb8b68ceb852036794
ms.sourcegitcommit: 8a45d209273d748ee0f2a96c97893288c0b7efa5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/08/2021
ms.locfileid: "102446916"
---
# <a name="file-types-supported-by-the-azure-information-protection-aip-unified-labeling-client"></a>Tipi di file supportati dal Azure Information Protection (AIP) Unified Labeling client

>***Si applica a** [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012*>
>
>*Se si dispone di Windows 7 o Office 2010, vedere [AIP e versioni legacy di Windows e Office](../known-issues.md#aip-and-legacy-windows-and-office-versions).*
>
>***Pertinente per**: [AIP Unified Labeling client only](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client classico, vedere [tipi di file client classici](client-admin-guide-file-types.md)*

Questo articolo elenca i tipi di file e le dimensioni supportati dal client di assegnazione unificata di Azure Information Protection (AIP)

> [!NOTE]
> Per i tipi di file elencati, i percorsi WebDav non sono supportati.
> 
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
    |doc<br /><br />docm<br /><br />docx<br /><br />dot<br /><br />dotm<br /><br />dotx<br /><br />potm<br /><br />potx<br /><br />pps<br /><br />ppsm<br /><br />ppsx<br /><br />ppt<br /><br />pptm<br /><br />pptx<br /><br />.vdw<br /><br />vsd|.vsdm<br /><br /> .vsdx<br /><br />.vss<br /><br />.vssm<br /><br />.vst<br /><br />.vstm<br /><br />.vssx<br /><br />.vstx<br /><br />xls<br /><br />xlsb<br /><br />xlt<br /><br />xlsm<br /><br />xlsx<br /><br />xltm<br /><br />xltx|
    | | |

Gli altri tipi di file supportano la classificazione quando vengono anche protetti. Per altre informazioni su questi file, vedere la sezione [Tipi di file supportati per la classificazione e la protezione](#supported-file-types-for-classification-and-protection).

Esempi:

- Se l'etichetta di riservatezza **generale** applica la classificazione e non applica la protezione: è possibile applicare l'etichetta **generale** a un file denominato sales.pdf ma non è stato possibile applicare questa etichetta a un file denominato sales.txt.

- Se l'etichetta **riservata \ tutti i dipendenti** applica la classificazione e la protezione: è possibile applicare questa etichetta a un file denominato sales.pdf e a un file denominato sales.txt. È possibile applicare solo la protezione a questi file, senza applicare la classificazione.

## <a name="file-types-supported-for-protection"></a>Tipi di file supportati per la protezione

Il Azure Information Protection client di etichetta unificata supporta la protezione a due livelli diversi, come descritto nella tabella seguente.

|Tipo di protezione|Nativo|Generico|
|----------------------|----------|-----------|
|**Descrizione**|Per file di testo e immagine, file di Microsoft Office (Word, Excel e PowerPoint), file con estensione pdf e altri tipi di file di applicazione che supportano un servizio Rights Management, la protezione nativa offre un forte livello di protezione che include crittografia e applicazione di diritti (autorizzazioni).|Per gli altri tipi di file supportati, la protezione generica fornisce un livello di protezione che include sia l'incapsulamento dei file con il tipo di file. Pfile che l'autenticazione per verificare se un utente è autorizzato ad aprire il file.|
|**Protezione**|La protezione dei file viene applicata nei modi seguenti:<br /><br />-Prima del rendering del contenuto protetto, è necessario che venga eseguita l'autenticazione per gli utenti che ricevono il file tramite posta elettronica o a cui viene concesso l'accesso tramite autorizzazioni file o condivisione.<br /><br />- Vengono anche applicati tutti i diritti di utilizzo e i criteri impostati dal proprietario del contenuto al momento dell'applicazione della protezione ai file quando viene eseguito il rendering del contenuto nel visualizzatore Azure Information Protection (per i file di testo e immagine protetti) o nell'applicazione associata (per tutti gli altri tipi di file supportati).|La protezione dei file viene applicata nei modi seguenti:<br /><br />- Prima di eseguire il rendering del contenuto protetto, è necessario che venga eseguita l'autenticazione per coloro che sono autorizzati ad aprire il file e a cui viene concesso l'accesso al file. Se l'autorizzazione non riesce, il file non viene aperto.<br /><br />- Vengono visualizzati i diritti di utilizzo e i criteri impostati dal proprietario del contenuto per comunicare agli utenti autorizzati i criteri di utilizzo previsti.<br /><br />- Viene effettuata la registrazione di controllo dell'apertura di file e dell'accesso a questi da parte di utenti autorizzati. I diritti di utilizzo, tuttavia, non vengono applicati.|
|**Livello predefinito per tipi di file**|Livello di protezione predefinito per i tipi di file seguenti:<br /><br />- File di testo e immagine<br /><br />- File di Microsoft Office (Word, Excel, PowerPoint)<br /><br />- Formato di documento portatile (.pdf)<br /><br />Per altre informazioni, vedere la sezione che segue, [Tipi di file supportati per la classificazione e la protezione](#supported-file-types-for-classification-and-protection).|Protezione predefinita per tutti gli altri tipi di file (ad esempio. vsdx,. RTF e così via) che non sono supportati dalla protezione nativa.|
| | |

Non è possibile modificare il livello di protezione predefinito a cui si applica il client di etichetta unificato Azure Information Protection o lo scanner. Tuttavia, è possibile modificare i tipi di file protetti. Per ulteriori informazioni, vedere [modificare i tipi di file da proteggere](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect).

La protezione può essere applicata automaticamente quando un utente seleziona un'etichetta di riservatezza configurata da un amministratore oppure gli utenti possono specificare le proprie impostazioni di protezione personalizzate usando i [livelli di autorizzazione](../configure-usage-rights.md#rights-included-in-permissions-levels).

### <a name="file-sizes-supported-for-protection"></a>Dimensioni dei file supportati per la protezione

Sono disponibili dimensioni massime per i file che la Azure Information Protection client Unified Labeling supporta per la protezione.

**Per i file di Office**:

|                                                     Applicazione di Office                                                      |                                                Dimensione massima del file supportata                                                 |
|-----------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
|             Word 2010<br /><br />Word 2013<br /><br />Word 2016             |                                          32 bit: 512 MB<br /><br />64 bit: 512 MB                                          |
|           Excel 2010<br /><br />Excel 2013<br /><br />Excel 2016           |                      32 bit: 2 GB<br /><br />64 bit: limitato solo dalla memoria e dallo spazio disponibile su disco                       |
| PowerPoint 2010<br /><br />PowerPoint 2013<br /><br />PowerPoint 2016 | 32 bit: limitato solo dalla memoria e dallo spazio disponibile su disco<br /><br />64 bit: limitato solo dalla memoria e dallo spazio disponibile su disco |
| | |

> [!IMPORTANT]
> Supporto "Extended" per Office 2010 terminato il 13 ottobre 2020. Per altre informazioni, vedere [AIP e versioni legacy di Windows e Office](../known-issues.md#aip-and-legacy-windows-and-office-versions).
>

**Per tutti gli altri file**:

- **Per proteggere altri tipi di file** e per aprire questi tipi di file nel Visualizzatore Azure Information Protection: le dimensioni massime del file sono limitate solo dalla memoria e dallo spazio disponibile su disco.

- **Per rimuovere la protezione dei file** tramite il cmdlet [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) : le dimensioni massime del file supportate per i file con estensione pst sono pari a 5 GB. Gli altri tipi di file sono limitati solo dalla memoria e dallo spazio disponibile su disco.

> [!TIP]
> Per cercare o ripristinare gli elementi protetti in file con estensione pst di grandi dimensioni, vedere le [linee guida per l'uso di Unprotect-RMSFile per eDiscovery](../configure-super-users.md#guidance-for-using-unprotect-rmsfile-for-ediscovery).
> 
### <a name="supported-file-types-for-classification-and-protection"></a>Tipi di file supportati per la classificazione e la protezione

La tabella seguente elenca un subset di tipi di file che supportano la protezione nativa dal client Azure Information Protection Unified Labeling e che possono anche essere classificati.

Questi tipi di file vengono identificati separatamente perché quando sono protetti in modo nativo l'estensione del nome file originale viene modificata e i file diventano di sola lettura. Quando i file sono protetti in modo generico, l'estensione del nome file originale viene sempre modificata in `.p<file-type>` .

> [!WARNING]
> Se si dispone di firewall, proxy Web o software di protezione che esaminano e agiscono in base alle estensioni di file, potrebbe essere necessario riconfigurare tali software e dispositivi di rete per supportare queste nuove estensioni.

|Estensione del file originale|Estensione dei file protetti|
|--------------------------------|-------------------------------------|
|bmp|pbmp|
|gif|pgif|
|jfif|pjfif|
|jpe|pjpe|
|jpeg|pjpeg|
|jpg|pjpg|
|jt|pjt|
|png|ppng|
|tif|.ptif|
|tiff|ptiff|
|.txt|ptxt|
|xla |.pxla | 
|xlam |.pxlam |
|xml|pxml|
| | |

**Tipi di file supportati da Office**

L'elenco seguente include i tipi di file rimanenti che supportano la protezione nativa da parte del client Azure Information Protection Unified Labeling e che possono anche essere classificati. Questi sono riconoscibili come tipi di file delle app di Microsoft Office. I formati di file supportati per questi tipi di file sono i formati 97-2003 e Office Open XML per i programmi di Office seguenti: Word, Excel e PowerPoint.

Per questi file, l'estensione del nome file *rimane invariata* dopo che il file è protetto da un servizio Rights Management.

:::row:::
   :::column span="4":::
doc

docm

docx

dot

dotm

dotx

potm

   :::column-end:::
   :::column span="":::

potx

pps

ppsm

ppsx

ppt

pptm

pptx


   :::column-end:::
   :::column span="":::
.vsdm

.vsdx

.vssm

.vssx

.vstm

.vstx

xls

   :::column-end:::
   :::column span="":::

xlsb

xlt

xlsm

xlsx

xltm

xltx

xps
   :::column-end:::
:::row-end:::

## <a name="file-types-excluded-from-classification-and-protection"></a>Tipi di file esclusi dalla classificazione e dalla protezione

Per impedire agli utenti di modificare file critici per il funzionamento del computer, alcuni tipi di file e cartelle vengono automaticamente esclusi dalla classificazione e dalla protezione. Se gli utenti provano a classificare o proteggere questi file usando il client Azure Information Protection Unified Labeling, visualizzano un messaggio che ne è escluso.

- **Tipi di file esclusi**: INK, EXE, COM, CMD, BAT, DLL, INI, PST, SCA, DRM, SYS, CPL, INF, DRV, DAT, TMP, MSP, MSI, PDB, JAR

- **Cartelle escluse**:
    - Windows
    - Programmi (\Programmi e \Programmi (x86))
    - ProgramData
    - \AppData (per tutti gli utenti)

### <a name="file-types-that-are-excluded-from-classification-and-protection-by-the-azure-information-protection-scanner"></a>Tipi di file esclusi dalla classificazione e dalla protezione dallo scanner di Azure Information Protection

Per impostazione predefinita, lo scanner esclude anche gli stessi tipi di file del client di Azure Information Protection Unified labeling. 

Per lo scanner vengono esclusi anche i seguenti tipi di file:. msg,. RTF e. rar

Per modificare i tipi di file inclusi o esclusi per l'ispezione dei file dallo scanner, configurare i **tipi di file da analizzare** nel [processo di analisi del contenuto](../deploy-aip-scanner-configure-install.md#configure-the-scanner-in-the-azure-portal).
    
> [!NOTE]
> Se si includono file con estensione RTF per l'analisi, è consigliabile monitorare attentamente lo scanner. Alcuni file con estensione rtf non possono essere controllati dallo scanner: per questi file l'ispezione non viene completata ed è necessario riavviare il servizio.

Per impostazione predefinita lo scanner protegge solo i tipi di file di Office e i file PDF se questi sono protetti usando lo standard ISO per la crittografia dei file PDF. Per modificare questo comportamento per lo scanner, usare l'impostazione avanzata di PowerShell, **PFileSupportedExtensions**. Per altre informazioni, vedere [usare PowerShell per modificare i tipi di file protetti](../deploy-aip-scanner-configure-install.md#change-which-file-types-to-protect) dalle istruzioni per la distribuzione dello scanner.

### <a name="files-that-cannot-be-protected-by-default"></a>File che non possono essere protetti per impostazione predefinita

Qualsiasi file protetto da password non può essere protetto in modo nativo dal client Azure Information Protection Unified Labeling, a meno che il file non sia attualmente aperto nell'applicazione che applica la protezione. Spesso sono i file con estensione pdf ad essere protetti da password, ma anche altre applicazioni, come ad esempio le app di Office,offrono questa funzionalità.

### <a name="limitations-for-container-files-such-as-zip-files"></a>Limitazioni per i file contenitore (ad esempio, file con estensione zip)

Per ulteriori informazioni, vedere la [Azure Information Protection problemi noti](../known-issues.md#client-support-for-container-files-such-as-zip-files).

## <a name="file-types-supported-for-inspection"></a>Tipi di file supportati per il controllo

Senza alcuna configurazione aggiuntiva, il client Azure Information Protection Unified Labeling utilizza Windows IFilter per esaminare il contenuto dei documenti. Windows IFilter viene usato da Windows Search per l'indicizzazione. Di conseguenza, è possibile controllare i tipi di file seguenti quando si usa il comando di PowerShell [set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification) .

|Tipo di applicazione|Tipo file|
|--------------------------------|-------------------------------------|
|**Word**|doc docx;. docm;. dot;. dotm;. dotx|
|**Excel**|.xls; .xlt; .xlsx; .xltx; .xltm; .xlsm; .xlsb|
|**PowerPoint**|.ppt; .pps; .pot; .pptx; .ppsx; .pptm; .ppsm; .potx; .potm|
|**PDF** |pdf|
|**Text**|.txt; .xml; .csv|
| | | |

Con la configurazione aggiuntiva, è anche possibile controllare altri tipi di file. Ad esempio, è possibile [registrare un'estensione di file personalizzata per utilizzare il gestore filtro Windows esistente per i file di testo](/windows/desktop/search/-search-ifilter-registering-filters)ed è possibile installare altri filtri dai fornitori di software.

Per verificare quali filtri sono installati, vedere la sezione [Finding a Filter Handler for a Given File Extension](/windows/desktop/search/-search-ifilter-registering-filters#finding-a-filter-handler-for-a-given-file-extension) (Come trovare un gestore filtri per un'estensione di file data) nella Guida sviluppatori di Windows Search.

Le sezioni seguenti includono istruzioni di configurazione per il controllo dei file con estensione zip e tiff.

### <a name="to-inspect-zip-files"></a>Per esaminare i file con estensione zip

Lo scanner di Azure Information Protection e il comando di PowerShell [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification) consentono di esaminare i file con estensione zip se si seguono queste istruzioni:

1. Per il computer che esegue lo scanner o la sessione di PowerShell, installare [Office 2010 Filter Pack SP2](https://support.microsoft.com/help/2687447/description-of-office-2010-filter-pack-sp2).

2. Per lo scanner: dopo aver individuato le informazioni riservate, se il file zip deve essere classificato e protetto con un'etichetta, specificare l'estensione zip con l'impostazione avanzata di PowerShell, **PFileSupportedExtensions**, come descritto in [usare PowerShell per modificare i tipi di file protetti](../deploy-aip-scanner-configure-install.md#change-which-file-types-to-protect) dalle istruzioni per la distribuzione dello scanner.

Scenario di esempio dopo avere eseguito questi passaggi:

Un file denominato **accounts.zip** contiene fogli di calcolo di Excel con i numeri di carta di credito. Si dispone di un'etichetta di **riservatezza denominata Confidential \ Finance**, configurata per individuare i numeri di carta di credito e applicare automaticamente l'etichetta con la protezione che limita l'accesso al gruppo Finance.

Dopo aver esaminato il file, il client Unified Labeling dalla sessione di PowerShell classifica il file come **Confidential \ Finance**, applica la protezione generica al file in modo che solo i membri dei gruppi finance possano decomprimerlo e rinominare il file **accounts.zip. Pfile**.

### <a name="to-inspect-tiff-files-by-using-ocr"></a>Per esaminare i file con estensione tiff tramite OCR

Il comando di PowerShell [set-AIPFileClassiciation](/powershell/module/azureinformationprotection/set-aipfileclassification) può usare il riconoscimento ottico dei caratteri (OCR) per controllare le immagini TIFF con estensione TIFF quando si installa la funzionalità IFilter TIFF di Windows e quindi configurare le [impostazioni di IFilter TIFF di Windows](/previous-versions/windows/it-pro/windows-7/dd744701(v=ws.10)) nel computer che esegue la sessione di PowerShell.

Per lo scanner: dopo aver individuato le informazioni riservate, se il file con estensione TIFF deve essere classificato e protetto con un'etichetta, specificare questa estensione di file con l'impostazione avanzata di PowerShell, **PFileSupportedExtensions**, come descritto in [usare PowerShell per modificare i tipi di file protetti](../deploy-aip-scanner-configure-install.md#change-which-file-types-to-protect) dalle istruzioni per la distribuzione dello scanner.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni, vedere:

- [Personalizzazioni](clientv2-admin-guide-customizations.md)

- [File del client e registrazione dell'utilizzo](clientv2-admin-guide-files-and-logging.md)

- [Comandi di PowerShell](clientv2-admin-guide-powershell.md)