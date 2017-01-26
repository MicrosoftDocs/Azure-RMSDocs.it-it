---
title: Visualizzare e usare i file che sono stati protetti da Rights Management | Azure Information Protection
description: Istruzioni per visualizzare e usare un file protetto che richiede l&quot;installazione del client di Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/07/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ce1c7d4c-b5ff-4672-8b9a-a72129bac992
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 364891123720daaacacbea1b382b7d101d75cd1a


---

# <a name="view-and-use-files-that-have-been-protected-by-rights-management"></a>Visualizzare e usare i file che sono stati protetti da Rights Management

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*

**[Questa versione del client è in anteprima e soggetta a modifiche].**

Quando il [client di Azure Information Protection viene installato nel computer in uso](install-client-app.md), è possibile visualizzare un file protetto aprendo semplicemente il file. Ad esempio, è possibile fare doppio clic su un allegato in un messaggio di posta elettronica o fare doppio clic su un file in Esplora file oppure è possibile fare clic su un collegamento a un file.

> [!NOTE]
> Per consentire a un utente di visualizzare il file protetto, il servizio Rights Management deve prima verificare che sia autorizzato e a questo scopo controlla il nome utente e la password. In alcuni casi, questo potrebbe essere memorizzato nella cache e non verrà visualizzato un messaggio che richiede l'immissione delle credenziali. In altri casi, verrà richiesto di fornire le credenziali.
>
> Se l'organizzazione non ha un account basato su cloud (per Office 365 o Azure) e non usa AD RMS, è possibile richiedere un account gratuito che accetterà le credenziali in modo che sia possibile aprire i file protetti tramite Rights Management:
>
> -   Per richiedere questo account, fare clic sul collegamento per richiedere [RMS per utenti singoli](http://go.microsoft.com/fwlink/?LinkId=309469).
>
>     Quando si effettua l'iscrizione, utilizzare l'indirizzo di posta elettronica della società anziché un indirizzo di posta elettronica personale. Se si esegue l'iscrizione perché è stato inviato un allegato protetto tramite posta elettronica, utilizzare lo stesso indirizzo di posta elettronica utilizzato per inviare il messaggio di posta elettronica.
> -   Per ulteriori informazioni, vedere [RMS per utenti singoli e Azure Rights Management](../understand-explore/rms-for-individuals.md).

## <a name="to-view-and-use-a-protected-file"></a>Visualizzare e usare un file protetto

1. Aprire il file protetto (ad esempio, facendo doppio clic sul file o sull'allegato oppure facendo clic sul collegamento al file). Se viene chiesto di selezionare un'app, selezionare l'app **visualizzatore Azure Information Protection (anteprima)**. 

2. Se viene visualizzata una pagina di **accesso** o **iscrizione**: fare clic su **Accedi** e immettere le credenziali. Se il file protetto è stato inviato come allegato, assicurarsi di specificare lo stesso indirizzo di posta elettronica usato per l'invio del file.
    
    Se l'account specificato non viene accettato, vedere la nota nella parte superiore della pagina. Iscriversi per un account gratuito e tornare a queste istruzioni.

3. Una versione di sola lettura del file viene aperta nel **visualizzatore Azure Information Protection**. Se si hanno autorizzazioni sufficienti, è possibile stampare il file e modificarlo. 

    È possibile controllare le autorizzazioni per il file facendo clic su **Autorizzazioni**. Nella finestra di dialogo **Autorizzazioni** è possibile anche identificare il proprietario del file da contattare se si vuole richiedere una nuova versione del file con autorizzazioni aggiuntive.
    
    Per altre informazioni sulle autorizzazioni e sui diritti di utilizzo di ciascuna autorizzazione, vedere [Diritti inclusi nei livelli di autorizzazioni](../deploy-use/configure-usage-rights.md#rights-included-in-permissions-levels).

4. Per modificare il file, fare clic su **Salva con nome**, che consente di salvare il file senza protezione con l'estensione del nome file originale. È quindi possibile modificare il file usando l'applicazione associata al tipo di file.

5. Per aprire altri file protetti, è possibile visualizzarli direttamente nel visualizzatore usando l'opzione **Apri**. Il file selezionato sostituisce il file originale nel visualizzatore. 

> [!TIP]
> Se il file protetto non si apre, scaricare e usare lo [strumento RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437). Seguire le istruzioni visualizzate nello strumento per determinare se nel computer si sono verificati problemi che possono impedire l'apertura di un documento protetto.


## <a name="other-instructions"></a>Altre istruzioni
Per le istruzioni d'uso, vedere le sezioni seguenti della Guida per l'utente di Azure Information Protection:

-   [Per saperne di più](client-user-guide.md#what-do-you-want-to-do)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO4-->


