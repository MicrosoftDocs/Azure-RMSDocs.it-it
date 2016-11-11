---
title: Domande frequenti sull&quot;app Azure Information Protection per iOS e Android | Azure Information Protection
description: 
keywords: Alcune domande frequenti riguardanti l&quot;uso dell&quot;app Azure Information Protection per iOS e Android
author: cabailey
manager: mbaldwin
ms.date: 11/03/2016
ms.topic: article
ms.prod: azure
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 539b4ff8-5d3b-4c4d-9c84-c14da83ff76d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2f1930f4657278d25ef6dd369866f16e4ba71644
ms.openlocfilehash: 1cafa88ded2bf951f8af93e4b27cc526735d19e8


---

# <a name="faqs-for-microsoft-azure-information-protection-app-for-ios-and-android"></a>Domande frequenti sull'app Microsoft Azure Information Protection per iOS e Android

*Si applica a: Active Directory Rights Management Services, Azure Information Protection*

Questa pagina riporta le risposte a domande frequenti sull'app Microsoft Azure Information Protection per iOS e Android.

## <a name="what-can-i-do-with-the-azure-information-protection-app"></a>Quali operazioni è possibile eseguire con l'app Azure Information Protection?

L'app consente di visualizzare i messaggi di posta elettronica protetti da diritti (file con estensione rpmsg) se l'app di posta elettronica in uso non supporta la protezione dei dati di gestione dei diritti in modo nativo. Questa app consente anche di visualizzare file PDF, file di testo e di immagini protetti da diritti. Attualmente, l'app non può essere usata per creare nuovi messaggi di posta elettronica protetti, rispondere ai messaggi oppure creare o modificare i file protetti.

## <a name="can-i-open-pdf-files-that-are-in-sharepoint-protected-libraries-and-onedrive-for-business"></a>È possibile aprire file PDF che si trovano in librerie protette da SharePoint e OneDrive For Business?

Sì, è possibile aprire file PDF protetti che altri utenti hanno condiviso tramite SharePoint e OneDrive for Business. Toccare il collegamento e scegliere l'app per aprire il file automaticamente. 

## <a name="how-do-i-get-started-with-the-viewer-app"></a>Come si può iniziare a usare l'app visualizzatore?

Accedere a uno dei file supportati dall'app dal dispositivo mobile per aprire il visualizzatore. Ad esempio:

- **Un file con estensione rpmsg**: si tratta di un messaggio di posta elettronica protetto da diritti visualizzato come allegato in un messaggio di posta elettronica quando l'app di posta elettronica del dispositivo mobile non supporta la protezione dei dati di gestione dei diritti in modo nativo. 
    
    Usare un altro dispositivo per inviare a se stessi un messaggio di posta elettronica protetto da diritti a cui è possibile accedere dal dispositivo mobile. Ad esempio, usare Outlook da un computer Windows. Per un elenco dei client di posta elettronica che supportano la gestione dei diritti in modo nativo, vedere la colonna POSTA ELETTRONICA nella pagina [Applicazioni che supportano la protezione dati di Azure Rights Management](../get-started/requirements-applications.md).

- **Un file PDF protetto da diritti**: usare l'applicazione di condivisione Rights Management da un computer Windows o un'applicazione PDF che supporta in modo nativo la gestione dei diritti per inviare a se stessi un file PDF protetto da diritti come allegato di un messaggio di posta elettronica. In alternativa, caricare un file PDF in una raccolta protetta di SharePoint e condividerlo usando l'indirizzo di posta elettronica.

- **File con estensione PTXT, PJPG o PFILE**: usare l'applicazione di condivisione Rights Management da un computer Windows e l'opzione [Condividi file protetto](sharing-app-protect-by-email.md) per inviare un file protetto come allegato di un messaggio ad un indirizzo di posta elettronica personale. Per l'elenco completo dei tipi di file che è possibile usare per il test, vedere la prima tabella della sezione [Tipi ed estensioni di file supportati](sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions) della Guida dell'amministratore dell'applicazione di condivisione Rights Management. 

Per visualizzare questi file nell'app visualizzatore Azure Information Protection, toccare l'allegato di posta elettronica o il collegamento. Quando viene chiesto di selezionare un'app per aprire i file, selezionare l'app visualizzatore **AIP**. Verrà quindi chiesto di accedere con l'account aziendale o dell'istituto di istruzione. Dopo aver eseguito l'autenticazione, l'app Azure Information Protection visualizza il messaggio di posta elettronica o il file da leggere.

## <a name="what-credentials-should-i-use-to-sign-in-to-this-app"></a>Quali credenziali usare per accedere all'app?

Se l'organizzazione dispone già di AD RMS locale (con l'estensione per dispositivi mobili) o usa il servizio Azure Rights Management, è possibile accedere con le proprie credenziali. In caso contrario, è possibile richiedere un nuovo account gratuito usando la [pagina Azure Information Protection](https://portal.office.com/signup?sku=rms&ru=https%3A%2F%2Fportal.azurerms.com%2F%23%2Fdownload).

## <a name="can-i-sign-up-for-the-free-account-with-my-personal-email-address-such-as-a-hotmail-or-gmail-account"></a>È possibile accedere gratuitamente con un indirizzo di posta elettronica personale, ad esempio un account Hotmail o Gmail?

Non ancora. Attualmente è possibile accedere solo con l'indirizzo di posta elettronica dell'organizzazione (account aziendale o dell'istituto di istruzione). Microsoft sta implementando il supporto per gli indirizzi di posta elettronica personali. Questa risposta verrà aggiornata quando tale funzionalità sarà disponibile.

## <a name="which-file-extensions-can-i-open-with-this-app"></a>Quali estensioni di file è possibile aprire con questa app?

È possibile aprire i file con estensione rpmsg, pdf, ppdf, pjpg e ptxt, oltre ad altri numerosi formati di file di testo e immagine.

##  <a name="how-do-i-provide-feedback-about-this-app"></a>In che modo è possibile fornire feedback sull'app?

Nell'app passare a **Settings (Impostazioni)** > **Send feedback (Invia feedback)**.


## <a name="my-question-has-not-been-answeredwhat-should-i-do"></a>La domanda non è stata soddisfatta. Come si deve procedere?

Inviare la domanda al [sito Yammer](http://www.yammer.com/AskIPTeam) o [inviare un messaggio di posta elettronica al team di Information Protection](mailto:askIPteam@microsoft.com?subject=Question%20about%20Azure%20Information%20Protection%20app).



<!--HONumber=Nov16_HO1-->


