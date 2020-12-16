---
title: Client Azure Information Protection - Installare e configurare
description: Informazioni per gli amministratori sulla distribuzione dei client di Azure Information Protection su computer e dispositivi mobili Windows.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/16/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b1a19ae7-db26-40da-9e21-6620af3d0b02
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 2da5d348f497a74e88c0bf11da023be6e3cb0152
ms.sourcegitcommit: efeb486e49c3e370d7fd8244687cd3de77cd8462
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/16/2020
ms.locfileid: "97583541"
---
# <a name="azure-information-protection-client-installation-and-configuration-for-clients"></a>Client Azure Information Protection: installazione e configurazione per i client

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Pertinente per**: [AIP Unified Labeling client e client classico](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE]
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Il client AIP Unified Labeling è consigliato per tutti i computer Windows, perché installa un componente aggiuntivo di Office che consente agli utenti di etichettare e proteggere facilmente i documenti direttamente dalla barra multifunzione di Office. 

Il client offre anche:

- Assegnazione di etichette e protezione per i tipi di file che non sono supportati dal servizio di protezione incorporato (Rights Management di Azure).
- Un visualizzatore per i file protetti che non possono essere aperti dalle app di Office. È disponibile un visualizzatore simile per iOS e Android.
- Funzionalità per il rilevamento e la revoca dell'accesso ai file protetti.

I computer che eseguono Office 2010 richiedono che il client di Azure Information Protection esegua l'autenticazione al servizio di Azure Information Protection. Per ulteriori informazioni, vedere [AIP per le versioni di Windows e Office nel supporto esteso](known-issues.md#aip-for-windows-and-office-versions-in-extended-support).
## <a name="the-azure-information-protection-client-for-windows-installation-and-configuration"></a>Client Azure Information Protection per Windows: installazione e configurazione

Per un'installazione e una configurazione aziendali del client di per Windows, vedere la [Guida dell'amministratore del client Azure Information Protection Unified Labeling](./rms-client/clientv2-admin-guide.md).

Se si vuole installare e testare rapidamente questi client per un singolo computer, vedere [scaricare e installare la Azure Information Protection Unified Labeling client](./rms-client/install-unifiedlabelingclient-app.md).

**Solo client classico**: se è installato il client classico, usare invece questi collegamenti:

- [Guida per l'amministratore del client di Azure Information Protection](./rms-client/client-admin-guide.md)
- [Scaricare e installare il client di Azure Information Protection](./rms-client/install-client-app.md).

## <a name="the-azure-information-protection-app-for-ios-and-android-installation-and-management"></a>App Azure Information Protection per iOS e Android: installazione e gestione

Per installare il Visualizzatore app Azure Information Protection per iOS e Android, usare i collegamenti nella [pagina Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970). Non è richiesta alcuna configurazione.

> [!NOTE]
> Per i computer Mac, i collegamenti contenuti in questa pagina consentono di scaricare l'app RMS sharing. Questi computer non supportano il client Azure Information Protection.

### <a name="integration-with-intune"></a>Integrazione con Intune

Poiché l'app visualizzatore Azure Information Protection usa il Software Development Kit di Microsoft Intune app, quando i dispositivi iOS e Android sono registrati da Intune, è possibile distribuire e gestire l'app visualizzatore Azure Information Protection per questi dispositivi:

1. [Aggiungere l'app Azure Information Protection a Intune](/intune/apps/apps-add)

2. Eseguire una o entrambe le azioni seguenti:

    - Distribuire l'app [assegnandola agli utenti](/intune/apps/apps-deploy)

    - Gestire l'app usando [criteri di protezione delle app](/intune/apps/app-protection-policies)

Informazioni aggiuntive per l'aggiunta dell'app Azure Information Protection a Intune:

- Per iOS: cercare e aggiungere l'app da Intune.

- Per Android: quando si aggiunge l'app, usare l' **URL AppStore** seguente:

    ```md
    https://play.google.com/store/apps/details?id=com.microsoft.ipviewer
    ```

Quando l'app Azure Information Protection viene configurata per un criterio di protezione delle app per dispositivi Android, oltre ad aprire documenti di testo, immagini e PDF protetti, quest'app può anche aprire file audio e video. Per altre informazioni, vedere [Visualizzare file multimediali con l'app Azure Information Protection](/intune/fundamentals/end-user-mam-apps-android#view-media-files-with-the-azure-information-protection-app).

## <a name="next-steps"></a>Passaggi successivi

Dopo aver installato e configurato Azure Information Protection client, potrebbe essere necessario ottenere ulteriori informazioni sul modo in cui il client interpreta i diversi diritti di utilizzo che possono essere utilizzati per proteggere documenti e messaggi di posta elettronica. Per altre informazioni, vedere [configurazione dei diritti di utilizzo per Azure Information Management](configure-usage-rights.md).
