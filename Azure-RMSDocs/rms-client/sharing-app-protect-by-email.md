---
title: Condividere file protetti con l'app RMS sharing - AIP
description: Istruzioni su come condividere in modo sicuro un documento tramite posta elettronica.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4c1cd1d3-78dd-4f90-8b37-dcc9205a6736
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 71bc303aaadf6856cce2f63db0acf5280fbe172b
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
ms.locfileid: "30206496"
---
# <a name="protect-a-file-that-you-share-by-email-by-using-the-rights-management-sharing-application"></a>Proteggere un file che si condivide tramite posta elettronica usando l'applicazione Rights Management sharing

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 7 con SP1, Windows 8, Windows 8.1*

Quando si protegge un file che si condivide tramite e-mail viene creata una nuova versione del file originale. Il file originale rimane non protetto mentre la nuova versione viene protetta e automaticamente allegata a un messaggio e-mail che quindi può essere inviato.

In alcuni casi (per i file creati da Microsoft Word, Excel e PowerPoint), l'applicazione RMS sharing crea due versioni del file che viene allegato al messaggio di posta elettronica. La seconda versione del file ha l’estensione di file **.ppdf** ed è una copia shadow in formato PDF del file. Questa versione del file garantisce che i destinatari possano leggere sempre il file, anche se non dispongono della stessa applicazione che è stata utilizzata per crearlo. Questo accade spesso quando gli utenti leggono il messaggio e-mail sui dispositivi mobili e desiderano visualizzare gli allegati e-mail. Per aprire il file hanno bisogno solo dell'applicazione RMS sharing. Quindi, possono leggere il file allegato, ma non saranno in grado di modificarlo fino a quando non aprono l'altra versione del file usando un'applicazione che supporta un servizio Rights Management.

Se l'organizzazione usa Azure Information Protection, è possibile tenere traccia dei file protetti tramite la condivisione:

-   Selezionare un'opzione per ricevere un messaggio e-mail quando qualcuno tenta di aprire gli allegati protetti. Ogni volta che viene eseguito l'accesso al file, verrà comunicato chi ha tentato di aprire il file e quando e se l’operazione ha avuto esito positivo (è stato correttamente autenticato) o meno.

-   Usare il sito di rilevamento della documentazione. È anche possibile arrestare la condivisione del file, revocandone l’accesso nel sito di rilevamento documenti. Per altre informazioni, vedere [Tenere traccia dei documenti e revocarli quando si usa l'applicazione RMS sharing](sharing-app-track-revoke.md).

## <a name="using-outlook-to-protect-a-file-that-you-share-by-email"></a>Tramite Outlook: Per proteggere un file che si condivide tramite e-mail

1.  Creare il messaggio e-mail e allegare il file. Nella scheda **Messaggio** , nel gruppo **RMS** , fare clic su **Condividi file protetto** e quindi fare di nuovo clic su **Condividi file protetto** :

    ![Componente aggiuntivo di Outlook per l'applicazione RMS sharing](../media/ADRMS_MSRMSApp_SP_OutlookToolbar.png)

    Se questo pulsante non è visualizzato, è probabile che l'applicazione RMS sharing non sia installata nel computer, che non sia installata la versione più recente o che sia necessario riavviare il computer per completare l'installazione. Per altre informazioni su come installare l'applicazione, vedere [Scaricare e installare l'applicazione Rights Management sharing](install-sharing-app.md).

2.  Specificare le opzioni desiderate per questo file nella [finestra di dialogo Condividi file protetto](sharing-app-dialog-box.md), quindi fare clic su **Invia ora**.

### <a name="other-ways-to-protect-a-file-that-you-share-by-email"></a>Altri modi per proteggere un file che si condivide tramite e-mail
Oltre alla condivisione di un file protetto tramite Outlook, è possibile utilizzare queste alternative:

-   Da Esplora file: Questo metodo funziona per tutti i file.

-   Da un'applicazione Office: questo metodo funziona per le applicazioni supportate dall'applicazione RMS sharing usando il componente aggiuntivo di Office in modo da visualizzare il gruppo **RMS** sulla barra multifunzione.

#### <a name="using-file-explorer-or-an-office-application-to-protect-a-file-that-you-share-by-email"></a>Tramite Esplora file o un'applicazione di Office: Per proteggere un file che si condivide tramite e-mail

1.  Usare uno dei seguenti metodi:

    -   Per Esplora file: fare clic con il pulsante destro del mouse sul file, selezionare **Proteggi tramite RMS**, quindi selezionare **Condividi file protetto**:

        ![Opzione di menu Condividi file protetto](../media/ADRMS_MSRMSApp_ShareProtectedMenu.png)

    -   Per le applicazioni di Office Word, Excel e PowerPoint: Assicurarsi che il file sia stato prima salvato. Quindi, nella scheda **Home** , nel gruppo **RMS** , fare clic su **Condividi file protetto** e quindi fare nuovamente clic su **Condividi file protetto** :

        ![Componente aggiuntivo della barra degli strumenti di Office](../media/ADRMS_MSRMSApp_SP_OfficeToolbar.png)

    Se queste opzioni per la protezione non sono visualizzate, è probabile che l'applicazione RMS sharing non sia installata nel computer, che non sia installata la versione più recente o che sia necessario riavviare il computer per completare l'installazione. Per altre informazioni su come installare l'applicazione, vedere [Scaricare e installare l'applicazione Rights Management sharing](install-sharing-app.md).

2.  Specificare le opzioni desiderate per questo file nella [finestra di dialogo Condividi file protetto](sharing-app-dialog-box.md), quindi fare clic su **Invia**.

3.  È possibile visualizzare rapidamente una finestra di dialogo indicante che il file è protetto e quindi viene visualizzato un messaggio e-mail creato che indica ai destinatari che gli allegati sono protetti con Microsoft RMS e che devono effettuare l'accesso. Quando si fa clic sul collegamento per accedere, vengono visualizzate le istruzioni e i collegamenti per permettergli di aprire l'allegato protetto.

    Esempio:

    ![Messaggio di posta elettronica per Azure Information Protection](../media/ADRMS_MSRMSApp_EmailMessage.PNG)

    Ci si potrebbe chiedere: [Che cos'è il file .ppdf che viene creato automaticamente?](sharing-app-dialog-box.md#whats-the-ppdf-file-thats-automatically-created)

4.  Facoltativo: È possibile modificare qualsiasi elemento nel messaggio e-mail. Ad esempio, è possibile aggiungere o modificare l'oggetto o il testo del messaggio.

    > [!WARNING]
    > Anche se è possibile aggiungere o rimuovere utenti dal messaggio e-mail, ciò non modifica le autorizzazioni per l'allegato specificato nella finestra di dialogo **Condividi file protetto** . Per modificare le autorizzazioni, ad esempio per concedere a una nuova persona le autorizzazioni per aprire il file, occorre chiudere il messaggio e-mail senza salvarlo o inviarlo e tornare al passaggio 1.

5.  Inviare il messaggio e-mail.

## <a name="examples-and-other-instructions"></a>Esempi e altre istruzioni
Per esempi di come è possibile usare l'applicazione Rights Management sharing e informazioni sulle procedure da seguire, vedere le sezioni seguenti della Guida dell'utente dell'applicazione Rights Management sharing:

-   [Esempi per l'uso dell'applicazione RMS sharing](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [Per saperne di più](sharing-app-user-guide.md#what-do-you-want-to-do)

## <a name="see-also"></a>Vedere anche
[Guida dell'utente dell'applicazione di condivisione Rights Management](sharing-app-user-guide.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]