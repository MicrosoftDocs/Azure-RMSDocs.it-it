---
title: Domande frequenti su Azure Rights Management| Azure RMS
description: Alcune domande frequenti su Microsoft Azure Rights Management, noto anche come Azure RMS.
author: cabailey
manager: mbaldwin
ms.date: 09/29/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 71ce491f-41c1-4d15-9646-455a6eaa157d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 47328bc0c3cc66e99a98b7c8abc553f25d956404
ms.openlocfilehash: e485286a0bd42bbcfb46a8aabe4d2ee66d65b4a1


---

# Domande frequenti su Azure Rights Management

>*Si applica a: Azure Rights Management, Office 365*

Alcune domande frequenti su Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], noto anche come Azure RMS:

## Quali sono i requisiti necessari e i passaggi da eseguire per distribuire Azure RMS?
Vedere innanzitutto l'argomento [Requisiti per Azure Rights Management](requirements-azure-rms.md) contenente informazioni su opzioni di sottoscrizione cloud, modalità d'uso dei server locali con Azure RMS, scenari di distribuzione attualmente non supportati e applicazioni e dispositivi supportati da Azure RMS, e un collegamento se si ha bisogno di un elenco di indirizzi IP e di nomi di dominio per firewall o server proxy. 

Può essere utile vedere anche gli altri argomenti della sezione **Introduzione** e della sezione **Comprendere ed esplorare** per comprendere l'uso di [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] per proteggere i dati dell'organizzazione, il funzionamento del servizio con le applicazioni, il confronto con la versione locale di Active Directory Rights Management e i termini e le abbreviazioni specifiche di [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

Per continuare, quindi, usare la [Guida di orientamento per la distribuzione di Microsoft Azure Rights Management](../plan-design/deployment-roadmap.md).

## Per essere protetti da Azure RMS, i file devono trovarsi sul cloud?
No, questo è un malinteso comune. Il servizio Azure Rights Management e Microsoft non visualizzano o archiviano i dati dell'utente come parte del processo di protezione delle informazioni. Le informazioni protette non vengono mai inviate o archiviate in Azure, a meno di archiviarle in modo esplicito in Azure o di usare un altro servizio cloud che le archivia in Azure. 

Per ulteriori informazioni, vedere [Funzionamento di Azure RMS Dietro le quinte](../understand-explore/how-does-it-work.md) per comprendere come la formula segreta per una bevanda gassata creata e archiviata in locale viene protetta da Azure RMS pur rimanendo in locale.

## È possibile integrare Azure RMS con il server locale?
Sì. Azure RMS può essere integrato con i server in locale, ad esempio Exchange Server, SharePoint e file server Windows. A tale scopo, si usa il [Connettore Rights Management](../deploy-use/deploy-rms-connector.md). In alternativa, se si è solo interessati all'uso dell'infrastruttura di classificazione file con Windows Server, vedere [Protezione RMS con l'infrastruttura di classificazione file (FCI, File Classification Infrastructure) per Windows Server](https://technet.microsoft.com/library/mt601315%28v=ws.10%29.aspx). È inoltre possibile sincronizzare ed eseguire la federazione dei controller di dominio di Active Directory con Azure AD per un'esperienza di autenticazione più semplice per gli utenti, ad esempio utilizzando [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/).

Azure RMS genera e gestisce automaticamente i certificati XrML come richiesto, quindi non usa un'infrastruttura PKI locale. Per altre informazioni sull'uso dei certificati in Azure RMS, vedere la sezione [Procedura dettagliata del funzionamento di Azure RMS: primo uso, protezione dei contenuti, uso del contenuto](../understand-explore/how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) nell'articolo [Funzionamento di Azure RMS](../understand-explore/how-does-it-work.md).

## Dove è possibile trovare informazioni su soluzioni di terze parti si integrano con Azure RMS?

Molti fornitori di software offrono o implementano già soluzioni in grado di integrarsi con Azure RMS e l'elenco di tali soluzioni cresce molto rapidamente. Potrebbe risultare utile visitare l'[Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services) (Blog sulla mobilità e la sicurezza aziendale) e ottenere gli aggiornamenti più recenti da [Dan Plastina @TheRMSGuy](https://twitter.com/TheRMSGuy) su Twitter. In caso di domande specifiche, tuttavia, inviare un messaggio di posta elettronica al team di Information Protection: askipteam@microsoft.com.

## Esiste un Management Pack o un meccanismo di controllo simile per il connettore RMS?

Il connettore Rights Management registra informazioni, avvisi e messaggi di errore nel registro eventi, ma non esiste un Management Pack che includa il monitoraggio di questi eventi. Tuttavia, l'elenco di eventi e le relative descrizioni con altre informazioni che consentono di adottare misure correttive è documentato [Monitorare il connettore di Azure Rights Management](../deploy-use/monitor-rms-connector.md).

## È necessario essere un amministratore globale per configurare Azure RMS oppure tale configurazione può essere delegata ad altri amministratori?

Gli amministratori globali per un tenant di Office 365 o di Azure AD possono ovviamente eseguire tutte le attività amministrative per Azure RMS. Se tuttavia si vogliono assegnare autorizzazioni amministrative ad altri utenti, è possibile farlo usando il cmdlet [Add-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/dn629417.aspx) di Azure RMS PowerShell. È possibile assegnare questo ruolo amministrativo per account utente o per gruppo. Sono disponibili due ruoli: **amministratore globale** e **amministratore del connettore**. 

Come è possibile capire dal nome, il primo ruolo concede le autorizzazioni necessarie per eseguire tutte le attività amministrative per Azure Rights Management, senza rendere gli utenti interessati amministratori globali di altri servizi cloud, mentre il secondo ruolo concede le autorizzazioni necessarie per eseguire solo il connettore Rights Management (RMS).

Alcune osservazioni:

- Solo gli amministratori globali per Office 365 e gli amministratori globali per Azure AD possono configurare Azure RMS tramite i portali di gestione (l'interfaccia di amministrazione di Office 365 o il portale di Azure classico). Gli utenti a cui viene assegnato il ruolo di amministratore globale per Azure RMS devono configurare Azure RMS tramite i comandi di Azure RMS PowerShell. Per trovare con più facilità i cmdlet giusti per attività specifiche, vedere [Amministrazione di Windows Azure Rights Management mediante Windows PowerShell](../deploy-use/administer-powershell.md).

- Se i [controlli di caricamento](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) sono stati configurati, ciò non influisce sulla possibilità di amministrare Azure RMS, fatta eccezione per il connettore RMS. Ad esempio, se i controlli di selezione sono stati configurati in modo da limitare la protezione del contenuto al gruppo "Reparto IT", l'account usato per installare e configurare il connettore RMS deve essere membro di tale gruppo. 

- Nessun amministratore per Azure RMS (l'amministratore globale del tenant o un amministratore globale di Azure RMS) può rimuovere automaticamente la protezione da documenti o messaggi di posta elettronica protetti da Azure RMS. Possono farlo solo gli utenti a cui è assegnato il ruolo di utente con privilegi avanzati, e solo quando la funzionalità utente con privilegi avanzati è abilitata. Tuttavia, l'amministratore globale del tenant e tutti gli amministratori globali di Azure RMS possono assegnare il ruolo di utente con privilegi avanzati a qualsiasi utente, compreso il proprio account. Possono anche abilitare la funzionalità utente con privilegi avanzati. Queste azioni vengono registrate nel registro amministratore di Azure RMS. Per altre informazioni, vedere la sezione sulle procedure consigliate in [Configurazione degli utenti con privilegi avanzati per Azure Rights Management e servizi di individuazione o ripristino dei dati](../deploy-use/configure-super-users.md). 


## Dispongo di una distribuzione ibrida di Exchange con alcuni utenti su Exchange Online e altri su Exchange Server; questo è supportato da Azure RMS?
Assolutamente e l'aspetto interessante è che gli utenti saranno in grado di proteggere e utilizzare senza problemi messaggi di posta elettronica e allegati protetti con le due distribuzioni di Exchange. Per questa configurazione, [attivare Azure RMS](../deploy-use/activate-service.md) e [abilitare IRM per Exchange Online](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx), quindi [distribuire e configurare il connettore RMS](../deploy-use/deploy-rms-connector.md) per Exchange Server.

## Sono disponibili istruzioni dettagliate per configurare Exchange Online per l'uso di Azure RMS?

Sì. Vedere [Exchange Online: configurazione di IRM](../deploy-use/configure-office365.md#exchange-online-irm-configuration) per visualizzare un set tipico di comandi che consentono a Exchange Online di usare Azure RMS, le informazioni sul motivo per cui Outlook Web App non visualizza immediatamente le opzioni di menu **Imposta autorizzazioni** e il comando da eseguire in caso di modifica o aggiornamento dei modelli di Azure RMS. 

## Se si distribuisce Azure RMS nell'ambiente di produzione, l’azienda è bloccata nella soluzione o esiste il rischio di perdere l'accesso ai contenuti protetti con Azure RMS?
No, si ha sempre il controllo dei dati e si può continuare ad accedere ad essi, anche se si decide di non usare più Azure RMS. Per altre informazioni, vedere [Rimozione delle autorizzazioni e disattivazione di Azure Rights Management](../deploy-use/decommission-deactivate.md).

Tuttavia, prima di disabilitare la distribuzione di Azure RMS, desideriamo sapere e comprendere il motivo per cui è stata presa questa decisione. Se Azure RMS non soddisfa i requisiti aziendali, contattarci per sapere se sono previste nuove funzionalità per l'immediato futuro o se esistono alternative. Inviare un messaggio di posta elettronica a [AskIPTeam@Microsoft.com](mailto:askipteam@microsoft.com?subject=Planning%20to%20decommission%20Azure%20RMS) e saremo lieti di discutere i requisiti tecnici e aziendali.

## È possibile determinare quali utenti possono usare Azure RMS per proteggere i contenuti?
Sì, Azure RMS include controlli di selezione utenti per questo scenario. Per altre informazioni, vedere la sezione [Configurazione dei controlli di selezione utenti per una distribuzione graduale](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) dell'articolo [Attivazione di Azure Rights Management](../deploy-use/activate-service.md).

## È possibile impedire agli utenti di condividere documenti protetti con aziende specifiche?
Uno dei vantaggi principali offerti da Azure RMS è il supporto della collaborazione business-to-business senza che sia necessario configurare trust espliciti per ciascuna azienda partner, in quanto l'autenticazione viene eseguita automaticamente da Azure AD.

Non sono disponibili opzioni di amministrazione che consentano di impedire agli utenti di condividere documenti in modo sicuro con aziende specifiche. Si supponga, ad esempio, di voler bloccare un'azienda che non si considera attendibile o una società concorrente. Impedire ad Azure RMS di inviare documenti protetti agli utenti di queste società non ha alcuna utilità, in quanto gli utenti condividerebbero i documenti in modalità non protetta, con maggiori rischi per l'azienda stessa. Inoltre, non sarebbe possibile identificare gli utenti che condividono i documenti aziendali riservati e i rispettivi destinatari in queste aziende, mentre questo è possibile quando i documenti o le email sono protetti tramite Azure RMS.

## Quando condivido un documento protetto con qualcuno all'esterno della mia azienda, come viene autenticato questo utente?
Azure RMS utilizza sempre un account di Azure Active Directory e un indirizzo di posta elettronica associato per l'autenticazione utente, semplificando la collaborazione business-to-business per gli amministratori. Se l'altra organizzazione utilizza i servizi di Azure, gli utenti avranno già account in Azure Active Directory, anche se questi account vengono creati e gestiti in locale e poi sincronizzati in Azure. Se l'organizzazione dispone di Office 365, dietro le quinte, questo servizio utilizza anche Azure Active Directory per gli account utente. Se nell'organizzazione dell'utente non esistono account gestiti in Azure, gli utenti possono iscriversi a [RMS per utenti singoli](../understand-explore/rms-for-individuals.md), che consente di creare un tenant e una directory di Azure non gestiti per l'organizzazione con un account per l'utente, in modo che questo utente e gli utenti successivi possano quindi essere autenticati per Azure RMS.

Il metodo di autenticazione per questi account può variare a seconda di come l'amministratore dell’altra organizzazione ha configurato gli account di Azure Active Directory. Ad esempio, è possibile utilizzare password create per questi account, Multi-Factor Authentication (MFA), la federazione o password create in servizi di dominio di Active Directory e quindi sincronizzate con Azure Active Directory.

## È possibile aggiungere utenti all'esterno della mia azienda per i modelli personalizzati?
Sì. La creazione di modelli personalizzati che gli utenti finali (e gli amministratori) possono scegliere dalle applicazioni rende rapida e semplice l’applicazione della protezione delle informazioni, attraverso i criteri specificati. Una delle impostazioni nel modello riguarda chi è in grado di accedere al contenuto ed è possibile specificare utenti e gruppi all'interno dell'organizzazione e utenti al suo esterno.

Per specificare gli utenti esterni all'organizzazione, aggiungerli come contatti a un gruppo da selezionare nel portale di Azure classico quando si configurano i modelli. In alternativa, usare il [modulo Windows PowerShell per Microsoft Azure Rights Management](../deploy-use/install-powershell.md):

-   **Usare un oggetto di definizione dei diritti per creare o aggiornare un modello**:    specificare gli indirizzi di posta elettronica esterni e i relativi diritti in un oggetto di definizione dei diritti, che verrà quindi usato per creare o aggiornare un modello. È possibile specificare l'oggetto di definizione dei diritti usando il cmdlet [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) per creare una variabile e quindi fornire questa variabile al parametro -RightsDefinition con il cmdlet [Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx) (per un nuovo modello) o [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx) (per modificare un modello esistente). Tuttavia, se si stanno aggiungendo questi utenti a un modello esistente, sarà necessario definire gli oggetti di definizione dei diritti per i gruppi esistenti nei modelli e non solo gli utenti esterni.

Per altre informazioni sui modelli personalizzati, vedere l'articolo relativo alla [configurazione di modelli personalizzati per Azure Rights Management](../deploy-use/configure-custom-templates.md).

## Azure RMS funziona con i gruppi dinamici in Azure AD?
Una funzionalità di Azure AD Premium consente di configurare l'appartenenza dinamica per gruppi specificando [regole basate su attributi](https://azure.microsoft.com/documentation/articles/active-directory-accessmanagement-groups-with-advanced-rules/). Quando si crea un gruppo di sicurezza in Azure AD, questo tipo di gruppo supporta l'appartenenza dinamica, ma non supporta un indirizzo email e pertanto non può essere usato con Azure RMS. Tuttavia, ora è possibile creare un nuovo tipo di gruppo in Azure AD che supporta sia l'appartenenza dinamica ed è abilitato alla posta elettronica. Quando si aggiunge un nuovo gruppo nel portale classico di Azure, è possibile scegliere di **TIPO DI GRUPPO** dell'**"Anteprima" Office 365**. Poiché questo gruppo è abilitato alla posta elettronica, è possibile usarlo con Azure RMS.

Come il nome opzionale mostra chiaramente, il nuovo tipo di gruppo è ancora in anteprima, con la funzionalità aggiuntiva prevista e la nuova documentazione da seguire. Nel frattempo, desideravamo confermare che è possibile usare questo nuovo tipo di gruppo con Azure RMS.


## Quali dispositivi e quali tipi di file sono supportati da Azure RMS?
Per un elenco dei dispositivi supportati, vedere [Requisiti per Azure RMS: dispositivi client che supportano Azure RMS](../get-started/requirements-client-devices.md). Dal momento che non tutti i dispositivi supportati consentono l'uso di tutte le funzionalità RMS, vedere anche la tabella in [Requisiti per Azure RMS: applicazioni](../get-started/requirements-applications.md).

Azure RMS supporta tutti i tipi di file. Per file di testo, di immagine, di Microsoft Office (file di Word, Excel e PowerPoint), file .pdf e alcuni altri tipi di file di applicazione, Azure RMS fornisce protezione nativa, incluse crittografia e applicazione di diritti (autorizzazioni). Per tutte le altre applicazioni e tipi di file, la protezione generica fornisce funzionalità di incapsulamento e autenticazione dei file che consentono di verificare se un utente è autorizzato ad aprire il file.

Per un elenco delle estensioni di file supportate in modo nativo da Azure RMS, vedere la sezione [Tipi di file e estensioni di file supportati](../rms-client/sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions) della [Guida dell'amministratore dell'applicazione di condivisione Rights Management](../rms-client/sharing-app-admin-guide.md). Le estensioni di file non incluse nell'elenco sono supportate mediante l'uso dell'applicazione RMS sharing, che applica automaticamente la protezione generica a tali file.

## Quando si apre un documento di Office protetto da RMS, anche il file temporaneo associato è protetto da RMS?

No. In questo scenario, il file temporaneo associato non contiene i dati del documento originale, ma solo i dati immessi dall'utente mentre il file è aperto. A differenza del file originale, il file temporaneo non è destinato alla condivisione e rimarrà disponibile nel dispositivo, protetto dai controlli di protezione locali, ad esempio BitLocker ed EFS.

## Quando verrà supportata la migrazione da AD RMS?
La migrazione da una distribuzione locale di Rights Management, ad esempio AD RMS, non è stata supportata nelle versioni iniziali di Azure RMS, ma è attualmente supportata.

Per altre informazioni, vedere [Migrazione da AD RMS ad Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

## Desideriamo davvero utilizzare BYOK con Azure RMS, ma abbiamo appreso che non è compatibile con Exchange Online, cosa consigliate?
Non lasciare che questa limitazione attuale ritardi la distribuzione di Azure RMS. Se si dispone di Exchange Online e si desidera utilizzare BYOK, si consiglia di distribuire Azure RMS nella modalità predefinita per la gestione delle chiavi, con cui Microsoft genera e gestisce la chiave. In questo modo, si ottengono ora tutti i vantaggi della protezione di file e messaggi di posta elettronica importanti, con l'opzione per passare a BYOK in un secondo momento (ad esempio, quando Exchange Online supporterà BYOK). Quando si passa alla modalità BYOK, i documenti precedentemente protetti e i messaggi di posta elettronica rimangono comunque accessibili tramite una chiave archiviata.

Tuttavia, se i criteri aziendali richiedono di utilizzare un modulo di protezione hardware (HSM) e ciò altrimenti bloccherebbe la distribuzione di Azure RMS, un'altra opzione consiste nel distribuire Azure RMS con BYOK ora, con funzionalità di RMS ridotte per Exchange. Per altre informazioni, vedere [Prezzi e restrizioni BYOK](../plan-design/byok-price-restrictions.md) da [pianificazione e implementazione della chiave del tenant Azure Rights Management](../plan-design/plan-implement-tenant-key.md).

## Una funzionalità che cerco non sembra funzionare con le librerie protette di SharePoint, è previsto il supporto per la mia funzionalità?
Attualmente, SharePoint supporta documenti protetti da RMS utilizzando le librerie protette IRM, che non supportano i modelli personalizzati, il rilevamento dei documenti e alcune altre funzionalità. Per ulteriori informazioni, vedere la sezione [SharePoint Online e SharePoint Server](../understand-explore/office-apps-services-support.md#sharepoint-online-and-sharepoint-server) nell'articolo [Servizi e applicazioni di Office](../understand-explore/office-apps-services-support.md).

Se si è interessati a una funzionalità specifica non ancora supportata, assicurarsi di controllare gli annunci nell'[Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services) (Blog sulla mobilità e la sicurezza aziendale).

## Come è possibile configurare One Drive for Business in SharePoint Online, in modo che gli utenti possano condividere i propri file in modo sicuro con le persone all'interno e all'esterno della società?
Per impostazione predefinita, in qualità di amministratore di Office 365, non si configura questo oggetto. L'operazione viene eseguita dagli utenti.

Proprio come gli amministratori del sito di SharePoint abilitano e configurano IRM per una raccolta di SharePoint che possiedono, OneDrive for Business è progettato per consentire agli utenti di attivare e configurare IRM per la propria raccolta OneDrive for Business.  Tuttavia, usando PowerShell, è possibile eseguire questa operazione per gli utenti. Per istruzioni, vedere la sezione [SharePoint Online e OneDrive for Business: configurazione di IRM](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration) dell'articolo [Office 365: configurazione di client e servizi online](../deploy-use/configure-office365.md).

## Sono disponibili suggerimenti per una corretta distribuzione di RMS?
Dopo aver supervisionato un elevato numero di distribuzioni e ascoltato il parere di clienti, partner, consulenti e tecnici del servizio di supporto, uno dei principali suggerimenti che possiamo fornire è **Progettare e distribuire criteri semplici per i diritti d'uso**.

Poiché Azure RMS supporta la condivisione sicura dei dati con qualsiasi utente, si possono raggiungere livelli di protezione delle informazioni molto elevati, ma bisogna impostare criteri rigorosi per i diritti d'uso. Per la maggior parte delle organizzazioni, l'impatto maggiore risulta dall'esigenza di impedire la perdita dei dati applicando il modello predefinito dei criteri per i diritti d'uso che limita l'accesso agli utenti dell'organizzazione. Si possono anche applicare criteri più specifici, ad esempio impedire agli utenti di stampare o modificare documenti, ma è preferibile impostarli solo per documenti che richiedono un alto livello di sicurezza. Evitare di applicare tutti questi criteri più restrittivi in un'unica soluzione pianificandone invece un approccio per fasi.

## Quali funzionalità possono o non possono essere usate con le diverse sottoscrizioni per Azure RMS?
Le funzionalità RMS supportate presentano alcune differenze per le diverse sottoscrizioni a pagamento che supportano Azure RMS (Office 365, Azure RMS Premium ed Enterprise Mobility Suite). Per un elenco, vedere [Confronto tra le offerte di Rights Management Services (RMS)](http://technet.microsoft.com/dn858608)

La sottoscrizione gratuita che supporta Azure RMS (RMS per utenti singoli) supporta l'utilizzo di contenuti protetti da Azure RMS. Per ulteriori informazioni, vedere [RMS per utenti singoli e Azure Rights Management](../understand-explore/rms-for-individuals.md).

## Dov'è possibile trovare informazioni tecniche sulla sottoscrizione Azure RMS gratuita (RMS per utenti singoli), ad esempio il suo funzionamento, come assumere il controllo degli account e quali sono i domini che non è possibile usare?
Le risposte a queste domande sono disponibili nell'articolo [RMS per utenti singoli e Azure Rights Management](../understand-explore/rms-for-individuals.md) e in articoli correlati.

## Come possiamo riottenere l'accesso ai file che sono stati protetti da un dipendente che ora ha lasciato l'organizzazione?
Utilizzare la funzionalità per utenti con privilegi avanzati di Azure RMS, che consente agli utenti autorizzati di disporre di diritti completi di proprietario per tutte le licenze d'uso che sono state concesse dal tenant RMS dell'organizzazione. Questa stessa funzionalità consente ai servizi autorizzati di indicizzare e analizzare i file, in base alle esigenze.

Per ulteriori informazioni, vedere [Configurazione degli utenti con privilegi avanzati per Rights Management di Azure e servizi di individuazione o ripristino dei dati](../deploy-use/configure-super-users.md).

## Rights Management può impedire l'acquisizione di schermate?
Non concedendo **Copia** [come diritto di uso](../deploy-use/configure-usage-rights.md), Rights Management può impedire l'acquisizione di schermate dagli strumenti più usati per l'acquisizione di schermate nelle piattaforme Windows (Windows 7, Windows 8.1, Windows 10, Windows Phone) e Android. I dispositivi iOS e Mac, tuttavia, non consentono ad alcuna app di impedire l'acquisizione di schermate e i browser, ad esempio se usati con Outlook Web App e Office Online, non possono impedire l'acquisizione di schermate.

Impedire l'acquisizione di schermate può consentire di evitare la diffusione accidentale o non appropriata di informazioni riservate o sensibili. Tuttavia, vi sono molti modi in cui un utente può condividere i dati visualizzati sullo schermo e acquisire una schermata è solo uno di questi metodi. Ad esempio, un utente che desidera condividere informazioni visualizzate può scattare una foto dei dati con la fotocamera del telefono, ridigitarli o semplicemente comunicarli verbalmente a qualcuno.

Come illustrato da questi esempi, anche se tutte le piattaforme e tutto il software supportassero le API di Rights Management per il blocco dell'acquisizione di schermate, la sola tecnologia non sarebbe in grado di impedire sempre agli utenti di condividere dati che dovrebbero essere riservati. Rights Management può contribuire a salvaguardare i dati importanti tramite i criteri di autorizzazione e per l'uso, ma questa soluzione aziendale per la gestione delle autorizzazioni deve essere usata insieme ad altri controlli. Ad esempio, implementare la sicurezza fisica, selezionare e monitorare attentamente le persone che hanno accesso in modo autorizzato ai dati dell'organizzazione e investire nella formazione degli utenti per aiutarli a capire quali dati non devono essere condivisi.

## Qual è la differenza tra un utente che protegge un messaggio di posta elettronica con l'opzione Non inoltrare e un modello che non include il diritto di inoltro?

Nonostante il nome e l'aspetto, l'opzione **Non inoltrare** non è il contrario dell'inoltro immediato né un modello. Si tratta in realtà di un insieme di diritti che limitano la copia, la stampa, il salvataggio di allegati e l'inoltro dei messaggi di posta elettronica. I diritti vengono applicati dinamicamente agli utenti tramite i destinatari scelti anziché in modo statico in base alle assegnazioni dall'amministratore. Per altre informazioni, vedere la sezione [Do Not Forward option for emails](../deploy-use/configure-usage-rights.md#do-not-forward-option-for-emails) (Opzione Non inoltrare per i messaggi di posta elettronica) dell'articolo [Configuring usage rights for Azure Rights Management](../deploy-use/configure-usage-rights.md) (Configurazione dei diritti di utilizzo per Azure Rights Management).

## Dov'è possibile reperire le informazioni di supporto per Azure RMS, ad esempio le note legali, le informazioni sulla conformità e i contratti di servizio?
Azure RMS supporta altri servizi e si basa inoltre su altri servizi. Per informazioni correlate ad Azure RMS, ma non riferite alla modalità di utilizzo del servizio Azure RMS, esaminare le risorse seguenti:

**Note legali e privacy:**

-   Per informazioni sul contratto di Microsoft Azure: [Contratto di Microsoft Azure](http://azure.microsoft.com/support/legal/subscription-agreement/)

-   Per informazioni sulla privacy di Microsoft Azure: [Informativa sulla privacy di Microsoft Azure](http://azure.microsoft.com/support/legal/privacy-statement/)

**Sicurezza, conformità e controllo:**

Vedere la sezione [Requisiti di sicurezza, conformità e normativi](../understand-explore/azure-rms-problems-it-solves.md#security-compliance-and-regulatory-requirements) dell'articolo [Problemi risolti da Azure RMS](../understand-explore/azure-rms-problems-it-solves.md). Inoltre:

-   Per le certificazioni esterne per Azure RMS: [Centro protezione di Microsoft Azure](http://azure.microsoft.com/support/trust-center/)

-   Per informazioni su FIPS 140: [Convalida di FIPS 140](https://technet.microsoft.com/library/security/cc750357.aspx)

**Contratti di servizio:**

-   Contratto di servizio per Azure RMS, per un'area selezionata: [scaricare dalla pagina di ricerca di licenza del prodotto](http://microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&amp;DocumentTypeId=37)

    - Ad esempio, fare clic su **OnlineSvcsConsolidatedSLA(WW)(Inglese)(marzo 2016)** per scaricare il contratto di servizio marzo 2016 per il Nord America.

-   Contratto di servizio per Azure Active Directory: [Contratti di servizio](http://azure.microsoft.com/support/legal/sla/)

**Documentazione:**

-   Sito della documentazione di Azure Active Directory: [Azure Active Directory](http://azure.microsoft.com/documentation/services/active-directory/)

-   Libreria di Azure Active Directory: [Azure Active Directory](https://msdn.microsoft.com/library/azure/mt168838.aspx)

-   Libreria di Office 365: [Office 365](http://technet.microsoft.com/library/dn127064%28v=office.14%29.aspx)

## Quali sono le ultime novità sulla nuova funzionalità di classificazione e aggiunta di etichette?

Questa funzionalità, presente in Azure Information Protection, è ora disponibile in anteprima pubblica. Per provarla e per un elenco di risorse disponibili, vedere [What is Azure Information Protection (preview)?](../information-protection/what-is-information-protection.md) (Che cos'è Azure Information Protection (anteprima)?)


## Secondo alcune voci, sarà presto disponibile una nuova versione di Azure RMS. Quando verrà rilasciata?

La documentazione tecnica non contiene informazioni sulle versioni future. Per questo tipo di informazioni e per gli annunci di nuove versioni visitare l'[Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services) (Blog sulla mobilità e la sicurezza aziendale) e ottenere gli aggiornamenti più recenti da [Dan Plastina @TheRMSGuy](https://twitter.com/TheRMSGuy) su Twitter. Se si è interessati a una versione di Office, assicurarsi di vedere anche il [blog di Office](https://blogs.office.com/).

## Cosa fare se la domanda non è presente?
usare i link e le risorse elencate in [Informazioni e supporto per Azure Rights Management](information-support.md).

Inoltre, esistono Domande frequenti progettate per gli utenti finali:

-   [Domande frequenti sull'applicazione di condivisione Rights Management per Windows](https://technet.microsoft.com/dn467883)

-   [Domande frequenti sull'applicazione di condivisione Rights Management per piattaforme mobili e Mac](https://technet.microsoft.com/dn451248)

-   [Domande frequenti relative al rilevamento dei documenti](http://go.microsoft.com/fwlink/?LinkId=523977)

La pagina delle domande frequenti verrà aggiornata periodicamente e le nuove aggiunte saranno pubblicate negli annunci mensili di aggiornamento della documentazione sull'[Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services) (Blog sulla mobilità e la sicurezza aziendale).





<!--HONumber=Aug16_HO5-->


