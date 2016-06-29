---
# required metadata

title: Panoramica tecnica per l'applicazione Rights Management sharing | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/20/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f7b13fa4-4f8e-489a-ba46-713d7a79f901

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Panoramica tecnica per l'applicazione di condivisione Microsoft Rights Management

*Si applica a: Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 con SP1, Windows 8, Windows 8.1*


L'applicazione di condivisione Microsoft Rights Management è un'applicazione facoltativa scaricabile per Microsoft Windows e altre piattaforme e che fornisce le operazioni seguenti:

-   Protezione di un singolo un singolo file o più file in blocco oppure di tutti i file contenuti in una cartella selezionata.

-   Supporto completo per la protezione di qualsiasi tipo di file e un visualizzatore integrato per i tipi di file di testo e immagine d’uso comune.

-   Protezione generica per i file che non supportano la protezione RMS.

-   Completa interoperabilità con i file protetti tramite Office Information Rights Management (IRM).

-   Completa interoperabilità con i file PDF protetti con Infrastruttura di classificazione file (FCI, File Classification Infrastructure) e gli strumenti di creazione di PDF supportati.

L’applicazione di condivisione Rights Management di Microsoft utilizza il nuovo [runtime Client AD RMS 2.1](http://www.microsoft.com/download/details.aspx?id=38396). Utilizzando la funzionalità di AD RMS 2.1, l'applicazione di condivisione Rights Management di Microsoft consente agli utenti finali un'esperienza semplice di protezione e di utilizzo.

Con la versione di ottobre 2013 di RMS, è possibile proteggere i documenti utilizzando Office 2010 in modo nativo e inviarli a persone in un'altra società, che possono quindi utilizzarli tramite Azure RMS. Inoltre, con questa versione, se si utilizza AD RMS in modalità crittografia 2, è possibile usare RMS per utenti singoli e utilizzare il contenuto delle persone in un'altra società che utilizza Azure RMS. Per ulteriori informazioni sulla modalità di crittografia 2, vedere [Modalità di crittografia di AD RMS](http://technet.microsoft.com/library/hh867439%28v=ws.10%29.aspx).

Per informazioni sulla distribuzione, vedere [Distribuzione automatica dell'applicazione Microsoft Rights Management sharing](sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application)

## Livelli di protezione – nativo e generico
Applicazione di condivisione Rights Management di Microsoft supporta la protezione a due livelli diversi, come descritto nella tabella seguente.

|Tipo di protezione|Nativo|Generico|
|----------------------|----------|-----------|
|Descrizione|Per file di testo, di immagine, di Microsoft Office (file di Word, Excel e PowerPoint), file .pdf e altri tipi di file di applicazione, che supportano AD RMS, la protezione nativa fornisce un forte livello di protezione che include crittografia e applicazione di diritti (autorizzazioni).|Per tutte le altre applicazioni e tipi di file, la protezione generica fornisce un livello di protezione che include sia l’incapsulamento di file mediante l'autenticazione e il tipo di file .pfile per verificare se un utente è autorizzato per aprire il file.|
|Protezione|I file sono completamente crittografati e la protezione viene applicata nei modi seguenti:<br /><br />- Prima di eseguire il rendering del contenuto protetto, è necessario che venga eseguita l'autenticazione per coloro che ricevono il file tramite posta elettronica o a cui viene concesso l'accesso al file tramite autorizzazioni di file o condivisione.<br /><br />- Inoltre, vengono applicati tutti i diritti di utilizzo e i criteri impostati dal proprietario del contenuto per i file protetti quando viene eseguito il rendering del contenuto nel Visualizzatore IP (per i file protetti di testo e immagine) o nell'applicazione associata (per tutti gli altri tipi di file supportati).|La protezione dei file viene applicata nei modi seguenti:<br /><br />- Prima di eseguire il rendering del contenuto protetto, è necessario che venga eseguita l'autenticazione per coloro che sono autorizzati ad aprire il file e a cui viene concesso l'accesso al file. Se l'autorizzazione ha esito negativo, il file non si apre.<br /><br />- Vengono visualizzati i diritti di utilizzo e i criteri impostati dal proprietario del contenuto per comunicare agli utenti autorizzati i criteri di utilizzo previsti.<br /><br />- Si verifica la registrazione di controllo degli utenti autorizzati all'apertura e all'accesso dei file, ma non vengono applicati diritti di utilizzo da applicazioni non compatibili.|
|Impostazione predefinita per i tipi di file|Questo è il livello predefinito di protezione per i tipi di file seguenti:<br /><br />- File di testo e immagine<br /><br />- File di Microsoft Office (Word, Excel, PowerPoint)<br /><br />- Formato di documento portatile (.pdf)<br /><br />Per altre informazioni, vedere la sezione di seguito, [Tipi di file supportati e le estensioni di nome di file](#supported-file-types-and-file-name-extensions).|Questa è la protezione predefinita per tutti gli altri tipi di file (ad esempio con estensione vsdx, rtf e così via) non è supportata tramite la protezione completa.|
È possibile modificare il livello di protezione predefinito che applica l'applicazione di condivisione RMS. È possibile modificare il livello predefinito da nativo a generico, da generico a nativo, e anche impedire l'applicazione di condivisione RMS dalla protezione di applicazione. Per altre informazioni, vedere la sezione [Modifica del livello di protezione predefinito dei file](#changing-the-default-protection-level-of-files) in questo articolo.

## Tipi di file supportati e le estensioni di nome di file
Nella tabella seguente sono elencati i tipi di file supportati in modo nativo dall’applicazione di condivisione Rights Management di Microsoft. Per questi tipi di file, l'estensione del nome file originale viene modificato quando viene applicato il prodotto nativo, e questi file diventano di sola lettura.

Inoltre, quando l'applicazione di condivisione RMS protegge in modo nativo un file di Word, Excel o PowerPoint che gli utenti proteggono tramite la condivisione, questa azione crea automaticamente un secondo file che è una copia dell'originale con lo stesso nome ma con un’estensione del nome file **.ppdf** ¹. Questa versione del file garantisce che i destinatari che installano l'applicazione di condivisione RMS possano sempre aprire il file in cui è applicata la protezione nativa.

Per i file protetti in modo generico, l'estensione del nome file originale viene sempre modificata in .pfile.

> [!WARNING] Se sono presenti firewall, proxy Web o software di protezione che esaminano e agiscono in base alle estensioni di file, potrebbe essere necessario eseguire una riconfigurazione per supportare queste nuove estensioni di file.

|Estensione del nome di file originale|Estensione del nome di file protetti tramite RMS|
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
|.giff|.pgiff|
|.jpe|.pjpe|
|.jfif|.pjfif|
|.jt|.pjt|
Rendering PDF con tecnologia Foxit ¹. Copyright © 2003-2014, Foxit Corporation.

Nella tabella seguente sono elencati i tipi di file che l'applicazione di condivisione Microsoft Rights Management supporta in modo nativo in Microsoft Office 2016, Office 2013 e Office 2010. Per questi file, l'estensione del nome di file rimane invariato dopo che il file viene protetto da RMS.

|Tipi di file supportati da Office|Tipi di file supportati da Office|
|----------------------------------|----------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm|.pptx<br /><br />.thmx<br /><br />.xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />.xps|

### Modifica del livello di protezione predefinito dei file
È possibile modificare come l’applicazione di condivisione RMS protegge i file modificando il Registro di sistema. Ad esempio, è possibile forzare i file che supportano la protezione nativa ad essere protetti in modo generico dall'applicazione di condivisione RMS.

Motivi per cui è possibile eseguire questa operazione:

-   Per garantire che tutti gli utenti possano aprire il file dai dispositivi mobili.

-   Per verificare che tutti gli utenti possano aprire il file se non dispongono di un'applicazione che supporta la protezione nativa.

-   Per ospitare i sistemi di sicurezza che intervengono sui file tramite l'estensione del nome di file e possono essere riconfigurati per adattare l'estensione .pfile ma non possono essere riconfigurati per gestire più estensioni di nome di file per la protezione nativa.

Analogamente, è possibile forzare l'applicazione di condivisione RMS ad applicare la protezione nativa ai file che per impostazione predefinita, avrebbero la protezione generica applicata . Questo potrebbe essere appropriato se si dispone di un'applicazione che supporta APIs RMS, ad esempio, un'applicazione line-of-business scritta per gli sviluppatori interni o un'applicazione acquistata da un fornitore di software indipendenti (ISV).

È inoltre possibile forzare l'applicazione di condivisione RMS per la protezione dei file di blocco (non si applica protezione nativa o protezione generica). Ad esempio, questa potrebbe essere necessaria se si dispone di un'applicazione automatica o di un servizio che deve essere in grado di aprire un file specifico per elaborare il relativo contenuto. Quando si blocca la protezione per un tipo di file, gli utenti non possono utilizzare l'applicazione di condivisione RMS per proteggere un file con il tipo di file. Quando tentano, viene visualizzato un messaggio in base al quale l'amministratore ha impedito la protezione ed è necessario annullare la loro azione per proteggere il file.

Per configurare l'applicazione di condivisione RMS per applicare la protezione generica a tutti i file che, per impostazione predefinita, avrebbe una protezione nativa applicata , apportare le seguenti modifiche al Registro di sistema:

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection**: creare una nuova chiave denominata *.

    Questa impostazione indica i file con qualsiasi estensione di file.

2.  Nella nuova chiave aggiunta di HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection\\\*, creare un nuovo valore stringa (REG_SZ) denominato **Crittografia** con valore di dati **Pfile**.

    Questa impostazione determina l’applicazione di condivisione RMS applicando la protezione generica.

Queste due impostazioni determinano l'applicazione di condivisione RMS applicando la protezione generica a tutti i file con estensione del nome di file. Se questo è l'obiettivo, non è richiesta alcuna ulteriore configurazione. Tuttavia, è possibile definire eccezioni per specifici tipi di file, in modo che siano protetti comunque in modo nativo. A tale scopo, è necessario eseguire tre modifiche aggiuntive del Registro di sistema per ogni tipo di file:

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection**: aggiungere una nuova chiave con il nome dell'estensione di nome file (senza il punto iniziale).

    Ad esempio, i file con estensione del nome di file .docx, creano una chiave denominata **DOCX**.

2.  Nella chiave del tipo di file appena aggiunto (ad esempio, **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection\DOCX**), creare un nuovo valore DWORD denominato **AllowPFILEEncryption** con un valore di **0**.

3.  Nella chiave del tipo di file appena aggiunto (ad esempio, **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection\DOCX**), creare un nuovo valore stringa denominato **crittografia** con un valore **nativo**.

In seguito a queste impostazioni, tutti i file sono protetti in modo generico ad eccezione dei file che dispongono di un'estensione di file con estensione .docx, che sono protetti in modo nativo per l'applicazione di condivisione RMS.

Ripetere questi tre passaggi per altri tipi di file che si desidera definire come eccezioni, in quanto supportano protezione nativa e non si desidera che possano essere genericamente protetti mediante l'applicazione di condivisione RMS.

È possibile apportare modifiche di registro di sistema simile per altri scenari modificando il valore della stringa **Crittografia** che supporta i seguenti valori:

-   **Pfile**: Protezione generica

-   **Nativo**: Protezione nativa

-   **Off**: Protezione di blocco

## Vedere anche
[Guida dell'utente dell'applicazione di condivisione Rights Management](sharing-app-user-guide.md)



<!--HONumber=May16_HO3-->


