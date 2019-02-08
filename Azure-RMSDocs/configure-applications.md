---
title: Configurazione di applicazioni per Azure Rights Management - AIP
description: Istruzioni che consentono agli amministratori di configurare applicazioni e servizi per supportare il servizio di protezione Azure Rights Management per Azure Information Protection. Ad esempio, le applicazioni di Office quali Word 2013 e Word 2010 e i servizi come Exchange Online (le regole di trasporto, la prevenzione della perdita di dati, l'opzione Non inoltrare e la crittografia messaggi) e SharePoint Online (librerie protette).
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/01/2019
ms.topic: conceptual
ms.service: information-protection
ms.assetid: ea09cbc5-b98b-444e-8b60-5bc3cb199c36
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 63444cf83ef6b4135d72fccea27baa4f4e0afa8c
ms.sourcegitcommit: 8558af7116f62414054feffa346aba197a1250d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2019
ms.locfileid: "55559547"
---
# <a name="configuring-applications-for-azure-rights-management"></a>Configurazione di applicazioni per Azure Rights Management

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

> [!NOTE]
> Queste informazioni sono destinate agli amministratori e ai consulenti IT che hanno distribuito Azure Information Protection. Per informazioni su come usare la funzionalità Rights Management per una specifica applicazione o aprire un file protetto da diritti, vedere la guida e le informazioni aggiuntive fornite con l'applicazione.
>
> Ad esempio, per le applicazioni Office fare clic sull'icona della Guida e immettere i termini di ricerca, ad esempio **Rights Management** o **IRM**. Per il client Azure Information Protection per Windows, vedere la [Guida per l'utente del client Azure Information Protection](./rms-client/client-user-guide.md).

Dopo avere distribuito Azure Information Protection per l'organizzazione, usare le informazioni seguenti per configurare le applicazioni, il client Azure Information Protection e i servizi. Ad esempio, le applicazioni di Office come Word 2016, Word 2013 e Word 2010 e i servizi come Exchange Online (regole di trasporto, prevenzione della perdita dei dati, opzione Non inoltrare e Message Encryption) e SharePoint Online (librerie protette). Per informazioni su come questi servizi e applicazioni supportano il servizio di protezione dei dati di Azure Information Protection, vedere [Supporto del servizio Azure Rights Management da parte delle applicazioni](applications-support.md).

> [!IMPORTANT]
> Per informazioni sulle versioni supportate e altri requisiti, vedere [Requisiti per Azure Rights Management](requirements.md).

-   [Office 365: configurazione di client e servizi online](configure-office365.md)

    -   [Exchange Online: configurazione di IRM](configure-office365.md#exchangeonline-irm-configuration)

    -   [SharePoint Online e OneDrive for Business: configurazione di IRM](configure-office365.md#sharepointonline-and-onedrive-for-business-irm-configuration)

- [Applicazioni Office: configurazione dei client](configure-office-apps.md)

    -   [Office 2016 e Office 2013](configure-office-apps.md#office2016-and-office-2013)

    -   [Office 2010](configure-office-apps.md#office2010)

-   [Client Azure Information Protection: installazione e configurazione dei client](configure-client.md)

Per configurare server locali quali Exchange Server e SharePoint Server, vedere l'articolo relativo alla [distribuzione del connettore Azure Rights Management](deploy-rms-connector.md).

Oltre a queste applicazioni e a questi servizi, esistono altre applicazioni che supportano le API di Rights Management. Questa categoria include le applicazioni line-of-business scritte internamente mediante Rights Management SDK, nonché le applicazioni di fornitori di software scritte mediante Rights Management SDK. Per tali applicazioni, seguire le istruzioni fornite con esse.

## <a name="next-steps"></a>Passaggi successivi
Dopo aver configurato le applicazioni per il supporto del servizio Azure Rights Management, usare la [Guida di orientamento per la distribuzione di Azure Information Protection](deployment-roadmap.md) per verificare se può essere necessario eseguire operazioni di configurazione aggiuntive prima di distribuire Azure Information Protection a utenti e amministratori. Se tali operazioni non sono necessarie, possono risultare utili le informazioni operative seguenti:

- [Verifica del servizio Azure Rights Management](verify.md)

- [Consentire agli utenti di proteggere i file mediante il servizio Azure Rights Management](help-users.md)

- [Registrazione e analisi del servizio Azure Rights Management](log-analyze-usage.md)

- [Operazioni relative alla chiave del tenant di Azure Information Protection](operations-tenant-key.md)


