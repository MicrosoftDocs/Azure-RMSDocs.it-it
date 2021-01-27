---
title: Configurare i server per il connettore di Rights Management - AIP
description: Informazioni per configurare i server locali che sfrutteranno il connettore di Azure Rights Management (RMS). Queste procedure illustrano il passaggio 5 di Distribuzione del connettore di Azure Rights Management.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 09/10/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 75846ee1-2370-4360-81ad-e2b6afe3ebc9
ms.subservice: connector
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: e07d4f634d774be91df03c279705f52e9bee6c8c
ms.sourcegitcommit: f6d536b6a3b5e14e24f0b9e58d17a3136810213b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98809669"
---
# <a name="configuring-servers-for-the-azure-rights-management-connector"></a>Configurazione dei server per il connettore di Azure Rights Management

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 *
>
>***Rilevante per**: [Client di etichettatura unificata e client classico di AIP](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Usare le informazioni seguenti per configurare il server locale che sfrutterà il connettore di Azure Rights Management (RMS). Queste procedure illustrano il passaggio 5 della [distribuzione del connettore Azure Rights Management](deploy-rms-connector.md).

**Prerequisiti**: prima di iniziare, verificare di avere:
    - Installato e configurato il connettore RMS
    - Verifica dei [prerequisiti](deploy-rms-connector.md#prerequisites-for-the-rms-connector) pertinenti per i server che utilizzeranno il connettore.

## <a name="configuring-servers-to-use-the-rms-connector"></a>Configurazione dei server per l'uso del connettore RMS
Dopo aver installato e configurato il connettore RMS, è possibile configurare i server locali che si connetteranno al servizio Azure Rights Management e usare questa tecnologia di protezione usando il connettore. 

È necessario configurare i server seguenti:

|Ambiente  |Server da configurare  |
|---------|---------|
|**Exchange 2016 ed Exchange 2013**     |  server Accesso client e server Cassette postali       |
|**Exchange 2019**     |   server Accesso client e server Trasporto hub      |
|**SharePoint**     |    server Web front-end di SharePoint, inclusi quelli che ospitano il server Amministrazione centrale     |
|**Infrastruttura di classificazione file**     |   computer Windows Server in cui è installato File Resource Manager      |
| | |

Questa configurazione richiede impostazioni del registro di sistema, con le opzioni seguenti:

- [Modificare automaticamente le impostazioni del registro di sistema](#edit-registry-settings-automatically---advantages-and-disadvantages)
- [Modificare manualmente le impostazioni del registro di sistema](#edit-registry-settings-manually---advantages-and-disadvantages)

> [!IMPORTANT]
> In entrambi i casi, è necessario installare manualmente i prerequisiti e configurare Exchange, SharePoint e Infrastruttura di classificazione file per l'uso di Rights Management.

> [!NOTE]
> Per la maggior parte delle organizzazioni, la configurazione automatica mediante lo strumento di configurazione server per il connettore Microsoft RMS è l'opzione più conveniente poiché assicura livelli di efficienza e affidabilità più elevati rispetto alla configurazione manuale.
> 

Dopo aver apportato le modifiche alla configurazione in questi server, è necessario riavviarli se eseguono Exchange o SharePoint e sono stati configurati in precedenza per utilizzare AD RMS. Il riavvio di questi server non è necessario se vengono configurati per Rights Management per la prima volta. 

Dopo aver apportato queste modifiche alla configurazione, è sempre necessario riavviare il file server configurato per l'uso di Infrastruttura di classificazione file.
### <a name="edit-registry-settings-automatically---advantages-and-disadvantages"></a>Modificare automaticamente le impostazioni del registro di sistema: vantaggi e svantaggi

Modificare automaticamente le impostazioni del registro di sistema, usando lo strumento di configurazione server per il connettore Microsoft RMS.

I **vantaggi includono**:

- Non è necessario modificare direttamente il Registro di sistema. Le modifiche necessarie vengono apportate automaticamente mediante uno script.

- Non è necessario eseguire un cmdlet di Windows PowerShell per ottenere l'URL di Microsoft RMS.

- Se si esegue lo strumento in locale, i prerequisiti vengono verificati automaticamente (le correzioni eventualmente necessarie, tuttavia, non vengono eseguite automaticamente).

Gli **svantaggi includono**: quando si esegue lo strumento, è necessario effettuare una connessione a un server in cui è già in esecuzione il connettore RMS.

Per altre informazioni, vedere [come usare lo strumento di configurazione server per il connettore Microsoft RMS](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector).
### <a name="edit-registry-settings-manually---advantages-and-disadvantages"></a>Modificare manualmente le impostazioni del registro di sistema: vantaggi e svantaggi

I **vantaggi includono**: non è necessaria alcuna connettività a un server che esegue il connettore RMS.

Gli **svantaggi includono**:

- Si verifica un sovraccarico amministrativo, con aumentata possibilità di errore.

- È necessario ottenere l'URL di Microsoft RMS, operazione che richiede l'esecuzione di un comando di Windows PowerShell.

- È necessario controllare manualmente tutti i prerequisiti.

### <a name="how-to-use-the-server-configuration-tool-for-microsoft-rms-connector"></a>Come usare lo strumento di configurazione server per il connettore Microsoft RMS

1.  Se non è stato ancora scaricato lo script per lo strumento di configurazione server per il connettore Microsoft RMS **(GenConnectorConfig.ps1)**, scaricarlo dall' [area download Microsoft](https://go.microsoft.com/fwlink/?LinkId=314106).

2.  Salvare il file di **GenConnectorConfig.ps1** nel computer in cui verrà eseguito lo strumento. 

    Se lo strumento viene eseguito localmente, il file deve essere salvato sul server che si desidera configurare per comunicare con il connettore RMS. In caso contrario, è possibile salvare il file su qualsiasi computer.

3.  Stabilire la modalità di esecuzione dello strumento:
    
    |Metodo  |Descrizione  |
    |---------|---------|
    |**In locale**     |  Eseguire lo strumento in modo interattivo, dal server da configurare per comunicare con il connettore RMS. <br><br>**Suggerimento**: questa operazione è utile per una configurazione unica, ad esempio un ambiente di testing.       |
    |**Distribuzione software**     |  Eseguire lo strumento per generare i file del registro di sistema, che vengono quindi distribuiti in uno o più server rilevanti. <br><br>Distribuire i file del registro di sistema usando un'applicazione di gestione dei sistemi che supporta la distribuzione del software, ad esempio System Center Configuration Manager.       |
    |**Criteri di gruppo**     | Eseguire lo strumento per produrre uno script da assegnare a un amministratore che può creare oggetti Criteri di gruppo per i server da configurare. <br><br>Questo script crea un oggetto Criteri di gruppo per ciascun tipo di server da configurare. L'amministratore può quindi assegnare l'oggetto corretto ai server pertinenti.        |
    | | |

    > [!NOTE]
    > Questo strumento consente di configurare i server che comunicheranno con il connettore RMS e che sono elencati all'inizio di questa sezione. Non eseguire questo strumento sui server che eseguono il connettore RMS.

4.  Avviare Windows PowerShell con l'opzione **Esegui come amministratore** e usare il comando **Get-Help** per leggere le istruzioni su come usare lo strumento per il metodo di configurazione scelto:

    ```PowerShell
    Get-help .\GenConnectorConfig.ps1 -detailed
    ```

Per eseguire lo script è necessario immettere l'URL del connettore RMS dell'organizzazione. 

Immettere il prefisso del protocollo (HTTP:// o HTTPS://) e il nome del connettore definito nel DNS per l'indirizzo di bilanciamento del carico del connettore stesso, Ad esempio: `https:\//connector.contoso.com`. 

Lo strumento usa quindi tale URL per contattare i server che eseguono il connettore RMS e ottenere altri parametri usati per creare le configurazioni richieste.

> [!IMPORTANT]
> Quando si esegue questo strumento, assicurarsi di specificare il nome del connettore RMS con carico bilanciato per l'organizzazione e non il nome di un singolo server che esegue il servizio del connettore RMS.

Nelle sezioni seguenti sono disponibili informazioni specifiche per ciascun tipo di servizio:

-   [Configurazione di un server di Exchange per l'uso del connettore](#configuring-an-exchange-server-to-use-the-connector)

-   [Configurazione di un server SharePoint per l'uso del connettore](#configuring-a-sharepoint-server-to-use-the-connector)

-   [Configurazione di un file server per l'infrastruttura di classificazione file per l'uso del connettore](#configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector)

**Quando installare le applicazioni client in computer distinti, che non sono configurati per l'uso del connettore**

Dopo aver configurato questi server per l'uso del connettore, è possibile che le applicazioni client installate in locale su tali server non siano in grado di funzionare con RMS. Questo inconveniente si verifica perché le applicazioni tentano di usare il connettore anziché usare direttamente RMS.

Inoltre, se Office 2010 è installato localmente in un server Exchange, le funzionalità IRM dell'app client potrebbero funzionare da tale computer dopo che il server è stato configurato per l'uso del connettore, ma questa operazione non è supportata. 

In entrambi gli scenari, è necessario installare le applicazioni client in computer separati non configurati per l'uso del connettore. Tali computer useranno quindi RMS direttamente.

> [!IMPORTANT]
> Supporto "Extended" per Office 2010 terminato il 13 ottobre 2020. Per altre informazioni, vedere [AIP e versioni legacy di Windows e Office](known-issues.md#aip-and-legacy-windows-and-office-versions).
> 
## <a name="configuring-an-exchange-server-to-use-the-connector"></a>Configurazione di un server di Exchange per l'uso del connettore
I seguenti ruoli di Exchange comunicano con il connettore RMS:

-   Per Exchange 2016 ed Exchange 2013: server Accesso client e server Cassette postali

-   Per Exchange 2019: server Accesso client e server Trasporto Hub

Per usare un connettore RMS, è necessario che i server di Exchange eseguano una delle versioni seguenti del software:

-   Exchange Server 2016

-   Exchange Server 2013 con aggiornamento cumulativo 3

-   Exchange Server 2019

È anche necessario che sui server sia disponibile una versione 1 del client RMS (noto anche come MSDRM) con supporto per la modalità di crittografia RMS 2. Il client MSDRM è incluso in tutti i sistemi operativi Windows, ma le prime versioni del client non supportano la modalità di crittografia 2. Se i server Exchange in uso eseguono Windows Server 2012 o versioni successive, non sono necessarie azioni aggiuntive poiché il client RMS installato in questi sistemi operativi supporta in modo nativo la modalità di crittografia 2. 


> [!IMPORTANT]
> Se non sono state installate queste versioni (o versioni successive) di Exchange e del client MSDRM, non sarà possibile configurare Exchange per l'uso del connettore. Prima di continuare, verificare che siano state installate le versioni corrette.

### <a name="to-configure-exchange-servers-to-use-the-connector"></a>Per configurare server di Exchange per l'uso del connettore

1. Assicurarsi che i server Exchange siano autorizzati a usare il connettore RMS tramite lo strumento di amministrazione del connettore RMS e le informazioni della sezione [Autorizzazione dei server all'uso del connettore RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector). 

    Questa configurazione è necessaria in modo tale che Exchange possa usare il connettore RMS.

2. Nei ruoli del server di Exchange che comunicano con il connettore RMS, effettuare una delle seguenti operazioni:

   -   **Eseguire lo strumento di configurazione server per il connettore Microsoft RMS**. 

       Per altre informazioni, vedere [come usare lo strumento di configurazione server per il connettore Microsoft RMS](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector).

        Ad esempio, per eseguire lo strumento localmente per configurare un server che esegue Exchange 2016 o Exchange 2013:

       ```PowerShell
       .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetExchange2013
       ```

    
   -   **Apportare modifiche manuali al registro di sistema**. Per altre informazioni, vedere [impostazioni del registro di sistema per il connettore RMS](rms-connector-registry-settings.md). 

3. Abilitare la funzionalità IRM per Exchange usando il cmdlet di PowerShell per Exchange [Set-IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/set-irmconfiguration). Impostare `InternalLicensingEnabled $true` e `ClientAccessServerEnabled $true`.


## <a name="configuring-a-sharepoint-server-to-use-the-connector"></a>Configurazione di un server di SharePoint per l'uso del connettore

I server Web front-end di SharePoint, inclusi quelli che ospitano il server di amministrazione centrale, comunicano con il connettore RMS.

Per usare un connettore RMS, è necessario che i server di SharePoint eseguano una delle versioni seguenti del software:

-   SharePoint Server 2019

-   SharePoint Server 2016

-   SharePoint Server 2013

-   SharePoint Server 2010

Un server che esegue SharePoint 2019, 2016 o SharePoint 2013 deve eseguire anche una versione del client MSIPC 2,1 supportata con il connettore RMS. 

Per assicurarsi che sia disponibile la versione supportata, scaricare il client più recente da [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=38396).

> [!WARNING]
> Sono disponibili più versioni del client MSIPC 2.1. Assicurarsi quindi di avere la versione 1.0.2004.0 o successiva.
>
> È possibile verificare la versione del client controllando il numero di versione di MSIPC.dll, disponibile in **\Programmi\Active Directory Rights Management Services Client 2.1**. La finestra di dialogo delle proprietà indica il numero di versione del client MSIPC 2.1.

È necessario che nei server che eseguono SharePoint 2010 sia installata una versione del client MSDRM che includa il supporto della Modalità crittografia 2 di RMS. Windows Server 2012 e Windows Server 2012 R2 offrono supporto nativo per la modalità di crittografia 2.

### <a name="to-configure-sharepoint-servers-to-use-the-connector"></a>Per configurare server di SharePoint per l'uso del connettore

1. Assicurarsi che i server di SharePoint siano autorizzati a usare il connettore RMS tramite lo strumento di amministrazione del connettore RMS e le informazioni della sezione [Autorizzazione dei server all'uso del connettore RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector). 

    Questa configurazione è necessaria per consentire ai server di SharePoint di usare il connettore RMS.

2.  Sui server di SharePoint che comunicano con il connettore RMS, effettuare una delle seguenti operazioni:

    -   **Eseguire lo strumento di configurazione server per il connettore Microsoft RMS** 

        Per altre informazioni, vedere [come usare lo strumento di configurazione server per il connettore Microsoft RMS](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector).

        Ad esempio, per eseguire lo strumento localmente per configurare un server che esegue SharePoint 2019, 2016 o SharePoint 2013:

        ```PowerShell
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetSharePoint2013
        ```

    -   **Se si usa sharepoint 2019, 2016 o sharepoint 2013, apportare modifiche manuali al registro** di sistema usando le informazioni contenute in [impostazioni del registro di sistema per il connettore RMS](rms-connector-registry-settings.md) per aggiungere manualmente le impostazioni del registro di sistema nei server. 

3.  Abilitare IRM in SharePoint. Per ulteriori informazioni, vedere [Configurare Information Rights Management (SharePoint Server 2010)](/previous-versions/office/sharepoint-server-2010/hh545607(v=office.14)) nella libreria di SharePoint.

    Quando si seguono queste istruzioni, è necessario configurare SharePoint per l'uso del connettore. A questo scopo, specificare l'opzione **Usa il server RMS seguente** e immettere l'URL del connettore di bilanciamento del carico configurato. 

    Immettere il prefisso del protocollo (HTTP:// o HTTPS://) e il nome del connettore definito nel DNS per l'indirizzo di bilanciamento del carico del connettore stesso, 

    Ad esempio, se il nome del connettore è `https:\//connector.contoso.com`, la configurazione sarà simile all'immagine seguente:

    ![Configurazione di SharePoint Server per il connettore RMS](./media/AzRMS_SharePointConnector.png)

    Una volta abilitato Information Rights Management (IRM) per una farm di SharePoint, è possibile abilitarlo per singole raccolte usando l'opzione **Information Rights Management** nella pagina **Impostazioni raccolta** di ciascuna raccolta.

## <a name="configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector"></a>Configurazione di un file server per consentire l'uso del connettore alla funzionalità Infrastruttura di classificazione file

Per usare il connettore RMS e la funzionalità Infrastruttura di classificazione file per proteggere i documenti di Office, è necessario che il file server esegua uno dei sistemi operativi seguenti:

- Windows Server 2016

- Windows Server 2012 R2

- Windows Server 2012

### <a name="to-configure-file-servers-to-use-the-connector"></a>Per configurare file server per l'uso del connettore

1. Assicurarsi che i file server siano autorizzati a usare il connettore RMS tramite lo strumento di amministrazione del connettore RMS e le informazioni della sezione [Autorizzazione dei server all'uso del connettore RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector). 

    Questa configurazione è necessaria per consentire ai file server di usare il connettore RMS.

2. Sui file server configurati per Infrastruttura di classificazione file e che comunicheranno con il connettore RMS, effettuare una delle seguenti operazioni:

    -   **Eseguire lo strumento di configurazione server per il connettore Microsoft RMS** 
    
        Per altre informazioni, vedere [come usare lo strumento di configurazione server per il connettore Microsoft RMS](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector).

        Ad esempio, per eseguire lo strumento localmente per configurare un file server che esegue FCI:

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetFCI2012
        ```

    - **Apportare modifiche manuali al registro di sistema** usando le informazioni contenute in [impostazioni del registro di sistema per il connettore RMS](rms-connector-registry-settings.md) per aggiungere manualmente le impostazioni del registro di sistema nei server. 

3. Creare regole di classificazione e attività di gestione di file per proteggere i documenti con la crittografia RMS e quindi specificare un modello RMS per applicare automaticamente criteri RMS. 

    Per altre informazioni, vedere la [panoramica di gestione risorse del file server](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831701(v=ws.11)) nella libreria della documentazione di Windows Server.

## <a name="next-steps"></a>Passaggi successivi
Dopo aver installato e configurato il connettore RMS e configurato i server per l'uso di tale connettore, gli amministratori IT e gli utenti possono proteggere e gestire messaggi di posta elettronica e documenti mediante il servizio Azure Rights Management. 

Per facilitare questa operazione per gli utenti, distribuire il client Azure Information Protection, che installa un componente aggiuntivo per Office e aggiunge nuove opzioni al menu di scelta rapida di Esplora file. 

Per altre informazioni, vedere la [Guida dell'amministratore del client Azure Information Protection](./rms-client/client-admin-guide.md).

Si noti che se si configurano modelli di reparto da usare con le regole di trasporto di Exchange o l'infrastruttura di classificazione file (FCI, File Classification Infrastructure) per Windows Server, la configurazione dell'ambito deve includere l'opzione di compatibilità dell'applicazione in modo che la casella di controllo **Mostra questo modello a tutti gli utenti quando le applicazioni non supportano l'identità utente** sia selezionata.

È possibile usare [Azure Information Protection deployment roadmap](deployment-roadmap-classify-label-protect.md) (Roadmap della distribuzione di Azure Information Protection) per verificare se sono necessarie altre operazioni di configurazione prima di distribuire Azure Rights Management a utenti e amministratori.

Per monitorare il connettore RMS, vedere [Monitorare il connettore di Azure Rights Management](monitor-rms-connector.md).