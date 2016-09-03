---
title: Applicazione di condivisione Rights Management&colon; Cronologia delle versioni | Azure RMS
description: "Il team di Rights Management aggiorna regolarmente l'applicazione di condivisione di condivisione Rights Management con correzioni e nuove funzionalità. Usare le informazioni seguenti per visualizzare gli elementi nuovi o modificati in una versione. La versione più recente è elencata per prima."
author: cabailey
manager: mbaldwin
ms.date: 07/13/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 6751bd90-959f-4eba-91ed-6588ac983762
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 26b043f1f9e7a1e0cd00c2f31c28f7d6685f0232
ms.openlocfilehash: 060324fd6f0a87839ff267b540b9e5024498c242


---

# Applicazione di condivisione Rights Management: Cronologia delle versioni

>*Si applica a: Active Directory Rights Management Services, Azure Rights Management, Windows 10, Windows 7 con SP1, Windows 8, Windows 8.1*

Il team di Rights Management aggiorna regolarmente l'applicazione di condivisione di condivisione Rights Management con correzioni e nuove funzionalità. Utilizzare le informazioni seguenti per visualizzare gli elementi nuovi o modificati in una versione. La versione più recente è elencata per prima.

Non sono elencate le versioni precedenti al 1 gennaio 2015.

> [!NOTE]
> Per commenti o domande sull'applicazione di RMS sharing, inviare un messaggio di posta elettronica a [AskIPTeam](mailto:AskIPTeam@microsoft.com?subject=RMS%20sharing%20app:%20Feedback%20or%20question).

## Versione 1.0.2217.0

**Rilasciata**: 13/07/2016

**Correzioni**:

- Per gli utenti di organizzazioni che usano la federazione e l'autenticazione a più fattori non viene più visualizzato l'errore 0x800704DC quando proteggono il contenuto.



## Versione 1.0.2191.0
**Rilasciata il**: 16/06/2016

**Correzioni**:

- Il sito del rilevamento dei documenti ora specifica il numero di visualizzazioni corretto per ogni documento rilevato.

- I modelli per tutte le impostazioni locali vengono ora visualizzati come disponibili agli utenti.

- Dopo aver usato Condividi file protetto per un file di PowerPoint, le modifiche apportate alla versione locale del file ora vengono salvate correttamente.

- Risoluzione di alcuni bug minori e miglioramenti per i messaggi di errore.


## Versione 1.0.2004.0
**Rilasciata**: 11/12/2015

**Correzioni**:

-   Solo il proprietario dei file e le persone con livelli di autorizzazione **Comproprietario** possono rimuovere la protezione di file. In precedenza, potevano rimuovere la protezione di file il proprietario e le persone con livelli di autorizzazione **Coautore** e **Comproprietario**.

-   Protezione nativa per file con estensione **tif** (oltre ai file con estensione tiff), per produrre un file con estensione **ptif** di sola lettura protetto tramite RMS.

-   Miglioramenti relativi ai messaggi di errore (precisione e chiarezza).

-   Miglioramenti di prestazioni durante la crittografia e la decrittografia di contenuti.

**Nuove funzionalità**:

-   Supporto per l'installazione da parte di utenti non amministratori, in modo che anche utenti standard possano installare l'applicazione di condivisione RMS.

    Sono tuttavia previste alcune limitazioni per gli utenti standard che eseguono Office 2010. Per altre informazioni, vedere la sezione relativa agli [utenti che non sono amministratori locali e usano Office 2010](install-sharing-app.md#if-you-are-not-a-local-administrator-and-use-office-2010) nelle istruzioni utente [Scaricare e installare l'applicazione Rights Management sharing](install-sharing-app.md).

## Versione 1.0.1908.0
**Rilasciata**: 16/9/2015

**Correzioni**:

-   Supporto per Multi-Factor Authentication (MFA) per Azure RMS, che rimuove inoltre la dipendenza dall’Assistente per l'accesso Microsoft per applicazioni che utilizzano l’autenticazione moderna.

    Per altre informazioni, vedere la sezione [Multi-Factor Authentication (MFA) e Azure RMS](../get-started/requirements-azure-ad.md#multi-factor-authentication-mfa-and-azure-rms) di [Requisiti per Azure Rights Management](../get-started/requirements-azure-rms.md).

## Versione 1.0.1784.0
**Rilasciata**: 30/7/2015

**Correzioni**:

-   L'intervallo di aggiornamento predefinito per i modelli di criteri viene ridotto da 7 giorni per 1 giorno.

-   Numero inferiore di regressioni e bug secondari.

## Versione 1.0.1770.0
**Rilasciata**: 25/4/2015

**Correzioni**:

-   A questo punto, solo i proprietari e i comproprietari possono rimuovere la protezione, non i co-autori.

-   Ora è possibile proteggere i file che si trovano in una condivisione di rete.

**Nuove funzionalità**:

-   Supporto per rilevamento e revoca dei documenti. Per altre informazioni, vedere [Rilevare e revocare i documenti quando si usa l'applicazione RMS sharing](sharing-app-track-revoke.md).

-   Il supporto del modello quando si sceglie **Condividi file protetto**:

    -   Ora è possibile selezionare i modelli.

    -   Anziché il dispositivo di scorrimento, verranno visualizzati una casella di riepilogo che include i modelli e le autorizzazioni personalizzate.

    -   Non si visualizzano più le opzioni per **Consenti consumo su tutti i dispositivi** e **Applica restrizioni d'uso**. Al contrario, **Protezione generica** viene selezionato automaticamente in base al tipo di file.

    Per altre informazioni, vedere [Opzioni della finestra di dialogo per l'applicazione Rights Management sharing](sharing-app-dialog-box.md).

## Versione 1.0.1667.0
**Rilasciata**: 19/1/2015

**Correzioni**:

-   Supporto per i caratteri in cinese nel visualizzatore PPDF dell’app di RMS sharing.

-   Miglioramento della gestione degli errori e della messaggistica.

-   Correggere un problema con la notifica di aggiornamento automatico quando è disponibile per il download una versione più recente dell'applicazione.

**Nuove funzionalità**:

-   **Supporto per più domini di posta elettronica all'interno dell'organizzazione**: se si usa AD RMS e gli utenti dell'organizzazione dispongono di più domini di posta elettronica, questo aggiornamento consente loro di utilizzare contenuti protetti dagli utenti dell'organizzazione in altri domini. Per altre informazioni, vedere la sezione [Solo AD RMS: Supporto per più domini di posta elettronica all'interno dell'organizzazione](sharing-app-admin-guide.md#ad-rms-only-support-for-multiple-email-domains-within-your-organization) della [Guida dell'amministratore dell'applicazione Rights Management sharing](sharing-app-admin-guide.md).




<!--HONumber=Aug16_HO4-->


