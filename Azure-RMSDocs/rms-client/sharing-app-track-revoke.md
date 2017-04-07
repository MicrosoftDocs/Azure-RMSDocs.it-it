---
title: Tenere traccia dei documenti e revocarli con l&quot;app RMS sharing - AIP
description: "Dopo che i documenti sono stati protetti usando l&quot;applicazione RMS sharing, è possibile rilevare come tali documenti vengono usati dagli utenti. Se necessario, è anche possibile revocare l&quot;accesso a questi documenti quando si desidera interromperne la condivisione."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 61f349ce-bdd2-45c1-acc5-bc83937fb187
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: b56bebbdebc79cfd0d53b4e83714f8a04dfb5a25
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="track-and-revoke-your-documents-when-you-use-the-rms-sharing-application"></a>Tenere traccia dei documenti e revocarli quando si usa l'applicazione RMS sharing

>*Si applica a: Azure Information Protection, Windows 10, Windows 7 con SP1, Windows 8, Windows 8.1*

Dopo avere protetto i documenti tramite l'applicazione RMS sharing, se l'organizzazione usa Azure Information Protection invece di Active Directory Rights Management Services, è possibile tenere traccia del modo in cui le persone usano i documenti protetti. Se necessario, è anche possibile revocare l'accesso a questi documenti quando si desidera interromperne la condivisione. A tale scopo, usare il **sito di rilevamento del documento**, a cui è possibile accedere dai computer Windows, dai computer Mac e anche da tablet e telefoni.

<div style="padding-top: 56.25%; position: relative; width: 100%;">
<iframe style="position: absolute;top: 0;left: 0;right: 0;bottom: 0;" width="100%" height="100%" src="https://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation/player" frameborder="0" allowfullscreen></iframe>
</div>

Quando si accede a questo sito, eseguire l'accesso per effettuare il rilevamento dei documenti. A condizione che l'organizzazione abbia una [sottoscrizione che supporta il rilevamento e la revoca dei documenti](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features) e di avere ricevuto una licenza per tale sottoscrizione, è quindi possibile sapere chi ha tentato di aprire i file protetti e se il tentativo ha avuto esito positivo (ovvero se è stata eseguita correttamente l'autenticazione) o meno. Ogni volta che ha tentato di accedere al documento e la sua posizione in quel momento. Inoltre:

-   Se è necessario interrompere la condivisione di un documento: Fare clic su **Revocare l'accesso**, si noti il periodo di tempo in cui il documento continuerà a essere disponibile, e decidere se si vuol far sapere agli utenti che si sta revocando l'accesso al documento condiviso in precedenza e inviare un messaggio personalizzato. Quando si revoca un documento, il documento condiviso non viene eliminato ma gli utenti autorizzati non potranno più aprirlo.

-   Se si vuole esportare in Excel: fare clic su **Esporta in CSV**, in modo da poter poi modificare i dati e creare le visualizzazioni e i grafici.

-   Se si desidera configurare notifiche tramite posta elettronica: Fare clic su **Impostazioni** e selezionare come e se ricevere un messaggio di posta elettronica quando si accede al documento.

- Se si vuole tenere traccia dei documenti condivisi e revocarli per conto di altri utenti: gli amministratori di Azure Information Protection possono eseguire queste operazioni facendo clic sull'icona di amministrazione. Solo gli amministratori visualizzano questa icona.

-   Se si hanno domande o si vogliono lasciare commenti e suggerimenti sul sito di rilevamento del documento: fare clic sull'icona della Guida per accedere a [Domande frequenti sul rilevamento dei documenti](http://go.microsoft.com/fwlink/?LinkId=523977).

## <a name="using-office-to-access-the-document-tracking-site"></a>Utilizzare Office per accedere al sito di rilevamento del documento

-   Per le applicazioni di Office, Word, Excel e PowerPoint: Nella scheda **Home** , nel gruppo **RMS** , fare clic su **Condivisione protetta**, e poi fare clic su **Rileva utilizzo**.

    ![Rilevare l'utilizzo dalle applicazioni di Office quando si usa l'applicazione RMS sharing ](../media/ADRMS_MSRMSApp_OfficeToolbarTrackUsage.png)

-   Per Outlook: In Outlook, nella scheda **Home** , nel gruppo  **RMS** , fare clic su **Rileva utilizzo**.

    ![Selezionare Rileva utilizzo da Outlook quando si usa l'applicazione RMS sharing ](../media/ADRMS_MSRMSApp_OutlookTrackUsage.png)

Se queste opzioni per RMS non sono visualizzate, è probabile che l'applicazione RMS sharing non sia installata nel computer o che il computer debba essere riavviato per completare l'installazione. Per altre informazioni su come installare l'applicazione, vedere [Scaricare e installare l'applicazione Rights Management sharing](install-sharing-app.md).

> [!NOTE] 
> Se è stato installato il [client di Azure Information Protection](../rms-client/info-protect-client.md), è possibile accedere anche al sito di rilevamento dei documenti usando il pulsante **Proteggi**: 
> 
> - In un'applicazione di Office, nel gruppo **Protezione** della scheda **Home** fare clic su **Proteggi** > **Rileva utilizzo**. 

### <a name="other-ways-to-track-and-revoke-your-documents"></a>Altri modi per tenere traccia dei documenti e revocarli
Oltre a tenere traccia dei documenti nei computer Windows utilizzando applicazioni Office, è anche possibile utilizzare queste alternative:

-   **Tramite un browser web**: Questo metodo funziona per tutti i dispositivi supportati.

-   **Tramite Esplora File**: Questo metodo funziona per i computer Windows.

-   **Tramite un messaggio di posta elettronica di Outlook**: Questo metodo funziona per i computer Windows.

#### <a name="using-a-web-browser-to-access-the-doc-tracking-site"></a>Tramite l’utilizzo di un browser per accedere al sito di rilevamento dei documenti

-   Tramite l’utilizzo di un browser supportato, passare al [sito di rilevamento del documento](http://go.microsoft.com/fwlink/?LinkId=529562).

    Browser supportati: È consigliabile utilizzare almeno la versione  10 di Internet Explorer, ma è possibile utilizzare uno qualsiasi dei browser seguenti per utilizzare il sito di rilevamento del documento:

    -   Internet Explorer: Almeno la versione  10

    -   Internet Explorer 9 con almeno MS12-037: aggiornamento cumulativo della sicurezza per Internet Explorer: 12 giugno 2012

    -   Mozilla Firefox: Almeno la versione  12

    -   Apple Safari 5: Almeno la versione  5

    -   Google Chrome: Almeno la versione  18

#### <a name="using-file-explorer-to-access-the-doc-tracking-site"></a>Utilizzando Esplora File per accedere al sito di rilevamento del documento

-   Fare clic con il pulsante destro del mouse sul file, selezionare **Proteggi tramite RMS**, poi selezionare **Rileva utilizzo**:

    ![Selezionare Rileva utilizzo da Explorer quando si usa l'applicazione RMS sharing](../media/ADRMS_MSRMSApp_ExplorerTrackUsage.png)

#### <a name="using-an-outlook-email-message-to-access-the-doc-tracking-site"></a>Utilizzo di un messaggio di posta elettronica di Outlook per accedere al sito di rilevamento del documento

-   In un messaggio di posta elettronica, nella scheda **Messaggio** , nel gruppo  **RMS** , fare clic su **Condivisione protetta**, e poi fare clic su **Traccia utilizzo**:

    ![Selezionare Rileva utilizzo da Outlook quando si usa l'applicazione RMS sharing](../media/ADRMS_MSRMSApp_OutlookMessageTrackUsage.png)

## <a name="examples-and-other-instructions"></a>Esempi e altre istruzioni
Per esempi di come è possibile usare l'applicazione Rights Management sharing e informazioni sulle procedure da seguire, vedere le sezioni seguenti della Guida dell'utente dell'applicazione Rights Management sharing:

-   [Esempi per l'uso dell'applicazione RMS sharing](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [Per saperne di più](sharing-app-user-guide.md#what-do-you-want-to-do)

## <a name="see-also"></a>Vedere anche
[Guida dell'utente dell'applicazione di condivisione Rights Management](sharing-app-user-guide.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]