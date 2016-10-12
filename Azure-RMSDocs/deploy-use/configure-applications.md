---
title: Configurazione di applicazioni per il servizio Azure Rights Management | Azure Information Protection
description: Istruzioni che consentono agli amministratori di configurare applicazioni e servizi per supportare il servizio di protezione Azure Rights Management per Azure Information Protection. Ad esempio, le applicazioni di Office quali Word 2013 e Word 2010 e i servizi come Exchange Online (le regole di trasporto, la prevenzione della perdita di dati, l'opzione Non inoltrare e la crittografia messaggi) e SharePoint Online (librerie protette).
author: cabailey
manager: mbaldwin
ms.date: 10/05/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ea09cbc5-b98b-444e-8b60-5bc3cb199c36
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9dee9e7c925258ffd3cd9e783582733e9518d3fa
ms.openlocfilehash: d141bf56515853f7b6fddda1ddf150b8d3730b78


---

# Configurazione di applicazioni per Azure Rights Management

>*Si applica a: Azure Information Protection, Office 365*

> [!NOTE]
> Queste informazioni sono destinate agli amministratori e ai consulenti IT che hanno distribuito Azure Information Protection. Per informazioni su come usare la funzionalità Rights Management per una specifica applicazione o aprire un file protetto da diritti, vedere la guida e le informazioni aggiuntive fornite con l'applicazione.
>
> Ad esempio, per le applicazioni Office fare clic sull'icona della Guida e immettere i termini di ricerca, ad esempio **Rights Management** o **IRM**. Per l'applicazione RMS sharing per Windows, vedere la [Guida dell'utente dell'applicazione Rights Management sharing](../rms-client/sharing-app-user-guide.md).

Dopo avere distribuito Azure Information Protection per l'organizzazione, usare le informazioni seguenti per configurare applicazioni e servizi per il supporto del servizio Azure Rights Management di Azure Information Protection. Sono incluse le applicazioni di Office quali Word 2013 e Word 2010 e i servizi come Exchange Online (le regole di trasporto, la prevenzione della perdita di dati, l'opzione Non inoltrare e la crittografia messaggi) e SharePoint Online (librerie protette). Per informazioni sul supporto di Rights Management da parte di queste applicazioni e di questi servizi, vedere [Supporto del servizio Azure Rights Management da parte delle applicazioni](../understand-explore/applications-support.md).

> [!IMPORTANT]
> Per informazioni sulle versioni supportate e altri requisiti, vedere [Requisiti per Azure Rights Management](../get-started/requirements-azure-rms.md).

-   [Office 365: configurazione di client e servizi online](configure-office365.md)

    -   [Exchange Online: configurazione di IRM](configure-office365.md#exchange-online-irm-configuration)

    -   [SharePoint Online e OneDrive for Business: configurazione di IRM](configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration)

- [Applicazioni di Office: configurazione dei client](configure-office-apps.md)

    -   [Office 2016 e Office 2013](configure-office-apps.md#office-2016-and-office-2013)

    -   [Office 2010](configure-office-apps.md#office-2010)

-   [Applicazione Rights Management sharing: installazione e configurazione dei client](configure-sharing-app.md)

    -   [Applicazione RMS sharing per Windows: installazione e configurazione](configure-sharing-app.md#the-rms-sharing-application-for-windows-installation-and-configuration)

    -   [Applicazione RMS sharing per piattaforme mobili: Installazione e gestione](configure-sharing-app.md#the-rms-sharing-application-for-mobile-platforms-installation-and-management)


Per configurare server locali quali Exchange Server e SharePoint Server, vedere l'articolo relativo alla [distribuzione del connettore Azure Rights Management](deploy-rms-connector.md).

> [!TIP]
> Per esempi generali e screenshot delle applicazioni configurate per l'uso del servizio Azure Rights Management, vedere [Azure RMS in azione: Cosa vedono gli amministratori e gli utenti](../understand-explore/what-admins-users-see.md).


Oltre a queste applicazioni e a questi servizi, esistono altre applicazioni che supportano le API di Rights Management. Questa categoria include le applicazioni line-of-business scritte internamente mediante Rights Management SDK, nonché le applicazioni di fornitori di software scritte mediante Rights Management SDK. Per tali applicazioni, seguire le istruzioni fornite con esse.

## Passaggi successivi
Dopo aver configurato le applicazioni per il supporto del servizio Azure Rights Management, usare la [Guida di orientamento per la distribuzione di Azure Information Protection](../plan-design/deployment-roadmap.md) per verificare se può essere necessario eseguire operazioni di configurazione aggiuntive prima di distribuire Azure Information Protection a utenti e amministratori. Se tali operazioni non sono necessarie, possono risultare utili le informazioni operative seguenti:

- [Verifica del servizio Azure Rights Management](verify.md)

- [Consentire agli utenti di proteggere i file mediante il servizio Azure Rights Management](help-users.md)

- [Registrazione e analisi del servizio Azure Rights Management](log-analyze-usage.md)

- [Operazioni relative alla chiave del tenant di Azure Information Protection](operations-tenant-key.md)





<!--HONumber=Sep16_HO5-->


