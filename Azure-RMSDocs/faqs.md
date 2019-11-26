---
title: Domande frequenti su Azure Information Protection
description: Some frequently asked questions about Azure Information Protection and its protection service, Azure Rights Management (Azure RMS).
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/25/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: f4583260708267575f35d4c67d6cd2afc5add68d
ms.sourcegitcommit: fed1df1858f8316f7dd45e751c6910b444651a87
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/25/2019
ms.locfileid: "74474345"
---
# <a name="frequently-asked-questions-for-azure-information-protection"></a>Domande frequenti su Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Di seguito sono riportate alcune possibili domande su Azure Information Protection o sul servizio Azure Rights Management (Azure RMS) e le relative risposte.

La pagina delle domande frequenti viene aggiornata periodicamente e le nuove aggiunte vengono pubblicate negli annunci mensili di aggiornamento della documentazione nel [blog tecnico di Azure Information Protection](https://aka.ms/AIPblog).

## <a name="whats-the-difference-between-azure-information-protection-and-microsoft-information-protection"></a>Qual è la differenza tra Azure Information Protection e Microsoft Information Protection?

Diversamente da Azure Information Protection, Microsoft Information Protection non è una sottoscrizione o un prodotto che è possibile acquistare. Si tratta invece di un framework per prodotti e funzionalità integrate, che consente di proteggere le informazioni riservate dell'organizzazione:

- I singoli prodotti inclusi in questo framework sono Azure Information Protection, Office 365 Information Protection (ad esempio, Office 365 DLP), Windows Information Protection e Microsoft Cloud App Security. 

- Le funzionalità integrate in questo framework includono la gestione unificata delle etichette, esperienze di etichettatura per l'utente finale incorporate nelle app di Office, la capacità di Windows di comprendere le etichette unificate e applicare la protezione ai dati, Microsoft Information Protection SDK e nuove funzionalità in Adobe Acrobat Reader per visualizzare i documenti PDF etichettati e protetti.

Per altre informazioni, vedere [Announcing availability of information protection capabilities to help protect your sensitive data](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967) (Annuncio della disponibilità di funzionalità di protezione delle informazioni per proteggere i dati sensibili).

## <a name="whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365"></a>Qual è la differenza tra le etichette in Azure Information Protection e in Office 365?

Originariamente, Office 365 aveva solo [etichette di conservazione](https://support.office.com/article/af398293-c69d-465e-a249-d74561552d30) che consentivano di classificare documenti e messaggi di posta elettronica per il controllo e la conservazione quando il contenuto si trovava in servizi di Office 365. Le etichette in Azure Information Protection consentono invece di applicare criteri di classificazione e protezione coerenti per documenti e messaggi di posta elettronica, sia locali che nel cloud.

Announced at Microsoft Ignite 2018 in Orlando, you now have an option to create and configure [sensitivity labels](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels) in addition to retention labels in one of the admin centers: The Office 365 Security & Compliance Center, the Microsoft 365 security center, or the Microsoft 365 compliance center. You can migrate your existing Azure Information Protection labels to the new unified labeling store, to be used as sensitivity labels with Office apps. 

Per altre informazioni sulla gestione dell'etichettatura unificata e su come verranno supportate queste etichette, vedere il post di blog, [Announcing availability of information protection capabilities to help protect your sensitive data](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967) (Annuncio della disponibilità di funzionalità di protezione delle informazioni per proteggere i dati sensibili).

For more information about migrating your existing labels, see [How to migrate Azure Information Protection labels to unified sensitivity labels](configure-policy-migrate-labels.md).

## <a name="how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform"></a>How can I determine if my tenant is on the unified labeling platform?

When your tenant is on the unified labeling platform, sensitivity labels can be used by [clients and services that support unified labeling](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling). If you obtained your subscription for Azure Information Protection in June 2019 or later, your tenant is automatically on the unified labeling platform and no further action is needed. Your tenant might also be on this platform because somebody migrated your Azure Information Protection labels.

To check the status, in the Azure portal, go to **Azure Information Protection** > **Manage** > **Unified labeling**, and view the status of **Unified labeling**:

- If you see **Activated**, your tenant is on the unified labeling platform.

- If you see **Not activated**, your tenant is not on the unified labeling platform. For migration instructions, see [How to migrate Azure Information Protection labels to unified sensitivity labels](configure-policy-migrate-labels.md).

## <a name="whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client"></a>What's the difference between the Azure Information Protection client and the Azure Information Protection unified labeling client?

The **Azure Information Protection client (classic)** has been available since Azure Information Protection was first announced as a new service for classifying and protecting files and emails. This client downloads labels and policy settings from Azure, and you configure the Azure Information Protection policy from the Azure portal. For more information, see [Overview of the Azure Information Protection policy](overview-policy.md). 

The **Azure Information Protection unified labeling client** is a more recent addition, to support the unified labeling store that multiple applications and services support. This client downloads sensitivity labels and policy settings from the following admin centers: The Office 365 Security & Compliance Center, the Microsoft 365 security center, and the Microsoft 365 compliance center. For more information, see [Overview of sensitivity labels](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels).

If you're not sure which client to use, see [Choose which Azure Information Protection client to use](./rms-client/use-client.md#choose-which-labeling-client-to-use-for-windows-computers).

### <a name="identify-which-client-you-have-installed"></a>Identify which client you have installed

Both clients, when they are installed, display **Azure Information Protection**. To help you identify which client you have installed, use the **Help and feedback** option to open the **Microsoft Azure Information Protection** dialog box:

- Da Esplora file: fare clic con il pulsante destro del mouse su uno o più file o su una cartella, scegliere **Classifica e proteggi** e quindi **Guida e commenti**.

- From an Office application: From the **Protect** button (the classic client) or **Sensitivity** button (unified labeling client), select **Help and Feedback**.

Use the **Version** number displayed to identify the client:

- A version **1**, for example, **1.53.10.0**, identifies the Azure Information Protection client (classic).

- A version **2**, for example, **2.2.14.0**, identifies the Azure Information Protection unified labeling client.

## <a name="when-is-the-right-time-to-migrate-my-labels"></a>When is the right time to migrate my labels?

Now that the option to migrate labels in the Azure portal is in general availability, we recommend you activate the migration so that you can use your labels as sensitivity labels with [clients and services that support unified labeling](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling).

For more information and instructions, see [How to migrate Azure Information Protection labels to unified sensitivity labels](configure-policy-migrate-labels.md).

## <a name="after-ive-migrated-my-labels-which-management-portal-do-i-use"></a>Dopo aver eseguito la migrazione delle etichette, qual è il portale di gestione da usare?

Dopo aver eseguito la migrazione delle etichette nel portale di Azure:

- If you have [unified labeling clients and services](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling), go to one of the admin centers (Office 365 Security & Compliance Center, Microsoft 365 security center, or Microsoft 365 compliance center) to publish these labels, and to configure their policy settings. Per le modifiche delle etichette, da ora in poi usare uno di questi centri di amministrazione. I client di etichettatura unificata scaricano le etichette e le impostazioni dei criteri da uno di questi centri di amministrazione.

- If you have the [Azure Information Protection client (classic)](./rms-client/aip-client.md), continue to use the Azure portal to edit your labels and policy settings. The classic client continues to download labels and policy settings from Azure.

- If you have both [unified labeling clients](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling) and [classic clients](./rms-client/aip-client.md), you can use the admin centers or the Azure portal to make label changes. However, for the classic clients to pick up the label changes that you make in the admin centers, you must return to the Azure portal: Use the **Publish** option from the **Azure Information Protection - Unified labeling** pane in the Azure portal. 

Continuare a usare il portale di Azure per il [reporting centralizzato](reports-aip.md) e lo [scanner](deploy-aip-scanner.md).

## <a name="whats-the-difference-between-azure-information-protection-and-azure-rights-management"></a>Quale è la differenza tra Azure Information Protection e Azure Rights Management?

Azure Information Protection offre funzionalità per la classificazione, l'assegnazione di etichette e la protezione per i documenti e i messaggi di posta elettronica di un'organizzazione. La tecnologia di protezione è basata sul servizio Azure Rights Management, che è ora un componente di Azure Information Protection.

## <a name="whats-the-role-of-identity-management-for-azure-information-protection"></a>What's the role of identity management for Azure Information Protection?

Un utente deve avere un nome utente e una password validi per accedere al contenuto protetto da Azure Information Protection. Per altre informazioni su come Azure Information Protection consente di proteggere i dati, vedere [Il ruolo di Azure Information Protection nella protezione dei dati](/enterprise-mobility-security/solutions/azure-information-protection-securing-data). 

## <a name="what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included"></a>Quale sottoscrizione è necessaria per Azure Information Protection e quali funzionalità sono incluse?

Vedere le informazioni sulla sottoscrizione e l'elenco delle funzionalità nella pagina [Prezzi di Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection).

Se si ha un abbonamento a Office 365 che include la protezione dei dati di Azure Rights Management, scaricare il [foglio dati di licenza di Azure Information Protection](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

Per altre domande sulle licenze, cercare le risposte nella sezione [Domande frequenti sulle licenze](https://azure.microsoft.com/pricing/details/information-protection#faq).

## <a name="is-the-azure-information-protection-client-only-for-subscriptions-that-include-classification-and-labeling"></a>Il client Azure Information Protection è disponibile solo per le sottoscrizioni che includono la classificazione e l'assegnazione di etichette?

No. The Azure Information Protection client (classic) can also be used with subscriptions that include just the Azure Rights Management service to protect data.

When the classic client is installed and it doesn't have an Azure Information Protection policy, this client automatically operates in [protection-only mode](./rms-client/client-protection-only-mode.md). In questa modalità gli utenti possono applicare facilmente modelli di Rights Management e autorizzazioni personalizzate. Se successivamente si acquista una sottoscrizione che include la classificazione e l'assegnazione di etichette, il client passa automaticamente alla modalità standard durante il download dei criteri di Azure Information Protection.

## <a name="do-you-need-to-be-a-global-admin-to-configure-azure-information-protection-or-can-i-delegate-to-other-administrators"></a>È necessario essere un amministratore globale per configurare Azure Information Protection oppure tale configurazione può essere delegata ad altri amministratori?

Gli amministratori globali per un tenant di Office 365 o di Azure AD possono ovviamente eseguire tutte le attività amministrative per Azure Information Protection. Se tuttavia si vogliono assegnare autorizzazioni amministrative ad altri utenti, sono disponibili le opzioni seguenti:

- **Azure Information Protection administrator**: This Azure Active Directory administrator role lets an administrator configure Azure Information Protection but not other services. Un amministratore con questo ruolo può attivare e disattivare il servizio di protezione Azure Rights Management, configurare le etichette e le impostazioni di protezione e configurare i criteri di Azure Information Protection. In addition, an administrator with this role can run all the PowerShell cmdlets for the [Azure Information Protection client](./rms-client/client-admin-guide-powershell.md) and from the [AIPService module](administer-powershell.md). However, this role doesn't support tracking and revoking documents for users.
    
    > [!NOTE]
    > This role is not supported in the Azure portal if your tenant is on the [unified labeling platform](#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform).
    
    Per assegnare un utente a questo ruolo amministrativo, vedere [Assegnare un utente ai ruoli di amministratore in Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal).

- **Compliance administrator** or **Compliance data administrator**: These Azure Active Directory administrator roles let an administrator configure Azure Information Protection, which includes activate and deactivate the Azure Rights Management protection service, configure protection settings and labels, and configure the Azure Information Protection policy. In addition, an administrator with either of these roles can run all the PowerShell cmdlets for the [Azure Information Protection client](./rms-client/client-admin-guide-powershell.md) and from the [AIPService module](administer-powershell.md). However, these roles don't support tracking and revoking documents for users.
    
    To assign a user to one of these administrative roles, see [Assign a user to administrator roles in Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal). To see what other permissions a user with these roles have, see the [Available roles](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles) section from the Azure Active Directory documentation.

- **Security reader** or **Global reader**: For [Azure Information Protection analytics](reports-aip.md) only. Questo ruolo di amministratore di Azure Active Directory consente agli amministratori di visualizzare come vengono usate le etichette, monitorare l'accesso degli utenti ai documenti e ai messaggi di posta elettronica etichettati ed eventuali modifiche della classificazione, nonché di identificare documenti che contengono informazioni sensibili che devono essere protette. Because this feature uses Azure Monitor, you must also have a supporting [RBAC role](reports-aip.md#permissions-required-for-azure-information-protection-analytics).
    
    > [!NOTE]
    > The Security reader and Global reader roles are not supported if your tenant is on the [unified labeling platform](#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform).

- **Security administrator**: This Azure Active Directory administrator role lets an administrator configure Azure Information Protection in the Azure portal, in addition to configuring some aspects of other Azure services. An administrator with this role cannot run any of the [PowerShell cmdlets from the AIPService module](administer-powershell.md), or track and revoke documents for users.
    
    Per assegnare un utente a questo ruolo amministrativo, vedere [Assegnare un utente ai ruoli di amministratore in Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal). Per conoscere le altre autorizzazioni di cui dispone un utente con questo ruolo, vedere la sezione [Ruoli disponibili](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles) della documentazione di Azure Active Directory.

- Azure Rights Management **Global Administrator** and **Connector Administrator**: For these Azure Rights Management administrator roles, the first grants users permissions to run all [PowerShell cmdlets from the AIPService module](administer-powershell.md) without making them a global administrator for other cloud services, and the second role grants permissions to run only the Rights Management (RMS) connector. Neither of these administrative roles grant permissions to management consoles or tracking and revoking documents for users.
    
    To assign either of these administrative roles, use the AIPService PowerShell cmdlet, [Add-AipServiceRoleBasedAdministrator](/powershell/module/aipservice/add-aipservicerolebasedadministrator).

Alcune osservazioni:

- Microsoft accounts are not supported for delegated administration of Azure Information Protection, even if these accounts are assigned to one of the administrative roles listed. 

- Se i [controlli di onboarding](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) sono stati configurati, ciò non influisce sulla possibilità di amministrare Azure Information Protection, fatta eccezione per il connettore RMS. Ad esempio, se i controlli di selezione sono stati configurati in modo da limitare la protezione del contenuto al gruppo "Reparto IT", l'account usato per installare e configurare il connettore RMS deve essere membro di tale gruppo. 

- Gli utenti a cui è assegnato un ruolo amministrativo non possono rimuovere automaticamente la protezione dai documenti o dai messaggi di posta elettronica che sono stati protetti tramite Azure Information Protection. Possono farlo solo gli utenti a cui è assegnato il ruolo di utente con privilegi avanzati, e solo quando la funzionalità utente con privilegi avanzati è abilitata. Tuttavia, tutti gli utenti a cui si assegnano autorizzazioni amministrative per Azure Information Protection possono assegnare il ruolo di utente con privilegi avanzati a qualsiasi utente, compreso il proprio account. Possono anche abilitare la funzionalità utente con privilegi avanzati. Queste azioni vengono registrate in un registro amministratore. For more information, see the security best practices section in [Configuring super users for Azure Information Protection and discovery services or data recovery](configure-super-users.md). 

- If you are migrating your Azure Information Protection labels to the unified labeling store, be sure to read the following section from the label migration documentation: [Administrative roles that support the unified labeling platform](configure-policy-migrate-labels.md#administrative-roles-that-support-the-unified-labeling-platform).

## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>Azure Information Protection supporta scenari locali e ibridi?

Sì. Anche se è una soluzione basata sul cloud, Azure Information Protection può classificare, etichettare e proteggere documenti e messaggi di posta elettronica archiviati in locale, oltre che nel cloud.

Se si ha Exchange Server, SharePoint Server e file server Windows, è possibile distribuire il [connettore Rights Management](deploy-rms-connector.md) per consentire a questi server locali di usare il servizio Azure Rights Management per proteggere messaggi di posta elettronica e documenti. È inoltre possibile sincronizzare ed eseguire la federazione dei controller di dominio di Active Directory con Azure AD per un'esperienza di autenticazione più semplice per gli utenti, ad esempio usando [Azure AD Connect](/azure/active-directory/hybrid/whatis-azure-ad-connect).

Il servizio Azure Rights Management genera e gestisce automaticamente i certificati XrML come richiesto e quindi non usa un'infrastruttura PKI locale. Per altre informazioni sull'uso dei certificati in Azure Rights Management, vedere la sezione [Procedura dettagliata del funzionamento di Azure RMS: primo uso, protezione dei contenuti, utilizzo del contenuto](./how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) nell'articolo [Funzionamento di Azure RMS](./how-does-it-work.md).

## <a name="what-types-of-data-can-azure-information-protection-classify-and-protect"></a>Quali tipi di dati è possibile classificare e proteggere tramite Azure Information Protection?

Azure Information Protection consente di classificare e proteggere messaggi di posta elettronica e documenti, sia in locale che nel cloud. Questi documenti includono documenti di Word, fogli di calcolo di Excel, presentazioni di PowerPoint, documenti PDF, file di testo e file di immagine. Per un elenco dei tipi di documenti supportati, vedere l'elenco dei [tipi di file supportati](./rms-client/clientv2-admin-guide-file-types.md) nella Guida dell'amministratore.

Azure Information Protection cannot classify and protect structured data such as database files, calendar items, Yammer posts, Sway content, and OneNote notebooks.

**Newly announced in preview**: Power BI now supports classification by using sensitivity labels and can apply protection from those labels to data that is exported to the following file formats: .pdf, .xls, and .ppt. For more information, see [Data protection in Power BI (preview)](https://docs.microsoft.com/power-bi/admin/service-security-data-protection-overview).

## <a name="i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work"></a>Azure Information Protection è elencata come un'app cloud disponibile per l'accesso condizionale, come funziona?

Nell'offerta di anteprima è ora possibile configurare l'accesso condizionale di Azure Active Directory per Azure Information Protection.

Quando un utente apre un documento protetto da Azure Information Protection, gli amministratori possono ora bloccare o concedere l'accesso agli utenti nel tenant, in base ai controlli di accesso condizionale standard. La richiesta di autenticazione a più fattori (MFA) è una delle condizioni più comunemente richieste. Un'altra è che i dispositivi siano [conformi ai criteri di Intune](/intune/conditional-access-intune-common-ways-use) in modo che, ad esempio, i dispositivi mobili soddisfino i requisiti relativi alle password e possiedano una versione minima del sistema operativo e i computer siano appartenenti a un dominio.

Per altre informazioni ed esempi di procedura dettagliata, vedere il post del blog [Conditional Access policies for Azure Information Protection](https://cloudblogs.microsoft.com/enterprisemobility/2017/10/17/conditional-access-policies-for-azure-information-protection/) (Criteri di accesso condizionale per Azure Information Protection).

Altre informazioni:

- Per i computer Windows: per la versione di anteprima corrente vengono valutati i criteri di accesso condizionale per Azure Information Protection quando [viene inizializzato l'ambiente utente](./how-does-it-work.md#initializing-the-user-environment) (questo processo è noto anche come bootstrap) e in seguito ogni 30 giorni.

- È possibile ottimizzare la frequenza con cui vengono valutati i criteri di accesso condizionale. A questo scopo è possibile configurare la durata del token. Per altre informazioni, vedere [Durata dei token configurabili in Azure Active Directory](/azure/active-directory/active-directory-configurable-token-lifetimes).

- We recommend that you do not add administrator accounts to your conditional access policies because these accounts will not be able to access the Azure Information Protection pane in the Azure portal.

- Se si usa l'autenticazione a più fattori nei criteri di accesso condizionale per la collaborazione con altre organizzazioni (B2B), è necessario usare la [collaborazione B2B di Azure AD](/azure/active-directory/b2b/what-is-b2b) e creare account guest per gli utenti con cui si vuole procedere alla condivisione nell'altra organizzazione.

- Con la versione di anteprima di dicembre 2018 di Azure Active Directory è ora possibile richiedere agli utenti di accettare le condizioni per l'utilizzo prima di aprire per la prima volta un documento protetto. For more information, see the following blog post announcement: [Updates to Azure AD Terms of Use functionality within conditional access](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Updates-to-Azure-AD-Terms-of-Use-functionality-within/ba-p/294822)

- Se si usano numerose app cloud per l'accesso condizionale, si potrebbe riscontrare che l'app **Microsoft Azure Information Protection** non viene visualizzata nell'elenco per la selezione. In questo caso, usare la casella di ricerca nella parte superiore dell'elenco. Iniziare a digitare "Microsoft Azure Information Protection" per filtrare le app disponibili. Se si ha una sottoscrizione supportata, l'app **Microsoft Azure Information Protection** verrà quindi visualizzata per la selezione. 

## <a name="i-see-azure-information-protection-is-listed-as-a-security-provider-for-microsoft-graph-securityhow-does-this-work-and-what-alerts-will-i-receive"></a>Azure Information Protection è elencato come provider di sicurezza per l'API Sicurezza di Microsoft Graph: come funziona e quali avvisi verranno inviati?

Nell'ambito dell'anteprima pubblica offerta è ora possibile ricevere un avviso per le **anomalie nell'accesso ai dati di Azure Information Protection**. Questo avviso viene attivato quando si verificano tentativi insoliti di accesso ai dati protetti da Azure Information Protection, ad esempio l'accesso a un volume insolitamente elevato di dati, in orari anomali o da una posizione sconosciuta.

Tali avvisi possono essere utili per rilevare gli attacchi avanzati relativi ai dati e le minacce interne nell'ambiente. Questi avvisi usano l'apprendimento automatico per analizzare il comportamento degli utenti che accedono ai dati protetti. 

È possibile accedere agli avvisi di Azure Information Protection [tramite l'API Sicurezza di Microsoft Graph](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/security-api-overview) oppure è possibile [trasmettere avvisi](https://developer.microsoft.com/graph/docs/concepts/security_siemintegration) a soluzioni SIEM come Splunk e IBM Qradar tramite Monitoraggio di Azure.

Per altre informazioni sull'API Sicurezza di Microsoft Graph, vedere [Microsoft Graph Security API overview](https://developer.microsoft.com/graph/docs/concepts/security-concept-overview) (Panoramica dell'API Sicurezza di Microsoft Graph).

## <a name="whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner"></a>Qual è la differenza tra Infrastruttura di classificazione file di Windows Server e lo scanner di Azure Information Protection?

L'infrastruttura di classificazione file di Windows Server è stata storicamente un'opzione per classificare i documenti e quindi proteggerli tramite il [connettore Rights Management](deploy-rms-connector.md) (solo documenti di Office) o uno [script di PowerShell](./rms-client/configure-fci.md) (tutti i tipi di file). 

Si consiglia ora di usare lo [scanner di Azure Information Protection](deploy-aip-scanner.md). Lo scanner usa il client Azure Information Protection e i criteri di Azure Information Protection per assegnare etichette ai documenti (tutti i tipi di file) in modo che questi documenti possano essere poi classificati e, facoltativamente, protetti.

Le differenze principali tra queste due soluzioni sono le seguenti:

|Infrastruttura di classificazione file di Windows Server|Scanner di Azure Information Protection|
|--------------------------------|-------------------------------------|
|Archivi dati supportati: <br /><br />- Cartelle locali in Windows Server|Archivi dati supportati: <br /><br />- Cartelle locali in Windows Server<br /><br />- Condivisione file di Windows e NAS (Network-Attached Storage)<br /><br />- SharePoint Server 2016 e SharePoint Server 2013. Anche SharePoint Server 2010 è supportato per i clienti che dispongono del [supporto "Extended" per questa versione di SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).|
|Modalità operativa: <br /><br />- Tempo reale|Modalità operativa: <br /><br />- Ricerca per indicizzazione sistematica degli archivi dati, con esecuzione una tantum o ripetuta del ciclo|
|Supporto per i tipi di file: <br /><br />- Per impostazione predefinita, sono protetti tutti i tipi di file <br /><br />- Specifici tipi di file possono essere esclusi dalla protezione modificando il Registro di sistema|Supporto per i tipi di file: <br /><br />- I tipi di file Office e i documenti PDF sono protetti per impostazione predefinita <br /><br />- Altri tipi di file possono essere inclusi nella protezione modificando il Registro di sistema|

There is a difference in setting the [Rights Management owner](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner) for files that are protected on a local folder or network share. Per impostazione predefinita, per entrambe le soluzioni, il proprietario di Rights Management viene impostato sull'account che protegge il file, ma è possibile sostituire questa impostazione:

- Per Infrastruttura di classificazione file di Windows Server è possibile impostare il proprietario di Rights Management su un singolo account per tutti i file o impostare in modo dinamico il proprietario di Rights Management per ogni file. Per impostare in modo dinamico il proprietario di Rights Management, usare il parametro **-OwnerMail [posta elettronica proprietario file di origine]** e relativo valore. Questa configurazione recupera l'indirizzo di posta elettronica dell'utente da Active Directory usando il nome dell'account utente specificato nella proprietà del proprietario del file.

- For the Azure Information Protection scanner: For newly protected files, you can set the Rights Management owner to be a single account for all files on a specified data store, but you cannot dynamically set the Rights Management owner for each file. Il proprietario di Rights Management non viene modificato per i file già protetti. Per impostare l'account per i file appena protetti, specificare l'impostazione **Proprietario predefinito** nel profilo dello scanner. 

Quando lo scanner protegge i file inclusi in siti e librerie di SharePoint, il proprietario di Rights Management viene impostato in modo dinamico per ogni file usando il valore Editor di SharePoint.

## <a name="ive-heard-a-new-release-is-going-to-be-available-soon-for-azure-information-protectionwhen-will-it-be-released"></a>Secondo alcune voci, sarà presto disponibile una nuova versione di Azure Information Protection. Quando verrà rilasciata?

La documentazione tecnica non contiene informazioni sulle versioni future. For this type of information, use the [Microsoft 365 Roadmap](https://www.microsoft.com/microsoft-365/roadmap?&filters=Azure%20Information%20Protection%2CO365%20Information%20Protection#owRoadmapMainContent), check the [Enterprise Mobility + Security Blog](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/bg-p/enterprisemobilityandsecurity?product=azure-information-protection,azure-rights-management-services).

## <a name="is-azure-information-protection-suitable-for-my-country"></a>Azure Information Protection è disponibile in tutti i paesi?

Paesi diversi hanno normative e requisiti differenti. Per ottenere una risposta a questa domanda per l'organizzazione specifica, vedere [Idoneità per paesi diversi](./compliance.md#suitability-for-different-countries).

## <a name="how-can-azure-information-protection-help-with-gdpr"></a>In quale modo Azure Information Protection può essere utile per il Regolamento generale sulla protezione dei dati?

Per scoprire come Azure Information Protection possa essere utile per soddisfare i requisiti del Regolamento generale sulla protezione dei dati, vedere l'annuncio nel post di blog seguente con video: [Microsoft 365 provides an information protection strategy to help with the GDPR](https://blogs.office.com/2018/02/22/microsoft-365-provides-an-information-protection-strategy-to-help-with-the-gdpr) (Microsoft 365 offre una strategia di protezione delle informazioni a supporto del Regolamento generale sulla protezione dei dati).

## <a name="where-can-i-find-supporting-information-for-azureinformation-protectionsuch-as-legal-compliance-and-slas"></a>Dov'è possibile reperire le informazioni di supporto per Azure Information Protection, ad esempio le note legali, le informazioni sulla conformità e i contratti di servizio?
Vedere [Informazioni su conformità e supporto per Azure Information Protection](./compliance.md).

## <a name="how-can-i-report-a-problem-or-send-feedback-for-azure-information-protection"></a>Come è possibile segnalare un problema o inviare commenti e suggerimenti per Azure Information Protection?

Per il supporto tecnico, usare i canali di supporto standard oppure [contattare il supporto tecnico Microsoft](information-support.md#to-contact-microsoft-support).

È anche possibile rivolgersi al team di ingegneri nel [sito di Yammer per Azure Information Protection](https://www.yammer.com/askipteam/). 

## <a name="what-do-i-do-if-my-question-isnt-here"></a>Cosa fare se la domanda non è presente?

Esaminare prima le domande frequenti relative alle funzionalità di classificazione e assegnazione di etichette o alla protezione dei dati. Il servizio Azure Rights Management (Azure RMS) offre la tecnologia di protezione dati per Azure Information Protection. Azure RMS può essere usato con la classificazione e l'assegnazione di etichette o in modo indipendente. 

- [Domande frequenti sulla classificazione e l'assegnazione di etichette](faqs-infoprotect.md)

- [Domande frequenti sulla protezione dei dati](faqs-rms.md)

Per eventuali altri dubbi, usare i collegamenti e le risorse elencate in [Informazioni e supporto per Azure Information Protection](information-support.md).

Esistono anche Domande frequenti progettate per gli utenti finali:

- [Domande frequenti sull'app Azure Information Protection per iOS e Android](./rms-client/mobile-app-faq.md)

- [Domande frequenti per l'app RMS sharing per computer Mac](https://technet.microsoft.com/dn451248)

