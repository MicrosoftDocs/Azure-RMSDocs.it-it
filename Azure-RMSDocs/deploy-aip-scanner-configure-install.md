---
title: Installare e configurare lo scanner di etichettatura unificata di Azure Information Protection (AIP)
description: Istruzioni per l'installazione e la configurazione del Azure Information Protection scanner unificato di etichette per individuare, classificare e proteggere i file negli archivi dati.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/29/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: e786b30075f7a72781dd6cac13af4e14b70fc2db
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/07/2020
ms.locfileid: "86049642"
---
# <a name="configuring-and-installing-the--azure-information-protection-unified-labeling-scanner"></a>Configurazione e installazione dello scanner di Azure Information Protection Unified Labeling

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), windows server 2019, windows server 2016, windows Server 2012 R2*

>[!NOTE] 
> Se si lavora con lo scanner classico di AIP, vedere [installazione e configurazione dello scanner classico Azure Information Protection](deploy-aip-scanner-configure-install-classic.md).

Prima di iniziare la configurazione e l'installazione del Azure Information Protection scanner, verificare che il sistema sia conforme ai [prerequisiti richiesti](deploy-aip-scanner-prereqs.md).

Quando si è pronti, continuare con i passaggi seguenti:

1. [Configurare lo scanner nel portale di Azure](#configure-the-scanner-in-the-azure-portal)

1. [Installare lo scanner](#install-the-scanner)

1. [Ottenere un token di Azure AD per lo scanner](#get-an-azure-ad-token-for-the-scanner)

1. [Configurare lo scanner per applicare la classificazione e la protezione](#configure-the-scanner-to-apply-classification-and-protection)
 
Eseguire le seguenti procedure di configurazione aggiuntive secondo le necessità del sistema:

|Procedura  |Descrizione  |
|---------|---------|
|[Modificare i tipi di file da proteggere](#change-which-file-types-to-protect) |Potrebbe essere necessario analizzare, classificare o proteggere tipi di file diversi da quelli predefiniti. Per altre informazioni, vedere [processo di analisi AIP](deploy-aip-scanner.md#aip-scanning-process). |
|[Aggiornamento dello scanner](#upgrading-your-scanner) | Aggiornare lo scanner per sfruttare le funzionalità e i miglioramenti più recenti.|
|[Modifica delle impostazioni del repository di dati in blocco](#editing-data-repository-settings-in-bulk)| Usare le opzioni di importazione ed esportazione per apportare modifiche in blocco per più repository di dati.|
|[Usare lo scanner con configurazioni alternative](#using-the-scanner-with-alternative-configurations)| Usare lo scanner senza configurare le etichette con le condizioni |
|[Ottimizzare le prestazioni](#optimizing-scanner-performance)| Linee guida per ottimizzare le prestazioni dello scanner|
| | |

Per ulteriori informazioni, vedere anche [l'elenco dei cmdlet per lo scanner](#list-of-cmdlets-for-the-scanner).

## <a name="configure-the-scanner-in-the-azure-portal"></a>Configurare lo scanner nel portale di Azure

Prima di installare lo scanner o aggiornarlo da una versione di disponibilità generale precedente dello scanner, creare un cluster e un processo di analisi del contenuto per lo scanner nel portale di Azure. 

Configurare quindi il processo del cluster e dell'analisi del contenuto con le impostazioni dello scanner e i repository di dati da analizzare.

Per configurare lo scanner: 

1. [Accedere al portale di Azure](configure-policy.md#signing-in-to-the-azure-portal)e passare al riquadro **Azure Information Protection** . 
    
    Ad esempio, nella casella di ricerca di risorse, servizi e documentazione: iniziare a digitare **Informazioni** e selezionare **Azure Information Protection**.
    
1. Individuare le opzioni del menu **scanner** e selezionare **cluster**.

1. Nel riquadro **Azure Information Protection-cluster** selezionare **Aggiungi**:
    
    :::image type="content" source="media/scanner-add-profile.png" alt-text="Aggiunta del processo di analisi del contenuto per lo scanner Azure Information Protection":::

1. Nel riquadro **Aggiungi nuovo cluster** :

    1. Specificare un nome significativo per lo scanner. Questo nome viene usato per identificare le impostazioni di configurazione dello scanner e i repository di dati da analizzare. 

        Ad esempio, è possibile specificare **Europa** per identificare la posizione geografica dei repository di dati che verranno analizzati dallo scanner. Quando si installa o si aggiorna lo scanner in un secondo momento, sarà necessario specificare lo stesso nome del cluster.
   
    2. Facoltativamente, specificare una descrizione per scopi amministrativi che consenta di identificare il nome del cluster dello scanner.

    3. Selezionare **Salva**.
1. Individuare le opzioni del menu **scanner** e selezionare **processi di analisi del contenuto**.
1. Nel riquadro **processi di analisi del Azure Information Protection di contenuto** selezionare **Aggiungi**.
 
1. Per questa configurazione iniziale, configurare le impostazioni seguenti e quindi selezionare **Salva** senza chiudere il riquadro:
    
    |Sezione  |Impostazioni  |
    |---------|---------|
    |**Impostazioni del processo di analisi del contenuto**     |    - **Pianificazione**: Mantieni il valore predefinito **manuale** </br>- **Tipi di informazioni da**individuare: modificare **solo i criteri** </br>- **Configurare i repository**: non configurare in questo momento perché è necessario salvare prima il processo di analisi del contenuto.         |
    |**Imposizione dei criteri**     | - **Imponi**: seleziona **disattivato** </br>- **Etichettare i file in base al contenuto**: Mantieni il valore predefinito **in** </br>- **Etichetta predefinita**: Mantieni il valore predefinito dei **criteri predefiniti** </br>- Modifica **etichette file**: Mantieni il valore predefinito **off**        |
    |**Configurare le impostazioni del file**     | - **Mantieni "Data modifica", "Ultima modifica" e "modificato da"**: Mantieni il valore predefinito **in** </br>- **Tipi di file da analizzare**: Mantieni i tipi di file predefiniti per l' **esclusione** </br>- **Proprietario predefinito**: Mantieni il valore predefinito dell' **account scanner**        |
    | | |


1. Ora che il processo di analisi del contenuto viene creato e salvato, si è pronti per tornare all'opzione **Configura repository** per specificare gli archivi dati da analizzare. 

    Specificare i percorsi UNC e gli URL di SharePoint Server per le cartelle e le raccolte documenti locali di SharePoint. 
    
    > [!NOTE]
    > SharePoint Server 2019, SharePoint Server 2016 e SharePoint Server 2013 sono supportati per SharePoint. Anche SharePoint Server 2010 è supportato quando è disponibile il [supporto "Extended" per questa versione di SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).
    >     
    Per aggiungere il primo archivio dati, nel riquadro **Aggiungi un nuovo processo di analisi del contenuto** selezionare **Configura repository** per aprire il riquadro **repository** :
    
    :::image type="content" source="media/scanner-repositories-bar.png" alt-text="Configurare i repository di dati per lo scanner di Azure Information Protection":::

1. Nel riquadro **Repository** selezionare **Aggiungi**:
    
    :::image type="content" source="media/scanner-repository-add.png" alt-text="Aggiungere il repository di dati per lo scanner di Azure Information Protection":::

1. Nel riquadro **repository** specificare il percorso per il repository dei dati e quindi selezionare **Salva**.

    Ad esempio: 

    - Per una condivisione di rete, usare `\\Server\Folder` . 
    - Per una raccolta di SharePoint, usare `http://sharepoint.contoso.com/Shared%20Documents/Folder` .

    > [!NOTE]
    > I caratteri jolly e i percorsi WebDav non sono supportati.
    >     

    Quando si aggiungono i percorsi di SharePoint, utilizzare la sintassi seguente:
    
    |Percorso  |Sintassi  |
    |---------|---------|
    |**Percorso radice**     | `http://<SharePoint server name>` </br></br>Analizza tutti i siti, incluse le raccolte siti consentite per l'utente dello scanner. </br>Richiede [autorizzazioni aggiuntive](quickstart-findsensitiveinfo.md#permission-users-to-scan-sharepoint-repositories) per individuare automaticamente il contenuto radice        |
    |**Raccolta o sito secondario di SharePoint specifico**     | I tipi validi sono: </br>- `http://<SharePoint server name>/<subsite name>` </br>- `http://SharePoint server name>/<site collection name>/<site name>` </br></br>Richiede [autorizzazioni aggiuntive](quickstart-findsensitiveinfo.md#permission-users-to-scan-sharepoint-repositories) per individuare automaticamente il contenuto della raccolta siti         |
    |**Raccolta di SharePoint specifica**     | I tipi validi sono: </br>- `http://<SharePoint server name>/<library name>` </br>- `http://SharePoint server name>/.../<library name>`       |
    |**Cartella di SharePoint specifica**     | `http://<SharePoint server name>/.../<folder name>`        |
    | | |

    Per le impostazioni rimanenti di questo riquadro, non modificarle per questa configurazione iniziale, ma mantenerle come **predefinite del processo di analisi del contenuto**. L'impostazione predefinita indica che il repository dei dati eredita le impostazioni dal processo di analisi del contenuto.

    <!--
        > [!IMPORTANT]
        > While the local file system can be scanned, this configuration is not recommended for production deployments and can **only** be used in single node clusters.
        >
        > Scanning of local folders by multi-node clusters is not supported. If you need to scan a folder on the local file system, we recommend creating a share, and scanning it using a network URL.
    -->

1. Se si desidera aggiungere un altro repository di dati, ripetere i passaggi 8 e 9. 

1. Chiudere il riquadro **repository** e il riquadro del **processo di analisi del contenuto** . 

Tornare al riquadro del **processo di analisi del contenuto Azure Information Protection** , viene visualizzato il nome dell'analisi del contenuto, insieme alla colonna **Schedule** che mostra **Manual** e la colonna **Imponi** è vuota.

A questo punto si è pronti per installare lo scanner con il processo di analisi del contenuto creato. Continuare con [installare lo scanner](#install-the-scanner).

## <a name="install-the-scanner"></a>Installare lo scanner

Dopo aver [configurato il Azure Information Protection scanner nel portale di Azure](#configure-the-scanner-in-the-azure-portal), attenersi alla procedura seguente per installare lo scanner:

1. Accedere al computer Windows Server che eseguirà lo scanner. Usare un account con diritti di amministratore locale e con le autorizzazioni per scrivere nel database master di SQL Server.

    > [!IMPORTANT]
    > Per ulteriori informazioni, vedere [prerequisiti per l'installazione e la distribuzione di Azure Information Protection scanner](deploy-aip-scanner-prereqs.md).
    >
 
1. Aprire una sessione di Windows PowerShell con l'opzione **Esegui come amministratore**.

1. Eseguire il cmdlet [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner) , specificando l'istanza di SQL Server in cui creare un database per lo scanner Azure Information Protection e il nome del cluster dello scanner specificato nella sezione precedente: 
    
    ```
    Install-AIPScanner -SqlServerInstance <name> -Profile <cluster name>
    ```
    
    Esempi, usando il nome di profilo **Europe**:
    
    - Per un'istanza predefinita: `Install-AIPScanner -SqlServerInstance SQLSERVER1 -Profile Europe`
    
    - Per un'istanza denominata: `Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER -Profile Europe`
    
    - Per SQL Server Express: `Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS -Profile Europe`
    
    Quando viene richiesto, specificare le credenziali per l'account del servizio scanner ( \<domain\user name> ) e la password.

1. Verificare che il servizio sia ora installato utilizzando **strumenti di amministrazione**  >  **Servizi**. 
    
    Il servizio installato è denominato **Azure Information Protection Scanner** ed è configurato per essere eseguito usando l'account del servizio scanner creato.

Ora che è stato installato lo scanner, è necessario [ottenere un token di Azure ad per l'account del servizio scanner](#get-an-azure-ad-token-for-the-scanner) da autenticare, in modo che lo scanner possa essere eseguito in modo automatico. 

## <a name="get-an-azure-ad-token-for-the-scanner"></a>Ottenere un token di Azure AD per lo scanner

Un token di Azure AD consente allo scanner di eseguire l'autenticazione al servizio Azure Information Protection.

Per ottenere un token di Azure AD:

1. Tornare alla portale di Azure per creare un'applicazione Azure AD per specificare un token di accesso per l'autenticazione. Questo token consente di eseguire lo scanner in modo non interattivo. Per ulteriori informazioni, vedere [come etichettare i file in modo non interattivo per Azure Information Protection](./rms-client/clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection).

2. Dal computer Windows Server, se all'account del servizio di scanner è stato concesso il diritto di **accesso locale** per l'installazione, accedere con questo account e avviare una sessione di PowerShell. 

    Eseguire [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) specificando i valori copiati nel passaggio precedente:
    
    ```ps
    Set-AIPAuthentication -AppId <ID of the registered app> -AppSecret <client secret sting> -TenantId <your tenant ID> -DelegatedUser <Azure AD account>
    ```
        
    Ad esempio:

    ```ps
    $pscreds = Get-Credential CONTOSO\scanner
    Set-AIPAuthentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -DelegatedUser scanner@contoso.com -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -OnBehalfOf $pscreds
    Acquired application access token on behalf of CONTOSO\scanner.
    ```

> [!TIP]
> Se all'account del servizio scanner non è possibile concedere il diritto di **accesso locale** per l'installazione, usare il parametro *OnBehalfOf* con [set-AIPAuthentication](https://docs.microsoft.com/powershell/module/azureinformationprotection/set-aipauthentication), come descritto in [come etichettare i file in modo non interattivo per Azure Information Protection](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection).

Lo scanner dispone ora di un token per l'autenticazione a Azure AD, che è valido per un anno, due anni o mai, in base alla configurazione del segreto client di/API per l' **app Web** nel Azure ad. 

Quando il token scade, è necessario ripetere questa procedura.

Si è ora pronti per eseguire la prima analisi in modalità di individuazione. Per altre informazioni, vedere [eseguire un ciclo di individuazione e visualizzare i report per lo scanner](deploy-aip-scanner-manage.md#run-a-discovery-cycle-and-view-reports-for-the-scanner).

Se è già stata eseguita un'analisi di individuazione, continuare con [configurare lo scanner per applicare la classificazione e la protezione](#configure-the-scanner-to-apply-classification-and-protection).

## <a name="configure-the-scanner-to-apply-classification-and-protection"></a>Configurare lo scanner per applicare la classificazione e la protezione

Le impostazioni predefinite consentono di configurare lo scanner affinché venga eseguito una sola volta e in modalità di sola segnalazione.

Per modificare queste impostazioni, modificare il processo di analisi del contenuto:

1. Nella portale di Azure, nel riquadro **processi di analisi Azure Information Protection-contenuto** selezionare il processo del cluster e del processo di analisi del contenuto da modificare.

2. Nel riquadro del processo di analisi del contenuto modificare gli elementi seguenti e quindi selezionare **Salva**:
    
   - Nella sezione del **processo di analisi del contenuto** modificare la **pianificazione** in **Always** .
   - Dalla sezione relativa all' **applicazione dei criteri** : modificare **applica** a **attivato**
    
    > [!TIP]
    > Potrebbe essere necessario modificare le altre impostazioni in questo riquadro, ad esempio se gli attributi del file vengono modificati e se lo scanner è in grado di rietichettare i file. Usare la Guida con informazioni popup per altre informazioni sulle singole impostazioni di configurazione.

3. Prendere nota dell'ora corrente e avviare di nuovo lo scanner dal riquadro **processi di analisi del Azure Information Protection-contenuto** :

    :::image type="content" source="media/scanner-scan-now.png" alt-text="Avviare l'analisi per lo scanner di Azure Information Protection":::
    
    In alternativa, eseguire il comando seguente nella sessione di PowerShell:
    
    ```ps
    Start-AIPScan
    ```

Lo scanner è ora pianificato per l'esecuzione continua. Quando lo scanner funziona in tutti i file configurati, avvia automaticamente un nuovo ciclo in modo che vengano individuati tutti i file nuovi e modificati.

## <a name="change-which-file-types-to-protect"></a>Modificare i tipi di file da proteggere

Per impostazione predefinita, lo scanner AIP protegge solo i tipi di file di Office e i file PDF.

Usare i comandi di PowerShell per modificare questo comportamento in base alle esigenze, ad esempio per configurare lo scanner in modo da proteggere tutti i tipi di file, come per il client o per proteggere altri tipi di file specifici. 

Per un criterio etichetta applicabile all'account utente che Scarica le etichette per lo scanner, specificare un'impostazione avanzata di PowerShell denominata **PFileSupportedExtensions**. 

Per uno scanner con accesso a Internet, questo account utente è l'account specificato per il parametro *DelegatedUser* con il comando set-AIPAuthentication.

**Esempio 1:**  Comando di PowerShell per lo scanner per proteggere tutti i tipi di file, in cui il criterio dell'etichetta è denominato "scanner":

```ps
Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions="*"}
```

**Esempio 2:** Comando di PowerShell per lo scanner per proteggere i file con estensione XML e i file TIFF oltre ai file di Office e PDF, in cui il criterio dell'etichetta è denominato "scanner":

```ps
Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions=ConvertTo-Json(".xml", ".tiff")}
```

Per ulteriori informazioni, vedere [modificare i tipi di file da proteggere](./rms-client/clientv2-admin-guide-customizations.md#change-which-file-types-to-protect).

## <a name="upgrading-your-scanner"></a>Aggiornamento dello scanner
 
Se in precedenza è stato installato lo scanner e si vuole eseguire l'aggiornamento, usare le istruzioni descritte in [aggiornamento dello scanner Azure Information Protection](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner).

Quindi, [configurare](deploy-aip-scanner-configure-install.md) e [usare lo scanner](deploy-aip-scanner-manage.md) come di consueto, ignorando i passaggi per installare lo scanner.

## <a name="editing-data-repository-settings-in-bulk"></a>Modifica delle impostazioni del repository di dati in blocco

Usare i pulsanti **Esporta** e **Importa** per apportare modifiche per lo scanner in diversi repository. 

In questo modo, non è necessario apportare le stesse modifiche più volte manualmente nel portale di Azure.

Se, ad esempio, si dispone di un nuovo tipo di file in diversi repository di dati SharePoint, è possibile aggiornare in blocco le impostazioni per tali repository.

Per apportare modifiche in blocco tra i repository:

1. Nella portale di Azure nel riquadro **repository** selezionare l'opzione **Esporta** . Ad esempio:

    :::image type="content" source="media/export-scanner-repositories.png" alt-text="Esportazione delle impostazioni del repository di dati per lo scanner Azure Information Protection":::

1. Modificare manualmente il file esportato per apportare la modifica. 

1. Usare l'opzione di **importazione** nella stessa pagina per importare nuovamente gli aggiornamenti nei repository.

## <a name="using-the-scanner-with-alternative-configurations"></a>Uso dello scanner con configurazioni alternative

Lo scanner Azure Information Protection in genere cerca le condizioni specificate per le etichette per classificare e proteggere il contenuto in base alle esigenze.

Negli scenari seguenti, lo scanner Azure Information Protection è anche in grado di analizzare il contenuto e gestire le etichette, senza alcuna condizione configurata:

- [Applicare un'etichetta predefinita a tutti i file in un repository di dati](#apply-a-default-label-to-all-files-in-a-data-repository)
- [Rimuovere le etichette esistenti da tutti i file in un repository di dati](#remove-existing-labels-from-all-files-in-a-data-repository)
- [Identificare tutte le condizioni personalizzate e i tipi di informazioni riservate note](#identify-all-custom-conditions-and-known-sensitive-information-types)
### <a name="apply-a-default-label-to-all-files-in-a-data-repository"></a>Applicare un'etichetta predefinita a tutti i file in un repository di dati

In questa configurazione tutti i file senza etichetta nel repository sono contrassegnati con l'etichetta predefinita specificata per il repository o il processo di analisi del contenuto. I file sono contrassegnati senza ispezione. 

Configurare le seguenti impostazioni: 

|Impostazione  |Descrizione  |
|---------|---------|
|**Etichettare i file in base al contenuto**    |Imposta su **disattivato**         |
|**Etichetta predefinita**     | Impostare su **personalizzato**, quindi selezionare l'etichetta da usare       |
|**Applica etichetta predefinita**     | Selezionare questa opzione per fare in modo che l'etichetta predefinita venga applicata a tutti i file, anche se è già etichettata.        |
| | |

### <a name="remove-existing-labels-from-all-files-in-a-data-repository"></a>Rimuovere le etichette esistenti da tutti i file in un repository di dati

In questa configurazione tutte le etichette esistenti vengono rimosse, inclusa la protezione, se la protezione è stata applicata con l'etichetta. La protezione applicata indipendentemente da un'etichetta viene mantenuta.

Configurare le seguenti impostazioni: 

|Impostazione  |Descrizione  |
|---------|---------|
|**Etichettare i file in base al contenuto**    |Imposta su **disattivato**         |
|**Etichetta predefinita**     | Imposta su **nessuno**  |
|**Modifica etichette file** | Impostare **su on**, con la casella di controllo **Imponi etichetta predefinita** selezionata|
| | |

### <a name="identify-all-custom-conditions-and-known-sensitive-information-types"></a>Identificare tutte le condizioni personalizzate e i tipi di informazioni riservate note

Questa configurazione consente di trovare informazioni riservate che potrebbero non essere realizzate, a scapito delle frequenze di analisi per lo scanner. 

Impostare i **tipi di informazioni da** individuare su **tutti**. 

Per identificare le condizioni e i tipi di informazioni per l'assegnazione di etichette, lo scanner utilizza tutti i tipi di informazioni riservate personalizzate specificati e l'elenco dei tipi di informazioni riservate predefinite che è possibile selezionare, come definito nel centro di gestione delle etichette.

## <a name="optimizing-scanner-performance"></a>Ottimizzazione delle prestazioni dello scanner

> [!NOTE]
> Se si desidera migliorare la velocità di risposta del computer dello scanner anziché le prestazioni dello scanner, utilizzare un'impostazione client avanzata per [limitare il numero di thread utilizzati dallo scanner](./rms-client/clientv2-admin-guide-customizations.md#limit-the-number-of-threads-used-by-the-scanner).
> 

Usare le opzioni e le linee guida seguenti per ottimizzare le prestazioni dello scanner:

|Opzione  |Description  |
|---------|---------|
|**Disporre di una connessione di rete ad alta velocità e affidabile tra il computer dello scanner e l'archivio dei dati analizzati**     |  Ad esempio, posizionare il computer dello scanner nella stessa LAN o preferibilmente nello stesso segmento di rete dell'archivio dati scansionato. </br></br>La qualità della connessione di rete influiscono sulle prestazioni dello scanner perché, per esaminare i file, lo scanner trasferisce il contenuto dei file nel computer in cui è in esecuzione il servizio scanner. </br></br>Riducendo o eliminando gli hop di rete necessari per i dati da spostare, viene ridotto anche il carico sulla rete.      |
|**Verificare che il computer dello scanner abbia risorse del processore disponibili**     | Esaminare il contenuto del file e crittografare e decrittografare i file sono azioni che richiedono un utilizzo intensivo del processore. </br></br>Monitorare i cicli di analisi tipici degli archivi dati specificati per identificare se le risorse del processore influiscono negativamente sulle prestazioni dello scanner.        |
|**Installare più istanze dello scanner** | Lo scanner Azure Information Protection supporta più database di configurazione nella stessa istanza di SQL Server quando si specifica un nome di cluster personalizzato (profilo) per lo scanner. </br></br>Più scanner possono inoltre condividere lo stesso cluster (profilo), ottenendo tempi di analisi più rapidi.|
|**Controllare l'utilizzo della configurazione alternativa** |L'esecuzione dello scanner è più rapida quando si usa la [configurazione alternativa](#using-the-scanner-with-alternative-configurations) per applicare un'etichetta predefinita a tutti i file in quanto lo scanner non esamina i contenuti del file. <br/></br>L'esecuzione dello scanner è più lenta quando si usa la [configurazione alternativa](#using-the-scanner-with-alternative-configurations) per identificare tutte le condizioni personalizzate e i tipi di informazioni riservate noti.|
| | |

<!-- removed when removing local folders
|**Do not scan local folders on the computer running the scanner service**     | If you have folders to scan on a Windows server, install the scanner on a different computer and configure those folders as network shares to scan. </br></br>Separating the two functions of hosting files and scanning files means that the computing resources for these services are not competing with one another.        |
-->

### <a name="additional-factors-that-affect-performance"></a>Fattori aggiuntivi che influiscono sulle prestazioni

Ulteriori fattori che influiscono sulle prestazioni dello scanner includono:

|Fattore  |Descrizione  |
|---------|---------|
|**Tempi di caricamento/risposta**     |Anche i tempi di caricamento e di risposta correnti degli archivi dati che contengono i file da analizzare influiscono sulle prestazioni dello scanner.         |
|**Modalità scanner** (individuazione/applicazione)    | La modalità di individuazione ha in genere una velocità di analisi superiore rispetto alla modalità di applicazione. </br></br>Per l'individuazione è necessaria un'azione di lettura di un singolo file, mentre la modalità di applicazione richiede azioni di lettura e scrittura.        |
|**Modifiche dei criteri**     |È possibile che le prestazioni dello scanner siano invariate se sono state apportate modifiche all'etichettatura automatica nei criteri etichetta. </br></br>Il primo ciclo di analisi, quando lo scanner deve controllare tutti i file, avrà più tempo dei cicli di analisi successivi che, per impostazione predefinita, ispeziona solo i file nuovi e modificati. </br></br>Se si modificano le condizioni o le impostazioni di etichetta automatica, tutti i file vengono nuovamente sottoposti a scansione. Per ulteriori informazioni, vedere ripetizione dell' [analisi dei file](deploy-aip-scanner-manage.md#rescanning-files).|
|**Costruzioni Regex**    | Le prestazioni dello scanner sono influenzate dal modo in cui vengono costruite le espressioni Regex per le condizioni personalizzate. </br></br> Per evitare un consumo intenso di memoria e il rischio di timeout (15 minuti per ogni file), rivedere le espressioni regex per assicurarsi che usino criteri di ricerca efficienti. </br></br>Ad esempio: </br>-Evitare [quantificatori greedy](https://docs.microsoft.com/dotnet/standard/base-types/quantifiers-in-regular-expressions) </br>-Usare gruppi non di acquisizione come `(?:expression)` anziché`(expression)`    |
|**Livello di registrazione**     |  Le opzioni a livello di log includono **debug**, **info**, **Error** e **off** per i report dello scanner.</br></br>- **Risultati migliori** prestazioni </br>- Il **debug** rallenta notevolmente lo scanner e deve essere usato solo per la risoluzione dei problemi. </br></br>Per altre informazioni, vedere il parametro *ReportLevel* del cmdlet [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration).       |
|**File sottoposti a scansione**     |-Ad eccezione dei file di Excel, i file di Office vengono analizzati più rapidamente rispetto ai file PDF. </br></br>-I file non protetti sono più veloci da analizzare rispetto ai file protetti. </br></br>-I file di grandi dimensioni hanno ovviamente più tempo per l'analisi di file di piccole dimensioni.         |
| | |

## <a name="list-of-cmdlets-for-the-scanner"></a>Elenco dei cmdlet per lo scanner

Questa sezione elenca i cmdlet di PowerShell supportati per lo scanner Azure Information Protection.

> [!NOTE]
> Lo scanner Azure Information Protection viene configurato dal portale di Azure. Pertanto, i cmdlet usati nelle versioni precedenti per configurare i repository dei dati e l'elenco dei tipi di file analizzati sono ora deprecati.
> 

I cmdlet supportati per lo scanner includono:

- [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration)

- [Get-AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus)

- [Export-AIPLogs](/powershell/module/azureinformationprotection/Export-AIPLogs)

- [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration)

- [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner)

- [Set-AIPScanner](/powershell/module/azureinformationprotection/Set-AIPScanner)

- [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)

- [Start-AIPScanDiagnostics](/powershell/module/azureinformationprotection/Start-AIPScanDiagnostics)

- [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan)

- [Stop-AIPScan](/powershell/module/azureinformationprotection/Stop-AIPScan)

- [Uninstall-AIPScanner](/powershell/module/azureinformationprotection/Uninstall-AIPScanner)

- [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner)

## <a name="next-steps"></a>Passaggi successivi

Dopo aver installato e configurato lo scanner, avviare [l'analisi dei file](deploy-aip-scanner-manage.md).

Vedere anche: [distribuzione di Azure Information Protection scanner per classificare e proteggere automaticamente i file](deploy-aip-scanner.md).

**Ulteriori informazioni:**

- Se si è interessati a scoprire come è stato implementato questo scanner dai team Microsoft Core Services Engineering e Operations,  leggere il case study tecnico: [Automating data protection with Azure Information Protection scanner](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner) (Automatizzazione della protezione dei dati con lo scanner di Azure Information Protection).

- Ci si potrebbe chiedere: [Qual è la differenza tra il cluster di failover di Windows Server e il Azure Information Protection scanner?](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

- Usare PowerShell per classificare e proteggere in modo interattivo i file dal computer desktop. Per altre informazioni su questo e altri scenari in cui viene usato PowerShell, vedere [uso di PowerShell con il Azure Information Protection Unified Labeling client](./rms-client/clientv2-admin-guide-powershell.md).
