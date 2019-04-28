---
title: Tipi di file supportati dal client Azure Information Protection unified l'assegnazione di etichette
description: Dettagli tecnici sui tipi di file supportati, estensioni di file e i livelli di protezione per gli amministratori che sono responsabili per il client di assegnazione di etichette unificato di Azure Information Protection per Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: aca0fe5d3d9624676bc2bb12a772f5b753eb1a0d
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60183756"
---
# <a name="admin-guide-file-types-supported-by-the-azure-information-protection-unified-labeling-client"></a>Guida dell'amministratore: Tipi di file supportati dal client Azure Information Protection unified l'assegnazione di etichette

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*>
>
> *Istruzioni per: [Azure Information Protection unified client per l'assegnazione di etichette per Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Il client di assegnazione di etichette unificato di Azure Information Protection è possibile applicare quanto segue a documenti e messaggi di posta elettronica:

- Solo classificazione

- Classificazione e protezione

- Solo protezione

Il client di assegnazione di etichette unificato di Azure Information Protection è anche possibile esaminare il contenuto di alcuni tipi di file utilizzando tipi di informazioni riservate noto o espressioni regolari definite.

Usare le informazioni seguenti per verificare quali tipi di file supporta il client di assegnazione di etichette unificato di Azure Information Protection, comprendere i diversi livelli di protezione e come modificare il livello di protezione predefinito e per identificare quali file vengono automaticamente esclusi (ignorati) dalla classificazione e protezione.

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
    |.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm<br /><br />.pptx<br /><br />.vdw<br /><br />.vsd|.vsdm<br /><br /> .vsdx<br /><br />.vss<br /><br />.vssm<br /><br />.vst<br /><br />.vstm<br /><br />.vssx<br /><br />.vstx<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx|

Tipi di file aggiuntivi supportano la classificazione anche quando sono protetti. Per altre informazioni su questi file, vedere la sezione [Tipi di file supportati per la classificazione e la protezione](#supported-file-types-for-classification-and-protection).

Esempi:

- Se il **generale** etichetta di riservatezza si applica alla classificazione e non applicare la protezione: È possibile applicare l'etichetta **Generale** a un file denominato sales.pdf, ma non a un file denominato sales.txt. 

- Se il **riservato \ tutti i dipendenti** si applica etichetta di riservatezza di classificazione e protezione: È possibile applicare questa etichetta a un file denominato sales.pdf, ma non a un file denominato sales.txt. È possibile applicare solo la protezione a questi file, senza applicare la classificazione.

## <a name="file-types-supported-for-protection"></a>Tipi di file supportati per la protezione

Il client di assegnazione di etichette unificato di Azure Information Protection supporta la protezione a due livelli diversi, come descritto nella tabella seguente.

|Tipo di protezione|Nativo|Generico|
|----------------------|----------|-----------|
|Descrizione|Per file di testo e immagine, file di Microsoft Office (Word, Excel e PowerPoint), file con estensione pdf e altri tipi di file di applicazione che supportano un servizio Rights Management, la protezione nativa offre un forte livello di protezione che include crittografia e applicazione di diritti (autorizzazioni).|Per tutte le altre applicazioni e tipi di file, la protezione generica fornisce un livello di protezione che include sia l’incapsulamento di file mediante l'autenticazione e il tipo di file .pfile per verificare se un utente è autorizzato per aprire il file.|
|Protezione|La protezione dei file viene applicata nei modi seguenti:<br /><br />- Prima di eseguire il rendering del contenuto protetto, è necessario che venga eseguita l'autenticazione per coloro che ricevono il file tramite posta elettronica o a cui viene concesso l'accesso al file tramite autorizzazioni di file o condivisione.<br /><br />- Vengono anche applicati tutti i diritti di utilizzo e i criteri impostati dal proprietario del contenuto al momento dell'applicazione della protezione ai file quando viene eseguito il rendering del contenuto nel visualizzatore Azure Information Protection (per i file di testo e immagine protetti) o nell'applicazione associata (per tutti gli altri tipi di file supportati).|La protezione dei file viene applicata nei modi seguenti:<br /><br />- Prima di eseguire il rendering del contenuto protetto, è necessario che venga eseguita l'autenticazione per coloro che sono autorizzati ad aprire il file e a cui viene concesso l'accesso al file. Se l'autorizzazione ha esito negativo, il file non si apre.<br /><br />- Vengono visualizzati i diritti di utilizzo e i criteri impostati dal proprietario del contenuto per comunicare agli utenti autorizzati i criteri di utilizzo previsti.<br /><br />- Viene effettuata la registrazione di controllo dell'apertura di file e dell'accesso a questi da parte di utenti autorizzati. I diritti di utilizzo, tuttavia, non vengono applicati.|
|Impostazione predefinita per i tipi di file|Questo è il livello predefinito di protezione per i tipi di file seguenti:<br /><br />- File di testo e immagine<br /><br />- File di Microsoft Office (Word, Excel, PowerPoint)<br /><br />- Formato di documento portatile (.pdf)<br /><br />Per altre informazioni, vedere la sezione che segue, [Tipi di file supportati per la classificazione e la protezione](#supported-file-types-for-classification-and-protection).|Questa è la protezione predefinita per tutti gli altri tipi di file (ad esempio i file con estensione vsdx, rtf e così via) che non sono supportati dalla protezione nativa.|

È possibile modificare il livello di protezione predefinito che il client di assegnazione di etichette unificato di Azure Information Protection applica. È possibile modificare il livello predefinito nativo a generico, da generico a nativo e anche evitare che il client di assegnazione di etichette unificato di Azure Information Protection da applicare la protezione. Per altre informazioni, vedere la sezione [Modifica del livello di protezione predefinito dei file](#changing-the-default-protection-level-of-files) in questo articolo.

La protezione può essere applicata automaticamente quando un utente seleziona un'etichetta di riservatezza che un amministratore ha configurato o gli utenti possono specificare le proprie impostazioni di protezione personalizzate utilizzando [livelli di autorizzazione](../configure-usage-rights.md#rights-included-in-permissions-levels). 

### <a name="file-sizes-supported-for-protection"></a>Dimensioni dei file supportati per la protezione

Esistono dimensioni massime dei file supportati dal client Azure Information Protection unified imprevisto delle etichette per la protezione.

- **Per i file di Office:**


  |                                                     Applicazione di Office                                                      |                                                Dimensione massima del file supportata                                                 |
  |-----------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
  |             Word 2010<br /><br />Word 2013<br /><br />Word 2016             |                                          32 bit: 512 MB<br /><br />64 bit: 512 MB                                          |
  |           Excel 2010<br /><br />Excel 2013<br /><br />Excel 2016           |                      32 bit: 2 GB<br /><br />64 bit: limitato solo dalla memoria e dallo spazio disponibile su disco                       |
  | PowerPoint 2010<br /><br />PowerPoint 2013<br /><br />PowerPoint 2016 | 32 bit: limitato solo dalla memoria e dallo spazio disponibile su disco<br /><br />64 bit: limitato solo dalla memoria e dallo spazio disponibile su disco |


- **Per tutti gli altri file**: 

  - Per proteggere altri tipi di file e aprire questi tipi di file nel visualizzatore Azure Information Protection: le dimensioni massime dei file sono limitate solo dallo spazio disponibile su disco e dalla memoria disponibile.

  - Per rimuovere la protezione dei file tramite il cmdlet [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile): le dimensioni massime dei file supportate sono pari a 5 GB. Gli altri tipi di file sono limitati solo dalla memoria e dallo spazio disponibile su disco.

    Suggerimento: se è necessario cercare o recuperare elementi protetti in file PST di grandi dimensioni, vedere [Linee guida per l'uso di Unprotect-RMSFile per eDiscovery](../configure-super-users.md#guidance-for-using-unprotect-rmsfile-for-ediscovery).

### <a name="supported-file-types-for-classification-and-protection"></a>Tipi di file supportati per la classificazione e la protezione

Nella tabella seguente elenca un subset dei tipi di file che supportano la protezione nativa dal client Azure Information Protection unified l'assegnazione di etichette e che può anche essere classificata. 

Questi tipi di file vengono identificati separatamente perché quando sono protetti in modo nativo l'estensione del nome file originale viene modificata e i file diventano di sola lettura. Si noti che se i file sono protetti in modo generico, l'estensione del nome file originale viene sempre modificata in pfile.

> [!WARNING]
> Se si dispone di firewall, proxy Web o software di protezione che esaminano e agiscono in base alle estensioni di file, potrebbe essere necessario riconfigurare tali software e dispositivi di rete per supportare queste nuove estensioni.

|Estensione dei file originali|Estensione dei file protetti|
|--------------------------------|-------------------------------------|
|.txt|.ptxt|
|.xml|.pxml|
|.jpg|.pjpg|
|.jpeg|.pjpeg|
|.png|.ppng|
|.tif|.ptif|
|.tiff|.ptiff|
|.bmp|.pbmp|
|.gif|.pgif|
|.jpe|.pjpe|
|.jfif|.pjfif|
|.jt|.pjt|

La tabella seguente elenca i rimanenti tipi di file che supportano la protezione nativa dal client Azure Information Protection unified l'assegnazione di etichette e che può anche essere classificata. Questi sono riconoscibili come tipi di file delle app di Microsoft Office. I formati di file supportati per questi tipi di file sono i formati 97-2003 e Office Open XML per i programmi di Office seguenti: Word, Excel e PowerPoint.

Per questi file, l'estensione del nome di file rimane invariata dopo che il file è stato protetto da un servizio Rights Management.

|Tipi di file supportati da Office|Tipi di file supportati da Office|
|----------------------------------|----------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm<br /><br />.pptx<br /><br />.vsdm|.vsdx<br /><br />.vssm<br /><br />.vssx<br /><br />.vstm<br /><br />.vstx<br /><br />.xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />.xps|

### <a name="changing-the-default-protection-level-of-files"></a>Modifica del livello di protezione predefinito dei file
È possibile modificare come il client di assegnazione di etichette unificato di Azure Information Protection protegge i file modificando il Registro di sistema. Ad esempio, è possibile forzare i file che supportano la protezione nativa che vengano protetti genericamente dal client Azure Information Protection unified imprevisto delle etichette.

Motivi per cui è possibile eseguire questa operazione:

- Per verificare che tutti gli utenti possano aprire il file se non dispongono di un'applicazione che supporta la protezione nativa.

- Per ospitare i sistemi di sicurezza che intervengono sui file tramite l'estensione del nome di file e possono essere riconfigurati per adattare l'estensione .pfile ma non possono essere riconfigurati per gestire più estensioni di nome di file per la protezione nativa.

Analogamente, è possibile forzare il client di assegnazione di etichette unificato di Azure Information Protection per applicare la protezione nativa ai file di cui per impostazione predefinita, verrebbe applicata la protezione generica. Questa azione potrebbe essere appropriata se si ha un'applicazione che supporta le API RMS, ad esempio, un'applicazione line-of-business scritta da sviluppatori interni oppure acquistata da un fornitore di software indipendente (ISV).

È anche possibile forzare il client di imprevisto delle etichette unificato di Azure Information Protection a bloccare la protezione dei file (si applica protezione nativa o generica). Ad esempio, questa azione potrebbe essere necessaria se si ha un'applicazione automatica o un servizio che deve essere in grado di aprire un file specifico per elaborare il relativo contenuto. Quando si blocca la protezione per un tipo di file, gli utenti non è possibile usare il client di assegnazione di etichette unificato di Azure Information Protection per proteggere un file con quel tipo di file. Quando tentano, viene visualizzato un messaggio in base al quale l'amministratore ha impedito la protezione ed è necessario annullare la loro azione per proteggere il file.

Per configurare il client di assegnazione di etichette unificato di Azure Information Protection per applicare la protezione generica a tutti i file cui per impostazione predefinita, verrebbe applicata la protezione nativa, apportare le modifiche seguenti al Registro di sistema. Se la chiave FileProtection non esiste, è necessario crearla manualmente.

1. Creare una nuova chiave denominata * per il percorso del Registro di sistema seguente, che indica i file con qualsiasi estensione del nome file:

    - Per una versione di Windows a 32 bit: **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection**

    - Per una versione di Windows a 64 bit: **HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\FileProtection** e **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection**

2. Nella nuova chiave aggiunta (ad esempio HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\\\*), creare un nuovo valore stringa (REG_SZ) denominato **Encryption** con valore dati **Pfile**.

    Questa impostazione ha come risultato l'applicazione della protezione generica da parte del client Azure Information Protection.

Queste due impostazioni conseguenza il client l'assegnazione di etichette unificato Azure Information Protection Applica protezione generica a tutti i file che hanno un'estensione di file. Se questo è l'obiettivo, non è richiesta alcuna ulteriore configurazione. Tuttavia, è possibile definire eccezioni per specifici tipi di file, in modo che siano protetti comunque in modo nativo. A tale scopo, è necessario apportare 3 (per Windows a 32 bit) o 6 (per Windows a 64 bit) modifiche aggiuntive del Registro di sistema per ogni tipo di file:

1. Per **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection** e **HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\FileProtection** (se applicabile): Aggiungere una nuova chiave con il nome dell'estensione di file (senza il punto iniziale).

    Ad esempio, i file con estensione del nome di file .docx, creano una chiave denominata **DOCX**.

2. nella nuova chiave aggiunta per il tipo di file, ad esempio **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX**, creare un nuovo valore DWORD denominato **AllowPFILEEncryption** con valore **0**.

3. Nella nuova chiave aggiunta per il tipo di file, ad esempio **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RmsSharingApp\FileProtection\DOCX**, creare un nuovo valore stringa denominato **Encryption** con valore **Native**.

In seguito a queste impostazioni, tutti i file sono protetti in modo generico ad eccezione dei file con estensione docx, Questi file sono protetti in modo nativo dal client Azure Information Protection unified imprevisto delle etichette.

Ripetere questi tre passaggi per altri tipi di file che si desidera definire come eccezioni, in quanto supportano la protezione nativa e non dovranno essere protetti in modo generico dal client Azure Information Protection unified imprevisto delle etichette.

È possibile apportare modifiche di registro di sistema simile per altri scenari modificando il valore della stringa **Crittografia** che supporta i seguenti valori:

- **Pfile**: protezione generica

- **Native**: protezione nativa

- **Off**: Protezione di blocco

Dopo aver apportato queste modifiche del Registro di sistema, non è necessario riavviare il computer. Tuttavia, se si usano i comandi di PowerShell per proteggere i file, è necessario avviare una nuova sessione di PowerShell per rendere effettive le modifiche.

Per altre informazioni sulla modifica del Registro di sistema per modificare il livello di protezione predefinito dei file, vedere [Configurazione dell'API file](../develop/file-api-configuration.md) nelle linee guida per sviluppatori. Per fare riferimento alla protezione generica, questa documentazione per sviluppatori usa il termine "PFile".

## <a name="file-types-that-are-excluded-from-classification-and-protection"></a>Tipi di file esclusi dalla classificazione e dalla protezione

Per impedire agli utenti di modificare file critici per il funzionamento del computer, alcuni tipi di file e cartelle vengono automaticamente esclusi dalla classificazione e dalla protezione. Se gli utenti provano a classificare o proteggere questi file usando il client di assegnazione di etichette unificato di Azure Information Protection, viene visualizzato un messaggio che sono esclusi.

- **Tipi di file esclusi**: lnk, exe, com, cmd, bat, dll, ini, pst, sca, drm, sys, cpl, inf, drv, dat, tmp, msg, msp, msi, pdb, jar


- **Cartelle escluse**: 
    - Windows
    - Programmi (\Programmi e \Programmi (x86))
    - ProgramData 
    - \AppData (per tutti gli utenti)


### <a name="files-that-cannot-be-protected-by-default"></a>File che non possono essere protetti per impostazione predefinita

Qualsiasi file che è protetto da password non può essere protetti in modo nativo dal client Azure Information Protection unified l'assegnazione di etichette, a meno che il file è attualmente aperto nell'applicazione che applica la protezione. Spesso sono i file con estensione pdf ad essere protetti da password, ma anche altre applicazioni, come ad esempio le app di Office,offrono questa funzionalità.

### <a name="limitations-for-container-files-such-as-zip-files"></a>Limitazioni per i file contenitore (ad esempio, file con estensione zip)

I file contenitore sono file che contengono altri file, ad esempio i file con estensione zip che contengono file compressi. Altri esempi includono file con estensione rar, 7z e msg e documenti PDF che includono allegati.

È possibile classificare e proteggere i file contenitore, ma la classificazione e la protezione non vengono applicate ai singoli file all'interno del contenitore.

Se è presente un file contenitore che include file classificati e protetti, è necessario estrarre i file per modificarne le impostazioni di classificazione o protezione.

Il visualizzatore di Azure Information Protection non supporta l'apertura di allegati in un documento PDF protetto. In questo scenario, quando il documento viene aperto nel visualizzatore, gli allegati non sono visibili.

## <a name="next-steps"></a>Passaggi successivi
Dopo aver identificato i tipi di file supportati dal client Azure Information Protection unified l'assegnazione di etichette, vedere le risorse seguenti per informazioni aggiuntive che potrebbe essere necessario supportare il client:

- [Personalizzazioni](clientv2-admin-guide-customizations.md)

- [File del client e registrazione dell'utilizzo](clientv2-admin-guide-files-and-logging.md)

- [Comandi di PowerShell](clientv2-admin-guide-powershell.md)

