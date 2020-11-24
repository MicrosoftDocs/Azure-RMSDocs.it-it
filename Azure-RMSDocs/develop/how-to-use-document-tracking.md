---
title: Come usare il rilevamento dei documenti | Azure RMS
description: La funzionalità di rilevamento dei documenti richiede la comprensione di alcuni aspetti semplici relativi alla gestione dei metadati associati e alla registrazione con il servizio.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 70E10936-7953-49B0-B0DC-A5E7C4772E60
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: dfcb4c616be2f5891b242a918a06abf2708c12cc
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "95568197"
---
# <a name="how-to-use-document-tracking"></a>Procedura: Usare il rilevamento dei documenti

[!INCLUDE [deprecation notice](../includes/deprecation-warning.md)]

L'uso della funzionalità di rilevamento dei documenti richiede la comprensione di alcuni aspetti semplici relativi alla gestione dei metadati associati e alla registrazione con il servizio.

## <a name="managing-document-tracking-metadata"></a>Gestione dei metadati associati al rilevamento dei documenti

Tutti i sistemi operativi che supportano il rilevamento dei documenti presentano implementazioni simili, tra cui un set di proprietà che rappresentano i metadati, un nuovo parametro aggiunto ai metodi di creazione dei criteri utente e un metodo per la registrazione dei criteri di cui tenere traccia con il servizio di rilevamento dei documenti.

Dal punto di vista operativo, solo le proprietà relative al **nome contenuto** e al **tipo di notifica** sono necessarie per rilevamento dei documenti.

La sequenza di passaggi da usare per configurare il rilevamento dei documenti per un dato contenuto è la seguente:

- Creare un oggetto **metadati di licenza** e impostare il **nome contenuto** e il **tipo di notifica**. Queste sono le uniche proprietà necessarie.
  - [LicenseMetadata](/previous-versions/windows/desktop/msipcthin2/licensemetadata-interface-java) per Android
  -  [MSLicenseMetadata](/previous-versions/windows/desktop/msipcthin2/mslicensemetadata-class-objc) per iOS

Scegliere il tipo di criterio: modello o ad hoc:
- Per il rilevamento dei documenti basato su modello, creare un oggetto **criteri utente** passando i metadati di licenza come parametro.
  - [UserPolicy.create](/previous-versions/windows/desktop/msipcthin2/userpolicy-class-java) per Android
  - [MSUserPolicy.userPolicyWithTemplateDescriptor](/previous-versions/windows/desktop/msipcthin2/msuserpolicy-templatedescriptor-property-objc) per iOS

- Per il rilevamento dei documenti su base ad hoc, impostare la proprietà **metadati di licenza** sull’oggetto **descrittore criteri**.
  - [PolicyDescriptor.setLicenseMetadata](/previous-versions/windows/desktop/msipcthin2/policydescriptor-setlicensemetadata-java) per Android
  - [MSPolicyDescriptor.licenseMetadata](/previous-versions/windows/desktop/msipcthin2/mspolicydescriptor-licensemetadata-property-objc) per iOS

    **Nota**    L'oggetto metadati di licenza è direttamente accessibile solo durante il processo di configurazione del rilevamento dei documenti per i criteri utente specificati. Dopo la creazione dell'oggetto criteri utente, i metadati di licenza associati non sono accessibili, ad esempio la modifica dei valori dei metadati di licenza non produce alcun effetto.

     

- Chiamare alla fine il metodo di registrazione alla piattaforma per il rilevamento dei documenti.
  - [UserPolicy.registerForDocTracking asynchronous](/previous-versions/windows/desktop/msipcthin2/userpolicy-registerfordoctracking-boolean--sting--authenticationcallback--creationcallback--java) o [UserPolicy.registerForDocTracking synchronous](/previous-versions/windows/desktop/msipcthin2/userpolicy-registerfordoctracking-synchronous-method-java) per Android
  - [MSUserPolicy.registerForDocTracking](/previous-versions/windows/desktop/msipcthin2/msuserpolicy-registerfordoctracking-userid-authenticationcallback-completionblock-method-objc) per iOS