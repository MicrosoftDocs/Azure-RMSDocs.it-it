---
title: Installare e configurare il connettore di Rights Management - AIP
description: Informazioni sull'installazione e la configurazione del connettore Azure Rights Management (RMS). Queste procedure illustrano i passaggi da 1 a 4 di Distribuzione del connettore di Azure Rights Management.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/16/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 4fed9d4f-e420-4a7f-9667-569690e0d733
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 2e3babe4a402b8f77700e9b9890dc5f826a5850a
ms.sourcegitcommit: d06594550e7ff94b4098a2aa379ef2b19bc6123d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/07/2018
ms.locfileid: "53026929"
---
# <a name="installing-and-configuring-the-azure-rights-management-connector"></a>Installazione e configurazione del connettore di Azure Rights Management

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2*

Nelle sezioni seguenti vengono fornite informazioni sull’installazione e la configurazione del connettore RMS di Azure Rights Management (RMS). Queste procedure illustrano i passaggi da 1 a 4 di [Distribuzione del connettore di Azure Rights Management](deploy-rms-connector.md).

Prima di iniziare, assicurarsi di aver esaminato e controllato i [prerequisiti](deploy-rms-connector.md#prerequisites-for-the-rms-connector) per questa distribuzione.


## <a name="installing-the-rms-connector"></a>Installazione del connettore RMS

1.  Identificare i computer (almeno due) che eseguiranno
2.  il connettore RMS. È necessario che tali computer siano conformi alle specifiche minime elencate nei prerequisiti.

    > [!NOTE]
    > Installare un singolo connettore RMS (costituito da più server per la disponibilità elevata) per ogni tenant (tenant di Office 365 o di Azure AD). A differenza di Active Directory RMS, non è necessario installare un connettore RMS in ogni foresta.

2.  Scaricare i file di origine per il connettore RMS dall' [Area download Microsoft](https://go.microsoft.com/fwlink/?LinkId=314106).

    Per installare il connettore RMS, scaricare il file RMSConnectorSetup.exe.

    Inoltre:

    -   Se si prevede di installare il connettore anche su un computer a 32 bit, scaricare il file RMSConnectorAdminToolSetup_x86.exe.

    -   Se per il connettore RMS si desidera usare lo strumento di configurazione server in modo da automatizzare la configurazione delle impostazioni del Registro di sistema sui server locali, scaricare anche il file GenConnectorConfig.ps1.

3.  Eseguire il file **RMSConnectorSetup.exe** con privilegi di amministratore sul computer in cui si desidera installare il connettore RMS.

4.  Nella home page della configurazione del connettore Microsoft Rights Management selezionare **Installa connettore Microsoft Rights Management sul computer**, quindi fare clic su **Avanti**.

5.  Leggere e accettare i termini del contratto di licenza del connettore RMS, quindi fare clic su **Avanti**.

Per continuare, immettere un account e una password per configurare il connettore RMS.

## <a name="entering-credentials"></a>Immissione delle credenziali
Per poter configurare il connettore RMS, è necessario immettere le credenziali per un account dotato di privilegi sufficienti per la configurazione del connettore. È ad esempio possibile digitare **admin@contoso.com** e quindi specificare la password per questo account.

Questo account non deve richiedere l'autenticazione a più fattori (MFA, Multi-Factor Authentication) perché lo strumento di amministrazione Microsoft Rights Management non supporta l'autenticazione MFA per questo account. 

Sono previste anche alcune limitazioni per i caratteri della password del connettore. Non è possibile usare una password che includa uno dei caratteri seguenti: e commerciale (**&**), parentesi quadra aperta (**[**), parentesi quadra chiusa (**]**), virgolette semplici (**"**) e apostrofo (**'**). Se la password include uno di questi caratteri non è possibile effettuare l'autenticazione per il connettore RMS e viene visualizzato il messaggio di errore **La combinazione nome utente e password specificata non è corretta**, anche se l'accesso con questo account e questa password funziona in altri scenari. Se si verifica questa situazione per la password in uso, scegliere un account diverso con una password che non include questi caratteri speciali oppure reimpostare la password in modo che non includa i caratteri speciali.

Inoltre, se sono stati implementati i [controlli di selezione utenti](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment), assicurarsi che l'account specificato sia in grado di proteggere il contenuto. Ad esempio, se è stata limitata la possibilità di proteggere il contenuto per il gruppo "Reparto IT", l'account specificato deve essere un membro del gruppo. In caso contrario, verrà visualizzato il messaggio di errore: **Tentativo di individuare la posizione del servizio di amministrazione e dell'organizzazione non riuscito. Assicurarsi che il servizio Microsoft Rights Management sia abilitato per l’organizzazione.**

È possibile usare un account con uno dei privilegi seguenti:

-   **Amministratore globale per il tenant**: account amministratore globale per il tenant di Office 365 o per il tenant di Azure AD.

-   **Amministratore globale di Azure Rights Management**: account in Azure Active Directory a cui è stato assegnato il ruolo di amministratore globale di Azure RMS.

-   **Amministratore di connettore di Azure Rights Management**: account di Azure Active Directory a cui sono stati concessi i diritti di installazione e amministrazione del connettore RMS per l'organizzazione.

    > [!NOTE]
    > Il ruolo di amministratore globale di Azure Rights Management e il ruolo di amministratore di connettore di Azure Rights Management vengono assegnati agli account con il cmdlet di Azure RMS [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator).
    > 
    > Per eseguire il connettore RMS con privilegi minimi, creare un account dedicato a questo scopo e assegnare a questo il ruolo di amministratore di connettore di Azure RMS tramite le operazioni seguenti:
    >
    > 1.  Se non è ancora stato fatto, scaricare e installare Windows PowerShell per Rights Management. Per altre informazioni, vedere [Installazione del modulo PowerShell AADRM](install-powershell.md).
    >
    >     Avviare Windows PowerShell con l'opzione **Esegui come amministratore** e usare il comando [Connect-AadrmService](/powershell/module/aadrm/connect-aadrmservice) per connettersi al servizio Azure RMS:
    >
    >     ```
    >     Connect-AadrmService                   //provide Office 365 tenant administrator or Azure RMS global administrator credentials
    >     ```
    > 2.  Eseguire quindi il comando [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator) usando solo uno dei parametri seguenti:
    >
    >     ```
    >     Add-AadrmRoleBasedAdministrator -EmailAddress <email address> -Role "ConnectorAdministrator"
    >     ```
    >
    >     ```
    >     Add-AadrmRoleBasedAdministrator -ObjectId <object id> -Role "ConnectorAdministrator"
    >     ```
    >
    >     ```
    >     Add-AadrmRoleBasedAdministrator -SecurityGroupDisplayName <group Name> -Role "ConnectorAdministrator"
    >     ```
    >     Ad esempio, digitare: **Add-AadrmRoleBasedAdministrator -EmailAddress melisa@contoso.com -Role "ConnectorAdministrator"**
    >
    >     Anche se questi comandi assegnano il ruolo di amministratore di connettore, è possibile usare anche il ruolo GlobalAdministrator.

Durante il processo di installazione del connettore RMS, vengono eseguite la convalida e l'installazione di tutti i prerequisiti software, l'installazione di Internet Information Services (se non già presente nel sistema) e l'installazione e configurazione del software del connettore. Viene anche preparata la configurazione di Azure RMS con la creazione degli elementi seguenti:

-   Una tabella vuota relativa ai server autorizzati a usare il connettore per le comunicazioni con Azure RMS. I server vengono aggiunti alla tabella in un secondo momento.

-   Un set di token di sicurezza per il connettore, che autorizzano operazioni con Azure RMS. Questi token vengono scaricati da Azure RMS e installati nel computer locale nel Registro di sistema. Sono protetti tramite l’interfaccia di programmazione dell’applicazione di protezione dei dati (DPAPI) e le credenziali dell'account Sistema locale.

Nella pagina finale della procedura guidata, eseguire le operazioni indicate di seguito e fare clic su **Fine**:

-   Se si è installato il primo connettore, non selezionare l'opzione **Avvia console di amministrazione del connettore per autorizzare i server** . Questa opzione, infatti, deve essere selezionata dopo l'installazione del secondo (o dell'ultimo) connettore RMS. È invece necessario eseguire di nuovo la procedura guidata su almeno un altro computer. Installare almeno due connettori.

-   Se si è installato il secondo (o l'ultimo) connettore, selezionare l'opzione **Avvia console di amministrazione del connettore per autorizzare i server**.

> [!TIP]
> A questo punto, è possibile eseguire un test di verifica per testare l'operatività dei servizi Web per il connettore RMS:
>
> -   Da un Web browser, connettersi a **http://&lt;indirizzoconnettore&gt;/_wmcs/certification/servercertification.asmx**, sostituendo *&lt;indirizzoconnettore&gt;* con l'indirizzo o il nome del server in cui è installato il connettore RMS. Se la connessione ha esito positivo, viene visualizzata una pagina **ServerCertificationWebService** .

Se è necessario disinstallare il connettore RMS, eseguire di nuovo la procedura guidata e selezionare l'opzione per la disinstallazione.

Se si verificano problemi durante l'installazione, controllare il log di installazione: **%LocalAppData%\Temp\Microsoft Rights Management connector_\<data e ora>.log** 

Ad esempio, il log di installazione potrebbe essere simile a C:\Users\Administrator\AppData\Local\Temp\Microsoft Rights Management connector_20170803110352.log

## <a name="authorizing-servers-to-use-the-rms-connector"></a>Autorizzazione dei server all'uso del connettore RMS
Dopo aver installato il connettore RMS in almeno due computer, è possibile autorizzare all'uso del connettore i server e i servizi desiderati, ad esempio i server che eseguono Exchange Server 2013 o SharePoint Server 2013.

Per definire tali server, eseguire lo strumento di amministrazione di connettore RMS e aggiungerli all'elenco dei server autorizzati. È possibile eseguire questo strumento quando si seleziona **Avvia console di amministrazione del connettore per autorizzare i server** al termine dell'installazione guidata del connettore Microsoft Rights Management. In alternativa, è possibile eseguirlo in modo separato dalla procedura guidata.

Quando si autorizzano i server, tenere presente quanto segue:

- I server aggiunti all'elenco godono di privilegi speciali. A tutti gli account specificati per il ruolo Exchange Server nella configurazione del connettore viene concesso il [ruolo utente con privilegi avanzati](configure-super-users.md) in Azure RMS, che consente l'accesso a tutto il contenuto per questo tenant di RMS. La funzionalità di utente con privilegi avanzati viene attivata automaticamente a questo punto, se necessario. Per evitare i rischi per la sicurezza dovuti all'elevazione dei privilegi, specificare solo gli account usati dai server di Exchange dell'organizzazione. A tutti i server configurati come server di SharePoint o file server che usano FCI vengono concessi i privilegi di utente normale.

- È possibile aggiungere più server all'elenco come voce singola specificando un gruppo di Active Directory di sicurezza o di distribuzione oppure un account del servizio usato da più di un server. Se si usa questa configurazione i server del gruppo condividono gli stessi certificati RMS e sono considerati tutti proprietari del contenuto protetto da ognuno di essi. Per ridurre il sovraccarico amministrativo, per autorizzare i server di Exchange dell'organizzazione o una server farm di SharePoint si consiglia di usare la configurazione di un gruppo anziché singoli server.

Nella pagina **Server a cui è consentito l'uso del connettore** , fare clic su **Aggiungi**.

> [!NOTE]
> L’autorizzazione dei server in Azure RMS è la configurazione equivalente alla configurazione di AD RMS quando si applicano manualmente i diritti NTFS a ServerCertification.asmx per gli account di servizio o del computer server e si concedono manualmente diritti di utente con privilegi avanzati agli account di Exchange. L'applicazione dei diritti NTFS a ServerCertification.asmx non è necessaria per il connettore.


### <a name="add-a-server-to-the-list-of-allowed-servers"></a>Aggiunta di un server all'elenco dei server autorizzati
Nella pagina **Consenti a un server di utilizzare il connettore** immettere il nome dell'oggetto oppure individuare e selezionare l'oggetto da autorizzare.

È importante autorizzare l'oggetto corretto. Per consentire a un server di usare il connettore, è necessario selezionare per l'autorizzazione l'account che esegue il servizio locale, ad esempio Exchange o SharePoint. Se, ad esempio, il servizio viene eseguito come account del servizio, aggiungere all'elenco il nome del servizio. Se il servizio viene eseguito come sistema locale, aggiungere il nome dell'oggetto computer, ad esempio SERVERNAME$. Si consiglia di creare un gruppo contenente gli account e di specificare tale gruppo anziché i nomi dei singoli server.

Di seguito sono riportate altre informazioni sui diversi ruoli server:

-   Per i server che eseguono Exchange: è necessario specificare un gruppo di sicurezza ed è possibile usare il gruppo predefinito (**Server Exchange**) creato automaticamente da Exchange e che gestisce tutti i server di Exchange della foresta.

-   Per i server che eseguono SharePoint:

    -   Se si configura un server SharePoint 2010 in modo che venga eseguito come sistema locale (non usando un account del servizio), creare manualmente un gruppo di sicurezza nei Servizi di dominio Active Directory e aggiungere a questo gruppo l'oggetto nome computer per il server in questa configurazione.

    -   Se un server SharePoint è configurato per l'uso di un account del servizio (procedura consigliata per SharePoint 2010 e unica opzione possibile per SharePoint 2016 e SharePoint 2013), procedere come segue:

        1.  Aggiungere l'account del servizio che esegue Amministrazione centrale SharePoint per abilitare la configurazione di SharePoint dalla relativa console di amministrazione.

        2.  Aggiungere l'account configurato per il pool di applicazioni di SharePoint.

        > [!TIP]
        > Se i due account sono diversi, per ridurre il sovraccarico amministrativo è consigliabile creare un singolo gruppo che li contenga entrambi.

-   Per i file server che usano la funzionalità Infrastruttura di classificazione file, i servizi associati vengono eseguiti come account di sistema locale. È quindi necessario autorizzare l'account del computer per i file server (ad esempio SERVERNAME$) o un gruppo contenente tali account di computer.

Una volta completata l'aggiunta dei server all'elenco, fare clic su **Chiudi**.

Se non si è ancora provveduto, è ora necessario configurare il bilanciamento del carico per i server in cui è installato il connettore RMS. È inoltre opportuno valutare la possibilità di usare HTTPS per le connessioni tra questi server e i server appena autorizzati.

## <a name="configuring-load-balancing-and-high-availability"></a>Configurazione del bilanciamento del carico per elevati livelli di disponibilità
Dopo aver installato la seconda o l'ultima istanza del connettore RMS, definire il nome server dell'URL del connettore e configurare un sistema di bilanciamento del carico.

Il nome server dell'URL del connettore può essere qualsiasi nome incluso in uno spazio dei nomi controllato. È possibile, ad esempio, creare una voce nel sistema DNS per **rmsconnector.contoso.com** e configurarla per l'uso di un indirizzo IP nel sistema di bilanciamento del carico. Il nome non presenta requisiti speciali e non deve essere configurato sui server del connettore. Non è necessario che il nome sia risolvibile in Internet, a meno che i server di Exchange e SharePoint non comunichino con il connettore attraverso Internet.

> [!IMPORTANT]
> Si consiglia di non modificare il nome dopo aver configurato i server di Exchange o SharePoint per l'uso del connettore. Se si modificasse il nome, sarebbe infatti necessario eliminare tali server da tutte le configurazioni IRM e configurarli nuovamente.

Dopo aver creato un nome nel DNS e averlo configurato per un indirizzo IP, impostare il bilanciamento del carico per tale indirizzo, operazione che indirizza il traffico ai server del connettore. A tale scopo è possibile usare qualsiasi servizio di bilanciamento del carico, inclusa la funzionalità Bilanciamento carico di rete di Windows Server. Per altre informazioni, vedere la [guida di distribuzione relativa al bilanciamento del carico](https://technet.microsoft.com/library/cc754833%28v=WS.10%29.aspx).

Usare le impostazioni seguenti per configurare il cluster di Bilanciamento carico di rete:

-   Porte: 80 (per HTTP) o 443 (per HTTPS)

    Per altre informazioni sull'uso di HTTP o HTTPS, vedere la sezione successiva.

-   Gruppo di affinità: Nessuno

-   Metodo di distribuzione: Uguale

Questo nome definito per il sistema con carico bilanciato (per i server che eseguono il servizio del connettore RMS) è il nome del connettore RMS dell'organizzazione che viene usato in seguito quando si configurano i server locali per l'uso di Azure RMS.

## <a name="configuring-the-rms-connector-to-use-https"></a>Configurazione del connettore RMS per l'uso di HTTPS
> [!NOTE]
> Questo passaggio di configurazione è facoltativo, ma si consiglia di effettuarlo per ottenere una maggiore sicurezza.

Anche se TLS o SSL è facoltativo per il connettore RMS, se ne consiglia comunque l'uso per qualsiasi servizio basato su HTTP con esigenze particolari a livello di sicurezza. Questa configurazione esegue l'autenticazione dei server che eseguono il connettore ai server di Exchange e SharePoint che lo usano. Inoltre, tutti i dati inviati da questi server al connettore vengono crittografati.

Per abilitare il connettore RMS all'uso di TLS è necessario installare su ogni server che esegue tale connettore un certificato di autenticazione server contenente il nome usato per il connettore stesso. Se, ad esempio, il nome del connettore RMS definito nel DNS è **rmsconnector.contoso.com**, distribuire un certificato di autenticazione server che contiene **rmsconnector.contoso.com** come nome comune nel soggetto del certificato. In alternativa, specificare **rmsconnector.contoso.com** nel nome alternativo del certificato come valore DNS. Il certificato non deve includere il nome del server. In IIS, associare quindi il certificato al sito Web predefinito.

Se si usa l'opzione HTTPS, assicurarsi che tutti i server che eseguono il connettore dispongano di un certificato di autenticazione server valido concatenato a un'autorità di certificazione (CA) radice considerata attendibile dai server di Exchange e SharePoint dell'organizzazione. Inoltre, se l'autorità di certificazione (CA) che ha emesso i certificati per i server del connettore pubblica un elenco di revoche di certificati (CRL), è necessario che i server di Exchange e SharePoint siano in grado di scaricare tale CRL.

> [!TIP]
> Per richiedere e installare un certificato di autenticazione server e per associare quest'ultimo al sito Web predefinito in IIS, usare le informazioni e le risorse indicate di seguito:
>
> - Se per distribuire i certificati di autenticazione server si usano Servizi certificati Active Directory e un'autorità di certificazione (CA) globale (enterprise), è possibile duplicare e quindi usare il modello di certificato del server Web. Questo modello di certificato usa **Fornito nella richiesta** per il nome soggetto del certificato. Questo significa che, quando si richiede il certificato, è possibile fornire il nome di dominio completo del nome del connettore RMS come nome soggetto del certificato o come nome alternativo del soggetto.
> -   Se si usa una CA autonoma o si acquista il certificato da un'altra società, vedere la sezione relativa alla [configurazione dei certificati del server Internet (IIS 7)](https://technet.microsoft.com/library/cc731977%28v=ws.10%29.aspx) nella raccolta di documentazione relativa al [Server Web (IIS)](https://technet.microsoft.com/library/cc753433%28v=ws.10%29.aspx) su TechNet.
> - Per configurare IIS per l'uso del certificato, vedere la sezione relativa all'[Add a Binding to a Site (IIS 7)](https://technet.microsoft.com/library/cc731692.aspx) (Aggiungere un'associazione a un sito - IIS 7) nella raccolta di documentazione [Web Server (IIS)](https://technet.microsoft.com/library/cc753433%28v=ws.10%29.aspx) (Server Web - IIS) su TechNet.

## <a name="configuring-the-rms-connector-for-a-web-proxy-server"></a>Configurazione del connettore RMS per un server proxy Web
Se i server del connettore sono installati in una rete che non dispone di connettività Internet diretta e richiede la configurazione manuale di un server proxy Web per l'accesso a Internet in uscita, è necessario configurare il Registro di sistema dei server per il connettore RMS.

#### <a name="to-configure-the-rms-connector-to-use-a-web-proxy-server"></a>Per configurare il connettore RMS per l'uso di un server proxy Web

1.  Su ogni server che esegue il connettore RMS aprire un editor del Registro di sistema, ad esempio Regedit.

2.  Passare a **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\AADRM\Connector**

3.  Aggiungere il valore stringa **ProxyAddress**, quindi impostare i dati di questo valore su **http://&lt;MyProxyDomainOrIPaddress&gt;:&lt;MyProxyPort&gt;**

    Ad esempio: **http://proxyserver.contoso.com:8080**

4.  Chiudere l'editor del Registro di sistema, quindi riavviare il server o eseguire un comando IISReset per riavviare IIS.

## <a name="installing-the-rms-connector-administration-tool-on-administrative-computers"></a>Installazione dello strumento di amministrazione di connettore RMS su computer amministrativi
È possibile eseguire lo strumento di amministrazione di connettore RMS da un computer in cui non è installato tale connettore se il computer soddisfa i requisiti seguenti:

-   Un computer fisico o virtuale che esegue Windows Server 2012 o Windows Server 2012 R2 (tutte le edizioni), Windows Server 2008 R2 o Windows Server 2008 R2 Service Pack 1 (tutte le edizioni), Windows 8.1, Windows 8 o Windows 7.

-   Almeno 1 GB di RAM.

-   Almeno 64 GB di spazio su disco.

-   Almeno un'interfaccia di rete.

-   Accesso a Internet tramite un firewall o un proxy Web.

Per installare lo strumento di amministrazione di connettore RMS, eseguire i file seguenti:

-   Per un computer a 32 bit: RMSConnectorAdminToolSetup_x86.exe

-   Per un computer a 64 bit: RMSConnectorSetup.exe

Se non sono stati già scaricati questi file, è possibile farlo dall' [Area download Microsoft](https://go.microsoft.com/fwlink/?LinkId=314106).


## <a name="next-steps"></a>Passaggi successivi
Dopo l’installazione e la configurazione del connettore RMS, è possibile configurare i server locali per l'uso del connettore stesso. Passare a [Configurazione dei server per il connettore di Azure Rights Management](configure-servers-rms-connector.md).

