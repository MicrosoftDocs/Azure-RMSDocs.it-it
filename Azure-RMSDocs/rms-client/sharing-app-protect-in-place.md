---
# required metadata

title: Proteggere un file in un dispositivo (protezione sul posto) tramite l'applicazione Rights Management sharing | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 33920329-5247-4f6c-8651-6227afb4a1fa

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Proteggere un file in un dispositivo (protezione locale) mediante l'applicazione di condivisione Rights Management

*Si applica a: Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 con SP1, Windows 8, Windows 8.1*

Quando si protegge un file localmente, esso sostituisce il file originale non protetto. È quindi possibile lasciare il file dove si trova, copiarlo in un'altra cartella o dispositivo o condividere la cartella in cui si trova e il file rimarrà protetto. È possibile anche allegare il file protetto a un messaggio di posta elettronica, sebbene il modo consigliato per condividere un file protetto tramite posta elettronica sia di condividerlo direttamente da Esplora file o da un'applicazione di Office. Vedere [Proteggere un file che si condivide tramite e-mail utilizzando l'applicazione di condivisione Rights Management](sharing-app-protect-by-email.md)).

> [!TIP]
> Se vengono visualizzati errori quando si tenta di proteggere i file, vedere [FAQ for Microsoft Rights Management Sharing Application for Windows (Domande frequenti sull’applicazione di condivisione Microsoft Rights Management per Windows)](http://go.microsoft.com/fwlink/?LinkId=303971).

## Per proteggere un file in un dispositivo (protezione locale)

1.  In Esplora file, selezionare un file da proteggere. Fare clic sul pulsante destro del mouse, selezionare **Proteggi tramite RMS**, quindi selezionare **Proteggi sul posto**. Ad esempio:

    ![Opzione di menu Proteggi sul posto](../media/ADRMS_MSRMSApp_SP_CompanyDefined.png)

    > [!NOTE]
    > Se non viene visualizzata l’opzione **Proteggi tramite RMS** , è probabile che l'applicazione di RMS sharing non sia installata nel computer o che il computer debba essere riavviato per completare l'installazione. Per altre informazioni sull'installazione dell'applicazione di condivisione RMS, vedere [Scaricare e installare l'applicazione di condivisione Rights Management](install-sharing-app.md).

2.  Eseguire una delle operazioni seguenti:

    -   Selezionare un modello di criteri: Queste sono autorizzazioni predefinite che in genere limitano l'accesso e l’utilizzo agli utenti dell'organizzazione. Se ad esempio il nome dell'organizzazione è "Contoso, Ltd", potrebbe essere visualizzato **Contoso, Ltd - Solo visione riservata**. Se questa è la prima volta che si protegge un file nel computer, è necessario innanzitutto selezionare **Protezione definita dall'azienda** per scaricare i modelli.

        La volta successiva che si fa clic sull'opzione **Proteggi sul posto**, verranno visualizzati fino a 10 modelli tra cui scegliere. Se sono disponibili più di 10 modelli e quello desiderato non è visualizzato, fare clic su **Protezione definita dall'azienda** per scaricare e visualizzare tutti i modelli.

        Quando si seleziona un modello di criteri, è inoltre possibile proteggere più file e una cartella. Quando si seleziona una cartella, tutti i file al suo interno vengono selezionati automaticamente per la protezione, ma nuovi file creati in tale cartella non verranno protetti automaticamente.

    -   Selezionare **Autorizzazioni personalizzate**: Scegliere questa opzione se i modelli non forniscono il livello di protezione necessario o si desidera impostare in modo esplicito le opzioni di protezione. Specificare le opzioni desiderate per questo file nella [finestra di dialogo Aggiungi protezione](sharing-app-dialog-box.md), quindi fare clic su **Applica**.

3.  È possibile visualizzare rapidamente una finestra di dialogo per indicare che il file è protetto e tornare a Esplora file. I file selezionati sono ora protetti. In alcuni casi (quando l'aggiunta della protezione modifica l'estensione del nome di file), il file originale in Esplora file viene sostituito con un nuovo file con l'icona di blocco della protezione di Rights Management. Ad esempio:

    ![File protetto con l'icona di blocco per l'applicazione di condivisione RMS](../media/ADRMS_MSRMSApp_Pfile.png)

Se in un secondo momento è necessario rimuovere la protezione da un file, vedere [Rimuovere la protezione da un file mediante l'applicazione di condivisione Rights Management](sharing-app-remove-protection.md).

## Esempi e altre istruzioni
Per esempi di come è possibile utilizzare l'applicazione di condivisione Rights Management e procedure, vedere le sezioni seguenti della Guida dell’utente dell’applicazione di condivisione Rights Management:

-   [Esempi per l'utilizzo dell’applicazione di condivisione RMS](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [Come procedere](sharing-app-user-guide.md#what-do-you-want-to-do-)

## Vedere anche
[Guida dell'utente dell'applicazione di condivisione Rights Management](sharing-app-user-guide.md)


<!--HONumber=May16_HO2-->


