---
title: Installazione e configurazione del connettore Azure Rights Management - AIP
description: Informazioni che consentono di installare e configurare il connettore Azure Rights Management (RMS). Queste procedure illustrano i passaggi da 1 a 4 descritti nell'articolo Distribuzione del connettore Azure Rights Management.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/11/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4fed9d4f-e420-4a7f-9667-569690e0d733
ms.subservice: connector
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 0bdf9feb0b81d6fe39dba3545b171c60ec0661b5
ms.sourcegitcommit: f6d536b6a3b5e14e24f0b9e58d17a3136810213b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98809483"
---
# <a name="installing-and-configuring-the-azure-rights-management-connector"></a>Installazione e configurazione del connettore Azure Rights Management

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), windows server 2019, 2016, 2012 R2 e Windows Server 2012 *
>
>***Rilevante per**: [Client di etichettatura unificata e client classico di AIP](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Usare le informazioni seguenti per installare e configurare il connettore Azure Rights Management (RMS). Queste procedure illustrano i passaggi da 1 a 4 descritti nell'articolo [Distribuzione del connettore Azure Rights Management](deploy-rms-connector.md).

Prima di iniziare verificare di aver riesaminato e controllato i [prerequisiti](deploy-rms-connector.md#prerequisites-for-the-rms-connector) per questa distribuzione.

Assicurarsi di conoscere l'istanza corretta di Azure Sovereign cloud per consentire al connettore di completare l'installazione e la configurazione: 
- **AzureCloud**: offerta commerciale di Azure
- **AzureChinaCloud**: Azure gestito da 21ViaNet
- **AzureUSGovernment**: Azure per enti pubblici (GCC High/DOD)
- **AzureUSGovernment2**: Azure per enti pubblici 2
- **AzureUSGovernment3**: Azure per enti pubblici 3


## <a name="installing-the-rms-connector"></a>Installazione del connettore RMS

1.  Identificare i computer (almeno due) per eseguire il connettore RMS. Questi computer devono soddisfare le specifiche minime elencate nei prerequisiti.

    > [!NOTE]
    > Installare un singolo connettore RMS (costituito da più server per la disponibilità elevata) per ogni tenant (Microsoft 365 tenant o Azure AD tenant). A differenza di Active Directory RMS, non è necessario installare un connettore RMS in ogni foresta.

2.  Scaricare i file di origine per il connettore RMS dall'[Area download Microsoft](https://go.microsoft.com/fwlink/?LinkId=314106).

    Per installare il connettore RMS, scaricare RMSConnectorSetup.exe.

    Inoltre:

    -   Se si desidera usare lo strumento di configurazione del server per il connettore RMS in modo da automatizzare la configurazione delle impostazioni del registro sui server locali, scaricare anche GenConnectorConfig.ps1.

3.  Nel computer in cui si vuole installare il connettore RMS eseguire **RMSConnectorSetup.exe** con privilegi di amministratore.

4.  Nella pagina iniziale del programma di installazione di Microsoft Rights Management Connector selezionare **installa Microsoft Rights Management Connector nel computer**, quindi fare clic su **Avanti**.

5.  Leggere e accettare i termini del contratto di licenza del connettore RMS, quindi fare clic su **Avanti**.


## <a name="entering-credentials"></a>Immissione delle credenziali

Prima di poter configurare il connettore RMS, è innanzitutto necessario selezionare l'ambiente cloud corrispondente alla soluzione.   
- **AzureCloud**: offerta commerciale di Azure
- **AzureChinaCloud**: Azure gestito da 21ViaNet
- **AzureUSGovernment**: Azure per enti pubblici (GCC High/DOD)
- **AzureUSGovernment2**: Azure per enti pubblici 2
- **AzureUSGovernment3**: Azure per enti pubblici 3

:::image type="content" source="media/authenticate_tenant_rms_connector.png" alt-text="Selezionare l'ambiente Azure corretto per autenticare il nuovo connettore AAD RM":::

Dopo avere selezionato l'ambiente cloud, immettere il **nome utente** e la **password**. Assicurarsi di immettere le credenziali per un account che dispone di privilegi sufficienti per configurare il connettore RMS. Ad esempio, è possibile digitare <strong>admin@contoso.com</strong> e quindi specificare la password per l'account.


Inoltre, se sono stati implementati i [controlli di onboarding](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment), verificare che l'account specificato sia in grado di proteggere il contenuto. Ad esempio, se è stata limitata la possibilità di proteggere il contenuto per il gruppo "Reparto IT", l'account specificato deve essere un membro del gruppo. In caso contrario, viene visualizzato il messaggio di errore: **tentativo di individuare la posizione del servizio di amministrazione e dell'organizzazione non riuscito. Verificare che il servizio Microsoft Rights Management sia abilitato per l'organizzazione.**

È possibile usare un account con uno dei privilegi seguenti:

-   **Amministratore globale per il tenant**: un account amministratore globale per il tenant di Microsoft 365 o Azure ad tenant.

-   **Amministratore globale di Azure Rights Management**: account in Azure Active Directory a cui è stato assegnato il ruolo di amministratore globale di Azure RMS.

-   **Amministratore del connettore Azure Rights Management**: account in Azure Active Directory a cui sono stati accordati i diritti di installazione e amministrazione del connettore RMS per l'organizzazione.

    > [!NOTE]
    > Il ruolo di amministratore globale di Azure Rights Management e il ruolo di amministratore del connettore Azure Rights Management sono assegnati agli account tramite il cmdlet [Add-AipServiceRoleBasedAdministrator](/powershell/module/aipservice/add-aipservicerolebasedadministrator) .
    > 
    > Per eseguire il connettore RMS con privilegi minimi, creare un account dedicato a questo scopo, quindi assegnare il ruolo di amministratore del connettore Azure RMS tramite le operazioni seguenti:
    >
    > 1. Se non è già stato fatto, scaricare e installare il modulo AIPService di PowerShell. Per altre informazioni, vedere [installazione del modulo PowerShell AIPService](install-powershell.md).
    >
    >     Avviare Windows PowerShell con il comando **Esegui come amministratore** e connettersi al servizio di protezione usando il comando [Connect-AipService](/powershell/module/aipservice/connect-aipservice) :
    >
    >     ```
    >     Connect-AipService                   //provide Microsoft 365 tenant administrator or Azure RMS global administrator credentials
    >     ```
    > 2.  Eseguire quindi il comando [Add-AipServiceRoleBasedAdministrator](/powershell/module/aipservice/add-aipservicerolebasedadministrator) usando solo uno dei parametri seguenti:
    >
    >     ```
    >     Add-AipServiceRoleBasedAdministrator -EmailAddress <email address> -Role "ConnectorAdministrator"
    >     ```
    >
    >     ```
    >     Add-AipServiceRoleBasedAdministrator -ObjectId <object id> -Role "ConnectorAdministrator"
    >     ```
    >
    >     ```
    >     Add-AipServiceRoleBasedAdministrator -SecurityGroupDisplayName <group Name> -Role "ConnectorAdministrator"
    >     ```
    >     Ad esempio, digitare: **Add-AipServiceRoleBasedAdministrator-EmailAddress melisa@contoso.com -Role "ConnectorAdministrator"**
    >
    >     Anche se questi comandi assegnano il ruolo di amministratore del connettore, è possibile usare anche il ruolo GlobalAdministrator.

Durante il processo di installazione del connettore RMS, viene eseguita la convalida e l'installazione di tutti i prerequisiti software, l'installazione di Internet Information Services (IIS) se non già presente, e l'installazione e la configurazione del software del connettore. Viene anche preparata la configurazione di Azure RMS attraverso la creazione degli elementi seguenti:

-   Una tabella vuota relativa ai server autorizzati a usare il connettore per comunicare con Azure RMS. Aggiungere i server a questa tabella in un secondo momento.

-   Un set di token di sicurezza per il connettore che autorizzano operazioni con Azure RMS. Questi token vengono scaricati da Azure RMS e installati nel computer locale nel registro di sistema. Sono protetti tramite l'interfaccia di programmazione dell'applicazione di protezione dei dati (DPAPI) e le credenziali dell'account di sistema locale.

Nella pagina finale della procedura guidata, eseguire le operazioni indicate di seguito e fare clic su **Fine**:

-   Se si è installato il primo connettore, non selezionare l'opzione **Avvia console di amministrazione del connettore per autorizzare i server** . Questa opzione potrà essere selezionata dopo aver installato il secondo (o l'ultimo) connettore RMS. In alternativa, eseguire nuovamente la procedura guidata su almeno un altro computer. È necessario installare almeno due connettori.

-   Se si è installato il secondo (o l'ultimo) connettore, selezionare l'opzione **Avvia la console di amministrazione del connettore per autorizzare i server**.

> [!TIP]
> A questo punto, è possibile eseguire un test di verifica per testare l'operatività dei servizi Web per il connettore RMS:
>
> -   Da un Web browser, connettersi a **http://&lt;indirizzoconnettore&gt;/_wmcs/certification/servercertification.asmx**, sostituendo *&lt;indirizzoconnettore&gt;* con l'indirizzo o il nome del server in cui è installato il connettore RMS. Se la connessione ha esito positivo, viene visualizzata una pagina **ServerCertificationWebService**.

Se è necessario disinstallare il connettore RMS, eseguire di nuovo la procedura guidata e selezionare l'opzione di disinstallazione.

Se si verificano problemi durante l'installazione, controllare il log di installazione: **%LocalAppData%\Temp\Microsoft Rights Management connector_ \<date and time> . log** 

Ad esempio, il log di installazione potrebbe essere simile a **C:\Users\Administrator\AppData\Local\Temp\Microsoft Rights Management connector_20170803110352. log**

## <a name="authorizing-servers-to-use-the-rms-connector"></a>Autorizzazione dei server all'uso del connettore RMS
Dopo aver installato il connettore RMS in almeno due computer, è possibile autorizzare i server e i servizi desiderati nei quali usare il connettore RMS. Ad esempio, i server che eseguono Exchange Server 2013 o SharePoint Server 2013.

Per definire tali server, eseguire lo strumento di amministrazione del connettore RMS e aggiungerli all'elenco dei server autorizzati. È possibile eseguire questo strumento quando si seleziona **Avvia console di amministrazione del connettore per autorizzare i server** al termine dell'installazione guidata del connettore Microsoft Rights Management. In alternativa, è possibile eseguirlo in modo separato dalla procedura guidata.

Quando si autorizzano i server, tenere presente le considerazioni seguenti:

- I server aggiunti godono di privilegi speciali. A tutti gli account specificati per il ruolo nella configurazione del connettore Exchange Server viene concesso il [ruolo utente con privilegi avanzati](configure-super-users.md) in Azure RMS, che consente l'accesso a tutto il contenuto per questo tenant di RMS. La funzionalità per utenti con privilegi avanzati viene attivata automaticamente a questo punto, se necessario. Per evitare i rischi per la sicurezza dovuti all'elevazione dei privilegi, assicurarsi di specificare solo gli account usati dai server Exchange dell'organizzazione. A tutti i server configurati come server SharePoint o file server che usano FCI vengono concessi privilegi di utente normale.

- È possibile aggiungere più server come voce singola specificando una protezione Active Directory o gruppo di distribuzione, oppure un account del servizio usato da più server. Quando si usa questa configurazione, il gruppo di server condivide gli stessi certificati RMS e sono tutti considerati proprietari del contenuto protetto da ciascuno di essi. Per ridurre il sovraccarico amministrativo, è consigliabile usare questa configurazione di un singolo gruppo anziché singoli server per autorizzare i server Exchange dell'organizzazione o il server farm SharePoint.

Nella pagina **Server a cui è consentito l'uso del connettore**, fare clic su **Aggiungi**.

> [!NOTE]
> L'autorizzazione dei server è la configurazione equivalente in Azure RMS per la configurazione di AD RMS quando si applicano manualmente i diritti NTFS a ServerCertification.asmx per gli account computer del server o del servizio e si concedono manualmente diritti con privilegi avanzati agli account di Exchange. L'applicazione dei diritti NTFS a ServerCertification.asmx non è necessaria per il connettore.


### <a name="add-a-server-to-the-list-of-allowed-servers"></a>Aggiungere un server all'elenco dei server autorizzati
Nella pagina **Autorizza un server all'uso del connettore** immettere il nome dell'oggetto oppure individuare e selezionare l'oggetto da autorizzare.

È importante autorizzare l'oggetto corretto. Per consentire a un server di usare il connettore, è necessario selezionare l'account che esegue il servizio locale (ad esempio Exchange o SharePoint) per l'autorizzazione. Ad esempio, se il servizio è in esecuzione come account del servizio configurato, aggiungere il nome dell'account del servizio all'elenco. Se il servizio è in esecuzione come sistema locale, aggiungere il nome dell'oggetto computer (ad esempio SERVERNAME$). Come procedura consigliata, creare un gruppo contenente gli account e specificare il gruppo anziché i nomi dei singoli server.

Per altre informazioni sui diversi ruoli dei server:

-   Per i server che eseguono Exchange: è necessario specificare un gruppo di sicurezza ed è possibile usare il gruppo predefinito (**Server Exchange**) automaticamente da Exchange per creare e gestire tutti i server Exchange della foresta.

-   Per i server che eseguono SharePoint:

    -   Se un server SharePoint 2010 è configurato per l'esecuzione come sistema locale (senza l'uso di un account di servizio), creare manualmente un gruppo di sicurezza in Active Directory Domain Services e aggiungere a questo gruppo l'oggetto nome computer per il server in questa configurazione.

    -   Se un server SharePoint è configurato per usare un account del servizio (procedura consigliata per SharePoint 2010 e l'unica opzione per SharePoint 2016 e SharePoint 2013), eseguire le operazioni seguenti:

        1.  Aggiungere l'account del servizio che esegue il servizio Amministrazione centrale SharePoint per abilitare la configurazione dalla relativa console di amministrazione.

        2.  Aggiungere l'account configurato per il pool di applicazioni SharePoint.

        > [!TIP]
        > Se i due account sono diversi, è consigliabile creare un singolo gruppo che contiene entrambi gli account per ridurre al minimo il sovraccarico amministrativo.

-   Per i file server che usano l'infrastruttura di classificazione file, i servizi associati vengono eseguiti come account di sistema locale, pertanto è necessario autorizzare l'account computer per i file server (ad esempio, **ServerName $**) o un gruppo che contiene gli account computer.

Una volta completata l'aggiunta dei server all'elenco, fare clic su **Chiudi**.

Se non è già stato fatto, è necessario quindi configurare il bilanciamento del carico per i server sui quali è stato installato il connettore RMS e valutare se usare HTTPS per le connessioni tra questi server e i server appena autorizzati.

## <a name="configuring-load-balancing-and-high-availability"></a>Configurazione del bilanciamento del carico e disponibilità elevata
Dopo aver installato la seconda o l'ultima istanza del connettore RMS, definire un nome server URL connettore e configurare un sistema di bilanciamento del carico.

Il nome del server dell'URL del connettore può essere qualsiasi nome incluso in uno spazio dei nomi controllato. Ad esempio, è possibile creare una voce nel sistema DNS per **rmsconnector.contoso.com** e configurarla per l'uso di un indirizzo IP nel sistema di bilanciamento del carico. Non sono previsti requisiti speciali per il nome e lo stesso non deve essere configurato sui server del connettore. A meno che i server Exchange e SharePoint non comunichino con il connettore tramite Internet, non è necessario che questo nome venga risolto in Internet.

> [!IMPORTANT]
> È consigliabile non modificare questo nome dopo aver configurato i server Exchange o SharePoint per l'utilizzo del connettore, poiché altrimenti sarà necessario eliminare tali server da tutte le configurazioni IRM e configurarli nuovamente.

Dopo aver creato il nome nel DNS e averlo configurato per un indirizzo IP, configurare il bilanciamento del carico per tale indirizzo in modo da indirizzare il traffico ai server del connettore. A tale scopo, è possibile usare qualsiasi servizio di bilanciamento del carico basato su IP, inclusa la funzionalità di bilanciamento del carico di rete (NLB) in Windows Server. Per altre informazioni, vedere la [guida di distribuzione relativa al bilanciamento del carico](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754833(v=ws.10)).

Usare le impostazioni seguenti per configurare il cluster NLB:

-   **Porte**: 80 (per http) o 443 (per HTTPS)

    Per altre informazioni sull'uso di HTTP o HTTPS, vedere la sezione successiva.

-   **Affinità**: nessuna

-  **Metodo di distribuzione**: uguale a

Questo nome definito per il sistema con carico bilanciato (per i server che eseguono il servizio del connettore RMS) è il nome del connettore RMS dell'organizzazione che viene usato in seguito quando si configurano i server locali per l'uso di Azure RMS.

## <a name="configuring-the-rms-connector-to-use-https"></a>Configurazione del connettore RMS per l'uso di HTTPS
> [!NOTE]
> Questo passaggio di configurazione è facoltativo ma consigliato per una maggiore sicurezza.

Sebbene l'uso di TLS o SSL sia facoltativo per il connettore RMS, se ne consiglia comunque l'uso per qualsiasi servizio basato su HTTP con esigenze particolari a livello di sicurezza. Questa configurazione consente di autenticare i server che eseguono il connettore ai server Exchange e SharePoint che usano il connettore. Inoltre, tutti i dati inviati da questi server al connettore vengono crittografati.

Per abilitare il connettore RMS all'uso di TLS, su ogni server che esegue il connettore RMS installare un certificato di autenticazione server contenente il nome usato per il connettore stesso. Se, ad esempio, il nome del connettore RMS definito nel DNS è **rmsconnector.contoso.com**, distribuire un certificato di autenticazione server che contiene **rmsconnector.contoso.com** come nome comune nel soggetto del certificato. In alternativa, specificare **rmsconnector.contoso.com** nel nome alternativo del certificato come valore DNS. Il certificato non deve includere il nome del server. In IIS, associare quindi il certificato al sito Web predefinito.

Se si usa l'opzione HTTPS, assicurarsi che tutti i server che eseguono il connettore dispongano di un certificato di autenticazione server valido concatenato a un'autorità di certificazione (CA) radice considerata attendibile dai server Exchange e SharePoint dell'organizzazione. Inoltre, se l'autorità di certificazione (CA) che ha emesso i certificati per i server del connettore pubblica un elenco di revoche di certificati (CRL), è necessario che i server Exchange e SharePoint siano in grado di scaricare tale CRL.

> [!TIP]
> Per richiedere e installare un certificato di autenticazione server e per associare quest'ultimo al sito Web predefinito in IIS, usare le informazioni e le risorse indicate di seguito:
>
> - Se per distribuire i certificati di autenticazione server si usano Servizi certificati Active Directory e un'autorità di certificazione (CA) globale (enterprise), è possibile duplicare e quindi usare il modello di certificato del server Web. Questo modello di certificato usa **Fornito nella richiesta** per il nome soggetto del certificato. Questo significa che, quando si richiede il certificato, è possibile fornire il nome di dominio completo del nome del connettore RMS come nome soggetto del certificato o come nome alternativo del soggetto.
> -   Se si usa una CA autonoma o si acquista il certificato da un'altra società, vedere la sezione relativa alla [configurazione dei certificati del server Internet (IIS 7)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731977(v=ws.10)) nella raccolta di documentazione relativa al [Server Web (IIS)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753433(v=ws.10)) su TechNet.
> - Per configurare IIS per l'uso del certificato, vedere [Add a Binding to a Site (IIS 7)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731692(v=ws.10)) (Aggiungere un'associazione a un sito - IIS 7) nella raccolta di documentazione [Web Server (IIS)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753433(v=ws.10)) (Server Web - IIS) su TechNet.

## <a name="configuring-the-rms-connector-for-a-web-proxy-server"></a>Configurazione del connettore RMS per un server proxy web
Se i server del connettore sono installati in una rete che non dispone di connettività Internet diretta e richiede la configurazione manuale di un server proxy Web per l'accesso a Internet in uscita, è necessario configurare il registro di sistema in questi server per il connettore RMS.

#### <a name="to-configure-the-rms-connector-to-use-a-web-proxy-server"></a>Per configurare il connettore RMS per l'uso di un server proxy Web

1.  Su ogni server che esegue il connettore RMS aprire un editor del registro di sistema, ad esempio Regedit.

2.  Spostarsi in **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\AADRM\Connector**

3.  Aggiungere il valore di stringa **ProxyAddress**, quindi impostare i dati per questo valore **http://&lt;MyProxyDomainOrIPaddress&gt;:&lt;MyProxyPort&gt;**

    Per esempio: **http://proxyserver.contoso.com:8080**

4.  Chiudere l'editor del Registro di sistema, quindi riavviare il server o eseguire un comando IISReset per riavviare IIS.

## <a name="installing-the-rms-connector-administration-tool-on-administrative-computers"></a>Installazione dello strumento di amministrazione del connettore RMS su computer amministrativi
È possibile eseguire lo strumento di amministrazione del connettore RMS da un computer in cui è installato il connettore se il computer soddisfa i requisiti seguenti:

-   Un computer fisico o virtuale che esegue Windows Server 2019, 2016, 2012 o Windows Server 2012 R2 (tutte le edizioni), Windows 10, Windows 8.1, Windows 8.

-   Almeno 1 GB di RAM.

-   Almeno 64 GB di spazio su disco.

-   Almeno un'interfaccia di rete.

-   Accesso a Internet tramite un firewall o un proxy Web.

Per installare lo strumento di amministrazione del connettore RMS, eseguire i file seguenti:

-   Per un computer a 64 bit: RMSConnectorSetup.exe

Se non sono stati già scaricati questi file, è possibile farlo dall'[Area download Microsoft](https://go.microsoft.com/fwlink/?LinkId=314106).


## <a name="next-steps"></a>Passaggi successivi
Dopo l'installazione e la configurazione del connettore RMS, è possibile configurare i server locali per l'uso del connettore stesso. Passare a [Configurazione dei server per il connettore di Azure Rights Management](configure-servers-rms-connector.md).