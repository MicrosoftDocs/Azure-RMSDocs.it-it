---
title: Tenere traccia dei documenti protetti e revocarli quando si usa Azure Information Protection | Azure Information Protection
description: "Dopo aver protetto i documenti, è possibile tenere traccia del modo in cui tali documenti vengono usati dagli utenti. Se necessario, è anche possibile revocare l&quot;accesso a questi documenti se gli utenti non dovranno più essere in grado di leggerli."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/07/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 643c762e-23ca-4b02-bc39-4e3eeb657a1d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 54abc32a6065bb3863cf55b42466250f8fc9c634


---

# <a name="track-and-revoke-your-documents-when-you-use-azure-information-protection"></a>Tenere traccia dei documenti e revocarli quando si usa Azure Information Protection

>*Si applica a: Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*

**[Questa versione del client è in anteprima e soggetta a modifiche].**

Dopo avere protetto i documenti con Azure Information Protection, è possibile tenere traccia del modo in cui tali documenti vengono usati dagli utenti. Se necessario, è anche possibile revocare l'accesso a questi documenti se gli utenti non dovranno più essere in grado di leggerli. A tale scopo, usare il **sito di rilevamento del documento**, a cui è possibile accedere dai computer Windows, dai computer Mac e anche da tablet e telefoni.

<div style="padding-top: 56.25%; position: relative; width: 100%;">
<iframe style="position: absolute;top: 0;left: 0;right: 0;bottom: 0;" width="100%" height="100%" src="https://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation/player" frameborder="0" allowfullscreen></iframe>
</div>

Quando si accede a questo sito, eseguire l'accesso per effettuare il rilevamento dei documenti. A condizione che l'organizzazione abbia una [sottoscrizione che supporta il rilevamento e la revoca dei documenti](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features) e di avere ricevuto una licenza per tale sottoscrizione, è quindi possibile sapere chi ha tentato di aprire i file protetti e se il tentativo ha avuto esito positivo (ovvero se è stata eseguita correttamente l'autenticazione) o meno. È anche possibile verificare ogni tentativo di accesso al documento e la posizione dell'utente in quel momento. Inoltre:

-   Se è necessario interrompere la condivisione di un documento: Fare clic su **Revocare l'accesso**, si noti il periodo di tempo in cui il documento continuerà a essere disponibile, e decidere se si vuol far sapere agli utenti che si sta revocando l'accesso al documento condiviso in precedenza e inviare un messaggio personalizzato. Quando si revoca un documento, il documento condiviso non viene eliminato, ma gli utenti autorizzati non potranno più aprirlo.

-   Se si vuole esportare in Excel: fare clic su **Esporta in CSV**, in modo da poter poi modificare i dati e creare le visualizzazioni e i grafici.

-   Se si desidera configurare notifiche tramite posta elettronica: Fare clic su **Impostazioni** e selezionare come e se ricevere un messaggio di posta elettronica quando si accede al documento.

- Se si vuole tenere traccia dei documenti condivisi e revocarli per conto di altri utenti: gli amministratori di Azure Information Protection possono eseguire queste operazioni facendo clic sull'icona di amministrazione. Solo gli amministratori visualizzano questa icona.

-   Se si hanno domande o si vogliono lasciare commenti e suggerimenti sul sito di rilevamento del documento: fare clic sull'icona della Guida per accedere a [Domande frequenti sul rilevamento dei documenti](http://go.microsoft.com/fwlink/?LinkId=523977).

## <a name="using-office-to-access-the-document-tracking-site"></a>Utilizzare Office per accedere al sito di rilevamento del documento

-   Per le applicazioni di Office, Word, Excel, PowerPoint e Outlook: nel gruppo **Protezione** della scheda **Home** fare clic su **Proteggi** > **Rileva utilizzo**.

Se queste opzioni non vengono visualizzate nelle applicazioni di Office, è probabile che il client di Azure Information Protection non sia installato nel computer, che sia necessario riavviare le applicazioni di Office o che sia necessario riavviare il computer per completare l'installazione. Per altre informazioni su come installare il client di Azure Information Protection, vedere [Scaricare e installare il client di Azure Information Protection](install-client-app.md).


### <a name="other-ways-to-track-and-revoke-your-documents"></a>Altri modi per tenere traccia dei documenti e revocarli
Oltre a tenere traccia dei documenti protetti nei computer Windows con le applicazioni di Office, è anche possibile usare queste alternative:

-   **Tramite un browser web**: Questo metodo funziona per tutti i dispositivi supportati.

-   **Tramite Esplora File**: Questo metodo funziona per i computer Windows.

#### <a name="using-a-web-browser-to-access-the-doc-tracking-site"></a>Tramite l’utilizzo di un browser per accedere al sito di rilevamento dei documenti

-   Tramite l’utilizzo di un browser supportato, passare al [sito di rilevamento del documento](https://go.microsoft.com/fwlink/?LinkId=529562).

    Browser supportati: È consigliabile utilizzare almeno la versione  10 di Internet Explorer, ma è possibile utilizzare uno qualsiasi dei browser seguenti per utilizzare il sito di rilevamento del documento:

    -   Internet Explorer: Almeno la versione  10

    -   Internet Explorer 9 con almeno MS12-037: aggiornamento cumulativo della sicurezza per Internet Explorer: 12 giugno 2012

    -   Mozilla Firefox: Almeno la versione  12

    -   Apple Safari 5: Almeno la versione  5

    -   Google Chrome: Almeno la versione  18

#### <a name="using-file-explorer-to-access-the-doc-tracking-site"></a>Utilizzando Esplora File per accedere al sito di rilevamento del documento

-   Fare clic con il pulsante destro del mouse sul file, scegliere **Classifica e proteggi (anteprima)**, quindi nel **visualizzatore Azure Information Protection** selezionare l'icona Rileva utilizzo.


## <a name="other-instructions"></a>Altre istruzioni
Per le istruzioni d'uso, vedere le sezioni seguenti della Guida per l'utente di Azure Information Protection:

-   [Per saperne di più](client-user-guide.md#what-do-you-want-to-do)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO4-->


