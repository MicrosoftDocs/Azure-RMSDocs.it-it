---
title: Requisiti per Azure Information Protection - Articolo completo
description: Identificare i prerequisiti per distribuire Azure Information Protection per l&quot;organizzazione.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 10cf9371-a61b-495f-9d42-898448806994
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 94259046ed2eb78bce9d7ce49a4dc3b9c99d55c3
ms.lasthandoff: 02/24/2017


---


# <a name="requirements-for-azure-information-protection"></a>Requisiti per Azure Information Protection

>*Si applica a: Azure Information Protection, Office 365*


Prima di distribuire Azure Information Protection per l'organizzazione, verificare di soddisfare i prerequisiti seguenti. 

|Requisito|Altre informazioni|
|---------------|--------------------|
|Una sottoscrizione di Azure Information Protection|Esaminare le [informazioni sulla sottoscrizione](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing) e l'[elenco delle funzionalità](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features) nel sito Azure Information Protection per verificare che la sottoscrizione dell'organizzazione includa le funzionalità di Azure Information Protection che si vogliono usare.|
|Azure Active Directory|Per supportare l'autenticazione utente per Azure Information Protection, un'organizzazione deve avere Azure Active Directory (Azure AD). Inoltre, se si vuole usare gli account utente dalla directory locale (AD DS), è necessario anche configurare l'integrazione delle directory.<br /><br />Gli account federati, ad esempio AD FS, devono usare l'autenticazione integrata di Windows. L'autenticazione basata su moduli non è supportata per Azure Information Protection.<br /><br />Multi-Factor Authentication (MFA) è supportato in Azure Information Protection quando si ha il software client richiesto e l'infrastruttura di supporto MFA è configurata correttamente.<br /><br />Per altre informazioni, vedere [Requisiti di Azure Active Directory per Azure Information Protection](requirements-azure-ad.md).|
|Dispositivi client|Gli utenti devono avere dispositivi client, quali computer o dispositivi mobili, che eseguono un sistema operativo che supporta Azure Information Protection.<br /><br />I dispositivi seguenti supportano il client di Azure Information Protection, che consente agli utenti di classificare ed etichettare i messaggi di posta elettronica e i documenti di Office:<br /><br />- Windows 10 (x86, x64)<br /><br />- Windows 8.1 (x86, x64)<br /><br />- Windows 8 (x86, x64)<br /><br />- Windows 7 Service Pack 1 (x86, x64)<br /><br />Quando questo client protegge i dati tramite il servizio Azure Rights Management, può essere utilizzato dagli stessi dispositivi (Windows, Mac, iOS, Android) che supportano il servizio Azure Rights Management. <br /><br />Per informazioni dettagliate sui dispositivi che supportano il servizio Azure Rights Management, vedere [Dispositivi client che supportano la protezione dati di Azure Rights Management](../get-started/requirements-client-devices.md).|
|Applicazioni|Il client di Azure Information Protection supporta l'assegnazione di etichette e la protezione dei file e dei messaggi di posta elettronica creati dalle applicazioni **Word**, **Excel**, **PowerPoint** e **Outlook** delle famiglie di prodotti Office seguenti:<br /><br />- Office Professional Plus 2016<br /><br />- Office Professional Plus 2013 con Service Pack 1<br /><br />- Office Professional Plus 2010<br /><br />Per informazioni sulle applicazioni che supportano il servizio Azure Rights Management, vedere [Applicazioni che supportano la protezione dati di Azure Rights Management](requirements-applications.md).|
|Infrastruttura in grado di supportare la connettività a Internet e ai servizi cloud dipendenti.|Se è presente un firewall o dispositivi di rete di protezione simili che devono essere configurati per consentire connessioni specifiche, vedere le informazioni relative ad **Azure Rights Management (RMS)** nella sezione [Portale e condivisione di Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#BKMK_Portal-identity) dell'articolo [URL e intervalli di indirizzi IP per Office 365](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).<br /><br />Usare le istruzioni in questo articolo per mantenersi aggiornati sulle modifiche apportate a queste informazioni tramite la sottoscrizione a un feed RSS.<br /><br />Oltre alle informazioni nell'articolo di Office, le istruzioni seguenti sono specifiche per Azure Information Protection:<br /><br />- Consentire il traffico HTTPS sulla porta TCP 443 per **api.informationprotection.azure.com**.<br /><br />- Non terminare la connessione TLS dal client al servizio, ad esempio per il controllo a livello di pacchetti. In questo modo viene interrotta l'associazione del certificato usata dai client RMS con le autorità di certificazione gestite da Microsoft per la protezione delle comunicazioni con Azure RMS.<br /><br />- Se si usa un proxy Web che richiede l'autenticazione, è necessario configurarlo per l'uso dell'autenticazione integrata di Windows con le credenziali di accesso di Active Directory dell'utente.|

Se si vuole usare il servizio Azure Rights Management di Azure Information Protection con server locali, sono supportati i prodotti seguenti:

-   Exchange Server

-   SharePoint Server

-   File server di Windows Server che supportano la funzionalità Infrastruttura di classificazione file

Per informazioni sui requisiti aggiuntivi per questo scenario, vedere [Server locali che supportano la protezione dati di Azure Rights Management](requirements-servers.md).

> [!IMPORTANT]
> Lo scenario di distribuzione seguente non è supportato, a meno che non si usi la protezione di AD RMS con Azure Information Protection (configurazione "hold your own key" o HYOK):
> 
> -   Esecuzione side-by-side di AD RMS e di Azure RMS nella stessa organizzazione, tranne che durante la migrazione, come descritto in [Migrazione da AD RMS ad Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).
> 
> È disponibile un percorso di migrazione supportato [da AD RMS ad Azure Information Protection](http://technet.microsoft.com/library/Dn858447.aspx) e da [Azure Information Protection ad AD RMS](http://msdn.microsoft.com/library/azure/dn629429.aspx). Se si distribuisce Azure Information Protection e poi si decide di interrompere l'uso del servizio cloud, vedere [Rimozione delle autorizzazioni e disattivazione di Azure Information Protection](../deploy-use/decommission-deactivate.md).

## <a name="azure-active-directory-requirements-for-azure-information-protection"></a>Requisiti di Azure Active Directory per Azure Information Protection

Per usare Azure Information Protection, è necessario avere una directory di Azure AD. L'account aziendale per questa directory consente di accedere al portale di Azure classico, in cui è possibile, ad esempio, configurare e gestire i modelli di Rights Management.

Se non si ha una sottoscrizione di Azure aziendale, è possibile ottenerne una registrandosi per una versione di valutazione gratuita: andare alla pagina [Introduzione - Microsoft Azure](https://account.windowsazure.com/organization) e seguire le istruzioni.

Per altre informazioni, vedere le risorse seguenti contenute nella documentazione di Azure Active Directory:

-   [Che cos'è una directory di Azure AD?](/active-directory/active-directory-whatis)

-   [Associare le sottoscrizioni di Azure ad Azure Active Directory](/active-directory/active-directory-how-subscriptions-associated-directory)

Se si vuole integrare la directory di Azure AD con le foreste di AD locali, vedere [Integrazione delle identità locali con Azure Active Directory](/active-directory/active-directory-aadconnect).

> [!NOTE]
> Se si hanno dispositivi mobili o computer Mac che eseguono l'autenticazione locale tramite AD FS o un provider di autenticazione equivalente:
> 
> -   È necessario usare AD FS nella versione server minima di **Windows Server 2012 R2** oppure un provider di autenticazione alternativo che supporti il protocollo OAuth 2.0.

### <a name="multi-factor-authentication-mfa-and-azure-information-protection"></a>Multi-Factor Authentication (MFA) e Azure Information Protection
Per usare Multi-Factor Authentication (MFA) con Azure Information Protection, è necessario almeno uno degli elementi seguenti:

-   Office 2013 (versione minima):

    -   Se si ha Office 2013, è necessario installare anche l'[aggiornamento del 9 giugno 2015 per Office 2013 (KB3054853)](https://support.microsoft.com/kb/3054853). Per altre informazioni su questo aggiornamento e su come l'autenticazione moderna porta Active Directory Authentication Library in Office 2013, vedere il post relativo all'[anteprima pubblica di autenticazione moderna di Office 2013 annunciata](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/) sul blog di Office.

-   Applicazione Rights Management sharing per Windows:

    -   È necessario avere installato la versione minima 1.0.1908.0, che può essere confermata tramite Pannello di controllo, Programmi e funzionalità. Per altre informazioni sull'applicazione, vedere [Applicazione Rights Management sharing per Windows](../rms-client/sharing-app-windows.md).

-   App di condivisione Rights Management per dispositivi mobili e computer Mac:

    -   Assicurarsi di avere la versione più recente installata. Il supporto di MFA è entrato nella versione di settembre 2015 dell’app di RMS sharing.

Quindi, configurare la soluzione MFA:

-   Per i tenant gestiti da Microsoft (si dispone di Azure Active Directory o Office 365):

    -   Configurare Azure MFA per forzare l'autenticazione a più fattori per gli utenti. Per istruzioni, vedere [Introduzione ad Azure Multi-Factor Authentication nel cloud](/multi-factor-authentication/multi-factor-authentication-get-started-cloud) nella documentazione di Multi-factor Authentication.

        Per altre informazioni su Azure MFA, vedere [Informazioni su Azure Multi-Factor Authentication](/multi-factor-authentication/multi-factor-authentication).

-   Per i tenant federativi (si gestiscono i server in locale):

    -   Configurare i server federativi per Azure Active Directory o Office 365. Ad esempio, se si usa AD FS, vedere [Configurare metodi di autenticazione aggiuntivi per ADFS](https://technet.microsoft.com/library/dn758113.aspx) su TechNet.

        Per altre informazioni su questo scenario, vedere il post relativo al [programma di gestione delle identità per Office 365](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/) sul blog di Office.

## <a name="client-devices-that-support-azure-rights-management-data-protection"></a>Dispositivi client che supportano la protezione dati di Azure Rights Management

Usare le sezioni seguenti per identificare i dispositivi che supportano il servizio Azure Rights Management, che garantisce la protezione dei dati per Azure Information Protection.

### <a name="computers"></a>Computer
I seguenti sistemi operativi per computer supportano il servizio Azure Rights Management:

-   **Windows 7** (x86, x64)

-   **Windows 8** (x86, x64)

-   **Windows 8.1** (x86, x64)

-   **Windows 10** (x86, x64)

-   **Mac OS X**: la versione minima di Mac OS X è 10.8 (Mountain Lion)

### <a name="mobile-devices"></a>Dispositivi mobili
I seguenti sistemi operativi per dispositivi mobili supportano il servizio Azure Rights Management:

-   **Windows Phone**: Windows Phone 8.1

-   **Telefoni e tablet Android**: la versione minima di Android è 4.0.3

-   **iPhone e iPad**: la versione minima di iOS è 7.0

-   **Tablet Windows**: Windows 10 Mobile e Windows 8.1 RT

## <a name="applications-that-support-azure-rights-management-data-protection"></a>Applicazioni che supportano la protezione dati di Azure Rights Management

Usare la tabella seguente per identificare le applicazioni che supportano il servizio Azure Rights Management (Azure RMS) a livello nativo, che garantisce la protezione dei dati per Azure Information Protection. 

Per queste applicazioni il supporto di Rights Management è perfettamente integrato mediante l'uso delle API di Rights Management per supportare le restrizioni di utilizzo. Queste applicazioni sono anche dette applicazioni abilitate per RMS.

Se non diversamente indicato, le funzionalità supportate sono valide sia per Azure RMS che per AD RMS. Per il supporto di AD RMS in iOS, Android, OS X e Windows Phone 8.1 è inoltre richiesta l'[estensione per dispositivi mobili Active Directory Rights Management Services](https://technet.microsoft.com/library/dn673574.aspx).

Informazioni sulle colonne della tabella:

-   **PDF protetto**: file caratterizzati dall'estensione ppdf e creati automaticamente quando si usa l'applicazione RMS sharing per condividere file di Office e file PDF tramite posta elettronica. L'applicazione RMS sharing e l'app Azure Information Protection per iOS e Android includono un lettore per i file PDF protetti. Se in precedenza sono stati creati file PDF protetti tramite Azure RMS o AD RMS, per continuare a leggere questi file su dispositivi Windows, iOS e Android, è possibile usare Foxit Reader e Nitro Pro.

-   **Posta elettronica**: i client di posta elettronica elencati possono proteggere il messaggio di posta elettronica stesso, proteggendo quindi automaticamente eventuali file allegati. In questo scenario la funzionalità di anteprima del client può mostrare il contenuto protetto (messaggio e allegato) ai destinatari autorizzati. Se tuttavia un messaggio di posta elettronica non è protetto ma lo è l'allegato, la funzionalità di anteprima del client non potrà mostrare l'allegato protetto ai destinatari autorizzati.

-   **Altri tipi di file**: file di testo e di immagine con estensioni quali txt, xml, jpg e jpeg. L'estensione cambia dopo che i file vengono protetti in modo nativo da Rights Management e diventano di sola lettura. I file che non possono essere protetti in modo nativo, dopo essere stati protetti in modo generico da Rights Management hanno un'estensione di tipo pfile. Per altre informazioni, vedere [Guida dell'amministratore dell'applicazione Rights Management sharing](../rms-client/sharing-app-admin-guide.md).


|**Sistema operativo dispositivo**|Word, Excel, PowerPoint|PDF protetto|Posta elettronica|Altri tipi di file|
|-------------------------------|---------------------------|-----------------|---------|--------------------|
|**Windows**|Office 2010<br /><br />Office 2013<br /><br />Office 2016 <br /><br />App Office Mobile (solo Azure RMS) [[1]](#footnote-1)<br /><br />Office Online [[2]](#footnote-2)|Gaaiho Doc<br /><br />GigaTrust Desktop PDF Client for Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br />App di condivisione RMS|Outlook 2010<br /><br />Outlook 2013<br /><br />Office 2016 <br /><br />Outlook Web App (OWA) [[3]](#footnote-3)<br /><br />Windows Mail [[4]](#footnote-4)|Applicazione RMS sharing per Windows: testo, immagini, pfile<br /><br />Siemens JT2Go: file JT (solo Windows 10)|
|**iOS**|Office per iPad e iPhone [[5]](#footnote-5)<br /><br />Office Online [[2]](#footnote-2)<br /><br />TITUS Docs|App Azure Information Protection [[1]](#footnote-1)<br /><br /> Foxit Reader<br /><br />TITUS Docs|App Azure Information Protection [[1]](#footnote-1)<br /><br />Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook per iPad e iPhone [[4]](#footnote-4)<br /><br />OWA per iOS [[3]](#footnote-3)<br /><br />TITUS Mail|App Azure Information Protection [[1]](#footnote-1): testo, immagini<br /><br />TITUS Docs: pfile|
|**Android**|GigaTrust App for Android<br /><br />Office Online [[2]](#footnote-2)<br /><br />Office Mobile (solo Azure RMS) [[1]](#footnote-1)|App Azure Information Protection [[1]](#footnote-1)<br /><br />GigaTrust App for Android<br /><br />Foxit Reader<br /><br />App RMS sharing [[1]](#footnote-1)|9Folders [[4]](#footnote-4)<br /><br />App Azure Information Protection [[1]](#footnote-1)<br /><br />GigaTrust App for Android [[4]](#footnote-4)<br /><br />Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook per Android [[4]](#footnote-4)<br /><br />OWA per Android [[3]](#footnote-3) e [[7]](#footnote-7)<br /><br />Samsung Email (S3 e versioni successive) [[7]](#footnote-7)<br /><br />Classificazione TITUS per dispositivi mobili|App Azure Information Protection [[1]](#footnote-1): testo, immagini|
|**OS X**|Office 2011 (solo AD RMS)<br /><br />Office 2016 per Mac<br /><br />Office Online [[2]](#footnote-2)|Foxit Reader<br /><br />App RMS sharing [[1]](#footnote-1)|Outlook 2011 (solo AD RMS)<br /><br />Outlook 2016 per Mac<br /><br />Outlook per Mac|App RMS sharing [[1]](#footnote-1): testo, immagini, pfile|
|**Windows 10 Mobile**|App Office Mobile (solo Azure RMS)[[1]](#footnote-1)|Non supportato|Citrix WorxMail [[6]](#footnote-6)<br /><br />Posta di Outlook|Non supportato|
|**Windows RT**|Office 2013 RT<br /><br />Office Online [[2]](#footnote-2)|Non supportato|Outlook 2013 RT<br /><br />App di posta elettronica per Windows<br /><br />Windows Mail [[4]](#footnote-4)|Siemens JT2Go: file JT|
|**Windows Phone 8.1**|Office Mobile (solo AD RMS)|App RMS sharing [[1]](#footnote-1)|Outlook Mobile [[4]](#footnote-4)|App RMS sharing [[1]](#footnote-1): testo, immagini, pfile|
|**Blackberry 10**|Non supportato|Non supportato|Posta elettronica Blackberry [[4]](#footnote-4)|Non supportato|


##### <a name="footnote-1"></a>Nota 1
supporta la visualizzazione di contenuti protetti.

##### <a name="footnote-2"></a>Nota 2 
Supporta la visualizzazione di documenti protetti quando un documento non protetto viene caricato in una raccolta protetta di SharePoint Online e OneDrive for Business. 

##### <a name="footnote-3"></a>Nota 3
Se un destinatario riceve un messaggio di posta elettronica protetto e non usa Exchange come server di posta elettronica oppure se il mittente appartiene a un'altra organizzazione, il contenuto può essere aperto solo con un client di posta elettronica come Outlook e non da Outlook Web Access.

##### <a name="footnote-4"></a>Nota 4
utilizza Exchange ActiveSync IRM, che deve essere abilitato dall'amministratore di Exchange. Gli utenti possono visualizzare, rispondere e rispondere a tutti per messaggi di posta elettronica protetti, ma gli utenti non possono proteggere i nuovi messaggi di posta elettronica da sé.

Se un destinatario riceve un messaggio di posta elettronica protetto e non usa Exchange come server di posta elettronica oppure se il mittente appartiene a un'altra organizzazione, il contenuto può essere aperto solo con un client di posta elettronica come Outlook Il contenuto non può essere aperto da Outlook Web Access o dai client di posta elettronica per dispositivi mobili con Exchange Active Sync IRM.

##### <a name="footnote-5"></a>Nota 5
supporta la visualizzazione e la modifica di documenti protetti. Per altre informazioni, vedere il post sul blog di Office relativo al [supporto per Azure Rights Management disponibile in Office per iPad e iPhone](https://blogs.office.com/2015/07/22/azure-rights-management-support-comes-to-office-for-ipad-and-iphone-2/)

##### <a name="footnote-6"></a>Nota 6
Per altre informazioni, vedere la [documentazione del prodotto Citrix per WorxMail](http://docs.citrix.com/en-us/worx-mobile-apps/10/xmob-worx-mail.html).

##### <a name="footnote-7"></a>Nota 7
Per altre informazioni, vedere il post sul blog di Office relativo a [OWA per Android ora disponibile su dispositivi specifici](http://blogs.office.com/2014/06/11/owa-for-android-now-available-on-select-devices/)

## <a name="more-information-about-azure-rms-support-for-office"></a>Altre informazioni sul supporto di Azure RMS per Office

Azure RMS si integra perfettamente nelle applicazioni Word, Excel, PowerPoint e Outlook, dove questa funzionalità viene spesso denominata Information Rights Management (IRM). Le seguenti edizioni di client di Office supportano la protezione dei file e dei messaggi di posta elettronica tramite Azure RMS:

- Office Professional Plus 2016

- Office Professional Plus 2013

- Office Professional Plus 2010

Tutte le edizioni di Office, ad eccezione di Office 2007, possono utilizzare il contenuto protetto.

Azure RMS con Office Professional Plus 2010 oppure Office Professional 2010:

- Richiede l'applicazione Rights Management sharing per Windows

- Non supportato in Windows 10

### <a name="more-information-about-the-azure-information-protection-app-for-ios-and-android"></a>Altre informazioni sull'app Azure Information Protection per iOS e Android

L'app Azure Information Protection per iOS e Android sostituisce l'app RMS sharing per questi dispositivi. Offre la stessa funzionalità e inoltre supporta i messaggi di posta elettronica e i file PDF protetti da diritti in SharePoint Online.

Se i dispositivi iOS e Android sono registrati da Microsoft Intune, è possibile distribuire e gestire l'app tramite un'app gestita da criteri. Per altre informazioni, vedere l'articolo relativo alla [configurazione e distribuzione dei criteri di gestione delle applicazioni per dispositivi mobili nella console di Microsoft Intune](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console) nella documentazione di Intune Per il Passaggio 2 di questa documentazione di Intune, usare le istruzioni per pubblicare un'app gestita da criteri.

Per altre informazioni, vedere [Domande frequenti sull'app Azure Information Protection per iOS e Android](../rms-client/mobile-app-faq.md).


### <a name="more-information-about-the-rights-management-sharing-application"></a>Altre informazioni sull'applicazione Rights Management sharing

Per altre informazioni sull'applicazione Rights Management sharing per Windows, vedere le risorse seguenti:

-   [Guida dell'amministratore dell'applicazione di condivisione Rights Management](../rms-client/sharing-app-admin-guide.md)

-   [Guida dell'utente dell'applicazione di condivisione Rights Management](../rms-client/sharing-app-user-guide.md)

Per altre informazioni sull'applicazione Rights Management sharing per piattaforme mobili, vedere le risorse seguenti:

-   Per scaricare l'applicazione desiderata, fare clic sul collegamento corrispondente nella pagina [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970)

-   [Domande frequenti sull'applicazione di condivisione Microsoft Rights Management per piattaforme mobili](https://technet.microsoft.com/dn451248)

> [!NOTE]
> L'applicazione RMS sharing per iOS e Android è stata sostituita dall'app Azure Information Protection.

### <a name="more-information-about-other-applications-that-support-azure-rms"></a>Altre informazioni su ulteriori applicazioni che supportano Azure RMS

Oltre alle applicazioni riportate nella tabella, è possibile integrare con Azure RMS le applicazioni che supportano le API RMS, tra cui:

- Applicazioni line-of-business create internamente mediante RMS SDK

- Applicazioni di fornitori di software create mediante RMS SDK

Per altre informazioni sull'SDK, vedere la pagina relativa a [Microsoft Rights Management SDK](../develop/developers-guide.md).

### <a name="applications-that-are-not-supported-by-azure-rms"></a>Applicazioni non supportate da Azure RMS

Le applicazioni chi non sono attualmente supportate da Azure RMS sono le seguenti:

-   Microsoft Office per Mac 2011

-   Microsoft OneDrive for Business per SharePoint Server 2013

-   XPS Viewer
 
L'applicazione RMS sharing prevede inoltre le restrizioni seguenti:

-   Per i computer Windows, la versione minima richiesta è Windows 7 Service Pack 1

## <a name="on-premises-servers-that-support-azure-rights-management-data-protection"></a>Server locali che supportano la protezione dati di Azure Rights Management

I prodotti server locali seguenti sono supportati con Azure Information Protection quando si usa il connettore di Azure Rights Management. Il connettore funziona come interfaccia di comunicazione (inoltro) tra i server locali e il servizio Azure Rights Management che è usato da Azure Information Protection per proteggere messaggi di posta elettronica e documenti di Office. 

Per usare questo connettore, è necessario configurare la sincronizzazione delle directory tra le foreste Active Directory e Azure Active Directory.

-   **Exchange Server**:

    -   Exchange Server 2016

    -   Exchange Server 2013

    -   Exchange Server 2010

-   **Office SharePoint Server**:

    -   Office SharePoint Server 2016

    -   Office SharePoint Server 2013

    -   Office SharePoint Server 2010

-   **File server che eseguono Windows Server e usano la funzionalità Infrastruttura di classificazione file (FCI, File Classification Infrastructure)**:

    -   Windows Server 2012 R2

    -   Windows Server 2012

    > [!NOTE]
    > Poiché i file server che eseguono Windows Server 2008 R2 non includono un'azione predefinita per le attività di gestione file per l'applicazione della protezione Rights Management, non sarà possibile usare il connettore di Rights Management per questo scenario. È tuttavia possibile usare Infrastruttura di classificazione file e Azure RMS in questi sistemi operativi se si configura un'attività personalizzata di gestione file per l'esecuzione di un file eseguibile o di uno script in grado di proteggere i file tramite Azure RMS. Ad esempio, uno script di Windows PowerShell che usa i [cmdlet di protezione RMS](https://msdn.microsoft.com/library/azure/mt433195.aspx).
    > 
    > È inoltre possibile utilizzare questi cmdlet con server che eseguono versioni successive di Windows Server, con il vantaggio che questi cmdlet possono proteggere tutti i tipi di file. Il connettore RMS protegge solo i file di Office. Per le istruzioni d'uso, vedere [Protezione RMS con l'infrastruttura di classificazione file (FCI, File Classification Infrastructure) per Windows Server&#40;FCI&#41;](../rms-client/configure-fci.md).

Il connettore di Rights Management è supportato in Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2.

Per altre informazioni sulla modalità di configurazione del connettore di Rights Management per questi server locali, vedere [Distribuzione del connettore di Azure Rights Management](../deploy-use/deploy-rms-connector.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

