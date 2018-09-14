---
title: Rimuovere la protezione tramite l'app RMS sharing - AIP
description: Istruzioni per rimuovere la protezione da un file protetto in precedenza con l'applicazione RMS sharing.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: da95b938-eaad-4c83-a21e-ff1d4872aae4
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 871a9c34e3b02fcf1e7295228d1c79f9840f719b
ms.sourcegitcommit: 26a2c1becdf3e3145dc1168f5ea8492f2e1ff2f3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/07/2018
ms.locfileid: "44151589"
---
# <a name="remove-protection-from-a-file-by-using-the-rights-management-sharing-application"></a>Rimuovere la protezione da un file mediante l'applicazione Rights Management sharing

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 7 con SP1, Windows 8, Windows 8.1*

Per rimuovere la protezione da un file (ovvero lasciare un file non protetto) che in precedenza è stato protetto mediante l'applicazione RMS sharing, usare l'opzione **Rimuovi protezione** da Esplora file.

> [!IMPORTANT]
> Per rimuovere la protezione, è necessario essere proprietario del file.

## <a name="to-remove-protection-from-a-file"></a>Per rimuovere la protezione da un file

1.  Da Esplora File, fare clic con il pulsante destro sul file (ad esempio, Sample.ptxt), selezionare **Proteggi tramite RMS**, fare clic su **Proteggi sul posto**, quindi fare clic su **Rimuovi protezione**:

    ![Rimuovere l'opzione di menu di protezione per l'applicazione RMS sharing](../media/ADRMS_MSRMSApp_RemoveProtection.png)

    è possibile che vengano richieste le credenziali.

Nota: se queste opzioni non sono visualizzate, è probabile che l'applicazione RMS sharing non sia installata nel computer, che non sia installata la versione più recente o che sia necessario riavviare il computer per completare l'installazione. Per ulteriori informazioni su come installare l'applicazione di condivisione, vedere [Scaricare e installare l'applicazione Rights Management sharing](install-sharing-app.md).

Il file protetto originale viene eliminato (ad esempio, Sample.ptxt) e sostituito con un file con lo stesso nome ma con l'estensione del nome del file non protetto (ad esempio Sample.txt).

## <a name="examples-and-other-instructions"></a>Esempi e altre istruzioni
Per esempi di come è possibile usare l'applicazione Rights Management sharing e informazioni sulle procedure da seguire, vedere le sezioni seguenti della Guida dell'utente dell'applicazione Rights Management sharing:

-   [Esempi per l'uso dell'applicazione RMS sharing](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [Per saperne di più](sharing-app-user-guide.md#what-do-you-want-to-do)

## <a name="see-also"></a>Vedere anche
[Guida dell'utente dell'applicazione di condivisione Rights Management](sharing-app-user-guide.md)
