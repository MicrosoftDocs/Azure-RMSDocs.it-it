---
title: Domande frequenti su Azure RMS - AIP
description: Domande frequenti sul servizio di protezione dei dati, Azure Rights Management (Azure RMS) di Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/22/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 90df11c5-355c-4ae6-a762-351b05d0fbed
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: dccc643ae49521262d5327b4d3d98801f88b3894
ms.openlocfilehash: ed200df12b3d0665920091c7772ed88a79143e70
ms.lasthandoff: 02/25/2017


---

# <a name="frequently-asked-questions-about-data-protection-in-azure-information-protection"></a>Domande frequenti sulla protezione dei dati in Azure Information Protection

>*Si applica a: Azure Information Protection, Office 365*

Di seguito sono riportate alcune possibili domande sul servizio di protezione dei dati, Azure Rights Management, di Azure Information Protection e le relative risposte. 

## <a name="do-files-have-to-be-in-the-cloud-to-be-protected-by-azure-rights-management"></a>Per essere protetti da Azure Rights Management, i file devono trovarsi sul cloud?
No, questo è un malinteso comune. Il servizio Azure Rights Management e Microsoft non visualizzano né archiviano i dati dell'utente come parte del processo di protezione delle informazioni. Le informazioni protette non vengono mai inviate o archiviate in Azure, a meno di archiviarle in modo esplicito in Azure o di usare un altro servizio cloud che le archivia in Azure. 

Per altre informazioni, vedere [Funzionamento di Azure RMS: dietro le quinte](../understand-explore/how-does-it-work.md) per comprendere come la formula segreta per una bevanda gassata creata e archiviata in locale viene protetta dal servizio Azure Rights Management pur rimanendo in locale.

## <a name="whats-the-difference-between-azure-rights-management-encryption-and-encryption-in-other-microsoft-cloud-services"></a>Qual è la differenza tra la crittografia in Azure Rights Management e la crittografia in altri servizi cloud Microsoft?

Microsoft offre più tecnologie di crittografia che consentono di proteggere i dati nell'ambito di scenari diversi e spesso complementari. Ad esempio, mentre Office 365 offre la crittografia dei dati inattivi per i dati archiviati in Office 365, il servizio Azure Rights Management di Azure Information Protection esegue la crittografia indipendente dei dati, in modo che risultino protetti indipendentemente dalla posizione in cui si trovano o dalla modalità in cui vengono trasmessi.

Queste tecnologie di crittografia sono complementari e per usarle è necessario abilitarle e configurarle in modo indipendente. Durante questa operazione è possibile che venga offerta la possibilità di usare una chiave personale per la crittografia, scenario noto anche come "BYOK" (Bring Your Own Key). L'abilitazione della modalità BYOK per una di queste tecnologie non influirà in alcun modo sulle altre. Ad esempio, è possibile usare la modalità BYOK per Azure Information Protection e non per altre tecnologie di crittografia, e viceversa. Le chiavi usate dalle varie tecnologie possono coincidere o essere diverse, a seconda di come sono state configurate le opzioni di crittografia per ogni servizio.

## <a name="whats-the-difference-between-byok-and-hyok-and-when-should-i-use-them"></a>Qual è la differenza tra le modalità BYOK e HYOK e quando è opportuno usarle?

Quando si usa la modalità **BYOK** (Bring Your Own Key) nel contesto di Azure Information Protection, si crea una chiave personale locale per la protezione di Azure Rights Management. Si trasferisce quindi tale chiave a un modulo di protezione hardware (HSM) in Azure Key Vault in cui si continua a possedere e gestire la chiave. Se non si esegue questa operazione, la protezione di Azure Rights Management userà una chiave creata e gestita automaticamente in Azure. Questa configurazione predefinita è indicata come "Gestione di Microsoft" anziché come "Gestione del cliente" (l'opzione BYOK).

Per altre informazioni su BYOK e sull'opportunità di scegliere questa topologia di chiave per l'organizzazione, vedere [Pianificazione e implementazione della chiave del tenant di Azure Information Protection](../plan-design/plan-implement-tenant-key.md). 

La modalità **HYOK** (Hold Your Own Key) nel contesto di Azure Information Protection interessa un numero limitato di organizzazioni in cui è archiviato un subset di documenti o messaggi di posta elettronica che non possono essere protetti da una chiave archiviata nel cloud. Per tali organizzazioni, questa restrizione si applica anche se la chiave è stata creata e viene gestita tramite BYOK. La restrizione può essere spesso dovuta a requisiti normativi o di conformità e la configurazione HYOK deve essere applicata esclusivamente a informazioni altamente riservate, che non verranno mai condivise all'esterno dell'organizzazione, che verranno utilizzate solo nella rete interna e che non devono essere accessibili da dispositivi mobili. 

Per queste eccezioni (che in genere interessano meno del 10% dell'intero contenuto da proteggere), le organizzazioni possono creare la chiave da mantenere in locale usando una soluzione locale, Active Directory Rights Management Services. Con questa soluzione, i computer ottengono i criteri di Azure Information Protection dal cloud, ma il contenuto identificato può essere protetto tramite la chiave locale.

Per altre informazioni su HYOK e per assicurarsi di conoscere le restrizioni e le limitazioni di questa modalità e sapere quando è opportuno usarla, vedere [Requisiti e restrizioni HYOK per la protezione di AD RMS](../deploy-use/configure-adrms-restrictions.md).

## <a name="where-can-i-find-information-about-3rd-party-solutions-that-integrate-with-azure-rms"></a>Dove è possibile trovare informazioni su soluzioni di terze parti si integrano con Azure RMS?

Molti fornitori di software offrono o implementano già soluzioni in grado di integrarsi con Azure Rights Management e l'elenco di tali soluzioni cresce molto rapidamente. Può risultare utile visitare il [blog di Enterprise Mobility + Security](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services) e ottenere gli aggiornamenti più recenti da [Dan Plastina @TheRMSGuy](https://twitter.com/TheRMSGuy) su Twitter. In caso di domande specifiche, tuttavia, inviare un messaggio di posta elettronica al team di Information Protection: askipteam@microsoft.com.

## <a name="is-there-a-management-pack-or-similar-monitoring-mechanism-for-the-rms-connector"></a>Esiste un Management Pack o un meccanismo di controllo simile per il connettore RMS?

Il connettore Rights Management registra informazioni, avvisi e messaggi di errore nel registro eventi, ma non esiste un Management Pack che includa il monitoraggio di questi eventi. Tuttavia, l'elenco di eventi e le relative descrizioni con altre informazioni che consentono di adottare misure correttive è documentato [Monitorare il connettore di Azure Rights Management](../deploy-use/monitor-rms-connector.md).

## <a name="do-you-need-to-be-a-global-admin-to-configure-azure-rms-or-can-i-delegate-to-other-administrators"></a>È necessario essere un amministratore globale per configurare Azure RMS oppure tale configurazione può essere delegata ad altri amministratori?

Gli amministratori globali per un tenant di Office 365 o di Azure AD possono ovviamente eseguire tutte le attività amministrative per il servizio Azure Rights Management. Se tuttavia si vogliono assegnare autorizzazioni amministrative ad altri utenti, è possibile farlo usando il cmdlet [Add-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/dn629417.aspx) di Azure RMS PowerShell. È possibile assegnare questo ruolo amministrativo per account utente o per gruppo. Sono disponibili due ruoli: **amministratore globale** e **amministratore del connettore**. 

Come è possibile capire dal nome, il primo ruolo concede le autorizzazioni necessarie per eseguire tutte le attività amministrative per Azure Rights Management, senza rendere gli utenti interessati amministratori globali di altri servizi cloud, mentre il secondo ruolo concede le autorizzazioni necessarie per eseguire solo il connettore Rights Management (RMS).

Alcune osservazioni:

- Solo gli amministratori globali per Office 365 e gli amministratori globali per Azure AD possono configurare Azure RMS tramite i portali di gestione (l'interfaccia di amministrazione di Office 365 o il portale di Azure classico). Gli utenti a cui viene assegnato il ruolo di amministratore globale per Azure RMS devono configurare Azure RMS tramite i comandi di Azure RMS PowerShell. Per trovare con più facilità i cmdlet giusti per attività specifiche, vedere [Amministrazione di Azure Rights Management mediante Windows PowerShell](../deploy-use/administer-powershell.md).

- Se i [controlli di caricamento](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) sono stati configurati, ciò non influisce sulla possibilità di amministrare Azure RMS, fatta eccezione per il connettore RMS. Ad esempio, se i controlli di selezione sono stati configurati in modo da limitare la protezione del contenuto al gruppo "Reparto IT", l'account usato per installare e configurare il connettore RMS deve essere membro di tale gruppo. 

- Nessun amministratore per Azure RMS (l'amministratore globale del tenant o un amministratore globale di Azure RMS) può rimuovere automaticamente la protezione da documenti o messaggi di posta elettronica protetti da Azure RMS. Possono farlo solo gli utenti a cui è assegnato il ruolo di utente con privilegi avanzati, e solo quando la funzionalità utente con privilegi avanzati è abilitata. Tuttavia, l'amministratore globale del tenant e tutti gli amministratori globali di Azure RMS possono assegnare il ruolo di utente con privilegi avanzati a qualsiasi utente, compreso il proprio account. Possono anche abilitare la funzionalità utente con privilegi avanzati. Queste azioni vengono registrate nel registro amministratore di Azure RMS. Per altre informazioni, vedere la sezione sulle procedure consigliate in [Configurazione degli utenti con privilegi avanzati per Azure Rights Management e servizi di individuazione o ripristino dei dati](../deploy-use/configure-super-users.md). 


## <a name="i-have-a-hybrid-deployment-of-exchange-with-some-users-on-exchange-online-and-others-on-exchange-serveris-this-supported-by-azure-rms"></a>Dispongo di una distribuzione ibrida di Exchange con alcuni utenti su Exchange Online e altri su Exchange Server; questo è supportato da Azure RMS?
Assolutamente e l'aspetto interessante è che gli utenti saranno in grado di proteggere e utilizzare senza problemi messaggi di posta elettronica e allegati protetti con le due distribuzioni di Exchange. Per questa configurazione, [attivare Azure RMS](../deploy-use/activate-service.md) e [abilitare IRM per Exchange Online](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx), quindi [distribuire e configurare il connettore RMS](../deploy-use/deploy-rms-connector.md) per Exchange Server.

## <a name="if-i-use-this-protection-for-my-production-environment-is-my-company-then-locked-into-the-solution-or-risk-losing-access-to-content-that-we-protected-with-azure-rms"></a>Se si usa questa protezione nell'ambiente di produzione, l'azienda è costretta a usare sempre questa soluzione o esiste il rischio di perdere l'accesso ai contenuti protetti con Azure RMS?
No, si ha sempre il controllo dei dati e si può continuare ad accedervi, anche se si decide di non usare più il servizio Azure Rights Management. Per altre informazioni, vedere [Rimozione delle autorizzazioni e disattivazione di Azure Rights Management](../deploy-use/decommission-deactivate.md).

Tuttavia, prima di disabilitare la distribuzione di Azure RMS, desideriamo sapere e comprendere il motivo per cui è stata presa questa decisione. Se la tecnologia di protezione Azure Rights Management non soddisfa i requisiti aziendali, contattarci per sapere se sono previste nuove funzionalità per l'immediato futuro o se esistono alternative. Inviare un messaggio di posta elettronica a [AskIPTeam@Microsoft.com](mailto:askipteam@microsoft.com?subject=Planning%20to%20decommission%20Azure%20RMS) per informazioni sui requisiti tecnici e aziendali.

## <a name="can-i-control-which-of-my-users-can-use-azure-rms-to-protect-content"></a>È possibile determinare quali utenti possono usare Azure RMS per proteggere i contenuti?
Sì, il servizio Azure Rights Management include controlli di selezione utenti per questo scenario. Per altre informazioni, vedere la sezione [Configurazione dei controlli di selezione utenti per una distribuzione graduale](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) dell'articolo [Attivazione di Azure Rights Management](../deploy-use/activate-service.md).

## <a name="can-i-prevent-users-from-sharing-protected-documents-with-specific-organizations"></a>È possibile impedire agli utenti di condividere documenti protetti con aziende specifiche?
Uno dei vantaggi principali offerti dal servizio Azure Rights Management per la protezione dei dati è il supporto della collaborazione business-to-business senza che sia necessario configurare trust espliciti per ogni organizzazione partner, in quanto l'autenticazione viene eseguita automaticamente da Azure AD.

Non sono disponibili opzioni di amministrazione che consentano di impedire agli utenti di condividere documenti in modo sicuro con aziende specifiche. Si supponga, ad esempio, di voler bloccare un'azienda che non si considera attendibile o una società concorrente. Impedire al servizio Azure Rights Management di inviare documenti protetti agli utenti di queste società non ha alcuna utilità, in quanto gli utenti condividerebbero i documenti in modalità non protetta, con maggiori rischi per l'azienda stessa. Inoltre, non sarebbe possibile identificare gli utenti che condividono i documenti aziendali riservati e i rispettivi destinatari in queste aziende, mentre questo è possibile quando i documenti o i messaggi di posta elettronica sono protetti tramite il servizio Azure Rights Management.

## <a name="when-i-share-a-protected-document-with-somebody-outside-my-company-how-does-that-user-get-authenticated"></a>Quando condivido un documento protetto con qualcuno all'esterno della mia azienda, come viene autenticato questo utente?
Il servizio Azure Rights Management usa sempre un account di Azure Active Directory e un indirizzo di posta elettronica associato per l'autenticazione utente, semplificando la collaborazione business-to-business per gli amministratori. Se l'altra organizzazione utilizza i servizi di Azure, gli utenti avranno già account in Azure Active Directory, anche se questi account vengono creati e gestiti in locale e poi sincronizzati in Azure. Se l'organizzazione dispone di Office 365, dietro le quinte, questo servizio utilizza anche Azure Active Directory per gli account utente. Se nell'organizzazione dell'utente non esistono account gestiti in Azure, gli utenti possono iscriversi a [RMS per utenti singoli](../understand-explore/rms-for-individuals.md), che consente di creare un tenant e una directory di Azure non gestiti per l'organizzazione con un account per l'utente, in modo che questo utente e gli utenti successivi possano quindi essere autenticati per il servizio Azure Rights Management.

Il metodo di autenticazione per questi account può variare a seconda di come l'amministratore dell’altra organizzazione ha configurato gli account di Azure Active Directory. Ad esempio, è possibile utilizzare password create per questi account, Multi-Factor Authentication (MFA), la federazione o password create in servizi di dominio di Active Directory e quindi sincronizzate con Azure Active Directory.

## <a name="can-i-add-external-users-people-from-outside-my-company-to-custom-templates"></a>È possibile aggiungere utenti esterni (persone all'esterno della mia azienda) ai modelli personalizzati?
Sì. La creazione di modelli personalizzati che gli utenti finali (e gli amministratori) possono scegliere dalle applicazioni rende rapida e semplice l’applicazione della protezione delle informazioni, attraverso i criteri specificati. Una delle impostazioni nel modello riguarda chi è in grado di accedere al contenuto ed è possibile specificare utenti e gruppi interni o esterni all'organizzazione. 

Per specificare gli utenti esterni all'organizzazione, aggiungerli come contatti a un gruppo da selezionare nel portale di Azure classico quando si configurano i modelli. Per specificare gruppi esterni all'organizzazione, è necessario usare il [modulo di Windows PowerShell per Azure Rights Management](../deploy-use/install-powershell.md), che è anche possibile usare per specificare singoli utenti esterni, nonché tutti gli utenti di un'altra organizzazione:

-   **Usare un oggetto di definizione dei diritti per creare o aggiornare un modello**:    specificare gli indirizzi di posta elettronica esterni e i relativi diritti in un oggetto di definizione dei diritti, che verrà quindi usato per creare o aggiornare un modello. È possibile specificare l'oggetto di definizione dei diritti usando il cmdlet [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) per creare una variabile e quindi fornire questa variabile al parametro -RightsDefinition con il cmdlet [Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx) (per un nuovo modello) o [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx) (per modificare un modello esistente). Tuttavia, se si stanno aggiungendo questi utenti a un modello esistente, sarà necessario definire gli oggetti di definizione dei diritti per i gruppi esistenti nei modelli e non solo gli utenti esterni.

Per altre informazioni sui modelli personalizzati, vedere [Configurazione di modelli personalizzati per il servizio Azure Rights Management](../deploy-use/configure-custom-templates.md).

## <a name="does-azure-rms-work-with-dynamic-groups-in-azure-ad"></a>Azure RMS funziona con i gruppi dinamici in Azure AD?
Una funzionalità di Azure AD Premium consente di configurare l'appartenenza dinamica per gruppi specificando [regole basate su attributi](https://azure.microsoft.com/documentation/articles/active-directory-accessmanagement-groups-with-advanced-rules/). Quando si crea un gruppo di sicurezza in Azure AD, questo tipo di gruppo supporta l'appartenenza dinamica, ma non supporta un indirizzo di posta elettronica e pertanto non può essere usato con il servizio Azure Rights Management. Tuttavia, ora è possibile creare un nuovo tipo di gruppo in Azure AD che supporta sia l'appartenenza dinamica ed è abilitato alla posta elettronica. Quando si aggiunge un nuovo gruppo nel portale classico di Azure, è possibile scegliere di **TIPO DI GRUPPO** dell'**"Anteprima" Office 365**. Poiché questo gruppo è abilitato alla posta elettronica, è possibile usarlo con la protezione Azure Rights Management.

## <a name="what-devices-and-which-file-types-are-supported-by-azure-rms"></a>Quali dispositivi e quali tipi di file sono supportati da Azure RMS?
Per un elenco dei dispositivi che supportano il servizio Azure Rights Management, vedere [Dispositivi client che supportano la protezione dati di Azure Rights Management](../get-started/requirements-client-devices.md). Dal momento che non tutti i dispositivi supportati consentono l'uso di tutte le funzionalità di Rights Management, assicurarsi di controllare anche la tabella in [Applicazioni che supportano la protezione dati di Azure Rights Management](../get-started/requirements-applications.md).

Il servizio Azure Rights Management può supportare tutti i tipi di file. Per file di testo e di immagine, file di Microsoft Office (Word, Excel e PowerPoint), file con estensione pdf e altri tipi di file di applicazione, Azure Rights Management fornisce la protezione nativa, incluse crittografia e applicazione di diritti (autorizzazioni). Per tutte le altre applicazioni e tipi di file, la protezione generica fornisce funzionalità di incapsulamento e autenticazione dei file che consentono di verificare se un utente è autorizzato ad aprire il file.

Per un elenco delle estensioni di file supportate in modo nativo da Azure Rights Management, vedere [Tipi di file supportati dal client Azure Information Protection](../rms-client/client-admin-guide-file-types.md). Le estensioni di file non incluse nell'elenco sono supportate mediante l'uso del client Azure Information Protection, che applica automaticamente la protezione generica a tali file.

## <a name="when-i-open-an-rms-protected-office-document-does-the-associated-temporary-file-become-rms-protected-as-well"></a>Quando si apre un documento di Office protetto da RMS, anche il file temporaneo associato è protetto da RMS?

No. In questo scenario, il file temporaneo associato non contiene i dati del documento originale, ma solo i dati immessi dall'utente mentre il file è aperto. A differenza del file originale, il file temporaneo non è destinato alla condivisione e rimarrà disponibile nel dispositivo, protetto dai controlli di protezione locali, ad esempio BitLocker ed EFS.

## <a name="we-really-want-to-use-byok-with-azure-information-protection-but-learned-that-this-isnt-compatible-with-exchange-onlinewhats-your-advice"></a>Si vuole usare la modalità BYOK con Azure Information Protection, ma si è appreso che questa non è compatibile con Exchange Online. Quale soluzione è preferibile adottare?
Non lasciare che questa limitazione attuale ritardi la distribuzione del servizio Azure Rights Management di Azure Information Protection. Se si dispone di Exchange Online e si vuole usare la modalità BYOK, è consigliabile distribuire Azure Information Protection nella modalità predefinita per la gestione delle chiavi, in base alla quale Microsoft genera e gestisce la chiave. In questo modo, si ottengono ora tutti i vantaggi della protezione di file e messaggi di posta elettronica importanti, con l'opzione per passare a BYOK in un secondo momento (ad esempio, quando Exchange Online supporterà BYOK). Quando si passa alla modalità BYOK, i documenti precedentemente protetti e i messaggi di posta elettronica rimangono comunque accessibili tramite una chiave archiviata.

Tuttavia, se i criteri aziendali richiedono di usare un modulo di protezione hardware (HSM) e ciò altrimenti bloccherebbe la distribuzione di Azure Information Protection, un'altra soluzione consiste nel distribuire subito Azure Information Protection con la modalità BYOK, con funzionalità di protezione di Rights Management ridotte per Exchange. Per altre informazioni, vedere [Prezzi e restrizioni BYOK](../plan-design/byok-price-restrictions.md) da [pianificazione e implementazione della chiave del tenant Azure Rights Management](../plan-design/plan-implement-tenant-key.md).

## <a name="a-feature-i-am-looking-for-doesnt-seem-to-work-with-sharepoint-protected-librariesis-support-for-my-feature-planned"></a>Una funzionalità che cerco non sembra funzionare con le librerie protette di SharePoint, è previsto il supporto per la mia funzionalità?
Attualmente, SharePoint supporta documenti protetti da Rights Management usando le librerie protette IRM, che non supportano i modelli personalizzati, il rilevamento dei documenti e alcune altre funzionalità. Per altre informazioni, vedere la sezione [SharePoint Online e SharePoint Server](../understand-explore/office-apps-services-support.md#sharepoint-online-and-sharepoint-server) nell'articolo [Servizi e applicazioni di Office](../understand-explore/office-apps-services-support.md).

Se si è interessati a una funzionalità specifica non ancora supportata, assicurarsi di controllare gli annunci nel [blog di Enterprise Mobility + Security](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services).

## <a name="how-do-i-configure-one-drive-for-business-in-sharepoint-online-so-that-users-can-safely-share-their-files-with-people-inside-and-outside-the-company"></a>Come è possibile configurare One Drive for Business in SharePoint Online, in modo che gli utenti possano condividere i propri file in modo sicuro con le persone all'interno e all'esterno della società?
Per impostazione predefinita, in qualità di amministratore di Office 365, non si configura questo oggetto. L'operazione viene eseguita dagli utenti.

Proprio come gli amministratori del sito di SharePoint abilitano e configurano IRM per una raccolta di SharePoint che possiedono, OneDrive for Business è progettato per consentire agli utenti di attivare e configurare IRM per la propria raccolta OneDrive for Business. Tuttavia, usando PowerShell, è possibile eseguire questa operazione per gli utenti. Per istruzioni, vedere la sezione [SharePoint Online e OneDrive for Business: configurazione di IRM](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration) dell'articolo [Office 365: configurazione di client e servizi online](../deploy-use/configure-office365.md).

## <a name="do-you-have-any-tips-or-tricks-for-a-successful-deployment"></a>Sono disponibili suggerimenti per una corretta distribuzione?
Dopo aver supervisionato un elevato numero di distribuzioni e ascoltato il parere di clienti, partner, consulenti e tecnici del servizio di supporto, uno dei principali suggerimenti che possiamo fornire è **Progettare e distribuire criteri semplici per i diritti d'uso**.

Poiché Azure Information Protection supporta la condivisione sicura con qualsiasi utente, si possono raggiungere livelli di protezione dei dati molto elevati, ma bisogna impostare criteri rigorosi per i diritti d'uso. Per la maggior parte delle organizzazioni, l'impatto maggiore risulta dall'esigenza di impedire la perdita dei dati applicando il modello predefinito dei criteri per i diritti d'uso che limita l'accesso agli utenti dell'organizzazione. Si possono anche applicare criteri più specifici, ad esempio impedire agli utenti di stampare o modificare documenti, ma è preferibile impostarli solo per documenti che richiedono un alto livello di sicurezza. Evitare di applicare tutti questi criteri più restrittivi in un'unica soluzione pianificandone invece un approccio per fasi.

## <a name="how-do-we-regain-access-to-files-that-were-protected-by-an-employee-who-has-now-left-the-organization"></a>Come possiamo riottenere l'accesso ai file che sono stati protetti da un dipendente che ora ha lasciato l'organizzazione?
Usare la [funzionalità per utenti con privilegi avanzati](../deploy-use/configure-super-users.md), che consente agli utenti autorizzati di disporre di diritti completi di utilizzo per tutte le licenze d'uso che sono state concesse dal tenant dell'organizzazione. Questa stessa funzionalità consente ai servizi autorizzati di indicizzare e analizzare i file, in base alle esigenze.

## <a name="when-i-test-revocation-in-the-document-tracking-site-i-see-a-message-that-says-people-can-still-access-the-document-for-up-to-30-daysis-this-time-period-configurable"></a>Quando si testa una revoca nel sito di rilevamento del documento, viene visualizzato un messaggio che informa che gli utenti possono ancora accedere al documento per 30 giorni. È possibile configurare questo periodo di tempo?

Sì. Questo messaggio indica la licenza d'uso per il file specifico. Una licenza d'uso è un certificato associato a un documento. Viene concesso a un utente che apre un file o un messaggio e-mail protetto. Questo certificato contiene i diritti dell'utente per il file o per il messaggio di posta elettronica e la chiave di crittografia usata per crittografare il contenuto, nonché altre restrizioni di accesso definite nei criteri del documento. Quando il periodo di validità della licenza d'uso scade e l'utente tenta di aprire il file o il messaggio di posta elettronica, è necessario che le credenziali dell'utente vengano inviate di nuovo al servizio Azure Rights Management. 

Se si revoca un file, tale azione può essere imposta solo quando l'utente si autentica al servizio Azure Rights Management. Pertanto, se un file ha un periodo di validità della licenza d'uso di 30 giorni e l'utente ha già aperto il documento, tale utente continuerà ad avere accesso al documento per la durata della licenza d'uso. Quando la licenza d'uso scade, l'utente deve ripetere l'autenticazione e a questo punto verrà negato l'accesso perché il documento è ora revocato.

Il valore predefinito per il periodo di validità della licenza d'uso per un tenant è di 30 giorni ed è possibile configurare questo valore tramite il cmdlet PowerShell, [Set-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932063.aspx). Questa impostazione può essere sostituita da un'impostazione più restrittiva in un modello personalizzato. 

Per altre informazioni ed esempi su come funziona la licenza d'uso, vedere la descrizione dettagliata di [Set-AadrmMaxUseLicenseValidityTime](https://msdn.microsoft.com/library/azure/dn932063.aspx).

## <a name="can-rights-management-prevent-screen-captures"></a>Rights Management può impedire l'acquisizione di schermate?
Non concedendo **Copia** [come diritto di uso](../deploy-use/configure-usage-rights.md), Rights Management può impedire l'acquisizione di schermate dagli strumenti più usati per l'acquisizione di schermate nelle piattaforme Windows (Windows 7, Windows 8.1, Windows 10, Windows Phone) e Android. I dispositivi iOS e Mac, tuttavia, non consentono ad alcuna app di impedire l'acquisizione di schermate e i browser, ad esempio se usati con Outlook Web App e Office Online, non possono impedire l'acquisizione di schermate.

Impedire l'acquisizione di schermate può consentire di evitare la diffusione accidentale o non appropriata di informazioni riservate o sensibili. Tuttavia, vi sono molti modi in cui un utente può condividere i dati visualizzati sullo schermo e acquisire una schermata è solo uno di questi metodi. Ad esempio, un utente che desidera condividere informazioni visualizzate può scattare una foto dei dati con la fotocamera del telefono, ridigitarli o semplicemente comunicarli verbalmente a qualcuno.

Come illustrato da questi esempi, anche se tutte le piattaforme e tutto il software supportassero le API di Rights Management per il blocco dell'acquisizione di schermate, la sola tecnologia non sarebbe in grado di impedire sempre agli utenti di condividere dati che dovrebbero essere riservati. Rights Management può contribuire a salvaguardare i dati importanti tramite i criteri di autorizzazione e per l'uso, ma questa soluzione aziendale per la gestione delle autorizzazioni deve essere usata insieme ad altri controlli. Ad esempio, implementare la sicurezza fisica, selezionare e monitorare attentamente le persone che hanno accesso in modo autorizzato ai dati dell'organizzazione e investire nella formazione degli utenti per aiutarli a capire quali dati non devono essere condivisi.

## <a name="whats-the-difference-between-a-user-protecting-an-email-with-do-not-forward-and-a-template-that-doesnt-include-the-forward-right"></a>Qual è la differenza tra un utente che protegge un messaggio di posta elettronica con l'opzione Non inoltrare e un modello che non include il diritto di inoltro?

Nonostante il nome e l'aspetto, l'opzione **Non inoltrare** non è il contrario dell'inoltro immediato né un modello. Si tratta in realtà di un insieme di diritti che limitano la copia, la stampa, il salvataggio di allegati e l'inoltro dei messaggi di posta elettronica. I diritti vengono applicati dinamicamente agli utenti tramite i destinatari scelti anziché in modo statico in base alle assegnazioni dall'amministratore. Per altre informazioni, vedere la sezione [Do Not Forward option for emails](../deploy-use/configure-usage-rights.md#do-not-forward-option-for-emails) (Opzione Non inoltrare per i messaggi di posta elettronica) dell'articolo [Configuring usage rights for Azure Rights Management](../deploy-use/configure-usage-rights.md) (Configurazione dei diritti di utilizzo per Azure Rights Management).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



