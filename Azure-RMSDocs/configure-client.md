---
title: Client Azure Information Protection - Installare e configurare
description: Informazioni per gli amministratori sulla distribuzione del client Azure Information Protection in computer e dispositivi mobili Windows.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/05/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b1a19ae7-db26-40da-9e21-6620af3d0b02
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 79d4dbb1d6339f0261d57b32cf77addee9ca9744
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60180342"
---
# <a name="azure-information-protection-client-installation-and-configuration-for-clients"></a>Client Azure Information Protection: Installazione e configurazione dei client

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Nei computer con Office 2010 il client Azure Information Protection deve eseguire l'autenticazione nel servizio Azure Rights Management e nel servizio Azure Information Protection. Questo client è consigliato anche per tutti i computer Windows e i dispositivi iOS e Android che supportano il servizio Azure Rights Management e Azure Information Protection. 

Il client Azure Information Protection si integra con le applicazioni di Office tramite l'installazione di un componente aggiuntivo di Office, che permette agli utenti di applicare etichette e protezione a documenti e messaggi di posta elettronica in tutta semplicità direttamente dalla barra multifunzione di Office. Questo client offre anche etichette e protezione per tutti i tipi di file che non sono supportati in modo nativo dal servizio Azure Rights Management, un visualizzatore per i file protetti e un sito di rilevamento dei documenti che permette agli utenti di tenere traccia dei file che hanno protetto e revocarli.

## <a name="the-azure-information-protection-client-for-windows-installation-and-configuration"></a>Client Azure Information Protection per Windows: Installazione e configurazione

Per un'installazione e una configurazione a livello aziendale del client per Windows, vedere la [Guida dell'amministratore del client Azure Information Protection](./rms-client/client-admin-guide.md).

> [!TIP]
> Se si vuole installare e testare rapidamente il client Azure Information Protection per un singolo computer, vedere [Scaricare e installare il client di Azure Information Protection](./rms-client/install-client-app.md) nella [Guida per l'utente del client Azure Information Protection](./rms-client/client-user-guide.md).

## <a name="the-azure-information-protection-client-for-ios-and-android-installation-and-management"></a>Client Azure Information Protection per iOS e Android: Installazione e gestione

Per installare il client Azure Information Protection per queste piattaforme per dispositivi mobili comuni, è possibile scaricare l'app rilevante usando i collegamenti disponibili nella [pagina di Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970). Nessuna configurazione richiesta.

> [!NOTE]
> Per i computer Mac, i collegamenti contenuti in questa pagina consentono di scaricare l'app RMS sharing. Questi computer non supportano il client Azure Information Protection.

### <a name="integration-with-intune"></a>Integrazione con Intune

Poiché l'app Azure Information Protection usa Microsoft Intune App Software Development Kit, quando i dispositivi iOS e Android vengono registrati da Intune, è possibile distribuire e gestire l'app Azure Information Protection per questi dispositivi:

1. [Aggiungere l'app Azure Information Protection a Intune](/intune/apps-add) 

2. Eseguire una o entrambe le azioni seguenti:
    
    - Distribuire l'app [assegnandola agli utenti](/intune/apps-deploy)
    
    - Gestire l'app usando [criteri di protezione delle app](/intune/app-protection-policies)

Informazioni aggiuntive per l'aggiunta dell'app Azure Information Protection a Intune:

- Per iOS: cercare e aggiungere l'app da Intune.

- Per Android: quando si aggiunge l'app, usare l'**URL di App Store** seguente:
        
        https://play.google.com/store/apps/details?id=com.microsoft.ipviewer

Quando l'app Azure Information Protection viene configurata per un criterio di protezione delle app per dispositivi Android, oltre ad aprire documenti di testo, immagini e PDF protetti, quest'app può anche aprire file audio e video. Per altre informazioni, vedere [Visualizzare file multimediali con l'app Azure Information Protection](/intune/end-user-mam-apps-android#view-media-files-with-the-azure-information-protection-app).

## <a name="next-steps"></a>Passaggi successivi

Dopo aver installato e configurato il client Azure Information Protection, può essere necessario scoprire come il client interpreta i diversi diritti di utilizzo che possono essere usati per proteggere documenti e messaggi di posta elettronica. Per altre informazioni, vedere [Configurazione dei diritti di utilizzo per Azure Rights Management](configure-usage-rights.md).
