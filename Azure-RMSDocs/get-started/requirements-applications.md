---
title: Supporto delle applicazioni per la protezione dei dati RMS - AIP
description: Identificare le applicazioni che usano le API di RMS per il supporto nativo del servizio Azure Rights Management di Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/27/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: d5371ad1a5fb89176e47406b6c051efd1fa33b37
ms.sourcegitcommit: faaab68064f365c977dfd1890f7c8b05a144a95c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2017
---
# <a name="applications-that-support-azure-rights-management-data-protection"></a>Applicazioni che supportano la protezione dati di Azure Rights Management

>*Si applica a: Azure Information Protection, Office 365*


Usare le tabelle seguenti per identificare le applicazioni e le soluzioni che supportano il servizio Azure Rights Management (Azure RMS) a livello nativo, che garantisce la protezione dei dati per Azure Information Protection.

Per queste applicazioni e soluzioni, il supporto di Rights Management è perfettamente integrato mediante l'uso delle API di Rights Management per le restrizioni di utilizzo. Queste applicazioni e soluzioni sono anche note come "abilitate per RMS".

Se non diversamente indicato, le funzionalità supportate sono valide sia per Azure RMS che per AD RMS. Per il supporto di AD RMS in iOS, Android, macOS e Windows Phone 8.1 è inoltre richiesta l'[estensione per dispositivi mobili Active Directory Rights Management Services](https://technet.microsoft.com/library/dn673574.aspx).

## <a name="rms-enlightened-applications"></a>Applicazioni abilitate per RMS

La tabella seguente mostra le applicazioni client abilitate per RMS di Microsoft e dei fornitori di software.

Informazioni sulle colonne della tabella:

-   **PDF protetto**: questi file possono avere l'estensione di nome file pdf o ppdf.

-   **Posta elettronica:** i client di posta elettronica elencati possono proteggere il messaggio di posta elettronica, che a sua volta protegge automaticamente eventuali file Office allegati non protetti. In questo scenario la funzionalità di anteprima del client può visualizzare il contenuto protetto (messaggio e allegato) ai destinatari autorizzati. Se tuttavia un messaggio di posta elettronica non è protetto ma l'allegato è protetto, la funzionalità di anteprima del client non potrà visualizzare l'allegato protetto ai destinatari autorizzati.

-   **Altri tipi di file**: file di testo e file immagine con estensioni come txt, xml, jpg e jpeg. L'estensione cambia dopo che i file vengono protetti in modo nativo da Rights Management e diventano di sola lettura. I file che non possono essere protetti in modo nativo, dopo essere stati protetti in modo generico da Rights Management hanno un'estensione di tipo pfile. Per altre informazioni, vedere [Tipi di file supportati](../rms-client/client-admin-guide-file-types.md) nella Guida dell'amministratore del client Azure Information Protection.


|**Sistema operativo dispositivo**|Word, Excel, PowerPoint|PDF protetto|Posta elettronica|Altri tipi di file|
|-------------------------------|---------------------------|-----------------|---------|--------------------|
|**Windows**|Office 2010<br /><br />Office 2013<br /><br />Office 2016 <br /><br />Office Online [[1]](#footnote-1)<br /><br />Web browser [[2]](#footnote-2)|Client Azure Information Protection per Windows <br /><br />Gaaiho Doc<br /><br />GigaTrust Desktop PDF Client for Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br />App di condivisione RMS|Outlook 2010<br /><br />Outlook 2013<br /><br />Office 2016 <br /><br />Web browser [[3]](#footnote-3)<br /><br />Windows Mail [[4]](#footnote-4) |Client Azure Information Protection per Windows: testo, immagini, pfile<br /><br />Applicazione RMS sharing per Windows: testo, immagini, pfile<br /><br />Plug-in SealPath RMS per AutoCAD: dwg|
|**iOS**|Office Mobile (visualizzazione e modifica di documenti protetti)<br /><br />Office Online [[1]](#footnote-1)<br /><br />GigaTrust<br /><br /> TITUS Docs<br /><br />Web browser [[2]](#footnote-2)|App Azure Information Protection (visualizzazione di documenti protetti)<br /><br /> Foxit Reader<br /><br />TITUS Docs|App Azure Information Protection (visualizzazione di posta elettronica protetta)<br /><br />Citrix WorxMail <br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook per iPad e iPhone [[4]](#footnote-4)<br /><br />TITUS Mail <br /><br />Web browser [[3]](#footnote-3)|App Azure Information Protection (visualizzazione di testo e immagini di protezione)<br /><br />TITUS Docs: pfile|
|**Android**|GigaTrust App for Android<br /><br />Office Online [[1]](#footnote-1)<br /><br />Office Mobile (visualizzazione di documenti protetti) <br /><br />Web browser [[2]](#footnote-2)|App Azure Information Protection (visualizzazione di documenti protetti) <br /><br />GigaTrust App for Android<br /><br />Foxit Reader|9Folders [[4]](#footnote-4)<br /><br />App Azure Information Protection (visualizzazione di messaggi di posta elettronica protetti)<br /><br />GigaTrust App for Android [[4]](#footnote-4)<br /><br />Citrix WorxMail <br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook per Android [[4]](#footnote-4)<br /><br />Samsung Email (S3 e versioni successive) [[4]](#footnote-4)<br /><br />Classificazione TITUS per dispositivi mobili <br /><br />Web browser [[3]](#footnote-3)|App Azure Information Protection (visualizzazione di testo e immagini protetti)|
|**macOS**|Office 2011 (solo AD RMS)<br /><br />Office 2016 per Mac<br /><br />Office Online [[1]](#footnote-1)<br /><br />Web browser [[2]](#footnote-2)|Foxit Reader<br /><br />App RMS sharing (visualizzazione di documenti protetti)|Outlook 2011 (solo AD RMS)<br /><br />Outlook 2016 per Mac<br /><br />Outlook per Mac <br /><br />Web browser [[3]](#footnote-3)|App RMS sharing (visualizzazione di testo e immagini protetti e di file protetti in modo generico)|
|**Windows 10 Mobile**|App Office Mobile (visualizzazione di documentazione protetta con Azure RMS) <br /><br />Web browser [[2]](#footnote-2)|Non supportato|Citrix WorxMail <br /><br />Posta di Outlook <br /><br />Web browser [[3]](#footnote-3)|Non supportato|
|**Windows RT**|Office 2013 RT<br /><br />Office Online [[1]](#footnote-1)<br /><br />Web browser [[2]](#footnote-2)|Non supportato|Outlook 2013 RT<br /><br />App di posta elettronica per Windows<br /><br />Web browser [[3]](#footnote-3)<br /><br />Windows Mail [[4]](#footnote-4)|Siemens JT2Go: file JT|
|**Windows Phone 8.1**|Office Mobile (solo AD RMS)<br /><br />Web browser [[2]](#footnote-2)|App RMS sharing (visualizzazione di documenti protetti)|Outlook Mobile [[4]](#footnote-4) <br /><br />Web browser [[3]](#footnote-3)|App RMS sharing (visualizzazione di testo e immagini protetti e di file protetti in modo generico)|
|**Blackberry 10**|Web browser [[2]](#footnote-2)|Non supportato|Posta elettronica Blackberry [[4]](#footnote-4) <br /><br />Web browser [[3]](#footnote-3)|Non supportato|


###### <a name="footnote-1"></a>Nota 1
Supporta la visualizzazione di documenti protetti quando un documento non protetto viene caricato in una raccolta protetta di SharePoint Online e OneDrive for Business.

###### <a name="footnote-2"></a>Nota 2
Per [allegati Office](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM) protetti tramite [Office 365 Message Encryption con le nuove funzionalità](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801).

###### <a name="footnote-3"></a>Nota 3
Se il mittente e il destinatario fanno parte della stessa organizzazione. In alternativa, in una delle condizioni seguenti:

- Il mittente o il destinatario usa Exchange Online.

- Il mittente usa Exchange locale in una configurazione ibrida. 

###### <a name="footnote-4"></a>Nota 4
utilizza Exchange ActiveSync IRM, che deve essere abilitato dall'amministratore di Exchange. Gli utenti possono visualizzare i messaggi di posta elettronica protetti, rispondere al mittente di questi e rispondere a tutti, ma non sono in grado di proteggere nuovi messaggi.
 
Se l'applicazione di posta elettronica non riesce a eseguire il rendering del messaggio perché Exchange ActiveSync IRM non è abilitato, il destinatario può visualizzare il messaggio in un Web browser se il mittente usa Exchange Online o Exchange locale in una configurazione ibrida. 



### <a name="more-information-about-azure-rms-support-for-office"></a>Altre informazioni sul supporto di Azure RMS per Office

Azure RMS si integra perfettamente nelle applicazioni Word, Excel, PowerPoint e Outlook, dove questa funzionalità viene spesso denominata Information Rights Management (IRM). 

Le famiglie di prodotti client di Office seguenti supportano la protezione dei file e dei messaggi di posta elettronica nei computer Windows tramite Azure RMS:

- Office 365 ProPlus: Office 2016 e Office 2013

- Office Professional Plus 2016

- Office Professional Plus 2013

- Office Professional Plus 2010 con Service Pack 2

Tutte le edizioni di Office, ad eccezione di Office 2007, possono utilizzare il contenuto protetto.

Azure RMS con Office Professional Plus 2010 con Service Pack 2 o Office Professional 2010 con Service Pack 2:

- Richiede il client Azure Information Protection per Windows o l'applicazione di condivisione Rights Management per Windows.

- Non supportato in Windows 10.

- Non supporta l'autenticazione basata su moduli per gli account utente federati. Questi account devono usare l'Autenticazione integrata di Windows.

- Non supporta l'override della protezione dei modelli tramite autorizzazioni personalizzate selezionate con il client di Azure Information Protection. In questo scenario, prima di applicare autorizzazioni personalizzate è necessario rimuovere la protezione originaria.

Le famiglie di prodotti client di Office seguenti supportano la protezione dei file e dei messaggi di posta elettronica in macOS tramite Azure RMS:

- Office 365 ProPlus: Office 2016

- Office Standard 2016 per Mac

Vedere anche: [Descrizione del servizio per le applicazioni di Office](https://technet.microsoft.com/library/office-applications-service-description.aspx)

### <a name="more-information-about-the-azure-information-protection-app-for-ios-and-android"></a>Altre informazioni sull'app Azure Information Protection per iOS e Android

L'app Azure Information Protection per iOS e Android sostituisce l'app RMS sharing per questi dispositivi. Offre la stessa funzionalità e inoltre supporta i messaggi di posta elettronica e i file PDF protetti da diritti in SharePoint Online.

Se i dispositivi iOS e Android sono registrati da Microsoft Intune, è possibile distribuire e gestire l'app tramite un'app gestita da criteri. Per altre informazioni, vedere l'articolo relativo alla [configurazione e distribuzione dei criteri di gestione delle applicazioni per dispositivi mobili nella console di Microsoft Intune](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console) nella documentazione di Intune Per il Passaggio 2 di questa documentazione di Intune, usare le istruzioni per pubblicare un'app gestita da criteri.

Per altre informazioni, vedere [Domande frequenti sull'app Azure Information Protection per iOS e Android](../rms-client/mobile-app-faq.md).


### <a name="more-information-about-the-azure-information-protection-client-for-windows"></a>Altre informazioni sul client Azure Information Protection per Windows

Questo client sostituisce ora l'applicazione di condivisione Rights Management per Windows.

Per altre informazioni, vedere le risorse seguenti:

- [Guida per l'amministratore del client di Azure Information Protection](../rms-client/client-admin-guide.md)

- [Guida per l'utente del client Azure Information Protection](../rms-client/client-user-guide.md)

- [Domande frequenti sull'app Azure Information Protection per iOS e Android](../rms-client/mobile-app-faq.md)

Per scaricare l'app desiderata, fare clic sul collegamento corrispondente nella [pagina di Microsoft Azure Information Protection](http://go.microsoft.com/fwlink/?LinkId=303970).

### <a name="more-information-about-the-rights-management-sharing-application"></a>Altre informazioni sull'applicazione Rights Management sharing

Questa applicazione verrà sostituita dal client Azure Information Protection. È ancora necessaria per i computer Mac e i dispositivi mobili Windows Phone.

Per altre informazioni, vedere le risorse seguenti:

-   [Guida dell'amministratore dell'applicazione di condivisione Rights Management](../rms-client/sharing-app-admin-guide.md)

-   [Guida dell'utente dell'applicazione di condivisione Rights Management](../rms-client/sharing-app-user-guide.md)

-   [Domande frequenti sull'applicazione di condivisione Microsoft Rights Management per piattaforme mobili](https://technet.microsoft.com/dn451248)

Per scaricare l'app per computer Mac e per dispositivi Windows Phone, fare clic sul collegamento corrispondente nella [pagina di Microsoft Azure Information Protection](http://go.microsoft.com/fwlink/?LinkId=303970).


### <a name="more-information-about-other-applications-that-support-azure-information-protection"></a>Altre informazioni su ulteriori applicazioni che supportano Azure Information Protection

Oltre alle applicazioni nella tabella, tutte le applicazioni che supportano le API per il servizio Azure Rights Management possono essere integrate con Azure Information Protection, tra cui:

- Applicazioni line-of-business create internamente mediante RMS SDK

- Applicazioni di fornitori di software create mediante RMS SDK

Per altre informazioni, vedere la [Guida per gli sviluppatori di Azure Information Protection](../develop/developers-guide.md).

### <a name="applications-that-are-not-supported-by-azure-rms"></a>Applicazioni non supportate da Azure RMS

Le applicazioni chi non sono attualmente supportate da Azure RMS sono le seguenti:

-   Microsoft Office per Mac 2011

-   Microsoft OneDrive for Business per SharePoint Server 2013

-   XPS Viewer

L'applicazione di condivisione RMS e il client Azure Information Protection prevedono anche le restrizioni seguenti:

-   Per i computer Windows, la versione minima richiesta è Windows 7 Service Pack 1

## <a name="rms-enlightened-solutions"></a>Soluzioni abilitate per RMS

La tabella seguente mostra le soluzioni abilitate per RMS dei fornitori di software.

Se si è un fornitore di software e si ha una soluzione per questa tabella non inclusa nell'elenco, registrare l'applicazione con Azure AD. Per altre informazioni, vedere [Come registrare l'app e abilitarla per RMS con Azure AD](../develop/authentication-integration.md).


|Prodotto|Fornitore|Descrizione|
|-------------------------------|---------------------------|-----------------|
|Absolute|Absolute|Prevenzione della perdita dei dati (DLP) per proteggere il contenuto.|
|Content Locker|VMware|Funzionalità per archiviare, utilizzare e creare contenuto protetto.|
|Controle|TakeControle|eDiscovery tramite l'assegnazione di etichette e la protezione.|
|Halocore|Secude|Protezione dei file esportati da ambienti SAP.|
|MaaS 360|IBM|Integrazione per l'utilizzo e la protezione di documenti.|
|Mobiliya|Mobiliya|Protezione di documenti provenienti da repository Documentum di EMC.
|Ramessys|Ramessys|Integrazione per Chemcart e Documentum.
|Sealpath|Sealpath Technologies|Integrazione con strumenti di progettazione CAD, ad esempio AutoCAD e Siemens Jt2GO.
|SecRMM|Sqaudra Technologies |Protezione dei documenti per i supporti rimovibili.
|Security Sheriff|CryptZone |Gestione degli accessi in SharePoint e protezione dei documenti, in base alla classificazione e alle autorizzazioni di accesso.
|Symantec DLP|Symantec |Rilevamento e monitoraggio per i file protetti.

## <a name="next-steps"></a>Passaggi successivi
Per verificare gli altri requisiti, vedere [Requisiti per Azure Information Protection](requirements-azure-rms.md).

Per altre informazioni sul supporto di Azure RMS da parte delle applicazioni più diffuse, vedere [Supporto del servizio Azure Rights Management da parte delle applicazioni](../understand-explore/applications-support.md).

Per informazioni sulle modalità di configurazione delle applicazioni più diffuse per Azure RMS, vedere [Configurazione di applicazioni per Azure Rights Management](../deploy-use/configure-applications.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
