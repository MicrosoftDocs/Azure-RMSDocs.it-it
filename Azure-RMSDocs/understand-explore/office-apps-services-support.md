---
title: Informazioni su come servizi e applicazioni di Office supportano Azure RMS da AIP
description: Informazioni su come le applicazioni di Office, come Word e Outlook, e i servizi di Office, come Exchange e SharePoint, possono usare il servizio Azure Rights Management da AIP per proteggere i dati dell'organizzazione.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/17/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 388e67cd-c16f-4fa0-a7bb-ffe0def2be81
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 0a9dacaee902d802311c8b7ca76f3f8ed538b667
ms.sourcegitcommit: 44ff610dec678604c449d42cc0b0863ca8224009
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39373355"
---
# <a name="how-office-applications-and-services-support-azure-rights-management"></a>Informazioni su come le applicazioni e i servizi di Office supportano Azure Rights Management 

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Le applicazioni di Office e i servizi Office possono usare il servizio Azure Rights Management di Azure Information Protection per proteggere i dati dell'organizzazione. Le applicazioni di Office sono Word, Excel, PowerPoint e Outlook. I servizi di Office sono Exchange e SharePoint. Le configurazioni di Office che supportano il servizio Azure Rights Management spesso usano il termine **Information Rights Management (IRM)**.

## <a name="office-applications-word-excel-powerpoint-outlook"></a>Applicazioni Office: Word, Excel, PowerPoint, Outlook
Queste applicazioni supportano Azure Rights Management a livello nativo e consentono agli utenti di applicare la protezione a un documento salvato oppure a un messaggio e-mail da inviare. Gli utenti possono applicare alcuni modelli di protezione. In alternativa, per Word, Excel e PowerPoint, possono scegliere impostazioni personalizzate per limitare l'accesso, i diritti e l'utilizzo. 

Ad esempio, gli utenti possono configurare un documento di Word in modo che possano accedervi solo persone interne all'organizzazione. In alternativa, è possibile controllare se un foglio di calcolo di Excel può essere modificato o limitato alla sola lettura o impedire che venga stampato. Per i file soggetti a vincoli temporali, è possibile configurare un'ora di scadenza per stabilire il momento in cui non è più possibile accedere al file. Questa configurazione può essere effettuata direttamente dall'utente oppure applicando un modello. Per Outlook, gli utenti possono anche scegliere l'opzione **Non inoltrare** per impedire la perdita di dati.

Oltre al supporto di Office nativo per Azure Rights Management, queste applicazioni supportano anche la barra di Azure Information Protection che viene installata con il [client Azure Information Protection](../rms-client/aip-client.md). Questa barra mostra le etichette che consentono agli utenti di applicare automaticamente e con maggiore facilità la protezione a documenti e messaggi di posta elettronica che contengono dati sensibili.

Se si è pronti per la configurazione delle app di Office e del client Azure Information Protection:

- Per configurare le app di Office, vedere [App di Office: configurazione dei client](../deploy-use/configure-office-apps.md).

- Per installare e configurare il client Azure Information Protection, vedere [Client Azure Information Protection: installazione e configurazione dei client](../deploy-use/configure-client.md).

## <a name="exchange-online-and-exchange-server"></a>Exchange Online ed Exchange Server
Quando si usa Exchange Online o Exchange Server, è possibile configurare le opzioni di Information Rights Management (IRM) che supportano Azure Rights Management. Questa configurazione consente a Exchange di offrire le soluzioni di protezione seguenti:

-   **Exchange ActiveSync IRM** per proteggere dispositivi mobili e usare messaggi di posta elettronica protetti.

-   Supporto di protezione della posta elettronica per **Outlook sul Web**, implementato in modo analogo al client Outlook. Questa configurazione consente agli utenti di proteggere i messaggi di posta elettronica tramite modelli o tramite la specifica di singole opzioni. Gli utenti possono leggere e usare messaggi di posta elettronica protetti ricevuti.

-   **Regole di protezione** per client Outlook che un amministratore configura per applicare automaticamente modelli di protezione ai messaggi di posta elettronica per destinatari specifici. Quando ad esempio vengono inviati messaggi e-mail interni all'ufficio legale dell'organizzazione, è possibile configurare tali messaggi in modo che possano essere letti solo dai membri dell'ufficio e che non possano essere inoltrati. Prima di inviare il messaggio di posta elettronica gli utenti vedono la regola di protezione applicata e, per impostazione predefinita, possono rimuovere la protezione se ritengono non sia necessaria. I messaggi e-mail vengono crittografati prima dell'invio. Per altre informazioni, vedere [Regole di protezione di Outlook](https://technet.microsoft.com/library/dd638178%28v=exchg.150%29.aspx) e [Creare una regola di protezione di Outlook](https://technet.microsoft.com/library/dd638196%28v=exchg.150%29.aspx) nella libreria di Exchange.

-   **Regole del flusso di posta** che un amministratore configura per applicare automaticamente modelli di protezione della posta elettronica. Queste regole sono basate su proprietà quali il mittente, il destinatario, l'oggetto e il contenuto del messaggio. Queste regole sono concettualmente analoghe alle regole di protezione, ma non consentono agli utenti di rimuovere la protezione. Le regole possono essere applicate ad Outlook sul Web e ai messaggi di posta elettronica inviati da dispositivi mobili. Inoltre, queste regole non crittografano i messaggi di posta elettronica prima che vengano inviati dal client. Per altre informazioni, vedere [Creare una regola di protezione del trasporto](https://technet.microsoft.com/library/dd302432.aspx) nella libreria di Exchange.

-   **Criteri di prevenzione della perdita dei dati** che contengono set di condizioni per filtrare i messaggi di posta elettronica e intraprendere azioni per prevenire la perdita di dati nel caso di informazioni riservate o sensibili, ad esempio quelle personali o correlate alla carta di credito. Quando si rilevano dati sensibili, è possibile usare i suggerimenti relativi ai criteri per avvertire gli utenti che potrebbe essere necessario applicare la protezione. Per altre informazioni, vedere [Prevenzione della perdita di dati](https://technet.microsoft.com/library/jj150527(v=exchg.160\).aspx) nella libreria di Exchange.

-   **Office 365 Message Encryption** che supporta l'invio di un messaggio di posta elettronica protetto e di documenti di Office protetti come allegati a qualsiasi indirizzo in un dispositivo qualunque. Per gli account utente che non usano Azure AD. Questa esperienza Web supporta i provider di identità basati su social network e un passcode monouso. Per altre informazioni, vedere [Set up new Office 365 Message Encryption capabilities built on top of Azure Information Protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e) (Impostare le nuove funzionalità di Office 365 Message Encryption basate su Azure Information Protection).

Se si usa Exchange locale, è possibile usare le funzionalità IRM con il servizio di Azure Rights Management tramite la distribuzione del connettore Azure Rights Management. Il connettore funziona come un relè tra i server locali e il servizio di Azure Rights Management.

Se si è pronti per la configurazione di Exchange per IRM:

- Per Exchange Online, vedere [Exchange Online: configurazione di IRM](../deploy-use/configure-office365.md#exchange-online-irm-configuration).

- Per Exchange locale, vedere [Distribuzione del connettore di Azure Rights Management](../deploy-use/deploy-rms-connector.md).


## <a name="sharepoint-online-and-sharepoint-server"></a>SharePoint Online e SharePoint Server

Quando si usa SharePoint Online o SharePoint Server è possibile proteggere i documenti con la funzionalità Information Rights Management (IRM) di SharePoint. Questa funzionalità consente agli amministratori di proteggere elenchi o raccolte in modo che, se un utente estrae un documento, il file scaricato sia protetto e solo le persone autorizzate possano visualizzarlo e usarlo in base ai criteri di protezione delle informazioni specificati. Il file ad esempio potrebbe essere di sola lettura, potrebbe esserne stata disabilitata la copia del testo oppure potrebbe esserne stato impedito il salvataggio di una copia locale e la stampa.

I documenti di Word, PowerPoint, Excel e PDF supportano questo tipo di protezione IRM SharePoint. Per impostazione predefinita, la protezione è limitata alla persona che scarica il documento, ma è possibile modificarla con un'opzione di configurazione che estende la protezione a tutti gli utenti che hanno accesso al documento in SharePoint o a un gruppo specificato.

La protezione delle informazioni per elenchi e raccolte di SharePoint viene sempre configurata da un amministratore e mai da un utente finale. Le autorizzazioni vengono impostate a livello di sito e per impostazione predefinita vengono ereditate da qualsiasi elenco o raccolta in tale sito. Se si usa SharePoint Online, gli utenti possono anche configurare la propria raccolta OneDrive for Business per la protezione IRM.

Per ottenere un controllo più granulare, è possibile configurare un elenco o una raccolta nel sito in modo che non erediti più le autorizzazioni dal relativo padre. È quindi possibile configurare a livello di elenco o raccolta le autorizzazioni IRM, a cui successivamente viene fatto riferimento come "autorizzazioni univoche". Tuttavia, le autorizzazioni vengono sempre impostate a livello di contenitore. Non è possibile impostare autorizzazioni su singoli file. 

È necessario inoltre che il servizio IRM sia abilitato per SharePoint. Quindi, si specificano le autorizzazioni IRM per una raccolta. Per SharePoint Online e OneDrive for Business, gli utenti possono specificare anche autorizzazioni IRM per la propria raccolta OneDrive for Business. SharePoint non usa modelli di criteri per i diritti, anche se è possibile selezionare impostazioni di configurazione di SharePoint molto simili ad alcune impostazioni che si possono specificare nei modelli.

Se si usa SharePoint Server, è possibile usare questo tipo di protezione IRM distribuendo il connettore di Azure Rights Management. Il connettore funziona come un relè tra i server locali e il servizio cloud di Rights Management. Per ulteriori informazioni, vedere [Distribuzione del connettore di Azure Rights Management](../deploy-use/deploy-rms-connector.md).

> [!NOTE]
> Attualmente esistono alcune limitazioni quando si usa il servizio IRM per SharePoint:
> 
> - Non è possibile usare i modelli di protezione predefiniti o personalizzati gestiti nel portale di Azure. 
> 
> - I file con un'estensione di file .ppdf per i file PDF protetti non sono supportati. I file con estensione PDF sono supportati e, una volta scaricati, possono essere aperti tramite un'applicazione PDF che supporta in modo nativo Rights Management. Ad esempio, il client di Azure Information Protection per Windows include un visualizzatore per questi file PDF protetti. Visualizzatori PDF alternativi sono elencati nella [tabella delle applicazioni abilitate per RMS](../get-started/requirements-applications.md#rms-enlightened-applications).
> 
> - La creazione condivisa, ovvero la modifica di un documento da parte di più utenti contemporaneamente, non è supportata. Per modificare un documento in una libreria protetta tramite IRM, è innanzitutto necessario estrarre il documento, scaricarlo e quindi modificarlo nell'applicazione Office. Di conseguenza, solo un utente alla volta può modificare il documento.

Per le librerie non protette con IRM, se si protegge un file e quindi il file viene caricato in SharePoint o OneDrive, le seguenti funzionalità del file vengono disattivate: Creazione condivisa, Office Online, ricerca, anteprima dei documenti, anteprima dei video, eDiscovery e prevenzione della perdita di dati (DLP).

Quando si usa la protezione IRM per SharePoint il servizio Azure Rights Management applica restrizioni d'uso e crittografia dei dati ai documenti quando questi vengono scaricati da SharePoint, e non quando il documento viene creato per la prima volta in SharePoint o caricato nella raccolta. Per informazioni su come vengono protetti i documenti di essere scaricati, vedere [Crittografia dei dati in OneDrive for Business e SharePoint Online](https://technet.microsoft.com/library/dn905447.aspx) nella documentazione di SharePoint.

Anche se non è recente, il post seguente del blog di Office 365 contiene altre informazioni che possono risultare utili: [What's New with Information Rights Management in SharePoint and SharePoint Online](https://www.microsoft.com/en-us/microsoft-365/blog/2012/11/09/whats-new-with-information-rights-management-in-sharepoint-and-sharepoint-online/) (Novità di Information Rights Management in SharePoint e SharePoint Online)

Se si è pronti per la configurazione di SharePoint per IRM:

- Per SharePoint Online, vedere [SharePoint Online e OneDrive for Business: configurazione di IRM](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration).

- Per SharePoint Server, vedere [Distribuzione del connettore di Azure Rights Management](../deploy-use/deploy-rms-connector.md).


## <a name="next-steps"></a>Passaggi successivi

Se si usa Office 365, può essere interessante leggere il documento [File Protection Solutions in Office 365](/office365/enterprise/microsoft-cloud-it-architecture-resources#BKMK_O365fileprotect) (Soluzioni di protezione dei file in Office 365), che indica le funzionalità consigliate per la protezione dei file in Office 365.

Per informazioni su come altri servizi e applicazioni supportano il servizio Azure Rights Management di Azure Information Protection, vedere [Supporto del servizio Azure Rights Management da parte delle applicazioni](applications-support.md).

Se si è pronti per iniziare la distribuzione, che include la configurazione di tali applicazioni e servizi, vedere la [Guida di orientamento per la distribuzione di Azure Information Protection](../plan-design/deployment-roadmap.md).
