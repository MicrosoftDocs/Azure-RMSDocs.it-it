---
title: Domande frequenti su Azure RMS - AIP
description: Domande frequenti sul servizio di protezione dei dati, Azure Rights Management (Azure RMS) di Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/14/2018
ms.topic: conceptual
ms.service: information-protection
ms.custom: askipteam
ms.assetid: 90df11c5-355c-4ae6-a762-351b05d0fbed
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ac079a7046b6166b89c828054ed5f94e756fa99f
ms.sourcegitcommit: 8bda26b8b84cb8b66ae8f927906710d60c4b6a80
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2019
ms.locfileid: "54397981"
---
# <a name="frequently-asked-questions-about-data-protection-in-azure-information-protection"></a>Domande frequenti sulla protezione dei dati in Azure Information Protection

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Di seguito sono riportate alcune possibili domande sul servizio di protezione dei dati, Azure Rights Management, di Azure Information Protection e le relative risposte.

## <a name="do-files-have-to-be-in-the-cloud-to-be-protected-by-azure-rights-management"></a>Per essere protetti da Azure Rights Management, i file devono trovarsi sul cloud?
No, questo è un malinteso comune. Il servizio Azure Rights Management e Microsoft non visualizzano né archiviano i dati dell'utente come parte del processo di protezione delle informazioni. Le informazioni protette non vengono mai inviate o archiviate in Azure, a meno di archiviarle in modo esplicito in Azure o di usare un altro servizio cloud che le archivia in Azure.

Per altre informazioni, vedere [Funzionamento di Azure RMS: dietro le quinte](./how-does-it-work.md) per comprendere come la formula segreta per una bevanda gassata creata e archiviata in locale viene protetta dal servizio Azure Rights Management pur rimanendo in locale.

## <a name="whats-the-difference-between-azure-rights-management-encryption-and-encryption-in-other-microsoft-cloud-services"></a>Qual è la differenza tra la crittografia in Azure Rights Management e la crittografia in altri servizi cloud Microsoft?

Microsoft offre più tecnologie di crittografia che consentono di proteggere i dati nell'ambito di scenari diversi e spesso complementari. Ad esempio, mentre Office 365 offre la crittografia dei dati inattivi per i dati archiviati in Office 365, il servizio Azure Rights Management di Azure Information Protection esegue la crittografia indipendente dei dati, in modo che risultino protetti indipendentemente dalla posizione in cui si trovano o dalla modalità in cui vengono trasmessi.

Queste tecnologie di crittografia sono complementari e per usarle è necessario abilitarle e configurarle in modo indipendente. In tale contesto può essere consentito l'uso di una chiave personale per la crittografia, scenario detto anche "BYOK" (Bring Your Own Key). L'abilitazione della modalità BYOK per una di queste tecnologie non influirà in alcun modo sulle altre. Ad esempio, è possibile usare la modalità BYOK per Azure Information Protection e non per altre tecnologie di crittografia, e viceversa. Le chiavi usate dalle varie tecnologie possono coincidere o essere diverse, a seconda di come sono state configurate le opzioni di crittografia per ogni servizio.

## <a name="whats-the-difference-between-byok-and-hyok-and-when-should-i-use-them"></a>Qual è la differenza tra le modalità BYOK e HYOK e quando è opportuno usarle?

Quando si usa la modalità **BYOK** (Bring Your Own Key) nel contesto di Azure Information Protection, si crea una chiave personale locale per la protezione di Azure Rights Management. Si trasferisce quindi tale chiave a un modulo di protezione hardware (HSM) in Azure Key Vault in cui si continua a possedere e gestire la chiave. Se non si esegue questa operazione, la protezione di Azure Rights Management userà una chiave creata e gestita automaticamente in Azure. Questa configurazione predefinita è indicata come "Gestione di Microsoft" anziché come "Gestione del cliente" (l'opzione BYOK).

Per altre informazioni su BYOK e sull'opportunità di scegliere questa topologia di chiave per l'organizzazione, vedere [Pianificazione e implementazione della chiave del tenant di Azure Information Protection](plan-implement-tenant-key.md).

La modalità **HYOK** (Hold Your Own Key) nel contesto di Azure Information Protection interessa un numero limitato di organizzazioni in cui è archiviato un sottoinsieme di documenti o messaggi di posta elettronica che non possono essere protetti da una chiave archiviata nel cloud. Per tali organizzazioni, questa restrizione si applica anche se la chiave è stata creata e viene gestita tramite BYOK. La restrizione può essere spesso dovuta a requisiti normativi o di conformità e la configurazione HYOK deve essere applicata esclusivamente a informazioni altamente riservate, che non verranno mai condivise all'esterno dell'organizzazione, che verranno utilizzate solo nella rete interna e che non devono essere accessibili da dispositivi mobili.

Per queste eccezioni (che in genere interessano meno del 10% dell'intero contenuto da proteggere), le organizzazioni possono creare la chiave da mantenere in locale usando una soluzione locale, Active Directory Rights Management Services. Con questa soluzione, i computer ottengono i criteri di Azure Information Protection dal cloud, ma il contenuto identificato può essere protetto tramite la chiave locale.

Per altre informazioni su HYOK e per assicurarsi di conoscere le restrizioni e le limitazioni di questa modalità e sapere quando è opportuno usarla, vedere [Requisiti e restrizioni HYOK per la protezione di AD RMS](configure-adrms-restrictions.md).

## <a name="can-i-now-use-byok-with-exchange-online"></a>Ora è possibile usare BYOK con Exchange Online?

Sì, ora è possibile usare BYOK con Exchange Online seguendo le istruzioni in [Set up new Office 365 Message Encryption capabilities built on top of Azure Information Protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e) (Impostare nuove funzionalità di Office 365 Message Encryption basate su Azure Information Protection). Queste istruzioni abilitano le nuove funzionalità di Exchange Online, che supportano l'uso di BYOK per Azure Information Protection e la nuova funzionalità Office 365 Message Encryption.

Per altre informazioni su questa modifica, vedere l'annuncio: [Office 365 Message Encryption with the new capabilities](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801) (Crittografia messaggi di Office 365 con nuove funzionalità) nel blog

## <a name="where-can-i-find-information-about-third-party-solutions-that-integrate-with-azure-rms"></a>Dove sono disponibili informazioni sulle soluzioni di terze parti che si integrano con Azure RMS?

Molti fornitori di software offrono o implementano già soluzioni in grado di integrarsi con Azure Rights Management e l'elenco di tali soluzioni cresce rapidamente. Può essere utile controllare l'elenco di [soluzioni abilitate per RMS](requirements-applications.md#rms-enlightened-solutions) e ottenere gli aggiornamenti più recenti da [Microsoft Mobility@MSFTMobility](https://twitter.com/MSFTMobility) su Twitter. Controllare anche la [Guida per gli sviluppatori](./develop/developers-guide.md) e inserire eventuali domande integrative specifiche sul [sito Yammer](https://www.yammer.com/AskIPTeam) di Azure Information Protection.

## <a name="is-there-a-management-pack-or-similar-monitoring-mechanism-for-the-rms-connector"></a>Esiste un Management Pack o un meccanismo di controllo simile per il connettore RMS?

Il connettore Rights Management registra informazioni, avvisi e messaggi di errore nel registro eventi, ma non esiste un Management Pack che includa il monitoraggio di questi eventi. Tuttavia, l'elenco di eventi e le relative descrizioni con altre informazioni che consentono di adottare misure correttive è documentato [Monitorare il connettore di Azure Rights Management](monitor-rms-connector.md).

## <a name="do-you-need-to-be-a-global-admin-to-configure-azure-rms-or-can-i-delegate-to-other-administrators"></a>È necessario essere un amministratore globale per configurare Azure RMS oppure tale configurazione può essere delegata ad altri amministratori?

Con l'introduzione del nuovo ruolo di amministratore di Information Protection, questa domanda (con la relativa risposta) è stata spostata nella pagina principale delle Domande frequenti: [È necessario essere un amministratore globale per configurare Azure Information Protection oppure tale configurazione può essere delegata ad altri amministratori?](faqs.md#do-you-need-to-be-a-global-admin-to-configure-azure-information-protection-or-can-i-delegate-to-other-administrators)

## <a name="how-do-i-create-a-new-custom-template-in-the-azure-portal"></a>Come creare un nuovo modello personalizzato nel portale di Azure?

È stato effettuato lo spostamento dei modelli personalizzati nel portale di Azure, dove è possibile continuare a gestirli come modelli o convertirli in etichette. Per creare un nuovo modello, creare una nuova etichetta e configurare le impostazioni di protezione dati per Azure RMS. Dietro le quinte, viene creato un nuovo modello che può essere usato dai servizi e le applicazioni che si integrano con i modelli di Rights Management.

Per altre informazioni sui modelli nel portale di Azure, vedere [Configurazione e gestione dei modelli per Azure Information Protection](configure-policy-templates.md).

## <a name="ive-protected-a-document-and-now-want-to-change-the-usage-rights-or-add-usersdo-i-need-to-reprotect-the-document"></a>Se si vuole modificare i diritti di utilizzo o aggiungere utenti a un documento protetto, è necessario proteggerlo nuovamente?

Se il documento è stato protetto usando un'etichetta o un modello, non è necessario proteggerlo nuovamente. Modificare l'etichetta o il modello apportando le modifiche ai diritti di utilizzo o aggiungendo nuovi gruppi o utenti, e salvare le modifiche:

- Quando un utente non ha eseguito l'accesso al documento prima che venissero apportate le modifiche, le modifiche diventano effettive non appena l'utente apre il documento.

- Se l'utente ha già eseguito l'accesso al documento, le modifiche diventano effettive dopo la scadenza del [contratto di licenza con l'utente finale](configure-usage-rights.md#rights-management-use-license). Proteggere nuovamente il documento solo se non è possibile attendere la scadenza del contratto di licenza con l'utente finale. Quando si protegge nuovamente il documento, viene creata una nuova versione del documento e un nuovo contratto di licenza con l'utente finale.

In alternativa, se è già stato configurato un gruppo per le autorizzazioni necessarie, è possibile modificare l'appartenenza al gruppo per includere o escludere gli utenti e non è necessario modificare l'etichetta o il modello. Potrebbe verificarsi un piccolo ritardo prima che le modifiche abbiano effetto, poiché l'appartenenza al gruppo viene [memorizzata nella cache](prepare.md#group-membership-caching-by-azure-information-protection) dal servizio Azure Rights Management.

Se il documento è stato protetto usando le autorizzazioni personalizzate, non è possibile modificare le autorizzazioni per il documento esistente. È necessario proteggere di nuovo il documento e specificare tutti gli utenti e tutti i diritti di utilizzo che sono necessari per la nuova versione del documento. Per proteggere nuovamente un documento protetto, è necessario avere il diritto di utilizzo Controllo completo.

Suggerimento: per verificare se un documento è protetto da un modello o da un'autorizzazione personalizzata, usare il cmdlet di PowerShell [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus). Per le autorizzazioni personalizzate è sempre visibile la descrizione **Accesso limitato** per il modello, con un ID di modello univoco che non viene visualizzato quando si esegue [Get-RMSTemplate](/powershell/module/azureinformationprotection/get-rmstemplate).

## <a name="i-have-a-hybrid-deployment-of-exchange-with-some-users-on-exchange-online-and-others-on-exchange-serveris-this-supported-by-azure-rms"></a>Dispongo di una distribuzione ibrida di Exchange con alcuni utenti su Exchange Online e altri su Exchange Server; questo è supportato da Azure RMS?
Assolutamente e l'aspetto interessante è che gli utenti sono in grado di proteggere e usare senza problemi messaggi di posta elettronica e allegati protetti con le due distribuzioni di Exchange. Per questa configurazione, [attivare Azure RMS](activate-service.md) e [abilitare IRM per Exchange Online](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx), quindi [distribuire e configurare il connettore RMS](deploy-rms-connector.md) per Exchange Server.

## <a name="if-i-use-this-protection-for-my-production-environment-is-my-company-then-locked-into-the-solution-or-risk-losing-access-to-content-that-we-protected-with-azurerms"></a>Se si usa questa protezione nell'ambiente di produzione, l'azienda è costretta a usare sempre questa soluzione o esiste il rischio di perdere l'accesso ai contenuti protetti con Azure RMS?
No, si ha sempre il controllo dei dati e si può continuare ad accedervi, anche se si decide di non usare più il servizio Azure Rights Management. Per altre informazioni, vedere [Rimozione delle autorizzazioni e disattivazione di Azure Rights Management](decommission-deactivate.md).

## <a name="can-i-control-which-of-my-users-can-use-azure-rms-to-protect-content"></a>È possibile determinare quali utenti possono usare Azure RMS per proteggere i contenuti?
Sì, il servizio Azure Rights Management include controlli di selezione utenti per questo scenario. Per altre informazioni, vedere la sezione [Configurazione dei controlli di selezione utenti per una distribuzione graduale](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) dell'articolo [Attivazione di Azure Rights Management](activate-service.md).

## <a name="can-i-prevent-users-from-sharing-protected-documents-with-specific-organizations"></a>È possibile impedire agli utenti di condividere documenti protetti con aziende specifiche?
Uno dei vantaggi principali offerti dal servizio Azure Rights Management per la protezione dei dati è il supporto della collaborazione business-to-business senza che sia necessario configurare trust espliciti per ogni organizzazione partner, in quanto l'autenticazione viene eseguita automaticamente da Azure AD.

Non sono disponibili opzioni di amministrazione che consentano di impedire agli utenti di condividere documenti in modo sicuro con aziende specifiche. Si supponga, ad esempio, di voler bloccare un'azienda che non si considera attendibile o una società concorrente. Impedire al servizio Azure Rights Management di inviare documenti protetti agli utenti di queste società non ha alcuna utilità, dal momento che gli utenti condividerebbero i documenti in modalità non protetta, con maggiori rischi per l'azienda stessa. Inoltre, non sarebbe possibile identificare gli utenti che condividono i documenti aziendali riservati e i rispettivi destinatari in queste aziende, mentre questo è possibile quando i documenti o i messaggi di posta elettronica sono protetti tramite il servizio Azure Rights Management.

## <a name="when-i-share-a-protected-document-with-somebody-outside-my-company-how-does-that-user-get-authenticated"></a>Quando condivido un documento protetto con qualcuno all'esterno della mia azienda, come viene autenticato questo utente?

Per impostazione predefinita, il servizio Azure Rights Management usa un account di Azure Active Directory e un indirizzo di posta elettronica associato per l'autenticazione utente, semplificando la collaborazione business-to-business per gli amministratori. Se l'altra organizzazione usa i servizi di Azure, gli utenti hanno già account in Azure Active Directory, anche se questi account vengono creati e gestiti in locale e poi sincronizzati in Azure. Se l'organizzazione dispone di Office 365, dietro le quinte, questo servizio utilizza anche Azure Active Directory per gli account utente. Se nell'organizzazione dell'utente non esistono account gestiti in Azure, gli utenti possono iscriversi a [RMS per utenti singoli](./rms-for-individuals.md), che consente di creare un tenant e una directory di Azure non gestiti per l'organizzazione con un account per l'utente, in modo che questo utente e gli utenti successivi possano quindi essere autenticati per il servizio Azure Rights Management.

Il metodo di autenticazione per questi account può variare a seconda di come l'amministratore dell’altra organizzazione ha configurato gli account di Azure Active Directory. Ad esempio, è possibile utilizzare password create per questi account, la federazione o password create in Active Directory Domain Services e quindi sincronizzate con Azure Active Directory.

Altri metodi di autenticazione:

- Se si protegge un messaggio di posta elettronica che include come allegato un documento di Office, destinato a un utente che non dispone di un account in Azure AD, il metodo di autenticazione cambia. Il servizio Azure Rights Management è federato con alcuni provider di identità di social networking di grande diffusione, ad esempio Gmail. Se il provider di posta elettronica dell'utente è supportato, l'utente può accedere al servizio e il provider di posta elettronica provvede all'autenticazione dell'utente. Se il provider di posta elettronica dell'utente non è supportato o se l'utente lo desidera, è possibile richiedere un passcode monouso, che permette l'autenticazione e quindi visualizza il messaggio di posta elettronica con il documento protetto in un browser Web.

- Azure Information Protection può usare gli account Microsoft per le applicazioni supportate. Attualmente, non tutte le applicazioni possono aprire contenuti protetti quando viene usato un account Microsoft per l'autenticazione. [Altre informazioni](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)

## <a name="can-i-add-external-users-people-from-outside-my-company-to-custom-templates"></a>È possibile aggiungere utenti esterni (persone all'esterno della mia azienda) ai modelli personalizzati?

Sì. Le [impostazioni di protezione](configure-policy-protection.md) che è possibile configurare nel portale di Azure consentono di aggiungere le autorizzazioni a utenti e gruppi esterni all'organizzazione e anche a tutti gli utenti di un'altra organizzazione. Può risultare utile per fare riferimento all'esempio dettagliato [Proteggere la collaborazione ai documenti tramite Azure Information Protection](secure-collaboration-documents.md). 

Si noti che, in presenza di eventuali etichette di Azure Information Protection, è prima necessario convertire il modello personalizzato in un'etichetta per poter configurare queste impostazioni di protezione nel portale di Azure. Per altre informazioni, vedere [Configurazione e gestione dei modelli per Azure Information Protection](configure-policy-templates.md).

In alternativa, è possibile aggiungere utenti esterni a modelli (ed etichette) personalizzati tramite PowerShell. Questa configurazione richiede l'uso di un oggetto di definizione dei diritti per l'aggiornamento del modello:

1. Specificare gli indirizzi di posta elettronica esterni e i relativi diritti in un oggetto di definizione dei diritti usando il cmdlet [New-AadrmRightsDefinition](/powershell/module/aadrm/new-aadrmrightsdefinition) per creare una variabile.

2. Specificare questa variabile nel parametro RightsDefinition con il cmdlet [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty).

    Quando si aggiungono utenti a un modello esistente, oltre ai nuovi utenti è necessario definire gli oggetti di definizione dei diritti per gli utenti esistenti nei modelli. Per questo scenario può essere utile l'**esempio 3, relativo all'aggiunta di nuovi utenti e diritti a un modello personalizzato** della sezione [Examples](/powershell/module/aadrm/set-aadrmtemplateproperty#examples) (Esempi) per il cmdlet.

## <a name="what-type-of-groups-can-i-use-with-azure-rms"></a>Quali tipi di gruppi è possibile usare con Azure RMS?
Per la maggior parte degli scenari è possibile usare qualsiasi tipo di gruppo di Azure AD che dispone di un indirizzo di posta elettronica. Questa regola empirica è sempre valida quando si assegnano i diritti di utilizzo, ma esistono alcune eccezioni per l'amministrazione del servizio Azure Rights Management. Per altre informazioni, vedere [Requisiti di Azure Information Protection per gli account di gruppo](prepare.md#azure-information-protection-requirements-for-group-accounts).

## <a name="how-do-i-send-a-protected-email-to-a-gmail-or-hotmail-account"></a>Come si invia un messaggio di posta elettronica protetto a un account Gmail o Hotmail?

Quando si usa Exchange Online e il servizio Azure Rights Management, è sufficiente inviare il messaggio di posta elettronica all'utente come messaggio protetto. Ad esempio, è possibile selezionare il nuovo pulsante **Proteggi** nella barra dei comandi in Outlook sul web, usare il pulsante o l'opzione di menu **Non inoltrare** di Outlook. In alternativa, è possibile selezionare un'etichetta di Azure Information Protection che applica automaticamente il comando Non inoltrare e classifica il messaggio di posta elettronica.

Il destinatario visualizza un'opzione per accedere al proprio account Gmail, Yahoo o Microsoft e quindi può leggere il messaggio di posta elettronica protetto. In alternativa il destinatario può optare per un passcode monouso e leggere il messaggio di posta elettronica in un browser.

Per supportare questo scenario, Exchange Online deve essere abilitato per il servizio Azure Rights Management e per le nuove funzionalità di Office 365 Message Encryption. Per altre informazioni su questa configurazione, vedere [Exchange Online: configurazione di IRM](configure-office365.md#exchangeonline-irm-configuration).

Per altre informazioni sulle nuove funzionalità che includono il supporto di tutti gli account di posta elettronica in tutti i dispositivi, vedere il post di blog seguente: [Announcing new capabilities available in Office 365 Message Encryption](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801) (Annuncio di nuove funzionalità disponibili in Crittografia messaggi di Office 365).

## <a name="what-devices-and-which-file-types-are-supported-by-azure-rms"></a>Quali dispositivi e quali tipi di file sono supportati da Azure RMS?
Per un elenco dei dispositivi che supportano il servizio Azure Rights Management, vedere [Dispositivi client che supportano la protezione dati di Azure Rights Management](./requirements-client-devices.md). Dal momento che non tutti i dispositivi supportati consentono l'uso di tutte le funzionalità di Rights Management, controllare anche la tabella relativa alle [applicazioni abilitate per RMS](./requirements-applications.md#rms-enlightened-applications).

Il servizio Azure Rights Management può supportare tutti i tipi di file. Per file di testo e di immagine, file di Microsoft Office (Word, Excel e PowerPoint), file con estensione pdf e altri tipi di file di applicazione, Azure Rights Management fornisce la protezione nativa, incluse crittografia e applicazione di diritti (autorizzazioni). Per tutte le altre applicazioni e tipi di file, la protezione generica fornisce funzionalità di incapsulamento e autenticazione dei file che consentono di verificare se un utente è autorizzato ad aprire il file.

Per un elenco delle estensioni di file supportate in modo nativo da Azure Rights Management, vedere [Tipi di file supportati dal client Azure Information Protection](./rms-client/client-admin-guide-file-types.md). Le estensioni di file non incluse nell'elenco sono supportate mediante l'uso del client Azure Information Protection, che applica automaticamente la protezione generica a tali file.

## <a name="how-do-i-configure-a-mac-computer-to-protect-and-track-documents"></a>Come configurare un computer Mac per proteggere e tracciare i documenti?

Prima di tutto, assicurarsi di avere installato Office per Mac usando il collegamento di installazione software da https://portal.office.com. Per le istruzioni complete, vedere [Scaricare e installare o reinstallare Office 365 o Office 2016 in un PC o Mac](https://support.office.com/en-us/article/Download-and-install-or-reinstall-Office-365-or-Office-2016-on-a-PC-or-Mac-4414EAAF-0478-48BE-9C42-23ADC4716658).

Aprire Outlook e creare un profilo mediante l'account aziendale o dell'istituto di istruzione di Office 365. Creare quindi un nuovo messaggio ed eseguire le operazioni seguenti per configurare Office in modo che possa proteggere documenti e messaggi di posta elettronica tramite il servizio Azure Rights Management:

1. Nella scheda **Opzioni** del nuovo messaggio fare clic su **Autorizzazioni** e quindi su **Verifica credenziali**.

2. Quando richiesto, specificare nuovamente il proprio account aziendale o dell'istituto di istruzione di Office 365 e selezionare **Accedi**.

    Vengono scaricati i modelli di Azure Rights Management e l'opzione **Verifica credenziali** viene sostituita da opzioni che includono **Nessuna restrizione**, **Non inoltrare** e tutti i modelli di Azure Rights Management pubblicati per il tenant. È ora possibile annullare questo nuovo messaggio.

Per proteggere un messaggio di posta elettronica o un documento: nella scheda **Opzioni** fare clic su **Autorizzazioni** e scegliere un'opzione o un modello che protegge il messaggio di posta elettronica o il documento.

Per tenere traccia di un documento dopo averlo protetto: da un computer Windows in cui è installato il client Azure Information Protection, registrare il documento con il sito di rilevamento dei documenti usando un'applicazione di Office o Esplora file. Per le relative istruzioni, vedere [Tenere traccia dei documenti e revocarli](./rms-client/client-track-revoke.md). Dal computer Mac ora è possibile usare il Web browser e accedere al sito di rilevamento dei documenti (https://track.azurerms.com)) per rilevare e revocare il documento.

## <a name="when-i-open-an-rms-protected-office-document-does-the-associated-temporary-file-become-rms-protected-as-well"></a>Quando si apre un documento di Office protetto da RMS, anche il file temporaneo associato è protetto da RMS?
No. In questo scenario, il file temporaneo associato non contiene i dati del documento originale, ma solo i dati immessi dall'utente mentre il file è aperto. A differenza del file originale, il file temporaneo non è destinato alla condivisione e rimarrà disponibile nel dispositivo, protetto dai controlli di protezione locali, ad esempio BitLocker ed EFS.

## <a name="a-feature-i-am-looking-for-doesnt-seem-to-work-with-sharepoint-protected-librariesis-support-for-my-feature-planned"></a>Una funzionalità che cerco non sembra funzionare con le librerie protette di SharePoint, è previsto il supporto per la mia funzionalità?
Attualmente, SharePoint supporta documenti protetti da RMS usando le librerie protette IRM, che non supportano i modelli di Rights Management, il rilevamento dei documenti e alcune altre funzionalità. Per altre informazioni, vedere la sezione [SharePoint Online e SharePoint Server](./office-apps-services-support.md#sharepoint-online-and-sharepoint-server) nell'articolo [Servizi e applicazioni di Office](./office-apps-services-support.md).

Se si è interessati a una funzionalità specifica non ancora supportata, assicurarsi di controllare gli annunci nel [blog di Enterprise Mobility + Security](https://cloudblogs.microsoft.com/enterprisemobility/?product=azure-rights-management-services).

## <a name="how-do-i-configure-one-drive-for-business-in-sharepoint-online-so-that-users-can-safely-share-their-files-with-people-inside-and-outside-the-company"></a>Come è possibile configurare One Drive for Business in SharePoint Online, in modo che gli utenti possano condividere i propri file in modo sicuro con le persone all'interno e all'esterno della società?
Per impostazione predefinita, in qualità di amministratore di Office 365, non si configura questo oggetto. L'operazione viene eseguita dagli utenti.

Proprio come gli amministratori del sito di SharePoint abilitano e configurano IRM per una raccolta di SharePoint che possiedono, OneDrive for Business è progettato per consentire agli utenti di attivare e configurare IRM per la propria raccolta OneDrive for Business. Tuttavia, usando PowerShell, è possibile eseguire questa operazione per gli utenti. Per le istruzioni, vedere la sezione [SharePoint Online e OneDrive for Business: configurazione IRM](configure-office365.md#sharepointonline-and-onedrive-for-business-irm-configuration) nell'articolo [Office 365: configurazione di client e servizi online](configure-office365.md).

## <a name="do-you-have-any-tips-or-tricks-for-a-successful-deployment"></a>Sono disponibili suggerimenti per una corretta distribuzione?

Dopo aver supervisionato un elevato numero di distribuzioni e ascoltato il parere di clienti, partner, consulenti e tecnici del servizio di supporto, uno dei principali suggerimenti che possiamo fornire è **Progettare e distribuire criteri semplici**.

Poiché Azure Information Protection supporta la condivisione sicura con qualsiasi utente, si possono raggiungere livelli di protezione dei dati molto elevati, Prestare tuttavia attenzione quando si configurano restrizioni dei diritti di utilizzo. Per la maggior parte delle organizzazioni, l'impatto operativo principale deriva dall'esigenza di impedire la fuga di dati limitando l'accesso agli utenti dell'organizzazione. Si possono anche applicare criteri più specifici, ad esempio impedire agli utenti di stampare o modificare documenti, ma è preferibile impostarli solo per documenti che richiedono un alto livello di sicurezza. Evitare di applicare tutti questi diritti di utilizzo più restrittivi in un'unica soluzione, pianificando invece un approccio per fasi.

## <a name="how-do-we-regain-access-to-files-that-were-protected-by-an-employee-who-has-now-left-the-organization"></a>Come possiamo riottenere l'accesso ai file che sono stati protetti da un dipendente che ora ha lasciato l'organizzazione?
Usare la [funzionalità utente con privilegi avanzati](configure-super-users.md), che garantisce i diritti di utilizzo Controllo completo per tutti i documenti e i messaggi di posta elettronica protetti dal tenant. Gli utenti con privilegi avanzati possono leggere sempre questi contenuti protetti e, se necessario, rimuovere la protezione o riapplicarla ai contenuti per altri utenti. Questa stessa funzionalità consente ai servizi autorizzati di indicizzare e analizzare i file, in base alle esigenze.

## <a name="when-i-test-revocation-in-the-document-tracking-site-i-see-a-message-that-says-people-can-still-access-the-document-for-up-to-30-daysis-this-time-period-configurable"></a>Quando si testa una revoca nel sito di rilevamento del documento, viene visualizzato un messaggio che informa che gli utenti possono ancora accedere al documento per 30 giorni. È possibile configurare questo periodo di tempo?

Sì. Il messaggio indica il [contratto di licenza con l'utente finale](configure-usage-rights.md#rights-management-use-license) per il file specifico.

Se si revoca un file, tale azione può essere imposta solo quando l'utente si autentica al servizio Azure Rights Management. Pertanto se il periodo di validità della licenza d'uso di un file è pari a 30 giorni e l'utente ha già aperto il documento, tale utente può continuare ad accedere al documento per la durata della licenza d'uso. Quando la licenza d'uso scade l'utente deve ripetere l'autenticazione e a questo punto l'accesso viene negato, perché ora il documento è revocato.

L'utente che ha protetto il documento, ovvero l'[emittente di Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner), è esente da questa revoca ed è sempre in grado di accedere ai propri documenti.

Il valore predefinito per il periodo di validità del contratto di licenza con l'utente finale per un tenant è 30 giorni e questa impostazione può essere sottoposta a override tramite un'impostazione più restrittiva in un'etichetta o un modello. Per altre informazioni sul contratto di licenza con l'utente finale e su come configurarlo, vedere la documentazione [Configurazione dei diritti di utilizzo per Azure Rights Management](configure-usage-rights.md#rights-management-use-license).

## <a name="can-rights-management-prevent-screen-captures"></a>Rights Management può impedire l'acquisizione di schermate?
Non concedendo **Copia** come [diritto di utilizzo](configure-usage-rights.md), Rights Management può impedire l'acquisizione di schermate dagli strumenti più usati per l'acquisizione di schermate nelle piattaforme Windows (Windows 7, Windows 8.1, Windows 10, Windows Phone) e Android. I dispositivi iOS e Mac, tuttavia, non consentono ad alcuna app di impedire l'acquisizione di schermate e i browser, ad esempio se usati con Outlook Web App e Office Online, non possono impedire l'acquisizione di schermate.

Impedire l'acquisizione di schermate può consentire di evitare la diffusione accidentale o non appropriata di informazioni riservate o sensibili. Tuttavia, vi sono molti modi in cui un utente può condividere i dati visualizzati sullo schermo e acquisire una schermata è solo uno di questi metodi. Ad esempio, un utente che desidera condividere informazioni visualizzate può scattare una foto dei dati con la fotocamera del telefono, ridigitarli o semplicemente comunicarli verbalmente a qualcuno.

Come illustrato da questi esempi, anche se tutte le piattaforme e tutto il software supportassero le API di Rights Management per il blocco dell'acquisizione di schermate, la sola tecnologia non sarebbe in grado di impedire sempre agli utenti di condividere dati che dovrebbero essere riservati. Rights Management può contribuire a salvaguardare i dati importanti tramite i criteri di autorizzazione e per l'uso, ma questa soluzione aziendale per la gestione delle autorizzazioni deve essere usata insieme ad altri controlli. Ad esempio, implementare la sicurezza fisica, selezionare e monitorare attentamente le persone che hanno accesso in modo autorizzato ai dati dell'organizzazione e investire nella formazione degli utenti per aiutarli a capire quali dati non devono essere condivisi.

## <a name="whats-the-difference-between-a-user-protecting-an-email-with-do-not-forward-and-a-template-that-doesnt-include-the-forward-right"></a>Qual è la differenza tra un utente che protegge un messaggio di posta elettronica con l'opzione Non inoltrare e un modello che non include il diritto di inoltro?

Nonostante il nome e l'aspetto, l'opzione **Non inoltrare** non è il contrario del diritto Inoltra e neanche un modello. Si tratta in realtà di un insieme di diritti che limitano la copia, la stampa, il salvataggio di allegati e l'inoltro dei messaggi di posta elettronica. I diritti vengono applicati dinamicamente agli utenti tramite i destinatari scelti anziché in modo statico in base alle assegnazioni dall'amministratore. Per altre informazioni, vedere la sezione [Do Not Forward option for emails](configure-usage-rights.md#do-not-forward-option-for-emails) (Opzione Non inoltrare per i messaggi di posta elettronica) dell'articolo [Configuring usage rights for Azure Rights Management](configure-usage-rights.md) (Configurazione dei diritti di utilizzo per Azure Rights Management).

