---
title: Note sulla versione
description: Vedere le note sulla versione per Microsoft Rights Management Service SDK v 2.1 ottobre 2019 e gli aggiornamenti precedenti.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 10/18/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: CE379738-4E1D-42AD-83F4-F89B70456EBB
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.custom: dev, has-adal-ref
ms.openlocfilehash: f8b0aa99b4a18f1e2b9d0c9b3ddedf2d745b3e19
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "95568281"
---
# <a name="release-notes"></a>Note sulla versione

Questo articolo contiene informazioni importanti su questa versione e quelle precedenti di RMS SDK 2.1.

## <a name="october-2019---update"></a>2019 ottobre-aggiornamento

- In alcuni casi, l'uso dell'autenticazione con chiave simmetrica non riesce ad autenticare l'utente con Azure RMS che impedisce la protezione e la rimozione della protezione del contenuto.
- Il client RMS potrebbe arrestarsi in modo anomalo durante il tentativo di verificare se alcuni documenti PDF precedentemente protetti e non protetti sono attualmente protetti.
- L'uso del reindirizzamento DNS per i server AD RMS che sono stati configurati in porte speciali non funzionerà correttamente.

## <a name="september-2019---update"></a>2019 settembre-aggiornamento

- Correzione di un deadlock che può verificarsi quando si tenta di chiamare i metodi di inizializzazione contemporaneamente ad altri metodi client RMS.
- È stato risolto un problema per determinare se i file di Office protetti con password sono protetti da RMS.
-   Aggiornare la convalida delle licenze per licenze per scopi specifici.
- Aggiornamenti alla protezione PDF.
- Altre correzioni di bug.
- Aggiornare per collegare staticamente alle librerie di runtime C.

## <a name="april-2019---update"></a>Aprile 2019-aggiornamento
- Correzioni di bug nell'API file.
- API file aggiornata per verificare il diritto di esportazione anziché il diritto di estrazione durante la decrittografia del contenuto.
- Correzione del programma di installazione per assicurarsi che durante l'aggiornamento venga installata la nuova protezione PDF V2.
- I dati di telemetria cambiano. Questa modifica richiede un aggiornamento del pacchetto di installazione che consente di installare le librerie di runtime C.
- Modifiche all'autenticazione del back-end del servizio. eseguire l' **aggiornamento a questa versione dell'SDK per minmize l'interferenza se si usa l'autenticazione con chiave simmetrica per le applicazioni**
- Supporto per VC 15,9


## <a name="october-2017---update"></a>Aggiornamento di ottobre 2017

- Aggiunta di due nuove API per l'inizializzazione e l'annullamento dell'inizializzazione dell'ambiente. Per informazioni, vedere [IpcInitializeEnvironment](/previous-versions/windows/desktop/msipc/microsoft-information-protection-and-control-client-functions) e [IpcUninitializeEnvironment](/previous-versions/windows/desktop/msipc/microsoft-information-protection-and-control-client-functions).
- Ora sono supportati i tipi di file di Visio. Per altre informazioni, vedere [configurazione dell'API file](file-api-configuration.md).

## <a name="february-2016---sdk-documentation-update"></a>Aggiornamento di febbraio 2016 della documentazione dell'SDK

>[!Note]
> Gli aggiornamenti della documentazione delle funzionalità in questa sezione si applicano al download dell'SDK con data 11/12/2015.

- **Flusso di autenticazione migliorato** usando l'autenticazione OAuth2 basata su token tramite [Azure Active Directory Authentication Library (ADAL)](/azure/active-directory/azuread-dev/active-directory-authentication-libraries). Per altre informazioni su questo processo e sulle estensioni API, vedere [autenticazione adal per l'applicazione abilitata per RMS](how-to-use-adal-authentication.md).

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

-   **App di servizio e RMS**  -  basato su cloud [IPC \_ La \_ \_ chiave simmetrica delle credenziali](/previous-versions/windows/desktop/msipc/ipc-credential-symmetric-key) richiede tre tipi di informazioni: chiave simmetrica, **AppPrincipalId** e **TenantBposId**. L'articolo è stato aggiornato per offrire linee guida sull'elaborazione di queste informazioni. Per questo aggiornamento, vedere la versione aggiornata di [Consentire all'applicazione di servizio di usare RMS basato su cloud](how-to-use-file-api-with-aadrm-cloud.md).

## <a name="april-2015-update"></a>Aggiornamento di aprile 2015

-   **Il controllo dei documenti** è attualmente possibile grazie a una serie di nuove API. Per ulteriori informazioni, vedere [rilevamento del contenuto](tracking-content.md).
-   **Tipo di crittografia** -È ora supportato il controllo a livello di API per la selezione del pacchetto di crittografia. Per ulteriori informazioni, vedere [utilizzo della crittografia](working-with-encryption.md).

    **Nota**    Non verrà più esposto il flag **IPC \_ li \_ deprecated \_ Encryption \_ algoritmi** nell'API. Ciò significa che le app future non saranno più compilate se fanno riferimento a questo flag, tuttavia le app già create continueranno a funzionare poiché si rispetta il flag privatamente nel codice API. È possibile comunque ottenere il vantaggio del flag di algoritmi di crittografia precedenti deprecati, semplicemente modificando un flag. Per ulteriori informazioni, vedere [utilizzo della crittografia](working-with-encryption.md).

-   **Le applicazioni in modalità server**, che usano [valori modalità API](/previous-versions/windows/desktop/msipc/api-mode-values) di **IPC\_API\_MODE\_SERVER**, non richiedono un manifesto dell'applicazione. È possibile testare l'applicazione rispetto a un server RMS di produzione e non sono necessarie per ottenere una licenza di produzione quando si passa all'ambiente di produzione. Per ulteriori informazioni sulle applicazioni in modalità server, vedere [tipi](application-types.md)di applicazioni.
-   **La Registrazione** ora viene implementata tramite i metodi per file e di Event Tracing for Windows.
-   Se si usa una **macchina Windows 7 SP1 o Windows Server 2008 R2**, vedere la nota che segue in "Note importanti per gli sviluppatori".

## <a name="january-2015-update"></a>Aggiornamento di gennaio 2015

-   **Aumento delle dimensioni del file protetto (pfile) supportato** - Supporta ora pfile di dimensioni maggiori di 1 gigabyte (1 GB). Per altre informazioni su pfile, vedere [Supported File Formats](supported-file-formats.md) (Formati file supportati).
-   **Miglioramento della registrazione per una migliore diagnostica** - Sui livelli di registrazione sarà visualizzato **ERRORE** o **AVVISO** per i messaggi da rivedere. Tutti gli altri messaggi incluse le eccezioni ancora visualizzate saranno registrati come **INFO**.

    È stato scelto questo approccio per evitare perdite di dettagli. A questo punto, solo i messaggi importanti sono visualizzati con livello AVVISO.

-   **Acquisizione dei modelli aziendali** - sostanziali correzioni al codice di acquisizione del modello, in base ai commenti e suggerimenti e ai report del cliente.
-   Maggiore coerenza nella localizzazione

## <a name="october-2014-update"></a>Aggiornamento di ottobre 2014

-   Aggiornamento dei comportamenti predefiniti del componente API file di SDK. Per altre informazioni, vedere [configurazione dell'API file](file-api-configuration.md).
-   La nuova funzionalità Notifica tramite posta elettronica è descritta nell'articolo [Abilitazione della notifica tramite email](how-to-enable-email-notification.md) delle note per gli sviluppatori.

## <a name="july-2014-update"></a>Aggiornamento di luglio 2014

Il componente API File dell'SDK è stato integrato e ora offre le funzionalità seguenti:

-   Identifica il programma di protezione da usare.
-   Fornisce la protezione RMS a livello di granularità di un file.

    Funzioni aggiunte in questa versione:

    **Nota**   -Sono stati aggiunti altri tipi di dati e strutture di supporto, non elencati qui, per le estensioni dell'API file. Tutti gli articoli aggiornati per questa versione sono contrassegnati come **preliminari e soggetti a modifiche**.

    -   [IpcfOpenFileOnHandle](/previous-versions/windows/desktop/msipc/ipcfopenfileonhandle)
    -   [IpcfOpenFileOnILockBytes](/previous-versions/windows/desktop/msipc/ipcfopenfileonilockbytes)
    -   [IpcfGetFileProperty](/previous-versions/windows/desktop/msipc/ipcfgetfileproperty)
    -   [IpcfLogicalFileRangeToRawFileRange](/previous-versions/windows/desktop/msipc/ipcflogicalfilerangetorawfilerange)
    -   [IpcfReadFile](/previous-versions/windows/desktop/msipc/ipcfreadfile)
    -   [IpcfSetEndOfFile](/previous-versions/windows/desktop/msipc/ipcfsetendoffile)
    -   [IpcfWriteFile](/previous-versions/windows/desktop/msipc/ipcfwritefile)

## <a name="april-2014-update"></a>Aggiornamento di aprile 2014

-   **Uso della memoria API file**, ha subito notevoli miglioramenti, soprattutto per PFile di grandi dimensioni.
-   L' **ID contenuto** è ora accessibile in scrittura tramite la proprietà **IPC \_ li \_ Content \_ ID**. Per altre informazioni, vedere [tipi di proprietà di licenza](/previous-versions/windows/desktop/msipc/license-property-types).
-   **Requisito del manifesto di produzione**: quando applicazioni o servizi con abilitazione RMS sono in esecuzione in modalità server, il manifesto non sarà più richiesto. Per ulteriori informazioni, vedere [tipi di applicazioni](application-types.md).
-   **Aggiornamenti alla documentazione**

    **Procedura consigliata di test**: aggiunta di linee guida per l'uso del server locale prima dei test con Azure RMS. Per altre informazioni, vedere [consentire all'applicazione di servizio di usare RMS basato su cloud](how-to-use-file-api-with-aadrm-cloud.md).

## <a name="important-developer-notes"></a>Note importanti per gli sviluppatori

-   **Supporto nativo per tutti i tipi di file**

    Con questa versione di Rights Management Services SDK 2.1. è possibile aggiungere il supporto nativo per qualsiasi tipo di file (estensione). Ad esempio, per tutte le estensioni &lt;ext&gt; (non Office e pdf), verrà usata l'estensione \*p&lt;ext&gt; se la configurazione dell'amministratore per l'estensione è "NATIVA".

    Per altre informazioni sui tipi di file supportati, vedere [Configurazione API file](file-api-configuration.md).

-   I **computer con Windows 7 SP1 e Windows Server 2008 R2 SP1** senza l'aggiornamento [KB2533623](https://support.microsoft.com/kb/2533623) potrebbero visualizzare l'errore seguente durante la protezione dei file di Office "Parametro non corretto. Codice di errore 0x80070057". In tal caso, installare l'aggiornamento e riprovare. Se il problema persiste, contattare l'alias RMS SDK Beta Feedback <rmcstbeta@microsoft.com>.

    **Nota**    A partire dalla versione di aprile 2015, al processo di installazione per questa KB è stato aggiunto un controllo.



-   **Integrazione di API file**

    L'API file Active Directory Rights Management Services, con l'aggiunta dell'API File, offre le funzionalità e i vantaggi riportati di seguito.

      - È possibile proteggere i dati riservati in modo automatico senza dover conoscere i dettagli dell'implementazione Information Rights Management (IRM) usata da diversi formati di file.

      - È possibile proteggere file di Microsoft Office, file PDF (Portable Document Format) e selezionati di altro tipo tramite la protezione nativa dei file. Per un elenco completo dei tipi di file che possono essere protetti con la protezione nativa, vedere [configurazione dell'API file](file-api-configuration.md).

      - È possibile proteggere tutti i file, ad eccezione di file di sistema e file di Office usando il formato di File protetto RMS (PFile).

    L'API file viene implementata tramite le quattro nuove funzioni seguenti: [IpcfDecryptFile](/previous-versions/windows/desktop/msipc/ipcfdecryptfile), [IpcfEncryptFile](/previous-versions/windows/desktop/msipc/ipcfencryptfile), [IpcfGetSerializedLicenseFromFile](/previous-versions/windows/desktop/msipc/ipcfgetserializedlicensefromfile) e [IpcfIsFileEncrypted](/previous-versions/windows/desktop/msipc/ipcfisfileencrypted).

    L'API file richiede che Rights Management Service Client 2.1 sia installato nel computer client e che il computer disponga di connettività a un server RMS. Per altre informazioni sul server RMS, il client RMS e le relative funzionalità, vedere il contenuto TechNet relativo alla [documentazione di RMS per i professionisti IT](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771234(v=ws.10)).

-   **Problema**: durante la creazione di una licenza da zero, i diritti di proprietà devono essere concessi esplicitamente.

    **Soluzione**: l'applicazione deve aggiungere esplicitamente i diritti di **proprietario** al proprietario della licenza durante la creazione di una licenza da zero, usando [IpcCreateLicenseFromScratch](/previous-versions/windows/desktop/msipc/ipccreatelicensefromscratch). Per ulteriori informazioni, vedere [aggiungere diritti proprietario espliciti](add-explicit-owner-rights.md).

-   **Problema**: se un'applicazione chiama [IpcProtectWindow](/previous-versions/windows/desktop/msipc/ipcprotectwindow) o [IpcUnprotectWindow](/previous-versions/windows/desktop/msipc/ipcunprotectwindow) due volte per la stessa finestra usando il relativo handle, RMS SDK 2,1 restituirà un errore in **HRESULT**.

    **Soluzione**: per linee guida specifiche, vedere la sezione Osservazioni in [IpcProtectWindow](/previous-versions/windows/desktop/msipc/ipcprotectwindow) e [IpcUnprotectWindow](/previous-versions/windows/desktop/msipc/ipcunprotectwindow).

-   **Problema**: quando si compila per diverse architetture, è necessario usare queste linee guida.

    **Soluzione**: se si vuole usare ilisv.dll Ipcsecproc \* per un'architettura diversa, ad esempio è stato installato l'SDK a 64 bit in un computer a 64 bit, ma ora si vuole eseguire la distribuzione in un computer a 32 bit che richiede Ipcsecproc \*isv.dll), è necessario installare l'SDK a 32 bit in un computer diverso e copiare i \* file diisv.dll IPCSECPROC nella cartella "% ProgramFiles% \\ Microsoft Information Protection and Control" (il percorso predefinito o quando si sceglie di installare l'SDK).

## <a name="frequently-asked-questions"></a>Domande frequenti

**D**: Come funziona il comportamento della lingua predefinita con le funzioni che accettano un parametro LCID?

**R**: usare 0 per le impostazioni locali predefinite. In questo caso, AD RMS Client 2.1 cerca i nomi e le descrizioni nella sequenza riportata di seguito, recuperando il primo disponibile:

1. LCID preferito dall'utente.
2. LCID delle impostazioni locali del sistema.
3. La prima lingua disponibile specificata nel modello di Rights Management Server (RMS).

Se non è possibile recuperare alcun nome e descrizione, viene restituito un errore. Può esistere un solo nome e una descrizione per un LCID specifico.