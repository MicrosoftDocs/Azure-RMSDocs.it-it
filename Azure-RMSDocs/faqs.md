---
title: Domande frequenti su Azure Information Protection
description: Alcune domande frequenti su Azure Information Protection e il relativo servizio di protezione, Azure Rights Management (Azure RMS).
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/06/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 2b473c242cdddd09c9902c56bd183e19c0a62267
ms.sourcegitcommit: 3b50727cb50a612b12f248a5d18b00175aa775f7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/08/2020
ms.locfileid: "75743618"
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

Annunciata presso Microsoft Ignite 2018 in Orlando, ora è possibile creare e configurare le etichette di [riservatezza](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels) oltre alle etichette di conservazione in uno dei centri di amministrazione: il Centro sicurezza e conformità di Office 365, il centro sicurezza Microsoft 365 o il centro di conformità Microsoft 365. È possibile eseguire la migrazione delle etichette di Azure Information Protection esistenti al nuovo archivio di etichette unificato, da usare come etichette di riservatezza con le app di Office. 

Per altre informazioni sulla gestione dell'etichettatura unificata e su come verranno supportate queste etichette, vedere il post di blog, [Announcing availability of information protection capabilities to help protect your sensitive data](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967) (Annuncio della disponibilità di funzionalità di protezione delle informazioni per proteggere i dati sensibili).

Per ulteriori informazioni sulla migrazione delle etichette esistenti, vedere [How to migrate Azure Information Protection labels to Unified Sensitivity labels](configure-policy-migrate-labels.md).

## <a name="how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform"></a>Come è possibile determinare se il tenant si trova nella piattaforma di etichettatura unificata?

Quando il tenant si trova nella piattaforma di etichettatura unificata, le etichette di riservatezza possono essere usate dai [client e dai servizi che supportano l'assegnazione di etichette unificata](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling). Se è stata ottenuta la sottoscrizione per Azure Information Protection nel 2019 giugno o versione successiva, il tenant si trova automaticamente nella piattaforma di assegnazione di etichette unificata e non è necessaria alcuna azione aggiuntiva. Il tenant potrebbe anche trovarsi su questa piattaforma perché qualcuno ha eseguito la migrazione delle etichette Azure Information Protection.

Per controllare lo stato, nella portale di Azure passare a **Azure Information Protection** > **Gestisci** > **etichetta unificata**e visualizzare lo stato dell' **etichettatura unificata**:

- Se viene visualizzato **attivato**, il tenant si trova nella piattaforma di etichettatura unificata.

- Se la visualizzazione **non è attivata**, il tenant non si trova nella piattaforma di assegnazione di etichette unificata. Per istruzioni sulla migrazione, vedere [How to migrate Azure Information Protection labels to Unified Sensitivity labels](configure-policy-migrate-labels.md).

## <a name="whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client"></a>Qual è la differenza tra il client Azure Information Protection e il client di Azure Information Protection Unified Labeling?

Il **client Azure Information Protection (classico)** è stato reso disponibile dal momento in cui Azure Information Protection stato annunciato per la prima volta come nuovo servizio per la classificazione e la protezione di file e messaggi di posta elettronica. Questo client Scarica le etichette e le impostazioni dei criteri da Azure e configura i criteri di Azure Information Protection dalla portale di Azure. Per ulteriori informazioni, vedere [Panoramica dei criteri di Azure Information Protection](overview-policy.md). 

Il **Azure Information Protection client di etichetta unificata** è un'aggiunta più recente, per supportare l'archivio di etichette unificato supportato da più applicazioni e servizi. Questo client Scarica le etichette di riservatezza e le impostazioni dei criteri dai centri di amministrazione seguenti: il Centro sicurezza e conformità di Office 365, il Centro sicurezza Microsoft 365 e la Microsoft 365 Compliance Center. Per altre informazioni, vedere [Panoramica delle etichette di riservatezza](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels).

Se non si è certi del client da usare, vedere [scegliere il client Azure Information Protection da usare](./rms-client/use-client.md#choose-which-labeling-client-to-use-for-windows-computers).

### <a name="identify-which-client-you-have-installed"></a>Identificare il client installato

Entrambi i client, quando sono installati, visualizzano **Azure Information Protection**. Per facilitare l'identificazione del client installato, utilizzare l'opzione **Guida e commenti** per aprire la finestra di dialogo **Microsoft Azure Information Protection** :

- Da Esplora file: fare clic con il pulsante destro del mouse su uno o più file o su una cartella, scegliere **Classifica e proteggi** e quindi **Guida e commenti**.

- Da un'applicazione di Office: dal pulsante **Proteggi** (client classico) o dal pulsante di **riservatezza** (client con etichetta unificata), scegliere **Guida e commenti**.

Usare il numero di **versione** visualizzato per identificare il client:

- Una versione **1**, ad esempio **1.53.10.0**, identifica il client di Azure Information Protection (classico).

- Una versione **2**, ad esempio, **2.2.14.0**, identifica il Azure Information Protection client unificato di assegnazione di etichette.

## <a name="when-is-the-right-time-to-migrate-my-labels"></a>Quando è il momento giusto per eseguire la migrazione delle etichette?

Ora che l'opzione per eseguire la migrazione delle etichette nel portale di Azure è disponibile a livello generale, è consigliabile attivare la migrazione in modo che sia possibile usare le etichette come etichette di riservatezza con [client e servizi che supportano l'assegnazione di etichette unificata](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling).

Per ulteriori informazioni e istruzioni, vedere [How to migrate Azure Information Protection labels to Unified Sensitivity labels](configure-policy-migrate-labels.md).

## <a name="after-ive-migrated-my-labels-which-management-portal-do-i-use"></a>Dopo aver eseguito la migrazione delle etichette, qual è il portale di gestione da usare?

Dopo aver eseguito la migrazione delle etichette nel portale di Azure:

- Se [i client e i servizi sono stati unificati](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling), passare a uno dei centri di amministrazione (Office 365 Centro sicurezza e conformità, Microsoft 365 Centro sicurezza o Microsoft 365 Compliance Center) per pubblicare queste etichette e per configurare le impostazioni dei criteri. Per le modifiche delle etichette, da ora in poi usare uno di questi centri di amministrazione. I client di etichettatura unificata scaricano le etichette e le impostazioni dei criteri da uno di questi centri di amministrazione.

- Se si dispone del [client di Azure Information Protection (classico)](./rms-client/aip-client.md), continuare a usare il portale di Azure per modificare le etichette e le impostazioni dei criteri. Il client classico continua a scaricare le etichette e le impostazioni dei criteri da Azure.

- Se sono presenti sia [client con etichetta unificata](configure-policy-migrate-labels.md#clients-and-services-that-support-unified-labeling) che client [classici](./rms-client/aip-client.md), è possibile usare il centro di amministrazione o il portale di Azure per apportare modifiche alle etichette. Tuttavia, affinché i client classici scelgano le modifiche apportate alle etichette nei centri di amministrazione, è necessario tornare al portale di Azure: usare l'opzione **pubblica** dal riquadro **Azure Information Protection-Unified labeling** nel portale di Azure. 

Continuare a usare il portale di Azure per il [reporting centralizzato](reports-aip.md) e lo [scanner](deploy-aip-scanner.md).

## <a name="whats-the-difference-between-azure-information-protection-and-azure-rights-management"></a>Quale è la differenza tra Azure Information Protection e Azure Rights Management?

Azure Information Protection offre funzionalità per la classificazione, l'assegnazione di etichette e la protezione per i documenti e i messaggi di posta elettronica di un'organizzazione. La tecnologia di protezione è basata sul servizio Azure Rights Management, che è ora un componente di Azure Information Protection.

## <a name="whats-the-role-of-identity-management-for-azure-information-protection"></a>Qual è il ruolo di gestione delle identità per Azure Information Protection?

Un utente deve avere un nome utente e una password validi per accedere al contenuto protetto da Azure Information Protection. Per altre informazioni su come Azure Information Protection consente di proteggere i dati, vedere [Il ruolo di Azure Information Protection nella protezione dei dati](/enterprise-mobility-security/solutions/azure-information-protection-securing-data). 

## <a name="what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included"></a>Quale sottoscrizione è necessaria per Azure Information Protection e quali funzionalità sono incluse?

Vedere le informazioni sulla sottoscrizione e l'elenco delle funzionalità nella pagina [Prezzi di Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection).

Se si ha un abbonamento a Office 365 che include la protezione dei dati di Azure Rights Management, scaricare il [foglio dati di licenza di Azure Information Protection](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

Per altre domande sulle licenze, cercare le risposte nella sezione [Domande frequenti sulle licenze](https://azure.microsoft.com/pricing/details/information-protection#faq).

## <a name="is-the-azure-information-protection-client-only-for-subscriptions-that-include-classification-and-labeling"></a>Il client Azure Information Protection è disponibile solo per le sottoscrizioni che includono la classificazione e l'assegnazione di etichette?

No. Il client Azure Information Protection (classico) può essere usato anche con le sottoscrizioni che includono solo il servizio Azure Rights Management per proteggere i dati.

Quando il client classico è installato e non dispone di un criterio di Azure Information Protection, questo client funziona automaticamente in [modalità di sola protezione](./rms-client/client-protection-only-mode.md). In questa modalità gli utenti possono applicare facilmente modelli di Rights Management e autorizzazioni personalizzate. Se successivamente si acquista una sottoscrizione che include la classificazione e l'assegnazione di etichette, il client passa automaticamente alla modalità standard durante il download dei criteri di Azure Information Protection.

## <a name="do-you-need-to-be-a-global-admin-to-configure-azure-information-protection-or-can-i-delegate-to-other-administrators"></a>È necessario essere un amministratore globale per configurare Azure Information Protection oppure tale configurazione può essere delegata ad altri amministratori?

Gli amministratori globali per un tenant di Office 365 o di Azure AD possono ovviamente eseguire tutte le attività amministrative per Azure Information Protection. Se tuttavia si vogliono assegnare autorizzazioni amministrative ad altri utenti, sono disponibili le opzioni seguenti:

- **Amministratore Azure Information Protection**: questo ruolo di amministratore Azure Active Directory consente a un amministratore di configurare Azure Information Protection ma non altri servizi. Un amministratore con questo ruolo può attivare e disattivare il servizio di protezione Azure Rights Management, configurare le etichette e le impostazioni di protezione e configurare i criteri di Azure Information Protection. Inoltre, un amministratore con questo ruolo può eseguire tutti i cmdlet di PowerShell per il [client Azure Information Protection](./rms-client/client-admin-guide-powershell.md) e dal [modulo AIPService](administer-powershell.md). Tuttavia, questo ruolo non supporta il rilevamento e la revoca dei documenti per gli utenti.
    
    > [!NOTE]
    > Questo ruolo non è supportato nel portale di Azure se il tenant si trova nella [piattaforma di etichettatura unificata](#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform).
    
    Per assegnare un utente a questo ruolo amministrativo, vedere [Assegnare un utente ai ruoli di amministratore in Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal).

- Amministratore della **conformità** o **amministratore dei dati di conformità**: questi ruoli di amministratore Azure Active Directory consentono a un amministratore di configurare Azure Information Protection, che include l'attivazione e la disattivazione del servizio Azure Rights Management Protection, la configurazione delle impostazioni di protezione e delle etichette e la configurazione dei criteri di Azure Information Protection. Inoltre, un amministratore con uno di questi ruoli può eseguire tutti i cmdlet di PowerShell per il [client Azure Information Protection](./rms-client/client-admin-guide-powershell.md) e dal [modulo AIPService](administer-powershell.md). Tuttavia, questi ruoli non supportano il rilevamento e la revoca dei documenti per gli utenti.
    
    Per assegnare un utente a uno di questi ruoli amministrativi, vedere [assegnare un utente ai ruoli di amministratore in Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal). Per visualizzare le altre autorizzazioni di un utente con questi ruoli, vedere la sezione [ruoli disponibili](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles) della documentazione Azure Active Directory.

- **Reader** per la sicurezza o **Reader globale**: solo per [Azure Information Protection Analytics](reports-aip.md) . Questo ruolo di amministratore di Azure Active Directory consente agli amministratori di visualizzare come vengono usate le etichette, monitorare l'accesso degli utenti ai documenti e ai messaggi di posta elettronica etichettati ed eventuali modifiche della classificazione, nonché di identificare documenti che contengono informazioni sensibili che devono essere protette. Poiché questa funzionalità USA monitoraggio di Azure, è necessario disporre anche di un ruolo di supporto [RBAC](reports-aip.md#permissions-required-for-azure-information-protection-analytics).

- **Amministratore della sicurezza**: questo ruolo Azure Active Directory amministratore consente a un amministratore di configurare Azure Information Protection nel portale di Azure, oltre a configurare alcuni aspetti di altri servizi di Azure. Un amministratore con questo ruolo non può eseguire alcun [cmdlet di PowerShell dal modulo AIPService](administer-powershell.md)oppure rilevare e revocare i documenti per gli utenti.
    
    Per assegnare un utente a questo ruolo amministrativo, vedere [Assegnare un utente ai ruoli di amministratore in Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal). Per conoscere le altre autorizzazioni di cui dispone un utente con questo ruolo, vedere la sezione [Ruoli disponibili](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles) della documentazione di Azure Active Directory.

- Amministratore **globale** di Azure Rights Management e **amministratore del connettore**: per questi ruoli di amministratore di Azure Rights Management, il primo concede agli utenti le autorizzazioni per eseguire tutti i [cmdlet di PowerShell dal modulo AIPService](administer-powershell.md) senza renderli un amministratore globale per altri servizi cloud, mentre il secondo ruolo concede le autorizzazioni per eseguire solo il connettore Rights Management (RMS). Nessuno di questi ruoli amministrativi concede le autorizzazioni per le console di gestione o il rilevamento e la revoca dei documenti per gli utenti.
    
    Per assegnare uno di questi ruoli amministrativi, usare il cmdlet di PowerShell AIPService, [Add-AipServiceRoleBasedAdministrator](/powershell/module/aipservice/add-aipservicerolebasedadministrator).

Alcune osservazioni:

- Gli account Microsoft non sono supportati per l'amministrazione delegata di Azure Information Protection, anche se questi account sono assegnati a uno dei ruoli amministrativi elencati. 

- Se i [controlli di onboarding](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) sono stati configurati, ciò non influisce sulla possibilità di amministrare Azure Information Protection, fatta eccezione per il connettore RMS. Ad esempio, se i controlli di selezione sono stati configurati in modo da limitare la protezione del contenuto al gruppo "Reparto IT", l'account usato per installare e configurare il connettore RMS deve essere membro di tale gruppo. 

- Gli utenti a cui è assegnato un ruolo amministrativo non possono rimuovere automaticamente la protezione dai documenti o dai messaggi di posta elettronica che sono stati protetti tramite Azure Information Protection. Possono farlo solo gli utenti a cui è assegnato il ruolo di utente con privilegi avanzati, e solo quando la funzionalità utente con privilegi avanzati è abilitata. Tuttavia, tutti gli utenti a cui si assegnano autorizzazioni amministrative per Azure Information Protection possono assegnare il ruolo di utente con privilegi avanzati a qualsiasi utente, compreso il proprio account. Possono anche abilitare la funzionalità utente con privilegi avanzati. Queste azioni vengono registrate in un registro amministratore. Per ulteriori informazioni, vedere la sezione procedure ottimali di sicurezza in [configurazione di utenti con privilegi avanzati per Azure Information Protection e servizi di individuazione o ripristino dei dati](configure-super-users.md). 

- Se si esegue la migrazione delle etichette di Azure Information Protection all'archivio delle etichette unificate, assicurarsi di leggere la sezione seguente dalla documentazione relativa alla migrazione delle etichette: [ruoli amministrativi che supportano la piattaforma di assegnazione di etichette unificata](configure-policy-migrate-labels.md#administrative-roles-that-support-the-unified-labeling-platform).

## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>Azure Information Protection supporta scenari locali e ibridi?

Sì. Anche se è una soluzione basata sul cloud, Azure Information Protection può classificare, etichettare e proteggere documenti e messaggi di posta elettronica archiviati in locale, oltre che nel cloud.

Se si ha Exchange Server, SharePoint Server e file server Windows, è possibile distribuire il [connettore Rights Management](deploy-rms-connector.md) per consentire a questi server locali di usare il servizio Azure Rights Management per proteggere messaggi di posta elettronica e documenti. È inoltre possibile sincronizzare ed eseguire la federazione dei controller di dominio di Active Directory con Azure AD per un'esperienza di autenticazione più semplice per gli utenti, ad esempio usando [Azure AD Connect](/azure/active-directory/hybrid/whatis-azure-ad-connect).

Il servizio Azure Rights Management genera e gestisce automaticamente i certificati XrML come richiesto e quindi non usa un'infrastruttura PKI locale. Per altre informazioni sull'uso dei certificati in Azure Rights Management, vedere la sezione [Procedura dettagliata del funzionamento di Azure RMS: primo uso, protezione dei contenuti, utilizzo del contenuto](./how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) nell'articolo [Funzionamento di Azure RMS](./how-does-it-work.md).

## <a name="what-types-of-data-can-azure-information-protection-classify-and-protect"></a>Quali tipi di dati è possibile classificare e proteggere tramite Azure Information Protection?

Azure Information Protection consente di classificare e proteggere messaggi di posta elettronica e documenti, sia in locale che nel cloud. Questi documenti includono documenti di Word, fogli di calcolo di Excel, presentazioni di PowerPoint, documenti PDF, file di testo e file di immagine. Per un elenco dei tipi di documenti supportati, vedere l'elenco dei [tipi di file supportati](./rms-client/clientv2-admin-guide-file-types.md) nella Guida dell'amministratore.

Azure Information Protection non è in grado di classificare e proteggere i dati strutturati, ad esempio file di database, elementi del calendario, post Yammer, contenuto Sway e notebook di OneNote.

**Appena annunciato in anteprima**: Power bi supporta ora la classificazione usando le etichette di riservatezza e può applicare la protezione da tali etichette ai dati esportati nei formati di file seguenti: PDF, xls e PPT. Per ulteriori informazioni, vedere [protezione dei dati in Power BI (anteprima)](https://docs.microsoft.com/power-bi/admin/service-security-data-protection-overview).

## <a name="i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work"></a>Azure Information Protection è elencata come un'app cloud disponibile per l'accesso condizionale, come funziona?

Nell'offerta di anteprima è ora possibile configurare l'accesso condizionale di Azure Active Directory per Azure Information Protection.

Quando un utente apre un documento protetto da Azure Information Protection, gli amministratori possono ora bloccare o concedere l'accesso agli utenti nel tenant, in base ai controlli di accesso condizionale standard. La richiesta di autenticazione a più fattori (MFA) è una delle condizioni più comunemente richieste. Un'altra è che i dispositivi siano [conformi ai criteri di Intune](/intune/conditional-access-intune-common-ways-use) in modo che, ad esempio, i dispositivi mobili soddisfino i requisiti relativi alle password e possiedano una versione minima del sistema operativo e i computer siano appartenenti a un dominio.

Per altre informazioni ed esempi di procedura dettagliata, vedere il post del blog [Conditional Access policies for Azure Information Protection](https://cloudblogs.microsoft.com/enterprisemobility/2017/10/17/conditional-access-policies-for-azure-information-protection/) (Criteri di accesso condizionale per Azure Information Protection).

Informazioni aggiuntive:

- Per i computer Windows: per la versione di anteprima corrente vengono valutati i criteri di accesso condizionale per Azure Information Protection quando [viene inizializzato l'ambiente utente](./how-does-it-work.md#initializing-the-user-environment) (questo processo è noto anche come bootstrap) e in seguito ogni 30 giorni.

- È possibile ottimizzare la frequenza con cui vengono valutati i criteri di accesso condizionale. A questo scopo è possibile configurare la durata del token. Per altre informazioni, vedere [Durata dei token configurabili in Azure Active Directory](/azure/active-directory/active-directory-configurable-token-lifetimes).

- Si consiglia di non aggiungere gli account amministratore ai criteri di accesso condizionale perché questi account non saranno in grado di accedere al riquadro Azure Information Protection nel portale di Azure.

- Se si usa l'autenticazione a più fattori nei criteri di accesso condizionale per la collaborazione con altre organizzazioni (B2B), è necessario usare la [collaborazione B2B di Azure AD](/azure/active-directory/b2b/what-is-b2b) e creare account guest per gli utenti con cui si vuole procedere alla condivisione nell'altra organizzazione.

- Con la versione di anteprima di dicembre 2018 di Azure Active Directory è ora possibile richiedere agli utenti di accettare le condizioni per l'utilizzo prima di aprire per la prima volta un documento protetto. Per altre informazioni, vedere il post di Blog seguente: [aggiornamenti per Azure ad le condizioni per l'utilizzo all'interno dell'accesso condizionale](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Updates-to-Azure-AD-Terms-of-Use-functionality-within/ba-p/294822)

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

Esiste una differenza nell'impostazione del [proprietario Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner) per i file protetti in una cartella locale o in una condivisione di rete. Per impostazione predefinita, per entrambe le soluzioni, il proprietario di Rights Management viene impostato sull'account che protegge il file, ma è possibile sostituire questa impostazione:

- Per Infrastruttura di classificazione file di Windows Server è possibile impostare il proprietario di Rights Management su un singolo account per tutti i file o impostare in modo dinamico il proprietario di Rights Management per ogni file. Per impostare in modo dinamico il proprietario di Rights Management, usare il parametro **-OwnerMail [posta elettronica proprietario file di origine]** e relativo valore. Questa configurazione recupera l'indirizzo di posta elettronica dell'utente da Active Directory usando il nome dell'account utente specificato nella proprietà del proprietario del file.

- Per il Azure Information Protection scanner: per i file appena protetti, è possibile impostare il proprietario Rights Management come un singolo account per tutti i file in un archivio dati specificato, ma non è possibile impostare dinamicamente il proprietario Rights Management per ogni file. Il proprietario di Rights Management non viene modificato per i file già protetti. Per impostare l'account per i file appena protetti, specificare l'impostazione **Proprietario predefinito** nel profilo dello scanner. 

Quando lo scanner protegge i file inclusi in siti e librerie di SharePoint, il proprietario di Rights Management viene impostato in modo dinamico per ogni file usando il valore Editor di SharePoint.

## <a name="ive-heard-a-new-release-is-going-to-be-available-soon-for-azure-information-protectionwhen-will-it-be-released"></a>Secondo alcune voci, sarà presto disponibile una nuova versione di Azure Information Protection. Quando verrà rilasciata?

La documentazione tecnica non contiene informazioni sulle versioni future. Per questo tipo di informazioni, usare la [Roadmap di Microsoft 365](https://www.microsoft.com/microsoft-365/roadmap?&filters=Azure%20Information%20Protection%2CO365%20Information%20Protection#owRoadmapMainContent), vedere il [Blog Enterprise Mobility + Security](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/bg-p/enterprisemobilityandsecurity?product=azure-information-protection,azure-rights-management-services).

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

