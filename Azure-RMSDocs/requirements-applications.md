---
title: Supporto delle applicazioni per la protezione dei dati RMS - AIP
description: Identificare le applicazioni che usano le API di RMS per il supporto nativo del servizio Azure Rights Management di Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/17/2019
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 0f83401b8cac96820f2628a501ca2f731d678126
ms.sourcegitcommit: 2daa75cda8475028a3dac83d70505fcfccef42a1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/17/2019
ms.locfileid: "54361801"
---
# <a name="applications-that-support-azure-rights-management-data-protection"></a>Applicazioni che supportano la protezione dati di Azure Rights Management

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Usare le tabelle seguenti per identificare le applicazioni e le soluzioni che supportano il servizio Azure Rights Management (Azure RMS) a livello nativo, che garantisce la protezione dei dati per Azure Information Protection.

Per queste applicazioni e soluzioni, il supporto di Rights Management è perfettamente integrato mediante l'uso delle API di Rights Management per le restrizioni di utilizzo. Queste applicazioni e soluzioni sono anche note come "abilitate per RMS".

Se non diversamente indicato, le funzionalità supportate sono valide sia per Azure RMS che per AD RMS. Per il supporto di AD RMS in iOS, Android, macOS e Windows Phone 8.1 è inoltre richiesta l'[estensione per dispositivi mobili Active Directory Rights Management Services](https://technet.microsoft.com/library/dn673574.aspx).

## <a name="rms-enlightened-applications"></a>Applicazioni abilitate per RMS

La tabella seguente mostra le applicazioni client abilitate per RMS di Microsoft e dei fornitori di software. 

Per informazioni sulla visualizzazione dei documenti PDF protetti, vedere [Lettori di file PDF protetti per Microsoft Information Protection](./rms-client/protected-pdf-readers.md).

Informazioni sulle colonne della tabella:

-   **Posta elettronica:** i client di posta elettronica elencati possono proteggere il messaggio di posta elettronica, che a sua volta protegge automaticamente eventuali file Office allegati non protetti. In questo scenario la funzionalità di anteprima del client può visualizzare il contenuto protetto (messaggio e allegato) ai destinatari autorizzati. Se tuttavia un messaggio di posta elettronica non è protetto ma l'allegato è protetto, la funzionalità di anteprima del client non potrà visualizzare l'allegato protetto ai destinatari autorizzati. 
    
    Suggerimento: Per i client di posta elettronica che non supportano la protezione della posta elettronica, valutare la possibilità di usare [regole del flusso di posta elettronica di Exchange Online per applicare questa protezione](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8).

-   **Altri tipi di file**: file di testo e di immagine con estensioni quali TXT, XML, JPG e JPEG. L'estensione cambia dopo che i file vengono protetti in modo nativo da Rights Management e diventano di sola lettura. I file che non possono essere protetti in modo nativo, dopo essere stati protetti in modo generico da Rights Management hanno un'estensione di tipo pfile. Per altre informazioni, vedere [Tipi di file supportati](./rms-client/client-admin-guide-file-types.md) nella Guida dell'amministratore del client Azure Information Protection.


|**Sistema operativo dispositivo**|Word, Excel, PowerPoint|Posta elettronica|Altri tipi di file|
|---------------------------|-----------------------|-----------------|---------|
|**Windows**|Office 2010<br /><br />Office 2013<br /><br />Office 2016 <br /><br />Office Online (visualizzazione di documenti protetti) [[1]](#footnote-1)<br /><br />Web browser [[2]](#footnote-2)|Outlook 2010<br /><br />Outlook 2013<br /><br />Office 2016 <br /><br />Web browser [[3]](#footnote-3)<br /><br />Windows Mail [[4]](#footnote-4) |Client Azure Information Protection per Windows: Testo, immagini, pfile<br /><br />Applicazione di condivisione RMS per Windows: Testo, immagini, pfile<br /><br />Plug-in SealPath RMS per AutoCAD: dwg|
|**iOS**|GigaTrust<br /><br /> Office Mobile (visualizzazione e modifica di documenti protetti)<br /><br />Office Online [[1]](#footnote-1)<br /><br />TITUS Docs<br /><br />Web browser [[2]](#footnote-2)|App Azure Information Protection (visualizzazione di posta elettronica protetta)<br /><br />BlackBerry Work<br /><br />Citrix WorxMail <br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook per iPad e iPhone [[4]](#footnote-4)<br /><br />TITUS Mail <br /><br />Web browser [[3]](#footnote-3)|App Azure Information Protection (visualizzazione di testo e immagini di protezione)<br /><br />TITUS Docs: Pfile|
|**Android**|GigaTrust App for Android<br /><br />Office Online [[1]](#footnote-1)<br /><br />Office Mobile <br /><br />Web browser [[2]](#footnote-2)|9Folders [[4]](#footnote-4)<br /><br />App Azure Information Protection (visualizzazione di messaggi di posta elettronica protetti)<br /><br />BlackBerry Work <br /><br />GigaTrust App for Android [[4]](#footnote-4)<br /><br />Citrix WorxMail <br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook per Android [[4]](#footnote-4)<br /><br />Samsung Email (S3 e versioni successive) [[4]](#footnote-4)<br /><br />Classificazione TITUS per dispositivi mobili <br /><br />Web browser [[3]](#footnote-3)|App Azure Information Protection (visualizzazione di testo e immagini protetti)|
|**macOS**|Office 2016 per Mac<br /><br />Office Online [[1]](#footnote-1)<br /><br />Web browser [[2]](#footnote-2)|Outlook 2016 per Mac<br /><br />Web browser [[3]](#footnote-3)|App RMS sharing (visualizzazione di testo e immagini protetti e di file protetti in modo generico)|
|**Windows 10 Mobile**|App Office Mobile (visualizzazione di documenti protetti con Azure RMS) <br /><br />Web browser [[2]](#footnote-2)|Citrix WorxMail <br /><br />Posta di Outlook (visualizzazione di messaggi di posta elettronica protetti) <br /><br />Web browser [[3]](#footnote-3)|Non supportato|
|**Windows RT**|Office 2013 RT<br /><br />Office Online [[1]](#footnote-1)<br /><br />Web browser [[2]](#footnote-2)|Outlook 2013 RT<br /><br />App di posta elettronica per Windows<br /><br />Web browser [[3]](#footnote-3)<br /><br />Windows Mail [[4]](#footnote-4)|Siemens JT2Go: file JT|
|**Windows Phone 8.1**|Office Mobile (solo AD RMS)<br /><br />Web browser [[2]](#footnote-2)|Outlook Mobile [[4]](#footnote-4) <br /><br />Web browser [[3]](#footnote-3)|App RMS sharing (visualizzazione di testo e immagini protetti e di file protetti in modo generico)|
|**Blackberry 10**|Web browser [[2]](#footnote-2)|Posta elettronica Blackberry [[4]](#footnote-4) <br /><br />Web browser [[3]](#footnote-3)|Non supportato|

###### <a name="footnote-1"></a>Nota 1
Supportato solo con SharePoint Online e OneDrive for Business e i documenti devono essere non protetti prima di essere caricati in una libreria protetta.

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

Vedere anche: [Descrizione del servizio per le applicazioni di Office](https://technet.microsoft.com/library/office-applications-service-description.aspx)

#### <a name="windows-computers-for-information-rights-management-irm"></a>Computer Windows per Information Rights Management (IRM)

Le famiglie di prodotti client di Office seguenti supportano la protezione dei file e dei messaggi di posta elettronica nei computer Windows tramite il servizio Azure Rights Management:

- Office 365 con le app di Office 2016 (versione minima 1805, build 9330.2078) quando all'utente viene assegnata una licenza per Azure Rights Management (detto anche Azure Information Protection per Office 365)

- Office 365 ProPlus: Office 2016 e Office 2013
    
    Queste edizioni di Office sono incluse nella maggior parte, ma non in tutte le sottoscrizione di Office 365 che includono la protezione dati di Azure Information Protection. Controllare le informazioni sulla sottoscrizione per verificare se Office 365 ProPlus è incluso. Queste informazioni si possono trovare anche nel [foglio dati di Azure Information Protection](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

- Office Professional Plus 2016

- Office Professional Plus 2013

- Office Professional Plus 2010 con Service Pack 2

Tutte le edizioni di Office, ad eccezione di Office 2007, possono utilizzare il contenuto protetto.

Quando si usa il servizio Azure Rights Management con Office Professional Plus 2010 e Service Pack 2 o Office Professional 2010 con Service Pack 2:

- Richiede il client Azure Information Protection per Windows o l'applicazione di condivisione Rights Management per Windows.

- Non supportato in Windows 10.

- Non supporta l'autenticazione basata su moduli per gli account utente federati. Questi account devono usare l'Autenticazione integrata di Windows.

- Non supporta l'override della protezione dei modelli tramite autorizzazioni personalizzate selezionate con il client di Azure Information Protection. In questo scenario, prima di applicare autorizzazioni personalizzate è necessario rimuovere la protezione originaria.

#### <a name="mac-computers-for-information-rights-management-irm"></a>Computer Mac per Information Rights Management (IRM)

Le famiglie di prodotti client di Office seguenti supportano la protezione dei file e dei messaggi di posta elettronica in macOS tramite Azure RMS:

- Office 365 ProPlus: Office 2016

- Office Standard 2016 per Mac

Tutte le edizioni di Office per Mac 2016 supportano l'utilizzo di contenuto protetto.

Suggerimento: per iniziare a proteggere i documenti usando Office per Mac può essere utile leggere la sezione [Come configurare un computer Mac per proteggere e tracciare i documenti?](faqs-rms.md#how-do-i-configure-a-mac-computer-to-protect-and-track-documents) delle domande frequenti.

### <a name="more-information-about-the-azure-information-protection-app-for-ios-and-android"></a>Altre informazioni sull'app Azure Information Protection per iOS e Android

L'app Azure Information Protection per iOS e Android fornisce un visualizzatore per i messaggi di posta elettronica protetti con RMS (file con estensione rpmsg) quando questi dispositivi mobili non dispongono di un'app di posta elettronica che supporta l'apertura di messaggi di posta elettronica protetti. Questa app consente anche di aprire file PDF, file di testo e di immagini protetti con RMS.

Se i dispositivi iOS e Android sono registrati da Microsoft Intune, gli utenti possono installare l'app dal portale aziendale e si può gestire l'app con i [criteri di protezione delle app](/intune/app-protection-policies) di Intune.

Per altre informazioni su come usare l'app, vedere [Domande frequenti sull'app Azure Information Protection per iOS e Android](./rms-client/mobile-app-faq.md).


### <a name="more-information-about-the-azure-information-protection-client-for-windows"></a>Altre informazioni sul client Azure Information Protection per Windows

Questo client sostituisce ora l'applicazione di condivisione Rights Management per Windows.

Per altre informazioni, vedere le risorse seguenti:

- [Guida per l'amministratore del client di Azure Information Protection](./rms-client/client-admin-guide.md)

- [Guida per l'utente del client Azure Information Protection](./rms-client/client-user-guide.md)

- [Domande frequenti sull'app Azure Information Protection per iOS e Android](./rms-client/mobile-app-faq.md)

Per scaricare l'app desiderata, fare clic sul collegamento corrispondente nella [pagina di Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970).

### <a name="more-information-about-the-rights-management-sharing-application"></a>Altre informazioni sull'applicazione Rights Management sharing

Questa applicazione verrà sostituita dal client Azure Information Protection. È ancora necessaria per i dispositivi mobili Windows Phone per visualizzare i file protetti. 

Per i computer Mac offre un visualizzatore per file PDF (con estensione ppdf) protetti, immagini con testo protetto e file protetti in modo generico. L'app RMS sharing per Mac è anche in grado di proteggere i file di immagine, ma non altri file. Per proteggere i file di Office, usare Office per Mac. 

Per altre informazioni, vedere le risorse seguenti:

-   [Guida dell'amministratore dell'applicazione di condivisione Rights Management](./rms-client/sharing-app-admin-guide.md)

-   [Guida dell'utente dell'applicazione di condivisione Rights Management](./rms-client/sharing-app-user-guide.md)

-   [Domande frequenti sull'applicazione di condivisione Microsoft Rights Management per piattaforme mobili](https://technet.microsoft.com/dn451248)

Scaricare il visualizzatore per computer Mac e per dispositivi Windows Phone usando il collegamento corrispondente nella [pagina di Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970).


### <a name="more-information-about-other-applications-that-support-azure-information-protection"></a>Altre informazioni su ulteriori applicazioni che supportano Azure Information Protection

Oltre alle applicazioni nella tabella, tutte le applicazioni che supportano le API per il servizio Azure Rights Management possono essere integrate con Azure Information Protection, tra cui:

- Applicazioni line-of-business create internamente mediante RMS SDK

- Applicazioni di fornitori di software create mediante RMS SDK

Per altre informazioni, vedere la [Guida per gli sviluppatori di Azure Information Protection](./develop/developers-guide.md).

### <a name="applications-that-are-not-supported-by-azure-rms"></a>Applicazioni non supportate da Azure RMS

Le applicazioni chi non sono attualmente supportate da Azure RMS sono le seguenti:

-   Microsoft OneDrive for Business per SharePoint Server 2013

-   XPS Viewer

L'applicazione di condivisione RMS e il client Azure Information Protection prevedono anche le restrizioni seguenti:

-   Per i computer Windows: la versione minima richiesta è Windows 7 Service Pack 1

## <a name="rms-enlightened-solutions"></a>Soluzioni abilitate per RMS

La tabella seguente mostra le soluzioni abilitate per RMS dei fornitori di software.

Se si è un fornitore di software e si ha una soluzione per questa tabella non inclusa nell'elenco, registrare l'applicazione con Azure AD. Per altre informazioni, vedere [Come registrare l'app e abilitarla per RMS con Azure AD](./develop/authentication-integration.md).


|Prodotto|Fornitore|Descrizione|
|-------------------------------|---------------------------|-----------------|
|Absolute|Absolute|Prevenzione della perdita dei dati (DLP) per proteggere il contenuto.|
|Content Locker|VMware|Funzionalità per archiviare, utilizzare e creare contenuto protetto.|
|Controle|TakeControle|eDiscovery tramite l'assegnazione di etichette e la protezione.|
|Forcepoint|Forcepoint DLP|Soluzione di prevenzione della perdita dei dati (DLP) degli endpoint per l'applicazione dei criteri di sicurezza dei dati dell'organizzazione.|
|Halocore|Secude|Protezione dei file esportati da ambienti SAP.|
|MaaS 360|IBM|Integrazione per l'utilizzo e la protezione di documenti.|
|Mobiliya|Mobiliya|Protezione di documenti provenienti da repository Documentum di EMC.
|Ramessys|Ramessys|Integrazione per Chemcart e Documentum.
|Sealpath|Sealpath Technologies|Integrazione con strumenti di progettazione CAD, ad esempio AutoCAD e Siemens Jt2GO.
|SecRMM|Sqaudra Technologies |Protezione dei documenti per i supporti rimovibili.
|Security Sheriff|CryptZone |Gestione degli accessi in SharePoint e protezione dei documenti, in base alla classificazione e alle autorizzazioni di accesso.
|Symantec DLP|Symantec |Rilevamento e monitoraggio per i file protetti.

## <a name="next-steps"></a>Passaggi successivi
Per verificare gli altri requisiti, vedere [Requisiti per Azure Information Protection](requirements.md).

Per altre informazioni sul supporto di Azure RMS da parte delle applicazioni più diffuse, vedere [Supporto del servizio Azure Rights Management da parte delle applicazioni](./applications-support.md).

Per informazioni sulle modalità di configurazione delle applicazioni più diffuse per Azure RMS, vedere [Configurazione di applicazioni per Azure Rights Management](configure-applications.md).

