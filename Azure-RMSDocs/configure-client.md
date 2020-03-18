---
title: Client Azure Information Protection - Installare e configurare
description: Informazioni per gli amministratori sulla distribuzione dei client di Azure Information Protection su computer e dispositivi mobili Windows.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b1a19ae7-db26-40da-9e21-6620af3d0b02
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 2219c1267d9c271106a7605f1947990bd1ea21a6
ms.sourcegitcommit: 8c39347d9b7a120014120860fff89c5616641933
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/18/2020
ms.locfileid: "79482675"
---
# <a name="azure-information-protection-client-installation-and-configuration-for-clients"></a>Client Azure Information Protection: installazione e configurazione per i client

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

>[!NOTE] 
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client di Azure Information Protection client (versione classica)** e la **Gestione etichette** nel portale di Azure vengono **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

I computer che eseguono Office 2010 richiedono il client di Azure Information Protection (classico) o il Azure Information Protection client di etichetta unificata per l'autenticazione al servizio di Azure Information Protection.

Non si è certi della differenza tra questi due client?  Vedere [Qual è la differenza tra il client Azure Information Protection e il client di Azure Information Protection Unified Labeling?](faqs.md#whats-the-difference-between-azure-information-protection-and-microsoft-information-protection)

Questi client sono consigliati anche per tutti i computer Windows perché installano un componente aggiuntivo di Office in modo che gli utenti possano facilmente etichettare e proteggere i documenti e i messaggi di posta elettronica direttamente dalla barra multifunzione di Office. Questi client offrono anche l'assegnazione di etichette e la protezione per i tipi di file che non sono supportati in modalità nativa dal servizio di protezione (Rights Management di Azure) e un visualizzatore per i file protetti che non possono essere aperti dalle app di Office. È disponibile un visualizzatore simile per iOS e Android.

Il client classico supporta inoltre un sito di rilevamento dei documenti che consente agli utenti di rilevare e revocare i file protetti.

## <a name="the-azure-information-protection-client-for-windows-installation-and-configuration"></a>Client Azure Information Protection per Windows: installazione e configurazione

Per un'installazione e una configurazione aziendali del client per Windows, vedere le guide di amministrazione seguenti:

- Client per l'assegnazione di etichette unificata: [Azure Information Protection guida dell'amministratore client Unified Labeling](./rms-client/clientv2-admin-guide.md)] (./RMS-client/client-admin-guide.MD)

- Client classico: [Guida dell'amministratore del client Azure Information Protection](./rms-client/client-admin-guide.md)

Tuttavia, se si vuole installare e testare rapidamente questi client per un singolo computer, vedere le istruzioni seguenti dalle guide per gli utenti:

- Client con etichetta unificata: [scaricare e installare il client di etichettatura unificata di Azure Information Protection](./rms-client/install-unifiedlabelingclient-app.md)

- Client classico: [scaricare e installare il client di Azure Information Protection](./rms-client/install-client-app.md) dalla [Guida per l'utente del client Azure Information Protection](./rms-client/client-user-guide.md).

## <a name="the-azure-information-protection-app-for-ios-and-android-installation-and-management"></a>App Azure Information Protection per iOS e Android: installazione e gestione

Per installare il Visualizzatore app Azure Information Protection per iOS e Android, usare i collegamenti nella [pagina Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970). Nessuna configurazione richiesta.

> [!NOTE]
> Per i computer Mac, i collegamenti contenuti in questa pagina consentono di scaricare l'app RMS sharing. Questi computer non supportano il client Azure Information Protection.

### <a name="integration-with-intune"></a>Integrazione con Intune

Poiché l'app visualizzatore Azure Information Protection usa il Software Development Kit di Microsoft Intune app, quando i dispositivi iOS e Android sono registrati da Intune, è possibile distribuire e gestire l'app visualizzatore Azure Information Protection per questi dispositivi:

1. [Aggiungere l'app Azure Information Protection a Intune](/intune/apps-add) 

2. Eseguire una o entrambe le azioni seguenti:
    
    - Distribuire l'app [assegnandola agli utenti](/intune/apps-deploy)
    
    - Gestire l'app usando [criteri di protezione delle app](/intune/app-protection-policies)

Informazioni aggiuntive per l'aggiunta dell'app Azure Information Protection a Intune:

- Per iOS: cercare e aggiungere l'app da Intune.

- Per Android: quando si aggiunge l'app, usare l' **URL AppStore**seguente:
        
        https://play.google.com/store/apps/details?id=com.microsoft.ipviewer

Quando l'app Azure Information Protection viene configurata per un criterio di protezione delle app per dispositivi Android, oltre ad aprire documenti di testo, immagini e PDF protetti, quest'app può anche aprire file audio e video. Per altre informazioni, vedere [Visualizzare file multimediali con l'app Azure Information Protection](/intune/end-user-mam-apps-android#view-media-files-with-the-azure-information-protection-app).

## <a name="next-steps"></a>Passaggi successivi

Dopo aver installato e configurato Azure Information Protection client, potrebbe essere necessario ottenere ulteriori informazioni sul modo in cui il client interpreta i diversi diritti di utilizzo che possono essere utilizzati per proteggere documenti e messaggi di posta elettronica. Per altre informazioni, vedere [configurazione dei diritti di utilizzo per Azure Information Management](configure-usage-rights.md).
