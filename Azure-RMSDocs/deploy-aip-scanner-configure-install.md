---
title: Installare e configurare lo scanner di etichettatura unificata di Azure Information Protection (AIP)
description: Istruzioni per l'installazione e la configurazione del Azure Information Protection scanner unificato di etichette per individuare, classificare e proteggere i file negli archivi dati.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: scanner
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: e6e90124dfae07e4ccc02a1d047fc15627b7b35f
ms.sourcegitcommit: 3780bd234c0af60d4376f1cae093b8b0ab035a9f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/09/2020
ms.locfileid: "95568479"
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

Prima di installare lo scanner o aggiornarlo da una versione di disponibilità generale precedente, configurare o verificare le impostazioni dello scanner nell'area Azure Information Protection della portale di Azure.

Per configurare lo scanner: 

1. Accedere al [portale di Azure](https://portal.azure.com) con uno dei ruoli seguenti:

    - **Amministratore di conformità**
    - **Amministratore dati di conformità**
    - **Amministratore della sicurezza**
    - **Amministratore globale**

    Quindi, passare al riquadro **Azure Information Protection** .
    
    Ad esempio, nella casella di ricerca di risorse, servizi e documenti iniziare a digitare **Information** e selezionare **Azure Information Protection**.

1. [Creare un cluster di scanner](#create-a-scanner-cluster). Questo cluster definisce lo scanner e viene usato per identificare l'istanza dello scanner, ad esempio durante l'installazione, gli aggiornamenti e altri processi.

1. Opzionale [Eseguire la scansione della rete per verificare la presenza di repository rischiosi](#create-a-network-scan-job-public-preview). Creare un processo di analisi di rete per analizzare un intervallo o un indirizzo IP specificato e fornire un elenco di repository rischiosi che potrebbero contenere contenuto sensibile che si vuole proteggere.  

    Eseguire il processo di analisi della rete e quindi [analizzare eventuali repository rischiosi trovati](#analyze-risky-repositories-found-public-preview).

1. [Creare un processo di analisi del contenuto](#create-a-content-scan-job) per definire i repository che si desidera analizzare.

### <a name="create-a-scanner-cluster"></a>Creare un cluster di scanner  

1. Dal menu **scanner** a **sinistra selezionare Clusters** ![icona Clusters](media/i-clusters.png "icona cluster").

1. Nel riquadro **Azure Information Protection-cluster** selezionare **Aggiungi** ![icona Aggiungi](media/i-add.png "icona Aggiungi").
    
1. Nel riquadro **Aggiungi nuovo cluster** immettere un nome significativo per lo scanner e una descrizione facoltativa. 
    
    Il nome del cluster viene usato per identificare le configurazioni e i repository dello scanner. Ad esempio, è possibile immettere **Europa** per identificare le posizioni geografiche dei repository di dati che si desidera analizzare. 

    Questo nome verrà usato in un secondo momento per identificare la posizione in cui si vuole installare o aggiornare lo scanner.

1. Selezionare **Salva** ![icona](media/qs-tutor/save-icon.png "icona Salva") Salva per salvare le modifiche.

### <a name="create-a-network-scan-job-public-preview"></a>Creare un processo di analisi di rete (anteprima pubblica)

A partire dalla versione [2.8.85.0](rms-client/unifiedlabelingclient-version-release-history.md#version-28850), è possibile analizzare la rete per i repository rischiosi. Aggiungere uno o più repository trovati a un processo di analisi del contenuto per analizzarli per verificare la presenza di contenuto sensibile.

- [Prerequisiti per l'individuazione della rete](#network-discovery-prerequisites)
- [Creazione di un processo di analisi di rete](#creating-a-network-scan-job)

> [!NOTE]
> La funzionalità di individuazione della rete Azure Information Protection è attualmente disponibile in anteprima. Le [condizioni aggiuntive per l'anteprima di Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) includono termini legali aggiuntivi che si applicano a funzionalità di Azure in versione beta, anteprima o diversamente non ancora disponibili a livello generale. 
> 

#### <a name="network-discovery-prerequisites"></a>Prerequisiti per l'individuazione della rete

|Prerequisito  |Descrizione  |
|---------|---------|
|**Installare il servizio di individuazione della rete**     |   Se è stato aggiornato di recente lo scanner, potrebbe essere necessario installare anche il servizio di individuazione della rete. <br /><br />Eseguire il cmdlet [**Install-MIPNetworkDiscovery**](/powershell/module/azureinformationprotection/Install-MIPNetworkDiscovery) per abilitare i processi di analisi di rete.      |
|**Analisi Azure Information Protection**     | Assicurarsi di aver abilitato Azure Information Protection Analytics. <br /><br />Nella portale di Azure passare a **Azure Information Protection > gestisci > Configura analisi (anteprima).** <br /><br />Per ulteriori informazioni, vedere [la pagina relativa alla creazione di report centrali per Azure Information Protection (anteprima pubblica)](reports-aip.md).|
| | |

#### <a name="creating-a-network-scan-job"></a>Creazione di un processo di analisi di rete

1. Accedere al portale di Azure e passare a **Azure Information Protection.** Nel menu **scanner** a sinistra selezionare l'icona processi di **analisi di rete (anteprima)** ![processi di analisi di rete](media/i-network-scan-jobs.png "icona dei processi di analisi di rete").
    
1. Nel riquadro **processi di analisi di rete Azure Information Protection** selezionare **Aggiungi** ![icona](media/i-add.png "icona Aggiungi")Aggiungi.
    
1. Nella pagina **Aggiungi un nuovo processo di analisi di rete** definire le impostazioni seguenti:
        
    |Impostazione  |Descrizione  |
    |---------|---------|
    |**Nome del processo di analisi di rete**     |Immettere un nome significativo per questo processo.  Questo campo è obbligatorio.       |
    |**Descrizione**     |   Immettere una descrizione significativa.      |
    |**Selezionare il cluster**     |Nell'elenco a discesa selezionare il cluster che si vuole usare per analizzare i percorsi di rete configurati.  <br /><br />**Suggerimento:** Quando si seleziona un cluster, assicurarsi che i nodi del cluster assegnati possano accedere agli intervalli di indirizzi IP configurati tramite SMB.      |
    |**Configura gli intervalli IP da individuare**     |   Fare clic per definire un intervallo o un indirizzo IP. <br /><br />Nel riquadro **Scegli intervalli IP** immettere un nome facoltativo, quindi un indirizzo IP iniziale e un indirizzo IP finale per l'intervallo. <br /><br />**Suggerimento:** Per eseguire la scansione solo di un indirizzo IP specifico, immettere l'indirizzo IP identico in entrambi i campi indirizzo IP **iniziale** e indirizzo IP **finale** .      |
    |**Imposta la pianificazione**     | Definire la frequenza con cui si vuole eseguire questo processo di analisi di rete.  <br /><br />Se si seleziona **settimanale**, viene visualizzata l'impostazione **Esegui processo di analisi di rete in** . Consente di selezionare i giorni della settimana in cui si desidera eseguire il processo di analisi della rete.       |
    |**Imposta l'ora di inizio (UTC)**     |Definire la data e l'ora in cui si vuole avviare l'esecuzione del processo di analisi di rete. Se si è scelto di eseguire il processo ogni giorno, ogni settimana o ogni mese, il processo viene eseguito all'ora definita, in corrispondenza della ricorrenza selezionata. <br /><br />**Nota**: prestare attenzione quando si imposta la data su qualsiasi giorno alla fine del mese. Se si seleziona **31,** il processo di analisi di rete non viene eseguito in un mese con un massimo di 30 giorni.    |
    | | |

1. Selezionare **Salva** ![icona](media/qs-tutor/save-icon.png "icona Salva") Salva per salvare le modifiche.

> [!TIP]
> Se si desidera eseguire la stessa analisi di rete utilizzando un altro scanner, modificare il cluster definito nel processo di analisi di rete.
> 
> Tornare al riquadro **processi di analisi di rete** e selezionare **assegna a cluster** per selezionare un cluster diverso o annullare l' **assegnazione del cluster** per apportare ulteriori modifiche in un secondo momento. 
>     

### <a name="analyze-risky-repositories-found-public-preview"></a>Analizza i repository rischiosi trovati (anteprima pubblica)

I repository trovati, da un processo di analisi di rete, da un processo di analisi del contenuto o dall'accesso utente rilevato nei file di log, vengono aggregati ed elencati nel riquadro [icona](media/i-repositories.png "icona repository") **dello scanner >** repository dei repository.

Se è stato [definito un processo di analisi di rete](#create-a-network-scan-job-public-preview) che è stato impostato per l'esecuzione in una data e a un orario specifici, attendere il completamento dell'esecuzione per verificare i risultati. È anche possibile tornare qui dopo l'esecuzione di un [processo di analisi del contenuto](#create-a-content-scan-job) per visualizzare i dati aggiornati.

> [!NOTE]
> La funzionalità **repository** Azure Information Protection è attualmente in fase di anteprima. Le [condizioni aggiuntive per l'anteprima di Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) includono termini legali aggiuntivi che si applicano a funzionalità di Azure in versione beta, anteprima o diversamente non ancora disponibili a livello generale. 
> 

1. Nel menu **scanner** a sinistra selezionare **repository repository** ![icona](media/i-repositories.png "icona repository").
    
    I repository trovati vengono visualizzati come segue:
    - Il grafico **repository per stato** Mostra il numero di repository già configurati per un processo di analisi del contenuto e il numero di repository che non lo sono.
    - Il grafico dei **primi 10 repository non gestiti per accesso** elenca i primi 10 repository che non sono attualmente assegnati a un processo di analisi del contenuto, oltre a dettagli relativi ai livelli di accesso. I livelli di accesso possono indicare la pericolosità dei repository.
    - La tabella sotto i grafici elenca ogni repository trovato e i relativi dettagli.

1. Eseguire una di queste operazioni:
    
    |Opzione  |Descrizione  |
    |---------|---------|
    |![icona colonne](media/i-columns.png "icona colonne")    | Selezionare le **colonne** per modificare le colonne della tabella visualizzate.        |
    |![icona di aggiornamento](media/i-refresh.png "icona di aggiornamento")   | Se lo scanner ha eseguito di recente i risultati dell'analisi di rete, selezionare **Aggiorna** per aggiornare la pagina.      |
    |![icona Aggiungi](media/i-add.png "icona Aggiungi")   | Selezionare uno o più repository elencati nella tabella e quindi selezionare **assegna elementi selezionati** per assegnarli a un processo di analisi del contenuto.          |
    |**Filter**     |   La riga filtro Mostra tutti i criteri di filtro attualmente applicati. Selezionare uno dei criteri mostrati per modificarne le impostazioni oppure selezionare **Aggiungi filtro** per aggiungere nuovi criteri di filtro. <br /><br />Selezionare **filtro** per applicare le modifiche e aggiornare la tabella con il filtro aggiornato.       |
    |![Icona Log Analytics](media/i-log-analytics.png "Icona Log Analytics") |Nell'angolo in alto a destra del grafico repository non gestiti fare clic sull'icona **log Analytics** per passare a log Analytics dati per questi repository. |
    | | |

#### <a name="repositories-with-public-access"></a>Repository con accesso pubblico

I repository in cui si trova **l'accesso pubblico** hanno funzionalità di **lettura** o di **lettura/scrittura** possono includere contenuti sensibili che devono essere protetti. Se l' **accesso pubblico** è false, il repository non è accessibile dal pubblico.

L'accesso pubblico a un repository viene segnalato solo se è stato impostato un account vulnerabile nel parametro **StandardDomainsUserAccount** del cmdlet [**Install-MIPNetworkDiscovery**](/powershell/module/azureinformationprotection/Install-MIPNetworkDiscovery) .

- Gli account definiti in questi parametri vengono usati per simulare l'accesso di un utente debole al repository. Se l'utente debole definito può accedere al repository, significa che è possibile accedere pubblicamente al repository. 

- Per assicurarsi che l'accesso pubblico venga segnalato correttamente, assicurarsi che l'utente specificato in questi parametri sia un membro del gruppo **Domain Users** .
       
### <a name="create-a-content-scan-job"></a>Creazione di un processo di analisi del contenuto

Approfondimento sui contenuti per analizzare i repository specifici per il contenuto sensibile. 

Questa operazione può essere eseguita solo dopo l'esecuzione di un processo di analisi di rete per analizzare i repository nella rete, ma può anche definire autonomamente i repository.
 
1. Nel menu **scanner** a sinistra selezionare **processi di analisi del contenuto**. 
   
1. Nel riquadro **processi di analisi del Azure Information Protection di contenuto** selezionare **Aggiungi** ![icona](media/i-add.png "icona Salva")Aggiungi.
 
1. Per questa configurazione iniziale, configurare le impostazioni seguenti e quindi selezionare **Salva** senza chiudere il riquadro.
    
    |Impostazione  |Descrizione  |
    |---------|---------|
    |**Impostazioni del processo di analisi del contenuto**     |    - **Pianificazione**: Mantieni il valore predefinito **manuale** <br />- **Tipi di informazioni da** individuare: modificare **solo i criteri** <br />- **Configurare i repository**: non configurare in questo momento perché è necessario salvare prima il processo di analisi del contenuto.         |
    |**Applicazione dei criteri**     | - **Imponi**: seleziona **disattivato** <br />- **Etichettare i file in base al contenuto**: Mantieni il valore predefinito **in** <br />- **Etichetta predefinita**: Mantieni il valore predefinito dei **criteri predefiniti** <br />- Modifica **etichette file**: Mantieni il valore predefinito **off**        |
    |**Configurare le impostazioni del file**     | - **Mantieni "Data modifica", "Ultima modifica" e "modificato da"**: Mantieni il valore predefinito **in** <br />- **Tipi di file da analizzare**: Mantieni i tipi di file predefiniti per l' **esclusione** <br />- **Proprietario predefinito**: Mantieni il valore predefinito dell' **account scanner**        |
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
    
        
        - Per una condivisione di rete, usare `\\Server\Folder` . 
        - Per una raccolta di SharePoint, usare `http://sharepoint.contoso.com/Shared%20Documents/Folder` .
        - Per un percorso locale: `C:\Folder`
        - Per un percorso UNC: `\\Server\Folder`

    > [!NOTE]
    > I caratteri jolly e i percorsi WebDav non sono supportati.
    >  
  
    Se si aggiunge un percorso di SharePoint per i **documenti condivisi**:
    - Specificare **Documenti condivisi** nel percorso quando si vogliono analizzare tutti i documenti e tutte le cartelle da Documenti condivisi. 
    ad esempio `http://sp2013/SharedDocuments`
    - Specificare **Documenti** nel percorso quando si vogliono analizzare tutti i documenti e tutte le cartelle da una sottocartella in Documenti condivisi. 
    ad esempio `http://sp2013/Documents/SalesReports`
    - In alternativa, specificare solo il **nome di dominio completo (FQDN** ) di SharePoint, ad esempio `http://sp2013` per [individuare e analizzare tutti i siti e i siti Web di SharePoint in un URL](deploy-aip-scanner-prereqs.md#discover-and-scan-all-sharepoint-sites-and-subsites-under-a-specific-url) e sottotitoli specifici in questo URL. Concedere i diritti dell' **agente di raccolta siti** scanner per abilitare questa operazione. 
    >


    Per le impostazioni rimanenti di questo riquadro, non modificarle per questa configurazione iniziale, ma mantenerle come **predefinite del processo di analisi del contenuto**. L'impostazione predefinita indica che il repository dei dati eredita le impostazioni dal processo di analisi del contenuto.

    Quando si aggiungono i percorsi di SharePoint, utilizzare la sintassi seguente:
    
    |Percorso  |Sintassi  |
    |---------|---------|
    |**Percorso radice**     | `http://<SharePoint server name>` <br /><br />Analizza tutti i siti, incluse le raccolte siti consentite per l'utente dello scanner. <br />Richiede [autorizzazioni aggiuntive](quickstart-findsensitiveinfo.md#permission-users-to-scan-sharepoint-repositories) per individuare automaticamente il contenuto radice        |
    |**Raccolta o sito secondario di SharePoint specifico**     | I tipi validi sono: <br />- `http://<SharePoint server name>/<subsite name>` <br />- `http://SharePoint server name>/<site collection name>/<site name>` <br /><br />Richiede [autorizzazioni aggiuntive](quickstart-findsensitiveinfo.md#permission-users-to-scan-sharepoint-repositories) per individuare automaticamente il contenuto della raccolta siti         |
    |**Raccolta di SharePoint specifica**     | I tipi validi sono: <br />- `http://<SharePoint server name>/<library name>` <br />- `http://SharePoint server name>/.../<library name>`       |
    |**Cartella di SharePoint specifica**     | `http://<SharePoint server name>/.../<folder name>`        |
    

1. Ripetere i passaggi precedenti per aggiungere tutti i repository necessari.

    Al termine, chiudere i riquadri **repository** e processo di **analisi del contenuto** . 

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

Un token di Azure AD consente allo scanner di eseguire l'autenticazione al servizio Azure Information Protection, consentendo allo scanner di eseguire in modo non interattivo.

Per altre informazioni, vedere [Come assegnare un'etichetta ai file in modo non interattivo per Azure Information Protection](./rms-client/clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection).

Per ottenere un token di Azure AD:

1. Tornare alla portale di Azure per creare un'applicazione Azure AD per specificare un token di accesso per l'autenticazione.

1. Dal computer Windows Server, se all'account del servizio di scanner è stato concesso il diritto di **accesso locale** per l'installazione, accedere con questo account e avviare una sessione di PowerShell. 

    Eseguire [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) specificando i valori copiati nel passaggio precedente:
    
    ```PowerShell
    Set-AIPAuthentication -AppId <ID of the registered app> -AppSecret <client secret sting> -TenantId <your tenant ID> -DelegatedUser <Azure AD account>
    ```
        
    Ad esempio:

    ```PowerShell
    $pscreds = Get-Credential CONTOSO\scanner
    Set-AIPAuthentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -DelegatedUser scanner@contoso.com -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -OnBehalfOf $pscreds
    Acquired application access token on behalf of CONTOSO\scanner.
    ```

> [!TIP]
> Se all'account del servizio scanner non è possibile concedere il diritto di **accesso locale** per l'installazione, usare il parametro *OnBehalfOf* con [set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication), come descritto in [come etichettare i file in modo non interattivo per Azure Information Protection](./rms-client//clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection).

Lo scanner dispone ora di un token per l'autenticazione in Azure AD. Questo token è valido per un anno, due anni o mai, in base alla configurazione del segreto client di/API per l' **app Web** in Azure ad. 

Quando il token scade, è necessario ripetere questa procedura.

Si è ora pronti per eseguire la prima analisi in modalità di individuazione. Per altre informazioni, vedere [eseguire un ciclo di individuazione e visualizzare i report per lo scanner](deploy-aip-scanner-manage.md#run-a-discovery-cycle-and-view-reports-for-the-scanner).

Dopo aver eseguito l'analisi iniziale dell'individuazione, continuare con [configurare lo scanner per applicare la classificazione e la protezione](#configure-the-scanner-to-apply-classification-and-protection).

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
    
    ```PowerShell
    Start-AIPScan
    ```

Lo scanner è ora pianificato per l'esecuzione continua. Quando lo scanner funziona in tutti i file configurati, avvia automaticamente un nuovo ciclo in modo che vengano individuati tutti i file nuovi e modificati.

## <a name="change-which-file-types-to-protect"></a>Modificare i tipi di file da proteggere

Per impostazione predefinita, lo scanner AIP protegge solo i tipi di file di Office e i file PDF.

Usare i comandi di PowerShell per modificare questo comportamento in base alle esigenze, ad esempio per configurare lo scanner in modo da proteggere tutti i tipi di file, come per il client o per proteggere altri tipi di file specifici. 

Per un criterio etichetta applicabile all'account utente che Scarica le etichette per lo scanner, specificare un'impostazione avanzata di PowerShell denominata **PFileSupportedExtensions**. 

Per uno scanner con accesso a Internet, questo account utente è l'account specificato per il parametro *DelegatedUser* con il comando Set-AIPAuthentication.

**Esempio 1:**  Comando di PowerShell per lo scanner per proteggere tutti i tipi di file, in cui il criterio dell'etichetta è denominato "scanner":

```PowerShell
Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions="*"}
```

**Esempio 2:** Comando di PowerShell per lo scanner per proteggere i file con estensione XML e i file TIFF oltre ai file di Office e PDF, in cui il criterio dell'etichetta è denominato "scanner":

```PowerShell
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

|Opzione  |Descrizione  |
|---------|---------|
|**Disporre di una connessione di rete ad alta velocità e affidabile tra il computer dello scanner e l'archivio dei dati analizzati**     |  Ad esempio, posizionare il computer dello scanner nella stessa LAN o preferibilmente nello stesso segmento di rete dell'archivio dati scansionato. <br /><br />La qualità della connessione di rete influiscono sulle prestazioni dello scanner perché, per esaminare i file, lo scanner trasferisce il contenuto dei file nel computer in cui è in esecuzione il servizio scanner. <br /><br />Riducendo o eliminando gli hop di rete necessari per i dati da spostare, viene ridotto anche il carico sulla rete.      |
|**Verificare che il computer dello scanner abbia risorse del processore disponibili**     | Esaminare il contenuto del file e crittografare e decrittografare i file sono azioni che richiedono un utilizzo intensivo del processore. <br /><br />Monitorare i cicli di analisi tipici degli archivi dati specificati per identificare se le risorse del processore influiscono negativamente sulle prestazioni dello scanner.        |
|**Installare più istanze dello scanner** | Lo scanner Azure Information Protection supporta più database di configurazione nella stessa istanza di SQL Server quando si specifica un nome di cluster personalizzato (profilo) per lo scanner. <br /><br />Più scanner possono inoltre condividere lo stesso cluster (profilo), ottenendo tempi di analisi più rapidi.|
|**Controllare l'utilizzo della configurazione alternativa** |L'esecuzione dello scanner è più rapida quando si usa la [configurazione alternativa](#using-the-scanner-with-alternative-configurations) per applicare un'etichetta predefinita a tutti i file in quanto lo scanner non esamina i contenuti del file. <br/><br />L'esecuzione dello scanner è più lenta quando si usa la [configurazione alternativa](#using-the-scanner-with-alternative-configurations) per identificare tutte le condizioni personalizzate e i tipi di informazioni riservate noti.|
| | |


### <a name="additional-factors-that-affect-performance"></a>Fattori aggiuntivi che influiscono sulle prestazioni

Ulteriori fattori che influiscono sulle prestazioni dello scanner includono:

|Fattore  |Descrizione  |
|---------|---------|
|**Tempi di caricamento/risposta**     |Anche i tempi di caricamento e di risposta correnti degli archivi dati che contengono i file da analizzare influiscono sulle prestazioni dello scanner.         |
|**Modalità scanner** (individuazione/applicazione)    | La modalità di individuazione ha in genere una velocità di analisi superiore rispetto alla modalità di applicazione. <br /><br />Per l'individuazione è necessaria un'azione di lettura di un singolo file, mentre la modalità di applicazione richiede azioni di lettura e scrittura.        |
|**Modifiche dei criteri**     |È possibile che le prestazioni dello scanner siano invariate se sono state apportate modifiche all'etichettatura automatica nei criteri etichetta. <br /><br />Il primo ciclo di analisi, quando lo scanner deve controllare tutti i file, avrà più tempo dei cicli di analisi successivi che, per impostazione predefinita, ispeziona solo i file nuovi e modificati. <br /><br />Se si modificano le condizioni o le impostazioni di etichetta automatica, tutti i file vengono nuovamente sottoposti a scansione. Per ulteriori informazioni, vedere ripetizione dell' [analisi dei file](deploy-aip-scanner-manage.md#rescanning-files).|
|**Costruzioni Regex**    | Le prestazioni dello scanner sono influenzate dal modo in cui vengono costruite le espressioni Regex per le condizioni personalizzate. <br /><br /> Per evitare un consumo intenso di memoria e il rischio di timeout (15 minuti per ogni file), rivedere le espressioni regex per assicurarsi che usino criteri di ricerca efficienti. <br /><br />Ad esempio: <br />-Evitare [quantificatori greedy](/dotnet/standard/base-types/quantifiers-in-regular-expressions) <br />-Usare gruppi non di acquisizione come `(?:expression)` anziché `(expression)`    |
|**Livello di log**     |  Le opzioni a livello di log includono **debug**, **info**, **Error** e **off** per i report dello scanner.<br /><br />- **Risultati migliori** prestazioni <br />- Il **debug** rallenta notevolmente lo scanner e deve essere usato solo per la risoluzione dei problemi. <br /><br />Per altre informazioni, vedere il parametro *ReportLevel* del cmdlet [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration).       |
|**File sottoposti a scansione**     |-Ad eccezione dei file di Excel, i file di Office vengono analizzati più rapidamente rispetto ai file PDF. <br /><br />-I file non protetti sono più veloci da analizzare rispetto ai file protetti. <br /><br />-I file di grandi dimensioni hanno ovviamente più tempo per l'analisi di file di piccole dimensioni.         |
| | |

## <a name="list-of-cmdlets-for-the-scanner"></a>Elenco dei cmdlet per lo scanner

Questa sezione elenca i cmdlet di PowerShell supportati per lo scanner Azure Information Protection.

> [!NOTE]
> Lo scanner Azure Information Protection viene configurato dal portale di Azure. Pertanto, i cmdlet usati nelle versioni precedenti per configurare i repository dei dati e l'elenco dei tipi di file analizzati sono ora deprecati.
> 

I cmdlet supportati per lo scanner includono:

- [Export-AIPLogs](/powershell/module/azureinformationprotection/Export-AIPLogs)

- [Get-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Get-AIPScannerConfiguration)

- [Get-AIPScannerStatus](/powershell/module/azureinformationprotection/Get-AIPScannerStatus)

- [Get-MIPNetworkDiscoveryConfiguration](/powershell/module/azureinformationprotection/Get-MIPNetworkDiscoveryConfiguration)

- [Get-MIPNetworkDiscoveryJobs](/powershell/module/azureinformationprotection/Get-MIPNetworkDiscoveryJobs)

- [Get-MIPNetworkDiscoveryStatus](/powershell/module/azureinformationprotection/Get-MIPNetworkDiscoveryStatus)

- [Import-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Import-AIPScannerConfiguration)

- [Import-MIPNetworkDiscoveryConfiguration](/powershell/module/azureinformationprotection/Import-MIPNetworkDiscoveryConfiguration)

- [Install-AIPScanner](/powershell/module/azureinformationprotection/Install-AIPScanner)

- [Install-MIPNetworkDiscovery](/powershell/module/azureinformationprotection/Install-MIPNetworkDiscovery)

- [Set-AIPScanner](/powershell/module/azureinformationprotection/Set-AIPScanner)

- [Set-AIPScannerConfiguration](/powershell/module/azureinformationprotection/Set-AIPScannerConfiguration)

- [Set-MIPNetworkDiscoveryConfiguration](/powershell/module/azureinformationprotection/Set-MIPNetworkDiscoveryConfiguration)

- [Start-AIPScan](/powershell/module/azureinformationprotection/Start-AIPScan)

- [Start-AIPScanDiagnostics](/powershell/module/azureinformationprotection/Start-AIPScannerDiagnostics)

- [Start-MIPNetworkDiscovery](/powershell/module/azureinformationprotection/Start-MIPNetworkDiscovery)

- [Stop-AIPScan](/powershell/module/azureinformationprotection/Stop-AIPScan)

- [Uninstall-AIPScanner](/powershell/module/azureinformationprotection/Uninstall-AIPScanner)

- [Uninstall-MIPNetworkDiscovery](/powershell/module/azureinformationprotection/Uninstall-MIPNetworkDiscovery)

- [Update-AIPScanner](/powershell/module/azureinformationprotection/Update-AIPScanner)

## <a name="next-steps"></a>Passaggi successivi

Dopo aver installato e configurato lo scanner, avviare [l'analisi dei file](deploy-aip-scanner-manage.md).

Vedere anche: [distribuzione di Azure Information Protection scanner per classificare e proteggere automaticamente i file](deploy-aip-scanner.md).

**Ulteriori informazioni:**

- Se si è interessati a scoprire come è stato implementato questo scanner dai team Microsoft Core Services Engineering e Operations,  leggere il case study tecnico: [Automating data protection with Azure Information Protection scanner](https://www.microsoft.com/itshowcase/Article/Content/1070/Automating-data-protection-with-Azure-Information-Protection-scanner) (Automatizzazione della protezione dei dati con lo scanner di Azure Information Protection).

- Ci si potrebbe chiedere: [Qual è la differenza tra il cluster di failover di Windows Server e il Azure Information Protection scanner?](faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)

- Usare PowerShell per classificare e proteggere in modo interattivo i file dal computer desktop. Per altre informazioni su questo e altri scenari in cui viene usato PowerShell, vedere [uso di PowerShell con il Azure Information Protection Unified Labeling client](./rms-client/clientv2-admin-guide-powershell.md).