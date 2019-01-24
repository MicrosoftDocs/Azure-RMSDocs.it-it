---
title: Domande frequenti sull'app Azure Information Protection per iOS e Android
description: Alcune domande frequenti riguardanti l'uso dell'app Azure Information Protection per iOS e Android
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/31/2018
ms.topic: conceptual
ms.service: information-protection
ms.custom: askipteam
ms.assetid: 539b4ff8-5d3b-4c4d-9c84-c14da83ff76d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 29c7d333131c0b85b9cdb83e9a2212420f60077f
ms.sourcegitcommit: 9dc6da0fb7f96b37ed8eadd43bacd1c8a1a55af8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2019
ms.locfileid: "54393658"
---
# <a name="faqs-for-microsoft-azure-information-protection-app-for-ios-and-android"></a>Domande frequenti sull'app Microsoft Azure Information Protection per iOS e Android

*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Questa pagina riporta le risposte a domande frequenti sull'app Microsoft Azure Information Protection per iOS e Android.

## <a name="what-can-i-do-with-the-azure-information-protection-app"></a>Quali operazioni è possibile eseguire con l'app Azure Information Protection?

L'app consente di visualizzare i messaggi di posta elettronica protetti da diritti (file con estensione rpmsg) se l'app di posta elettronica in uso non supporta la protezione dei dati di gestione dei diritti in modo nativo. Questa app consente anche di visualizzare documenti PDF, file di testo e di immagini protetti con RMS. 

Dato che questa app è un visualizzatore, non può essere usata per creare nuovi messaggi di posta elettronica protetti, rispondere ai messaggi oppure creare o modificare i file protetti. Inoltre, l'app non consente di aprire allegati per i file visualizzati. Ad esempio, gli allegati in documenti PDF protetti o nei messaggi di posta elettronica protetti con RMS.

## <a name="can-i-open-pdf-files-that-are-in-sharepoint-protected-libraries-and-onedrive-for-business"></a>È possibile aprire file PDF che si trovano in librerie protette di SharePoint e OneDrive for Business?

Sì, è possibile aprire file PDF protetti che altri utenti hanno condiviso tramite SharePoint e OneDrive for Business. Toccare il collegamento e scegliere l'app per aprire il file automaticamente. 

Questa app può anche aprire i file PDF protetti all'esterno di SharePoint e OneDrive for Business (file PPDF e PDF protetti).

## <a name="can-my-mobile-device-run-the-azure-information-protection-app"></a>È possibile eseguire l'app Azure Information Protection in un dispositivo mobile?

L'app Azure Information Protection supporta **iOS 8** o **Android 4.4** come versione minima.

Se sono disponibili queste versioni o versioni successive, è possibile installare l'app per eseguirla nel dispositivo mobile:

- Se il dispositivo mobile è gestito da Microsoft Intune, l'app Azure Information Protection dovrebbe essere disponibile per l'installazione dal portale aziendale.

- Se il dispositivo mobile non è gestito da Microsoft Intune o l'app Azure Information Protection non è disponibile dal portale aziendale, è possibile installare l'app direttamente dagli store iTunes e Google Play oppure facendo clic sull'icona di iOS o Android nella sezione **Dispositivi mobili** nella [pagina di download di Azure Information Protection](https://portal.azurerms.com/#/download). 

## <a name="how-do-i-get-started-with-the-viewer-app"></a>Come si può iniziare a usare l'app visualizzatore?

Dopo aver installato l'app, non è necessario eseguire altre operazioni. Attendere finché non viene visualizzato un file o un messaggio di posta elettronica protetto e quindi scegliere il **visualizzatore dell'API** per aprirlo. Verrà quindi chiesto di accedere con l'account aziendale o dell'istituto di istruzione oppure di selezionare un certificato. Dopo l'autenticazione delle credenziali, sarà quindi possibile leggere il contenuto.

Tuttavia, se non si vuole attendere, è possibile usare le istruzioni seguenti per inviare a se stessi un messaggio di posta elettronica protetto o un file da visualizzare: [Introduzione all'app Microsoft Azure Information Protection per iOS e Android](mobile-app-get-started.md) 

## <a name="what-credentials-should-i-use-to-sign-in-to-this-app"></a>Quali credenziali usare per accedere all'app?

Se l'organizzazione ha già AD RMS in locale (con l'estensione per dispositivi mobili) o usa il servizio Azure Rights Management, usare le credenziali dell'account aziendale per accedere. 

Se per proteggere il file è stato usato l'indirizzo di posta elettronica personale, usare le credenziali di un [account Microsoft](https://signup.live.com) gratuito per accedere.

## <a name="can-i-sign-up-for-the-free-account-with-my-personal-email-address-such-as-a-hotmail-or-gmail-account"></a>È possibile accedere gratuitamente con un indirizzo di posta elettronica personale, ad esempio un account Hotmail o Gmail?

Sì, quando si richiede un account Microsoft, è possibile specificare il proprio indirizzo di posta elettronica Hotmail o Gmail o qualsiasi altro indirizzo di posta elettronica personale. 

Tuttavia, anche se il visualizzatore può aprire file protetti con questo account, non tutte le applicazioni possono aprire contenuti protetti quando viene usato un account Microsoft per l'autenticazione. [Altre informazioni](../secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)

## <a name="which-file-extensions-can-i-open-with-this-app"></a>Quali estensioni di file è possibile aprire con questa app?

È possibile aprire i file con estensione rpmsg, pdf, ppdf, pjpg, pjpeg, ptiff, ppng, ptxt, pxml e altri formati di file di testo e immagine.

Per l'elenco completo delle estensioni dei nomi di file di testo e immagine, vedere la prima tabella in [Tipi di file supportati per la classificazione e la protezione](client-admin-guide-file-types.md#supported-file-types-for-classification-and-protection) nella Guida dell'amministratore.

##  <a name="how-do-i-provide-feedback-about-this-app"></a>In che modo è possibile fornire feedback sull'app?

Nell'app passare a **Settings (Impostazioni)** > **Send feedback (Invia feedback)**.


## <a name="my-question-has-not-been-answeredwhat-should-i-do"></a>La domanda non è stata soddisfatta. Come si deve procedere?

Inserire la domanda sul [sito Yammer](https://www.yammer.com/AskIPTeam).
