---
title: "Che cos'è Azure Information Protection?"
description: Informazioni generali sul servizio Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/24/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: cd8a88e2-3555-4be2-9637-3cdee992f2c8
ms.openlocfilehash: 0eeb9a6cf8eb819c19a32dbcf76e4d0104c18b99
ms.sourcegitcommit: ae4cdee7211796182c47a11c1853232464673834
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2018
---
# <a name="what-is-azure-information-protection"></a>Che cos'è Azure Information Protection?

>*Si applica a: Azure Information Protection*

Azure Information Protection è una soluzione basata sul cloud che consente alle organizzazioni di classificare, etichettare e proteggere documenti e messaggi di posta elettronica. Queste operazioni possono essere eseguite automaticamente dagli amministratori, che definiscono regole e condizioni, manualmente dagli utenti oppure da entrambi, quando gli utenti ricevono raccomandazioni dagli amministratori. 

L'immagine seguente mostra un esempio di Azure Information Protection in azione. L'amministratore ha configurato regole per rilevare dati sensibili (in questo caso, informazioni su carte di credito). Quando un utente salva un documento di Word che contiene informazioni relative a carte di credito vede una descrizione comando personalizzata, che consiglia di applicare un'etichetta specifica configurata dall'amministratore. Questa etichetta classifica e facoltativamente, a seconda della configurazione, protegge il documento. 

![Esempio di classificazione consigliata per Azure Information Protection](../media/info-protect-recommend-calloutsv2.png)

Dopo che il contenuto è stato classificato (e facoltativamente protetto), è possibile rilevare e controllare come viene usato. È possibile analizzare i flussi di dati per ottenere informazioni sulle attività aziendali, rilevare comportamenti a rischio e adottare misure correttive, tenere traccia dell'accesso ai documenti, impedire la perdita o l'uso improprio di dati e così via.

## <a name="how-labels-apply-classification"></a>Modalità di classificazione in base alle etichette

Le etichette di Azure Information Protection consentono di applicare la classificazione a documenti e messaggi di posta elettronica. In questo modo, la classificazione è identificabile in qualsiasi momento, indipendentemente dalla posizione di archiviazione dei dati o dagli utenti con cui è condivisa. Le etichette includono contrassegni visivi, ad esempio un'intestazione, un piè di pagina o una filigrana. I metadati vengono aggiunti a file e intestazioni di messaggi di posta elettronica come testo non crittografato. Il testo non crittografato consente ad altri servizi, ad esempio le soluzioni di prevenzione della perdita di dati, di identificare la classificazione e adottare le misure appropriate. 

Ad esempio il messaggio di posta elettronica seguente è stato classificato come "General" (Generale). Questa etichetta viene aggiunta come piè di pagina al messaggio di posta elettronica. Il piè di pagina è un indicatore visivo che segnala a tutti i destinatari dati aziendali generici, che non devono essere inviati fuori dall'organizzazione. L'etichetta viene incorporata anche nelle intestazioni dei messaggi di posta elettronica, in modo che i servizi di posta elettronica possano esaminare questo valore e creare una voce di controllo o impedirne l'invio all'esterno dell'organizzazione.

![Piè di pagina e intestazioni del messaggio di posta elettronica di esempio che mostrano la classificazione di Azure Information Protection](../media/example-email-footerv2.png)


## <a name="how-data-is-protected"></a>Modalità di protezione dei dati

Per la protezione viene usata la tecnologia *Azure Rights Management* (spesso abbreviata in Azure RMS). Questa tecnologia è integrata in altri servizi e applicazioni cloud Microsoft, ad esempio Office 365 e Azure Active Directory. Il servizio può essere usato anche con proprie applicazioni line-of-business e soluzioni di protezione dei dati di fornitori software in locale o sul cloud.

Questa tecnologia di protezione usa criteri di crittografia, identità e autorizzazione. Analogamente alle etichette, la protezione applicata tramite Rights Management rimane associata ai documenti e ai messaggi di posta elettronica indipendentemente dalla posizione: all'interno o all'esterno dell'organizzazione, in reti, file server o applicazioni. Questa soluzione per la protezione delle informazioni favorisce il controllo dei propri dati, anche quando sono condivisi con altre persone.

È ad esempio possibile configurare un documento di report o un foglio di calcolo di previsione delle vendite in modo che possano accedervi solo le persone appartenenti all'organizzazione e per controllare se tale documento può essere modificato oppure se può essere impostato come file di sola lettura o non stampabile. È possibile configurare in modo analogo i messaggi di posta elettronica e anche impedire che vengano inoltrati o che venga usata l'opzione Rispondi a tutti. 

Queste impostazioni di protezione possono essere parte della configurazione di etichetta in modo che gli utenti classifichino e proteggano i documenti e i messaggi di posta elettronica semplicemente applicando l'etichetta. Le stesse impostazioni di protezione, tuttavia, possono essere usate dalle applicazioni e dai servizi che supportano la protezione ma non l'assegnazione di etichette. Per le applicazioni e i servizi di questo tipo, le impostazioni di protezione diventano disponibili come *modelli di Rights Management*.

### <a name="rights-management-templates"></a>Modelli di Rights Management

Non appena si attiva il servizio Azure Rights Management, sono disponibili due modelli predefiniti che limitano l'accesso ai dati agli utenti all'interno dell'organizzazione. È possibile usare questi modelli per evitare immediatamente la perdita di dati dell'organizzazione. È anche possibile integrare questi modelli predefiniti configurando impostazioni di protezione personalizzate che applicano controlli più restrittivi.

Quando si crea un'etichetta per Azure Information Protection che include le impostazioni di protezione, viene automaticamente creato un modello di Rights Management corrispondente. Il modello può quindi essere usato anche con le applicazioni e i servizi che supportano Azure Rights Management.

Ad esempio, dall'interfaccia di amministrazione di Exchange è possibile configurare le regole del flusso di posta elettronica di Exchange Online per l'uso di questi modelli:

![Esempio di selezione di modelli per Exchange Online](../media/templates-exchangeonline-callouts.png)

Per altre informazioni sulla tecnologia di protezione Azure Rights Management, vedere [Informazioni su Microsoft Azure Rights Management](what-is-azure-rms.md).

## <a name="integration-with-end-user-workflows-for-documents-and-emails"></a>Integrazione con i flussi di lavoro dell'utente finale per i documenti e i messaggi di posta elettronica

Azure Information Protection si integra con i flussi di lavoro esistenti degli utenti finali quando viene installato il client di Azure Information Protection. Il client installa la barra di Information Protection nelle applicazioni di Office, come illustrato nella prima immagine che visualizza la barra in Word. La stessa barra di Information Protection viene aggiunta a Excel, PowerPoint e Outlook. Ad esempio:

![Esempio di barra di Azure Information Protection in Excel](../media/excel2016-infoprotect-barv2.png)

La barra di Information Protection rende più semplice per gli utenti finali la selezione delle etichette per la classificazione corretta. Se necessario è anche possibile applicare automaticamente le etichette, per eliminare le possibilità di errori o per garantire la conformità con i criteri dell'organizzazione.

Per classificare e proteggere tipi di file e per supportare più file contemporaneamente, gli utenti possono fare clic con il pulsante destro del mouse sui file o su una cartella in Esplora file di Windows:

![Comando Classifica e proteggi nel menu di scelta rapida in Esplora file con Azure Information Protection](../media/right-click-classify-protect-folder.png)

Quando l'utente sceglie l'opzione di menu **Classifica e proteggi** in Esplora file, può quindi selezionare un'etichetta in modo analogo a quando si usa la barra di Information Protection nelle app desktop di Office. Se necessario, è anche possibile impostare autorizzazioni personalizzate.

Gli utenti esperti (e gli amministratori) potrebbero trovare più comodo usare i comandi di PowerShell per gestire e impostare in modo più efficiente la classificazione e la protezione per più file. I comandi di PowerShell per queste operazioni sono inclusi automaticamente nel client, ma è anche possibile installare il modulo di PowerShell separatamente.

Quando un documento viene protetto, utenti e amministratori possono usare un sito di rilevamento dei documenti per monitorare gli utenti che accedono ai documenti e gli orari di accesso. Se sospettano un uso improprio, possono anche revocare l'accesso ai documenti:

![Icona per la revoca dell'accesso nel sito di rilevamento dei documenti](../media/tracking-site-revoke-access-icon.png)

### <a name="additional-integration-for-email"></a>Integrazione aggiuntiva per la posta elettronica

Usando Azure Information Protection con Exchange Online si ottiene un ulteriore vantaggio, ovvero la possibilità di inviare messaggi di posta elettronica protetti a qualsiasi utente, con la certezza che possano essere letti su qualsiasi dispositivo.

Ad esempio, gli utenti hanno l'esigenza di inviare informazioni riservate ad account di posta elettronica personali **Gmail**, **Hotmail** o **Microsoft** oppure a utenti che non hanno un account per Office 365 o in Azure AD. Questi messaggi di posta elettronica deve essere crittografati sia nella posizione di archiviazione che in transito e devono essere letti solo dai destinatari originali.

Questo scenario richiede le [nuove funzionalità di Crittografia messaggi di Office 365](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801). Se i destinatari non possono aprire il messaggio di posta elettronica protetto nel client di posta elettronica nativo, possono usare un passcode monouso per leggere le informazioni riservate in un browser.

Un utente di Gmail, ad esempio, visualizza quanto segue in un messaggio di posta elettronica:

![Esperienza per i destinatari Gmail per Crittografia messaggi di Office 365 e Azure Information Protection](../media/ome-message.png)

Per gli utenti che inviano il messaggio di posta elettronica, il flusso di lavoro è uguale a quello previsto per l'invio di un messaggio di posta elettronica protetto a un utente nella propria organizzazione. Ad esempio, possono selezionare il pulsante **Non inoltrare** che il client di Azure Information Protection consente di aggiungere alla barra multifunzione di Outlook. Questa funzionalità Non inoltre può anche essere integrata in una etichetta selezionabile dagli utenti, in modo che il messaggio di posta elettronica venga classificato oltre che protetto:

![Selezione di un'etichetta configurata per Non inoltrare](../media/recipients-only-label.png)

In alternativa, è possibile fornire automaticamente protezione agli utenti, usando regole del flusso di posta elettronica che applicano la protezione dei diritti. 

Quando si allegano documenti di Office a questi messaggi di posta elettronica, anche i documenti allegati vengono protetti automaticamente.

## <a name="resources-for-azure-information-protection"></a>Risorse per Azure Information Protection

- Versione di valutazione gratuita: [Enterprise Mobility + Security E5](https://portal.office.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)

- Download del client: [Azure Information Protection client](https://www.microsoft.com/en-us/download/details.aspx?id=53018) (Client di Azure Information Protection)

- Download di un manuale dell'utente personalizzabile: [Azure Information Protection End User Adoption Guide](https://download.microsoft.com/download/7/1/2/712A280C-1C66-4EF9-8DC3-88EE43BEA3D4/Azure_Information_Protection_End_User_Adoption_Guide_EN_US.pdf) (Manuale d'uso di Azure Information Protection per utenti finali)

- Domande frequenti: [Domande frequenti su Azure Information Protection](../get-started/faqs.md)

- Yammer: [Azure Information Protection](https://www.yammer.com/AskIPTeam)


**Microsoft Ignite 2017** offre anche numerose sessioni per Azure Information Protection disponibili su richiesta. Per un riepilogo degli annunci effettuati durante la conferenza, vedere il post di blog sulle [novità di Azure Information Protection in Ignite 2017](https://blogs.technet.microsoft.com/enterprisemobility/2017/09/27/whats-new-in-azure-information-protection-ignite-2017/). 

È possibile [cercare](https://myignite.microsoft.com/videos?q=%2522azure%2520information%2520protection%2522) le sessioni contrassegnate per Azure Information Protection nel sito Web dedicato a Ignite. Tuttavia, è consigliabile iniziare con le sessioni seguenti:

- [Protecting complete data lifecycle using Microsoft information protection capabilities](https://myignite.microsoft.com/videos/55397) (Protezione del ciclo di vita completo dei dati tramite le funzionalità di protezione delle informazioni Microsoft)

- [Accelerate Azure information protection deployment and adoption](https://myignite.microsoft.com/videos/53454) (Velocizzare l'adozione e la distribuzione di Azure Information Protection)

- [Discover what’s new in Azure Information Protection and learn about the roadmap and strategy](https://myignite.microsoft.com/videos/53453) (Novità in Azure Information Protection e informazioni su guida di orientamento e strategia)

- [Encryption key management strategies for compliance](https://myignite.microsoft.com/videos/53455) (Strategie di gestione delle chiavi di crittografia per la conformità)

- [Protect and control your sensitive emails with new Office 365 Message Encryption capabilities](https://myignite.microsoft.com/videos/53230) (Proteggere e controllare i messaggi di posta elettronica riservati con le nuove funzionalità di Office 365 Message Encryption)


## <a name="next-steps"></a>Passaggi successivi

Leggere il post di blog [Azure Information Protection: Ready, set, protect!](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/) (Azure Information Protection: una soluzione immediata ed efficiente per la protezione)

Configurare e provare a usare Azure Information Protection in cinque passaggi con l'[esercitazione introduttiva](../get-started/infoprotect-quick-start-tutorial.md). Oppure se si vuole distribuire il servizio nella propria organizzazione, vedere la [Guida di orientamento per la distribuzione di Azure Information Protection](../plan-design/deployment-roadmap.md).

Azure Information Protection è noto anche con un altro nome? Vedere [l'elenco delle denominazioni alternative del servizio](azure-rms-aka.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]