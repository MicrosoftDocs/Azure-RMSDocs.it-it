---
title: Proteggere un file condiviso tramite posta elettronica usando l'applicazione Rights Management sharing | Azure RMS
description: Istruzioni su come condividere in modo sicuro un documento tramite posta elettronica.
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4c1cd1d3-78dd-4f90-8b37-dcc9205a6736
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 035c9eb6cb630cafd5bd7fc7e2371340043ddc5e
ms.openlocfilehash: ff5dd6afaa454c20f35c237e94947dcec9e737f6


---

# Proteggere un file che si condivide tramite e-mail utilizzando l'applicazione di condivisione Rights Management

>*Si applica a: Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 con SP1, Windows 8, Windows 8.1*

Quando si protegge un file che si condivide tramite e-mail viene creata una nuova versione del file originale. Il file originale rimane non protetto mentre la nuova versione viene protetta e automaticamente allegata a un messaggio e-mail che quindi può essere inviato.

In alcuni casi (per i file creati da Microsoft Word, Excel e PowerPoint), l'applicazione di condivisione RMS crea due versioni del file che viene allegato al messaggio e-mail. La seconda versione del file ha l’estensione di file **.ppdf** ed è una copia shadow in formato PDF del file. Questa versione del file garantisce che i destinatari possano leggere sempre il file, anche se non dispongono della stessa applicazione che è stata utilizzata per crearlo. Questo accade spesso quando gli utenti leggono il messaggio e-mail sui dispositivi mobili e desiderano visualizzare gli allegati e-mail. Per aprire il file hanno bisogno solo dell'applicazione di condivisione RMS. Quindi, possono leggere il file allegato, ma non saranno in grado di modificarlo fino a quando non aprono l'altra versione del file utilizzando un'applicazione che supporta RMS.

Se l'organizzazione utilizza Azure RMS, è possibile registrare i file protetti tramite la condivisione:

-   Selezionare un'opzione per ricevere un messaggio e-mail quando qualcuno tenta di aprire gli allegati protetti. Ogni volta che viene eseguito l'accesso al file, verrà comunicato chi ha tentato di aprire il file e quando e se l’operazione ha avuto esito positivo (è stato correttamente autenticato) o meno.

-   Usare il sito di rilevamento della documentazione. È anche possibile arrestare la condivisione del file, revocandone l’accesso nel sito di rilevamento documenti. Per altre informazioni, vedere [Rilevare e revocare i documenti quando si usa l'applicazione di condivisione RMS](sharing-app-track-revoke.md).

## Tramite Outlook: Per proteggere un file che si condivide tramite e-mail

1.  Creare il messaggio e-mail e allegare il file. Nella scheda **Messaggio** , nel gruppo **RMS** , fare clic su **Condividi file protetto** e quindi fare di nuovo clic su **Condividi file protetto** :

    ![Componente aggiuntivo di Outlook per l'applicazione RMS sharing](../media/ADRMS_MSRMSApp_SP_OutlookToolbar.png)

    Se questo pulsante non è visualizzato, è probabile che l'applicazione di condivisione RMS non è installata nel computer, non è installata la versione più recente oppure è necessario riavviare il computer per completare l'installazione. Per altre informazioni su come installare l'applicazione, vedere [Scaricare e installare l'applicazione Rights Management sharing](install-sharing-app.md).

2.  Specificare le opzioni desiderate per questo file nella [finestra di dialogo Condividi file protetto](sharing-app-dialog-box.md), quindi fare clic su **Invia ora**.

### Altri modi per proteggere un file che si condivide tramite e-mail
Oltre alla condivisione di un file protetto tramite Outlook, è possibile utilizzare queste alternative:

-   Da Esplora file: Questo metodo funziona per tutti i file.

-   Da un'applicazione Office: questo metodo funziona per le applicazioni supportate dall'applicazione RMS sharing usando il componente aggiuntivo di Office in modo da visualizzare il gruppo **RMS** sulla barra multifunzione.

#### Tramite Esplora file o un'applicazione di Office: Per proteggere un file che si condivide tramite e-mail

1.  Usare uno dei seguenti metodi:

    -   Per Esplora file: fare clic con il pulsante destro del mouse sul file, selezionare **Proteggi tramite RMS**, quindi selezionare **Condividi file protetto**:

        ![Opzione di menu Condividi file protetto](../media/ADRMS_MSRMSApp_ShareProtectedMenu.png)

    -   Per le applicazioni di Office Word, Excel e PowerPoint: Assicurarsi che il file sia stato prima salvato. Quindi, nella scheda **Home** , nel gruppo **RMS** , fare clic su **Condividi file protetto** e quindi fare nuovamente clic su **Condividi file protetto** :

        ![Componente aggiuntivo della barra degli strumenti di Office](../media/ADRMS_MSRMSApp_SP_OfficeToolbar.png)

    Se queste opzioni per la protezione non sono visualizzate, è probabile che l'applicazione di condivisione RMS non è installata nel computer, non è installata la versione più recente oppure è necessario riavviare il computer per completare l'installazione. Per altre informazioni su come installare l'applicazione, vedere [Scaricare e installare l'applicazione Rights Management sharing](install-sharing-app.md).

2.  Specificare le opzioni desiderate per questo file nella [finestra di dialogo Condividi file protetto](sharing-app-dialog-box.md), quindi fare clic su **Invia**.

3.  È possibile visualizzare rapidamente una finestra di dialogo indicante che il file è protetto e quindi viene visualizzato un messaggio e-mail creato che indica ai destinatari che gli allegati sono protetti con Microsoft RMS e che devono effettuare l'accesso. Quando si fa clic sul collegamento per accedere, vengono visualizzate le istruzioni e i collegamenti per permettergli di aprire l'allegato protetto.

    Esempio:

    ![Messaggio di posta elettronica per Azure RMS](../media/ADRMS_MSRMSApp_EmailMessage.PNG)

    Ci si potrebbe chiedere: [Che cos'è il file .ppdf che viene creato automaticamente?](sharing-app-dialog-box.md#what-s-the-ppdf-file-that-s-automatically-created)

4.  Facoltativo: È possibile modificare qualsiasi elemento nel messaggio e-mail. Ad esempio, è possibile aggiungere o modificare l'oggetto o il testo del messaggio.

    > [!WARNING]
    > Anche se è possibile aggiungere o rimuovere utenti dal messaggio e-mail, ciò non modifica le autorizzazioni per l'allegato specificato nella finestra di dialogo **Condividi file protetto** . Per modificare le autorizzazioni, ad esempio per concedere a una nuova persona le autorizzazioni per aprire il file, occorre chiudere il messaggio e-mail senza salvarlo o inviarlo e tornare al passaggio 1.

5.  Inviare il messaggio e-mail.

## Esempi e altre istruzioni
Per esempi di come è possibile utilizzare l'applicazione di condivisione Rights Management e procedure, vedere le sezioni seguenti della Guida dell’utente dell’applicazione di condivisione Rights Management:

-   [Esempi per l'utilizzo dell’applicazione di condivisione RMS](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [Come procedere](sharing-app-user-guide.md#what-do-you-want-to-do)

## Vedere anche
[Guida dell'utente dell'applicazione di condivisione Rights Management](sharing-app-user-guide.md)



<!--HONumber=Aug16_HO4-->


