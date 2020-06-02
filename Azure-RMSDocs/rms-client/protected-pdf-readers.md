---
title: Lettori di file PDF protetti per Microsoft Information Protection
description: Installare un Reader per documenti PDF etichettati per la classificazione e la protezione
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 05/26/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: aab59e02-930b-4a17-8442-2d5d081fe1a6
ms.reviewer: kartikka
ms.suite: ems
ms.custom: user
search.appverid:
- MET150
ms.openlocfilehash: 755424c1f3c813ca517ae4afcbe1e4d7a134276f
ms.sourcegitcommit: fa16364879823b86b4e56ac18a1fc8de5a5dae57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/01/2020
ms.locfileid: "84250048"
---
# <a name="pdf-readers-that-support-microsoft-information-protection"></a>Lettori PDF che supportano Microsoft Information Protection

Se è necessario aprire un documento PDF protetto da Microsoft Information Protection, usare i collegamenti e le informazioni seguenti.

Un documento PDF protetto potrebbe contenere informazioni riservate. Per una maggiore sicurezza, il documento viene crittografato in modo che gli utenti non autorizzati non possano leggerlo e che gli utenti autorizzati non possano condividere schermate o screenshot che visualizzano il documento. 

Per aprire il documento, è necessario un lettore (talvolta denominato Visualizzatore) che verifica che siano state concesse le autorizzazioni per aprire il documento e quindi decrittografarlo.

## <a name="install-pdf-readers-for-your-device"></a>Installare i lettori PDF per il dispositivo

Selezionare il dispositivo che si sta usando per installare un lettore PDF in grado di aprire documenti PDF protetti. Tutti questi lettori possono aprire documenti protetti che rispettano lo standard ISO per la crittografia PDF:

- **Computer**: [Windows](protected-pdf-readers-windows.md)  |  [MacOS](protected-pdf-readers-mac.md)

- **Dispositivi mobili**: [Android](protected-pdf-readers-android.md)  |  [iOS](protected-pdf-readers-ios.md)

### <a name="support-for-previous-formats"></a>Supporto per i formati precedenti

I lettori PDF nella tabella seguente supportano i documenti PDF protetti con estensione Ppdf e i formati meno recenti con estensione. pdf. 

Attualmente, in Microsoft SharePoint viene utilizzato un formato precedente per i documenti PDF nelle librerie protette con IRM.


|Sistema operativo|Lettori supportati|
|----------------|-----------------------------------|
|Windows 10 e versioni precedenti<br />fino a Windows 7 Service Pack 1|Visualizzatore di Azure Information Protection<br /><br />Gaaiho Doc<br /><br />GigaTrust Desktop PDF Client for Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br /> Nuance Power PDF|
|Android|App Azure Information Protection<br /><br />Foxit MobilePDF with RMS<br /><br />GigaTrust App for Android|
|iOS|App Azure Information Protection<br /><br />Foxit MobilePDF with RMS<br /><br />TITUS Docs|

## <a name="using-adobe-acrobat-reader-with-the-adobe-plug-in"></a>Uso di Adobe Acrobat Reader con il plug-in Adobe

Una collaborazione tra Microsoft e Adobe ti offre un'esperienza più semplificata e coerente per i documenti PDF che sono stati classificati e, facoltativamente, protetti. Questa collaborazione offre il supporto per l'integrazione nativa di Adobe Acrobat con le soluzioni di Microsoft Information Protection, ad esempio [Azure Information Protection](../what-is-information-protection.md). 

L'integrazione nativa offre i vantaggi seguenti:

- È possibile visualizzare i documenti PDF protetti perché contengono informazioni riservate.

- È possibile visualizzare il valore di classificazione per l'etichetta dell'organizzazione applicata al documento.

- Supporto per lo standard ISO per la crittografia dei file PDF.
    
    A meno che questa funzionalità non sia stata [disabilitata da un amministratore](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption), questo formato di file PDF protetto è abilitato per impostazione predefinita per il client di Azure Information Protection (classico) e viene sempre usato dal client di Azure Information Protection Unified labeling.

È possibile usare il plug-in Adobe con [Windows](protected-pdf-readers-windows.md) e [MacOS](protected-pdf-readers-mac.md).

Per ulteriori informazioni, vedere i post di Blog seguenti: 

- [Disponibilità generale dell'integrazione di Adobe Acrobat Reader con Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-Integration-with/ba-p/298396)

- [Domande frequenti sull'integrazione di Adobe Reader e Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Microsoft-Information-Protection/Adobe-reader-and-Microsoft-Information-Protection-integration/ba-p/482219)

## <a name="next-steps"></a>Passaggi successivi

Utilizzare i collegamenti di questa pagina per installare un lettore PDF in modo da poter aprire documenti PDF protetti.

Per assistenza sull'utilizzo del lettore dopo l'installazione, utilizzare le istruzioni e la documentazione che accompagnano il lettore. Per il Visualizzatore Azure Information Protection per Windows, ad esempio, vedere [Guida dell'utente: visualizzare i file protetti con il client di Azure Information Protection Unified Labeling](clientv2-view-use-files.md).
