---
title: Configurazione di applicazioni per Azure Rights Management - AIP
description: Istruzioni che consentono agli amministratori di configurare applicazioni e servizi per supportare il servizio di protezione Azure Rights Management per Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/11/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ea09cbc5-b98b-444e-8b60-5bc3cb199c36
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 1f8100e22f1608ebbd678ec5f97f77b4abd53ff0
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97383653"
---
# <a name="configuring-applications-for-azure-rights-management"></a>Configurazione di applicazioni per Rights Management di Windows Azure

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Pertinente per**: [AIP Unified Labeling client e client classico](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

> [!NOTE]
> Queste informazioni sono destinate agli amministratori e ai consulenti IT che hanno distribuito Azure Information Protection. Per informazioni su come usare la funzionalità Rights Management per una specifica applicazione o aprire un file protetto da diritti, vedere la guida e le informazioni aggiuntive fornite con l'applicazione.
>
> Ad esempio, per le applicazioni Office fare clic sull'icona della Guida e immettere i termini di ricerca, ad esempio **Rights Management** o **IRM**. Per il client Azure Information Protection per Windows, vedere la [Guida per l'utente del client Azure Information Protection](./rms-client/clientv2-user-guide.md).

Dopo aver distribuito Azure Information Protection per l'organizzazione, usare le informazioni seguenti per configurare le applicazioni, il client di Azure Information Protection e i servizi, ad esempio:

- **Applicazioni di Office**, ad esempio Word 2019, Word 2016 e Word 2013. 
- **Servizi**, ad esempio Exchange Online (regole di trasporto, prevenzione della perdita dei dati, non inoltri e crittografia dei messaggi) e Microsoft SharePoint (librerie protette). 

Per informazioni su come questi servizi e applicazioni supportano il servizio di protezione dei dati di Azure Information Protection, vedere [Supporto del servizio Azure Rights Management da parte delle applicazioni](applications-support.md).

> [!IMPORTANT]
> Per informazioni sulle versioni supportate e altri requisiti, vedere [requisiti per Azure Information Protection](requirements.md).

-   [Office 365: configurazione per Servizi online](configure-office365.md)

    -   [Exchange Online: configurazione di IRM](configure-office365.md#exchangeonline-irm-configuration)

    -   [SharePoint in Microsoft 365 e OneDrive: configurazione di IRM](configure-office365.md#sharepoint-in-microsoft-365-and-onedrive-irm-configuration)

- [Applicazioni di Office: configurazione dei client](configure-office-apps.md)

    -   [App di Office 365, Office 2019, Office 2016 e Office 2013](configure-office-apps.md#office365-apps-office-2019-office-2016-and-office-2013)

    -   [Office 2010](configure-office-apps.md#office2010)

-   [Client Azure Information Protection: installazione e configurazione dei client](configure-client.md)

Per configurare i server locali, ad esempio Exchange Server e SharePoint Server, vedere [Deploying the Azure Rights Management Connector](deploy-rms-connector.md).

Oltre a queste applicazioni e a questi servizi, esistono altre applicazioni che supportano le API di Rights Management. Questa categoria include le applicazioni line-of-business scritte internamente mediante Rights Management SDK, nonché le applicazioni di fornitori di software scritte mediante Rights Management SDK. Per tali applicazioni, seguire le istruzioni fornite con esse.

## <a name="next-steps"></a>Passaggi successivi

Dopo aver configurato le applicazioni per supportare il servizio Azure Rights Management, usare la Guida di [orientamento per la distribuzione di AIP per la classificazione, l'assegnazione di etichette e la protezione](deployment-roadmap-classify-label-protect.md) per verificare se è possibile eseguire altri passaggi di configurazione prima di distribuire Azure Information Protection a utenti e amministratori. 

Se tali operazioni non sono necessarie, possono risultare utili le informazioni operative seguenti:

- [Verifica del servizio Azure Rights Management](verify.md)

- [Consentire agli utenti di proteggere i file mediante il servizio Azure Rights Management](help-users.md)

- [Registrazione e analisi del servizio Azure Rights Management](log-analyze-usage.md)

- [Operazioni relative alla chiave del tenant di Azure Information Protection](operations-tenant-key.md)


