---
title: Log & analizzare l'utilizzo della protezione da Azure Information Protection
description: Informazioni e istruzioni su come usare la registrazione dell'utilizzo per il servizio di protezione da Azure Information Protection.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/03/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a735f3f7-6eb2-4901-9084-8c3cd3a9087e
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: fc3dd9487548849d16f625092c2ff3dd121e4e54
ms.sourcegitcommit: b763a7204421a4c5f946abb7c5cbc06e2883199c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2020
ms.locfileid: "95567645"
---
# <a name="logging-and-analyzing-the-protection-usage-from-azure-information-protection"></a>Registrazione e analisi dell'utilizzo della protezione da Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Usare queste informazioni per comprendere come è possibile usare la registrazione dell'utilizzo per il servizio di protezione (Azure Rights Management) da Azure Information Protection. Questo servizio di protezione fornisce la protezione dei dati per i documenti e i messaggi di posta elettronica dell'organizzazione ed è in grado di registrare tutte le richieste. Sono esempi di richieste le azioni eseguite dagli utenti per proteggere documenti e messaggi di posta elettronica e per usare questi contenuti, le azioni eseguite dagli amministratori del servizio e le azioni eseguite da operatori Microsoft per il supporto delle distribuzioni di Azure Information Protection. 

È quindi possibile utilizzare i log di utilizzo della protezione per supportare gli scenari aziendali seguenti:

-   **Analisi per ottenere informazioni aziendali accurate**

    I log generati dal servizio di protezione possono essere importati in un repository di propria scelta, ad esempio un database, un sistema Online Analytical Processing (OLAP) o un sistema di riduzione delle mappe, per analizzare le informazioni e generare report. È possibile, ad esempio, identificare gli utenti che accedono ai dati protetti e determinare quali dati protetti vengono visualizzati, da quali dispositivi e da quali postazioni. È inoltre possibile stabilire se gli utenti possono leggere correttamente il contenuto protetto. È infine possibile identificare gli utenti che hanno letto un importante documento protetto.

-   **Monitoraggio per evitare eventuali abusi**

    La registrazione delle informazioni sull'utilizzo della protezione è disponibile quasi in tempo reale, in modo da poter monitorare costantemente l'utilizzo del servizio di protezione da parte della società. Il 99,9% dei log sono disponibili per il servizio entro 15 minuti dall'avvio di un'azione.

    È possibile, ad esempio, scegliere di ricevere un avviso nel caso in cui si verifichi un improvviso picco di accessi a dati protetti al di fuori del normale orario di lavoro. Un picco di questo tipo potrebbe indicare che un utente malintenzionato sta raccogliendo informazioni da vendere alla concorrenza. È possibile anche scegliere di ricevere un avviso se uno stesso utente sembra accedere ai dati da due indirizzi IP differenti nell'arco di un breve periodo di tempo. Questo evento può indicare infatti che un account utente è stato compromesso.

-   **Esecuzione di analisi per scopi legali**

    Se si verifica una perdita di informazioni, è probabile che all'amministratore vengano richiesti i nominativi degli utenti che hanno avuto accesso a specifici documenti e l'indicazione delle informazioni visualizzate di recente da una persona sospetta. È possibile rispondere a questi tipi di domande quando si usa questa registrazione perché gli utenti che usano contenuto protetto devono sempre ottenere una licenza di Rights Management per aprire documenti e immagini protette da Azure Information Protection, anche se questi file vengono spostati tramite posta elettronica o copiati in unità USB o altri dispositivi di archiviazione. Ciò significa che è possibile usare questi log come fonte definitiva di informazioni per l'analisi forense quando si proteggono i dati usando Azure Information Protection.

Oltre alla registrazione dell'utilizzo, sono disponibili anche le opzioni di registrazione seguenti:

|Opzione di registrazione|Descrizione|
|----------------|---------------|
|Log amministrazione|Registra le attività amministrative per il servizio di protezione. Ad esempio, se il servizio è disattivato, quando viene abilitata la funzionalità di utente con privilegi avanzati e quando agli utenti vengono delegate autorizzazioni di amministratore per il servizio. <br /><br />Per ulteriori informazioni, vedere il cmdlet di PowerShell [Get-AipServiceAdminLog](/powershell/module/aipservice/get-aipserviceadminlog).|
|Rilevamento dei documenti|Consente agli utenti di monitorare e revocare l'accesso ai documenti monitorati con il client Azure Information Protection. Gli amministratori globali possono inoltre eseguire il rilevamento di questi documenti per conto degli utenti. <br /><br />Per altre informazioni, vedere [Configurazione e uso del rilevamento dei documenti per Azure Information Protection](./rms-client/client-admin-guide-document-tracking.md).|
|Registri eventi del client|Attività di utilizzo per il client Azure Information Protection, registrata nel registro eventi locale di Windows **Applicazioni e servizi**, **Azure Information Protection**. <br /><br />Per altre informazioni, vedere [Registrazione dell'utilizzo per il client Azure Information Protection](./rms-client/client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client).|
|File di log del client|Log per la risoluzione dei problemi per il client Azure Information Protection, disponibili in **%localappdata%\Microsoft\MSIP**. <br /><br />Questi file sono progettati per il supporto tecnico Microsoft.|

Vengono raccolte informazioni anche dai registri d'uso del client e dallo scanner Azure Information Protection, che vengono aggregate per creare report nel portale di Azure. Per altre informazioni, vedere [Reporting per Azure Information Protection](reports-aip.md).

Utilizzare le sezioni seguenti per ulteriori informazioni sulla registrazione dell'utilizzo per il servizio di protezione. 

## <a name="how-to-enable-logging-for-protection-usage"></a>Come abilitare la registrazione per l'utilizzo della protezione
La registrazione dell'utilizzo della protezione è abilitata per impostazione predefinita per tutti i clienti. 

Non sono previsti costi aggiuntivi per l'archiviazione dei log o per il funzionamento della funzionalità di registrazione.

## <a name="how-to-access-and-use-your-protection-usage-logs"></a>Come accedere e usare i log di utilizzo della protezione
Azure Information Protection scrive i log come una serie di BLOB in un account di archiviazione di Azure creato automaticamente per il tenant. Ciascun blob contiene uno o più record di log in formato W3C esteso. I nomi dei blob sono numeri e corrispondono all'ordine di creazione. La sezione [Come interpretare i log dell'utilizzo di Azure Rights Management](#how-to-interpret-your-usage-logs) più avanti in questo argomento contiene altre informazioni sui contenuti dei log e sulla relativa creazione.

Dopo un'azione di protezione, la visualizzazione dei log nell'account di archiviazione può richiedere del tempo. La maggior parte dei log viene visualizzata entro 15 minuti. È consigliabile scaricare i log in uno spazio di archiviazione locale, ad esempio una cartella o un database, oppure in un repository MapReduce.

Per scaricare i log di utilizzo, si userà il modulo AIPService di PowerShell per Azure Information Protection. Per le istruzioni di installazione, vedere [installazione del modulo PowerShell AIPService](install-powershell.md).

### <a name="to-download-your-usage-logs-by-using-powershell"></a>Per scaricare i log dell'utilizzo con PowerShell

1.  Avviare Windows PowerShell con l'opzione **Esegui come amministratore** e usare il cmdlet [Connect-AipService](/powershell/module/aipservice/connect-aipservice) per connettersi a Azure Information Protection:

    ```
    Connect-AipService
    ```
    
2.  Eseguire il comando seguente per scaricare i log per una data specifica: 

    ```
    Get-AipServiceUserLog -Path <location> -fordate <date>
    ```

    Ad esempio, dopo avere creato una cartella denominata Logs sull'unità E:
    
    * Per scaricare i log per una data specifica, ad esempio 01/02/2016, eseguire il comando seguente: `Get-AipServiceUserLog -Path E:\Logs -fordate 2/1/2016`
    
    * Per scaricare i log per un intervallo di date, ad esempio da 01/02/2016 a 14/02/2016, eseguire il comando seguente: `Get-AipServiceUserLog -Path E:\Logs -fromdate 2/1/2016 –todate 2/14/2016` 

Quando si specifica solo il giorno, come negli esempi, si presuppone che l'ora corrisponda alle 00.00.00 nel fuso orario locale e l'orario viene quindi convertito in UTC. Quando si specifica un orario con i parametri -fromdate o -todate, ad esempio -fordate "1/2/2016 15:00:00", la data e l'ora vengono convertite in UTC. Il Get-AipServiceUserLog comando ottiene quindi i registri per il periodo di tempo UTC.

Non è possibile scaricare un intervallo di tempo inferiore a un giorno intero.

Per impostazione predefinita, questo cmdlet usa tre thread per scaricare i log. Se la larghezza di banda è sufficiente e si vuole ridurre il tempo necessario per scaricare i log, usare il parametro -NumberOfThreads, che supporta un valore compreso tra 1 e 32. Ad esempio, se si esegue il comando seguente il cmdlet genera 10 thread per il download dei log: `Get-AipServiceUserLog -Path E:\Logs -fromdate 2/1/2016 –todate 2/14/2016 -numberofthreads 10`


> [!TIP]
> È possibile aggregare tutti i file di log scaricati in un formato CSV mediante [Log Parser di Microsoft](https://www.microsoft.com/download/details.aspx?id=24659), uno strumento che consente di eseguire conversioni tra formati di log noti. È possibile usare questo strumento anche per convertire i dati in formato SYSLOG o per importarli in un database. Dopo aver installato lo strumento, eseguire `LogParser.exe /?` per informazioni e supporto sul relativo uso. 
>
> Ad esempio, se si esegue il comando seguente tutte le informazioni vengono importate in un file in formato .log: `logparser –i:w3c –o:csv "SELECT * INTO AllLogs.csv FROM *.log"`

## <a name="how-to-interpret-your-usage-logs"></a>Come interpretare i log di utilizzo
Usare le informazioni seguenti per interpretare i log di utilizzo della protezione.

### <a name="the-log-sequence"></a>Sequenza dei log
Azure Information Protection scrive i log sotto forma di una serie di BLOB.

Ogni voce del log ha un timestamp UTC. Poiché il servizio di protezione viene eseguito su più server tra più data center, talvolta i log potrebbero sembrare fuori sequenza, anche quando vengono ordinati in base al timestamp. Lo sfasamento è tuttavia minimo, in genere inferiore al minuto, e nella maggior parte dei casi non crea problemi per l'analisi dei log.

### <a name="the-blob-format"></a>Formato dei blob
Ciascun blob è scritto in formato di log W3C esteso ed inizia con le due righe seguenti:

**#Software: RMS**

**#Version: 1,1**

La prima riga indica che si tratta di log di protezione da Azure Information Protection. mentre la seconda indica che il resto del BLOB segue la specifica della versione 1.1. È importante che le applicazioni che analizzano questi log verifichino queste due righe prima di procedere con l'analisi della restante parte del blob.

La terza riga è costituita da un elenco di nomi separati da caratteri di tabulazione:

**#Fields: date            time            row-id        request-type           user-id       result          correlation-id          content-id                owner-email           issuer                     template-id             file-name                  date-published      c-info         c-ip            admin-action            acting-as-user**

Ciascuna delle righe seguenti è un record di log. I valori dei campi seguono lo stesso ordine della riga precedente e sono separati da caratteri di tabulazione. La tabella riportata di seguito consente di interpretare i campi.


|   Nome campo   | Tipo di dati W3C |                                                                                                                                                                          Descrizione                                                                                                                                                                          |                                                            Valore di esempio                                                            |
|----------------|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
|      data      |     Data      |                                                                                                                     La data UTC in cui è stata gestita la richiesta.<br /><br />L'origine è l'orologio locale del server che ha gestito la richiesta.                                                                                                                     |                                                             25-06-2013                                                              |
|      time      |     Ora      |                                                                                                            L'ora in cui è stata gestita la richiesta, in formato UTC 24 ore.<br /><br />L'origine è l'orologio locale del server che ha gestito la richiesta.                                                                                                            |                                                              21.59.28                                                               |
|     row-id     |     Testo      |                                                                           Il GUID univoco del record di log. Se non è presente alcun valore, identificare la voce tramite il valore correlation-id.<br /><br />Questo valore è utile quando i log vengono aggregati o copiati in un altro formato.                                                                           |                                                1c3fe7a9-d9e0-4654-97b7-14fafa72ea63                                                 |
|  request-type  |     Nome      |                                                                                                                                                            Il nome dell'API RMS richiesta.                                                                                                                                                            |                                                           AcquireLicense                                                            |
|    user-id     |    string     |                                                               L'utente che ha effettuato la richiesta.<br /><br />Questo valore è riportato tra virgolette singole. Le chiamate da una chiave del tenant gestita dall'utente (BYOK) hanno un valore **"**, che si applica anche quando i tipi di richiesta sono anonimi.                                                                |                                                          ‘joe@contoso.com’                                                          |
|     result     |    string     |                                                                                                                  La stringa 'Success' indica che la richiesta è stata eseguita con esito positivo.<br /><br />Se la richiesta ha avuto esito negativo, il tipo di errore viene riportato tra virgolette singole.                                                                                                                   |                                                              'Operazione riuscita'                                                              |
| correlation-id |     Testo      |                                                                                                 GUID comune tra il log del client e il log del server RMS per una determinata richiesta.<br /><br />Questo valore può essere utile per la risoluzione dei problemi del client.                                                                                                 |                                                cab52088-8925-4371-be34-4b71a3112356                                                 |
|   content-id   |     Testo      |                                                                      GUID, riportato tra parentesi graffe, che identifica il contenuto protetto, ad esempio un documento.<br /><br />In questo campo è presente un valore solo se la richiesta è di tipo AcquireLicense. Per tutti gli altri tipi di richiesta il campo è vuoto.                                                                       |                                               {bb4af47b-cfed-4719-831d-71b98191a4f2}                                                |
|  owner-email   |    string     |                                                                                                                       Indirizzo di posta elettronica del proprietario del documento.<br /><br /> Questo campo è vuoto se il tipo di richiesta è RevokeAccess.                                                                                                                        |                                                          alice@contoso.com                                                          |
|     autorità di certificazione     |    string     |                                                                                                                          Indirizzo di posta elettronica del soggetto emittente il documento. <br /><br /> Questo campo è vuoto se il tipo di richiesta è RevokeAccess.                                                                                                                          |                       alice@contoso.com (oppure) FederatedEmail.4c1f4d-93bf-00a95fa1e042@contoso.onmicrosoft.com'                       |
|  template-id   |    string     |                                                                                                                    ID del modello usato per proteggere il documento. <br /><br /> Questo campo è vuoto se il tipo di richiesta è RevokeAccess.                                                                                                                     |                                               {6d9371a6-4e2d-4e97-9a38-202233fed26e}                                                |
|   file-name    |    string     | Nome file di un documento protetto che viene monitorato tramite il client Azure Information Protection per Windows. <br /><br />Attualmente, alcuni file, ad esempio i documenti di Office, vengono visualizzati come GUID anziché come nome di file.<br /><br /> Questo campo è vuoto se il tipo di richiesta è RevokeAccess. |                                                       TopSecretDocument.docx                                                        |
| date-published |     Data      |                                                                                                                          Data in cui è stato protetto il documento.<br /><br /> Questo campo è vuoto se il tipo di richiesta è RevokeAccess.                                                                                                                           |                                                         2015-10-15T21:37:00                                                         |
|     c-info     |    string     |                                                                                   Informazioni sulla piattaforma client che effettua la richiesta.<br /><br />La stringa specifica varia a seconda dell'applicazione (ad esempio, il sistema operativo o il browser).                                                                                   | 'MSIPC;version=1.0.623.47;AppName=WINWORD.EXE;AppVersion=15.0.4753.1000;AppArch=x86;OSName=Windows;OSVersion=6.1.7601;OSArch=amd64' |
|      c-ip      |    Indirizzo    |                                                                                                                                                       L'indirizzo IP del client che effettua la richiesta.                                                                                                                                                        |                                                            64.51.202.144                                                            |
|  admin-action  |     Bool      |                                                                                                                                    Indica se un amministratore ha eseguito l'accesso al sito di rilevamento dei documenti in modalità Amministratore.                                                                                                                                    |                                                                True                                                                 |
| acting-as-user |    string     |                                                                                                                               Indirizzo di posta elettronica dell'utente per il quale un amministratore accede al sito di rilevamento dei documenti.                                                                                                                                |                                                          'joe@contoso.com'                                                          |

#### <a name="exceptions-for-the-user-id-field"></a>Eccezioni per il campo user-id
Anche se nel campo user-id è in genere riportato il nome dell'utente che ha effettuato la richiesta, esistono due eccezioni in cui il valore del campo non indica un utente reale:

-   Il valore **'microsoftrmsonline@&lt;YourTenantID&gt;.rms.&lt;region&gt;.aadrm.com'**.

    Indica che un servizio Office 365, ad esempio Exchange Online o Microsoft SharePoint, sta effettuando la richiesta. Nella stringa *&lt; YourTenantID &gt;* è il GUID del tenant e *&lt; Region &gt;* è l'area in cui è registrato il tenant. Ad esempio, **na** indica l'America del Nord, **eu** l'Europa e **ap** l'Asia.

-   Si sta usando il connettore RMS.

    Le richieste provenienti da questo connettore vengono registrate con il nome dell'entità servizio **Aadrm_S-1-7-0**, generato automaticamente quando si installa il connettore RMS.

#### <a name="typical-request-types"></a>Tipi di richiesta tipici
Sono disponibili molti tipi di richiesta per il servizio di protezione, ma nella tabella seguente vengono identificati alcuni dei tipi di richiesta più comunemente utilizzati.

|Tipo di richiesta|Descrizione|
|----------------|---------------|
|AcquireLicense|Un client da un computer basato su Windows richiede una licenza per il contenuto protetto.|
|AcquirePreLicense|Un client, per conto dell'utente, richiede una licenza per il contenuto protetto.|
|AcquireTemplates|È stata eseguita una chiamata per acquisire modelli in base agli ID modello.|
|AcquireTemplateInformation|È stata eseguita una chiamata per ottenere gli ID del modello dal servizio.|
|AddTemplate|Viene eseguita una chiamata dal portale di Azure per aggiungere un modello.|
|AllDocsCsv|Viene eseguita una chiamata dal sito di rilevamento dei documenti per scaricare il file con estensione csv dalla pagina **Tutti i documenti**.|
|BECreateEndUserLicenseV1|Viene eseguita una chiamata da un dispositivo mobile per creare un contratto di licenza con l'utente finale.|
|BEGetAllTemplatesV1|Viene eseguita una chiamata da un dispositivo mobile (back-end) per ottenere tutti i modelli.|
|Certify|Il client sta certificando l'utente per l'utilizzo e la creazione di contenuto protetto.|
|DeleteTemplateById|Viene eseguita una chiamata dal portale di Azure per eliminare un modello in base a un ID modello.|
|DocumentEventsCsv|Viene eseguita una chiamata dal sito di rilevamento dei documenti per scaricare il file con estensione csv per un singolo documento.|
|ExportTemplateById|Viene eseguita una chiamata dal portale di Azure per esportare un modello in base a un ID modello.|
|FECreateEndUserLicenseV1|Richiesta analoga ad AcquireLicense, ma inviata da dispositivi mobili.|
|FECreatePublishingLicenseV1|Questa richiesta corrisponde a una combinazione di Certify e GetClientLicensorCert ed è inviata da client mobili.|
|FEGetAllTemplates|Viene eseguita una chiamata da un dispositivo mobile (front-end) per ottenere i modelli.|
|FindServiceLocationsForUser|Viene eseguita una chiamata per effettuare una query di URL, che consente di chiamare la richiesta Certify o AcquireLicense.|
|GetAllDocs|Viene eseguita una chiamata dal sito di rilevamento dei documenti per caricare la pagina **Tutti i documenti** relativa a un utente o cercare tutti i documenti del tenant. Usare questo valore con i campi admin-action e acting-as-admin:<br /><br />- admin-action è vuoto: un utente visualizza la pagina **Tutti i documenti** relativa ai propri documenti.<br /><br />- admin-action è true e acting-as-user è vuoto: un amministratore visualizza tutti i documenti relativi al proprio tenant.<br /><br />- admin-action è true e acting-as-user non è vuoto: un amministratore visualizza la pagina **Tutti i documenti** relativa a un utente.|
|GetAllTemplates|Viene eseguita una chiamata dal portale di Azure per aggiungere tutti i modelli.|
|GetClientLicensorCert|Il client richiede un certificato di distribuzione, da usare in un secondo tempo per proteggere i contenuti, da un computer basato su Windows.|
|GetConfiguration|Un cmdlet di PowerShell Azure viene chiamato per ottenere la configurazione del tenant di Azure RMS.|
|GetConnectorAuthorizations|Viene eseguita una chiamata dai connettori RMS per ottenere la rispettiva configurazione dal cloud.|
|GetRecipients|Viene eseguita una chiamata dal sito di rilevamento dei documenti per passare alla visualizzazione elenco di un singolo documento.|
|GetSingle|Viene eseguita una chiamata dal sito di rilevamento dei documenti per passare alla pagina **Documento singolo**.|
|GetTenantFunctionalState|Il portale di Azure controlla se il servizio di protezione (Rights Management di Azure) è attivato.|
|GetTemplateById|Viene eseguita una chiamata dal portale di Azure per ottenere un modello specificando un ID modello.|
|KeyVaultDecryptRequest|Il client tenta di decrittografare il contenuto protetto con RMS. Applicabile solo per una chiave del tenant gestita dal cliente (BYOK) in Insieme di credenziali delle chiavi di Azure.|
|KeyVaultGetKeyInfoRequest|Viene eseguita una chiamata per verificare che la chiave specificata da usare in Insieme di credenziali delle chiavi di Azure per la chiave del tenant di Azure Information Protection sia accessibile e non sia già stata usata.|
|KeyVaultSignDigest|Viene eseguita una chiamata quando una chiave gestita dal cliente (BYOK) in Insieme di credenziali delle chiavi di Azure viene usata a scopo di firma. In genere, viene eseguita una chiamata per ogni richiesta AcquireLicence (o FECreateEndUserLicenseV1), Certify e GetClientLicensorCert (o FECreatePublishingLicenseV1).|
|KMSPDecrypt|Il client tenta di decrittografare il contenuto protetto con RMS. Applicabile solo per una chiave del tenant legacy gestita dal cliente (BYOK).|
|KMSPSignDigest|Viene eseguita una chiamata quando una chiave legacy gestita dal cliente (BYOK) viene usata a scopo di firma. In genere, viene eseguita una chiamata per ogni richiesta AcquireLicence (o FECreateEndUserLicenseV1), Certify e GetClientLicensorCert (o FECreatePublishingLicenseV1).|
|LoadEventsForMap|Viene eseguita una chiamata dal sito di rilevamento dei documenti per passare alla visualizzazione mappa di un singolo documento.|
|LoadEventsForSummary|Viene eseguita una chiamata dal sito di rilevamento dei documenti per passare alla visualizzazione sequenza temporale di un singolo documento.|
|LoadEventsForTimeline|Viene eseguita una chiamata dal sito di rilevamento dei documenti per passare alla visualizzazione mappa di un singolo documento.|
|ImportTemplate|Viene eseguita una chiamata dal portale di Azure per importare un modello.|
|RevokeAccess|Viene eseguita una chiamata dal sito di rilevamento dei documenti per revocare un documento.|
|SearchUsers |Viene eseguita una chiamata dal sito di rilevamento dei documenti per cercare tutti gli utenti in un tenant.|
|ServerCertify|Viene eseguita una chiamata da un client abilitato per RMS, come SharePoint, per certificare il server.|
|SetUsageLogFeatureState|Viene eseguita una chiamata per abilitare la funzionalità di registrazione dell'utilizzo.|
|SetUsageLogStorageAccount|Viene eseguita una chiamata per specificare il percorso dei log del servizio Azure Rights Management.|
|UpdateNotificationSettings|Viene eseguita una chiamata dal sito di rilevamento dei documenti per modificare le impostazioni di notifica di un singolo documento.|
|UpdateTemplate|Viene eseguita una chiamata dal portale di Azure per aggiornare un modello esistente.|


## <a name="powershell-reference"></a>Informazioni di riferimento su PowerShell

L'unico cmdlet di PowerShell necessario per accedere alla registrazione dell'utilizzo della protezione è [Get-AipServiceUserLog](/powershell/module/aipservice/get-aipserviceuserlog). 

Per altre informazioni sull'uso di PowerShell per Azure Information Protection, vedere [amministrazione della protezione da Azure Information Protection tramite PowerShell](administer-powershell.md).
