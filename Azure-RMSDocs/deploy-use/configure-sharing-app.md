---
title: Applicazione di condivisione Rights Management&colon; installazione e configurazione dei client | Azure RMS
description: Informazioni per gli amministratori sulla distribuzione dell'applicazione Rights Management (RMS) sharing nei computer e nei dispositivi mobili Windows.
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: b9af5dc3-73d4-4147-b7ef-f6803b0d5216
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ad32910b482ca9d92b4ac8f3f123eda195db29cd
ms.openlocfilehash: c73529b39f31fc6d819a3123bbdc2416f2d996f4


---

# Applicazione Rights Management sharing: installazione e configurazione dei client

>*Si applica a: Azure Rights Management, Office 365*

L'applicazione di condivisione Rights Management (RMS) è necessaria affinché i computer client possano usare Azure RMS con Office 2010 ed è consigliata per tutti i computer e i dispositivi mobili che supportano Azure RMS. L'applicazione di condivisione RMS si integra con le applicazioni di Office installando un componente aggiuntivo di Office per consentire agli utenti di proteggere facilmente i file e i messaggi e-mail direttamente dalla barra multifunzione. Offre anche protezione generica per tipi di file non supportati in modalità nativa da Azure RMS e un sito per il rilevamento dei documenti che permette agli utenti di tenere traccia dei file protetti e di revocarli.

## Applicazione RMS sharing per Windows: installazione e configurazione
Per installare e configurare l'applicazione RMS sharing per Windows per una distribuzione aziendale, vedere l'articolo contenente la [guida dell'amministratore dell'applicazione Rights Management sharing](../rms-client/sharing-app-admin-guide.md).

> [!TIP]
> Se si vuole installare e testare rapidamente l'applicazione RMS sharing per un singolo computer, vedere la sezione relativa al [download e all'installazione dell'applicazione Rights Management sharing](../rms-client/install-sharing-app.md) nella [Guida dell'utente dell'applicazione Rights Management sharing](../rms-client/sharing-app-user-guide.md).

## Applicazione RMS sharing per piattaforme mobili: Installazione e gestione
Per installare l'applicazione RMS sharing per le piattaforme mobili, è possibile scaricare l'app rilevante usando i collegamenti disponibili nella [pagina di Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970). Non è necessaria alcuna configurazione per usare Azure RMS con questa app.

**Se si ha Microsoft Intune**: poiché l'app RMS sharing include il kit di distribuzione del software per l'app Microsoft Intune, sono disponibili le opzioni seguenti:

-   Per i dispositivi registrati da Intune, è possibile distribuire e gestire l'app RMS sharing per i dispositivi che eseguono iOS e Android. Per altre informazioni, vedere l'articolo relativo alla [configurazione e distribuzione dei criteri di gestione delle applicazioni per dispositivi mobili nella console di Microsoft Intune](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console) nella documentazione di Intune Per il passaggio 2, usare le istruzioni per pubblicare un'app gestita da criteri.

-   Per i dispositivi non registrati da Intune, è possibile gestire l'app RMS sharing per i dispositivi che eseguono Android. Per altre informazioni, vedere l'articolo relativo alla [creazione e distribuzione dei criteri di gestione delle app per dispositivi mobili con Microsoft Intune](/intune/deploy-use/create-and-deploy-mobile-app-management-policies-with-microsoft-intune).




<!--HONumber=Aug16_HO4-->


