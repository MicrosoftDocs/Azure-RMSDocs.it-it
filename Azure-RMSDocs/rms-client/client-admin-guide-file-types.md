---
title: Tipi di file supportati da Azure Information Protection
description: Dettagli tecnici sui tipi di file supportati, le estensioni di file e i livelli di protezione per gli amministratori che sono responsabili del client Azure Information Protection per Windows.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/15/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: fe75945793d28ed78b46f6b9a421bd7aa9ae3dfd
ms.sourcegitcommit: d5ce1bce5e63b3e510033ff9d4d246dd3511ed7c
translationtype: HT
---
# <a name="file-types-supported-by-the-azure-information-protection-client"></a>Tipi di file supportati dal client Azure Information Protection

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*

Il client Azure Information Protection permette di applicare quanto segue a documenti e messaggi di posta elettronica:

- Solo classificazione

- Classificazione e protezione

- Solo protezione

Usare le informazioni seguenti per verificare quali tipi di file sono supportati, i diversi livelli di protezione e come modificare il livello di protezione predefinito, nonché quali file vengono automaticamente esclusi (ignorati) dalla classificazione e dalla protezione.

## <a name="file-types-supported-for-classification-only"></a>Tipi di file supportati solo per la classificazione

Per i tipi di file seguenti è supportata solo la classificazione. Gli altri tipi di file supportano la classificazione quando vengono anche protetti.

- **Adobe Portable Document Format**: .pdf

- **Microsoft Visio**: .vsdx, .vsdm, .vssx, .vssm, .vsd, .vdw, .vst

- **Microsoft Project**: .mpp, .mpt

- **Microsoft Publisher**: .pub

- **Microsoft Office 97, Office 2010, Office 2003**: .xls, .xlt, .doc, .dot, .ppt, .pps, .pot
- **Microsoft XPS**: .xps .oxps

- **Immagini**: .jpg, .jpe, .jpeg, .jif, .jfif, .jfi.png, .tif, .tiff

- **SolidWorks**: .sldprt, .slddrw, .sldasm

- **Autodesk Design Review 2013**: .dwfx

- **Adobe Photoshop**: .psd

- **Digital Negative**: .dng

## <a name="file-types-supported-for-protection"></a>Tipi di file supportati per la protezione

Il client Azure Information Protection supporta la protezione a due livelli diversi, come descritto nella tabella seguente.

|Tipo di protezione|Nativo|Generico|
|----------------------|----------|-----------|
|Descrizione|Per file di testo e immagine, file di Microsoft Office (Word, Excel e PowerPoint), file con estensione pdf e altri tipi di file di applicazione che supportano un servizio Rights Management, la protezione nativa offre un forte livello di protezione che include crittografia e applicazione di diritti (autorizzazioni).|Per tutte le altre applicazioni e tipi di file, la protezione generica fornisce un livello di protezione che include sia l’incapsulamento di file mediante l'autenticazione e il tipo di file .pfile per verificare se un utente è autorizzato per aprire il file.|
|Protezione|I file sono completamente crittografati e la protezione viene applicata nei modi seguenti:<br /><br />- Prima di eseguire il rendering del contenuto protetto, è necessario che venga eseguita l'autenticazione per coloro che ricevono il file tramite posta elettronica o a cui viene concesso l'accesso al file tramite autorizzazioni di file o condivisione.<br /><br />- Inoltre, vengono applicati tutti i diritti di utilizzo e i criteri impostati dal proprietario del contenuto per i file protetti quando viene eseguito il rendering del contenuto nel visualizzatore Azure Information Protection (per i file di testo e immagine protetti) o nell'applicazione associata (per tutti gli altri tipi di file supportati).|La protezione dei file viene applicata nei modi seguenti:<br /><br />- Prima di eseguire il rendering del contenuto protetto, è necessario che venga eseguita l'autenticazione per coloro che sono autorizzati ad aprire il file e a cui viene concesso l'accesso al file. Se l'autorizzazione ha esito negativo, il file non si apre.<br /><br />- Vengono visualizzati i diritti di utilizzo e i criteri impostati dal proprietario del contenuto per comunicare agli utenti autorizzati i criteri di utilizzo previsti.<br /><br />- Si verifica la registrazione di controllo degli utenti autorizzati all'apertura e all'accesso dei file, ma non vengono applicati diritti di utilizzo da applicazioni non compatibili.|
|Impostazione predefinita per i tipi di file|Questo è il livello predefinito di protezione per i tipi di file seguenti:<br /><br />- File di testo e immagine<br /><br />- File di Microsoft Office (Word, Excel, PowerPoint)<br /><br />- Formato di documento portatile (.pdf)<br /><br />Per altre informazioni, vedere la sezione di seguito, [Tipi ed estensioni di file supportati](#supported-file-types-for-protection-and-their-file-name-extensions).|Questa è la protezione predefinita per tutti gli altri tipi di file (ad esempio con estensione vsdx, rtf e così via) non è supportata tramite la protezione completa.|

È possibile modificare il livello di protezione predefinito applicato dal client Azure Information Protection. È possibile modificare il livello predefinito da nativo a generico, da generico a nativo e anche impedire al client Azure Information Protection di applicare la protezione. Per altre informazioni, vedere la sezione [Modifica del livello di protezione predefinito dei file](#changing-the-default-protection-level-of-files) in questo articolo.

La protezione dei dati può essere applicata automaticamente quando un utente seleziona un'etichetta configurata da un amministratore oppure gli utenti possono specificare impostazioni di protezione personalizzate tramite [livelli di autorizzazione](../deploy-use/configure-usage-rights.md#rights-included-in-permissions-levels). 

### <a name="supported-file-types-for-protection-and-their-file-name-extensions"></a>Tipi di file supportati per la protezione e relative estensioni
La tabella seguente contiene i tipi di file supportati in modo nativo dal client Azure Information Protection. Per questi tipi di file, l'estensione del nome file originale viene modificato quando viene applicato il prodotto nativo, e questi file diventano di sola lettura.

Per i file protetti in modo generico, l'estensione del nome file originale viene sempre modificata in .pfile.

> [!WARNING]
> Se si dispone di firewall, proxy web o software di protezione che esaminano e agiscono in base alle estensioni di file, potrebbe essere necessario riconfigurare tali impostazioni per supportare queste nuove estensioni di file.

|Estensione dei file originali|Estensione dei file protetti|
|--------------------------------|-------------------------------------|
|.txt|.ptxt|
|.xml|.pxml|
|.jpg|.pjpg|
|.jpeg|.ppng|
|.pdf|.ppdf|
|.png|.ppng|
|.tif|.ptif|
|.tiff|.ptiff|
|.bmp|.pbmp|
|.gif|.pgif|
|.jpe|.pjpe|
|.jfif|.pjfif|
|.jt|.pjt|


La tabella seguente contiene i tipi di file supportati in modo nativo dal client Azure Information Protection per le app di Microsoft Office. Per questi file, l'estensione del nome di file rimane invariata dopo che il file è stato protetto da un servizio Rights Management.

|Tipi di file supportati da Office|Tipi di file supportati da Office|
|----------------------------------|----------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm|.pptx<br /><br />.thmx<br /><br />.xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />.xps|

### <a name="changing-the-default-protection-level-of-files"></a>Modifica del livello di protezione predefinito dei file
È possibile modificare il modo in cui il client Azure Information Protection protegge i file modificando il Registro di sistema. Ad esempio, è possibile forzare la protezione generica da parte del client Azure Information Protection per i file che supportano la protezione nativa.

Motivi per cui è possibile eseguire questa operazione:

-   Per verificare che tutti gli utenti possano aprire il file se non dispongono di un'applicazione che supporta la protezione nativa.

-   Per ospitare i sistemi di sicurezza che intervengono sui file tramite l'estensione del nome di file e possono essere riconfigurati per adattare l'estensione .pfile ma non possono essere riconfigurati per gestire più estensioni di nome di file per la protezione nativa.

Analogamente, è possibile forzare il client Azure Information Protection ad applicare la protezione nativa ai file ai quali, per impostazione predefinita, viene applicata la protezione generica. Questo potrebbe essere appropriato se si dispone di un'applicazione che supporta APIs RMS, ad esempio, un'applicazione line-of-business scritta per gli sviluppatori interni o un'applicazione acquistata da un fornitore di software indipendenti (ISV).

È anche possibile forzare il client Azure Information Protection a bloccare la protezione dei file, ovvero a non applicare la protezione nativa o quella generica. Ad esempio, questa potrebbe essere necessaria se si dispone di un'applicazione automatica o di un servizio che deve essere in grado di aprire un file specifico per elaborare il relativo contenuto. Quando si blocca la protezione per un tipo di file, gli utenti non possono usare il client Azure Information Protection per proteggere un file del tipo specificato. Quando tentano, viene visualizzato un messaggio in base al quale l'amministratore ha impedito la protezione ed è necessario annullare la loro azione per proteggere il file.

Per configurare il client Azure Information Protection per l'applicazione della protezione generica a tutti i file per impostazione predefinita, apportare le modifiche seguenti al Registro di sistema. Se la chiave FileProtection non esiste, è necessario crearla manualmente.

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection**: creare una nuova chiave denominata *.

    Questa impostazione indica i file con qualsiasi estensione di file.

2.  Nella nuova chiave aggiunta di HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\\\* creare un nuovo valore stringa (REG_SZ) denominato **Encryption**, con valore dati **Pfile**.

    Questa impostazione ha come risultato l'applicazione della protezione generica da parte del client Azure Information Protection.

Queste due impostazioni hanno come risultato l'applicazione della protezione generica da parte del client Azure Information Protection a tutti i file dotati di estensione. Se questo è l'obiettivo, non è richiesta alcuna ulteriore configurazione. Tuttavia, è possibile definire eccezioni per specifici tipi di file, in modo che siano protetti comunque in modo nativo. A tale scopo, è necessario eseguire tre modifiche aggiuntive del Registro di sistema per ogni tipo di file:

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection**: aggiungere una nuova chiave con nome corrispondente all'estensione del file (senza il punto iniziale).

    Ad esempio, i file con estensione del nome di file .docx, creano una chiave denominata **DOCX**.

2.  nella nuova chiave aggiunta per il tipo di file, ad esempio **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX**, creare un nuovo valore DWORD denominato **AllowPFILEEncryption** con valore **0**.

3.  Nella nuova chiave aggiunta per il tipo di file, ad esempio **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RmsSharingApp\FileProtection\DOCX**, creare un nuovo valore stringa denominato **Encryption** con valore **Native**.

Come conseguenza di queste impostazioni, a tutti i file viene applicata la protezione generica, ad eccezione dei file con estensione docx, che vengono protetti in modo nativo dal client Azure Information Protection.

Ripetere questi tre passaggi per altri tipi di file da definire come eccezioni, in quanto supportano la protezione nativa e non si vuole vengano protetti in modo generico dal client Azure Information Protection.

È possibile apportare modifiche di registro di sistema simile per altri scenari modificando il valore della stringa **Crittografia** che supporta i seguenti valori:

-   **Pfile**: Protezione generica

-   **Nativo**: Protezione nativa

-   **Off**: Protezione di blocco

Per altre informazioni, vedere [Configurazione dell'API file](../develop/file-api-configuration.md) nelle linee guida per sviluppatori. Per fare riferimento alla protezione generica, questa documentazione per sviluppatori usa il termine "PFile". 

## <a name="file-types-that-are-excluded-from-classification-and-protection-by-the-azure-information-protection-client"></a>Tipi di file esclusi dalla classificazione e dalla protezione dal client Azure Information Protection

Per impedire agli utenti di modificare file critici per il funzionamento del computer, alcuni tipi di file e cartelle vengono automaticamente esclusi dalla classificazione e dalla protezione. Se gli utenti provano a classificare o proteggere questi file, visualizzano un messaggio indicante che i file sono esclusi.

- **Tipi di file esclusi**: INK, EXE, COM, CMD, BAT, DLL, INI, PST, SCA, DRM, SYS, CPL, INF, DRV, DAT, TMP, MSP, MSI, PDB, JAR

- **Cartelle escluse**: 
    - Windows
    - Programmi (\Programmi e \Programmi (x86))
    - ProgramData 
    - \AppData (per tutti gli utenti)




## <a name="next-steps"></a>Passaggi successivi
Dopo aver identificato i tipi di file supportati dal client Azure Information Protection, vedere gli argomenti seguenti per altre informazioni che potrebbero essere necessarie per supportare il client:

- [File del client e registrazione dell'utilizzo](client-admin-guide-files-and-logging.md)

- [Rilevamento dei documenti](client-admin-guide-document-tracking.md)

- [Comandi di PowerShell](client-admin-guide-powershell.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
