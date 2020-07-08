---
title: App Azure Information Protection per iOS & Android
description: Informazioni di base sulle app Azure Information Protection (AIP) per dispositivi iOS e Android
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/07/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 539b4ff8-5d3b-4c4d-9c84-c14da83ff76d
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 0f849dfefa6af9ffd95dcca0c731ed216f465b11
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/07/2020
ms.locfileid: "86046403"
---
# <a name="what-is-the-azure-information-protection-app-for-ios-or-android"></a>Che cos'è l'app Azure Information Protection per iOS o Android?

*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Le app Azure Information Protection (AIP) per iOS e Android consentono di visualizzare i messaggi di posta elettronica protetti da diritti (file con**estensione rpmsg** ) quando l'app di posta elettronica non supporta in modo nativo la protezione dei dati di Rights Management.  

Le app AIP consentono inoltre di visualizzare i documenti PDF protetti da diritti (file PDF e**Ppdf** protetti), le immagini e i file di testo.

> [!NOTE]
> Le app AIP sono solo visualizzatori e non consentono di creare nuovi messaggi di posta elettronica protetti oppure di creare o modificare file protetti. Le app non possono anche aprire allegati per i file visualizzati, ad esempio allegati a documenti PDF protetti o messaggi di posta elettronica.
>

## <a name="aip-mobile-app-requirements"></a>Requisiti dell'app mobile AIP

Le app per dispositivi mobili AIP per iOS e Android possono essere usate con i sistemi seguenti:

- [Versioni del sistema operativo per dispositivi mobili supportate](#supported-mobile-os-versions)
- [Credenziali di accesso supportate](#supported-sign-in-credentials)
- [Estensioni di file supportate](#supported-file-extensions)

### <a name="supported-mobile-os-versions"></a>Versioni del sistema operativo per dispositivi mobili supportate

Per le app per dispositivi mobili AIP è necessario uno dei seguenti sistemi operativi mobili minimi: 

- iOS 11 
- Android 6,0 

> [!NOTE]
> Le app per dispositivi mobili AIP non sono supportate nelle CPU Intel.
> 

### <a name="supported-sign-in-credentials"></a>Credenziali di accesso supportate

Per accedere a AIP, usare uno dei seguenti elementi: 

- **Credenziali aziendali o dell'Istituto di istruzione.** Usare se l'organizzazione ha già AD RMS locale con l'estensione per dispositivi mobili o USA Azure Information Protection.
 
- **Account Microsoft**. Se l'indirizzo di posta elettronica personale è stato usato per proteggere il file, accedere con un [account Microsoft](https://signup.live.com). 

    - È possibile usare Hotmail, Gmail o qualsiasi altro indirizzo di posta elettronica di cui si è proprietari quando si applica un account Microsoft.
    
> [!NOTE]
> Non tutte le applicazioni possono aprire il contenuto protetto quando si usa un account Microsoft. Per ulteriori informazioni, vedere la pagina relativa agli [scenari supportati per l'apertura di documenti protetti](../secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents).
> 

### <a name="supported-file-extensions"></a>Estensioni di file supportate

È possibile aprire i file con estensione rpmsg, pdf, ppdf, pjpg, pjpeg, ptiff, ppng, ptxt, pxml e altri formati di file di testo e immagine.

Per l'elenco completo delle estensioni dei nomi di file di testo e immagine, vedere la prima tabella in [Tipi di file supportati per la classificazione e la protezione](clientv2-admin-guide-file-types.md#supported-file-types-for-classification-and-protection) nella Guida dell'amministratore.

## <a name="installing-your-aip-mobile-apps-and-viewing-files"></a>Installazione delle app per dispositivi mobili AIP e visualizzazione dei file

Se il dispositivo mobile è gestito da Microsoft Intune, potrebbe essere possibile scaricare le app dal portale aziendale.

In caso contrario, accedere alle app da:

- Archivio [iTunes](https://apps.apple.com/app/microsoft-rights-management/id689516635) o [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.ipviewer)
- [Pagina di download Azure Information Protection](https://portal.azurerms.com/#/download). Selezionare le icone [iOS](https://apps.apple.com/app/microsoft-rights-management/id689516635) o [Android](https://play.google.com/store/apps/details?id=com.microsoft.ipviewer) nella sezione **dispositivi mobili** .

Al termine dell'installazione, attendere fino a quando non si riceve un messaggio di posta elettronica o un file protetto e selezionare il **Visualizzatore AIP** quando lo si apre.

Verrà richiesto di accedere con l'account aziendale o dell'Istituto di istruzione o di selezionare un certificato. Una volta eseguita l'autenticazione, il messaggio di posta elettronica o il file verrà aperto e sarà possibile leggerne il contenuto.

> [!TIP]
> Per provarlo subito, inviare un messaggio di posta elettronica o un file protetto da visualizzare. 
>
> Per altre informazioni, vedere [Introduzione all'app Microsoft Azure Information Protection per iOS e Android](mobile-app-get-started.md).
> 

## <a name="next-steps"></a>Passaggi successivi

Per fornire commenti e suggerimenti sulle app per dispositivi mobili AIP, usare uno dei metodi seguenti:

- Passare a **Impostazioni**  >  **Invia feedback**
- Invia una domanda nel [sito di Yammer](https://www.yammer.com/AskIPTeam)
