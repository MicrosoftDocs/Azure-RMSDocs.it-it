---
title: Informazioni su come servizi e applicazioni di Office supportano Azure RMS da AIP
description: Informazioni su come le applicazioni di Office, come Word e Outlook, e i servizi di Office, come Exchange e SharePoint, possono usare il servizio Azure Rights Management da AIP per proteggere i dati dell'organizzazione.
author: cabailey
ms.author: cabailey
manager: rkarlin
ms.date: 05/31/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 388e67cd-c16f-4fa0-a7bb-ffe0def2be81
ms.subservice: azurerms
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 8dc7cc5f8e7c7a09293fedf0b4bb9874df339437
ms.sourcegitcommit: fa16364879823b86b4e56ac18a1fc8de5a5dae57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/01/2020
ms.locfileid: "84249879"
---
# <a name="how-office-applications-and-services-support-azure-rights-management"></a>Informazioni su come le applicazioni e i servizi di Office supportano Azure Rights Management 

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Le applicazioni di Office e i servizi Office possono usare il servizio Azure Rights Management di Azure Information Protection per proteggere i dati dell'organizzazione. Le applicazioni di Office sono Word, Excel, PowerPoint e Outlook. I servizi Office sono Exchange e Microsoft SharePoint. Le configurazioni di Office che supportano il servizio Azure Rights Management spesso usano il termine **Information Rights Management (IRM)**.

## <a name="office-applications-word-excel-powerpoint-outlook"></a>Applicazioni Office: Word, Excel, PowerPoint, Outlook
Queste applicazioni supportano Azure Rights Management a livello nativo e consentono agli utenti di applicare la protezione a un documento salvato oppure a un messaggio e-mail da inviare. Gli utenti possono applicare alcuni [modelli](configure-policy-templates.md) di protezione. In alternativa, per Word, Excel e PowerPoint, possono scegliere impostazioni personalizzate per limitare l'accesso, i diritti e l'utilizzo.

Ad esempio, gli utenti possono configurare un documento di Word in modo che possano accedervi solo persone interne all'organizzazione. In alternativa, è possibile controllare se un foglio di calcolo di Excel può essere modificato o limitato alla sola lettura o impedire che venga stampato. Per i file soggetti a vincoli temporali, è possibile configurare un'ora di scadenza per stabilire il momento in cui non è più possibile accedere al file. Questa configurazione può essere effettuata direttamente dagli utenti oppure applicando un modello di protezione. Per Outlook, gli utenti possono anche scegliere l'opzione **Non inoltrare** per impedire la perdita di dati.

Se si è pronti per configurare le app di Office [, vedere app di Office: configurazione dei client](configure-office-apps.md).

> [!NOTE]
> A causa di una limitazione negli aggiornamenti recenti di Windows, è possibile che i file collegati ai messaggi di posta elettronica siano attualmente bloccati dopo l'apertura del file.

## <a name="exchange-online-and-exchange-server"></a>Exchange Online ed Exchange Server
Quando si usa Exchange Online o Exchange Server, è possibile configurare le opzioni per Azure Information Protection. Questa configurazione consente a Exchange di offrire le soluzioni di protezione seguenti:

-   **Exchange ActiveSync IRM** per proteggere dispositivi mobili e usare messaggi e-mail protetti.

-   Supporto di protezione della posta elettronica per **Outlook sul Web**, implementato in modo analogo al client Outlook. Questa configurazione consente agli utenti di proteggere i messaggi di posta elettronica tramite opzioni o modelli di protezione. Gli utenti possono leggere e usare messaggi di posta elettronica protetti ricevuti.

-   **Regole di protezione** per client Outlook che un amministratore configura per applicare automaticamente opzioni e modelli di protezione ai messaggi di posta elettronica per destinatari specifici. Quando ad esempio vengono inviati messaggi e-mail interni all'ufficio legale dell'organizzazione, è possibile configurare tali messaggi in modo che possano essere letti solo dai membri dell'ufficio e che non possano essere inoltrati. Prima di inviare il messaggio di posta elettronica gli utenti vedono la regola di protezione applicata e, per impostazione predefinita, possono rimuovere la protezione se ritengono non sia necessaria. I messaggi e-mail vengono crittografati prima dell'invio. Per altre informazioni, vedere [Regole di protezione di Outlook](https://technet.microsoft.com/library/dd638178%28v=exchg.150%29.aspx) e [Creare una regola di protezione di Outlook](https://technet.microsoft.com/library/dd638196%28v=exchg.150%29.aspx) nella libreria di Exchange.

-   **Regole del flusso di posta** che un amministratore configura per applicare automaticamente opzioni o modelli di protezione ai messaggi di posta elettronica. Queste regole sono basate su proprietà quali il mittente, il destinatario, l'oggetto e il contenuto del messaggio. Queste regole sono concettualmente analoghe a quelle di protezione, ma non consentono agli utenti di rimuovere la protezione perché quest'ultima viene impostata dal servizio Exchange anziché dal client. Dal momento che la protezione viene impostata dal servizio, non importa quale dispositivo o quale sistema operativo abbiano gli utenti. Per altre informazioni, vedere [Regole del flusso di posta (regole di trasporto) in Exchange Online](/exchange/security-and-compliance/mail-flow-rules/mail-flow-rules) e [Creare una regola di protezione del trasporto](https://technet.microsoft.com/library/dd302432.aspx) per Exchange locale.

-   **Criteri di prevenzione della perdita dei dati** che contengono set di condizioni per filtrare i messaggi di posta elettronica e intraprendere azioni, in modo da prevenire la perdita di dati nel caso di informazioni riservate o sensibili. Una delle azioni che è possibile specificare consiste nell'applicare la crittografia come protezione, specificando una delle opzioni o dei modelli di protezione. Quando si rilevano dati sensibili, è possibile usare i suggerimenti relativi ai criteri per avvertire gli utenti che potrebbe essere necessario applicare la protezione. Per altre informazioni, vedere [Prevenzione della perdita di dati](/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention) nella documentazione di Exchange Online.

-   **Office 365 Message Encryption** che supporta l'invio di un messaggio di posta elettronica protetto e di documenti di Office protetti come allegati a qualsiasi indirizzo di posta elettronica in un dispositivo qualunque. Per gli account utente che non usano Azure AD. Questa esperienza Web supporta i provider di identità basati su social network e un passcode monouso. Per altre informazioni, vedere [Configurare le nuove funzionalità di Office 365 Message Encryption basate su Azure Information Protection](/microsoft-365/compliance/set-up-new-message-encryption-capabilities) nella documentazione di Office 365. Per trovare altre informazioni correlate a questa configurazione, vedere [Office 365 Message Encryption](https://docs.microsoft.com/microsoft-365/compliance/ome).

Se si usa Exchange locale, è possibile usare le funzionalità IRM con il servizio di Azure Rights Management tramite la distribuzione del connettore Azure Rights Management. Il connettore funziona come un relè tra i server locali e il servizio di Azure Rights Management.

Per altre informazioni sui modelli di protezione, vedere [Configurazione e gestione dei modelli per Azure Information Protection](configure-policy-templates.md).

Per altre informazioni sulle opzioni per la posta elettronica che è possibile usare per proteggere i messaggi, vedere [Opzione Non inoltrare per i messaggi di posta elettronica](configure-usage-rights.md#do-not-forward-option-for-emails) e [Opzione Encrypt-Only (Solo crittografia) per i messaggi di posta elettronica](configure-usage-rights.md#encrypt-only-option-for-emails).

Se si è pronti per configurare Exchange per la protezione dei messaggi di posta elettronica:

- Per Exchange Online, vedere [Exchange Online: configurazione di IRM](configure-office365.md#exchangeonline-irm-configuration).

- Per Exchange locale, vedere [Distribuzione del connettore di Azure Rights Management](deploy-rms-connector.md).


## <a name="sharepoint-in-microsoft-365-and-sharepoint-server"></a>SharePoint in Microsoft 365 e SharePoint Server

Quando si utilizza SharePoint in Microsoft 365 o SharePoint Server, è possibile proteggere i documenti utilizzando la funzionalità di SharePoint Information Rights Management (IRM). Questa funzionalità consente agli amministratori di proteggere elenchi o raccolte in modo che, se un utente estrae un documento, il file scaricato sia protetto e solo le persone autorizzate possano visualizzarlo e usarlo in base ai criteri di protezione delle informazioni specificati. Il file ad esempio potrebbe essere di sola lettura, potrebbe esserne stata disabilitata la copia del testo oppure potrebbe esserne stato impedito il salvataggio di una copia locale e la stampa.

I documenti di Word, PowerPoint, Excel e PDF supportano questo tipo di protezione IRM SharePoint. Per impostazione predefinita, la protezione è limitata alla persona che scarica il documento, È possibile modificare questa impostazione predefinita con un'opzione di configurazione denominata **Consenti protezione gruppo**, che estende la protezione a un gruppo specificato. Ad esempio, è possibile specificare un gruppo autorizzato a modificare i documenti nella raccolta in modo che lo stesso gruppo di utenti possa modificare il documento all'esterno di SharePoint, indipendentemente dall'utente che ha scaricato il documento. In alternativa, è possibile specificare un gruppo senza le autorizzazioni in SharePoint, ma gli utenti in questo gruppo devono accedere al documento all'esterno di SharePoint. La protezione delle informazioni per elenchi e raccolte di SharePoint viene sempre configurata da un amministratore e mai da un utente finale. Le autorizzazioni vengono impostate a livello di sito e per impostazione predefinita vengono ereditate da qualsiasi elenco o raccolta in tale sito. Se si usa SharePoint in Microsoft 365, gli utenti possono anche configurare la relativa libreria OneDrive Microsoft per la protezione IRM.

Per ottenere un controllo più granulare, è possibile configurare un elenco o una raccolta nel sito in modo che non erediti più le autorizzazioni dal relativo padre. È quindi possibile configurare a livello di elenco o raccolta le autorizzazioni IRM, a cui successivamente viene fatto riferimento come "autorizzazioni univoche". Tuttavia, le autorizzazioni vengono sempre impostate a livello di contenitore. Non è possibile impostare autorizzazioni su singoli file. 

È necessario inoltre che il servizio IRM sia abilitato per SharePoint. Quindi, si specificano le autorizzazioni IRM per una raccolta. Per SharePoint e OneDrive, gli utenti possono anche specificare le autorizzazioni IRM per la propria libreria OneDrive. SharePoint non usa modelli di criteri per i diritti, anche se è possibile selezionare impostazioni di configurazione di SharePoint molto simili ad alcune impostazioni che si possono specificare nei modelli.

Se si usa SharePoint Server, è possibile usare questo tipo di protezione IRM distribuendo il connettore di Azure Rights Management. Il connettore funziona come un relè tra i server locali e il servizio cloud di Rights Management. Per altre informazioni, vedere [Deploying the Azure Rights Management Connector](deploy-rms-connector.md).

> [!NOTE]
> L'utilizzo di IRM per SharePoint presenta alcune limitazioni:
> 
> - Non è possibile usare i modelli di protezione predefiniti o personalizzati gestiti nel portale di Azure. 
> 
> - I file con un'estensione di file .ppdf per i file PDF protetti non sono supportati. Per altre informazioni sulla visualizzazione dei documenti PDF protetti, vedere [Lettori di file PDF protetti per Microsoft Information Protection](./rms-client/protected-pdf-readers.md).
> 
> - La creazione condivisa, ovvero la modifica di un documento da parte di più utenti contemporaneamente, non è supportata. Per modificare un documento in una libreria protetta tramite IRM, è innanzitutto necessario estrarre il documento, scaricarlo e quindi modificarlo nell'applicazione Office. Di conseguenza, solo un utente alla volta può modificare il documento.

Per le librerie che non sono protette con IRM, se si applica la protezione solo a un file che viene quindi caricato in SharePoint o OneDrive, le operazioni seguenti non funzionano con questo file: creazione condivisa, Office per il Web, ricerca, anteprima dei documenti, anteprima, eDiscovery e prevenzione della perdita dei dati (DLP).

> [!IMPORTANT]
> È possibile utilizzare IRM per SharePoint in combinazione con etichette di riservatezza che applicano la protezione. Quando si utilizzano entrambe le funzionalità insieme, il comportamento cambia per i file protetti. Per altre informazioni, vedere [abilitare le etichette di riservatezza per i file di Office in SharePoint e OneDrive](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files).

Quando si usa la protezione IRM per SharePoint il servizio Azure Rights Management applica restrizioni d'uso e crittografia dei dati ai documenti quando questi vengono scaricati da SharePoint, e non quando il documento viene creato per la prima volta in SharePoint o caricato nella raccolta. Per informazioni sul modo in cui i documenti vengono protetti prima del download, vedere la pagina relativa alla [crittografia dei dati in OneDrive e SharePoint](https://technet.microsoft.com/library/dn905447.aspx) dalla documentazione di SharePoint.

Sebbene non sia più nuovo, il post seguente del Blog di Office 365 contiene alcune informazioni aggiuntive che possono risultare utili: novità delle [informazioni Rights Management in SharePoint](https://www.microsoft.com/en-us/microsoft-365/blog/2012/11/09/whats-new-with-information-rights-management-in-sharepoint-and-sharepoint-online/)

Per le modifiche in arrivo, vedere [aggiornamenti alla sicurezza, all'amministrazione e alla migrazione di SharePoint](https://techcommunity.microsoft.com/t5/Microsoft-SharePoint-Blog/Updates-to-SharePoint-security-administration-and-migration/ba-p/549585).

Se si è pronti per la configurazione di SharePoint per IRM:

- Per SharePoint in Microsoft 365, vedere [SharePoint in Microsoft 365 e OneDrive: configurazione di IRM](configure-office365.md#sharepoint-in-microsoft-365-and-onedrive-irm-configuration).

- Per SharePoint Server, vedere [Distribuzione del connettore di Azure Rights Management](deploy-rms-connector.md).


## <a name="next-steps"></a>Passaggi successivi

Se si usa Office 365, può essere interessante leggere il documento [File Protection Solutions in Office 365](/office365/enterprise/microsoft-cloud-it-architecture-resources#BKMK_O365fileprotect) (Soluzioni di protezione dei file in Office 365), che indica le funzionalità consigliate per la protezione dei file in Office 365.

Per informazioni su come altri servizi e applicazioni supportano il servizio Azure Rights Management di Azure Information Protection, vedere [Supporto del servizio Azure Rights Management da parte delle applicazioni](applications-support.md).

Se si è pronti per iniziare la distribuzione, che include la configurazione di tali applicazioni e servizi, vedere la [Guida di orientamento per la distribuzione di Azure Information Protection](deployment-roadmap.md).
