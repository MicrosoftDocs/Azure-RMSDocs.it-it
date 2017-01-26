---
title: Applicazione Rights Management sharing&colon; installazione e configurazione dei client | Azure Information Protection
description: Informazioni per gli amministratori sulla distribuzione dell&quot;applicazione Rights Management (RMS) sharing nei computer e nei dispositivi mobili Windows.
author: cabailey
ms.author: cabailey
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
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 0d15a232bc1f0b1bce94e48c7e9c6f6b9419b5dd


---

# <a name="rights-management-sharing-application-installation-and-configuration-for-clients"></a>Applicazione Rights Management sharing: installazione e configurazione dei client

>*Si applica a: Azure Information Protection, Office 365*

L'applicazione Rights Management (RMS) sharing è necessaria affinché i computer client possano usare il servizio Azure Rights Management con Office 2010 ed è consigliata per tutti i computer e i dispositivi mobili che supportano il servizio Azure Rights Management di Azure Information Protection. L'applicazione RMS sharing si integra con le applicazioni di Office installando un componente aggiuntivo di Office per consentire agli utenti di proteggere con facilità i file e i messaggi di posta elettronica direttamente dalla barra multifunzione. Offre anche protezione generica per tipi di file non supportati in modalità nativa dal servizio Azure Rights Management e un sito per il rilevamento dei documenti che permette agli utenti di tenere traccia dei file protetti e di revocarli.

## <a name="the-rms-sharing-application-for-windows-installation-and-configuration"></a>Applicazione RMS sharing per Windows: installazione e configurazione
Per installare e configurare l'applicazione RMS sharing per Windows per una distribuzione aziendale, vedere l'articolo contenente la [guida dell'amministratore dell'applicazione Rights Management sharing](../rms-client/sharing-app-admin-guide.md).

> [!TIP]
> Se si vuole installare e testare rapidamente l'applicazione RMS sharing per un singolo computer, vedere la sezione relativa al [download e all'installazione dell'applicazione Rights Management sharing](../rms-client/install-sharing-app.md) nella [Guida dell'utente dell'applicazione Rights Management sharing](../rms-client/sharing-app-user-guide.md).

## <a name="the-rms-sharing-application-for-mobile-platforms-installation-and-management"></a>Applicazione RMS sharing per piattaforme mobili: Installazione e gestione
Per installare l'applicazione RMS sharing per le piattaforme mobili, è possibile scaricare l'app rilevante usando i collegamenti disponibili nella [pagina di Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970). L'uso del servizio Azure Rights Management con questa app non richiede attività di configurazione.

> [!NOTE]
> L'applicazione RMS sharing per iOS e Android è stata sostituita dall'app Azure Information Protection.

**Se si dispone di Microsoft Intune**: poiché l'app Azure Information Protection include Microsoft Intune App Software Development Kit, quando i dispositivi iOS e Android sono registrati da Intune, è possibile distribuire e gestire l'app Azure Information Protection per questi dispositivi. Per altre informazioni, vedere l'articolo relativo alla [configurazione e distribuzione dei criteri di gestione delle applicazioni per dispositivi mobili nella console di Microsoft Intune](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console) nella documentazione di Intune Per il passaggio 2, usare le istruzioni per pubblicare un'app gestita da criteri.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]





<!--HONumber=Jan17_HO4-->


