---
# required metadata

title: Requisiti per Azure RMS&#58; applicazioni | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/13/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Requisiti per Azure RMS: applicazioni

*Si applica a: Azure Rights Management, Office 365*


Usare la tabella seguente per identificare le applicazioni che offrono supporto nativo per Azure RMS, che è perfettamente integrato in queste applicazioni grazie alle API RMS, usate per supportare le restrizioni d'utilizzo. Queste applicazioni sono anche dette applicazioni abilitate per RMS.

Se non diversamente indicato, le funzionalità supportate sono valide sia per Azure RMS che per AD RMS. Per il supporto di AD RMS in iOS, Android, OS X e Windows Phone 8.1 è inoltre richiesta l'[estensione per dispositivi mobili Active Directory Rights Management Services](https://technet.microsoft.com/library/dn673574.aspx).

Informazioni sulle colonne della tabella:

-   **PDF protetto**: file caratterizzati dall'estensione ppdf e creati automaticamente quando si usa l'applicazione RMS sharing per condividere file di Office e file PDF tramite posta elettronica. L'applicazione RMS sharing include un lettore per i file PDF protetti. Se in precedenza sono stati creati file PDF protetti tramite Azure RMS o AD RMS, per continuare a leggere questi file su dispositivi Windows, iOS e Android, è possibile usare Foxit Reader e Nitro Pro.

-   **Posta elettronica**: i client di posta elettronica elencati possono proteggere il messaggio di posta elettronica stesso, proteggendo quindi automaticamente eventuali file allegati. In questo scenario la funzionalità di anteprima del client può visualizzare il contenuto protetto (messaggio e allegato) ai destinatari autorizzati. Se tuttavia un messaggio di posta elettronica non è protetto ma l'allegato è protetto, la funzionalità di anteprima del client non potrà visualizzare l'allegato protetto ai destinatari autorizzati.

-   **Altri tipi di file**: file di testo e di immagine con estensioni quali txt, xml, jpg e jpeg. L'estensione cambia dopo che i file vengono protetti in modalità nativa da RMS e diventano di sola lettura. I file che non possono essere protetti in modalità nativa, dopo essere stati protetti in modo generico da RMS hanno un'estensione di tipo pfile. Per altre informazioni, vedere [Guida dell'amministratore dell'applicazione di condivisione Rights Management](../rms-client/sharing-app-admin-guide.md).


|**Sistema operativo dispositivo**|Word, Excel, PowerPoint|PDF protetto|Posta elettronica|Altri tipi di file|
|-------------------------------|---------------------------|-----------------|---------|--------------------|
|**Windows**|Office 2010<br /><br />Office 2013<br /><br />Office 2016 <br /><br />App Office Mobile (solo Azure RMS) [[1]](#footnote-1)<br /><br />Office Online [[2]](#footnote-2)|Gaaiho Doc<br /><br />GigaTrust Desktop PDF Client for Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br />App di condivisione RMS|Outlook 2010<br /><br />Outlook 2013<br /><br />Office 2016 <br /><br />Outlook Web App (OWA) [[3]](footnote-3)<br /><br />Windows Mail [[4]](footnote-4)|Applicazione RMS sharing per Windows: testo, immagini, pfile<br /><br />Siemens JT2Go: file JT (solo Windows 10)|
|**iOS**|Office per iPad e iPhone [[5]](#footnote-5)<br /><br />Office Online [[2]](#footnote-2)<br /><br />TITUS Docs|Foxit Reader<br /><br />App RMS sharing [[1]](#footnote-1)<br /><br />TITUS Docs|Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook per iPad e iPhone [[4]](#footnote-4)<br /><br />OWA per iOS [[3]](#footnote-3)<br /><br />TITUS Mail|App RMS sharing [[1]](#footnote-1): testo, immagini, pfile<br /><br />TITUS Docs: pfile|
|**Android**|GigaTrust App for Android<br /><br />Office Online [[2]](#footnote-2)|GigaTrust App for Android<br /><br />Foxit Reader<br /><br />App RMS sharing [[1]](#footnote-1)|9Folders [[4]](#footnote-4)<br /><br />GigaTrust App for Android [[4]](#footnote-4)<br /><br />Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook per Android [[4]](#footnote-4)<br /><br />OWA per Android [[3]](#footnote-3) e [[7]](#footnote-7)<br /><br />Samsung Email (S3 e versioni successive) [[7]](#footnote-7)<br /><br />Classificazione TITUS per dispositivi mobili|App RMS sharing [[1]](#footnote-1): testo, immagini, pfile|
|**OS X**|Office 2011 (solo AD RMS)<br /><br />Office 2016 per Mac<br /><br />Office Online [[2]](#footnote-2)|Foxit Reader<br /><br />App RMS sharing [[1]](#footnote-1)|Outlook 2011 (solo AD RMS)<br /><br />Outlook 2016 per Mac<br /><br />Outlook per Mac|App RMS sharing [[1]](#footnote-1): testo, immagini, pfile|
|**Windows 10 Mobile**|App Office Mobile (solo Azure RMS)[[1]](#footnote-1)|Non supportato|Citrix WorxMail [[6]](#footnote-6)<br /><br />Posta di Outlook|Non supportato|
|**Windows RT**|Office 2013 RT<br /><br />Office Online [[2]](#footnote-2)|Non supportato|Outlook 2013 RT<br /><br />App di posta elettronica per Windows<br /><br />Windows Mail [[4]](#footnote-4)|Siemens JT2Go: file JT|
|**Windows Phone 8.1**|Office Mobile (solo AD RMS)|App RMS sharing [[1]](#footnote-1)|Outlook Mobile [[4]](#footnote-4)|App RMS sharing [[1]](#footnote-1): testo, immagini, pfile|
|**Blackberry 10**|Non supportato|Non supportato|Posta elettronica Blackberry [[4]](#footnote-4)|Non supportato|


###### Nota 1
supporta la visualizzazione di contenuti protetti.

###### Nota 2 
supporta la visualizzazione di contenuti protetti in SharePoint Online, OneDrive for Business e Outlook Web Access.

###### Nota 3
se un destinatario ha una cassetta postale di Exchange in locale e riceve un messaggio di posta elettronica protetto, il contenuto può essere aperto solo con un client di posta elettronica, come Outlook,  e non da Outlook Web Access.

###### Nota 4
utilizza Exchange ActiveSync IRM, che deve essere abilitato dall'amministratore di Exchange. Gli utenti possono visualizzare, rispondere e rispondere a tutti per messaggi di posta elettronica protetti, ma gli utenti non possono proteggere i nuovi messaggi di posta elettronica da sé.

Se un destinatario ha una cassetta postale di Exchange in locale e riceve un messaggio di posta elettronica protetto da un'altra organizzazione che usa Exchange, il contenuto può essere aperto solo con un client di posta elettronica, come Outlook,  e non con un dispositivo che usa Exchange Active Sync IRM.

###### Nota 5
supporta la visualizzazione e la modifica di documenti protetti. Per altre informazioni, vedere il post sul blog di Office relativo al [supporto per Azure Rights Management disponibile in Office per iPad e iPhone](https://blogs.office.com/2015/07/22/azure-rights-management-support-comes-to-office-for-ipad-and-iphone-2/)

###### Nota 6
Per altre informazioni, vedere la [documentazione del prodotto Citrix per WorxMail](http://docs.citrix.com/en-us/worx-mobile-apps/10/xmob-worx-mail.html).

###### Nota 7
Per altre informazioni, vedere il post sul blog di Office relativo a [OWA per Android ora disponibile su dispositivi specifici](http://blogs.office.com/2014/06/11/owa-for-android-now-available-on-select-devices/)

## Altre informazioni sul supporto di Azure RMS per Office

Tutte le edizioni di Office, ad eccezione di Office 2007, possono utilizzare il contenuto protetto.

Azure RMS con Office Professional Plus 2010 oppure Office Professional 2010:

- Richiede l'applicazione di condivisione Microsoft Rights Management per Windows

- Non supportato in Windows 10


## Altre informazioni sull'applicazione di condivisione Rights Management

Per altre informazioni sull'applicazione di condivisione Rights Management per Windows, vedere le risorse seguenti:

-   [Guida dell'amministratore dell'applicazione di condivisione Rights Management](../rms-client/sharing-app-admin-guide.md)

-   [Guida dell'utente dell'applicazione di condivisione Rights Management](../rms-client/sharing-app-user-guide.md)

Per altre informazioni sull'applicazione di condivisione Rights Management per piattaforme mobili, vedere le risorse seguenti:

-   Per scaricare l'applicazione desiderata, fare clic sul collegamento corrispondente nella pagina [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970)

-   Se si dispone di Microsoft Intune, è possibile distribuire e gestire l'app mediante un'app gestita da criteri: 

    -   Per dispositivi iOS e Android registrati da Intune, vedere l’articolo relativo alla [configurazione e distribuzione dei criteri di gestione delle applicazioni mobili nella console di Microsoft Intune](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console).

    -   Per i dispositivi Android che non sono registrati da Intune, vedere [Creare e distribuire i criteri di gestione delle app per dispositivi mobili con Microsoft Intune](/intune/deploy-use/create-and-deploy-mobile-app-management-policies-with-microsoft-intune)

-   [Domande frequenti sull'applicazione di condivisione Microsoft Rights Management per piattaforme mobili](https://technet.microsoft.com/dn451248)



## Altre informazioni su ulteriori applicazioni che supportano Azure RMS

Oltre alle applicazioni riportate nella tabella, è possibile integrare con Azure RMS le applicazioni che supportano le API RMS, tra cui:

- Applicazioni line-of-business create internamente mediante RMS SDK

- Applicazioni di fornitori di software create mediante RMS SDK

Per altre informazioni sull'SDK, vedere la pagina relativa a [Microsoft Rights Management SDK](../develop/developers-guide.md).

## Applicazioni non supportate da Azure RMS

Le applicazioni chi non sono attualmente supportate da Azure RMS sono le seguenti:

-   Microsoft Office per Mac 2011

-   Microsoft OneDrive for Business per SharePoint Server 2013

-   XPS Viewer
 
L'applicazione RMS sharing prevede inoltre le restrizioni seguenti:

-   Per i computer Windows, la versione minima richiesta è Windows 7 Service Pack 1



## Passaggi successivi
Per verificare gli altri requisiti, vedere [Requisiti per Azure Rights Management](requirements-azure-rms.md).

Per altre informazioni sul supporto di Azure RMS da parte delle applicazioni più diffuse, vedere [Supporto di Microsoft Azure Rights Management da parte delle applicazioni](../understand-explore/applications-support.md).

Per informazioni sulle modalità di configurazione delle applicazioni più diffuse per Azure RMS, vedere [Configurazione di applicazioni per Azure Rights Management](../deploy-use/configure-applications.md).

<!--HONumber=May16_HO2-->


