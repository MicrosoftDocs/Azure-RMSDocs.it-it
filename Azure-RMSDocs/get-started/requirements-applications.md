---
title: Supporto delle applicazioni per la protezione dati | Azure Information Protection
description: Identificare le applicazioni che usano le API di RMS per il supporto nativo del servizio Azure Rights Management di Azure Information Protection.
author: cabailey
manager: mbaldwin
ms.date: 10/31/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a036da617d88a65903cfea9df30d5f851bda6e36
ms.openlocfilehash: 80874b7e15fef7f4e7685774b31410149301c124


---


# <a name="applications-that-support-azure-rights-management-data-protection"></a>Applicazioni che supportano la protezione dati di Azure Rights Management

>*Si applica a: Azure Information Protection, Office 365*


Usare la tabella seguente per identificare le applicazioni che supportano il servizio Azure Rights Management (Azure RMS) a livello nativo, che garantisce la protezione dei dati per Azure Information Protection. 

Per queste applicazioni il supporto di Rights Management è perfettamente integrato mediante l'uso delle API di Rights Management per supportare le restrizioni di utilizzo. Queste applicazioni sono anche dette applicazioni abilitate per RMS.

Se non diversamente indicato, le funzionalità supportate sono valide sia per Azure RMS che per AD RMS. Per il supporto di AD RMS in iOS, Android, OS X e Windows Phone 8.1 è inoltre richiesta l'[estensione per dispositivi mobili Active Directory Rights Management Services](https://technet.microsoft.com/library/dn673574.aspx).

Informazioni sulle colonne della tabella:

-   **PDF protetto**: file caratterizzati dall'estensione ppdf e creati automaticamente quando si usa l'applicazione RMS sharing per condividere file di Office e file PDF tramite posta elettronica. L'applicazione RMS sharing e l'app Azure Information Protection per iOS e Android includono un lettore per i file PDF protetti. Se in precedenza sono stati creati file PDF protetti tramite Azure RMS o AD RMS, per continuare a leggere questi file su dispositivi Windows, iOS e Android, è possibile usare Foxit Reader e Nitro Pro.

-   **Posta elettronica**: i client di posta elettronica elencati possono proteggere il messaggio di posta elettronica stesso, proteggendo quindi automaticamente eventuali file allegati. In questo scenario la funzionalità di anteprima del client può visualizzare il contenuto protetto (messaggio e allegato) ai destinatari autorizzati. Se tuttavia un messaggio di posta elettronica non è protetto ma l'allegato è protetto, la funzionalità di anteprima del client non potrà visualizzare l'allegato protetto ai destinatari autorizzati.

-   **Altri tipi di file**: file di testo e di immagine con estensioni quali txt, xml, jpg e jpeg. L'estensione cambia dopo che i file vengono protetti in modo nativo da Rights Management e diventano di sola lettura. I file che non possono essere protetti in modo nativo, dopo essere stati protetti in modo generico da Rights Management hanno un'estensione di tipo pfile. Per altre informazioni, vedere [Guida dell'amministratore dell'applicazione Rights Management sharing](../rms-client/sharing-app-admin-guide.md).


|**Sistema operativo dispositivo**|Word, Excel, PowerPoint|PDF protetto|Posta elettronica|Altri tipi di file|
|-------------------------------|---------------------------|-----------------|---------|--------------------|
|**Windows**|Office 2010<br /><br />Office 2013<br /><br />Office 2016 <br /><br />App Office Mobile (solo Azure RMS) [[1]](#footnote-1)<br /><br />Office Online [[2]](#footnote-2)|Gaaiho Doc<br /><br />GigaTrust Desktop PDF Client for Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br />App di condivisione RMS|Outlook 2010<br /><br />Outlook 2013<br /><br />Office 2016 <br /><br />Outlook Web App (OWA) [[3]](#footnote-3)<br /><br />Windows Mail [[4]](#footnote-4)|Applicazione RMS sharing per Windows: testo, immagini, pfile<br /><br />Siemens JT2Go: file JT (solo Windows 10)|
|**iOS**|Office per iPad e iPhone [[5]](#footnote-5)<br /><br />Office Online [[2]](#footnote-2)<br /><br />TITUS Docs|App Azure Information Protection [[1]](#footnote-1)<br /><br /> Foxit Reader<br /><br />TITUS Docs|App Azure Information Protection [[1]](#footnote-1)<br /><br />Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook per iPad e iPhone [[4]](#footnote-4)<br /><br />OWA per iOS [[3]](#footnote-3)<br /><br />TITUS Mail|App Azure Information Protection [[1]](#footnote-1): testo, immagini<br /><br />TITUS Docs: pfile|
|**Android**|GigaTrust App for Android<br /><br />Office Online [[2]](#footnote-2)<br /><br />Office Mobile (solo Azure RMS) [[1]](#footnote-1)|App Azure Information Protection [[1]](#footnote-1)<br /><br />GigaTrust App for Android<br /><br />Foxit Reader<br /><br />App RMS sharing [[1]](#footnote-1)|9Folders [[4]](#footnote-4)<br /><br />App Azure Information Protection [[1]](#footnote-1)<br /><br />GigaTrust App for Android [[4]](#footnote-4)<br /><br />Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook per Android [[4]](#footnote-4)<br /><br />OWA per Android [[3]](#footnote-3) e [[7]](#footnote-7)<br /><br />Samsung Email (S3 e versioni successive) [[7]](#footnote-7)<br /><br />Classificazione TITUS per dispositivi mobili|App Azure Information Protection [[1]](#footnote-1): testo, immagini|
|**OS X**|Office 2011 (solo AD RMS)<br /><br />Office 2016 per Mac<br /><br />Office Online [[2]](#footnote-2)|Foxit Reader<br /><br />App RMS sharing [[1]](#footnote-1)|Outlook 2011 (solo AD RMS)<br /><br />Outlook 2016 per Mac<br /><br />Outlook per Mac|App RMS sharing [[1]](#footnote-1): testo, immagini, pfile|
|**Windows 10 Mobile**|App Office Mobile (solo Azure RMS)[[1]](#footnote-1)|Non supportato|Citrix WorxMail [[6]](#footnote-6)<br /><br />Posta di Outlook|Non supportato|
|**Windows RT**|Office 2013 RT<br /><br />Office Online [[2]](#footnote-2)|Non supportato|Outlook 2013 RT<br /><br />App di posta elettronica per Windows<br /><br />Windows Mail [[4]](#footnote-4)|Siemens JT2Go: file JT|
|**Windows Phone 8.1**|Office Mobile (solo AD RMS)|App RMS sharing [[1]](#footnote-1)|Outlook Mobile [[4]](#footnote-4)|App RMS sharing [[1]](#footnote-1): testo, immagini, pfile|
|**Blackberry 10**|Non supportato|Non supportato|Posta elettronica Blackberry [[4]](#footnote-4)|Non supportato|


##### <a name="footnote-1"></a>Nota 1
supporta la visualizzazione di contenuti protetti.

##### <a name="footnote-2"></a>Nota 2 
Supporta la visualizzazione di documenti protetti quando un documento non protetto viene caricato in una raccolta protetta di SharePoint Online e OneDrive for Business. 

##### <a name="footnote-3"></a>Nota 3
Se un destinatario riceve un messaggio di posta elettronica protetto e non usa Exchange come server di posta elettronica oppure se il mittente appartiene a un'altra organizzazione, il contenuto può essere aperto solo con un client di posta elettronica come Outlook e non da Outlook Web Access.

##### <a name="footnote-4"></a>Nota 4
utilizza Exchange ActiveSync IRM, che deve essere abilitato dall'amministratore di Exchange. Gli utenti possono visualizzare, rispondere e rispondere a tutti per messaggi di posta elettronica protetti, ma gli utenti non possono proteggere i nuovi messaggi di posta elettronica da sé.

Se un destinatario riceve un messaggio di posta elettronica protetto e non usa Exchange come server di posta elettronica oppure se il mittente appartiene a un'altra organizzazione, il contenuto può essere aperto solo con un client di posta elettronica come Outlook Il contenuto non può essere aperto da Outlook Web Access o dai client di posta elettronica per dispositivi mobili con Exchange Active Sync IRM.

##### <a name="footnote-5"></a>Nota 5
supporta la visualizzazione e la modifica di documenti protetti. Per altre informazioni, vedere il post sul blog di Office relativo al [supporto per Azure Rights Management disponibile in Office per iPad e iPhone](https://blogs.office.com/2015/07/22/azure-rights-management-support-comes-to-office-for-ipad-and-iphone-2/)

##### <a name="footnote-6"></a>Nota 6
Per altre informazioni, vedere la [documentazione del prodotto Citrix per WorxMail](http://docs.citrix.com/en-us/worx-mobile-apps/10/xmob-worx-mail.html).

##### <a name="footnote-7"></a>Nota 7
Per altre informazioni, vedere il post sul blog di Office relativo a [OWA per Android ora disponibile su dispositivi specifici](http://blogs.office.com/2014/06/11/owa-for-android-now-available-on-select-devices/)

## <a name="more-information-about-azure-rms-support-for-office"></a>Altre informazioni sul supporto di Azure RMS per Office

Azure RMS si integra perfettamente nelle applicazioni Word, Excel, PowerPoint e Outlook, dove questa funzionalità viene spesso denominata Information Rights Management (IRM). Le seguenti edizioni di client di Office supportano la protezione dei file e dei messaggi di posta elettronica tramite Azure RMS:

- Office Professional Plus 2016

- Office Professional Plus 2013

- Office Professional Plus 2010

Tutte le edizioni di Office, ad eccezione di Office 2007, possono utilizzare il contenuto protetto.

Azure RMS con Office Professional Plus 2010 oppure Office Professional 2010:

- Richiede l'applicazione Rights Management sharing per Windows

- Non supportato in Windows 10

## <a name="more-information-about-the-azure-information-protection-app-for-ios-and-android"></a>Altre informazioni sull'app Azure Information Protection per iOS e Android

L'app Azure Information Protection per iOS e Android sostituisce l'app RMS sharing per questi dispositivi. Offre la stessa funzionalità e inoltre supporta i messaggi di posta elettronica e i file PDF protetti da diritti in SharePoint Online.

Se i dispositivi iOS e Android sono registrati da Microsoft Intune, è possibile distribuire e gestire l'app tramite un'app gestita da criteri. Per altre informazioni, vedere l'articolo relativo alla [configurazione e distribuzione dei criteri di gestione delle applicazioni per dispositivi mobili nella console di Microsoft Intune](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console) nella documentazione di Intune Per il Passaggio 2 di questa documentazione di Intune, usare le istruzioni per pubblicare un'app gestita da criteri.

Per altre informazioni, vedere [Domande frequenti sull'app Azure Information Protection per iOS e Android](../rms-client/mobile-app-faq.md).


## <a name="more-information-about-the-rights-management-sharing-application"></a>Altre informazioni sull'applicazione Rights Management sharing

Per altre informazioni sull'applicazione Rights Management sharing per Windows, vedere le risorse seguenti:

-   [Guida dell'amministratore dell'applicazione di condivisione Rights Management](../rms-client/sharing-app-admin-guide.md)

-   [Guida dell'utente dell'applicazione di condivisione Rights Management](../rms-client/sharing-app-user-guide.md)

Per altre informazioni sull'applicazione Rights Management sharing per piattaforme mobili, vedere le risorse seguenti:

-   Per scaricare l'applicazione desiderata, fare clic sul collegamento corrispondente nella pagina [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970)

-   [Domande frequenti sull'applicazione di condivisione Microsoft Rights Management per piattaforme mobili](https://technet.microsoft.com/dn451248)

> [!NOTE]
> L'applicazione RMS sharing per iOS e Android è stata sostituita dall'app Azure Information Protection.

## <a name="more-information-about-other-applications-that-support-azure-rms"></a>Altre informazioni su ulteriori applicazioni che supportano Azure RMS

Oltre alle applicazioni riportate nella tabella, è possibile integrare con Azure RMS le applicazioni che supportano le API RMS, tra cui:

- Applicazioni line-of-business create internamente mediante RMS SDK

- Applicazioni di fornitori di software create mediante RMS SDK

Per altre informazioni sull'SDK, vedere la pagina relativa a [Microsoft Rights Management SDK](../develop/developers-guide.md).

## <a name="applications-that-are-not-supported-by-azure-rms"></a>Applicazioni non supportate da Azure RMS

Le applicazioni chi non sono attualmente supportate da Azure RMS sono le seguenti:

-   Microsoft Office per Mac 2011

-   Microsoft OneDrive for Business per SharePoint Server 2013

-   XPS Viewer
 
L'applicazione RMS sharing prevede inoltre le restrizioni seguenti:

-   Per i computer Windows, la versione minima richiesta è Windows 7 Service Pack 1



## <a name="next-steps"></a>Passaggi successivi
Per verificare gli altri requisiti, vedere [Requisiti per Azure Information Protection](requirements-azure-rms.md).

Per altre informazioni sul supporto di Azure RMS da parte delle applicazioni più diffuse, vedere [Supporto del servizio Azure Rights Management da parte delle applicazioni](../understand-explore/applications-support.md).

Per informazioni sulle modalità di configurazione delle applicazioni più diffuse per Azure RMS, vedere [Configurazione di applicazioni per Azure Rights Management](../deploy-use/configure-applications.md).


<!--HONumber=Nov16_HO1-->


