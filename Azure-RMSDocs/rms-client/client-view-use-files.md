---
title: Visualizzare e usare i documenti protetti con il client AIP
description: Istruzioni per visualizzare e usare un documento protetto che richiede l'installazione del client Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/30/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ce1c7d4c-b5ff-4672-8b9a-a72129bac992
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: d8fd80d6ff97118cd37dd62e293768b145c98595
ms.sourcegitcommit: 1c3ebf4ad64b55db4fec3ad007fca71ab7d38c02
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2017
---
# <a name="view-and-use-files-that-have-been-protected-by-rights-management"></a>Visualizzare e usare i file che sono stati protetti da Rights Management

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*

Per visualizzare un documento protetto, spesso è sufficiente aprirlo. Ad esempio, è possibile fare doppio clic su un allegato in un messaggio di posta elettronica o fare doppio clic su un file in Esplora file oppure è possibile fare clic su un collegamento a un file.

Se i file non si aprono immediatamente, il **visualizzatore Azure Information Protection** potrebbe essere in grado di aprirli. Il visualizzatore è in grado di aprire file di testo protetti, file di immagine protetti, file PDF protetti e tutti i file con estensione **PFILE**.

Viene automaticamente installato con il client Azure Information Protection oppure può essere installato separatamente. Il client e il visualizzatore possono essere entrambi installati dalla pagina [Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970) del sito Web Microsoft. Per altre informazioni sull'installazione del client, vedere [Scaricare e installare il client Azure Information Protection](install-client-app.md).

> [!NOTE]
> Benché l'installazione del client fornisca più funzionalità, richiede autorizzazioni di amministratore locale e la funzionalità completa richiede un servizio corrispondente per l'organizzazione:
> 
> - Azure Information Protection
> 
> - Azure Rights Management
> 
> - Active Directory Rights Management Services 
> 
> Installare il visualizzatore se si è ricevuto un documento protetto da un utente di un'altra organizzazione o se non si possiedono autorizzazioni di amministratore locale per il PC.

Per essere in grado di aprire un documento protetto, l'applicazione deve essere "abilitata per RMS". Le applicazioni Office e il visualizzatore Azure Information Protection sono esempi di applicazioni abilitate per RMS. Per visualizzare un elenco di applicazioni per tipo e i dispositivi supportati, vedere la [tabella delle applicazioni abilitate per RMS](../get-started/requirements-applications.md#rms-enlightened-applications).  
## <a name="messagerpmsg-as-an-email-attachment"></a>Message.rpmsg come allegato di posta elettronica

Se **message.rpmsg** appare come file allegato in un messaggio di posta elettronica, non si tratta di un documento protetto, ma di un messaggio di posta elettronica protetto visualizzato come allegato. Non è possibile usare il visualizzatore Azure Information Protection per Windows per visualizzare questo messaggio di posta elettronica protetto in un computer Windows. È invece necessaria un'applicazione di posta elettronica per Windows che supporti la protezione di Rights Management, ad esempio Office Outlook. Oppure si può usare Outlook sul Web.

Se tuttavia si usa un dispositivo iOS o Android, è possibile usare l'app di Azure Information Protection per aprire i messaggi di posta elettronica protetti. L'app per questi dispositivi mobili può essere scaricata dalla pagina [Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970) del sito Web Microsoft.

## <a name="prompts-for-authentication"></a>Richieste di autorizzazione

Prima di poter visualizzare il file protetto, il servizio Rights Management usato per proteggere il file deve prima di tutto verificare che siano presenti le autorizzazioni necessarie per la visualizzazione del file. A questo scopo, il servizio controlla il nome utente e la password. In alcuni casi, questo potrebbe essere memorizzato nella cache e non verrà visualizzato un messaggio che richiede l'immissione delle credenziali. In altri casi, verrà richiesto di fornire le credenziali.

Se l'organizzazione non ha un account basato sul cloud (per Office 365 o Azure) e non usa una versione locale equivalente (AD RMS), è possibile richiedere un account gratuito che accetterà le credenziali in modo da permettere l'apertura dei file protetti tramite Rights Management:

-   Per richiedere questo account, fare clic sul collegamento per richiedere [RMS per utenti singoli](http://go.microsoft.com/fwlink/?LinkId=309469).
    
    Quando si effettua l'iscrizione, utilizzare l'indirizzo di posta elettronica della società anziché un indirizzo di posta elettronica personale. Se si esegue l'iscrizione perché è stato inviato un allegato protetto tramite posta elettronica, utilizzare lo stesso indirizzo di posta elettronica utilizzato per inviare il messaggio di posta elettronica.
    
-   Per ulteriori informazioni, vedere [RMS per utenti singoli e Azure Rights Management](../understand-explore/rms-for-individuals.md).

## <a name="to-view-and-use-a-protected-document"></a>Per visualizzare e usare un documento protetto

1. Aprire il file protetto (ad esempio, facendo doppio clic sul file o sull'allegato oppure facendo clic sul collegamento al file). Se viene chiesto di selezionare un'app, selezionare l'app **Visualizzatore Azure Information Protection**. 

2. Se viene visualizzata una pagina di **accesso** o **iscrizione**: fare clic su **Accedi** e immettere le credenziali. Se il file protetto è stato inviato come allegato, assicurarsi di specificare lo stesso indirizzo di posta elettronica usato per l'invio del file.
    
    Se l'account specificato non viene accettato, vedere la sezione [Richieste di autorizzazione](#prompts-for-authentication) in questa pagina. Iscriversi per un account gratuito e tornare a queste istruzioni.

3. Una versione di sola lettura del file viene aperta nel **visualizzatore Azure Information Protection**. Se si hanno autorizzazioni sufficienti, è possibile stampare il file e modificarlo. 

    È possibile controllare le autorizzazioni per il file facendo clic su **Autorizzazioni**. Nella finestra di dialogo **Autorizzazioni** è possibile anche identificare il proprietario del file da contattare se si vuole richiedere una nuova versione del file con autorizzazioni aggiuntive.
    
    Per altre informazioni sulle autorizzazioni e sui diritti di utilizzo di ciascuna autorizzazione, vedere [Diritti inclusi nei livelli di autorizzazioni](../deploy-use/configure-usage-rights.md#rights-included-in-permissions-levels).

4. Per modificare il file, fare clic su **Salva con nome**, che consente di salvare il file senza protezione con l'estensione del nome file originale. È quindi possibile modificare il file usando l'applicazione associata al tipo di file.

5. Per aprire altri file protetti, è possibile visualizzarli direttamente nel visualizzatore usando l'opzione **Apri**. Il file selezionato sostituisce il file originale nel visualizzatore. 

> [!TIP]
> Se il file protetto non si apre, usare l'opzione **Guida e commenti** di Azure Information Protection e selezionare **Esegui diagnostica**. Al termine dei test, è possibile reimpostare il client, che potrebbe risolvere il problema.


## <a name="other-instructions"></a>Altre istruzioni
Ulteriori procedure nella Guida per l'utente di Azure Information Protection:

-   [Per saperne di più](client-user-guide.md#what-do-you-want-to-do)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]