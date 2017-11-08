---
title: Note sulla versione
description: Aggiornamenti all'SDK per revisione e altre informazioni per sviluppatori.
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 10/18/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: CE379738-4E1D-42AD-83F4-F89B70456EBB
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.openlocfilehash: 52733dd7cac356879408e774c79331d705a71ea0
ms.sourcegitcommit: 02e48f0e5137ba777ec9a2bccde08130e6075c20
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2017
---
# <a name="release-notes"></a>Note sulla versione

Questo articolo contiene informazioni importanti su questa versione e le versioni precedenti di RMS SDK 2.1.

## <a name="october-2017---update"></a>Aggiornamento di ottobre 2017

- Aggiunta di due nuove API per l'inizializzazione e l'annullamento dell'inizializzazione dell'ambiente. Per informazioni, vedere [IpcInitializeEnvironment](https://msdn.microsoft.com/library/hh535289.aspx) e [IpcUninitializeEnvironment](https://msdn.microsoft.com/library/hh535289.aspx).
- Ora sono supportati i tipi di file di Visio. Per altre informazioni, vedere [Configurazione dell'API file](file-api-configuration.md).

## <a name="february-2016---sdk-documentation-update"></a>Aggiornamento di febbraio 2016 della documentazione dell'SDK

>[!Note]
> Gli aggiornamenti della documentazione delle funzionalità in questa sezione si applicano al download dell'SDK con data 11/12/2015.

- **Flusso di autenticazione migliorato** usando l'autenticazione OAuth2 basata su token tramite [Azure Active Directory Authentication Library (ADAL)](https://azure.microsoft.com/en-us/documentation/articles/active-directory-authentication-libraries/). Per altre informazioni su questo processo e sulle relative estensioni API, vedere [ADAL authentication for your RMS enabled application](how-to-use-adal-authentication.md) (Autenticazione ADAL per l'applicazione abilitata per RMS).

- **Aggiornamento ad ADAL**: eseguendo l'aggiornamento dell'applicazione per l'uso dell'autenticazione ADAL anziché l'Assistente per l'accesso a Microsoft Online, l'utente e i clienti potranno:

 - Usare Multi-Factor Authentication
 - Installare il client RMS 2.1 senza necessità di privilegi amministrativi sul computer
 - Certificare l'applicazione per Windows 10

- **Il supporto dell'Assistente per l'accesso a Microsoft Online con RMS SDK verrà rimosso.** L'Assistente per l'accesso continuerà a essere supportato per sei mesi, dopodiché il supporto verrà sospeso.


## <a name="december-2015-update"></a>Aggiornamento di dicembre 2015

- In diverse aree sono stati implementati miglioramenti delle prestazioni, tra cui:
    - Quando si usano server con sola licenza pubblicare dal server primario di gestione delle licenze.
    - SDK 2.1 RMS riscontra errori più velocemente in assenza di connessione di rete.

- Numerosi aggiornamenti per migliorare i messaggi di errore e l'esperienza di risoluzione dei problemi.
- Si noti inoltre che è stato aggiornato anche l'elenco delle [le piattaforme supportate](supported-platforms.md).
- La necessità dell'ambiente di pre-produzione e dell'uso del manifesto dell'applicazione è stata rimossa a partire da RMS SDK 2.1. Queste sezioni del set di documentazione per gli sviluppatori sono state rimosse e l'intera documentazione è stata semplificata e riorganizzata.

## <a name="may-2015-update"></a>Aggiornamento di maggio 2015

-   **App di servizio e RMS basato su cloud** - [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx) richiede tre tipi di informazioni: chiave simmetrica, **AppPrincipalId** e **TenantBposId**. L'articolo è stato aggiornato per offrire linee guida sull'elaborazione di queste informazioni. Per questo aggiornamento, vedere la versione aggiornata di [Consentire all'applicazione di servizio di usare RMS basato su cloud](how-to-use-file-api-with-aadrm-cloud.md).

## <a name="april-2015-update"></a>Aggiornamento di aprile 2015

-   **Il controllo dei documenti** è attualmente possibile grazie a una serie di nuove API. Per altre informazioni, vedere [Controllo del contenuto](tracking-content.md).
-   **Tipo di crittografia** -È ora supportato il controllo a livello di API per la selezione del pacchetto di crittografia. Per altre informazioni, vedere [Uso della crittografia](working-with-encryption.md).

    **Nota**: nell'API non è più esposto il flag **IPC\_LI\_DEPRECATED\_ENCRYPTION\_ALGORITHMS**. Ciò significa che le app future non saranno più compilate se fanno riferimento a questo flag, tuttavia le app già create continueranno a funzionare poiché si rispetta il flag privatamente nel codice API. È possibile comunque ottenere il vantaggio del flag di algoritmi di crittografia precedenti deprecati, semplicemente modificando un flag. Per altre informazioni, vedere [Uso della crittografia](working-with-encryption.md).

-   **Le applicazioni in modalità server**, che usano [valori modalità API](https://msdn.microsoft.com/library/hh535236.aspx) di **IPC\_API\_MODE\_SERVER**, non richiedono un manifesto dell'applicazione. È possibile testare l'applicazione rispetto a un server RMS di produzione e non sono necessarie per ottenere una licenza di produzione quando si passa all'ambiente di produzione. Per altre informazioni sulle applicazioni in modalità server, vedere [Tipi di applicazioni](application-types.md).
-   **La Registrazione** ora viene implementata tramite i metodi per file e di Event Tracing for Windows.
-   Se si usa una **macchina Windows 7 SP1 o Windows Server 2008 R2**, vedere la nota che segue in "Note importanti per gli sviluppatori".

## <a name="january-2015-update"></a>Aggiornamento di gennaio 2015

-   **Aumento delle dimensioni del file protetto (pfile) supportato** - Supporta ora pfile di dimensioni maggiori di 1 gigabyte (1 GB). Per altre informazioni su pfile, vedere [Supported File Formats](supported-file-formats.md) (Formati file supportati).
-   **Miglioramento della registrazione per una migliore diagnostica** - Sui livelli di registrazione sarà visualizzato **ERRORE** o **AVVISO** per i messaggi da rivedere. Tutti gli altri messaggi incluse le eccezioni ancora visualizzate saranno registrati come **INFO**.

    È stato scelto questo approccio per evitare perdite di dettagli. A questo punto, solo i messaggi importanti sono visualizzati con livello AVVISO.

-   **Acquisizione dei modelli aziendali** - sostanziali correzioni al codice di acquisizione del modello, in base ai commenti e suggerimenti e ai report del cliente.
-   Maggiore coerenza nella localizzazione

## <a name="october-2014-update"></a>Aggiornamento di ottobre 2014

-   Aggiornamento dei comportamenti predefiniti del componente API file di SDK. Per altre informazioni, vedere [Configurazione dell'API file](file-api-configuration.md).
-   La nuova funzionalità Notifica tramite posta elettronica è descritta nell'articolo [Abilitazione della notifica tramite email](how-to-enable-email-notification.md) delle note per gli sviluppatori.

## <a name="july-2014-update"></a>Aggiornamento di luglio 2014

Il componente API File dell'SDK è stato integrato e ora offre le funzionalità seguenti:

-   Identifica il programma di protezione da usare.
-   Fornisce la protezione RMS a livello di granularità di un file.

    Funzioni aggiunte in questa versione:

    **Nota**: sono stati aggiunti altri tipi di dati di supporto e strutture, non elencati in questo articolo, per le estensioni dell'API file. Tutti gli articoli aggiornati per questa versione sono contrassegnati come **preliminari e soggetti a modifiche**.

    -   [IpcfOpenFileOnHandle](https://msdn.microsoft.com/library/dn771751.aspx)
    -   [IpcfOpenFileOnILockBytes](https://msdn.microsoft.com/library/dn771752.aspx)
    -   [IpcfGetFileProperty](https://msdn.microsoft.com/library/dn771749.aspx)
    -   [IpcfLogicalFileRangeToRawFileRange](https://msdn.microsoft.com/library/dn771750.aspx)
    -   [IpcfReadFile](https://msdn.microsoft.com/library/dn771753.aspx)
    -   [IpcfSetEndOfFile](https://msdn.microsoft.com/library/dn771754.aspx)
    -   [IpcfWriteFile](https://msdn.microsoft.com/library/dn771756.aspx)

## <a name="april-2014-update"></a>Aggiornamento di aprile 2014

-   **Uso della memoria API file**, ha subito notevoli miglioramenti, soprattutto per PFile di grandi dimensioni.
-   **L'ID contenuto** è ora accessibile in scrittura tramite la proprietà **IPC\_LI\_CONTENT\_ID**. Per altre informazioni, vedere [License property types](https://msdn.microsoft.com/library/hh535287.aspx) (Tipi di proprietà di licenza).
-   **Requisito del manifesto di produzione**: quando applicazioni o servizi con abilitazione RMS sono in esecuzione in modalità server, il manifesto non sarà più richiesto. Per altre informazioni, vedere [Tipi di applicazioni](application-types.md).
-   **Aggiornamenti della documentazione**

    **Procedura consigliata di test**: aggiunta di linee guida per l'uso del server locale prima dei test con Azure RMS. Per altre informazioni, vedere [Consentire all'applicazione di servizio di usare RMS basato su cloud](how-to-use-file-api-with-aadrm-cloud.md).

## <a name="important-developer-notes"></a>Note importanti per gli sviluppatori

-   **Supporto nativo per tutti i tipi di file**

    È possibile aggiungere il supporto nativo per qualsiasi tipo di file (estensione) con questa versione di SDK 2.1 Rights Management Services. Ad esempio, per tutte le estensioni &lt;ext&gt; (non Office e pdf), verrà usata l'estensione \*p&lt;ext&gt; se la configurazione dell'amministratore per l'estensione è "NATIVA".

    Per altre informazioni sui tipi di file supportati, vedere [Configurazione API file](file-api-configuration.md).

-   **Macchine con Windows 7 SP1 e Windows Server 2008 R2 SP1** senza l'aggiornamento, [KB2533623](https://support.microsoft.com/en-us/kb/2533623), potrebbero manifestare il seguente errore di protezione di qualsiasi file di Office "Parametro non corretto. Codice di errore 0x80070057". In tal caso, installare l'aggiornamento e riprovare. Se il problema persiste, contattare l'alias RMS SDK Beta Feedback <rmcstbeta@microsoft.com>.

    **Nota**: a partire dalla versione di aprile 2015, è stato aggiunto un controllo al processo di installazione per questo KB.

     

-   **Integrazione di API file**

    L'API file Active Directory Rights Management Services, con l'aggiunta dell'API File, offre i seguenti vantaggi e funzionalità.

      - È possibile proteggere i dati riservati in modo automatico senza dover conoscere i dettagli dell'implementazione Information Rights Management (IRM) usata da diversi formati di file.

      - È possibile proteggere file di Microsoft Office, file PDF (Portable Document Format) e selezionati di altro tipo tramite la protezione nativa dei file. Per un elenco completo dei tipi di file che possono essere protetti tramite la protezione nativa, vedere [Configurazione API File](file-api-configuration.md).

      - È possibile proteggere tutti i file, ad eccezione di file di sistema e file di Office usando il formato di File protetto RMS (PFile).

    L'API file viene implementata tramite le quattro nuove funzioni seguenti: [IpcfDecryptFile](https://msdn.microsoft.com/library/dn133058.aspx), [IpcfEncryptFile](https://msdn.microsoft.com/library/dn133059.aspx), [IpcfGetSerializedLicenseFromFile](https://msdn.microsoft.com/library/dn133060.aspx) e [IpcfIsFileEncrypted](https://msdn.microsoft.com/library/dn133061.aspx).

    L'API file richiede che Rights Management Service Client 2.1 sia installato nel computer client e che il computer disponga di connettività a un server RMS. Per altre informazioni sul server RMS, il client RMS e le relative funzionalità, vedere il contenuto TechNet relativo alla [documentazione di RMS per i professionisti IT](https://technet.microsoft.com/en-us/library/cc771234(v=ws.10).aspx).

-   **Problema**: durante la creazione di una licenza da zero, i diritti di proprietà devono essere concessi esplicitamente.

    **Soluzione**: l'applicazione deve aggiungere in modo esplicito i diritti di **proprietario** al proprietario della licenza durante la creazione di una licenza da zero tramite [IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx). Per altre informazioni, vedere [Aggiungere diritti espliciti di proprietario](add-explicit-owner-rights.md).

-   **Problema**: se un'applicazione chiama [IpcProtectWindow](https://msdn.microsoft.com/library/hh535268.aspx) o [IpcUnprotectWindow](https://msdn.microsoft.com/library/hh535272.aspx) due volte per la stessa finestra usando il relativo handle, SDK 2.1 RMS restituirà un errore in **HRESULT**.

    **Soluzione**: per linee guida specifiche su questo problema, vedere la sezione Osservazioni di [IpcProtectWindow](https://msdn.microsoft.com/library/hh535268.aspx) e [IpcUnprotectWindow](https://msdn.microsoft.com/library/hh535272.aspx).

-   **Problema**: quando si compila per diverse architetture, è necessario usare queste linee guida.

    **Soluzione**: se si vuole usare Ipcsecproc\*isv.dll per un'architettura diversa, ad esempio è stato installato l'SDK a 64 bit su un computer a 64 bit ma si vuole distribuire in un computer a 32 bit che richiede Ipcsecproc\*isv.dll, è necessario installare l'SDK a 32 bit su un altro computer e copiare i file Ipcsecproc\*isv.dll dalla cartella "%PROGRAMFILES%\\Microsoft Information Protection And Control" (percorso predefinito o punto in cui si è scelto di installare l'SDK).

## <a name="frequently-asked-questions"></a>Domande frequenti

**D**: Come funziona il comportamento della lingua predefinita con le funzioni che accettano un parametro LCID?

**R**: usare 0 per le impostazioni locali predefinite. In questo caso, il client 2.1 SDK cerca i nomi e le descrizioni nella sequenza riportata di seguito, recuperando il primo disponibile:

    1 - User preferred LCID.
    2 - System locale LCID.
    3 - The first available language specified in the Rights Management Server (RMS) template.

Se non è possibile recuperare alcun nome e descrizione, viene restituito un errore. Può esistere un solo nome e una descrizione per un LCID specifico.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]