---
title: Configurare i server per il connettore di Rights Management - AIP
description: Informazioni per configurare i server locali che sfrutteranno il connettore di Azure Rights Management (RMS). Queste procedure illustrano il passaggio 5 di Distribuzione del connettore di Azure Rights Management.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/18/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 75846ee1-2370-4360-81ad-e2b6afe3ebc9
ms.subservice: connector
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 05522bbb7f6357baac060062e6715fdf4807fa09
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/05/2019
ms.locfileid: "68788916"
---
# <a name="configuring-servers-for-the-azure-rights-management-connector"></a>Configurazione dei server per il connettore di Azure Rights Management

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*


Usare le informazioni seguenti per configurare il server locale che sfrutterà il connettore di Azure Rights Management (RMS). Queste procedure illustrano il passaggio 5 di [Distribuzione del connettore di Azure Rights Management](deploy-rms-connector.md).

Prima di iniziare, assicurarsi di aver installato e configurato il connettore RMS e che siano stati soddisfatti i [prerequisiti](deploy-rms-connector.md#prerequisites-for-the-rms-connector) applicabili per i server che useranno il connettore.


## <a name="configuring-servers-to-use-the-rms-connector"></a>Configurazione dei server per l'uso del connettore RMS
Dopo aver installato e configurato il connettore RMS, si è pronti per configurare i server locali che si connettono al servizio Azure Rights Management e usano la tecnologia di protezione mediante il connettore. È necessario configurare i server seguenti:

-   **Per Exchange 2016 ed Exchange 2013**: Server Accesso client e server cassette postali

-   **Per Exchange 2010**: Server Accesso client e server Trasporto Hub

-   **Per SharePoint**: server Web front-end di SharePoint, inclusi quelli che ospitano il server Amministrazione centrale

-   **Per Infrastruttura di classificazione file**: Computer Windows Server in cui è installato file Gestione risorse

Per questa configurazione sono necessarie alcune impostazioni del Registro di sistema. A questo scopo, sono disponibili due opzioni: automatica, usando lo strumento di configurazione server per il connettore Microsoft RMS o manuale modificando il Registro di sistema.

---

**Automaticamente, usando lo strumento di configurazione server per il connettore Microsoft RMS:**

- Vantaggi:

    - Non è necessario modificare direttamente il Registro di sistema. Le modifiche necessarie vengono apportate automaticamente mediante uno script.

    - Non è necessario eseguire un cmdlet di Windows PowerShell per ottenere l'URL di Microsoft RMS.

    - Se si esegue lo strumento in locale, i prerequisiti vengono verificati automaticamente (le correzioni eventualmente necessarie, tuttavia, non vengono eseguite automaticamente).

Svantaggi:

- Quando si esegue lo strumento, è necessario stabilire una connessione a un server che esegue già il connettore RMS.

---

**Manualmente, modificando il Registro di sistema:**

- Vantaggi:

    - Non è necessario stabilire una connessione a un server che esegue il connettore RMS.

- Svantaggi:

    - Si verifica un sovraccarico amministrativo, con aumentata possibilità di errore.

    - È necessario ottenere l'URL di Microsoft RMS, operazione che richiede l'esecuzione di un comando di Windows PowerShell.

    - È necessario controllare manualmente tutti i prerequisiti.


---

> [!IMPORTANT]
> In entrambi i casi, è necessario installare manualmente i prerequisiti e configurare Exchange, SharePoint e Infrastruttura di classificazione file per l'uso di Rights Management.

Per la maggior parte delle organizzazioni, la configurazione automatica mediante lo strumento di configurazione server per il connettore Microsoft RMS è l'opzione più conveniente poiché assicura livelli di efficienza e affidabilità più elevati rispetto alla configurazione manuale.

Dopo aver apportato modifiche alla configurazione di questi server, è necessario riavviarli se eseguono Exchange o SharePoint e sono stati configurati in precedenza per l'uso di AD RMS. Il riavvio di questi server non è necessario se vengono configurati per Rights Management per la prima volta. Dopo aver apportato queste modifiche alla configurazione, è sempre necessario riavviare il file server configurato per l'uso di Infrastruttura di classificazione file.

### <a name="how-to-use-the-server-configuration-tool-for-microsoft-rms-connector"></a>Come usare lo strumento di configurazione server per il connettore Microsoft RMS

1.  Se non è stato già scaricato lo script per lo strumento di configurazione del server per il connettore Microsoft RMS (Genconnectorconfig.ps1), scaricarlo dall' [Area download Microsoft](https://go.microsoft.com/fwlink/?LinkId=314106).

2.  Salvare il file GenConnectorConfig.ps1 sul computer su cui verrà eseguito lo strumento. Se lo strumento viene eseguito localmente, il file deve essere salvato sul server che si desidera configurare per comunicare con il connettore RMS. In caso contrario, è possibile salvare il file su qualsiasi computer.

3.  Stabilire la modalità di esecuzione dello strumento:

    -   **In locale**: È possibile eseguire lo strumento in modo interattivo, dal server da configurare per comunicare con il connettore RMS. Questa modalità è utile per una configurazione d'uso occasionale, ad esempio un ambiente di test.

    -   **Distribuzione software**: è possibile eseguire lo strumento per generare i file del Registro di sistema da distribuire a uno o più server pertinenti usando un'applicazione di gestione dei sistemi che supporta la distribuzione software, ad esempio System Center Configuration Manager.

    -   **Criteri di gruppo**: È possibile eseguire lo strumento per produrre uno script da assegnare a un amministratore che può creare oggetti Criteri di gruppo per i server da configurare. Questo script crea un oggetto Criteri di gruppo per ciascun tipo di server da configurare. L'amministratore può quindi assegnare l'oggetto corretto ai server pertinenti.

    > [!NOTE]
    > Questo strumento consente di configurare i server che comunicheranno con il connettore RMS e che sono elencati all'inizio di questa sezione. Non eseguire questo strumento sui server che eseguono il connettore RMS.

4.  Avviare Windows PowerShell con l'opzione **Esegui come amministratore**, quindi usare il comando Get-help e leggere le istruzioni relative alla modalità d'uso del metodo di configurazione scelto:

    ```
    Get-help .\GenConnectorConfig.ps1 -detailed
    ```

Per eseguire lo script è necessario immettere l'URL del connettore RMS dell'organizzazione. Immettere il prefisso del protocollo (HTTP:// o HTTPS://) e il nome del connettore definito nel DNS per l'indirizzo di bilanciamento del carico del connettore stesso, Ad esempio https:\//Connector.contoso.com. Lo strumento usa quindi tale URL per contattare i server che eseguono il connettore RMS e ottenere altri parametri usati per creare le configurazioni richieste.

> [!IMPORTANT]
> Quando si esegue questo strumento, assicurarsi di specificare il nome del connettore RMS con carico bilanciato per l'organizzazione e non il nome di un singolo server che esegue il servizio del connettore RMS.

Nelle sezioni seguenti sono disponibili informazioni specifiche per ciascun tipo di servizio:

-   [Configurazione di un server di Exchange per l'uso del connettore](#configuring-an-exchange-server-to-use-the-connector)

-   [Configurazione di un server di SharePoint per l'uso del connettore](#configuring-a-sharepoint-server-to-use-the-connector)

-   [Configurazione di un file server per consentire l'uso del connettore alla funzionalità Infrastruttura di classificazione file](#configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector)

> [!NOTE]
> Dopo aver configurato questi server per l'uso del connettore, è possibile che le applicazioni client installate in locale su tali server non siano in grado di funzionare con RMS. Questo inconveniente si verifica perché le applicazioni tentano di usare il connettore anziché usare direttamente RMS.
>
> Inoltre, se Office 2010 è installato in locale su un server di Exchange, dopo la configurazione del server per l'uso del connettore è possibile che le funzionalità IRM delle app client non funzionino correttamente sul computer.
>
> In entrambi gli scenari, è necessario installare le applicazioni client in computer separati non configurati per l'uso del connettore. Tali computer useranno quindi RMS direttamente.

## <a name="configuring-an-exchange-server-to-use-the-connector"></a>Configurazione di un server di Exchange per l'uso del connettore
I seguenti ruoli di Exchange comunicano con il connettore RMS:

-   Per Exchange 2016 ed Exchange 2013: Server Accesso client e server cassette postali

-   Per Exchange 2010: Server Accesso client e server Trasporto Hub

Per usare un connettore RMS, è necessario che i server di Exchange eseguano una delle versioni seguenti del software:

-   Exchange Server 2016

-   Exchange Server 2013 con aggiornamento cumulativo 3

-   Exchange Server 2010 con Service Pack 3, aggiornamento di rollup 6

È anche necessario che sui server sia disponibile una versione 1 del client RMS (noto anche come MSDRM) con supporto per la modalità di crittografia RMS 2. Il client MSDRM è incluso in tutti i sistemi operativi Windows, ma le prime versioni del client non supportano la modalità di crittografia 2. Se i server Exchange in uso eseguono Windows Server 2012 o versioni successive, non sono necessarie azioni aggiuntive poiché il client RMS installato in questi sistemi operativi supporta in modo nativo la modalità di crittografia 2. 

Se i server Exchange in uso eseguono invece una versione precedente del sistema operativo, verificare che la versione installata del client RMS supporti la modalità di crittografia 2. In particolare, controllare la versione installata del file Windows\System32\Msdrm.dll rispetto ai numeri di versione elencati nei seguenti articoli della Knowledge Base. Se il numero della versione installata è uguale o maggiore rispetto ai numeri di versione elencati, non sono necessarie azioni aggiuntive. Se invece il numero è inferiore, scaricare e installare l'aggiornamento rapido dall'articolo.

- Windows Server 2008: [https://support.microsoft.com/kb/2627272](https://support.microsoft.com/kb/2627272) 

- Windows Server 2008 R2: [https://support.microsoft.com/kb/2627273](https://support.microsoft.com/kb/2627273)

> [!IMPORTANT]
> Se non sono state installate queste versioni (o versioni successive) di Exchange e del client MSDRM, non sarà possibile configurare Exchange per l'uso del connettore. Prima di continuare, verificare che siano state installate le versioni corrette.

### <a name="to-configure-exchange-servers-to-use-the-connector"></a>Per configurare server di Exchange per l'uso del connettore

1. Assicurarsi che i server Exchange siano autorizzati a usare il connettore RMS tramite lo strumento di amministrazione del connettore RMS e le informazioni della sezione [Autorizzazione dei server all'uso del connettore RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector). Questa configurazione è necessaria in modo tale che Exchange possa usare il connettore RMS.

2. Nei ruoli del server di Exchange che comunicano con il connettore RMS, effettuare una delle seguenti operazioni:

   -   Eseguire lo strumento di configurazione server per il connettore Microsoft RMS. Per ulteriori informazioni, vedere [Come usare lo strumento di configurazione server per il connettore Microsoft RMS](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector) in questo articolo.

       Ad esempio, per eseguire lo strumento localmente per configurare un server che esegue Exchange 2016 o Exchange 2013:

       ```
       .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetExchange2013
       ```

   -   Modificare il registro utilizzando le informazioni contenute in [Impostazioni del Registro di sistema per il connettore RMS](rms-connector-registry-settings.md) per aggiungere manualmente le impostazioni del Registro di sistema sui server. 

3. Abilitare la funzionalità IRM per Exchange usando il cmdlet di PowerShell per Exchange [Set-IRMConfiguration](https://docs.microsoft.com/powershell/module/exchange/encryption-and-certificates/set-irmconfiguration?view=exchange-ps) `InternalLicensingEnabled $true` e `ClientAccessServerEnabled $true`impostare e.


## <a name="configuring-a-sharepoint-server-to-use-the-connector"></a>Configurazione di un server di SharePoint per l'uso del connettore
I seguenti ruoli di SharePoint comunicano con il connettore RMS:

-   server Web front-end di SharePoint, inclusi quelli che ospitano il server Amministrazione centrale

Per usare un connettore RMS, è necessario che i server di SharePoint eseguano una delle versioni seguenti del software:

-   SharePoint Server 2016

-   SharePoint Server 2013

-   SharePoint Server 2010

È necessario che un server che esegue SharePoint 2016 o SharePoint 2013 esegua anche una versione del client MSIPC 2.1 supportata con il connettore RMS. Per assicurarsi che sia disponibile la versione supportata, scaricare il client più recente da [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=38396).

> [!WARNING]
> Sono disponibili più versioni del client MSIPC 2.1. Assicurarsi quindi di avere la versione 1.0.2004.0 o successiva.
>
> È possibile verificare la versione del client controllando il numero di versione di MSIPC.dll, disponibile in **\Programmi\Active Directory Rights Management Services Client 2.1**. La finestra di dialogo delle proprietà indica il numero di versione del client MSIPC 2.1.

È necessario che nei server che eseguono SharePoint 2010 sia installata una versione del client MSDRM che includa il supporto della Modalità crittografia 2 di RMS. La versione minima supportata in Windows Server 2008 è inclusa nell'hotfix scaricabile dalla pagina dell'articolo relativo alla [lunghezza della chiave RSA aumentata a 2048 bit per AD RMS in Windows Server 2008 R2 e in Windows Server 2048](https://support.microsoft.com/kb/2627272), mentre la versione minima per Windows Server 7 R2 può essere scaricata dalla pagina dell'articolo relativo alla [lunghezza della chiave RSA aumentata a 2048 bit per AD RMS in Windows 7 o Windows Server 2008 R2](https://support.microsoft.com/kb/2627273). Windows Server 2012 e Windows Server 2012 R2 offrono supporto nativo per la modalità di crittografia 2.

### <a name="to-configure-sharepoint-servers-to-use-the-connector"></a>Per configurare server di SharePoint per l'uso del connettore

1. Assicurarsi che i server di SharePoint siano autorizzati a usare il connettore RMS tramite lo strumento di amministrazione del connettore RMS e le informazioni della sezione [Autorizzazione dei server all'uso del connettore RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector). Questa configurazione è necessaria per consentire ai server di SharePoint di usare il connettore RMS.

2.  Sui server di SharePoint che comunicano con il connettore RMS, effettuare una delle seguenti operazioni:

    -   Eseguire lo strumento di configurazione server per il connettore Microsoft RMS. Per ulteriori informazioni, vedere [Come usare lo strumento di configurazione server per il connettore Microsoft RMS](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector) in questo articolo.

        Ad esempio, per eseguire lo strumento in locale per configurare un server che esegue SharePoint 2016 o SharePoint 2013:

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetSharePoint2013
        ```

    -   Se si usa SharePoint 2016 o SharePoint 2013, modificare manualmente il Registro di sistema usando le informazioni disponibili in [Impostazioni del Registro di sistema per il connettore RMS](rms-connector-registry-settings.md) per aggiungere manualmente le impostazioni di registro nei server. 

3.  Abilitare IRM in SharePoint. Per ulteriori informazioni, vedere [Configurare Information Rights Management (SharePoint Server 2010)](https://technet.microsoft.com/library/hh545607%28v=office.14%29.aspx) nella libreria di SharePoint.

    Quando si seguono queste istruzioni, è necessario configurare SharePoint per l'uso del connettore. A questo scopo, specificare l'opzione **Usa il server RMS seguente** e immettere l'URL del connettore di bilanciamento del carico configurato. Immettere il prefisso del protocollo (HTTP:// o HTTPS://) e il nome del connettore definito nel DNS per l'indirizzo di bilanciamento del carico del connettore stesso, Ad esempio, se il nome del connettore è https\/:/Connector.contoso.com, la configurazione sarà simile all'immagine seguente:

    ![Configurazione di SharePoint Server per il connettore RMS](./media/AzRMS_SharePointConnector.png)

    Una volta abilitato Information Rights Management (IRM) per una farm di SharePoint, è possibile abilitarlo per singole raccolte usando l'opzione **Information Rights Management** nella pagina **Impostazioni raccolta** di ciascuna raccolta.


## <a name="configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector"></a>Configurazione di un file server per consentire l'uso del connettore alla funzionalità Infrastruttura di classificazione file
Per usare il connettore RMS e la funzionalità Infrastruttura di classificazione file per proteggere i documenti di Office, è necessario che il file server esegua uno dei sistemi operativi seguenti:

- Windows Server 2016

- Windows Server 2012 R2

- Windows Server 2012

### <a name="to-configure-file-servers-to-use-the-connector"></a>Per configurare file server per l'uso del connettore

1. Assicurarsi che i file server siano autorizzati a usare il connettore RMS tramite lo strumento di amministrazione del connettore RMS e le informazioni della sezione [Autorizzazione dei server all'uso del connettore RMS](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector). Questa configurazione è necessaria per consentire ai file server di usare il connettore RMS.

2. Sui file server configurati per Infrastruttura di classificazione file e che comunicheranno con il connettore RMS, effettuare una delle seguenti operazioni:

    -   Eseguire lo strumento di configurazione server per il connettore Microsoft RMS. Per ulteriori informazioni, vedere [Come usare lo strumento di configurazione server per il connettore Microsoft RMS](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector) in questo articolo.

        Ad esempio, per eseguire lo strumento localmente per configurare un file server che esegue FCI:

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetFCI2012
        ```

    - Modificare il registro utilizzando le informazioni contenute in [Impostazioni del Registro di sistema per il connettore RMS](rms-connector-registry-settings.md) per aggiungere manualmente le impostazioni del Registro di sistema sui server. 

3. Creare regole di classificazione e attività di gestione di file per proteggere i documenti con la crittografia RMS e quindi specificare un modello RMS per applicare automaticamente criteri RMS. Per altre informazioni, vedere la [panoramica di gestione risorse del file server](https://technet.microsoft.com/library/hh831701.aspx) nella libreria della documentazione di Windows Server.

## <a name="next-steps"></a>Passaggi successivi
Dopo aver installato e configurato il connettore RMS e configurato i server per l'uso di tale connettore, gli amministratori IT e gli utenti possono proteggere e gestire messaggi di posta elettronica e documenti mediante il servizio Azure Rights Management. Per facilitare questa operazione per gli utenti, distribuire il client Azure Information Protection, che installa un componente aggiuntivo per Office e aggiunge nuove opzioni al menu di scelta rapida di Esplora file. Per altre informazioni, vedere la [Guida dell'amministratore del client Azure Information Protection](./rms-client/client-admin-guide.md).

Si noti che se si configurano modelli di reparto da usare con le regole di trasporto di Exchange o l'infrastruttura di classificazione file (FCI, File Classification Infrastructure) per Windows Server, la configurazione dell'ambito deve includere l'opzione di compatibilità dell'applicazione in modo che la casella di controllo **Mostra questo modello a tutti gli utenti quando le applicazioni non supportano l'identità utente** sia selezionata.

È possibile usare [Azure Information Protection deployment roadmap](deployment-roadmap.md) (Roadmap della distribuzione di Azure Information Protection) per verificare se sono necessarie altre operazioni di configurazione prima di distribuire Azure Rights Management a utenti e amministratori.

Per monitorare il connettore RMS, vedere [Monitorare il connettore di Azure Rights Management](monitor-rms-connector.md). 
