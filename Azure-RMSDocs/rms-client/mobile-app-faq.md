---
title: App per dispositivi mobili Azure Information Protection per iOS & Android
description: Informazioni di base sulle app per dispositivi mobili Azure Information Protection (AIP) per dispositivi iOS e Android
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/24/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 539b4ff8-5d3b-4c4d-9c84-c14da83ff76d
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 4b936baf799808fadbdaaefc0ae1fd55a6853fb2
ms.sourcegitcommit: 78c7ab80be7c292ea4bc62954a4e29c449e97439
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/13/2021
ms.locfileid: "98164453"
---
# <a name="what-is-the-azure-information-protection-app-for-ios-or-android"></a>Che cos'è l'app Azure Information Protection per iOS o Android?

>***Si applica a**: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***Rilevante per**: [Client di etichettatura unificata e client classico di AIP](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

L'app per dispositivi mobili Azure Information Protection (AIP) per iOS e Android è un'app Viewer che consente di visualizzare messaggi di posta elettronica, file PDF, immagini e file di testo protetti e sono utili se le normali app per questi tipi di file non supportano la protezione. 

Ad esempio, se i messaggi di posta elettronica protetti vengono visualizzati nell'app per dispositivi mobili di posta elettronica normale come allegati, è possibile usare l'app AIP per dispositivi mobili per visualizzare il messaggio di posta elettronica.

Per altre informazioni sulle funzionalità di protezione supportate nelle app, [le applicazioni che supportano Azure Rights Management la protezione dei dati](../requirements-applications.md). 

> [!NOTE]
> Le app per dispositivi mobili AIP sono *solo visualizzatori* e non consentono di creare nuovi messaggi di posta elettronica o di rispondere ai messaggi di posta elettronica oppure di creare o modificare file protetti. Le app per dispositivi mobili AIP non possono anche aprire allegati a file PDF o messaggi di posta elettronica protetti.
> 

## <a name="download-and-install-the-aip-app-for-your-device"></a>Scaricare e installare l'app AIP per il dispositivo

Scaricare e installare le app per dispositivi mobili AIP da uno dei seguenti percorsi:

**iTunes**:

:::image type="content" source="../media/ios-icon.png" alt-text="iTunes" link="https://apps.apple.com/app/microsoft-rights-management/id689516635" border="false":::  

**Google Play**:

:::image type="content" source="../media/android-icon.png" alt-text="Google Play" link="https://play.google.com/store/apps/details?id=com.microsoft.ipviewer" border="false"::: 

**Portale aziendale**:

Se il dispositivo mobile è gestito da Microsoft Intune, potrebbe essere possibile scaricare le app per dispositivi mobili AIP dal portale aziendale. 

Per ulteriori informazioni, contattare l'amministratore di sistema. 
## <a name="ios-view-protected-files-on-your-device"></a>iOS: visualizzare i file protetti nel dispositivo

Dopo aver [installato l'app per dispositivi mobili AIP](#download-and-install-the-aip-app-for-your-device), aprire un file o un messaggio di posta elettronica protetto. 

1. Se viene richiesto di selezionare un'app per aprire il file, toccare il pulsante Condividi per condividere il file.

    Selezionare **Condividi file tramite...** e quindi selezionare **copia in AIP Viewer.**

    Ad esempio:

    :::image type="content" source="../media/ios-share-to-aip-viewer.png" alt-text="Condividi nel Visualizzatore AIP in iOS" border="false":::

1. Accedere o selezionare un certificato come richiesto.

    Una volta eseguita l'autenticazione, l'indirizzo di posta elettronica o il file si aprirà nel Visualizzatore AIP.
 
## <a name="android-view-protected-files-on-your-device"></a>Android: visualizzare i file protetti nel dispositivo

Dopo aver [installato l'app per dispositivi mobili AIP](#download-and-install-the-aip-app-for-your-device), aprire un file o un messaggio di posta elettronica protetto. 

1. Quando viene richiesto di selezionare un'app, selezionare il Visualizzatore AIP:

    :::image type="content" source="../media/select-aip-viewer.png" alt-text="Selezionare l'app per dispositivi mobili AIP Viewer":::

1. Accedere o selezionare un certificato come richiesto.

    Una volta eseguita l'autenticazione, l'indirizzo di posta elettronica o il file si aprirà nel Visualizzatore AIP.

## <a name="aip-mobile-app-requirements"></a>Requisiti dell'app mobile AIP

Le app per dispositivi mobili AIP per iOS e Android supportano i tipi di file e gli ambienti seguenti:

|Requisito  |Descrizione  |
|---------|---------|
|**Versioni dei sistemi operativi supportate**     | I sistemi operativi minimi per dispositivi mobili includono: </br>-iOS 11  </br>-Android 6,0 </br></br>**Nota**: le app per dispositivi mobili AIP non sono supportate nelle CPU Intel.  |
|**Credenziali di accesso supportate**     | Accedere alle app per dispositivi mobili AIP con una delle seguenti opzioni: </br></br>**Credenziali aziendali o dell'Istituto di istruzione.** Provare ad accedere con le credenziali aziendali o dell'Istituto di istruzione. In caso di domande, contattare l'amministratore per sapere se l'organizzazione ha AD RMS locale con l'estensione per dispositivi mobili o se usa Azure Information Protection. </br></br>**Account Microsoft.** Se l'indirizzo di posta elettronica personale è stato usato per proteggere il file, accedere con un [account Microsoft](https://signup.live.com). Se è necessario applicare una account Microsoft, è possibile usare Hotmail, Gmail o qualsiasi altro indirizzo di posta elettronica a tale scopo. </br></br>**Nota**: non tutte le applicazioni sono in grado di aprire il contenuto protetto con un account Microsoft. Per ulteriori informazioni, vedere la pagina relativa agli [scenari supportati per l'apertura di documenti protetti](../secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents).|
|**Tipi di file supportati**     | I tipi di file supportati includono messaggi di posta elettronica protetti, file PDF, immagini e file di testo. </br></br>Ad esempio, questi file includono le seguenti estensioni: **rpmsg**, **PDF**, **Ppdf**, **pjpg** **,** **pjpeg**, **ptiff** **, ppng** **, ptxt, pXML,** </br></br>Per un elenco completo dei tipi di file supportati, vedere [la guida dell'amministratore del client AIP](clientv2-admin-guide-file-types.md#supported-file-types-for-classification-and-protection).|
| | |

## <a name="admins-testing-the-aip-mobile-apps"></a>Amministratori: test delle app per dispositivi mobili AIP

La maggior parte degli utenti userà in genere l'app per dispositivi mobili AIP per aprire un file o un messaggio di posta elettronica protetto che non può essere aperto con le normali app per dispositivi mobili

Se si è un amministratore di sistema che vuole testare le app per dispositivi mobili AIP per la propria organizzazione o semplicemente provare a usarlo personalmente, usare le istruzioni riportate di seguito per esaminare l'intero processo.

1. Assicurarsi di avere accesso a un tipo di file supportato dall'app per dispositivi mobili AIP dal dispositivo. 

    Ad esempio, inviare manualmente uno dei seguenti file protetti con diritti:

    |Tipo file  |Istruzioni  |
    |---------|---------|
    |**Posta elettronica (. rpmsg)**     | Usare un altro dispositivo, ad esempio Outlook, da un computer Windows, per inviare a se stessi un messaggio di posta elettronica protetto da diritti a cui è possibile accedere dal dispositivo mobile.  |
    |**PDF**     | 1. da un computer Windows [proteggere un file PDF](clientv2-classify-protect.md) usando il client AIP. </br>2. inviare manualmente il file PDF protetto oppure caricarlo in una libreria protetta da SharePoint e condividerlo con il proprio indirizzo di posta elettronica.        |
    |**Image (. ptxt,. pjpg o. ppng)**     | 1. da un computer Windows [proteggere un file di testo o di immagine](clientv2-classify-protect.md) usando il client AIP. </br></br>2. inviare manualmente il file protetto oppure caricarlo in una raccolta protetta di SharePoint e condividerlo con il proprio indirizzo di posta elettronica.   |
| | |

1. Aprire il file protetto sul dispositivo mobile usando l'allegato di posta elettronica o il collegamento che è stato inviato a se stessi.

    Ad esempio, i messaggi di posta elettronica protetti vengono visualizzati nella normale app per dispositivi mobili di posta elettronica come allegati. 

1. Quando viene richiesto di selezionare un'app per aprire il file o la posta elettronica protetta, selezionare l'app **Visualizzatore AIP** .

1. Accedere o selezionare un certificato, come richiesto. 

    Una volta eseguita l'autenticazione, l'app visualizzatore AIP Visualizza il messaggio di posta elettronica o il file.

> [!NOTE]
> Aprire sempre l'app AIP aprendo il contenuto protetto. Non tentare di accedere all'app fino a quando non viene richiesto o aprire un file protetto dall'app di AIP Viewer.
> 

## <a name="next-steps"></a>Passaggi successivi

Per fornire commenti e suggerimenti sulle app per dispositivi mobili AIP, usare uno dei metodi seguenti:

- Passare a **Impostazioni**  >  **Invia feedback**
- Invia una domanda nel [sito di Yammer](https://www.yammer.com/AskIPTeam)
