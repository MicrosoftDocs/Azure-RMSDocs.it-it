---
title: Applicazione Rights Management sharing&colon; installazione e configurazione dei client | Azure Information Protection
description: Informazioni per gli amministratori sulla distribuzione dell'applicazione Rights Management (RMS) sharing nei computer e nei dispositivi mobili Windows.
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: b9af5dc3-73d4-4147-b7ef-f6803b0d5216
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 635c499dfd2ec82064b659823117cd78b268e74c
ms.openlocfilehash: 200b64f0f6ea13890068cfe0bd2b3858b73b648e


---

# Applicazione Rights Management sharing: installazione e configurazione dei client

>*Si applica a: Azure Information Protection, Office 365*

L'applicazione Rights Management (RMS) sharing è necessaria affinché i computer client possano usare il servizio Azure Rights Management con Office 2010 ed è consigliata per tutti i computer e i dispositivi mobili che supportano il servizio Azure Rights Management di Azure Information Protection. L'applicazione RMS sharing si integra con le applicazioni di Office installando un componente aggiuntivo di Office per consentire agli utenti di proteggere con facilità i file e i messaggi di posta elettronica direttamente dalla barra multifunzione. Offre anche protezione generica per tipi di file non supportati in modalità nativa dal servizio Azure Rights Management e un sito per il rilevamento dei documenti che permette agli utenti di tenere traccia dei file protetti e di revocarli.

## Applicazione RMS sharing per Windows: installazione e configurazione
Per installare e configurare l'applicazione RMS sharing per Windows per una distribuzione aziendale, vedere l'articolo contenente la [guida dell'amministratore dell'applicazione Rights Management sharing](../rms-client/sharing-app-admin-guide.md).

> [!TIP]
> Se si vuole installare e testare rapidamente l'applicazione RMS sharing per un singolo computer, vedere la sezione relativa al [download e all'installazione dell'applicazione Rights Management sharing](../rms-client/install-sharing-app.md) nella [Guida dell'utente dell'applicazione Rights Management sharing](../rms-client/sharing-app-user-guide.md).

## Applicazione RMS sharing per piattaforme mobili: Installazione e gestione
Per installare l'applicazione RMS sharing per le piattaforme mobili, è possibile scaricare l'app rilevante usando i collegamenti disponibili nella [pagina di Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970). L'uso del servizio Azure Rights Management con questa app non richiede attività di configurazione.

> [!NOTE]
> L'applicazione RMS sharing per iOS e Android è stata sostituita dall'app Azure Information Protection.

**Se si dispone di Microsoft Intune**: poiché l'app Azure Information Protection include Microsoft Intune App Software Development Kit, quando i dispositivi iOS e Android sono registrati da Intune, è possibile distribuire e gestire l'app Azure Information Protection per questi dispositivi. Per altre informazioni, vedere l'articolo relativo alla [configurazione e distribuzione dei criteri di gestione delle applicazioni per dispositivi mobili nella console di Microsoft Intune](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console) nella documentazione di Intune Per il passaggio 2, usare le istruzioni per pubblicare un'app gestita da criteri.






<!--HONumber=Sep16_HO4-->


