---
title: Che cos'è Azure Information Protection (AIP)?
description: Azure Information Protection (AIP) è un servizio che consente alle organizzazioni di assegnare etichette a documenti e messaggi di posta elettronica, classificando e proteggendo i dati ovunque si trovino.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/23/2020
ms.topic: overview
ms.collection: M365-security-compliance
ms.service: information-protection
Customer intent: As an administrator, I want to label documents and emails to classify and protect my organization's data, wherever it resides.
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 14626d02ca0b5d492312e9d17f0c801c782f5a15
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/07/2020
ms.locfileid: "86048740"
---
# <a name="what-is-azure-information-protection"></a>Che cos'è Azure Information Protection?

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Azure Information Protection è una soluzione basata sul cloud che consente alle organizzazioni di classificare e proteggere documenti e messaggi di posta elettronica mediante l'applicazione di etichette. Le etichette possono essere applicate automaticamente dagli amministratori usando regole e condizioni, manualmente dagli utenti o in modo combinato con gli amministratori che definiscono le raccomandazioni visualizzate agli utenti.

Ad esempio, l'amministratore potrebbe configurare un'etichetta con regole che rilevano dati sensibili, ad esempio le informazioni della carta di credito. In questo caso, qualsiasi utente che salva le informazioni della carta di credito in un file di Word potrebbe visualizzare una descrizione comando nella parte superiore del documento, che consiglia di applicare l'etichetta configurata per questo scenario.

Le etichette possono sia classificare che, facoltativamente, proteggere il documento.

La [classificazione](#how-labels-apply-classification) e la [protezione](#how-data-is-protected) del contenuto consentono di tenere traccia e di controllare il modo in cui viene usato, analizzare i flussi di dati per ottenere informazioni approfondite sull'azienda, rilevare comportamenti rischiosi e adottare misure correttive, tenere traccia dell'accesso ai documenti, impedire la perdita di dati o l'utilizzo improprio e altro ancora.

## <a name="how-labels-apply-classification"></a>Modalità di classificazione in base alle etichette

Le etichette di Azure Information Protection consentono di applicare la classificazione sia a documenti che a messaggi di posta elettronica. 

L'assegnazione di etichette al contenuto include:

- **Classificazione**, che può essere rilevata indipendentemente dalla posizione in cui sono archiviati i dati o da cui vengono condivisi.
- **Contrassegni visivi**, come intestazioni, piè di pagina o filigrane.
- I **metadati** vengono aggiunti a file e intestazioni di messaggi di posta elettronica come testo non crittografato. I metadati come testo non crittografato consentono ad altri servizi di identificare la classificazione e adottare le misure appropriate.

Nell'immagine seguente, ad esempio, l'assegnazione di etichette ha classificato un messaggio di posta elettronica come *Generale*, usando il [client di etichettatura unificata](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients):

:::image type="content" source="media/example-email-footerv2.png" alt-text="Piè di pagina e intestazioni del messaggio di posta elettronica di esempio che mostrano la classificazione di Azure Information Protection":::

In questo esempio, l'etichetta:

- **Aggiunge anche un piè di pagina con *Riservatezza: Generale* al messaggio di posta elettronica.** Il piè di pagina è un indicatore visivo che segnala a tutti i destinatari che il messaggio è previsto per dati aziendali generici che non devono essere inviati fuori dall'organizzazione. 
- **Metadati incorporati nelle intestazioni dei messaggi di posta elettronica.** I dati dell'intestazione consentono ai servizi di posta elettronica di ispezionare l'etichetta e, in teoria, di creare una voce di controllo o impedirne l'invio all'esterno dell'organizzazione.

## <a name="how-data-is-protected"></a>Modalità di protezione dei dati

Azure Information Protection usa il servizio *Azure Rights Management* (Azure RMS) per proteggere i dati. Azure RMS è integrato con altri servizi e applicazioni cloud Microsoft, ad esempio Office 365 e Azure Active Directory, e può essere usato anche con soluzioni di protezione delle informazioni e delle applicazioni personalizzate o di terze parti. Azure RMS funziona con soluzioni sia locali che cloud.

Azure RMS usa crittografia, identità e criteri di autorizzazione. Analogamente alle etichette AIP, la protezione applicata con Azure RMS rimane con i documenti e i messaggi di posta elettronica, indipendentemente dalla posizione del documento o del messaggio di posta elettronica, assicurando di mantenere il controllo del contenuto anche quando viene condiviso con altri utenti.

Le impostazioni di protezione possono fare parte della configurazione delle etichette, in modo che gli utenti classifichino e proteggano i documenti e i messaggi di posta elettronica semplicemente applicando un'etichetta. Le stesse impostazioni di protezione possono anche essere usate dalle applicazioni e dai servizi che supportano la protezione ma non l'assegnazione di etichette. Per le applicazioni e i servizi che supportano solo la protezione, le impostazioni di protezione vengono usate come [modelli di Rights Management](#rights-management-templates).

È possibile, ad esempio, configurare un report o un foglio di calcolo di previsione delle vendite in modo che sia accessibile solo per gli utenti dell'organizzazione. In questo caso, è necessario applicare le impostazioni di protezione per controllare se il documento può essere modificato, limitarlo alla sola lettura o impedire che venga stampato.

I messaggi di posta elettronica possono avere impostazioni di protezione simili per impedirne l'inoltro o l'uso dell'opzione Rispondi a tutti.

### <a name="rights-management-templates"></a>Modelli di Rights Management

Non appena viene attivato il servizio Azure Rights Management, sono disponibili due modelli predefiniti che limitano l'accesso ai dati agli utenti all'interno dell'organizzazione. Usare immediatamente questi modelli o configurare le proprie impostazioni di protezione per applicare controlli più restrittivi in nuovi modelli. 

I modelli di Rights Management possono essere usati con qualsiasi applicazione o servizio che supporta Azure Rights Management.

L'immagine seguente mostra un esempio dall'interfaccia di amministrazione di Exchange, in cui è possibile configurare le regole del flusso di posta elettronica di Exchange Online per l'uso dei modelli di RMS:

![Esempio di selezione di modelli per Exchange Online](./media/templates-exchangeonline-callouts.png)

> [!NOTE]
> La creazione di un'etichetta AIP che include le impostazioni di protezione crea anche un modello di Rights Management corrispondente che può essere usato separatamente dall'etichetta. 
>  

Per altre informazioni, vedere [Informazioni su Microsoft Azure Rights Management](what-is-azure-rms.md).

## <a name="aip-and-end-user-integration-for-documents-and-emails"></a>AIP e integrazione dell'utente finale per documenti e messaggi di posta elettronica

Il client AIP installa la barra di Information Protection per le applicazioni di Office e consente agli utenti finali di integrare AIP nei documenti e nei messaggi di posta elettronica.

Ad esempio, usando il [client di etichettatura unificata](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients) in Excel:

![Esempio di barra di Azure Information Protection in Excel](./media/excelproplus-infoprotect-bar.png)

Sebbene le etichette possano essere applicate automaticamente ai documenti e ai messaggi di posta elettronica, per evitare dubbi agli utenti o per conformarsi ai criteri di un'organizzazione, la barra di Information Protection consente agli utenti finali di selezionare le etichette e applicare la classificazione autonomamente.

Inoltre, il client AIP consente agli utenti di classificare e proteggere altri tipi di file o più file contemporaneamente, usando il menu di scelta rapida da Esplora file di Windows. Ad esempio:

![Comando Classifica e proteggi nel menu di scelta rapida in Esplora file con Azure Information Protection](./media/right-click-classify-protect-folder.png)

L'opzione di menu **Classifica e proteggi** funziona in modo analogo alla barra di Information Protection nelle applicazioni di Office, consentendo agli utenti di selezionare un'etichetta o impostare autorizzazioni personalizzate.

> [!TIP]
> Gli utenti esperti o gli amministratori potrebbero trovare più comodi i comandi di PowerShell per gestire e impostare la classificazione e la protezione per più file. I [comandi di PowerShell pertinenti](https://docs.microsoft.com/powershell/module/azureinformationprotection) sono inclusi nel client e possono anche essere installati separatamente.

Gli utenti e gli amministratori possono usare siti di rilevamento dei documenti per monitorare i documenti protetti, controllare chi vi accede e quando. Se sospettano un uso improprio, possono anche revocare l'accesso ai documenti. Ad esempio:

![Icona per la revoca dell'accesso nel sito di rilevamento dei documenti](./media/tracking-site-revoke-access-icon.png)

### <a name="additional-integration-for-email"></a>Integrazione aggiuntiva per la posta elettronica

L'uso di AIP con Exchange Online offre l'ulteriore vantaggio di poter inviare messaggi di posta elettronica protetti a tutti gli utenti, con la certezza che possano leggerli in qualsiasi dispositivo.

Ad esempio, potrebbe essere necessario inviare informazioni riservate agli indirizzi di posta elettronica personali che usano un account **Gmail**, **Hotmail** o **Microsoft** o a utenti che non hanno un account in Office 365 o Azure AD. Questi messaggi di posta elettronica deve essere crittografati sia nella posizione di archiviazione che in transito e devono essere letti solo dai destinatari originali.

Questo scenario richiede le [funzionalità di Crittografia messaggi di Office 365](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801). Se i destinatari non possono aprire il messaggio di posta elettronica protetto nel client di posta elettronica nativo, possono usare un passcode monouso per leggere le informazioni riservate in un browser.

Ad esempio, un utente di Gmail potrebbe visualizzare la richiesta seguente in un messaggio di posta elettronica ricevuto:

![Esperienza per i destinatari Gmail per Crittografia messaggi di Office 365 e Azure Information Protection](./media/ome-message.png)

Per l'utente che invia il messaggio di posta elettronica, le azioni necessarie sono le stesse per l'invio di un messaggio di posta elettronica protetto a un utente nella propria organizzazione. Ad esempio, selezionare il pulsante **Non inoltrare** che il client AIP può aggiungere alla barra multifunzione di Outlook. 

In alternativa, la funzionalità Non inoltrare può essere integrata in un'etichetta che gli utenti possono selezionare per applicare la classificazione e la protezione al messaggio di posta elettronica. Ad esempio, nel [client di etichettatura unificata](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients):

![Selezione di un'etichetta configurata per Non inoltrare](./media/recipients-only-label2.png)

Gli amministratori possono anche fornire automaticamente protezione per gli utenti configurando regole del flusso di posta che applicano la protezione dei diritti.

Vengono protetti automaticamente anche tutti i documenti di Office allegati a questi messaggi di posta elettronica.

## <a name="scanning-for-existing-content-to-classify-and-protect"></a>Ricerca del contenuto esistente da classificare e proteggere

Idealmente, i documenti e i messaggi di posta elettronica vengono etichettati al momento della creazione. È tuttavia probabile che esistano già molti documenti negli archivi locali o nel cloud e che si vogliano classificare e proteggere anche questi documenti.

Per classificare e proteggere il contenuto esistente, usare uno dei metodi seguenti:

- **Archiviazione locale**: usare lo [scanner di Azure Information Protection](deploy-aip-scanner.md) per individuare, classificare e proteggere i documenti nelle condivisioni di rete e in siti e raccolte di Microsoft SharePoint Server.

    Lo scanner viene eseguito come servizio in Windows Server e usa le stesse regole dei criteri per rilevare le informazioni riservate e applicare etichette specifiche ai documenti. 

    In alternativa, usare lo scanner per applicare un'etichetta predefinita a tutti i documenti in un archivio dati senza esaminare il contenuto dei file. Usare lo scanner in modalità solo report, per individuare informazioni sensibili che potrebbero non essere note.

- **Archiviazione dei dati nel cloud**: usare [Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security/azip-integration) per applicare le etichette ai documenti in Box, SharePoint e OneDrive. Per un'esercitazione, vedere [Applicare automaticamente etichette di classificazione di Azure Information Protection](https://docs.microsoft.com/cloud-app-security/use-case-information-protection) 

## <a name="latest-labeling-updates-for-microsoft-365"></a>Ultimi aggiornamenti di etichettatura per Microsoft 365

Vedere le informazioni più recenti su come Azure Information Protection consente di individuare, classificare, proteggere e monitorare le informazioni riservate, ovunque si trovino, usando Microsoft 365:

> [!VIDEO https://www.youtube.com/embed/UI0p9xqMNfI]

## <a name="additional-azure-information-protection-resources"></a>Risorse aggiuntive per Azure Information Protection

- Versione di valutazione gratuita: [Enterprise Mobility + Security E5](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)

- Opzioni e prezzi per la sottoscrizione: [Prezzi di Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)

- Scaricare il client: [Client di Azure Information Protection](https://www.microsoft.com/download/details.aspx?id=53018)

- Scaricare un manuale dell'utente personalizzabile: [Azure Information Protection End User Adoption Guide](https://download.microsoft.com/download/7/1/2/712A280C-1C66-4EF9-8DC3-88EE43BEA3D4/Azure_Information_Protection_End_User_Adoption_Guide_EN_US.pdf) (Manuale d'uso di Azure Information Protection per utenti finali)

- Domande frequenti: [Domande frequenti su Azure Information Protection](faqs.md)

- Yammer: [Azure Information Protection](https://www.yammer.com/AskIPTeam)

- Novità nella documentazione: [Blog tecnico di Azure Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/bg-p/AzureInformationProtectionBlog/label-name/Docs)

Risorse aggiuntive: [Informazioni e supporto per Azure Information Protection](information-support.md)

### <a name="microsoft-ignite"></a>Microsoft Ignite

Microsoft Ignite 2019 a Orlando è stato un ottimo successo. L'evento ha offerto molte informazioni utili su Azure Information Protection, con gli aggiornamenti e miglioramenti più recenti. Per chi non ha potuto partecipare, le sessioni sono state registrate per essere visualizzate in un secondo momento.

L'elenco seguente indicate le cinque sessioni principali consigliate:

- [BRK2119: Proteggere i dati sensibili. Informazioni sulle funzionalità più recenti di Microsoft Information Protection](https://myignite.techcommunity.microsoft.com/sessions/81172?source=sessions)
 
- [THR3067: Informazioni sui dati. I cinque suggerimenti e consigli più importanti per una miglior comprensione del panorama dei dati sensibili](https://myignite.techcommunity.microsoft.com/sessions/81183)

- [BRK3103: La protezione di file e dati sensibili può essere difficile. Scegliere le opzioni di protezione dati corrette per l'equilibrio tra sicurezza e produttività degli utenti](https://myignite.techcommunity.microsoft.com/sessions/81177?source=sessions)

- [BRK2120: Azure Information Protection è già presente? Esplorazione di etichette unificate, configurazione dei criteri, client e analisi](https://myignite.techcommunity.microsoft.com/sessions/81178?source=sessions)

- [BRK2121: Estendere la potenza dell'etichettatura e della protezione della riservatezza alle app e soluzioni ISV con Microsoft Information Protection SDK](https://myignite.techcommunity.microsoft.com/sessions/81179?source=sessions)

Ultimo post di blog: [Individuare i dati sensibili e proteggerli in modo intelligente con Microsoft 365](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Understand-where-your-sensitive-data-is-located-and/ba-p/960465)


## <a name="next-steps"></a>Passaggi successivi

Configurare e provare a usare Azure Information Protection in autonomia con l'[esercitazione introduttiva](quickstart-viewpolicy.md) e le [esercitazioni](infoprotect-quick-start-tutorial.md). Se invece si è pronti a distribuire il servizio nella propria organizzazione, vedere le [guide con le procedure](how-to-guides.md).
