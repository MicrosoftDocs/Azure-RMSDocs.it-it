---
title: Client Azure Information Protection &colon; installazione e configurazione
description: Informazioni per gli amministratori sulla distribuzione del client Azure Information Protection in computer e dispositivi mobili Windows.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: b1a19ae7-db26-40da-9e21-6620af3d0b02
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 54e66d8ffde33e3e73b24e39fa609686fa2601b0
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
ms.locfileid: "30204799"
---
# <a name="azure-information-protection-client-installation-and-configuration-for-clients"></a>Client Azure Information Protection: installazione e configurazione per i client

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Nei computer con Office 2010 è necessario installare il client Azure Information Protection (o l'applicazione di condivisione Rights Management) per l'autenticazione al servizio Azure Rights Management e al servizio Azure Information Protection. Questo client è consigliato anche per tutti i computer Windows e i dispositivi iOS e Android che supportano il servizio Azure Rights Management e Azure Information Protection. 

Il client Azure Information Protection si integra con le applicazioni di Office tramite l'installazione di un componente aggiuntivo di Office, che permette agli utenti di applicare etichette e protezione a documenti e messaggi di posta elettronica in tutta semplicità direttamente dalla barra multifunzione di Office. Questo client offre anche etichette e protezione per tutti i tipi di file che non sono supportati in modo nativo dal servizio Azure Rights Management, un visualizzatore per i file protetti e un sito di rilevamento dei documenti che permette agli utenti di tenere traccia dei file che hanno protetto e revocarli.

## <a name="the-azure-information-protection-client-for-windows-installation-and-configuration"></a>Client Azure Information Protection per Windows: installazione e configurazione
Per un'installazione e una configurazione a livello aziendale del client per Windows, vedere la [Guida dell'amministratore del client Azure Information Protection](../rms-client/client-admin-guide.md).

> [!TIP]
> Se si vuole installare e testare rapidamente il client Azure Information Protection per un singolo computer, vedere [Scaricare e installare il client di Azure Information Protection](../rms-client/install-client-app.md) nella [Guida per l'utente del client Azure Information Protection](../rms-client/client-user-guide.md).

## <a name="the-azure-information-protection-client-for-ios-and-android-installation-and-management"></a>Client Azure Information Protection per iOS e Android: installazione e gestione
Per installare il client Azure Information Protection per queste piattaforme per dispositivi mobili comuni, è possibile scaricare l'app rilevante usando i collegamenti disponibili nella [pagina di Azure Information Protection](http://go.microsoft.com/fwlink/?LinkId=303970). Nessuna configurazione richiesta.

> [!NOTE]
> Per computer Mac e dispositivi Windows Phone, i collegamenti contenuti in questa pagina permettono di scaricare le app RMS sharing per dispositivi mobili. Attualmente questi dispositivi non supportano il client Azure Information Protection.

**Se è installato Microsoft Intune**: poiché l'app Azure Information Protection include Microsoft Intune App Software Development Kit, quando i dispositivi iOS e Android sono registrati da Intune, è possibile distribuire e gestire il visualizzatore Azure Information Protection per questi dispositivi. Per altre informazioni, vedere l'articolo relativo alla [configurazione e distribuzione dei criteri di gestione delle applicazioni per dispositivi mobili nella console di Microsoft Intune](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console) nella documentazione di Intune Per il passaggio 2, usare le istruzioni per pubblicare un'app gestita da criteri.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


