---
title: Domande frequenti sul servizio di protezione dei dati, Azure Rights Management di Azure Information Protection | Azure Information Protection
description: Domande frequenti sul servizio di protezione dei dati, Azure Rights Management (Azure RMS) di Azure Information Protection.
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 90df11c5-355c-4ae6-a762-351b05d0fbed
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ad2d3d7962ab8f8422f4682e4ecd24a7cff3b239
ms.openlocfilehash: 1840954addbf7b3ad603c05b0c55f8bf99ccacfb


---

# Domande frequenti sulla protezione dei dati in Azure Information Protection

>*Si applica a: Azure Information Protection, Office 365*

Di seguito sono riportate alcune possibili domande sul servizio di protezione dei dati, Azure Rights Management, di Azure Information Protection e le relative risposte. 

## Per essere protetti da Azure Rights Management, i file devono trovarsi sul cloud?
No, questo è un malinteso comune. Il servizio Azure Rights Management e Microsoft non visualizzano né archiviano i dati dell'utente come parte del processo di protezione delle informazioni. Le informazioni protette non vengono mai inviate o archiviate in Azure, a meno di archiviarle in modo esplicito in Azure o di usare un altro servizio cloud che le archivia in Azure. 

Per altre informazioni, vedere [Funzionamento di Azure RMS: dietro le quinte](../understand-explore/how-does-it-work.md) per comprendere come la formula segreta per una bevanda gassata creata e archiviata in locale viene protetta dal servizio Azure Rights Management pur rimanendo in locale.

## È possibile integrare il servizio Azure Rights Management con i server locali?
Sì. Azure Rights Management può essere integrato con i server locali, ad esempio Exchange Server, SharePoint e file server Windows. A tale scopo, si usa il [Connettore Rights Management](../deploy-use/deploy-rms-connector.md). In alternativa, se si è solo interessati all'uso dell'infrastruttura di classificazione file con Windows Server, vedere [Protezione RMS con l'infrastruttura di classificazione file (FCI, File Classification Infrastructure) per Windows Server](https://technet.microsoft.com/library/mt601315%28v=ws.10%29.aspx). È inoltre possibile sincronizzare ed eseguire la federazione dei controller di dominio di Active Directory con Azure AD per un'esperienza di autenticazione più semplice per gli utenti, ad esempio utilizzando [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/).

Azure Rights Management genera e gestisce automaticamente i certificati XrML come richiesto, quindi non usa un'infrastruttura PKI locale. Per altre informazioni sull'uso dei certificati in Azure Rights Management, vedere la sezione [Procedura dettagliata del funzionamento di Azure RMS: primo uso, protezione dei contenuti, utilizzo del contenuto](../understand-explore/how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) nell'articolo [Funzionamento di Azure RMS](../understand-explore/how-does-it-work.md).

## Dove è possibile trovare informazioni su soluzioni di terze parti si integrano con Azure RMS?

Molti fornitori di software offrono o implementano già soluzioni in grado di integrarsi con Azure Rights Management e l'elenco di tali soluzioni cresce molto rapidamente. Potrebbe risultare utile visitare il [blog di Enterprise Mobility + Security](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services) e ottenere gli aggiornamenti più recenti da [Dan Plastina @TheRMSGuy](https://twitter.com/TheRMSGuy) su Twitter. In caso di domande specifiche, tuttavia, inviare un messaggio di posta elettronica al team di Information Protection: askipteam@microsoft.com.

## Esiste un Management Pack o un meccanismo di controllo simile per il connettore RMS?

Il connettore Rights Management registra informazioni, avvisi e messaggi di errore nel registro eventi, ma non esiste un Management Pack che includa il monitoraggio di questi eventi. Tuttavia, l'elenco di eventi e le relative descrizioni con altre informazioni che consentono di adottare misure correttive è documentato [Monitorare il connettore di Azure Rights Management](../deploy-use/monitor-rms-connector.md).

## È necessario essere un amministratore globale per configurare Azure RMS oppure tale configurazione può essere delegata ad altri amministratori?

Gli amministratori globali per un tenant di Office 365 o di Azure AD possono ovviamente eseguire tutte le attività amministrative per il servizio Azure Rights Management. Se tuttavia si vogliono assegnare autorizzazioni amministrative ad altri utenti, è possibile farlo usando il cmdlet [Add-AadrmRoleBasedAdministrator](https://msdn.microsoft.com/library/dn629417.aspx) di Azure RMS PowerShell. È possibile assegnare questo ruolo amministrativo per account utente o per gruppo. Sono disponibili due ruoli: **amministratore globale** e **amministratore del connettore**. 

Come è possibile capire dal nome, il primo ruolo concede le autorizzazioni necessarie per eseguire tutte le attività amministrative per Azure Rights Management, senza rendere gli utenti interessati amministratori globali di altri servizi cloud, mentre il secondo ruolo concede le autorizzazioni necessarie per eseguire solo il connettore Rights Management (RMS).

Alcune osservazioni:

- Solo gli amministratori globali per Office 365 e gli amministratori globali per Azure AD possono configurare Azure RMS tramite i portali di gestione (l'interfaccia di amministrazione di Office 365 o il portale di Azure classico). Gli utenti a cui viene assegnato il ruolo di amministratore globale per Azure RMS devono configurare Azure RMS tramite i comandi di Azure RMS PowerShell. Per trovare con più facilità i cmdlet giusti per attività specifiche, vedere [Amministrazione di Azure Rights Management mediante Windows PowerShell](../deploy-use/administer-powershell.md).

- Se i [controlli di caricamento](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) sono stati configurati, ciò non influisce sulla possibilità di amministrare Azure RMS, fatta eccezione per il connettore RMS. Ad esempio, se i controlli di selezione sono stati configurati in modo da limitare la protezione del contenuto al gruppo "Reparto IT", l'account usato per installare e configurare il connettore RMS deve essere membro di tale gruppo. 

- Nessun amministratore per Azure RMS (l'amministratore globale del tenant o un amministratore globale di Azure RMS) può rimuovere automaticamente la protezione da documenti o messaggi di posta elettronica protetti da Azure RMS. Possono farlo solo gli utenti a cui è assegnato il ruolo di utente con privilegi avanzati, e solo quando la funzionalità utente con privilegi avanzati è abilitata. Tuttavia, l'amministratore globale del tenant e tutti gli amministratori globali di Azure RMS possono assegnare il ruolo di utente con privilegi avanzati a qualsiasi utente, compreso il proprio account. Possono anche abilitare la funzionalità utente con privilegi avanzati. Queste azioni vengono registrate nel registro amministratore di Azure RMS. Per altre informazioni, vedere la sezione sulle procedure consigliate in [Configurazione degli utenti con privilegi avanzati per Azure Rights Management e servizi di individuazione o ripristino dei dati](../deploy-use/configure-super-users.md). 


## Dispongo di una distribuzione ibrida di Exchange con alcuni utenti su Exchange Online e altri su Exchange Server; questo è supportato da Azure RMS?
Assolutamente e l'aspetto interessante è che gli utenti saranno in grado di proteggere e utilizzare senza problemi messaggi di posta elettronica e allegati protetti con le due distribuzioni di Exchange. Per questa configurazione, [attivare Azure RMS](../deploy-use/activate-service.md) e [abilitare IRM per Exchange Online](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx), quindi [distribuire e configurare il connettore RMS](../deploy-use/deploy-rms-connector.md) per Exchange Server.

## Se si usa questa protezione nell'ambiente di produzione, l'azienda è costretta a usare sempre questa soluzione o esiste il rischio di perdere l'accesso ai contenuti protetti con Azure RMS?
No, si ha sempre il controllo dei dati e si può continuare ad accedervi, anche se si decide di non usare più il servizio Azure Rights Management. Per altre informazioni, vedere [Rimozione delle autorizzazioni e disattivazione di Azure Rights Management](../deploy-use/decommission-deactivate.md).

Tuttavia, prima di disabilitare la distribuzione di Azure RMS, desideriamo sapere e comprendere il motivo per cui è stata presa questa decisione. Se la tecnologia di protezione Azure Rights Management non soddisfa i requisiti aziendali, contattarci per sapere se sono previste nuove funzionalità per l'immediato futuro o se esistono alternative. Inviare un messaggio di posta elettronica a [AskIPTeam@Microsoft.com](mailto:askipteam@microsoft.com?subject=Planning%20to%20decommission%20Azure%20RMS) e saremo lieti di discutere i requisiti tecnici e aziendali.

## È possibile determinare quali utenti possono usare Azure RMS per proteggere i contenuti?
Sì, il servizio Azure Rights Management include controlli di selezione utenti per questo scenario. Per altre informazioni, vedere la sezione [Configurazione dei controlli di selezione utenti per una distribuzione graduale](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) dell'articolo [Attivazione di Azure Rights Management](../deploy-use/activate-service.md).

## È possibile impedire agli utenti di condividere documenti protetti con aziende specifiche?
Uno dei vantaggi principali offerti dal servizio Azure Rights Management per la protezione dei dati è il supporto della collaborazione business-to-business senza che sia necessario configurare trust espliciti per ogni organizzazione partner, in quanto l'autenticazione viene eseguita automaticamente da Azure AD.

Non sono disponibili opzioni di amministrazione che consentano di impedire agli utenti di condividere documenti in modo sicuro con aziende specifiche. Si supponga, ad esempio, di voler bloccare un'azienda che non si considera attendibile o una società concorrente. Impedire al servizio Azure Rights Management di inviare documenti protetti agli utenti di queste società non ha alcuna utilità, in quanto gli utenti condividerebbero i documenti in modalità non protetta, con maggiori rischi per l'azienda stessa. Inoltre, non sarebbe possibile identificare gli utenti che condividono i documenti aziendali riservati e i rispettivi destinatari in queste aziende, mentre questo è possibile quando i documenti o i messaggi di posta elettronica sono protetti tramite il servizio Azure Rights Management.

## Quando condivido un documento protetto con qualcuno all'esterno della mia azienda, come viene autenticato questo utente?
Il servizio Azure Rights Management usa sempre un account di Azure Active Directory e un indirizzo di posta elettronica associato per l'autenticazione utente, semplificando la collaborazione business-to-business per gli amministratori. Se l'altra organizzazione utilizza i servizi di Azure, gli utenti avranno già account in Azure Active Directory, anche se questi account vengono creati e gestiti in locale e poi sincronizzati in Azure. Se l'organizzazione dispone di Office 365, dietro le quinte, questo servizio utilizza anche Azure Active Directory per gli account utente. Se nell'organizzazione dell'utente non esistono account gestiti in Azure, gli utenti possono iscriversi a [RMS per utenti singoli](../understand-explore/rms-for-individuals.md), che consente di creare un tenant e una directory di Azure non gestiti per l'organizzazione con un account per l'utente, in modo che questo utente e gli utenti successivi possano quindi essere autenticati per il servizio Azure Rights Management.

Il metodo di autenticazione per questi account può variare a seconda di come l'amministratore dell’altra organizzazione ha configurato gli account di Azure Active Directory. Ad esempio, è possibile utilizzare password create per questi account, Multi-Factor Authentication (MFA), la federazione o password create in servizi di dominio di Active Directory e quindi sincronizzate con Azure Active Directory.

## È possibile aggiungere utenti all'esterno della mia azienda per i modelli personalizzati?
Sì. La creazione di modelli personalizzati che gli utenti finali (e gli amministratori) possono scegliere dalle applicazioni rende rapida e semplice l’applicazione della protezione delle informazioni, attraverso i criteri specificati. Una delle impostazioni nel modello riguarda chi è in grado di accedere al contenuto ed è possibile specificare utenti e gruppi all'interno dell'organizzazione e utenti al suo esterno.

Per specificare gli utenti esterni all'organizzazione, aggiungerli come contatti a un gruppo da selezionare nel portale di Azure classico quando si configurano i modelli. In alternativa, usare il [modulo Windows PowerShell per Microsoft Azure Rights Management](../deploy-use/install-powershell.md):

-   **Usare un oggetto di definizione dei diritti per creare o aggiornare un modello**:    specificare gli indirizzi di posta elettronica esterni e i relativi diritti in un oggetto di definizione dei diritti, che verrà quindi usato per creare o aggiornare un modello. È possibile specificare l'oggetto di definizione dei diritti usando il cmdlet [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) per creare una variabile e quindi fornire questa variabile al parametro -RightsDefinition con il cmdlet [Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx) (per un nuovo modello) o [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx) (per modificare un modello esistente). Tuttavia, se si stanno aggiungendo questi utenti a un modello esistente, sarà necessario definire gli oggetti di definizione dei diritti per i gruppi esistenti nei modelli e non solo gli utenti esterni.

Per altre informazioni sui modelli personalizzati, vedere l'articolo relativo alla [configurazione di modelli personalizzati per Azure Rights Management](../deploy-use/configure-custom-templates.md).

## Azure RMS funziona con i gruppi dinamici in Azure AD?
Una funzionalità di Azure AD Premium consente di configurare l'appartenenza dinamica per gruppi specificando [regole basate su attributi](https://azure.microsoft.com/documentation/articles/active-directory-accessmanagement-groups-with-advanced-rules/). Quando si crea un gruppo di sicurezza in Azure AD, questo tipo di gruppo supporta l'appartenenza dinamica, ma non supporta un indirizzo di posta elettronica e pertanto non può essere usato con il servizio Azure Rights Management. Tuttavia, ora è possibile creare un nuovo tipo di gruppo in Azure AD che supporta sia l'appartenenza dinamica ed è abilitato alla posta elettronica. Quando si aggiunge un nuovo gruppo nel portale classico di Azure, è possibile scegliere di **TIPO DI GRUPPO** dell'**"Anteprima" Office 365**. Poiché questo gruppo è abilitato alla posta elettronica, è possibile usarlo con la protezione Azure Rights Management.

Come il nome opzionale mostra chiaramente, il nuovo tipo di gruppo è ancora in anteprima, con la funzionalità aggiuntiva prevista e la nuova documentazione da seguire. Nel frattempo, è confermata la possibilità di usare questo nuovo tipo di gruppo con la protezione Azure Rights Management.


## Quali dispositivi e quali tipi di file sono supportati da Azure RMS?
Per un elenco di dispositivi che supportano il servizio Azure Rights Management, vedere [Requisiti per Azure RMS: dispositivi client che supportano Azure RMS](../get-started/requirements-client-devices.md). Dal momento che non tutti i dispositivi supportati consentono l'uso di tutte le funzionalità di Rights Managament, vedere anche la tabella in [Requisiti per Azure RMS: applicazioni](../get-started/requirements-applications.md).

Il servizio Azure Rights Management può supportare tutti i tipi di file. Per file di testo e di immagine, file di Microsoft Office (Word, Excel e PowerPoint), file con estensione pdf e altri tipi di file di applicazione, Azure Rights Management fornisce la protezione nativa, incluse crittografia e applicazione di diritti (autorizzazioni). Per tutte le altre applicazioni e tipi di file, la protezione generica fornisce funzionalità di incapsulamento e autenticazione dei file che consentono di verificare se un utente è autorizzato ad aprire il file.

Per un elenco delle estensioni di file supportate in modo nativo da Azure Rights Management, vedere la sezione [Tipi ed estensioni di file supportati](../rms-client/sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions) della [Guida dell'amministratore dell'applicazione Rights Management sharing](../rms-client/sharing-app-admin-guide.md). Le estensioni di file non incluse nell'elenco sono supportate mediante l'uso dell'applicazione RMS sharing, che applica automaticamente la protezione generica a tali file.

## Quando si apre un documento di Office protetto da RMS, anche il file temporaneo associato è protetto da RMS?

No. In questo scenario, il file temporaneo associato non contiene i dati del documento originale, ma solo i dati immessi dall'utente mentre il file è aperto. A differenza del file originale, il file temporaneo non è destinato alla condivisione e rimarrà disponibile nel dispositivo, protetto dai controlli di protezione locali, ad esempio BitLocker ed EFS.

## Si vuole usare la modalità BYOK con Azure Information Protection, ma si è appreso che questa non è compatibile con Exchange Online. Quale soluzione è preferibile adottare?
Non lasciare che questa limitazione attuale ritardi la distribuzione del servizio Azure Rights Management di Azure Information Protection. Se si dispone di Exchange Online e si vuole usare la modalità BYOK, è consigliabile distribuire Azure Information Protection nella modalità predefinita per la gestione delle chiavi, in base alla quale Microsoft genera e gestisce la chiave. In questo modo, si ottengono ora tutti i vantaggi della protezione di file e messaggi di posta elettronica importanti, con l'opzione per passare a BYOK in un secondo momento (ad esempio, quando Exchange Online supporterà BYOK). Quando si passa alla modalità BYOK, i documenti precedentemente protetti e i messaggi di posta elettronica rimangono comunque accessibili tramite una chiave archiviata.

Tuttavia, se i criteri aziendali richiedono di usare un modulo di protezione hardware (HSM) e ciò altrimenti bloccherebbe la distribuzione di Azure Information Protection, un'altra soluzione consiste nel distribuire subito Azure Information Protection con la modalità BYOK, con funzionalità di protezione di Rights Management ridotte per Exchange. Per altre informazioni, vedere [Prezzi e restrizioni BYOK](../plan-design/byok-price-restrictions.md) da [pianificazione e implementazione della chiave del tenant Azure Rights Management](../plan-design/plan-implement-tenant-key.md).

## Una funzionalità che cerco non sembra funzionare con le librerie protette di SharePoint, è previsto il supporto per la mia funzionalità?
Attualmente, SharePoint supporta documenti protetti da Rights Management usando le librerie protette IRM, che non supportano i modelli personalizzati, il rilevamento dei documenti e alcune altre funzionalità. Per ulteriori informazioni, vedere la sezione [SharePoint Online e SharePoint Server](../understand-explore/office-apps-services-support.md#sharepoint-online-and-sharepoint-server) nell'articolo [Servizi e applicazioni di Office](../understand-explore/office-apps-services-support.md).

Se si è interessati a una funzionalità specifica non ancora supportata, assicurarsi di controllare gli annunci nel [blog di Enterprise Mobility + Security](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services).

## Come è possibile configurare One Drive for Business in SharePoint Online, in modo che gli utenti possano condividere i propri file in modo sicuro con le persone all'interno e all'esterno della società?
Per impostazione predefinita, in qualità di amministratore di Office 365, non si configura questo oggetto. L'operazione viene eseguita dagli utenti.

Proprio come gli amministratori del sito di SharePoint abilitano e configurano IRM per una raccolta di SharePoint che possiedono, OneDrive for Business è progettato per consentire agli utenti di attivare e configurare IRM per la propria raccolta OneDrive for Business.  Tuttavia, usando PowerShell, è possibile eseguire questa operazione per gli utenti. Per istruzioni, vedere la sezione [SharePoint Online e OneDrive for Business: configurazione di IRM](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration) dell'articolo [Office 365: configurazione di client e servizi online](../deploy-use/configure-office365.md).

## Sono disponibili suggerimenti per una corretta distribuzione?
Dopo aver supervisionato un elevato numero di distribuzioni e ascoltato il parere di clienti, partner, consulenti e tecnici del servizio di supporto, uno dei principali suggerimenti che possiamo fornire è **Progettare e distribuire criteri semplici per i diritti d'uso**.

Poiché Azure Information Protection supporta la condivisione sicura con qualsiasi utente, si possono raggiungere livelli di protezione dei dati molto elevati, ma bisogna impostare criteri rigorosi per i diritti d'uso. Per la maggior parte delle organizzazioni, l'impatto maggiore risulta dall'esigenza di impedire la perdita dei dati applicando il modello predefinito dei criteri per i diritti d'uso che limita l'accesso agli utenti dell'organizzazione. Si possono anche applicare criteri più specifici, ad esempio impedire agli utenti di stampare o modificare documenti, ma è preferibile impostarli solo per documenti che richiedono un alto livello di sicurezza. Evitare di applicare tutti questi criteri più restrittivi in un'unica soluzione pianificandone invece un approccio per fasi.

## Come possiamo riottenere l'accesso ai file che sono stati protetti da un dipendente che ora ha lasciato l'organizzazione?
Utilizzare la funzionalità per utenti con privilegi avanzati di Azure RMS, che consente agli utenti autorizzati di disporre di diritti completi di proprietario per tutte le licenze d'uso che sono state concesse dal tenant RMS dell'organizzazione. Questa stessa funzionalità consente ai servizi autorizzati di indicizzare e analizzare i file, in base alle esigenze.

Per ulteriori informazioni, vedere [Configurazione degli utenti con privilegi avanzati per Rights Management di Azure e servizi di individuazione o ripristino dei dati](../deploy-use/configure-super-users.md).

## Rights Management può impedire l'acquisizione di schermate?
Non concedendo **Copia** [come diritto di uso](../deploy-use/configure-usage-rights.md), Rights Management può impedire l'acquisizione di schermate dagli strumenti più usati per l'acquisizione di schermate nelle piattaforme Windows (Windows 7, Windows 8.1, Windows 10, Windows Phone) e Android. I dispositivi iOS e Mac, tuttavia, non consentono ad alcuna app di impedire l'acquisizione di schermate e i browser, ad esempio se usati con Outlook Web App e Office Online, non possono impedire l'acquisizione di schermate.

Impedire l'acquisizione di schermate può consentire di evitare la diffusione accidentale o non appropriata di informazioni riservate o sensibili. Tuttavia, vi sono molti modi in cui un utente può condividere i dati visualizzati sullo schermo e acquisire una schermata è solo uno di questi metodi. Ad esempio, un utente che desidera condividere informazioni visualizzate può scattare una foto dei dati con la fotocamera del telefono, ridigitarli o semplicemente comunicarli verbalmente a qualcuno.

Come illustrato da questi esempi, anche se tutte le piattaforme e tutto il software supportassero le API di Rights Management per il blocco dell'acquisizione di schermate, la sola tecnologia non sarebbe in grado di impedire sempre agli utenti di condividere dati che dovrebbero essere riservati. Rights Management può contribuire a salvaguardare i dati importanti tramite i criteri di autorizzazione e per l'uso, ma questa soluzione aziendale per la gestione delle autorizzazioni deve essere usata insieme ad altri controlli. Ad esempio, implementare la sicurezza fisica, selezionare e monitorare attentamente le persone che hanno accesso in modo autorizzato ai dati dell'organizzazione e investire nella formazione degli utenti per aiutarli a capire quali dati non devono essere condivisi.

## Qual è la differenza tra un utente che protegge un messaggio di posta elettronica con l'opzione Non inoltrare e un modello che non include il diritto di inoltro?

Nonostante il nome e l'aspetto, l'opzione **Non inoltrare** non è il contrario dell'inoltro immediato né un modello. Si tratta in realtà di un insieme di diritti che limitano la copia, la stampa, il salvataggio di allegati e l'inoltro dei messaggi di posta elettronica. I diritti vengono applicati dinamicamente agli utenti tramite i destinatari scelti anziché in modo statico in base alle assegnazioni dall'amministratore. Per altre informazioni, vedere la sezione [Do Not Forward option for emails](../deploy-use/configure-usage-rights.md#do-not-forward-option-for-emails) (Opzione Non inoltrare per i messaggi di posta elettronica) dell'articolo [Configuring usage rights for Azure Rights Management](../deploy-use/configure-usage-rights.md) (Configurazione dei diritti di utilizzo per Azure Rights Management).






<!--HONumber=Sep16_HO4-->


