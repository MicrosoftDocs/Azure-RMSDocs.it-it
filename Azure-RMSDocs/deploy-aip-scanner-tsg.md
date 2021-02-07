---
title: Risolvere i problemi della distribuzione dello scanner locale
description: Istruzioni per la risoluzione dei problemi relativi alla distribuzione dello scanner locale con etichetta unificata
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 02/01/2021
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 84b2434004149c03888d15fdec34d2910b45ae9d
ms.sourcegitcommit: 7aa72a673a97d84a7aac36d912b118d68b4a5228
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/07/2021
ms.locfileid: "99804420"
---
# <a name="troubleshooting-your-unified-labeling-on-premises-scanner-deployment"></a>Risoluzione dei problemi di distribuzione dello scanner locale con etichetta unificata

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 *
>
>***Pertinente per**: [AIP Unified Labeling client only](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). *

Usare il contenuto di questo articolo per risolvere i problemi relativi alla distribuzione dello scanner locale.

## <a name="troubleshooting-using-the-scanner-diagnostic-tool"></a>Risoluzione dei problemi con lo strumento di diagnostica dello scanner

Se si verificano problemi con Azure Information scanner, verificare se la distribuzione è integra usando il comando di PowerShell [Start-AIPScannerDiagnostics](/powershell/module/azureinformationprotection/start-aipscannerdiagnostics) :

```powershell
Start-AIPScannerDiagnostics
```

Lo strumento di diagnostica controlla i dettagli seguenti e quindi Esporta un file di log con i risultati:

- Indica se il database è aggiornato
- Indica se gli URL di rete sono accessibili
- Indica se è presente un token di autenticazione valido e se è possibile acquisire i criteri
- Indica se il profilo è definito nel portale di Azure
- Se la configurazione offline/online esiste e può essere acquisita
- Indica se le regole configurate sono valide

> [!TIP]
> Se si esegue il comando con un utente che non è l'utente dello scanner, assicurarsi di aggiungere il parametro **-onconto** . 
>

> [!NOTE]
> Il comando **Start-AIPScannerDiagnostics** non esegue un controllo dei prerequisiti completo. Se si verificano problemi con lo scanner, verificare anche che il sistema sia conforme ai [requisiti dello scanner](deploy-aip-scanner-prereqs.md)e che la [configurazione e l'installazione dello scanner](deploy-aip-scanner-configure-install.md) siano completate.
>

## <a name="troubleshooting-a-scan-that-timed-out"></a>Risoluzione dei problemi relativi a un'analisi scaduta

Se lo scanner si arresta in modo imprevisto e non completa l'analisi di un numero elevato di file in un repository, potrebbe essere necessario modificare una delle impostazioni seguenti:

- **Numero di porte dinamiche**. Potrebbe essere necessario aumentare il numero di porte dinamiche per il sistema operativo che ospita i file. Uno dei motivi per cui lo scanner supera il numero di connessioni di rete consentite e pertanto si arresta può essere la protezione avanzata dei server per SharePoint.

    Per altre informazioni su come visualizzare l'intervallo di porte corrente e aumentarlo, vedere [Impostazioni che possono essere modificate per migliorare le prestazioni di rete](/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance).

- **Soglia visualizzazione elenco**. Per le farm di SharePoint di grandi dimensioni, potrebbe essere necessario aumentare la soglia di visualizzazione elenco. Per impostazione predefinita, la soglia di visualizzazione elenco è impostata su **5.000**.

    Per ulteriori informazioni, vedere [gestire elenchi e librerie di grandi dimensioni in SharePoint](https://support.office.com/article/manage-large-lists-and-libraries-in-sharepoint-b8588dae-9387-48c2-9248-c24122f07c59#__bkmkchangelimit&ID0EAABAAA=Server).


## <a name="scanner-error-reference"></a>Riferimento errore scanner

Usare le sezioni seguenti per comprendere i messaggi di errore specifici generati dallo scanner e la risoluzione dei problemi o le azioni di soluzione per risolvere il problema:

|Tipo di errore |Risoluzione dei problemi  |
|---------|---------|
|**Errori di autenticazione**     |  - [Il token di autenticazione non è accettato](#authentication-token-not-accepted) <br>  - [Token di autenticazione mancante](#authentication-token-missing)|
|**Errori dei criteri**     |  - [Criteri mancanti](#policy-missing) <br>- [Il criterio non include alcuna condizione di etichetta automatica](#policy-doesnt-include-any-automatic-labeling-condition)      |
|**Errori di database/schema**     |  - [Errori di database](#database-errors) <br> - [Schema non corrispondente o obsoleto](#mismatched-or-outdated-schema)  |
|**Altri errori**     |  - [Connessione sottostante chiusa](#underlying-connection-was-closed) <br> - [Processi di scanner bloccati](#stuck-scanner-processes) <br>- [Impossibile connettersi al server remoto](#unable-to-connect-to-remote-server) <br>- [Si è verificato un errore durante l'invio della richiesta](#error-occurred-while-sending-the-request) <br>- [Profilo o processo di analisi del contenuto mancante](#missing-content-scan-job-or-profile) <br>- [Nessun repository configurato](#no-repositories-configured) <br>- [Non sono stati trovati cluster](#no-cluster-found)   |
|     |         |


<!--Authentication errors-->

### <a name="authentication-token-not-accepted"></a>Il token di autenticazione non è accettato

**Messaggio di errore**

`Microsoft.InformationProtection.Exceptions.AccessDeniedException: The service didn't accept the auth token.`

**Soluzione**

Se il comando [set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) ha esito negativo, assicurarsi di definire correttamente le autorizzazioni nel portale di Azure.

Per altre informazioni, vedere [creare e configurare applicazioni Azure ad per set-AIPAuthentication](rms-client/clientv2-admin-guide-powershell.md#create-and-configure-azure-ad-applications-for-set-aipauthentication).

### <a name="authentication-token-missing"></a>Token di autenticazione mancante

**Messaggio di errore**

I tipi validi sono:

- `NoAuthTokenException: Client application failed to provide authentication token for HTTP request`

- `Microsoft.InformationProtection.Exceptions.NoAuthTokenException: Client application failed to provide authentication token for HTTP request. Failed with: System.AggregateException: One or more errors occurred. ---> Microsoft.IdentityModel.Clients.ActiveDirectory.AdalException: user_interaction_required: One of two conditions was encountered: 1. The PromptBehavior.Never flag was passed, but the constraint could not be honored, because user interaction was required. 2. An error occurred during a silent web authentication that prevented the http authentication flow from completing in a short enough time frame`

- `Failed to acquire a token using windows integrated authentication (No SSO)`

- Dalla portale di Azure, nella pagina **nodi** : `Policy does not include any automatic labeling condition`

**Soluzione**

Per eseguire lo scanner in modo non interattivo, è necessario eseguire l'autenticazione con un token. 

Quando si esegue il comando [set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) , assicurarsi di usare il parametro token per conto dell'utente dello scanner.

Ad esempio:

```powershell
$pscreds = Get-Credential CONTOSO\scanner
Set-AIPAuthentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -DelegatedUser scanner@contoso.com -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -OnBehalfOf $pscreds
Acquired application access token on behalf of CONTOSO\scanner.
```

Per altre informazioni, vedere [ottenere un token di Azure ad per lo scanner](deploy-aip-scanner-configure-install.md#get-an-azure-ad-token-for-the-scanner).

<!--Policy errors-->

### <a name="policy-missing"></a>Criteri mancanti

**Messaggio di errore**

`Policy is missing`

**Descrizione**

Lo scanner non è in grado di trovare il file dei criteri Microsoft Information Protection (MIP).

**Soluzione**

Per verificare che il file dei criteri esista come previsto, archiviare il percorso seguente: **% LocalAppData% \Microsoft\MSIP\mip\MSIP.Scanner.exe \mip\mip.Policies.sqlite3**

Per ulteriori informazioni sulle etichette MIP e sui criteri di etichetta, vedere [creare e configurare etichette di riservatezza e i relativi criteri](/microsoft-365/compliance/create-sensitivity-labels) nella documentazione di Microsoft 365.

### <a name="policy-doesnt-include-any-automatic-labeling-condition"></a>Il criterio non include alcuna condizione di etichetta automatica

**Error (Errore) (Error (Errore)e)**

Gli errori indicano che nei criteri di etichetta mancano le condizioni di etichettatura automatiche

**Soluzione**

Verificare i seguenti problemi:

|Soluzione  |Dettagli  |
|---------|---------|
|**Controllare le impostazioni del processo di analisi del contenuto**     | Nel portale di Azure eseguire questa procedura: <br> <br>- [Imposta i **tipi di informazioni da** rilevare a **tutti**](deploy-aip-scanner-configure-install.md#identify-all-custom-conditions-and-known-sensitive-information-types)  <br>- [Definire un'etichetta predefinita da applicare durante l'analisi](deploy-aip-scanner-configure-install.md#apply-a-default-label-to-all-files-in-a-data-repository)      |
|**Controllare le impostazioni dei criteri di etichettatura**     |  Nell'interfaccia di amministrazione di assegnazione di etichette, ad esempio il Microsoft 365 Security & Compliance Center, seguire questa procedura: <br> <br>- [Definire un'etichetta di riservatezza predefinita](/microsoft-365/compliance/create-sensitivity-labels#publish-sensitivity-labels-by-creating-a-label-policy)  <br> - [Definire le regole di etichettatura automatiche e consigliate](/microsoft-365/compliance/apply-sensitivity-label-automatically)       |
|**Verificare che i criteri siano accessibili**     | Se le impostazioni sono definite come previsto, il file dei criteri può essere mancante o inaccessibile, ad esempio quando si verifica un timeout dal centro di conformità Microsoft 365 sicurezza &. <br>  <br>Per verificare il file dei criteri, verificare che sia presente il file seguente: **% LocalAppData% \Microsoft\MSIP\mip\MSIP.Scanner.exe \mip\mip.Policies.sqlite3**        |
| | |

Per ulteriori informazioni, vedere [che cos'è il Azure Information Protection scanner Unified Labeling?](deploy-aip-scanner.md) e informazioni [sulle etichette di riservatezza](/microsoft-365/compliance/sensitivity-labels).

<!--DB / Schema errors-->

### <a name="database-errors"></a>Errori del database

**Messaggio di errore**

`DB error`

**Descrizione**

Lo scanner potrebbe non essere in grado di connettersi al database.

**Soluzione**

Verificare la connettività di rete tra il computer dello scanner e il database. 

Verificare inoltre che l'account del servizio utilizzato per eseguire i processi dello scanner disponga di tutte le autorizzazioni necessarie per accedere al database.

### <a name="mismatched-or-outdated-schema"></a>Schema non corrispondente o obsoleto

**Messaggio di errore**

I tipi validi sono:

- `SchemaMismatchException`

- Nella portale di Azure nella pagina **nodi** : `DB schema is not up to date. Run Update-AIPScanner command to update the DB schema` o `Error: DB schema is not up to date`

**Soluzione**

Eseguire il comando [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner) per risincronizzare lo schema e assicurarsi che sia aggiornato con tutte le modifiche recenti.


<!--Other errors-->

### <a name="underlying-connection-was-closed"></a>Connessione sottostante chiusa

**Messaggio di errore**

`System.Net.WebException: The underlying connection was closed: An unexpected error occurred on a send. ---> System.IO.IOException: Authentication failed because the remote party has closed the transport stream.`

**Soluzione**

Questo errore indica in genere che TLS 1,2 non è abilitato.

Per altre informazioni, vedere:

- [Requisiti dell'infrastruttura di rete e dei firewall](requirements.md#firewalls-and-network-infrastructure)
- [Come abilitare TLS 1.2](/mem/configmgr/core/plan-design/security/enable-tls-1-2-client) 
- [Abilitare il supporto TLS 1,1 e TLS 1,2 in Office Online Server](/officeonlineserver/enable-tls-1-1-and-tls-1-2-support-in-office-online-server)

### <a name="stuck-scanner-processes"></a>Processi di scanner bloccati

**Messaggio di errore**

Lo scanner sta elaborando un singolo file più a lungo del previsto. Il processo potrebbe essere bloccato.

**Soluzione**

Controllare il report dettagliato per verificare se il file è ancora in aumento o meno. 

Se il file continua ad aumentare, significa che lo scanner sta ancora elaborando i dati ed è necessario attendere il completamento dell'operazione.

Tuttavia, se il file non è più in aumento, procedere come segue:

1. Eseguire una o entrambe le operazioni seguenti:

    - Eseguire il cmdlet [Start-AIPScannerDiagnostics](/powershell/module/azureinformationprotection/start-aipscannerdiagnostics) per eseguire i controlli di diagnostica sullo scanner e i file di log di esportazione e zip per individuare eventuali errori.
    - Eseguire il cmdlet [Export-AIPLogs](/powershell/module/azureinformationprotection/export-aiplogs) per esportare e zippare i file di log dalla directory **%LocalAppData%\Microsoft\MSIP\Logs** .

1. Creare un file dump per il servizio MSIP scanner. In Gestione attività di Windows fare clic con il pulsante destro del mouse sul **servizio MSIP scanner** e scegliere **Crea file dump**.

1. Nel portale di Azure arrestare l'analisi. 

1. Nel computer dello scanner riavviare il servizio.

1. Aprire un ticket di supporto e alleghiare i file di dump dal processo dello scanner.

Per ulteriori informazioni, vedere [risoluzione dei problemi relativi a un'analisi che ha raggiunto il timeout](#troubleshooting-a-scan-that-timed-out). 

### <a name="unable-to-connect-to-remote-server"></a>Impossibile connettersi al server remoto

**Error (Errore) (Error (Errore)e)**

Nel file **% *LocalAppData*% \ Microsoft\MSIP\Logs\MSIPScanner.Iplog** ,`Unable to connect to the remote server ---> System.Net.Sockets.SocketException: Only one usage of each socket address (protocol/network address/port) is normally permitted IP:port`    

> [!NOTE]
> Il file verrà compresso se sono presenti più log.

**Descrizione**

Lo scanner ha superato il numero di connessioni di rete consentite.

**Soluzione**

Aumentare il numero di porte dinamiche per il sistema operativo che ospita i file.

Per altre informazioni su come visualizzare l'intervallo di porte corrente e aumentarlo, vedere [Impostazioni che possono essere modificate per migliorare le prestazioni di rete](/biztalk/technical-guides/settings-that-can-be-modified-to-improve-network-performance).


Vedere anche: [risoluzione dei problemi relativi a un'analisi che ha raggiunto il timeout](#troubleshooting-a-scan-that-timed-out).
### <a name="error-occurred-while-sending-the-request"></a>Si è verificato un errore durante l'invio della richiesta

**Messaggio di errore**

`[System.Net.Http.HttpRequestException: An error occurred while sending the request. ---> System.Net.WebException: The underlying connection was closed: An unexpected error occurred on a send. ---> System.IO.IOException: Unable to read data from the transport connection: An existing connection was forcibly closed by the remote host. ---> System.Net.Sockets.SocketException: An existing connection was forcibly closed by the remote host`

**Soluzione**

Questo errore indica in genere che TLS 1,2 non è abilitato.

Per altre informazioni, vedere:

- [Requisiti dell'infrastruttura di rete e dei firewall](requirements.md#firewalls-and-network-infrastructure)
- [Come abilitare TLS 1.2](/mem/configmgr/core/plan-design/security/enable-tls-1-2-client) 
- [Abilitare il supporto TLS 1,1 e TLS 1,2 in Office Online Server](/officeonlineserver/enable-tls-1-1-and-tls-1-2-support-in-office-online-server)


### <a name="missing-content-scan-job-or-profile"></a>Profilo o processo di analisi del contenuto mancante

**Error (Errore) (Error (Errore)e)**

Gli errori indicano che non è possibile trovare il profilo o il processo di analisi del contenuto.

Ad esempio, l'errore seguente nella portale di Azure nella pagina **nodi** : `No content scan job found`

**Soluzione**

Controllare la configurazione dello scanner nel portale di Azure.

Per altre informazioni, vedere [configurazione e installazione del Azure Information Protection scanner Unified Labeling](deploy-aip-scanner-configure-install.md). 

> [!NOTE]
> Un *profilo* è un termine dello scanner legacy che è stato sostituito dal cluster dello scanner e dal processo di analisi del contenuto nelle versioni più recenti dello scanner.
> 
### <a name="no-repositories-configured"></a>Nessun repository configurato

**Messaggio di errore**

Nella portale di Azure nella pagina **nodi** : `No repositories are configured`

**Descrizione**

È possibile che si disponga di un processo di analisi del contenuto senza repository configurati. 

**Soluzione**

Controllare le impostazioni del processo di analisi del contenuto e aggiungere almeno un repository. 

Per altre informazioni, vedere [creare un processo di analisi del contenuto](deploy-aip-scanner-configure-install.md#create-a-content-scan-job).

### <a name="no-cluster-found"></a>Non sono stati trovati cluster

**Messaggio di errore**

Nella portale di Azure nella pagina **nodi** : `No cluster found`

**Descrizione**

Non sono state trovate corrispondenze effettive per uno dei cluster di scanner definiti.

**Soluzione**

Verificare la configurazione del cluster e controllarla in base ai dettagli del sistema per errori e digitazioni.

Per altre informazioni, vedere [creare un cluster di scanner](deploy-aip-scanner-configure-install.md#create-a-scanner-cluster).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni, vedere il Blog relativo alle [procedure consigliate per la distribuzione e l'uso dello scanner AIP UL](https://techcommunity.microsoft.com/t5/microsoft-security-and/best-practices-for-deploying-and-using-the-aip-ul-scanner/ba-p/1878168).