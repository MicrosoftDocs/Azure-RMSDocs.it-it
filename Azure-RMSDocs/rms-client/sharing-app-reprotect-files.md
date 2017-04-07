---
title: Modificare le autorizzazioni sui file protetti da RMS - AIP
description: "Quando un file è protetto da Rights Management, è possibile modificarne le autorizzazioni riproteggendolo e quindi specificando tutti gli utenti che possono accedere al file e le autorizzazioni che si vogliono assegnare a tali utenti."
keywords: 
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5ac121b3-d7a0-40e4-8fe7-90bf4cf796f1
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: c355f3d7f21ece6a63c2b43982fcec8f668cd38a
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="change-permissions-on-files-that-have-been-protected-by-rights-management"></a>Modificare le autorizzazioni per i file protetti da Rights Management

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 7 con SP1, Windows 8, Windows 8.1*

Quando un file è protetto da Rights Management, è possibile modificarne le autorizzazioni riproteggendolo e quindi specificando tutti gli utenti che possono accedere al file e le autorizzazioni che si vogliono assegnare a tali utenti.

> [!IMPORTANT]
> Non si tratta di una modifica incrementale ma di una sostituzione completa. Si sta in effetti riproteggendo il file con il set completo delle autorizzazioni volute.
> 
>  Se ad esempio un file è protetto in modo che possano aprirlo solo gli utenti del reparto Marketing e si vuole che anche altri utenti del reparto Vendite possano aprirlo, è necessario riproteggere il file in modo che possa essere aperto dal reparto Vendite e dal reparto Marketing.
>
> Analogamente, se si vuole aggiungere o rimuovere un'autorizzazione, non è sufficiente specificare l'autorizzazione da aggiungere o rimuovere, ma è necessario specificare tutte le autorizzazioni che gli utenti specificati devono avere.

Il proprietario del file da riproteggere (l'utente che, ad esempio, ha originariamente protetto il file tramite l'applicazione di condivisione) ha automaticamente le autorizzazioni per riproteggere il file. Se l'utente non è il proprietario, il fatto che abbia le autorizzazioni necessarie a riproteggere il file dipende dalle autorizzazioni correnti del file protetto. Per proteggere un file, è necessario il [diritto di utilizzo del controllo completo](../deploy-use/configure-usage-rights.md#usage-rights-and-descriptions).

Se ad esempio un altro utente ha protetto il file tramite l'applicazione Rights Management sharing specificando per l'utente corrente un gruppo di appartenenza e l'autorizzazione personalizzata **Comproprietario**, l'utente corrente sarà in grado di riproteggere il file. Se invece l'altro utente non ha specificato il nome dell'utente corrente né un gruppo di appartenenza per quest'ultimo, oppure se ha selezionato **Revisore – Visualizzazione e Modifica** o un modello che non consente di rimuovere le autorizzazioni, l'utente corrente non sarà in grado di riproteggere il file. Il modo più semplice per scoprirlo è tentare di riproteggere il file.

Se si vogliono rimuovere completamente tutte le autorizzazioni in modo che il file non sia più protetto, vedere [Rimuovere la protezione da un file](sharing-app-remove-protection.md).

## <a name="to-re-protect-a-file-in-place"></a>Per riproteggere un file sul posto

1.  In Esplora file, selezionare un file da proteggere. Fare clic sul pulsante destro del mouse, selezionare **Proteggi tramite RMS**, quindi selezionare **Proteggi sul posto**. Ad esempio:

    ![Opzione di menu Proteggi sul posto](../media/ADRMS_MSRMSApp_SP_CompanyDefined.png)

    > [!NOTE]
    > Se non viene visualizzata l’opzione **Proteggi tramite RMS** , è probabile che l'applicazione di RMS sharing non sia installata nel computer o che il computer debba essere riavviato per completare l'installazione. Per altre informazioni su come installare l'applicazione RMS sharing, vedere [Scaricare e installare l'applicazione Rights Management sharing](install-sharing-app.md).

2.  Eseguire una delle operazioni seguenti:

    -   Selezionare un modello di criteri: Queste sono autorizzazioni predefinite che in genere limitano l'accesso e l’utilizzo agli utenti dell'organizzazione. Se ad esempio il nome dell'organizzazione è "Contoso, Ltd", potrebbe essere visualizzato **Contoso, Ltd - Solo visione riservata**. Se questa è la prima volta che si protegge un file nel computer, è necessario innanzitutto selezionare **Protezione definita dall'azienda** per scaricare i modelli.

        La volta successiva che si fa clic sull'opzione **Proteggi sul posto**, verranno visualizzati fino a 10 modelli tra cui scegliere. Se sono disponibili più di 10 modelli e quello desiderato non è visualizzato, fare clic su **Protezione definita dall'azienda** per scaricare e visualizzare tutti i modelli.

        Quando si seleziona un modello di criteri, è inoltre possibile proteggere più file e una cartella. Quando si seleziona una cartella, tutti i file al suo interno vengono selezionati automaticamente per la protezione, ma nuovi file creati in tale cartella non verranno protetti automaticamente.

    -   Selezionare **Autorizzazioni personalizzate**: Scegliere questa opzione se i modelli non forniscono il livello di protezione necessario o si desidera impostare in modo esplicito le opzioni di protezione. Specificare le opzioni desiderate per questo file nella [finestra di dialogo Aggiungi protezione](sharing-app-dialog-box.md), quindi fare clic su **Applica**.

3. Se non si hanno le autorizzazioni per riproteggere il file, viene visualizzato il messaggio **Unable to protect content** (Impossibile proteggere il contenuto) con l'indirizzo di posta elettronica della persona da contattare (il proprietario del documento) per ottenere la modifica delle autorizzazioni.

    Se si hanno le autorizzazioni necessarie per riproteggere il file, è possibile visualizzare rapidamente una finestra di dialogo per indicare che il file è protetto e tornare a Esplora file. I file selezionati sono ora protetti con le modifiche dell'utente. 

> [!NOTE]
> Prima di poter riapplicare la protezione al file, il servizio Rights Management deve verificare che l'utente sia autorizzato a eseguire l'azione sul file e a tale scopo controlla il nome utente e la password. In alcuni casi, questo potrebbe essere memorizzato nella cache e non verrà visualizzato un messaggio che richiede l'immissione delle credenziali. In altri casi, verrà richiesto di fornire le credenziali.
>
> Se l'organizzazione non usa Azure Information Protection o AD RMS, è possibile richiedere un account gratuito che accetterà le credenziali in modo che sia possibile usare file protetti tramite RMS:
>
> -   Per richiedere questo account, fare clic sul collegamento per richiedere [RMS per utenti singoli](http://go.microsoft.com/fwlink/?LinkId=309469).
>
>     Quando si effettua l'iscrizione, utilizzare l'indirizzo di posta elettronica della società anziché un indirizzo di posta elettronica personale. Se si esegue l'iscrizione perché è stato inviato un allegato protetto tramite posta elettronica, utilizzare lo stesso indirizzo di posta elettronica utilizzato per inviare il messaggio di posta elettronica.
> -   Per ulteriori informazioni, vedere [RMS per utenti singoli e Azure Rights Management](../understand-explore/rms-for-individuals.md).

## <a name="to-re-protect-a-file-that-you-have-emailed"></a>Per riproteggere un file inviato tramite posta elettronica

Se si vogliono modificare le autorizzazioni per un file inviato tramite posta elettronica:

- **Per consentire a più utenti di leggere il file**: inviare loro il file tramite posta elettronica, seguendo le istruzioni in [Proteggere un file che si condivide tramite e-mail](sharing-app-protect-by-email.md).

- **Per modificare le autorizzazioni per il file**: inviare di nuovo il file tramite posta elettronica, seguendo le istruzioni in [Proteggere un file che si condivide tramite e-mail](sharing-app-protect-by-email.md) e scegliere le nuove autorizzazioni volute. 

    Poiché non è possibile rimuovere le autorizzazioni precedenti dal file precedentemente inviato tramite posta elettronica, sostituirle solo con una nuova versione. Prendere in considerazione la possibilità di revocare il file inviato in precedenza in modo che i destinatari non possano più aprire quella versione del documento. La revoca è appropriata se è necessario rendere più restrittive le autorizzazioni, ad esempio rimuovendo gli utenti che non devono avere accesso al file o non devono più essere in grado di aprirlo.

    Per revocare un file inviato tramite posta elettronica, vedere [Tenere traccia dei documenti e revocarli](sharing-app-track-revoke.md).


## <a name="examples-and-other-instructions"></a>Esempi e altre istruzioni
Per esempi di come è possibile usare l'applicazione Rights Management sharing e informazioni sulle procedure da seguire, vedere le sezioni seguenti della Guida dell'utente dell'applicazione Rights Management sharing:

-   [Esempi per l'uso dell'applicazione RMS sharing](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [Per saperne di più](sharing-app-user-guide.md#what-do-you-want-to-do)

## <a name="see-also"></a>Vedere anche
[Guida dell'utente dell'applicazione di condivisione Rights Management](sharing-app-user-guide.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]