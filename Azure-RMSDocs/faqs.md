---
title: Domande frequenti su Azure Information Protection
description: Alcune domande frequenti su Azure Information Protection e sul relativo servizio di protezione dei dati, Azure Rights Management (Azure RMS).
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 71ce491f-41c1-4d15-9646-455a6eaa157d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 4d991a96dd82bdc27aed036fd05119ba3f7ca1f2
ms.sourcegitcommit: 26a2c1becdf3e3145dc1168f5ea8492f2e1ff2f3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/07/2018
ms.locfileid: "44151674"
---
# <a name="frequently-asked-questions-for-azure-information-protection"></a>Domande frequenti su Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Di seguito sono riportate alcune possibili domande su Azure Information Protection o sul servizio Azure Rights Management (Azure RMS) e le relative risposte.

La pagina delle domande frequenti viene aggiornata periodicamente e le nuove aggiunte vengono pubblicate negli annunci mensili di aggiornamento della documentazione nel [blog tecnico di Azure Information Protection](https://aka.ms/AIPblog).

## <a name="whats-the-difference-between-azure-information-protection-and-azure-rights-management"></a>Quale è la differenza tra Azure Information Protection e Azure Rights Management?

Azure Information Protection offre funzionalità per la classificazione, l'assegnazione di etichette e la protezione per i documenti e i messaggi di posta elettronica di un'organizzazione. La tecnologia di protezione è basata sul servizio Azure Rights Management, che è ora un componente di Azure Information Protection.

## <a name="what-is-the-role-of-identity-management-for-azure-information-protection"></a>Qual è il ruolo della gestione delle identità per Azure Information Protection?

Un utente deve avere un nome utente e una password validi per accedere al contenuto protetto da Azure Information Protection. Per altre informazioni su come Azure Information Protection consente di proteggere i dati, vedere [Il ruolo di Azure Information Protection nella protezione dei dati](/enterprise-mobility-security/solutions/azure-information-protection-securing-data). 

## <a name="what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included"></a>Quale sottoscrizione è necessaria per Azure Information Protection e quali funzionalità sono incluse?
Vedere le informazioni sulla sottoscrizione e l'elenco delle funzionalità nella pagina [Prezzi di Azure Information Protection](https://azure.microsoft.com/en-us/pricing/details/information-protection). 

Se si ha un abbonamento a Office 365 che include la protezione dei dati di Azure Rights Management, scaricare il [foglio dati di licenza di Azure Information Protection](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf), che include anche alcune domande frequenti sulle licenze.

## <a name="is-the-azure-information-protection-client-only-for-subscriptions-that-include-classification-and-labeling"></a>Il client Azure Information Protection è disponibile solo per le sottoscrizioni che includono la classificazione e l'assegnazione di etichette?

No. Anche se quasi tutte le presentazioni e demo del client Azure Information Protection illustrano le funzionalità di classificazione e assegnazione di etichette, questo client può essere usato anche con le sottoscrizioni che includono solo il servizio Azure Rights Management per la protezione dei dati.

Quando viene installato il client Azure Information Protection per Windows e non sono configurati criteri per Azure Information Protection, il client funziona automaticamente in [modalità di sola protezione](./rms-client/client-protection-only-mode.md). In questa modalità gli utenti possono applicare facilmente modelli di Rights Management e autorizzazioni personalizzate. Se successivamente si acquista una sottoscrizione che include la classificazione e l'assegnazione di etichette, il client passa automaticamente alla modalità standard durante il download dei criteri di Azure Information Protection.

Se si usa l'applicazione di condivisione Rights Management per Windows, è consigliabile sostituirla con il client Azure Information Protection. Il supporto per questa applicazione di condivisione terminerà il 31 gennaio 2019. Per una più facile transizione, vedere [Attività eseguite in precedenza con l'applicazione RMS sharing](./rms-client/upgrade-client-app.md).

## <a name="do-you-need-to-be-a-global-admin-to-configure-azure-information-protection-or-can-i-delegate-to-other-administrators"></a>È necessario essere un amministratore globale per configurare Azure Information Protection oppure tale configurazione può essere delegata ad altri amministratori?

Gli amministratori globali per un tenant di Office 365 o di Azure AD possono ovviamente eseguire tutte le attività amministrative per Azure Information Protection. Se tuttavia si vogliono assegnare autorizzazioni amministrative ad altri utenti, sono disponibili le opzioni seguenti:

- **Amministratore di Information Protection**: questo ruolo di amministratore di Azure Active Directory consente a un amministratore di configurare tutti gli aspetti di Azure Information Protection, ma non altri servizi. Un amministratore con questo ruolo può attivare e disattivare il servizio di protezione Azure Rights Management, configurare le etichette e le impostazioni di protezione e configurare i criteri di Azure Information Protection. Un amministratore con questo ruolo può anche eseguire tutti i cmdlet PowerShell per il [client Azure Information Protection](./rms-client/client-admin-guide-powershell.md) e per il [modulo AADRM](administer-powershell.md). 
    
    Per assegnare un utente a questo ruolo amministrativo, vedere [Assegnare un utente ai ruoli di amministratore in Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal).

- **Amministratore della sicurezza**: questo ruolo di amministratore di Azure Active Directory consente a un amministratore di configurare tutti gli aspetti di Azure Information Protection nel portale di Azure, oltre che di configurare alcuni aspetti di altri servizi di Azure. Un amministratore con questo ruolo non può eseguire alcuno dei [cmdlet PowerShell del modulo AADRM](administer-powershell.md).
    
    Per assegnare un utente a questo ruolo amministrativo, vedere [Assegnare un utente ai ruoli di amministratore in Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal). Per conoscere le altre autorizzazioni di cui dispone un utente con questo ruolo, vedere la sezione [Ruoli disponibili](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles) della documentazione di Azure Active Directory.

- **Amministratore globale** e **Amministratore connettore** di Azure Rights Management: per questi ruoli di amministratore di Azure Rights Management, il primo concede agli utenti le autorizzazioni per eseguire tutti i [cmdlet PowerShell del modulo AADRM](administer-powershell.md) senza diritti di amministratore globale per altri servizi cloud, mentre il secondo ruolo concede le autorizzazioni per eseguire solo il connettore Rights Management (RMS). Nessuno di questi ruoli amministrativi concede le autorizzazioni per le console di gestione o per usare la modalità di amministrazione nel sito di rilevamento dei documenti.

    Per assegnare uno di questi ruoli amministrativi, usare il cmdlet PowerShell di AADRM [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator).

Alcune osservazioni:

- Se i [controlli di onboarding](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) sono stati configurati, ciò non influisce sulla possibilità di amministrare Azure Information Protection, fatta eccezione per il connettore RMS. Ad esempio, se i controlli di selezione sono stati configurati in modo da limitare la protezione del contenuto al gruppo "Reparto IT", l'account usato per installare e configurare il connettore RMS deve essere membro di tale gruppo. 

- Gli utenti a cui è assegnato un ruolo amministrativo non possono rimuovere automaticamente la protezione dai documenti o dai messaggi di posta elettronica che sono stati protetti tramite Azure Information Protection. Possono farlo solo gli utenti a cui è assegnato il ruolo di utente con privilegi avanzati, e solo quando la funzionalità utente con privilegi avanzati è abilitata. Tuttavia, tutti gli utenti a cui si assegnano autorizzazioni amministrative per Azure Information Protection possono assegnare il ruolo di utente con privilegi avanzati a qualsiasi utente, compreso il proprio account. Possono anche abilitare la funzionalità utente con privilegi avanzati. Queste azioni vengono registrate in un registro amministratore. Per altre informazioni, vedere la sezione sulle procedure consigliate in [Configurazione degli utenti con privilegi avanzati per Azure Rights Management e servizi di individuazione o ripristino dei dati](configure-super-users.md). 


## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>Azure Information Protection supporta scenari locali e ibridi?

Sì. Anche se è una soluzione basata sul cloud, Azure Information Protection può classificare, etichettare e proteggere documenti e messaggi di posta elettronica archiviati in locale, oltre che nel cloud.

Se si hanno Exchange Server, SharePoint Server e file server Windows, è possibile distribuire il [connettore Rights Management](deploy-rms-connector.md) per consentire a questi server locali di usare il servizio Azure Rights Management per proteggere messaggi di posta elettronica e documenti. È inoltre possibile sincronizzare ed eseguire la federazione dei controller di dominio di Active Directory con Azure AD per un'esperienza di autenticazione più semplice per gli utenti, ad esempio utilizzando [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/).

Il servizio Azure Rights Management genera e gestisce automaticamente i certificati XrML come richiesto e quindi non usa un'infrastruttura PKI locale. Per altre informazioni sull'uso dei certificati in Azure Rights Management, vedere la sezione [Procedura dettagliata del funzionamento di Azure RMS: primo uso, protezione dei contenuti, utilizzo del contenuto](./how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) nell'articolo [Funzionamento di Azure RMS](./how-does-it-work.md).

## <a name="what-types-of-data-can-azure-information-protection-classify-and-protect"></a>Quali tipi di dati è possibile classificare e proteggere tramite Azure Information Protection?

Azure Information Protection consente di classificare e proteggere messaggi di posta elettronica e documenti, sia in locale che nel cloud. Questi documenti includono documenti di Word, fogli di calcolo di Excel, presentazioni di PowerPoint, documenti PDF, file di testo e file di immagine. Per un elenco dei tipi di documenti supportati, vedere l'elenco dei [tipi di file supportati](./rms-client/client-admin-guide-file-types.md) nella Guida dell'amministratore.

Azure Information Protection non consente di classificare e proteggere dati strutturati come file di database, elementi del calendario, report di Power BI, post di Yammer, contenuti di Sway e blocchi appunti di OneNote.

## <a name="i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work"></a>Azure Information Protection è elencata come un'app cloud disponibile per l'accesso condizionale, come funziona?

Nell'ambito dell'anteprima pubblica offerta è ora possibile configurare l'accesso condizionale di Azure Active Directory per Azure Information Protection.

Quando un utente apre un documento protetto da Azure Information Protection, gli amministratori possono ora bloccare o concedere l'accesso agli utenti nel tenant, in base ai controlli di accesso condizionale standard. La richiesta di autenticazione a più fattori (MFA) è una delle condizioni più comunemente richieste. Un'altra è che i dispositivi siano [conformi ai criteri di Intune](/intune/conditional-access-intune-common-ways-use) in modo che, ad esempio, i dispositivi mobili soddisfino i requisiti relativi alle password e possiedano una versione minima del sistema operativo e i computer siano appartenenti a un dominio.

Per altre informazioni ed esempi di procedura dettagliata, vedere il post del blog [Conditional Access policies for Azure Information Protection](https://cloudblogs.microsoft.com/enterprisemobility/2017/10/17/conditional-access-policies-for-azure-information-protection/) (Criteri di accesso condizionale per Azure Information Protection).

Informazioni aggiuntive:

- Per i computer Windows: per la versione di anteprima corrente vengono valutati i criteri di accesso condizionale per Azure Information Protection quando [viene inizializzato l'ambiente utente](./how-does-it-work.md#initializing-the-user-environment) (questo processo è noto anche come bootstrap) e in seguito ogni 30 giorni.

- È possibile ottimizzare la frequenza con cui vengono valutati i criteri di accesso condizionale. A questo scopo è possibile configurare la durata del token. Per altre informazioni, vedere [Durata dei token configurabili in Azure Active Directory](/azure/active-directory/active-directory-configurable-token-lifetimes).

- È consigliabile non aggiungere gli account amministratore ai criteri di accesso condizionale poiché questi account non saranno in grado di accedere al pannello di Azure Information Protection nel portale di Azure.

- Se si usano numerose app cloud per l'accesso condizionale, si potrebbe riscontrare che l'app **Microsoft Azure Information Protection** non viene visualizzata nell'elenco per la selezione. In questo caso, usare la casella di ricerca nella parte superiore dell'elenco. Iniziare a digitare "Microsoft Azure Information Protection" per filtrare le app disponibili. Se si ha una sottoscrizione supportata, l'app **Microsoft Azure Information Protection** verrà quindi visualizzata per la selezione. 

## <a name="whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365"></a>Qual è la differenza tra le etichette in Azure Information Protection e in Office 365?

Le etichette in Azure Information Protection consentono di applicare criteri di classificazione e protezione coerenti per documenti e messaggi di posta elettronica, sia locali che nel cloud. La classificazione e la protezione sono indipendenti dal percorso in cui è archiviato il contenuto o dalla modalità di spostamento. [Le etichette di sicurezza e conformità di Office 365](https://support.office.com/article/af398293-c69d-465e-a249-d74561552d30) consentono di classificare documenti e messaggi di posta elettronica per il controllo e la conservazione quando il contenuto è nei servizi di Office 365. 

Attualmente, le etichette vengono applicate e gestite separatamente ma Microsoft sta lavorando verso una strategia completa e unificata per le etichette per più servizi, tra cui Azure Information Protection, Office 365, Microsoft Cloud App Security e Windows Information Protection. È possibile che si sia sentito parlare di questa strategia come "Microsoft Information Protection" (MIP). Lo stesso schema e archivio per le etichette sarà disponibile anche per i fornitori di software. Per altre informazioni, vedere il post di blog, [Consistent labeling and protection policies coming to Office 365 and Azure Information Protection](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Consistent-labeling-and-protection-policies-coming-to-Office-365/ba-p/161553) (Criteri coerenti per etichette e protezione previsti per Office 365 e Azure Information Protection).

## <a name="whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner"></a>Qual è la differenza tra Infrastruttura di classificazione file di Windows Server e lo scanner di Azure Information Protection?

Per un periodo di tempo è stato possibile usare Infrastruttura di classificazione file di Windows Server per classificare i documenti e quindi proteggerli tramite il [connettore Rights Management](deploy-rms-connector.md) (solo documenti di Office) o uno [script di PowerShell](./rms-client/configure-fci.md) (tutti i tipi di file). 

Ora è possibile usare lo [scanner di Azure Information Protection](deploy-aip-scanner.md). Lo scanner usa il client Azure Information Protection e i criteri di Azure Information Protection per assegnare etichette ai documenti (tutti i tipi di file) in modo che questi documenti possano essere poi classificati e, facoltativamente, protetti.

Le differenze principali tra queste due soluzioni sono le seguenti:

|Infrastruttura di classificazione file di Windows Server|Scanner di Azure Information Protection|
|--------------------------------|-------------------------------------|
|Archivi dati supportati: <br /><br />- Cartelle locali in Windows Server|Archivi dati supportati: <br /><br />- Cartelle locali in Windows Server<br /><br />- Condivisione file di Windows e NAS (Network-Attached Storage)<br /><br />- SharePoint Server 2016 e SharePoint Server 2013. SharePoint Server 2010 è supportato anche per i clienti che hanno [esteso il supporto per questa versione di SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010) e che usano la versione di anteprima dello scanner.|
|Modalità operativa: <br /><br />- Tempo reale|Modalità operativa: <br /><br />- Ricerca per indicizzazione sistematica degli archivi dati, con esecuzione una tantum o ripetuta del ciclo|
|Supporto per i tipi di file: <br /><br />- Per impostazione predefinita, sono protetti tutti i tipi di file <br /><br />- Specifici tipi di file possono essere esclusi dalla protezione modificando il Registro di sistema|Supporto per i tipi di file: <br /><br />- Per impostazione predefinita, sono protetti i tipi di file di Office <br /><br />- Specifici tipi di file possono essere inclusi nella protezione modificando il Registro di sistema|

Esiste attualmente una differenza nell'impostazione del [proprietario di Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner) per i file protetti in una cartella locale o in una condivisione di rete. Per impostazione predefinita, per entrambe le soluzioni, il proprietario di Rights Management viene impostato sull'account che protegge il file, ma è possibile sostituire questa impostazione:

- Per Infrastruttura di classificazione file di Windows Server è possibile impostare il proprietario di Rights Management su un singolo account per tutti i file o impostare in modo dinamico il proprietario di Rights Management per ogni file. Per impostare in modo dinamico il proprietario di Rights Management, usare il parametro **-OwnerMail [posta elettronica proprietario file di origine]** e relativo valore. Questa configurazione recupera l'indirizzo di posta elettronica dell'utente da Active Directory usando il nome dell'account utente specificato nella proprietà del proprietario del file.

- Per lo scanner di Azure Information Protection è possibile impostare il proprietario di Rights Management su un singolo account per tutti i file di uno specifico archivio dati, ma non è possibile impostare in modo dinamico il proprietario di Rights Management per ogni file. Per impostare l'account, specificare il parametro **-DefaultOwner** per il [profilo del repository dei dati](/powershell/module/azureinformationprotection/Set-AIPScannerRepository?view=azureipps#optional-parameters).

Quando lo scanner protegge i file in siti e librerie di SharePoint, il proprietario di Rights Management viene impostato in modo dinamico per ogni file usando il valore dell'autore di SharePoint.

## <a name="ive-heard-a-new-release-is-going-to-be-available-soon-for-azure-information-protectionwhen-will-it-be-released"></a>Secondo alcune voci, sarà presto disponibile una nuova versione di Azure Information Protection. Quando verrà rilasciata?

La documentazione tecnica non contiene informazioni sulle versioni future. Per questo tipo di informazioni e per gli annunci di nuove versioni, visitare il [blog di Enterprise Mobility + Security](https://cloudblogs.microsoft.com/enterprisemobility/?product=azure-information-protection,azure-rights-management-services) e ottenere gli aggiornamenti più recenti da [Microsoft Mobility@MSFTMobility](https://twitter.com/MSFTMobility) su Twitter. Se si è interessati a una versione di Office, assicurarsi di vedere anche il [blog di Office](https://blogs.office.com/).

## <a name="is-azure-information-protection-suitable-for-my-country"></a>Azure Information Protection è disponibile in tutti i paesi?

Paesi diversi hanno normative e requisiti differenti. Per ottenere una risposta a questa domanda per l'organizzazione specifica, vedere [Idoneità per paesi diversi](./compliance.md#suitability-for-different-countries).

## <a name="how-can-azure-information-protection-help-with-gdpr"></a>In quale modo Azure Information Protection può essere utile per il Regolamento generale sulla protezione dei dati?

Per scoprire come Azure Information Protection possa essere utile per soddisfare i requisiti del Regolamento generale sulla protezione dei dati, vedere l'annuncio nel post di blog seguente con video: [Microsoft 365 provides an information protection strategy to help with the GDPR](https://blogs.office.com/2018/02/22/microsoft-365-provides-an-information-protection-strategy-to-help-with-the-gdpr) (Microsoft 365 offre una strategia di protezione delle informazioni a supporto del Regolamento generale sulla protezione dei dati).

## <a name="where-can-i-find-supporting-information-for-azure-information-protectionsuch-as-legal-compliance-and-slas"></a>Dov'è possibile reperire le informazioni di supporto per Azure Information Protection, ad esempio le note legali, le informazioni sulla conformità e i contratti di servizio?
Vedere [Informazioni su conformità e supporto per Azure Information Protection](./compliance.md).

## <a name="how-can-i-report-a-problem-or-send-feedback-for-azure-information-protection"></a>Come è possibile segnalare un problema o inviare commenti e suggerimenti per Azure Information Protection?

Per il supporto tecnico, usare i canali di supporto standard oppure [contattare il supporto tecnico Microsoft](information-support.md#to-contact-microsoft-support).

Per inviare commenti e suggerimenti per possibili miglioramenti o nuove funzionalità, fare clic su **Proteggi** e quindi su **Guida e commenti** nel gruppo **Protezione** della scheda **Home** dell'applicazione di Office. Nella finestra di dialogo **Microsoft Azure Information Protection** fare clic su **Invia commenti e suggerimenti**. Questa opzione determina l'apertura di un messaggio di posta elettronica da inviare al team di Information Protection.

È anche possibile rivolgersi al team di ingegneri nel [sito di Yammer per Azure Information Protection](https://www.yammer.com/askipteam/). 

## <a name="what-do-i-do-if-my-question-isnt-here"></a>Cosa fare se la domanda non è presente?

Esaminare prima le domande frequenti relative alle funzionalità di classificazione e assegnazione di etichette o alla protezione dei dati. Il servizio Azure Rights Management (Azure RMS) offre la tecnologia di protezione dati per Azure Information Protection. Azure RMS può essere usato con la classificazione e l'assegnazione di etichette o in modo indipendente. 

- [Domande frequenti sulla classificazione e l'assegnazione di etichette](faqs-infoprotect.md)

- [Domande frequenti sulla protezione dei dati](faqs-rms.md)

Per eventuali altri dubbi, usare i collegamenti e le risorse elencate in [Informazioni e supporto per Azure Information Protection](information-support.md).

Esistono anche Domande frequenti progettate per gli utenti finali:

- [Domande frequenti sull'app Azure Information Protection per iOS e Android](./rms-client/mobile-app-faq.md)

- [Domande frequenti sull'app RMS per computer Mac e dispositivi Windows Phone](https://technet.microsoft.com/dn451248)

- [Domande frequenti sull'applicazione Rights Management sharing per Windows](https://technet.microsoft.com/dn467883)



