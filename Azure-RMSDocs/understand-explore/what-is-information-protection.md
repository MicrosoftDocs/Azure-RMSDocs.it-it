---
title: "Che cos'è Azure Information Protection? | Azure Information Protection"
description: Informazioni generali sul servizio Azure Information Protection.
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: cd8a88e2-3555-4be2-9637-3cdee992f2c8
translationtype: Human Translation
ms.sourcegitcommit: 590f12e0c6c6122a6bc0a559940870c18f0e2d39
ms.openlocfilehash: 350a3cb877674208b4c560bb841135904aee1136


---

# Che cos'è Azure Information Protection?

>*Si applica a: Azure Information Protection*

Azure Information Protection è una soluzione basata sul cloud che consente alle organizzazioni di classificare, etichettare e proteggere documenti e messaggi di posta elettronica. Queste operazioni possono essere eseguite automaticamente dagli amministratori, che definiscono regole e condizioni, manualmente dagli utenti oppure da entrambi, quando gli utenti ricevono raccomandazioni dagli amministratori. 

L'immagine seguente mostra un esempio di Azure Information Protection in azione. L'amministratore ha configurato regole per rilevare dati sensibili (in questo caso, informazioni su carte di credito). Quando un utente salva un documento di Word che contiene informazioni relative a carte di credito, vede una descrizione comando personalizzata in cui si raccomanda di applicare un'etichetta specifica configurata dall'amministratore, che classifica e, facoltativamente, protegge il documento. 

![Esempio di classificazione consigliata per Azure Information Protection](../media/info-protect-recommend-callouts.png)

Dopo che il contenuto è stato classificato (e facoltativamente protetto), è possibile rilevare e controllare come viene usato. È possibile analizzare i flussi di dati per ottenere informazioni sulle attività aziendali, rilevare comportamenti a rischio e adottare misure correttive, tenere traccia dell'accesso ai documenti, impedire la perdita o l'uso improprio di dati e così via.

## Modalità di classificazione in base alle etichette

Per applicare la classificazione a documenti e messaggi di posta elettronica si usano le etichette di Azure Information Protection. In questo modo, la classificazione è identificabile in qualsiasi momento, indipendentemente dalla posizione di archiviazione dei dati o dagli utenti con cui è condivisa. Le etichette persistenti includono contrassegni visivi, ad esempio un'intestazione, un piè di pagina o una filigrana. A file e intestazioni di messaggi di posta elettronica in testo non crittografato vengono aggiunti metadati in modo che altri servizi, ad esempio soluzioni di prevenzione della perdita di dati, possano identificare la classificazione e agire in modo appropriato. 

Ad esempio, il messaggio di posta elettronica seguente è stato classificato come "Internal" (Interno). Questa etichetta viene aggiunta come piè di pagina al messaggio di posta elettronica, come indicatore visivo per tutti i destinatari allo scopo di segnalare che il messaggio è destinato a uso interno e non deve essere inviato all'esterno dell'organizzazione. Questa etichetta viene inoltre incorporata nelle intestazioni dei messaggi di posta elettronica in modo che i servizi di posta elettronica possano esaminare questo valore e creare una voce di controllo o impedirne l'invio all'esterno dell'organizzazione.

![Piè di pagina e intestazioni del messaggio di posta elettronica di esempio che mostrano la classificazione di Azure Information Protection](../media/example-email-footer-header.png)


## Modalità di protezione dei dati

Per la protezione viene usata la tecnologia *Azure Rights Management* (spesso abbreviata in Azure RMS). Questa tecnologia è integrata in altri servizi e applicazioni cloud Microsoft, ad esempio Office 365 e Azure Active Directory. Il servizio può essere usato anche con proprie applicazioni line-of-business e soluzioni di protezione dei dati di fornitori software in locale o sul cloud.

Questa tecnologia di protezione usa criteri di crittografia, identità e autorizzazione. Analogamente alle etichette persistenti, la protezione applicata tramite Rights Management rimane associata ai documenti e ai messaggi di posta elettronica indipendentemente dalla posizione: all'interno o all'esterno dell'organizzazione, in reti, file server o applicazioni. Questa soluzione per la protezione delle informazioni favorisce il controllo dei propri dati, anche quando sono condivisi con altre persone.

È ad esempio possibile configurare un documento di report o un foglio di calcolo di previsione delle vendite in modo che possano accedervi solo le persone appartenenti all'organizzazione e per controllare se tale documento può essere modificato oppure se può essere impostato come file di sola lettura o non stampabile. È possibile configurare i messaggi e-mail in modo analogo e, inoltre, impedire che vengano inoltrati o che venga usata l'opzione Rispondi a tutti. Queste attività di protezione possono essere semplificate tramite *modelli di Rights Management*.

### Modelli di Rights Management

Non appena si attiva il servizio Azure Rights Management, vengono creati due modelli predefiniti che limitano l'accesso ai dati agli utenti all'interno dell'organizzazione. È possibile usare questi modelli per evitare immediatamente la perdita di dati dell'organizzazione. È inoltre possibile integrare questi modelli predefiniti configurando modelli personalizzati che applicano controlli più restrittivi.

Questi modelli possono far parte della configurazione di un'etichetta, in modo che i dati vengano classificati e protetti automaticamente per effetto dell'applicazione di un'etichetta specifica a un documento (o a un messaggio di posta elettronica). I modelli possono inoltre essere selezionati da utenti o amministratori in prodotti e servizi che supportano la tecnologia Azure Rights Management.

Questo esempio mostra come è possibile selezionare un modello per un'etichetta quando si configurano i criteri di Azure Information Protection dal portale di Azure:

![Esempio di selezione di modelli nel portale di Azure](../media/templates-infoprotection-callouts.png)

Gli stessi modelli possono essere selezionati dall'interfaccia di amministrazione di Exchange per configurare regole del flusso di posta elettronica di Exchange Online, che supportano la tecnologia Azure Rights Management:

![Esempio di selezione di modelli per Exchange Online](../media/templates-exchangeonline-callouts.png)

Per altre informazioni sulla tecnologia di protezione Azure Rights Management, vedere [Informazioni su Microsoft Azure Rights Management](what-is-azure-rms.md).

## Integrazione con i flussi di lavoro degli utenti finali

Azure Information Protection si integra con i flussi di lavoro esistenti degli utenti finali quando viene installato il client di Azure Information Protection. Il client installa la barra di Information Protection nelle applicazioni di Office, come illustrato nella prima immagine. La stessa barra viene aggiunta a Excel, PowerPoint e Outlook. Ad esempio:

![Esempio di barra di Azure Information Protection in Excel](../media/excel2013-infoprotect-bar2.png)

Questa barra di Information Protection consente agli utenti finali di selezionare con facilità le etichette per la classificazione corretta, e quando necessario, le etichette possono anche proteggere automaticamente i documenti e i messaggi di posta elettronica.

Quando gli utenti condividono i documenti protetti tramite posta elettronica, possono usare un sito di rilevamento per monitorare gli utenti che accedono ai documenti e gli orari di accesso. Se sospettano un uso improprio, possono anche revocare l'accesso ai documenti.


## Risorse per Azure Information Protection

- Annuncio: [Azure Information Protection is now Generally Available](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/04/azure-information-protection-is-now-generally-available/) (Azure Information Protection è ora disponibile a livello generale)

- Versione di valutazione gratuita: [Enterprise Mobility + Security E5](https://portal.office.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)

- Download del client: [Azure Information Protection client](https://www.microsoft.com/en-us/download/details.aspx?id=53018) (Client di Azure Information Protection)

- Domande frequenti: [Domande frequenti su Azure Information Protection](../get-started/faqs.md)

- Yammer: [Azure Information Protection](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)

- Presentazione video:

    <iframe width="560" height="315" src="https://www.youtube.com/embed/N9Ip0m6d3G0" frameborder="0" allowfullscreen></iframe>


## Passaggi successivi

Configurare e provare a usare Azure Information Protection in cinque passaggi con [Esercitazione introduttiva di Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md).

Azure Information Protection o Azure Rights Management è noto anche con altri nomi. Vedere [l'elenco delle denominazioni alternative](azure-rms-aka.md).


<!--HONumber=Oct16_HO1-->

