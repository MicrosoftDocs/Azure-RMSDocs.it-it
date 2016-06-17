---
# required metadata

title: Note sulla versione | Azure RMS
description:
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 05/03/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: CE379738-4E1D-42AD-83F4-F89B70456EBB
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Note sulla versione

Questo argomento contiene informazioni importanti su questa versione e le precedenti dell'SDK 2.1 RMS.

## Novità dell'aggiornamento di febbraio 2016 della documentazione dell'SDK

>[!Note]  Gli aggiornamenti della documentazione delle funzionalità in questa sezione si applicano al download dell'SDK con data 11/12/2015.

- **Flusso di autenticazione migliorato**: usando l'autenticazione OAuth2 basata su token tramite [Azure Active Directory Authentication Library (ADAL)](https://azure.microsoft.com/en-us/documentation/articles/active-directory-authentication-libraries/). Per altre informazioni su questo processo e sulle relative estensioni API, vedere [ADAL authentication for your RMS enabled application](how-to-use-adal-authentication.md) (Autenticazione ADAL per l'applicazione abilitata per RMS).

- **Aggiornamento ad ADAL**: eseguendo l'aggiornamento dell'applicazione per l'uso dell'autenticazione ADAL anziché l'Assistente per l'accesso a Microsoft Online, l'utente e i clienti potranno:

 - Usare Multi-Factor Authentication
 - Installare il client RMS 2.1 senza necessità di privilegi amministrativi sul computer
 - Certificare l'applicazione per Windows 10

- **Il supporto dell'Assistente per l'accesso a Microsoft Online con RMS SDK verrà rimosso.** L'uso dell'Assistente per l'accesso continuerà a essere supportato per 6 mesi, trascorsi i quali verrà sospeso.


## Aggiornamento di dicembre 2015

- In diverse aree sono stati implementati miglioramenti delle prestazioni, tra cui:
    - Quando si usano server con sola licenza pubblicare dal server primario di gestione delle licenze.
    - SDK 2.1 RMS riscontra errori più velocemente in assenza di connessione di rete.

- Numerosi aggiornamenti per migliorare i messaggi di errore e l'esperienza di risoluzione dei problemi.
- Si noti inoltre che è stato aggiornato anche l'elenco delle [le piattaforme supportate](supported-platforms.md).
- La necessità dell'ambiente di pre-produzione e dell'utilizzo di manifesti dell'applicazione è stato rimosso a partire da RMS SDK 2.1. Queste sezioni del set di documentazione per gli sviluppatori sono state rimosse e l'intera documentazione è stata semplificata e riorganizzata.

## Aggiornamento di maggio 2015

-   **Applicazioni di servizio e RMS basato su cloud** - [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key) richiede tre tipi di informazioni: chiave simmetrica, **AppPrincipalId** e **TenantBposId**. L'argomento è stato aggiornato per fornire informazioni aggiuntive sull'elaborazione di queste informazioni di acquisizione. Per questo aggiornamento, vedere la versione aggiornata di [Consentire all'applicazione di servizio di usare RMS basato su cloud](how-to-use-file-api-with-aadrm-cloud.md).

## Aggiornamento di aprile 2015

-   **Il controllo dei documenti** è attualmente possibile grazie a una serie di nuove API. Per altre informazioni, vedere [Controllo del contenuto](tracking-content.md).
-   **Tipo di crittografia** -È ora supportato il controllo a livello di API per la selezione del pacchetto di crittografia. Per altre informazioni, vedere [Uso della crittografia](working-with-encryption.md).

    **Nota**: nell'API non è più esposto il flag **IPC\_LI\_DEPRECATED\_ENCRYPTION\_ALGORITHMS**. Ciò significa che le app future non saranno più compilate se fanno riferimento a questo flag, tuttavia le app già create continueranno a funzionare poiché si rispetta il flag privatamente nel codice API. È possibile comunque ottenere il vantaggio del flag di algoritmi di crittografia precedenti deprecati, semplicemente modificando un flag. Per altre informazioni, vedere [Uso della crittografia](working-with-encryption.md).

-   **Le applicazioni in modalità server**, che usano un [**valore modalità API**](/rights-management/sdk/2.1/api/win/api%20mode%20values#msipc_api_mode_values_IPC_API_MODE_SERVER) di **IPC\_API\_MODE\_SERVER**, non richiedono un manifesto dell'applicazione. È possibile testare l'applicazione rispetto a un server RMS di produzione e non sono necessarie per ottenere una licenza di produzione quando si passa all'ambiente di produzione. Per altre informazioni sulle applicazioni in modalità server, vedere [Tipi di applicazioni](application-types.md).
-   **La Registrazione** ora viene implementata tramite i metodi per file e di Event Tracing for Windows.
-   Se si usa una **macchina Windows 7 SP1 o Windows Server 2008 R2**, vedere la nota che segue in "Note importanti per gli sviluppatori".

## Aggiornamento di gennaio 2015

-   **Aumento delle dimensioni del file protetto (pfile) supportato** - Supporta ora pfile di dimensioni maggiori di 1 gigabyte (1 GB). Per altre informazioni su pfile, vedere [Supported File Formats](supported-file-formats.md) (Formati file supportati).
-   **Miglioramento della registrazione per una migliore diagnostica** - Sui livelli di registrazione sarà visualizzato **ERRORE** o **AVVISO** per i messaggi da rivedere. Tutti gli altri messaggi, incluse le eccezioni ancora visualizzate, saranno registrati come **INFO**.

    È stato scelto questo approccio per evitare perdite di dettagli. A questo punto, solo i messaggi importanti sono visualizzati con livello AVVISO.

-   **Acquisizione dei modelli aziendali** - sostanziali correzioni al codice di acquisizione del modello, in base ai commenti e suggerimenti e ai report del cliente.
-   Maggiore coerenza nella localizzazione

## Aggiornamento di ottobre 2014

-   Aggiornamento dei comportamenti predefiniti del componente API file di SDK. Per altre informazioni, vedere [Configurazione dell'API file](file-api-configuration.md).
-   La Notifica tramite posta elettronica, una nuova funzionalità, è descritta nella sezione Note per gli sviluppatori, [Abilitazione della notifica tramite email](how-to-enable-email-notification.md).

## Aggiornamento di luglio 2014

Estensione del componente API File di SDK e offre le funzionalità seguenti:

-   Identifica il programma di protezione da usare.
-   Fornisce la protezione RMS a livello di granularità di un file.

    Funzioni aggiunte in questa versione:

    **Nota**: sono stati aggiunti altre tipi di dati di supporto e le strutture, non è elencate qui, per le estensioni dell'API file. Tutti gli argomenti aggiornati per questa versione sono contrassegnati come **preliminari e soggetti a modifiche**.

    -   [**IpcfOpenFileOnHandle**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfopenfileonhandle)
    -   [**IpcfOpenFileOnILockBytes**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfopenfileonilockbytes)
    -   [**IpcfGetFileProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfgetfileproperty)
    -   [**IpcfLogicalFileRangeToRawFileRange**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcflogicalfilerangetorawfilerange)
    -   [**IpcfReadFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfreadfile)
    -   [**IpcfSetEndOfFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfsetendoffile)
    -   [**IpcfWriteFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfwritefile)

## Aggiornamento di aprile 2014

-   **Uso della memoria API file**, ha subito notevoli miglioramenti, soprattutto per PFile di grandi dimensioni.
-   **L'ID contenuto** è ora accessibile in scrittura tramite la proprietà **IPC\_LI\_CONTENT\_ID**. Per altre informazioni, vedere [**Tipi di proprietà di licenza**](/rights-management/sdk/2.1/api/win/License%20property%20types#msipc_license_property_types_IPC_LI_APP_SPECIFIC_DATA).
-   **Requisito del manifesto di produzione**: quando applicazioni o servizi con abilitazione RMS sono in esecuzione in modalità server, il manifesto non sarà più richiesto. Per altre informazioni, vedere [Tipi di applicazioni](application-types.md).
-   **Aggiornamenti della documentazione**

    **Procedura consigliata di test **: aggiunta di linee guida per l'uso del server locale prima dei test con Azure RMS. Per altre informazioni, vedere [Consentire all'applicazione di servizio di usare RMS basato su cloud](how-to-use-file-api-with-aadrm-cloud.md).

## Note importanti per gli sviluppatori

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

    L'API file viene implementata tramite le quattro nuove funzioni seguenti: [IpcfDecryptFile](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfdecryptfile), [IpcfEncryptFile](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile), [IpcfGetSerializedLicenseFromFile](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfgetserializedlicensefromfile) e [IpcfIsFileEncrypted](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfisfileencrypted).

    L'API file richiede che Rights Management Service Client 2.1 sia installato nel computer client e che il computer disponga di connettività a un server RMS. Per altre informazioni sul server RMS, il client RMS e le relative funzionalità, vedere il contenuto TechNet relativo alla [documentazione di RMS per i professionisti IT](https://technet.microsoft.com/en-us/library/cc771234(v=ws.10).aspx).

-   **Problema**: durante la creazione di una licenza da zero, i diritti di proprietà devono essere concessi esplicitamente.

    **Soluzione**: l'applicazione deve aggiungere esplicitamente i diritti di **proprietario** al proprietario della licenza durante la creazione di una licenza da zero, usando [**IpcCreateLicenseFromScratch**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch). Per altre informazioni, vedere [Aggiungere diritti espliciti di proprietario](add-explicit-owner-rights.md).

-   **Problema**: se un'applicazione chiama [**IpcProtectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcprotectwindow) o [**IpcUnprotectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcunprotectwindow) due volte per la stessa finestra usando il relativo handle, SDK 2.1 RMS restituirà un errore di **HRESULT**.

    **Soluzione**: per linee guida specifiche su questo, vedere la sezione Osservazioni in [**IpcProtectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcprotectwindow) e [**IpcUnprotectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcunprotectwindow).

-   **Problema**: quando si compila per diverse architetture, è necessario usare queste linee guida.

    **Soluzione**: se si vuole usare Ipcsecproc\*isv.dll per un'architettura diversa, ad esempio è stato installato l'SDK a 64 bit su un computer a 64 bit ma si vuole distribuire in un computer a 32 bit che richiede Ipcsecproc\*isv.dll, è necessario installare l'SDK a 32 bit su un altro computer e copiare i file Ipcsecproc\*isv.dll dalla cartella "%PROGRAMFILES%\\Microsoft Information Protection And Control" (percorso predefinito o punto in cui si è scelto di installare l'SDK).

## Domande frequenti

**D**: Come funziona il comportamento della lingua predefinita con le funzioni che accettano un parametro LCID?

**R**: usare 0 per le impostazioni locali predefinite. In questo caso, il client 2.1 SDK cerca i nomi e le descrizioni nella sequenza riportata di seguito, recuperando il primo disponibile:

    1 - User preferred LCID.
    2 - System locale LCID.
    3 - The first available language specified in the Rights Management Server (RMS) template.

Se non è possibile recuperare alcun nome e descrizione, viene restituito un errore. Può esistere un solo nome e una descrizione per un LCID specifico.

## Argomenti correlati

* [Panoramica](ad-rms-overview.md)
* [Aggiungere diritti espliciti di proprietario](add-explicit-owner-rights.md)
* [Configurazione dell'API file](file-api-configuration.md)
* [**IpcfGetSerializedLicenseFromFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfgetserializedlicensefromfile)
* [**IpcfEncryptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile)
* [**IpcfDecryptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfdecryptfile)
* [**IpcfIsFileEncrypted**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfisfileencrypted)
* [**IpcCreateLicenseFromScratch**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch)
* [**IpcProtectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcprotectwindow)
* [**IpcUnprotectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcunprotectwindow)
 

 


<!--HONumber=Jun16_HO2-->


