---
title: Lettori di file PDF protetti per Microsoft Information Protection
description: ''
keywords: ''
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/04/2018
ms.topic: article
ms.prod: azure
ms.service: information-protection
ms.assetid: aab59e02-930b-4a17-8442-2d5d081fe1a6
ms.reviewer: kartikka
ms.suite: ems
ms.openlocfilehash: d4421caa4ec6846456c12aa831644e957c5b4fd9
ms.sourcegitcommit: 8e7b135bf48ced7e53d91f45d62b7bbd0f37634e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/04/2018
ms.locfileid: "52861201"
---
# <a name="supported-pdf-readers-for-microsoft-information-protection"></a>Lettori di file PDF supportati per Microsoft Information Protection

Le informazioni seguenti consentono di acquisire familiarità con i documenti PDF etichettati per la classificazione e la protezione e con le modalità di visualizzazione di questi documenti.

Una collaborazione tra Microsoft e Adobe offre un'esperienza più semplice e coerente per i documenti PDF che sono stati classificati e, facoltativamente, protetti. Questa collaborazione offre il supporto per l'integrazione nativa di Adobe Acrobat con le soluzioni di Microsoft Information Protection, ad esempio [Azure Information Protection](../what-is-information-protection.md). 

L'integrazione nativa offre i vantaggi seguenti:

- È possibile visualizzare i documenti PDF protetti perché contengono informazioni riservate.

- È possibile visualizzare il valore di classificazione per l'etichetta dell'organizzazione applicata al documento.

- Supporto per lo standard ISO per la crittografia dei file PDF.
    
    A meno che questa funzionalità non sia stata [disabilitata dall'amministratore](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption), questo formato di file PDF protetto è ora abilitato per impostazione predefinita nella versione più recente del client Azure Information Protection.

Per altre informazioni, vedere questo post di blog: [Starting October, use Adobe Acrobat Reader for PDFs protected by Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Starting-October-use-Adobe-Acrobat-Reader-for-PDFs-protected-by/ba-p/262738) (A partire da ottobre è possibile usare Adobe Acrobat Reader per i PDF protetti da Microsoft Information Protection)

## <a name="supported-pdf-readers"></a>Lettori PDF supportati

I seguenti lettori di file PDF sono in grado di aprire i file PDF che rispettano lo standard ISO per la crittografia PDF:

|Sistema operativo|Lettori supportati e collegamento di download|
|----------------|-----------------------------------|
|Windows 10 e versioni precedenti<br />fino a Windows 7 Service Pack 1|Adobe Acrobat Reader (scelta consigliata):<br />-  [Leggere le condizioni generali per l'utilizzo di Adobe](https://www.adobe.com/legal/terms.html) <br />- [Scaricare l'anteprima](https://ardownload2.adobe.com/pub/adobe/reader/win/AcrobatDC/misc/MIP_Preview/1900820120/Adobe_MIP_Preview_1900820120.zip) <br /><br /> Visualizzatore Azure Information Protection: [Download](https://go.microsoft.com/fwlink/?linkid=838993)<br /><br />Foxit Reader: [Download](https://www.foxitsoftware.com/pdf-reader/)|
|Android|App Azure Information Protection: [Download](https://go.microsoft.com/fwlink/?LinkId=325340)|
|iOS|App Azure Information Protection: [Download](https://go.microsoft.com/fwlink/?LinkId=325338)|

### <a name="support-for-previous-formats"></a>Supporto per i formati precedenti

I lettori di file PDF riportati nella tabella successiva supportano i documenti PDF protetti con estensione PPDF e i formati di file precedenti con estensione PDF.

Attualmente, SharePoint Online e SharePoint locale usano un formato più datato per i documenti PDF nelle librerie protette con IRM.


|Sistema operativo|Lettori supportati|
|----------------|-----------------------------------|
|Windows 10 e versioni precedenti<br />fino a Windows 7 Service Pack 1|Visualizzatore di Azure Information Protection<br /><br />Gaaiho Doc<br /><br />GigaTrust Desktop PDF Client for Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br />App di condivisione RMS|
|Android|App Azure Information Protection<br /><br />Foxit MobilePDF with RMS<br /><br />GigaTrust App for Android|
|iOS|App Azure Information Protection<br /><br />Foxit MobilePDF with RMS<br /><br />TITUS Docs|
