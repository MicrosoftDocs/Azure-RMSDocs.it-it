---
title: Installare e configurare lo scanner di Azure Information Protection (AIP)
description: Istruzioni per l'installazione e la configurazione di Azure Information Protection scanner per individuare, classificare e proteggere i file negli archivi dati.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 02/01/2021
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ROBOTS: NOINDEX
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 46655ef7da2d8670ef3fced105b3d471bb05a8f9
ms.sourcegitcommit: caf2978ab03e4893b59175ce753791867793dcfe
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2021
ms.locfileid: "100524762"
---
# <a name="configuring-and-installing-the-azure-information-protection-classic-scanner"></a>Configurazione e installazione dello scanner classico Azure Information Protection

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 *
>
>***Pertinente per**: [Azure Information Protection client classico per Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per il client di etichettatura unificata, vedere [installazione e configurazione di AIP Unified Labeling scanner](deploy-aip-scanner-configure-install.md). *

> [!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

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

    Ad esempio, nella casella di ricerca di risorse, servizi e documentazione: iniziare a digitare **Information** e selezionare **Azure Information Protection**.

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
    |**Impostazioni del processo di analisi del contenuto**     |    - **Pianificazione**: Mantieni il valore predefinito **manuale** </br>- **Tipi di informazioni da** individuare: modificare **solo i criteri** </br>- **Configurare i repository**: non configurare in questo momento perché è necessario salvare prima il processo di analisi del contenuto.         |
    |**Criteri di riservatezza**     | - **Imponi**: seleziona **disattivato** </br>- **Etichettare i file in base al contenuto**: Mantieni il valore predefinito **in** </br>- **Etichetta predefinita**: Mantieni il valore predefinito dei **criteri predefiniti** </br>- Modifica **etichette file**: Mantieni il valore predefinito **off**        |
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

    :::image type="content" source="media/scanner-repository-add.png" alt-text="Aggiungere repository di dati per lo scanner Azure Information Protection":::

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

    ```PowerShell
    Install-AIPScanner -SqlServerInstance <name> -Profile <cluster name>
    ```

    Esempi, usando il nome di profilo **Europe**:

    - Per un'istanza predefinita: `Install-AIPScanner -SqlServerInstance SQLSERVER1 -Profile Europe`

    - Per un'istanza denominata: `Install-AIPScanner -SqlServerInstance SQLSERVER1\AIPSCANNER -Profile Europe`

    - Per SQL Server Express: `Install-AIPScanner -SqlServerInstance SQLSERVER1\SQLEXPRESS -Profile Europe`

    Quando viene richiesto, specificare le credenziali per l'account del servizio scanner ( `\<domain\user name>` ) e la password.

1. Verificare che il servizio sia ora installato utilizzando **strumenti di amministrazione**  >  **Servizi**.

    Il servizio installato è denominato **Azure Information Protection Scanner** ed è configurato per essere eseguito usando l'account del servizio scanner creato.

Ora che è stato installato lo scanner, è necessario [ottenere un token di Azure ad per l'account del servizio scanner](#get-an-azure-ad-token-for-the-scanner) da autenticare, in modo che lo scanner possa essere eseguito in modo automatico.

## <a name="get-an-azure-ad-token-for-the-scanner"></a>Ottenere un token di Azure AD per lo scanner

Un token di Azure AD consente allo scanner di eseguire l'autenticazione al servizio Azure Information Protection.

Per ottenere un token di Azure AD:

1. Tornare alla portale di Azure per creare due applicazioni Azure AD per specificare un token di accesso per l'autenticazione. Questo token consente di eseguire lo scanner in modo non interattivo.

    Per altre informazioni, vedere [Come assegnare un'etichetta ai file in modo non interattivo per Azure Information Protection](./rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection).

2. Dal computer Windows Server, se all'account del servizio di scanner è stato concesso il diritto di **accesso locale** per l'installazione, accedere con questo account e avviare una sessione di PowerShell.

    Eseguire [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) specificando i valori copiati nel passaggio precedente:

    ```PowerShell
    Set-AIPAuthentication -webAppId <ID of the "Web app / API" application> -webAppKey <key value generated in the "Web app / API" application> -nativeAppId <ID of the "Native" application>
    ```

    Quando richiesto, specificare la password per le credenziali dell'account del servizio per Azure AD e quindi fare clic su **Accetto**.

    Ad esempio:

    ```PowerShell
    Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "+LBkMvddz?WrlNCK5v0e6_=meM59sSAn" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f").token | clip
    Acquired application access token on behalf of the user
    ```

> [!TIP]
> Se all'account del servizio di scanner non è possibile concedere il diritto di **accesso locale** , [specificare e usare il parametro token per set-AIPAuthentication](./rms-client/client-admin-guide-powershell.md#specify-and-use-the-token-parameter-for-set-aipauthentication).
>

Lo scanner dispone ora di un token per l'autenticazione a Azure AD, che è valido per un anno, due anni o mai, in base alla configurazione dell' **app Web/API** in Azure ad.

Quando il token scade, è necessario ripetere i passaggi 1 e 2.

Si è ora pronti per eseguire la prima analisi in modalità di individuazione. Per altre informazioni, vedere [eseguire un ciclo di individuazione e visualizzare i report per lo scanner](deploy-aip-scanner-manage.md#run-a-discovery-cycle-and-view-reports-for-the-scanner).

Se è già stata eseguita un'analisi di individuazione, continuare con [configurare lo scanner per applicare la classificazione e la protezione](#configure-the-scanner-to-apply-classification-and-protection).

## <a name="configure-the-scanner-to-apply-classification-and-protection"></a>Configurare lo scanner per applicare la classificazione e la protezione

Le impostazioni predefinite consentono di configurare lo scanner affinché venga eseguito una sola volta e in modalità di sola segnalazione.

Per modificare queste impostazioni, modificare il processo di analisi del contenuto:

1. Nella portale di Azure, nel riquadro **processi di analisi Azure Information Protection-contenuto** selezionare il processo del cluster e del processo di analisi del contenuto da modificare.

2. Nel riquadro del processo di analisi del contenuto modificare gli elementi seguenti e quindi selezionare **Salva**:

   - Nella sezione del **processo di analisi del contenuto** modificare la **pianificazione** in **Always** .
   - Nella sezione **criteri di riservatezza** : modificare **applica** a **on**

    > [!TIP]
    > Potrebbe essere necessario modificare le altre impostazioni in questo riquadro, ad esempio se gli attributi del file vengono modificati e se lo scanner è in grado di rietichettare i file. Usare la Guida con informazioni popup per altre informazioni sulle singole impostazioni di configurazione.

3. Prendere nota dell'ora corrente e avviare di nuovo lo scanner dal riquadro **processi di analisi del Azure Information Protection-contenuto** :

    ![Avviare l'analisi per lo scanner di Azure Information Protection](./media/scanner-scan-now.png)

    In alternativa, eseguire il comando seguente nella sessione di PowerShell:

    ```PowerShell
    Start-AIPScan
    ```

4. Per visualizzare i report dei file con etichetta, quale classificazione è stata applicata e se è stata applicata la protezione, monitorare il registro eventi per il tipo informativo **911** e l'indicatore di ora più recente.

    Per informazioni dettagliate, controllare i report o usare i portale di Azure.

Lo scanner è ora pianificato per l'esecuzione continua. Quando lo scanner funziona in tutti i file configurati, avvia automaticamente un nuovo ciclo in modo che vengano individuati tutti i file nuovi e modificati.

## <a name="change-which-file-types-to-protect"></a>Modificare i tipi di file da proteggere

Per impostazione predefinita, lo scanner AIP protegge solo i tipi di file di Office e i file PDF. Per modificare questo comportamento, ad esempio per configurare lo scanner in modo da proteggere tutti i tipi di file, proprio come il client o per proteggere tipi di file aggiuntivi specifici, modificare il registro di sistema come segue:

- Specificare i tipi di file aggiuntivi che si desidera proteggere
- Specificare il tipo di protezione che si vuole applicare (nativo o generico)

Per fare riferimento alla protezione generica, questa documentazione per sviluppatori usa il termine "PFile".

Per allineare i tipi di file supportati con il client di, in cui tutti i file vengono protetti automaticamente con la protezione nativa o generica:

1. Specificare:

    - `*`Carattere jolly come chiave del registro di sistema
    - `Encryption` come valore (REG_SZ)
    - `Default` come dati del valore

1. Verificare che le chiavi **MSIPC** e **fileprotection** esistano. Crearli manualmente in caso contrario, quindi creare una sottochiave per ogni estensione di file.

    Ad esempio, affinché lo Scanner protegga le immagini TIFF oltre ai file di Office e PDF, il registro di sistema sarà simile al seguente dopo che è stato modificato:

    ![Modifica del Registro di sistema per l'applicazione della protezione con lo scanner](./media/editregistry-scanner.png)

    > [!NOTE]
    > Come file di immagine, i file TIFF supportano la protezione nativa e l'estensione del nome file risultante è **. ptiff**.
    >

    Per i file che non supportano la protezione nativa, specificare l'estensione del nome file come nuova chiave e **PFile** per la protezione generica. L'estensione del nome file risultante per il file protetto è **. Pfile**.

Per un elenco di tipi di file di testo e immagini che supportano la protezione nativa in modo analogo, ma che devono essere specificati nel registro di sistema, vedere [tipi di file supportati per la classificazione e la protezione](./rms-client/client-admin-guide-file-types.md#file-types-supported-for-protection).

## <a name="upgrading-your-scanner"></a>Aggiornamento dello scanner

Se lo scanner è stato installato in precedenza e si vuole eseguire l'aggiornamento, vedere [aggiornamento dello scanner Azure Information Protection](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner).

Quindi, [configurare](deploy-aip-scanner-configure-install-classic.md) e [usare lo scanner](deploy-aip-scanner-manage-classic.md) come di consueto, ignorando i passaggi per installare lo scanner.

>[!NOTE]
> Se si dispone di una versione dello scanner precedente a 1.48.204.0 e non si è pronti per aggiornarla, vedere [distribuzione di versioni precedenti dello scanner Azure Information Protection per classificare e proteggere automaticamente i file](deploy-aip-scanner-previousversions.md).

## <a name="editing-data-repository-settings-in-bulk"></a>Modifica delle impostazioni del repository di dati in blocco

Usare i pulsanti **Esporta** e **Importa** per apportare modifiche per lo scanner in diversi repository.

In questo modo, non è necessario apportare le stesse modifiche più volte manualmente nel portale di Azure.

Se, ad esempio, si dispone di un nuovo tipo di file in diversi repository di dati SharePoint, è possibile aggiornare in blocco le impostazioni per tali repository.

Per apportare modifiche in blocco tra i repository:

1. Nella portale di Azure nel riquadro **repository** selezionare l'opzione **Esporta** . Ad esempio:

    :::image type="content" source="media/export-scanner-repositories.png" alt-text="Esportazione delle impostazioni del repository dei dati per lo scanner":::

1. Modificare manualmente il file esportato per apportare la modifica.

1. Usare l'opzione di **importazione** nella stessa pagina per importare nuovamente gli aggiornamenti nei repository.

## <a name="using-the-scanner-with-alternative-configurations"></a>Uso dello scanner con configurazioni alternative

Lo scanner Azure Information Protection in genere cerca le condizioni specificate per le etichette per classificare e proteggere il contenuto in base alle esigenze.

Negli scenari seguenti, lo scanner Azure Information Protection è anche in grado di analizzare il contenuto e gestire le etichette, senza alcuna condizione configurata:

- [Applicare un'etichetta predefinita a tutti i file in un repository di dati](#apply-a-default-label-to-all-files-in-a-data-repository)
- [Identificare tutte le condizioni personalizzate e i tipi di informazioni riservate note](#identify-all-custom-conditions-and-known-sensitive-information-types)

### <a name="apply-a-default-label-to-all-files-in-a-data-repository"></a>Applicare un'etichetta predefinita a tutti i file in un repository di dati

In questa configurazione tutti i file senza etichetta nel repository sono contrassegnati con l'etichetta predefinita specificata per il repository o il processo di analisi del contenuto. I file sono contrassegnati senza ispezione.

Configurare le seguenti impostazioni:

- **Etichettare i file in base al contenuto**: impostato su **disattivato**
- **Etichetta predefinita**: impostare su **personalizzato**, quindi selezionare l'etichetta da usare

### <a name="identify-all-custom-conditions-and-known-sensitive-information-types"></a>Identificare tutte le condizioni personalizzate e i tipi di informazioni riservate note

Questa configurazione consente di trovare informazioni riservate che potrebbero non essere realizzate, a scapito delle frequenze di analisi per lo scanner.

Impostare i **tipi di informazioni da** individuare su **tutti**.

Per identificare le condizioni e i tipi di informazioni per l'assegnazione di etichette, lo scanner USA condizioni personalizzate specificate per le etichette e l'elenco dei tipi di informazioni disponibili per specificare le etichette, elencate nei criteri di Azure Information Protection.

Per ulteriori informazioni, vedere [Guida introduttiva: trovare le informazioni riservate](quickstart-findsensitiveinfo.md).

## <a name="optimizing-scanner-performance"></a>Ottimizzazione delle prestazioni dello scanner

> [!NOTE]
> Se si desidera migliorare la velocità di risposta del computer dello scanner anziché le prestazioni dello scanner, utilizzare un'impostazione client avanzata per [limitare il numero di thread utilizzati dallo scanner](./rms-client/client-admin-guide-customizations.md#limit-the-number-of-threads-used-by-the-scanner).
>

Usare le opzioni e le linee guida seguenti per ottimizzare le prestazioni dello scanner:

|Opzione  |Descrizione  |
|---------|---------|
|**Disporre di una connessione di rete ad alta velocità e affidabile tra il computer dello scanner e l'archivio dei dati analizzati**     |  Ad esempio, posizionare il computer dello scanner nella stessa LAN o preferibilmente nello stesso segmento di rete dell'archivio dati scansionato. </br></br>La qualità della connessione di rete influiscono sulle prestazioni dello scanner perché, per esaminare i file, lo scanner trasferisce il contenuto dei file nel computer in cui è in esecuzione il servizio scanner. </br></br>Riducendo o eliminando gli hop di rete necessari per i dati da spostare, viene ridotto anche il carico sulla rete.      |
|**Verificare che il computer dello scanner abbia risorse del processore disponibili**     | Esaminare il contenuto del file e crittografare e decrittografare i file sono azioni che richiedono un utilizzo intensivo del processore. </br></br>Monitorare i cicli di analisi tipici degli archivi dati specificati per identificare se le risorse del processore influiscono negativamente sulle prestazioni dello scanner.        |
|**Installare più istanze dello scanner** | Lo scanner Azure Information Protection supporta più database di configurazione nella stessa istanza di SQL Server quando si specifica un nome di cluster personalizzato (profilo) per lo scanner. |
|**Concedere diritti specifici e disabilitare il livello di integrità basso**|Verificare che l'account di servizio che esegue lo scanner disponga solo dei diritti documentati nei [requisiti dell'account del servizio](deploy-aip-scanner-prereqs.md#service-account-requirements). </br></br>Configurare quindi l' [impostazione client avanzata](./rms-client/client-admin-guide-customizations.md#disable-the-low-integrity-level-for-the-scanner) per disabilitare il livello di integrità basso per lo scanner.|
|**Controllare l'utilizzo della configurazione alternativa** |L'esecuzione dello scanner è più rapida quando si usa la [configurazione alternativa](#using-the-scanner-with-alternative-configurations) per applicare un'etichetta predefinita a tutti i file in quanto lo scanner non esamina i contenuti del file. <br/></br>L'esecuzione dello scanner è più lenta quando si usa la [configurazione alternativa](#using-the-scanner-with-alternative-configurations) per identificare tutte le condizioni personalizzate e i tipi di informazioni riservate noti.|
|**Riduci timeout scanner** | Ridurre i timeout dello scanner con [le impostazioni client avanzate](./rms-client/client-admin-guide-customizations.md#change-the-timeout-settings-for-the-scanner). I timeout dello scanner ridotti forniscono frequenze di analisi migliori e un consumo di memoria inferiore. </br></br>**Nota**: la riduzione dei timeout dello scanner indica che alcuni file possono essere ignorati.
| | |


### <a name="additional-factors-that-affect-performance"></a>Fattori aggiuntivi che influiscono sulle prestazioni

Ulteriori fattori che influiscono sulle prestazioni dello scanner includono:

|Fattore  |Descrizione  |
|---------|---------|
|**Tempi di caricamento/risposta**     |Anche i tempi di caricamento e di risposta correnti degli archivi dati che contengono i file da analizzare influiscono sulle prestazioni dello scanner.         |
|**Modalità scanner** (individuazione/applicazione)    | La modalità di individuazione ha in genere una velocità di analisi superiore rispetto alla modalità di applicazione. </br></br>Per l'individuazione è necessaria un'azione di lettura di un singolo file, mentre la modalità di applicazione richiede azioni di lettura e scrittura.        |
|**Modifiche dei criteri**     |Le prestazioni dello scanner potrebbero essere interessate se sono state apportate modifiche alle condizioni nei criteri di Azure Information Protection. </br></br>Il primo ciclo di analisi, quando lo scanner deve controllare tutti i file, avrà più tempo dei cicli di analisi successivi che, per impostazione predefinita, ispeziona solo i file nuovi e modificati. </br></br>Se si modificano le condizioni, tutti i file vengono nuovamente sottoposti a scansione. Per ulteriori informazioni, vedere ripetizione dell' [analisi dei file](deploy-aip-scanner-manage-classic.md#rescanning-files).|
|**Costruzioni Regex**    | Le prestazioni dello scanner sono influenzate dal modo in cui vengono costruite le espressioni Regex per le condizioni personalizzate. </br></br> Per evitare un consumo intenso di memoria e il rischio di timeout (15 minuti per ogni file), rivedere le espressioni regex per assicurarsi che usino criteri di ricerca efficienti. </br></br>Ad esempio: </br>-Evitare [quantificatori greedy](/dotnet/standard/base-types/quantifiers-in-regular-expressions) </br>-Usare gruppi non di acquisizione come `(?:expression)` anziché `(expression)`    |
|**Livello di log**     |  Le opzioni a livello di log includono **debug**, **info**, **Error** e **off** per i report dello scanner.</br></br>- **Risultati migliori** prestazioni </br>- Il **debug** rallenta notevolmente lo scanner e deve essere usato solo per la risoluzione dei problemi. </br></br>Per altre informazioni, vedere il parametro *ReportLevel* del cmdlet [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration).       |
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

**Ulteriori informazioni**:

Se si è interessati a scoprire come è stato implementato questo scanner dai team Microsoft Core Services Engineering e Operations,  leggere il case study tecnico: [Automating data protection with Azure Information Protection scanner](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner) (Automatizzazione della protezione dei dati con lo scanner di Azure Information Protection).

Ci si potrebbe chiedere: [Qual è la differenza tra il cluster di failover di Windows Server e il Azure Information Protection scanner?](faqs-classic.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

È anche possibile usare PowerShell per classificare e proteggere in modo interattivo i file dal computer desktop. Per altre informazioni su questo e altri scenari che usano PowerShell, vedere [Uso di PowerShell con il client Azure Information Protection](./rms-client/client-admin-guide-powershell.md).