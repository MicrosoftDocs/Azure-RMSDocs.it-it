---
title: Tenere traccia di documenti e revocarli - Azure Information Protection
description: "Dopo aver protetto i documenti, è possibile tenere traccia del modo in cui tali documenti vengono usati dagli utenti. Se necessario, è anche possibile revocare l'accesso a questi documenti se gli utenti non dovranno più essere in grado di leggerli."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 643c762e-23ca-4b02-bc39-4e3eeb657a1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 79c02795ca10ff875744f3b6c90cebd582cb8c3e
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/30/2017
---
<a id="track-and-revoke-your-documents-when-you-use-azure-information-protection" class="xliff"></a>

# Tenere traccia dei documenti e revocarli quando si usa Azure Information Protection

>*Si applica a: Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*

Dopo avere protetto i documenti con Azure Information Protection, è possibile tenere traccia del modo in cui tali documenti vengono usati dagli utenti. Se necessario, è anche possibile revocare l'accesso a questi documenti se gli utenti non dovranno più essere in grado di leggerli. A tale scopo, usare il **sito di rilevamento del documento**, a cui è possibile accedere dai computer Windows, dai computer Mac e anche da tablet e telefoni.

Quando si accede a questo sito, eseguire l'accesso per effettuare il rilevamento dei documenti. A condizione che l'organizzazione abbia una [sottoscrizione che supporta il rilevamento e la revoca dei documenti](https://www.microsoft.com/cloud-platform/azure-information-protection-features) e di avere ricevuto una licenza per tale sottoscrizione, è quindi possibile sapere chi ha tentato di aprire i file protetti e se il tentativo ha avuto esito positivo (ovvero se è stata eseguita correttamente l'autenticazione) o meno. È anche possibile verificare ogni tentativo di accesso al documento e la posizione dell'utente in quel momento. Inoltre:

- Se è necessario interrompere la condivisione di un documento, 
    
    - Fare clic sul pulsante **Revoca accesso**, annotare il periodo di tempo durante il quale il documento continuerà a essere disponibile e decidere se consentire alle persone di sapere che si sta revocando l'accesso al documento condiviso in precedenza e usare un messaggio personalizzato. Quando si revoca un documento, il documento condiviso non viene eliminato, ma gli utenti autorizzati non potranno più aprirlo:
        
        ![Icona per la revoca dell'accesso nel sito di rilevamento dei documenti](../media/tracking-site-revoke-access-icon.png)
        
- Per esportare in Excel, 
    
    - Fare clic su **Esporta in CSV**, in modo da poter modificare i dati e creare visualizzazioni e grafici personalizzati:
         
        ![Icona Esporta in CSV nel sito di rilevamento dei documenti](../media/tracking-site-export-icon.png)
         
- Per configurare notifiche di posta elettronica, 
     
    - Fare clic su **Impostazioni** e indicare se e in che modo ricevere una notifica di posta elettronica quando un utente accede al documento:
        
        ![Icona Esporta in CSV nel sito di rilevamento dei documenti](../media/tracking-site-settings-email.png)

- Per rilevare e revocare i documenti condivisi per conto di altri utenti:
    
    - gli amministratori di Azure Information Protection possono rilevare e revocare i documenti protetti per conto di altri facendo clic sull'icona di amministrazione. Solo gli amministratori possono visualizzare questa icona:
        
        ![Icona di amministrazione nel sito di rilevamento dei documenti](../media/tracking-site-admin-icon.png)

A meno che non sia un amministratore, l'utente può rilevare e revocare solo i documenti che ha protetto. Non è possibile rilevare i messaggi di posta elettronica protetti usando il sito di rilevamento dei documenti.

> [!NOTE] 
> Se l'amministratore ha configurato controlli sulla privacy per il sito di rilevamento dei documenti, può non essere possibile vedere quando gli utenti dell'organizzazione accedono a un documento rilevato. Un amministratore può escludere tutti gli utenti o solo alcuni utenti. Tuttavia, è sempre possibile revocare l'accesso ai documenti rilevati.

Per rilevare un documento protetto, è necessario usare il computer Windows per registrarlo con il sito di rilevamento dei documenti. A questo scopo, usare Esplora file o le app di Office.

<a id="using-office-to-track-or-revoke-the-document" class="xliff"></a>

## Uso di Office per tenere traccia del documento e revocarlo

Per le applicazioni di Office, Word, Excel, PowerPoint e Outlook: 

1. Aprire il documento protetto di cui tenere traccia o da revocare.

2. Nel gruppo **Protezione** della scheda **Home** fare clic su **Proteggi** > **Rileva e revoca**:

    ![Opzione Rileva utilizzo](../media/track-usage-callout.png)

Se queste opzioni non vengono visualizzate nelle applicazioni di Office, è probabile che il client di Azure Information Protection non sia installato nel computer, che sia necessario riavviare le applicazioni di Office o che sia necessario riavviare il computer per completare l'installazione. Per altre informazioni su come installare il client di Azure Information Protection, vedere [Scaricare e installare il client di Azure Information Protection](install-client-app.md).

<a id="using-file-explorer-to-track-or-revoke-the-document" class="xliff"></a>

## Uso di Esplora File per tenere traccia del documento o revocarlo

1. Fare clic con il pulsante destro del mouse sul file protetto e scegliere **Classifica e proteggi**.

2. Nella finestra di dialogo **Classifica e proteggi - Azure Information Protection** fare clic su **Rileva e revoca**.

    ![Icona Rileva e revoca nella finestra di dialogo Classifica e proteggi - Azure Information Protection](../media/track-and-revoke.png)


<a id="using-a-web-browser-to-track-and-revoke-documents-that-you-have-registered" class="xliff"></a>

### Uso di un Web browser per rilevare e revocare i documenti registrati

Dopo aver registrato i documenti protetti tramite le app di Office o Esplora file, è possibile tenere traccia di questi documenti e revocarli usando un Web browser supportato:

- Tramite il PC Windows, il computer Mac o il dispositivo mobile, visitare il [sito di rilevamento dei documenti](https://go.microsoft.com/fwlink/?LinkId=529562).

    **Browser supportati**: anche se è consigliabile usare almeno la versione 10 di Internet Explorer, è possibile usare anche uno qualsiasi dei browser seguenti per visitare il sito di rilevamento dei documenti:

    -   Internet Explorer: almeno la versione 10

    -   Internet Explorer 9 con almeno MS12-037: aggiornamento cumulativo della sicurezza per Internet Explorer: 12 giugno 2012

    -   Mozilla Firefox: Almeno la versione  12

    -   Apple Safari 5: Almeno la versione  5

    -   Google Chrome: Almeno la versione  18


<a id="other-instructions" class="xliff"></a>

## Altre istruzioni
Ulteriori procedure nella Guida per l'utente di Azure Information Protection:

- [Per saperne di più](client-user-guide.md#what-do-you-want-to-do)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]