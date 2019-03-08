---
title: Come usare le impostazioni di crittografia | Azure RMS
description: Linee guida sui pacchetti di crittografia di Azure RMS e sui relativi frammenti di codice.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: B1D2C227-F43D-4B18-9956-767B35145792
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 11ebf15c82d8e27399a9df004f98f00b274802f2
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57330363"
---
# <a name="how-to-work-with-encryption-settings"></a>Procedura: Usare le impostazioni di crittografia

Questo argomento descrive i pacchetti di crittografia e illustra alcuni frammenti di codice che ne consentono l'uso.

## <a name="support-for-aes-256-the-new-default"></a>Supporto per AES 256, il nuovo valore predefinito

Poiché è il nuovo valore predefinito, non è necessario alcun codice aggiuntivo per usare la crittografia basata su *AES 256*, purché si sfrutti l'aggiornamento di marzo 2015 di RMS SDK 2.1 o versione successiva. È consigliabile prendere in considerazione l'aggiornamento delle applicazioni con questa versione per poter beneficiare dei vantaggi di sicurezza aggiuntivi di *AES 256*.

> [!IMPORTANT]
> Il supporto per l'uso dei file protetti con *AES 256* è stato introdotto con la [versione di ottobre 2014](release-notes-rtm.md). Se si eseguono applicazioni create con una versione di SDK precedente a ottobre 2014, questo aggiornamento interromperà l'applicazione. Assicurarsi che i clienti delle applicazioni che si stanno creando usino SDK aggiornato o desiderino eseguire immediatamente l'aggiornamento alla versione più recente dell'applicazione.

 
## <a name="api-encryption-support"></a>Supporto della crittografia API

A partire dall'[aggiornamento di marzo 2015](release-notes-rtm.md), nell'API e nei pacchetti di crittografia associati sono state aggiunte i seguenti tre flag:

-   IPC\_ENCRYPTION\_PACKAGE\_AES256\_CBC4K
-   IPC\_ENCRYPTION\_PACKAGE \_AES128\_CBC4K
-   IPC\_ENCRYPTION\_PACKAGE \_AES128\_ECB (noto anche come algoritmo deprecato)

I flag del pacchetto di crittografia (vedere [Preferred encryption](https://msdn.microsoft.com/library/dn974065.aspx)) possono essere usati in combinazione con il flag della proprietà di licenza, *IPC\_LI\_PREFERRED\_ENCRYPTION\_PACKAGE*.

Di seguito sono elencati alcuni frammenti di codice semplici che dimostrano come utilizzare la nuova proprietà di licenza.

## <a name="deprecated-algorithms"></a>Algoritmi deprecati

Nell'API non è più esposto il flag *IPC\_LI\_DEPRECATED\_ENCRYPTION\_ALGORITHMS*. Ciò significa che le future applicazioni non verranno più compilate se faranno riferimento a questo flag, ma le applicazioni già create con questo flag continueranno a funzionare poiché risulta privato nel codice API.

È comunque possibile ottenere il vantaggio del flag obsoleto degli algoritmi di crittografia deprecati modificando semplicemente un flag. Vedere gli esempi seguenti di frammenti di codice.

## <a name="protect-files-with-aes-256-cbc4k"></a>Protezione dei file con AES 256 CBC4K

Nessuna modifica necessaria nel codice, *AES 256* CBC4K è l'impostazione predefinita.

    C++

    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID,
                                    0,
                                    NULL,
                                    &amp;pLicenseHandle);


## <a name="protect-files-with-aes-128-cbc4k"></a>Protezione dei file con AES-128 CBC4K

    C++

    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID,
                                    0,
                                    NULL,
                                    &amp;pLicenseHandle);

    DWORD dwEncryptionMode = IPC_ENCRYPTION_PACKAGE_AES128_CBC4K;

    hr = IpcSetLicenseProperty(pLicenseHandle,
                           false,
                           IPC_LI_PREFERRED_ENCRYPTION_PACKAGE,
                           &amp;dwEncryptionMode);


## <a name="protect-files-with-aes-128-ecb-deprecated-algorithms"></a>Protezione dei file con AES-128 ECB (algoritmi deprecati)

Questo esempio mostra anche la nuova modalità di supporto degli *algoritmi deprecati*.

    C++

    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID,
                                    0,
                                    NULL,
                                    &amp;pLicenseHandle);

    DWORD dwEncryptionMode = IPC_ENCRYPTION_PACKAGE_AES128_ECB;

    hr = IpcSetLicenseProperty(pLicenseHandle,
                           false,
                           IPC_LI_PREFERRED_ENCRYPTION_PACKAGE,
                           &amp;dwEncryptionMode);

