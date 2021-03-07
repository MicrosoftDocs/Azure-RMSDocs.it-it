---
title: Visualizzatori PDF protetti per Microsoft Information Protection
description: Informazioni su come aprire e visualizzare i file PDF etichettati per la classificazione e la protezione.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 10/29/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: aab59e02-930b-4a17-8442-2d5d081fe1a6
ms.reviewer: kartikka
ms.suite: ems
ms.custom: user
search.appverid:
- MET150
ms.openlocfilehash: c982293c4b6544e0bc093caef5a94596660bfcb5
ms.sourcegitcommit: 74b8d03d1ede3da12842b84546417e63897778bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/07/2021
ms.locfileid: "102415382"
---
# <a name="which-pdf-readers-are-supported-for-protected-pdfs"></a>Quali lettori PDF sono supportati per i PDF protetti?

>***Si applica a**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***Rilevante per**: [Client di etichettatura unificata e client classico di AIP](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE]
> Per offrire un'esperienza per i clienti unificata e semplificata, il **client classico di Azure Information Protection** e **Gestione etichette** nel portale di Azure saranno **deprecati** a partire dal **31 marzo 2021**. In questo intervallo di tempo tutti i clienti correnti di Azure Information Protection possono passare alla soluzione di etichettatura unificata usando la piattaforma di etichettatura unificata di Microsoft Information Protection. Altre informazioni nell'[avviso ufficiale sulla deprecazione](https://aka.ms/aipclassicsunset).

Questo articolo descrive i Reader PDF protetti supportati per Azure Information Protection (AIP). I lettori PDF protetti consentono agli utenti di aprire i file PDF crittografati e visualizzare le informazioni riservate contenute.

La crittografia dei file PDF con AIP garantisce che utenti non autorizzati non possano leggere il contenuto del file. Lettori PDF protetti che supportano AIP verificare che siano state concesse le autorizzazioni per aprire il documento e decrittografare anche il contenuto.

Ad esempio, l'immagine seguente mostra un documento crittografato aperto in Adobe Acrobat Reader. La barra nella parte superiore indica che il documento è protetto da una soluzione di Information Protection Microsoft.

:::image type="content" source="../media/protected-pdf-in-adobe-reader.png" alt-text="PDF protetto aperto in Adobe Acrobat Reader":::

Per istruzioni, vedere le sezioni seguenti:

- [Visualizzazione di PDF protetti in Microsoft Edge in Windows o Mac](#viewing-protected-pdfs-in-microsoft-edge-on-windows-or-mac)

- [Installazione di un lettore PDF protetto per Windows o Mac](#installing-a-protected-pdf-reader-for-windows-or-mac)

- [Installazione di un lettore PDF protetto per dispositivi mobili (iOS/Android)](#installing-a-protected-pdf-reader-for-mobile-iosandroid)

> [!TIP]
> Se il documento non viene aperto dopo l'installazione di un reader consigliato, è possibile che il documento sia protetto in un formato precedente. 
>
> In questo caso, provare uno dei lettori elencati come supportato per i formati precedenti. Per ulteriori informazioni, vedere [supporto per i formati precedenti](#support-for-previous-formats).
> 
### <a name="iso-standards-for-pdf-encryption"></a>Standard ISO per la crittografia PDF

I lettori PDF a cui viene fatto riferimento in questa pagina possono aprire tutti i documenti protetti che rispettano lo standard ISO per la crittografia PDF. 

Questo standard viene usato per impostazione predefinita dal client AIP.

> [!NOTE]
> **Solo client classico**: se si dispone del client AIP classico, questo potrebbe essere stato [disabilitato da un amministratore](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption).
> 

### <a name="viewing-protected-pdfs-in-adobe-acrobat-reader"></a>Visualizzazione di PDF protetti in Adobe Acrobat Reader

Adobe Acrobat Reader si integra con le soluzioni Information Protection Microsoft, ad esempio Azure Information Protection per offrire agli utenti un'esperienza semplificata e coerente per i file PDF classificati e/o protetti.

Adobe Acrobat Reader con Microsoft Information Protection Integration è supportato per [Windows](#installing-a-protected-pdf-reader-for-windows-or-mac) e [MacOS](#installing-a-protected-pdf-reader-for-windows-or-mac).

Per ulteriori informazioni, vedere i post di Blog seguenti: 

- [Disponibilità generale dell'integrazione di Adobe Acrobat Reader con Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-Integration-with/ba-p/298396)

- [Domande frequenti sull'integrazione di Adobe Reader e Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Microsoft-Information-Protection/Adobe-reader-and-Microsoft-Information-Protection-integration/ba-p/482219)

## <a name="viewing-protected-pdfs-in-microsoft-edge-on-windows-or-mac"></a>Visualizzazione di PDF protetti in Microsoft Edge in Windows o Mac

Microsoft Edge offre supporto incorporato per la visualizzazione di file PDF classificati e protetti. L'uso di Microsoft Edge garantisce che gli utenti possano aprire facilmente i file PDF protetti senza dover installare o configurare software o impostazioni aggiuntive.

Le versioni supportate includono:

- **Windows**: Windows 10 e versioni precedenti attraverso Windows 8. 
    
    Per ulteriori informazioni sulle versioni precedenti, vedere [supporto per i formati precedenti](#support-for-previous-formats).

- **Mac**: versioni MacOS 10,12 e successive 


**Istruzioni**: 

1. Verificare quale [versione di Microsoft Edge](https://support.microsoft.com/help/4027011/microsoft-edge-find-out-which-version-you-have) è installata nel sistema. 
1. Se la versione di Microsoft Edge è 83.0.478.37 o successiva, è possibile aprire i file protetti direttamente nel browser Microsoft Edge. 

1. Per aprire i file PDF in SharePoint, fare clic su **Apri**  >  **Apri nel browser**. 

    :::image type="content" source="../media/edge_open_browser.png" alt-text="Aprire un file PDF protetto usando Microsoft Edge dal browser usando l'opzione Apri nel browser":::
 
## <a name="installing-a-protected-pdf-reader-for-windows-or-mac"></a>Installazione di un lettore PDF protetto per Windows o Mac

Per aprire un documento PDF protetto sul computer desktop, si consiglia di installare il [plug-in Microsoft Information Protection (MIP) pertinente per Acrobat e Acrobat Reader](https://go.microsoft.com/fwlink/?linkid=2050049) per il sistema operativo in uso.

**Istruzioni**:

1. Se non è già stato fatto, installare Adobe Reader dal [sito di Adobe](https://www.adobe.com/).

    Assicurarsi di leggere e accettare le [condizioni d'uso generali di Adobe](https://www.adobe.com/legal/terms.html).

1. Installare il [plug-in MIP per Acrobat e Acrobat Reader](https://go.microsoft.com/fwlink/?linkid=2050049) per il sistema operativo in uso.  

    Le versioni supportate includono:

    - **Windows**: Windows 10 e versioni precedenti attraverso Windows 8. 
    
        Per ulteriori informazioni sulle versioni precedenti, vedere [supporto per i formati precedenti](#support-for-previous-formats).

    - **Mac**: versioni MacOS 10,12-10,14 

1. Se viene richiesta l'approvazione dell'amministratore, chiedere all'amministratore di autorizzare il plug-in.

    Ad esempio:
    
    :::image type="content" source="../media/admin-approval-for-mip-in-adobe-reader.png" alt-text="Approvazione dell'amministratore necessaria per installare il plug-in MIP per Acrobat e Acrobat Reader":::
    
> [!NOTE]
> Per ulteriori informazioni, vedere l' [annuncio Microsoft Information Protection e Adobe Release](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-integration-with/ba-p/298396).
> 

### <a name="alternative-protected-pdf-readers-for-windows"></a>Lettori PDF protetti alternativi per Windows

In alternativa, usare uno dei lettori PDF seguenti per Windows che aderiscono allo standard ISO per la crittografia PDF:

- [Visualizzatore di Azure Information Protection](https://go.microsoft.com/fwlink/?linkid=838993) 

- [Lettore Foxit](https://www.foxitsoftware.com/pdf-reader/)

## <a name="installing-a-protected-pdf-reader-for-mobile-iosandroid"></a>Installazione di un lettore PDF protetto per dispositivi mobili (iOS/Android)

Per aprire un file PDF protetto nel dispositivo iOS o Android, scaricare e installare l'app per il sistema operativo in uso:

|OS  |Collegamento  |
|---------|---------|
|**iTunes**     | [![Eseguire l'installazione da iTunes.](../media/small/ios-icon-small.png)](https://apps.apple.com/app/microsoft-rights-management/id689516635)        |
|**Google Play**     |[![Installare da Google Play.](../media/small/android-icon-small.png)](https://play.google.com/store/apps/details?id=com.microsoft.ipviewer)         |
| | |

Per altre informazioni, vedere [app del visualizzatore per dispositivi mobili per Azure Information Protection (iOS e Android)](mobile-app-faq.md).

## <a name="support-for-previous-formats"></a>Supporto per i formati precedenti

I lettori PDF seguenti supportano sia i file PDF protetti con estensione **Ppdf** che i formati precedenti con estensione **PDF** .

Se non si è in grado di aprire il file PDF protetto usando il lettore consigliato, il documento potrebbe essere protetto in un formato precedente. Ad esempio, in Microsoft SharePoint viene attualmente utilizzato un formato precedente per i documenti PDF nelle librerie protette con IRM.

- **Windows 10/versioni precedenti tramite Windows 7 Service Pack 1**

    - [Visualizzatore di Azure Information Protection](https://go.microsoft.com/fwlink/?linkid=838993)
    - Gaaiho Doc
    - GigaTrust Desktop PDF Client for Adobe
    - Foxit Reader
    - Nitro PDF Reader
    - Nuance Power PDF
    - Cromo perimetrale

- **Android**:

    - [App Azure Information Protection](mobile-app-faq.md)
    - Foxit MobilePDF with RMS
    - GigaTrust App for Android

- **iOS**:

    - [App Azure Information Protection](mobile-app-faq.md)
    - Foxit MobilePDF with RMS
    - TITUS Docs

- **MacOS Catalina**: cromo perimetrale

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni dopo l'installazione di, utilizzare le istruzioni e la documentazione per ogni lettore. Vedere ad esempio gli articoli seguenti:

- [Guida dell'utente: visualizzare i file protetti con il client di Azure Information Protection Unified Labeling](clientv2-view-use-files.md)
- [App del visualizzatore per dispositivi mobili per Azure Information Protection (iOS e Android)](mobile-app-faq.md)