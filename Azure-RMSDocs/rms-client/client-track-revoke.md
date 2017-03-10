---
title: Tenere traccia di documenti e revocarli - Azure Information Protection
description: "Dopo aver protetto i documenti, è possibile tenere traccia del modo in cui tali documenti vengono usati dagli utenti. Se necessario, è anche possibile revocare l&quot;accesso a questi documenti se gli utenti non dovranno più essere in grado di leggerli."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 643c762e-23ca-4b02-bc39-4e3eeb657a1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: a79c6d1ff5b3a031138cb3d4dde179909134353a
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="track-and-revoke-your-documents-when-you-use-azure-information-protection"></a>Tenere traccia dei documenti e revocarli quando si usa Azure Information Protection

>*Si applica a: Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*

Dopo avere protetto i documenti con Azure Information Protection, è possibile tenere traccia del modo in cui tali documenti vengono usati dagli utenti. Se necessario, è anche possibile revocare l'accesso a questi documenti se gli utenti non dovranno più essere in grado di leggerli. A tale scopo, usare il **sito di rilevamento del documento**, a cui è possibile accedere dai computer Windows, dai computer Mac e anche da tablet e telefoni.

Quando si accede a questo sito, eseguire l'accesso per effettuare il rilevamento dei documenti. A condizione che l'organizzazione abbia una [sottoscrizione che supporta il rilevamento e la revoca dei documenti](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features) e di avere ricevuto una licenza per tale sottoscrizione, è quindi possibile sapere chi ha tentato di aprire i file protetti e se il tentativo ha avuto esito positivo (ovvero se è stata eseguita correttamente l'autenticazione) o meno. È anche possibile verificare ogni tentativo di accesso al documento e la posizione dell'utente in quel momento. Inoltre:

-   Se è necessario interrompere la condivisione di un documento: Fare clic su **Revocare l'accesso**, si noti il periodo di tempo in cui il documento continuerà a essere disponibile, e decidere se si vuol far sapere agli utenti che si sta revocando l'accesso al documento condiviso in precedenza e inviare un messaggio personalizzato. Quando si revoca un documento, il documento condiviso non viene eliminato, ma gli utenti autorizzati non potranno più aprirlo:
    
    ![Icona per la revoca dell'accesso nel sito di rilevamento dei documenti](../media/tracking-site-revoke-access-icon.png)

-   Se si vuole esportare in Excel: fare clic su **Esporta in CSV** per poter quindi modificare i dati e creare visualizzazioni e grafici personalizzati:
    
    ![Icona Esporta in CSV nel sito di rilevamento dei documenti](../media/tracking-site-export-icon.png)

-   Se si vuole configurare notifiche tramite posta elettronica: fare clic su **Impostazioni** e selezionare come e se ricevere un messaggio di posta elettronica quando si accede al documento:
    
    ![Icona Esporta in CSV nel sito di rilevamento dei documenti](../media/tracking-site-settings-email.png)

- Se si vuole tenere traccia dei documenti condivisi e revocarli per conto di altri utenti: gli amministratori di Azure Information Protection possono eseguire queste operazioni facendo clic sull'icona di amministrazione. Solo gli amministratori possono visualizzare questa icona:
    
    ![Icona di amministrazione nel sito di rilevamento dei documenti](../media/tracking-site-admin-icon.png)

Per tenere traccia di un documento protetto, questo deve essere registrato nel sito di rilevamento dei documenti. A questo scopo, usare Esplora file o le app di Office.

## <a name="using-office-to-track-or-revoke-the-document"></a>Uso di Office per tenere traccia del documento e revocarlo

Per le applicazioni di Office, Word, Excel, PowerPoint e Outlook: 

1. Aprire il documento protetto di cui tenere traccia o da revocare.

2. Nel gruppo **Protezione** della scheda **Home** fare clic su **Proteggi** > **Rileva e revoca**:

    ![Opzione Rileva utilizzo](../media/track-usage-callout.png)

Se queste opzioni non vengono visualizzate nelle applicazioni di Office, è probabile che il client di Azure Information Protection non sia installato nel computer, che sia necessario riavviare le applicazioni di Office o che sia necessario riavviare il computer per completare l'installazione. Per altre informazioni su come installare il client di Azure Information Protection, vedere [Scaricare e installare il client di Azure Information Protection](install-client-app.md).

## <a name="using-file-explorer-to-track-or-revoke-the-document"></a>Uso di Esplora File per tenere traccia del documento o revocarlo

1. Fare clic con il pulsante destro del mouse sul file protetto e scegliere **Classifica e proteggi**.

2. Nella finestra di dialogo **Classifica e proteggi - Azure Information Protection** fare clic su **Rileva e revoca**.

    ![Icona Rileva e revoca nella finestra di dialogo Classifica e proteggi - Azure Information Protection](../media/track-and-revoke.png)


### <a name="using-a-web-browser-track-and-revoke-documents-that-you-have-registered"></a>Uso di un Web browser per tenere traccia di documenti registrati e revocarli

Dopo aver registrato i documenti protetti tramite le app di Office o Esplora file, è possibile tenere traccia di questi documenti e revocarli usando un Web browser supportato:

- Tramite il PC Windows, il computer Mac o il dispositivo mobile, visitare il [sito di rilevamento dei documenti](https://go.microsoft.com/fwlink/?LinkId=529562).

    **Browser supportati**: anche se è consigliabile usare almeno la versione 10 di Internet Explorer, è possibile usare anche uno qualsiasi dei browser seguenti per visitare il sito di rilevamento dei documenti:

    -   Internet Explorer: almeno la versione 10

    -   Internet Explorer 9 con almeno MS12-037: aggiornamento cumulativo della sicurezza per Internet Explorer: 12 giugno 2012

    -   Mozilla Firefox: Almeno la versione  12

    -   Apple Safari 5: Almeno la versione  5

    -   Google Chrome: Almeno la versione  18


## <a name="other-instructions"></a>Altre istruzioni
Ulteriori procedure nella Guida per l'utente di Azure Information Protection:

- [Per saperne di più](client-user-guide.md#what-do-you-want-to-do)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]