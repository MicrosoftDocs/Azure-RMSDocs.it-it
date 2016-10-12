---
title: Guida dell'utente dell'applicazione Rights Management sharing | Azure Information Protection
description: L'applicazione Microsoft Rights Management (RMS) sharing per Windows consente di proteggere le immagini e i documenti importanti da persone che non devono essere visualizzati, anche se vengono spediti per posta elettronica o salvati in un altro dispositivo.
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: eaf6d02c-aa36-4915-856e-49bb71ab1484
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: aac3c6c7b5167d729d9ac89d9ae71c50dd1b6a10
ms.openlocfilehash: c89c82350768222da44c631dd88c97bcdb0db4d5


---

# Guida dell'utente dell'applicazione Rights Management sharing

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 7 con SP1, Windows 8, Windows 8.1*

L'applicazione Microsoft Rights Management (RMS) sharing per Windows consente di proteggere le immagini e i documenti importanti da persone che non devono essere visualizzarli, anche se vengono inviati tramite posta elettronica o salvati in un altro dispositivo. È anche possibile eseguire questa applicazione per aprire e usare i file protetti da altri utenti tramite la stessa tecnologia di protezione Rights Management.

È sufficiente avere un computer che esegua almeno Windows 7 con Service Pack 1. Quindi [scaricare e installare](http://go.microsoft.com/fwlink/?LinkId=303970) questa applicazione gratuita da Microsoft.

In caso di domande per le quali non si trova risposta in questa Guida, vedere [Domande frequenti sull'applicazione Microsoft Rights Management sharing per Windows](http://go.microsoft.com/fwlink/?LinkId=303971). Questa pagina include anche alcune informazioni sulla risoluzione dei problemi, nel caso se ne verificassero.

## Esempi per l'uso dell'applicazione RMS sharing
Di seguito sono riportati solo alcuni esempi di come è possibile usare l'applicazione RMS sharing per proteggere i file.

|Si desidera...|Come effettuare questa operazione|
|----------------|------------------|
|**… condividere in modo sicuro le informazioni finanziarie con utenti attendibili che lavorano per un'altra organizzazione**<br /><br />Si lavora con una società partner e si desidera inviare tramite posta elettronica un foglio di calcolo di Excel contenente dati relativi alle vendite previste. Si desidera che siano in grado di visualizzare le cifre ma non di modificarle.|Si utilizza il pulsante **Condivisione protetta** sulla barra multifunzione di Excel, digitare gli indirizzi di posta elettronica delle due persone con cui si lavora nella società partner **Visualizzatore-Solo visualizzazione**, e fare clic su **Invio**.<br /><br />Quando il messaggio di posta elettronica arriva alla società partner, solo i destinatari nel messaggio di posta elettronica è possono visualizzare il foglio di calcolo e non possono essere salvarlo, modificarlo, stamparlo o inoltrarlo.<br /><br />Procedura dettagliata: [Proteggere un file condiviso tramite posta elettronica usando l'applicazione Rights Management sharing](sharing-app-protect-by-email.md).|
|**… invia in modo sicuro un documento per posta elettronica a qualcuno che utilizza un dispositivo iOS**<br /><br />Si desidera inviare tramite posta elettronica un documento di Word estremamente riservato a un collega che di solito controlla la posta elettronica da un dispositivo iOS.|Usare Esplora file per fare clic con il pulsante destro del mouse sul file, selezionare **Condividi file protetto** e inviare al collega il file come allegato.<br /><br />Il destinatario riceve il messaggio di posta elettronica sul dispositivo iOS. Non avendo Office per Ipad e Iphone, fa clic sul collegamento nel messaggio di posta elettronica che indica come scaricare l'applicazione di condivisione, installa la versione per dispositivi iOS e poi visualizza il documento¹.<br /><br />Procedura dettagliata: [Proteggere un file condiviso tramite posta elettronica usando l'applicazione Rights Management sharing](sharing-app-protect-by-email.md).|
|**… verificare chi ha aperto la cartella dei documenti protetti e quando, e revocare l'accesso se necessario**<br /><br />È stato condiviso in modo protetto un documento di progettazione riservato con fornitori potenziali e si desidera vedere chi vi ha avuto accesso, quando e da dove. Poi, quando a uno dei fornitori viene affidato il lavoro, si desidera revocare l'accesso al documento originale in modo che le persone che con cui è stato condiviso non possano più leggerlo.|Dopo aver condiviso un documento tramite posta elettronica, si passa al [sito di rilevamento dei documenti](http://go.microsoft.com/fwlink/?LinkId=529562) per controllare chi ha accesso al documento e quando. Quando è necessario interrompere la condivisione, selezionare l'opzione per revocare l'accesso.<br /><br />Procedura dettagliata: [Tenere traccia dei documenti e revocarli quando si usa l'applicazione di RMS sharing](sharing-app-track-revoke.md).|
|**… leggere un allegato ricevuto in un messaggio di posta elettronica che contiene un allegato con un file condiviso in modo protetto, ma non è possibile leggerlo in quanto l’azienda a cui si appartiene non utilizza Rights Management**<br /><br />Il mittente del messaggio di posta elettronica è qualcuno considerato attendibile perché ci si è già lavorato in passato e si ritiene che stia inviando informazioni su una potenziale nuova opportunità di business.|Seguire le istruzioni nel messaggio di posta elettronica e fare clic sul collegamento per iscriversi a Microsoft Rights Management. Microsoft verifica che l'organizzazione non disponga di una sottoscrizione che include Azure Information Protection e invia un messaggio di posta elettronica per completare il processo di iscrizione gratuita. A questo punto, è possibile accedere con il nuovo account. Si fa clic sul secondo collegamento nel messaggio di posta elettronica per installare l'applicazione Rights Management sharing e si può quindi aprire l'allegato di posta elettronica per leggere le informazioni sulla nuova opportunità di business.<br /><br />Procedura dettagliata: [Visualizzare e usare i file che sono stati protetti da Rights Management](sharing-app-view-use-files.md).|
|**… proteggere i file di informazioni aziendali riservate sul computer portatile in modo che non vi possano accedere utenti esterni all'azienda**<br /><br />Si viaggia molto e si utilizza il computer portatile per accedere e aggiornare i file in una cartella che deve essere protetta da accessi non autorizzati.|Si ha l'applicazione RMS sharing installata in un computer portatile. Si utilizza Esplora File per proteggere i file utilizzando un modello, che consente di proteggere rapidamente i file. Se il computer portatile viene rubato, si è tranquilli del fatto che nessuno esterno all'azienda può accedere a questi documenti.<br /><br />Procedura dettagliata: [Proteggere un file in un dispositivo &#40;protezione sul posto&#41; tramite l'applicazione Rights Management sharing](sharing-app-protect-in-place.md).|
Rendering PDF con tecnologia Foxit ¹. Copyright © 2003-2014, Foxit Corporation.

## Come procedere
> [!NOTE]
> Per altre informazioni tecniche, ad esempio sui [tipi di file supportati](sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions) e su [come installare questa applicazione in una rete aziendale](sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application), vedere la [Guida dell'amministratore dell'applicazione Rights Management sharing](sharing-app-admin-guide.md).

- [Scaricare e installare l'applicazione di condivisione](install-sharing-app.md)

- [Proteggere un file in un dispositivo (protezione sul posto)](sharing-app-protect-in-place.md)

- [Proteggere un file che si condivide tramite posta elettronica](sharing-app-protect-by-email.md)

- [Modificare le autorizzazioni per i file protetti](sharing-app-reprotect-files.md)

- [Tenere traccia dei documenti e revocarli](sharing-app-track-revoke.md)

- [Visualizzare e utilizzare i file che sono stati protetti](sharing-app-view-use-files.md)

- [Rimuovere la protezione da un file](sharing-app-remove-protection.md)

- [Utilizzare tasti di scelta rapida](sharing-app-keyboard-shortcuts.md)

- [Specificare le impostazioni nella finestra di dialogo](sharing-app-dialog-box.md)






<!--HONumber=Sep16_HO4-->


