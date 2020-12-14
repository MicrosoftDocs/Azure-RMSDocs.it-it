---
title: Domande frequenti per Azure RMS - Azure Information Protection
description: Alcune domande frequenti relative al servizio di protezione dati, Azure Rights Management (Azure RMS), da Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 12/02/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 90df11c5-355c-4ae6-a762-351b05d0fbed
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 3d376446354e591f9a5742d415b7b7cba75bf887
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97382259"
---
# <a name="frequently-asked-questions-about-data-protection-in-azure-information-protection"></a>Domande frequenti sulla protezione dati in Azure Information Protection

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Pertinente per**: [AIP Unified Labeling client e client classico](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients). Per ulteriori informazioni, vedere anche le [domande frequenti solo per il client classico](faqs-classic.md). *

>[!NOTE] 
> Per offrire un'esperienza utente unificata e semplificata, **Azure Information Protection** la gestione classica di client e **etichette** nel portale di Azure verrà **deprecata** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

In caso di domande relative al servizio di protezione dati, Azure Rights Management, da Azure Information Protection, vedere se la risposta è disponibile qui.

## <a name="do-files-have-to-be-in-the-cloud-to-be-protected-by-azure-rights-management"></a>I file devono trovarsi nel cloud per essere protetti da Azure Rights Management?

No, questo è un malinteso comune. Il servizio Azure Rights Management e Microsoft non vedono e non archiviano i dati come parte del processo di protezione delle informazioni. Le informazioni protette non vengono mai inviate o archiviate in Azure, a meno che non si archivino in Azure in modo esplicito o si usi un altro servizio cloud che le archivia in Azure.

Per ulteriori informazioni, vedere [come funziona Azure RMS? Dietro le quinte](./how-does-it-work.md) per comprendere in che modo una formula segreta di Cola creata e archiviata in locale è protetta dal servizio Rights Management di Azure, ma rimane in locale.

## <a name="whats-the-difference-between-azure-rights-management-encryption-and-encryption-in-other-microsoft-cloud-services"></a>Qual è la differenza tra la crittografia Rights Management Azure e la crittografia in altri servizi cloud Microsoft?

Microsoft offre varie tecnologie di crittografia che consentono di proteggere i dati per scenari differenti e spesso complementari. Ad esempio, mentre Microsoft 365 offre la crittografia dei dati inattivi per i dati archiviati in Microsoft 365, il servizio Azure Rights Management di Azure Information Protection crittografa i dati in modo indipendente, in modo che siano protetti indipendentemente dalla posizione in cui si trovano o dal modo in cui vengono trasmessi.

Queste tecnologie di crittografia sono complementari e per usarle è necessario abilitarle e configurarle in modo indipendente. Quando si esegue questa operazione, si potrebbe avere la possibilità di trasferire la propria chiave per la crittografia, uno scenario noto anche come "BYOK" (bring your own key). L'abilitazione della modalità BYOK per una di queste tecnologie non avrà effetti sulle altre. Ad esempio, è possibile usare la modalità BYOK di Azure Information Protection e non usare la modalità BYOK per altre tecnologie di crittografia e viceversa. Le chiavi utilizzate da queste tecnologie diverse potrebbero essere uguali o diverse, a seconda della modalità di configurazione delle opzioni di crittografia per ogni servizio.

## <a name="can-i-now-use-byok-with-exchange-online"></a>Adesso è possibile usare BYOK con Exchange Online?

Sì, è ora possibile usare BYOK con Exchange Online quando si seguono le istruzioni riportate in [configurare nuove funzionalità di crittografia dei messaggi Microsoft 365 basate su Azure Information Protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e). Queste istruzioni abilitano le nuove funzionalità di Exchange Online che supportano l'uso della modalità BYOK per Azure Information Protection, nonché la nuova crittografia Office 365.

Per altre informazioni su questa modifica, vedere l'annuncio sul blog [Office 365 Message Encryption with the new capabilities](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801) (La crittografia Office 365 con le nuove funzionalità)

## <a name="where-can-i-find-information-about-third-party-solutions-that-integrate-with-azure-rms"></a>Dove è possibile trovare informazioni sulle soluzioni di terze parti integrabili con Azure RMS?

Molti fornitori di software hanno già o stanno implementando soluzioni che si integrano con Azure Rights Management e l'elenco è in rapida crescita. Potrebbe risultare utile controllare gli elenchi di [applicazioni abilitate per RMS](requirements-applications.md#) e ottenere gli aggiornamenti più recenti da [Microsoft Mobility@MSFTMobility ](https://twitter.com/MSFTMobility) su Twitter. Controllare inoltre la [Guida per gli sviluppatori](./develop/developers-guide.md) e pubblicare eventuali domande specifiche sull'integrazione sul [sito Yammer](https://www.yammer.com/AskIPTeam) di Azure Information Protection.

## <a name="is-there-a-management-pack-or-similar-monitoring-mechanism-for-the-rms-connector"></a>Esiste un Management Pack o un meccanismo di monitoraggio simile per il connettore RMS?

Sebbene il connettore Rights Management registri informazioni, avvisi e messaggi di errore nel registro eventi, non esiste un Management Pack che includa il monitoraggio di questi eventi. Tuttavia, l'elenco degli eventi e le relative descrizioni, con altre informazioni che consentono di adottare misure correttive, è documentato in [Monitorare il connettore di Azure Rights Management](monitor-rms-connector.md).

## <a name="how-do-i-create-a-new-custom-template-in-the-azure-portal"></a>Come si crea un nuovo modello personalizzato nel portale di Azure?

I modelli personalizzati sono stati spostati nel portale di Azure dove è possibile continuare a gestirli come modelli o convertirli in etichette. Per creare un nuovo modello, creare una nuova etichetta e configurare le impostazioni di protezione dati per Azure RMS. Dietro le quinte viene creato un nuovo modello a cui possono accedere servizi e applicazioni che si integrano con i modelli di Rights Management.

Per altre informazioni sui modelli nel portale di Azure, vedere [Configurazione e gestione dei modelli per Azure Information Protection](configure-policy-templates.md).

## <a name="ive-protected-a-document-and-now-want-to-change-the-usage-rights-or-add-usersdo-i-need-to-reprotect-the-document"></a>È stato protetto un documento e si decide di modificare i diritti di utilizzo o aggiungere utenti: è necessario proteggere nuovamente il documento?

Se il documento è stato protetto usando un'etichetta o un modello, non è necessario proteggerlo nuovamente. Modificare l'etichetta o il modello apportando le modifiche ai diritti di utilizzo o aggiungendo nuovi gruppi o utenti, e salvare le modifiche:

- Se un utente non ha avuto accesso al documento prima che venissero apportate le modifiche, le modifiche diventano effettive non appena l'utente apre il documento.

- Se un utente ha già avuto accesso al documento, le modifiche diventano effettive dopo la scadenza della sua [licenza d'uso](configure-usage-rights.md#rights-management-use-license). Proteggere nuovamente il documento solo se non è possibile attendere la scadenza della licenza d'uso. Proteggendo nuovamente il documento ne viene creata una nuova versione e pertanto una nuova licenza d'uso per l'utente.

In alternativa, se è già stato configurato un gruppo con le autorizzazioni necessarie, è possibile modificare l'appartenenza al gruppo per includere o escludere utenti e non è necessario modificare l'etichetta o il modello. Potrebbe verificarsi un piccolo ritardo prima che le modifiche abbiano effetto, poiché l'appartenenza al gruppo viene [memorizzata nella cache](prepare.md#group-membership-caching-by-azure-information-protection) dal servizio Azure Rights Management.

Se il documento è stato protetto usando autorizzazioni personalizzate, è possibile modificare le autorizzazioni per il documento esistente. È necessario proteggere di nuovo il documento e specificare tutti gli utenti e tutti i diritti di utilizzo che sono necessari per questa nuova versione del documento. Per proteggere nuovamente un documento protetto, è necessario possedere il diritto di utilizzo Controllo completo.

Suggerimento: per controllare se un documento è stato protetto con un modello o tramite autorizzazione personalizzata, usare il cmdlet di PowerShell [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus). Per le autorizzazioni personalizzate è sempre presente la descrizione **Accesso limitato** con un ID modello univoco che non viene visualizzato quando si esegue [Get-RMSTemplate](/powershell/module/azureinformationprotection/get-rmstemplate).

## <a name="i-have-a-hybrid-deployment-of-exchange-with-some-users-on-exchange-online-and-others-on-exchange-serveris-this-supported-by-azure-rms"></a>Si ha una distribuzione ibrida di Exchange con alcuni utenti su Exchange Online e altri su Exchange Server: questa configurazione è supportata da Azure RMS?
Assolutamente e l'aspetto interessante è che gli utenti sono in grado di proteggere e usare senza problemi messaggi di posta elettronica e allegati protetti con le due distribuzioni di Exchange. Per questa configurazione [attivare Azure RMS](activate-service.md) e [abilitare IRM per Exchange Online](/microsoft-365/enterprise/activate-rms-in-microsoft-365), quindi [distribuire e configurare il connettore RMS](deploy-rms-connector.md) per Exchange Server.

## <a name="if-i-use-this-protection-for-my-production-environment-is-my-company-then-locked-into-the-solution-or-risk-losing-access-to-content-that-we-protected-with-azure-rms"></a>Se si usa questo tipo di protezione per l'ambiente di produzione, l'azienda è bloccata in questa soluzione o rischia di perdere l'accesso ai contenuti protetti con Azure RMS?
No, si mantiene sempre il controllo dei dati e si può continuare ad accedervi, anche se si decide di non usare più il servizio Azure Rights Management. Per altre informazioni, vedere [rimozione delle autorizzazioni e disattivazione di Azure Rights Management](decommission-deactivate.md).

## <a name="can-i-control-which-of-my-users-can-use-azure-rms-to-protect-content"></a>È possibile controllare quali utenti possono usare Azure RMS per proteggere i contenuti?
Sì, il servizio Azure Rights Management include controlli di onboarding degli utenti per questo scenario. Per ulteriori informazioni, vedere la sezione [configurazione dei controlli di onboarding per una distribuzione](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) in più fasi nell'articolo [attivazione del servizio di protezione da Azure Information Protection](activate-service.md) .

## <a name="can-i-prevent-users-from-sharing-protected-documents-with-specific-organizations"></a>È possibile impedire agli utenti di condividere documenti protetti con organizzazioni specifiche?
Uno dei vantaggi principali dell'uso del servizio Azure Rights Management per la protezione dati è il supporto della collaborazione business-to-business senza che sia necessario configurare trust espliciti per ciascuna organizzazione partner, poiché l'autenticazione viene eseguita automaticamente da Azure AD.

Non sono disponibili opzioni di amministrazione per impedire agli utenti di condividere i documenti in modo sicuro con organizzazioni specifiche. Si desidera, ad esempio, bloccare un'organizzazione che non si considera attendibile o che dispone di un'azienda concorrente. Impedire al servizio Rights Management di Azure di inviare documenti protetti agli utenti di queste organizzazioni non avrebbe senso perché gli utenti condividevano i documenti in modo non protetto, che probabilmente è l'ultima cosa che si vuole eseguire in questo scenario. Ad esempio, non sarà possibile identificare chi condivide documenti aziendali riservati con quali utenti di queste organizzazioni, che è possibile eseguire quando il documento (o messaggio di posta elettronica) è protetto dal servizio Rights Management di Azure.

## <a name="when-i-share-a-protected-document-with-somebody-outside-my-company-how-does-that-user-get-authenticated"></a>Quando si condivide un documento protetto con qualcuno all'esterno dell'azienda, come viene autenticato questo utente?

Per impostazione predefinita, il servizio Azure Rights Management usa un account Azure Active Directory e un indirizzo di posta elettronica associato per l'autenticazione dell'utente, semplificando la collaborazione business-to-business per gli amministratori. Se l'altra organizzazione usa i servizi di Azure, gli utenti hanno già account in Azure Active Directory, anche se questi account vengono creati e gestiti in locale e poi sincronizzati in Azure. Se l'organizzazione ha Microsoft 365, dietro le quinte, questo servizio usa anche Azure Active Directory per gli account utente. Se l'organizzazione dell'utente non dispone di account gestiti in Azure, gli utenti possono iscriversi a [RMS per utenti singoli](./rms-for-individuals.md), creando un tenant e una directory di Azure non gestiti per l'organizzazione con un account per l'utente, in modo che l'utente (e gli utenti successivi) possano quindi essere autenticati per il servizio Rights Management di Azure.

Il metodo di autenticazione per questi account può variare a seconda di come l'amministratore dell'altra organizzazione ha configurato l'account Azure Active Directory. Ad esempio, è possibile utilizzare password create per questi account, la federazione o password create in Active Directory Domain Services e quindi sincronizzate con Azure Active Directory.

Altri metodi di autenticazione:

- Se si protegge un messaggio di posta elettronica che ha come allegato un documento di Office ed è indirizzato a un utente che non dispone di un account in Azure AD, il metodo di autenticazione cambia. Il servizio Azure Rights Management è federato con alcuni provider di identità di social networking diffusi, ad esempio Gmail. Se il provider di posta elettronica dell'utente è supportato, l'utente può accedere al servizio e il suo provider di posta elettronica è responsabile della sua autenticazione. Se il provider di posta elettronica dell'utente non è supportato, o è supportato ma si preferisce quest'altra soluzione, l'utente può richiedere un passcode monouso per la propria autenticazione e visualizzare il messaggio di posta elettronica con il documento protetto in un Web browser.

- Azure Information Protection può usare gli account Microsoft per le applicazioni supportate. Attualmente, non tutte le applicazioni possono aprire contenuti protetti quando viene usato un account Microsoft per l'autenticazione. [Altre informazioni](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)

## <a name="can-i-add-external-users-people-from-outside-my-company-to-custom-templates"></a>È possibile aggiungere utenti esterni, ovvero persone esterne all'azienda, ai modelli personalizzati?

Sì. Le [impostazioni di protezione](configure-policy-protection.md) che è possibile configurare nel portale di Azure consentono di aggiungere autorizzazioni per utenti e gruppi esterni all'organizzazione e anche tutti gli utenti di un'altra organizzazione. Può risultare utile per fare riferimento all'esempio dettagliato [Proteggere la collaborazione ai documenti tramite Azure Information Protection](secure-collaboration-documents.md). 

Si noti che se si dispone di etichette di Azure Information Protection, è necessario convertire il modello personalizzato in un'etichetta prima di poter configurare queste impostazioni di protezione nel portale di Azure. Per altre informazioni, vedere [Configurazione e gestione dei modelli per Azure Information Protection](configure-policy-templates.md).

In alternativa è possibile aggiungere utenti esterni a modelli personalizzati ed etichette tramite PowerShell. In questa configurazione è necessario usare un oggetto di definizione dei diritti che consenta di aggiornare il modello:

1. Specificare gli indirizzi di posta elettronica esterni e i relativi diritti in un oggetto di definizione dei diritti, usando il cmdlet [New-AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition) per creare una variabile.

2. Fornire questa variabile al parametro RightsDefinition con il cmdlet [set-AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty) .

    Quando si aggiungono utenti a un modello esistente, è necessario definire gli oggetti di definizione dei diritti per gli utenti esistenti nei modelli, oltre ai nuovi utenti. Per questo scenario potrebbe risultare utile l'**esempio 3: aggiungere nuovi utenti e diritti a un modello personalizzato** della sezione relativa agli [esempi](/powershell/module/aipservice/set-aipservicetemplateproperty#examples) del cmdlet.

## <a name="what-type-of-groups-can-i-use-with-azure-rms"></a>Quali tipi di gruppo è possibile usare con Azure RMS?
Per la maggior parte degli scenari, è possibile usare qualsiasi tipo di gruppo di Azure AD che abbia un indirizzo di posta elettronica. Questa regola empirica vale sempre quando si assegnano diritti di utilizzo, ma esistono alcune eccezioni per l'amministrazione del servizio Azure Rights Management. Per altre informazioni, vedere [Requisiti di Azure Information Protection per gli account di gruppo](prepare.md#azure-information-protection-requirements-for-group-accounts).

## <a name="how-do-i-send-a-protected-email-to-a-gmail-or-hotmail-account"></a>Come si invia un messaggio di posta elettronica protetto a un account Gmail o Hotmail?

Quando si usa Exchange Online e il servizio Azure Rights Management, si invia semplicemente il messaggio di posta elettronica all'utente come messaggio protetto. Ad esempio, è possibile selezionare il nuovo pulsante **Proteggi** nella barra dei comandi di Outlook sul Web, usare il pulsante o l'opzione di Outlook **Non inoltrare**. In alternativa è possibile selezionare un'etichetta di Azure Information Protection che applica automaticamente l'opzione Non inoltrare e classifica il messaggio di posta elettronica.

Il destinatario visualizza un'opzione per accedere al proprio account Gmail, Yahoo o Microsoft e quindi può leggere il messaggio di posta elettronica protetto. In alternativa si può scegliere l'opzione di un passcode monouso per leggere il messaggio di posta elettronica in un browser.

Per supportare questo scenario, Exchange Online deve essere abilitato per il servizio Azure Rights Management e le nuove funzionalità di crittografia Office 365. Per altre informazioni su questa configurazione, vedere [Exchange Online: configurazione di IRM](configure-office365.md#exchangeonline-irm-configuration).

Per altre informazioni sulle nuove funzionalità che includono il supporto di tutti gli account di posta elettronica in tutti i dispositivi, vedere il seguente post di blog: [Announcing new capabilities available in Office 365 Message Encryption](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801) (Annuncio di nuove funzionalità di crittografia Office 365).

## <a name="what-devices-and-which-file-types-are-supported-by-azure-rms"></a>Quali dispositivi e quali tipi di file sono supportati da Azure RMS?

Per un elenco dei dispositivi che supportano il servizio Azure Rights Management, vedere [Dispositivi client che supportano la protezione dati di Azure Rights Management](./requirements.md#client-devices). Poiché non tutti i dispositivi supportati sono attualmente in grado di supportare tutte le funzionalità di Rights Management, assicurarsi di controllare anche le tabelle per le [applicazioni con RMS](./requirements-applications.md).

Il servizio Azure Rights Management può supportare tutti i tipi di file. Per i file di testo, immagini, Microsoft Office (Word, Excel, PowerPoint), PDF e quelli di altri tipi di applicazione, Azure Rights Management offre la protezione nativa che include crittografia e applicazione dei diritti (autorizzazioni). Per tutte le altre applicazioni e tipi di file, la protezione generica fornisce l'incapsulamento e l'autenticazione del file per verificare se un utente è autorizzato ad aprirlo.

Per un elenco delle estensioni di file supportate in modo nativo da Azure Rights Management, vedere [Tipi di file supportati dal client Azure Information Protection](./rms-client/clientv2-admin-guide-file-types.md). Le estensioni di file non elencate sono supportate tramite il client Azure Information Protection che applica automaticamente la protezione generica a tali file.

## <a name="when-i-open-an-rms-protected-office-document-does-the-associated-temporary-file-become-rms-protected-as-well"></a>Quando si apre un documento Office protetto da RMS, anche il file temporaneo associato diventa protetto con RMS?
No. In questo scenario, il file temporaneo associato non contiene dati del documento originale, ma solo ciò che l'utente immette mentre il file è aperto. A differenza del file originale, il file temporaneo ovviamente non è progettato per la condivisione e rimarrà disponibile nel dispositivo, protetto dai controlli di sicurezza locale, ad esempio BitLocker ed EFS.

## <a name="a-feature-i-am-looking-for-doesnt-seem-to-work-with-sharepoint-protected-librariesis-support-for-my-feature-planned"></a>Una funzionalità che si sta cercando non sembra funzionare con le librerie protette di SharePoint: il supporto per la funzionalità è pianificato?
Attualmente, Microsoft SharePoint supporta i documenti protetti da RMS utilizzando le librerie protette IRM, che non supportano i modelli di Rights Management, il rilevamento dei documenti e altre funzionalità. Per ulteriori informazioni, vedere la sezione [SharePoint in Microsoft 365 e SharePoint Server](./office-apps-services-support.md#sharepoint-in-microsoft-365-and-sharepoint-server) nell'articolo [Servizi e applicazioni di Office](./office-apps-services-support.md) .

Se si è interessati a una funzionalità specifica che non è ancora supportata, tenere d'occhio gli annunci del [blog su Enterprise Mobility e la sicurezza](https://cloudblogs.microsoft.com/enterprisemobility/?product=azure-rights-management-services).

## <a name="how-do-i-configure-one-drive-in-sharepoint-so-that-users-can-safely-share-their-files-with-people-inside-and-outside-the-company"></a>Ricerca per categorie configurare un'unità in SharePoint, in modo che gli utenti possano condividere i propri file in modo sicuro con le persone all'interno e all'esterno della società?
Per impostazione predefinita, come amministratore di Microsoft 365, non è necessario configurarlo; utenti.

Così come un amministratore del sito di SharePoint Abilita e configura IRM per una raccolta di SharePoint di cui è proprietario, OneDrive è progettato per consentire agli utenti di abilitare e configurare IRM per la propria libreria OneDrive. Tuttavia un amministratore può farlo per gli utenti usando PowerShell. Per istruzioni, vedere [SharePoint in Microsoft 365 e OneDrive: configurazione di IRM](configure-office365.md#sharepoint-in-microsoft-365-and-onedrive-irm-configuration).

## <a name="do-you-have-any-tips-or-tricks-for-a-successful-deployment"></a>Ci sono suggerimenti o trucchi per una distribuzione corretta?

Dall'esperienza acquisita supervisionando molte distribuzioni e ascoltando molti clienti, partner, consulenti e tecnici, uno dei principali suggerimenti che ne derivano è quello di **progettare e distribuire criteri semplici**.

Poiché Azure Information Protection supporta la condivisione in modo sicuro con altri utenti, è possibile ambire a livelli di protezione dati molto elevati. Tuttavia, è necessario essere cauti nella configurazione delle restrizioni ai diritti di utilizzo. Per molte organizzazioni l'impatto maggiore sull'attività deriva dal prevenire la perdita di dati limitando l'accesso alle persone nell'organizzazione. Naturalmente, è possibile ottenere una maggiore granularità rispetto a quando è necessario: impedire agli utenti di stampare, modificare e così via. Tuttavia, è consigliabile tenere conto delle restrizioni più granulari come eccezione per i documenti che necessitano di un livello di sicurezza elevato e non implementare questi diritti di utilizzo più restrittivi nel primo giorno, ma pianificare un approccio più graduale.

## <a name="how-do-we-regain-access-to-files-that-were-protected-by-an-employee-who-has-now-left-the-organization"></a>Come si riottiene l'accesso ai file che sono stati protetti da un dipendente che ora ha lasciato l'organizzazione?
Usare la [funzionalità relativa agli utenti con privilegi avanzati](configure-super-users.md), che garantisce i diritti di utilizzo Controllo completo agli utenti autorizzati per tutti i documenti e messaggi di posta elettronica che sono protetti dal tenant. Gli utenti con privilegi avanzati possono leggere sempre questi contenuti protetti e, se necessario, rimuovere la protezione o riapplicarla ai contenuti per altri utenti. Questa stessa funzionalità consente ai servizi autorizzati di indicizzare e analizzare i file, in base alle esigenze.

Se il contenuto è archiviato in SharePoint o OneDrive, gli amministratori possono eseguire il cmdlet [Unlock-SensitivityLabelEncryptedFile](/powershell/module/sharepoint-online/unlock-sposensitivitylabelencryptedfile) per rimuovere l'etichetta di riservatezza e la crittografia. Per altre informazioni, vedere la [documentazione di Microsoft 365](/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files#remove-encryption-for-a-labeled-document).

## <a name="can-rights-management-prevent-screen-captures"></a>Rights Management può impedire l'acquisizione di schermate?
Non concedendo **Copia come** [diritto di utilizzo](configure-usage-rights.md), Rights Management può impedire l'acquisizione di schermate dagli strumenti più usati per l'acquisizione di schermate nelle piattaforme Windows (Windows 7, Windows 8.1, Windows 10, Windows 10 Mobile) e Android. Tuttavia, i dispositivi iOS e Mac non consentono alle app di impedire l'acquisizione di schermate. Inoltre, i browser su qualsiasi dispositivo non possono impedire l'acquisizione di schermate. L'uso del browser include Outlook sul Web e Office per il Web.

Impedire l'acquisizione di schermate consente di evitare la diffusione accidentale o non appropriata di informazioni riservate o sensibili. Tuttavia, esistono molti modi in cui un utente può condividere i dati visualizzati in una schermata e l'acquisizione di una schermata è solo un metodo. Ad esempio, un utente che desidera condividere informazioni visualizzate può scattare una foto usando la fotocamera del telefono, digitare nuovamente i dati o semplicemente comunicarli verbalmente a qualcuno.

Come illustrano in questi esempi, anche se tutte le piattaforme e tutto il software supportassero le API di Rights Management per bloccare l'acquisizione di schermate, la sola tecnologia non può impedire sempre agli utenti di condividere dati che non dovrebbero. Rights Management può contribuire a salvaguardare i dati importanti tramite autorizzazioni e criteri di utilizzo, ma questa soluzione enterprise Rights Management deve essere usata con altri controlli. Ad esempio, implementare la sicurezza fisica, selezionare e monitorare con cura gli utenti che sono autorizzati all'accesso ai dati dell'organizzazione e investire nella formazione degli utenti in modo che sappiano quali dati non devono essere condivisi.

## <a name="whats-the-difference-between-a-user-protecting-an-email-with-do-not-forward-and-a-template-that-doesnt-include-the-forward-right"></a>Qual è la differenza tra un utente che protegge un messaggio di posta elettronica con Non inoltrare e un modello che non include il diritto Inoltra?

Nonostante il nome, **Non inoltrare** non è l'opposto del diritto Inoltra o un modello. Si tratta in realtà di un set di diritti che includono la limitazione della copia, della stampa e del salvataggio del messaggio di posta elettronica all'esterno della cassetta postale, oltre a limitare l'inoltro dei messaggi di posta elettronica. I diritti sono applicati dinamicamente agli utenti tramite i destinatari scelti e non assegnati staticamente dall'amministratore. Per ulteriori informazioni, vedere la sezione non [inviare l'opzione per i messaggi di posta elettronica](configure-usage-rights.md#do-not-forward-option-for-emails) in [configurazione dei diritti di utilizzo per Azure Information Protection](configure-usage-rights.md).