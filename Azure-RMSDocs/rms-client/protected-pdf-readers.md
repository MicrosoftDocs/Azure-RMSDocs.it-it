---
title: Lettori di file PDF protetti per Microsoft Information Protection
description: Installare un Reader per documenti PDF etichettati per la classificazione e la protezione
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/31/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: aab59e02-930b-4a17-8442-2d5d081fe1a6
ms.reviewer: kartikka
ms.suite: ems
search.appverid:
- MET150
ms.openlocfilehash: fae4a3f0e95e0ee3cf548c59aee55fc6e1a39831
ms.sourcegitcommit: 0ff7941832bd8476d53810d2c849c56efa0303fa
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68701601"
---
# <a name="install-a-pdf-reader-that-supports-microsoft-information-protection"></a>Installare un lettore PDF che supporta Microsoft Information Protection

Se è necessario aprire un documento PDF protetto da Microsoft Information Protection, usare i collegamenti e le informazioni seguenti.

## <a name="choose-your-pdf-reader"></a>Scegliere il lettore PDF

I lettori PDF seguenti possono aprire documenti PDF protetti che rispettano lo standard ISO per la crittografia PDF:

|Sistema operativo|Lettori supportati e collegamento di download|
|----------------|-----------------------------------|
|Windows 10 e versioni precedenti<br />fino a Windows 7 Service Pack 1|Adobe Acrobat Reader (scelta consigliata):<br /> 1. Leggere le [condizioni generali per l'utilizzo di Adobe](https://www.adobe.com/legal/terms.html) <br /> 2. Installare Adobe Reader per Windows dal [sito Adobe](https://www.adobe.com/)<br /> 3. Installare il [plug-in Adobe](https://go.microsoft.com/fwlink/?linkid=2050049) per Windows <br /> 4. Se richiesto, chiedere all'amministratore di [autorizzare il plug-in](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-integration-with/ba-p/298396) <br /><br /> Visualizzatore di Azure Information Protection: [Download](https://go.microsoft.com/fwlink/?linkid=838993)<br /><br />Foxit Reader: [Download](https://www.foxitsoftware.com/pdf-reader/)|
|Versioni MacOS 10,12-10,14 |Adobe Acrobat Reader:<br /> 1. Leggere le [condizioni generali per l'utilizzo di Adobe](https://www.adobe.com/legal/terms.html) <br /> 2. Installare Adobe Reader per Mac dal sito di [Adobe](https://www.adobe.com/)<br /> 3. Installare il [plug-in Adobe](https://go.microsoft.com/fwlink/?linkid=2050049) per Mac <br /> 4. Se richiesto, chiedere all'amministratore di [autorizzare il plug-in](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-integration-with/ba-p/298396)|
|Android|App Azure Information Protection: [Download](https://go.microsoft.com/fwlink/?LinkId=325340)|
|iOS|App Azure Information Protection: [Download](https://go.microsoft.com/fwlink/?LinkId=325338)|

### <a name="support-for-previous-formats"></a>Supporto per i formati precedenti

I lettori PDF nella tabella successiva supportano i documenti PDF protetti con estensione Ppdf e i formati meno recenti con estensione PDF di nome.

Attualmente, SharePoint Online e SharePoint locale usano un formato più datato per i documenti PDF nelle librerie protette con IRM.


|Sistema operativo|Lettori supportati|
|----------------|-----------------------------------|
|Windows 10 e versioni precedenti<br />fino a Windows 7 Service Pack 1|Visualizzatore di Azure Information Protection<br /><br />Gaaiho Doc<br /><br />GigaTrust Desktop PDF Client for Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br /> Nuance Power PDF<br /><br />App RMS sharing|
|Android|App Azure Information Protection<br /><br />Foxit MobilePDF with RMS<br /><br />GigaTrust App for Android|
|iOS|App Azure Information Protection<br /><br />Foxit MobilePDF with RMS<br /><br />TITUS Docs|

## <a name="using-adobe-acrobat-reader-with-the-adobe-plug-in"></a>Uso di Adobe Acrobat Reader con il plug-in Adobe

Una collaborazione tra Microsoft e Adobe ti offre un'esperienza più semplificata e coerente per i documenti PDF che sono stati classificati e, facoltativamente, protetti. Questa collaborazione offre il supporto per l'integrazione nativa di Adobe Acrobat con le soluzioni di Microsoft Information Protection, ad esempio [Azure Information Protection](../what-is-information-protection.md). 

L'integrazione nativa offre i vantaggi seguenti:

- È possibile visualizzare i documenti PDF protetti perché contengono informazioni riservate.

- È possibile visualizzare il valore di classificazione per l'etichetta dell'organizzazione applicata al documento.

- Supporto per lo standard ISO per la crittografia dei file PDF.
    
    A meno che questa funzionalità non sia stata [disabilitata da un amministratore](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption), questo formato di file PDF protetto è abilitato per impostazione predefinita per il client di Azure Information Protection (classico) e viene sempre usato dal client di Azure Information Protection Unified labeling.

Per ulteriori informazioni, vedere i post di Blog seguenti: 

- [Disponibilità generale dell'integrazione di Adobe Acrobat Reader con Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-Integration-with/ba-p/298396)

- [Domande frequenti sull'integrazione di Adobe Reader e Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Microsoft-Information-Protection/Adobe-reader-and-Microsoft-Information-Protection-integration/ba-p/482219)
