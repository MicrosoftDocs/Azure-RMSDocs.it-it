---
title: Che cos'è Azure Information Protection? - AIP
description: Panoramica tecnica del servizio Azure Information Protection, che consente a un'organizzazione di assegnare un'etichetta a documenti e messaggi di posta elettronica per classificare e proteggere i dati, ovunque si trovino.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/30/2019
ms.topic: overview
ms.collection: M365-security-compliance
ms.service: information-protection
Customer intent: As an administrator, I want to label documents and emails to classify and protect my organization's data, wherever it resides.
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: b71bc14817aadd1c67452fecc228a339dfebcb42
ms.sourcegitcommit: 1e25e7a32cc0b2a3a6c9b80575927009d8a96838
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/30/2019
ms.locfileid: "71689912"
---
# <a name="what-is-azure-information-protection"></a>Che cos'è Azure Information Protection?

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Azure Information Protection, noto anche come AIP, è una soluzione basata sul cloud che consente alle organizzazioni di classificare e facoltativamente proteggere documenti e messaggi di posta elettronica tramite l'applicazione di etichette. Le etichette possono essere applicate automaticamente dagli amministratori, che definiscono regole e condizioni, manualmente dagli utenti oppure da entrambi, quando gli utenti ricevono raccomandazioni dagli amministratori. 

L'immagine seguente mostra un esempio di Azure Information Protection in azione nel computer di un utente. L'amministratore ha configurato un'etichetta con regole che rilevano i dati sensibili e in questo esempio si tratta delle informazioni di carta di credito. Quando un utente salva un documento di Word che contiene un numero di carta di credito vede una descrizione comando personalizzata che consiglia di applicare l'etichetta configurata dall'amministratore. Questa etichetta classifica il documento e lo protegge. 

![Esempio di classificazione consigliata per Azure Information Protection](./media/info-protect-recommend-calloutsv2.png)

###### <a name="screenshot-from-the-azure-information-protection-client-classicfaqsmdwhats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client"></a>Screenshot dal [client di Azure Information Protection (classico)](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)

Dopo che il contenuto è stato classificato (e facoltativamente protetto), è possibile rilevare e controllare come viene usato. È possibile analizzare i flussi di dati per ottenere informazioni sulle attività aziendali, rilevare comportamenti a rischio e adottare misure correttive, tenere traccia dell'accesso ai documenti, impedire la perdita o l'uso improprio di dati e così via.

## <a name="how-labels-apply-classification"></a>Modalità di classificazione in base alle etichette

Le etichette di Azure Information Protection consentono di applicare la classificazione a documenti e messaggi di posta elettronica. In questo modo, la classificazione è identificabile indipendentemente dalla posizione di archiviazione dei dati o dagli utenti con cui è condivisa. Le etichette possono includere contrassegni visivi, ad esempio un'intestazione, un piè di pagina o una filigrana. I metadati vengono aggiunti a file e intestazioni di messaggi di posta elettronica come testo non crittografato. Il testo non crittografato consente ad altri servizi, ad esempio le soluzioni di prevenzione della perdita di dati, di identificare la classificazione e adottare le misure appropriate. 

Ad esempio il messaggio di posta elettronica seguente è stato classificato come "General" (Generale). L'etichetta ha aggiunto il piè di pagina "Sensitivity: General" (Riservatezza: Generale) al messaggio di posta elettronica. Il piè di pagina è un indicatore visivo che segnala a tutti i destinatari dati aziendali generici, che non devono essere inviati fuori dall'organizzazione. L'etichetta viene incorporata nelle intestazioni dei messaggi di posta elettronica, in modo che i servizi di posta elettronica possano esaminare questo valore e creare una voce di controllo o impedirne l'invio all'esterno dell'organizzazione.

![Piè di pagina e intestazioni del messaggio di posta elettronica di esempio che mostrano la classificazione di Azure Information Protection](./media/example-email-footerv2.png)

###### <a name="screenshot-from-the-azure-information-protection-client-classicfaqsmdwhats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client"></a>Screenshot dal [client di Azure Information Protection (classico)](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)

## <a name="how-data-is-protected"></a>Modalità di protezione dei dati

Per la protezione viene usata la tecnologia *Azure Rights Management* (spesso abbreviata in Azure RMS). Questa tecnologia è integrata in altri servizi e applicazioni cloud Microsoft, ad esempio Office 365 e Azure Active Directory. Il servizio può essere usato anche con proprie applicazioni line-of-business e soluzioni di protezione dei dati di fornitori software in locale o sul cloud.

Questa tecnologia di protezione usa criteri di crittografia, identità e autorizzazione. Analogamente alle etichette, la protezione applicata tramite Rights Management rimane associata ai documenti e ai messaggi di posta elettronica indipendentemente dalla posizione: all'interno o all'esterno dell'organizzazione, in reti, file server o applicazioni. Questa soluzione per la protezione delle informazioni favorisce il controllo dei propri dati, anche quando sono condivisi con altre persone.

È ad esempio possibile configurare un documento di report o un foglio di calcolo di previsione delle vendite in modo che possano accedervi solo le persone appartenenti all'organizzazione e per controllare se tale documento può essere modificato oppure se può essere impostato come file di sola lettura o non stampabile. È possibile configurare in modo analogo i messaggi di posta elettronica e anche impedire che vengano inoltrati o che venga usata l'opzione Rispondi a tutti. 

Queste impostazioni di protezione possono essere parte della configurazione di etichetta in modo che gli utenti classifichino e proteggano i documenti e i messaggi di posta elettronica semplicemente applicando l'etichetta. Le stesse impostazioni di protezione, tuttavia, possono essere usate dalle applicazioni e dai servizi che supportano la protezione ma non l'assegnazione di etichette. Per le applicazioni e i servizi di questo tipo, le impostazioni di protezione diventano disponibili come *modelli di Rights Management*.

### <a name="rights-management-templates"></a>Modelli di Rights Management

Non appena viene attivato il servizio Azure Rights Management, sono disponibili due modelli predefiniti che limitano l'accesso ai dati agli utenti all'interno dell'organizzazione. È possibile usare questi modelli per evitare immediatamente la perdita di dati dell'organizzazione. È anche possibile integrare questi modelli predefiniti configurando impostazioni di protezione personalizzate che applicano controlli più restrittivi.

Quando si crea un'etichetta per Azure Information Protection che include le impostazioni di protezione, viene automaticamente creato un modello di Rights Management corrispondente. Il modello può quindi essere usato anche con le applicazioni e i servizi che supportano Azure Rights Management.

Ad esempio, dall'interfaccia di amministrazione di Exchange è possibile configurare le regole del flusso di posta elettronica di Exchange Online per l'uso di questi modelli:

![Esempio di selezione di modelli per Exchange Online](./media/templates-exchangeonline-callouts.png)

Per altre informazioni sulla tecnologia di protezione Azure Rights Management, vedere [Informazioni su Microsoft Azure Rights Management](what-is-azure-rms.md)

## <a name="integration-with-end-user-workflows-for-documents-and-emails"></a>Integrazione con i flussi di lavoro dell'utente finale per i documenti e i messaggi di posta elettronica

Azure Information Protection si integra con i flussi di lavoro esistenti degli utenti finali quando viene installato il client di Azure Information Protection. Il client installa la barra di Information Protection nelle applicazioni di Office, come illustrato nella prima immagine che visualizza la barra in Word. La stessa barra di Information Protection viene aggiunta a Excel, PowerPoint e Outlook. Ad esempio:

![Esempio di barra di Azure Information Protection in Excel](./media/excelproplus-infoprotect-bar.png)

###### <a name="screenshot-from-the-azure-information-protection-unified-labeling-clientfaqsmdwhats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client"></a>Screenshot dal [client per l'etichettatura unificata Azure Information Protection](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client) 

La barra di Information Protection rende più semplice per gli utenti finali la selezione delle etichette per la classificazione corretta. Se necessario è anche possibile applicare automaticamente le etichette, per eliminare le possibilità di errori o per garantire la conformità con i criteri dell'organizzazione.

Per classificare e proteggere tipi di file e per supportare più file contemporaneamente, gli utenti possono fare clic con il pulsante destro del mouse sui file o su una cartella in Esplora file di Windows:

![Comando Classifica e proteggi nel menu di scelta rapida in Esplora file con Azure Information Protection](./media/right-click-classify-protect-folder.png)

Quando l'utente sceglie l'opzione di menu **Classifica e proteggi** in Esplora file, può quindi selezionare un'etichetta in modo analogo a quando si usa la barra di Information Protection nelle app desktop di Office. Se necessario, è anche possibile impostare autorizzazioni personalizzate.

Gli utenti esperti (e gli amministratori) potrebbero trovare più comodo usare i comandi di PowerShell per gestire e impostare in modo più efficiente la classificazione e la protezione per più file. I comandi di PowerShell per queste operazioni sono inclusi automaticamente nel client, ma è anche possibile installare il modulo di PowerShell separatamente.

Quando un documento viene protetto, utenti e amministratori possono usare un sito di rilevamento dei documenti per monitorare gli utenti che accedono ai documenti e gli orari di accesso. Se sospettano un uso improprio, possono anche revocare l'accesso ai documenti:

![Icona per la revoca dell'accesso nel sito di rilevamento dei documenti](./media/tracking-site-revoke-access-icon.png)

### <a name="additional-integration-for-email"></a>Integrazione aggiuntiva per la posta elettronica

Quando si usa Azure Information Protection con Exchange Online, si ottiene un vantaggio aggiuntivo: la possibilità di inviare messaggi di posta elettronica protetti a qualsiasi utente, con la certezza che possano essere letti in qualsiasi dispositivo.

Ad esempio, gli utenti hanno l'esigenza di inviare informazioni riservate a indirizzi di posta elettronica personali **Gmail**, **Hotmail** o **Microsoft** oppure a utenti che non hanno un account in Office 365 o Azure AD. Questi messaggi di posta elettronica deve essere crittografati sia nella posizione di archiviazione che in transito e devono essere letti solo dai destinatari originali.

Questo scenario richiede le [nuove funzionalità di Crittografia messaggi di Office 365](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801). Se i destinatari non possono aprire il messaggio di posta elettronica protetto nel client di posta elettronica nativo, possono usare un passcode monouso per leggere le informazioni riservate in un browser.

Un utente di Gmail, ad esempio, visualizza quanto segue in un messaggio di posta elettronica:

![Esperienza per i destinatari Gmail per Crittografia messaggi di Office 365 e Azure Information Protection](./media/ome-message.png)

Per gli utenti che inviano il messaggio di posta elettronica, il flusso di lavoro è uguale a quello previsto per l'invio di un messaggio di posta elettronica protetto a un utente nella propria organizzazione. Ad esempio, possono selezionare il pulsante **Non inoltrare** che il client di Azure Information Protection consente di aggiungere alla barra multifunzione di Outlook. Questa funzionalità Non inoltrare può anche essere integrata in un'etichetta selezionabile dagli utenti, in modo che il messaggio di posta elettronica venga classificato oltre che protetto. Ad esempio:

![Selezione di un'etichetta configurata per Non inoltrare](./media/recipients-only-label2.png)

###### <a name="screenshot-from-the-azure-information-protection-unified-labeling-clientfaqsmdwhats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client"></a>Screenshot dal [client per l'etichettatura unificata Azure Information Protection](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)

In alternativa, è possibile fornire automaticamente protezione agli utenti, usando regole del flusso di posta elettronica che applicano la protezione dei diritti. 

Quando si allegano documenti di Office a questi messaggi di posta elettronica, anche i documenti allegati vengono protetti automaticamente.

## <a name="classifying-and-protecting-existing-documents"></a>Classificazione e protezione dei documenti esistenti

Idealmente, i documenti e i messaggi di posta elettronica vengono etichettati al momento della creazione. Ma è probabile che esistano già molti documenti negli archivi dati e che si voglia classificare e proteggere anche questi documenti. Questi archivi dati potrebbero essere in locale o nel cloud.

Per gli archivi dati locali, usare lo scanner di Azure Information Protection per individuare, classificare e proteggere i documenti in cartelle locali, condivisioni di rete e siti e raccolte di SharePoint Server. Lo scanner viene eseguito come servizio in Windows Server. È possibile usare le stesse regole nei criteri per rilevare le informazioni sensibili e applicare etichette specifiche ai documenti. Oppure è possibile applicare un'etichetta predefinita a tutti i documenti in un archivio dati senza esaminare il contenuto dei file. È anche possibile usare lo scanner in modalità solo report, per facilitare l'individuazione di informazioni sensibili che potrebbero non essere note. 

Per altre informazioni sulla distribuzione e l'uso dello scanner, vedere [Distribuzione dello scanner di Azure Information Protection per classificare e proteggere automaticamente i file](deploy-aip-scanner.md).

Per gli archivi dati nel cloud, usare Microsoft Cloud App Security per applicare le etichette ai documenti in Box, SharePoint Online e OneDrive for Business. Per altre informazioni, vedere [Applicare automaticamente etichette di classificazione di Azure Information Protection](/cloud-app-security/use-case-information-protection) e [Integrazione di Azure Information Protection](/cloud-app-security/azip-integration).

## <a name="latest-labeling-updates-for-microsoft-365"></a>Ultimi aggiornamenti di etichettatura per Microsoft 365

Vedere le informazioni più recenti su come Azure Information Protection consente di individuare, classificare e proteggere e monitorare le informazioni riservate, ovunque si trovino:

> [!VIDEO https://www.youtube.com/embed/UI0p9xqMNfI]

## <a name="resources-for-azure-information-protection"></a>Risorse per Azure Information Protection

- Versione di valutazione gratuita: [Enterprise Mobility + Security E5](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)

- Opzioni e prezzi per la sottoscrizione: [Prezzi di Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)

- Scaricare il client: [Client di Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018)

- Scaricare un manuale dell'utente personalizzabile: [Azure Information Protection End User Adoption Guide](https://download.microsoft.com/download/7/1/2/712A280C-1C66-4EF9-8DC3-88EE43BEA3D4/Azure_Information_Protection_End_User_Adoption_Guide_EN_US.pdf) (Manuale d'uso di Azure Information Protection per utenti finali)

- Domande frequenti: [Domande frequenti su Azure Information Protection](faqs.md)

- Yammer: [Azure Information Protection](https://www.yammer.com/AskIPTeam)

- Novità nella documentazione: [Blog tecnico di Azure Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/bg-p/AzureInformationProtectionBlog/label-name/Docs)

Risorse aggiuntive: [Informazioni e supporto per Azure Information Protection](information-support.md)

### <a name="microsoft-ignite"></a>Microsoft Ignite

Microsoft Ignite 2018 a Orlando offre numerose sessioni per Azure Information Protection. Tutte le sessioni sono state registrate, pertanto se non è stato possibile seguirle, è comunque possibile guardare le sessioni. Di seguito sono riportate le prime cinque sessioni che è consigliabile seguire:

- [BRK2006 - Use Microsoft Information Protection (MIP) to help protect your sensitive data everywhere, throughout its lifecycle](https://youtu.be/gmHVF-1cLXA) (Usare Microsoft Information Protection (MIP) per la protezione dei dati sensibili ovunque si trovino, per l'intero ciclo di vita)
 
- [BRK3002 - Understanding how Microsoft Information Protection capabilities work together to protect sensitive information across devices, apps, and services](https://youtu.be/kL9Y7NGTyQQ) (Informazioni sull'interazione tra le funzionalità di Microsoft Information Protection per la protezione di informazioni sensibili tra dispositivi, app e servizi)

- [BRK3009 - Accelerate deployment and adoption of Microsoft Information Protection solutions](https://www.youtube.com/watch?v=JsCyIVyQJmE) (Accelerare la distribuzione e l'adozione di soluzioni basate su Microsoft Information Protection)

- [BRK3397 - Protect and control your sensitive emails with Office 365 Message Encryption](https://www.youtube.com/watch?v=Ld4b4pFua0g) (Proteggere e controllare i messaggi di posta elettronica sensibili con Office 365 Message Encryption)

- [THR2003 - Data discovery, Usage reporting and analytics for all your data with Microsoft Information Protection](https://www.youtube.com/watch?v=nzDIXd0XaeA) (Individuazione, report di utilizzo e analisi per tutti i dati utente con Microsoft Information Protection)

Per tutti gli annunci rilasciati in occasione di Ignite, vedere il post di blog [Announcing availability of information protection capabilities to help protect your sensitive data](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967) (Annuncio della disponibilità di funzionalità di protezione delle informazioni per la sicurezza dei dati sensibili).


## <a name="next-steps"></a>Passaggi successivi

Configurare e provare a usare Azure Information Protection con l'[esercitazione introduttiva](quickstart-viewpolicy.md) e le [esercitazioni](infoprotect-quick-start-tutorial.md). Se invece si è pronti a distribuire il servizio nella propria organizzazione, vedere le [guide procedurali](how-to-guides.md).
