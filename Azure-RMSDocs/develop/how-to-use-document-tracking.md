---
title: Come usare il rilevamento dei documenti | Azure RMS
description: La funzionalità di rilevamento dei documenti richiede la comprensione di alcuni aspetti semplici relativi alla gestione dei metadati associati e alla registrazione con il servizio.
keywords: ''
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 70E10936-7953-49B0-B0DC-A5E7C4772E60
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: a16425b891329e1cb7b8e2179c05bd0e8d6c3a93
ms.sourcegitcommit: 44ff610dec678604c449d42cc0b0863ca8224009
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39372870"
---
# <a name="how-to-use-document-tracking"></a>Procedura: Usare il rilevamento dei documenti

L'uso della funzionalità di rilevamento dei documenti richiede la comprensione di alcuni aspetti semplici relativi alla gestione dei metadati associati e alla registrazione con il servizio.

## <a name="managing-document-tracking-metadata"></a>Gestione dei metadati associati al rilevamento dei documenti

Tutti i sistemi operativi che supportano il rilevamento dei documenti presentano implementazioni simili, tra cui un set di proprietà che rappresentano i metadati, un nuovo parametro aggiunto ai metodi di creazione dei criteri utente e un metodo per la registrazione dei criteri di cui tenere traccia con il servizio di rilevamento dei documenti.

Dal punto di vista operativo, solo le proprietà relative al **nome contenuto** e al **tipo di notifica** sono necessarie per rilevamento dei documenti.

La sequenza di passaggi da usare per configurare il rilevamento dei documenti per un dato contenuto è la seguente:

-   Creare un oggetto **metadati di licenza** e impostare il **nome contenuto** e il **tipo di notifica**. Queste sono le uniche proprietà necessarie.
   - [LicenseMetadata](https://msdn.microsoft.com/library/mt573675.aspx) per Android
   -  [MSLicenseMetadata](https://msdn.microsoft.com/library/mt573683.aspx) per iOS

Scegliere il tipo di criterio: modello o ad hoc:
- Per il rilevamento dei documenti basato su modello, creare un oggetto **criteri utente** passando i metadati di licenza come parametro.
  - [UserPolicy.create](https://msdn.microsoft.com/library/dn790887.aspx) per Android
  - [MSUserPolicy.userPolicyWithTemplateDescriptor](https://msdn.microsoft.com/library/dn790808.aspx) per iOS

- Per il rilevamento dei documenti su base ad hoc, impostare la proprietà **metadati di licenza** sull’oggetto **descrittore criteri**.
  - [PolicyDescriptor.setLicenseMetadata](https://msdn.microsoft.com/library/mt573698.aspx) per Android
  - [MSPolicyDescriptor.licenseMetadata](https://msdn.microsoft.com/library/mt573693.aspx) per iOS

    **Nota** È possibile accedere direttamente all’oggetto  metadati di licenza solo durante il processo di configurazione del rilevamento dei documenti per i criteri utente specificati. Dopo la creazione dell'oggetto criteri utente, i metadati di licenza associati non sono accessibili, ad esempio la modifica dei valori dei metadati di licenza non produce alcun effetto.

     

-   Chiamare alla fine il metodo di registrazione alla piattaforma per il rilevamento dei documenti.
  - [UserPolicy.registerForDocTracking asynchronous](https://msdn.microsoft.com/library/mt573699.aspx) o [UserPolicy.registerForDocTracking synchronous](https://msdn.microsoft.com/library/mt631387.aspx) per Android
  - [MSUserPolicy.registerForDocTracking](https://msdn.microsoft.com/library/mt573694.aspx) per iOS
