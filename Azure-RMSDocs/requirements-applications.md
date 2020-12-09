---
title: Supporto delle applicazioni per la protezione dei dati RMS per Azure Information Protection
description: Identificare le applicazioni e le soluzioni con supporto nativo per il servizio Azure Rights Management (Azure RMS). Azure RMS offre la protezione dei dati per Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 10/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa
ms.subservice: prereqs
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: f25b020a72a48e79b24840a597aefd4cc9e594af
ms.sourcegitcommit: 13dac930fabafeb05d71d7ae8acf5c0a78c12397
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/08/2020
ms.locfileid: "96849704"
---
# <a name="applications-that-support-azure-rights-management-data-protection"></a>Applicazioni che supportano la protezione dati di Azure Rights Management

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Le applicazioni e le soluzioni elencate in questa pagina supportano a livello nativo il servizio Azure Rights Management (Azure RMS), che garantisce la protezione dei dati per Azure Information Protection.

Queste applicazioni e soluzioni sono dette "abilitate per RMS" e il supporto di Rights Management e delle [restrizioni di utilizzo](configure-usage-rights.md) è perfettamente integrato mediante l'uso delle API di Rights Management.

> [!NOTE]
> Se non diversamente indicato, le funzionalità supportate sono valide sia per Azure RMS che per AD RMS. 
>
> Per il supporto di AD RMS in iOS, Android, macOS e Windows Phone 8.1 è inoltre richiesta l'[estensione di Active Directory Rights Management Services per dispositivi mobili](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\)).
> 

## <a name="windows-rms-enlightened-applications"></a>Applicazioni Windows abilitate per RMS

|Tipo  |Applicazioni supportate   |
|---------|---------|
|**Word, Excel, PowerPoint**    | - [Microsoft 365 Apps](#microsoft-365-app-support) <br />- Office 2010 <br />- Office 2013<br />- Office 2016 <br />- Office 2019 <br />- [Office per il Web (visualizzazione di documenti protetti)](#viewing-protected-documents-in-office-for-the-web)<br />- [Web browser](#web-browser-support)        |
|[**E-mail**](#viewing-protected-content-in-email-clients)      |   - Outlook 2010<br />- Outlook 2013<br />- Outlook 2016 <br />- Outlook 2019 <br />- Outlook di Microsoft 365 Apps for enterprise<br />- [Web browser](#web-browser-support)<br />- [Windows Mail](#email-clients-using-exchange-activesync-irm)|
|[**Altri tipi di file**](#supported-text-and-image-file-types)    |  -Visio di Microsoft 365 Apps, Office 2019 e Office 2016: **.vsdm,** **.vsdx,** **.vssm**, **.vstm**, **.vssx**, **.vstx** <br />- Client Azure Information Protection per Windows: Testo, immagini, **pfile** <br />- Plug-in SealPath RMS per AutoCAD: **.dwg**       |
| | |

## <a name="macos-rms-enlightened-applications"></a>Applicazioni macOS abilitate per RMS

|Tipo  |Applicazioni supportate   |
|---------|---------|
|**Word, Excel, PowerPoint**    |  - Microsoft 365 Apps, versione 16.40 o successive <br />- Office 2019 per Mac, versione 16.40 o successive<br />- Office 2016 per Mac, versione 16.16.27 o successive<br />- [Office per il Web](#viewing-protected-documents-in-office-for-the-web)<br />- [Web browser](#web-browser-support)    |
|[**E-mail**](#viewing-protected-content-in-email-clients)   |   - Outlook 2019 per Mac, versione 16.40 o successive<br />- Outlook 2016 per Mac, versione 16.16.27 o successive<br />- [Web browser](#web-browser-support)     |
|[**Altri tipi di file**](#supported-text-and-image-file-types)    | App RMS sharing (visualizzazione di testo e immagini protetti e di file protetti in modo generico)   |
| | |

## <a name="android-rms-enlightened-applications"></a>Applicazioni Android abilitate per RMS

|Tipo  |Applicazioni supportate   |
|---------|---------|
|**Word, Excel, PowerPoint**    |- App GigaTrust per Android<br />- [Office per il Web](#viewing-protected-documents-in-office-for-the-web)<br />- Office Mobile (a meno che non si utilizzino etichette di riservatezza, limitato alla visualizzazione e alla modifica di documenti protetti) <br />- [Web browser](#web-browser-support)      |
|[**E-mail**](#viewing-protected-content-in-email-clients)     | - [9Folders](#email-clients-using-exchange-activesync-irm)<br />- App Azure Information Protection (visualizzazione di messaggi di posta elettronica protetti)<br />- BlackBerry Work <br />- [App GigaTrust per Android](#email-clients-using-exchange-activesync-irm) <br />- Citrix WorxMail <br />- [NitroDesk](#email-clients-using-exchange-activesync-irm)<br />- [Outlook per Android](#email-clients-using-exchange-activesync-irm)<br />- [Samsung Email (S3 e versioni successive)](#email-clients-using-exchange-activesync-irm)<br />- TITUS Classification for Mobile <br /><br />- [Web browser](#web-browser-support)       |
|[**Altri tipi di file**](#supported-text-and-image-file-types)    |  App Azure Information Protection (visualizzazione di testo e immagini protetti)  |
| | |


## <a name="ios-rms-enlightened-applications"></a>Applicazioni iOS abilitate per RMS

|Tipo  |Applicazioni supportate   |
|---------|---------|
|**Word, Excel, PowerPoint**    |  - GigaTrust<br />- Office Mobile <br />- [Office per il Web](#viewing-protected-documents-in-office-for-the-web)<br />- TITUS Docs<br />- [Web browser](#web-browser-support)    |
|[**E-mail**](#viewing-protected-content-in-email-clients)     |   - App Azure Information Protection (visualizzazione di posta elettronica protetta)<br />- BlackBerry Work<br />- Citrix WorxMail <br />- [NitroDesk](#email-clients-using-exchange-activesync-irm)<br />- [Outlook per iPad e iPhone](#email-clients-using-exchange-activesync-irm)<br />- TITUS Mail <br />- [Web browser](#web-browser-support)     |
|[**Altri tipi di file**](#supported-text-and-image-file-types)     | - App Azure Information Protection (visualizzazione di testo e immagini di protezione)<br />- TITUS Docs: **Pfile**  |
| | |

## <a name="windows-10-mobile-rms-enlightened-applications"></a>Applicazioni Windows 10 Mobile abilitate per RMS

|Tipo  |Applicazioni supportate   |
|---------|---------|
|**Word, Excel, PowerPoint**    | - App Office Mobile (visualizzazione di documenti protetti con Azure RMS) <br />- [Web browser](#web-browser-support)    |
|[**E-mail**](#viewing-protected-content-in-email-clients)    |  - Citrix WorxMail <br />- Posta di Outlook (visualizzazione di messaggi di posta elettronica protetti) <br />- [Web browser](#web-browser-support)     |
|[**Altri tipi di file**](#supported-text-and-image-file-types)    | Non supportato   |
| | |

## <a name="blackberry-10-rms-enlightened-applications"></a>Applicazioni Blackberry 10 abilitate per RMS

|Tipo  |Applicazioni supportate   |
|---------|---------|
|**Word, Excel, PowerPoint**    | - [Web browser](#web-browser-support)    |
|[**E-mail**](#viewing-protected-content-in-email-clients)   | - [Posta elettronica Blackberry](#email-clients-using-exchange-activesync-irm) <br />- [Web browser](#web-browser-support)      |
|[**Altri tipi di file**](#supported-text-and-image-file-types)    | Non supportato   |
| | |


## <a name="additional-details-about-rms-enlightened-applications"></a>Altre informazioni sulle applicazioni abilitate per RMS

Per ulteriori informazioni sulle applicazioni abilitate per RMS elencate in precedenza, vedere:

- [Visualizzazione di contenuto protetto nei client di posta elettronica](#viewing-protected-content-in-email-clients)
- [Tipi di file di testo e di immagine supportati](#supported-text-and-image-file-types)
- [Supporto delle app di Microsoft 365](#microsoft-365-app-support)
- [Visualizzazione di documenti protetti in Office per il Web](#viewing-protected-documents-in-office-for-the-web)
- [Supporto Web browser](#web-browser-support)
- [Client di posta elettronica che usano Information Rights Management (IRM) in Exchange ActiveSync](#email-clients-using-exchange-activesync-irm)

### <a name="viewing-protected-content-in-email-clients"></a>Visualizzazione di contenuto protetto nei client di posta elettronica

Quando un client di posta elettronica protegge un messaggio, gli eventuali file di Office allegati al messaggio e attualmente non protetti vengono protetti insieme al messaggio di posta elettronica. In questi casi, sia il messaggio di posta elettronica che gli allegati possono essere visualizzati nel client di posta elettronica solo da destinatari autorizzati.

Tuttavia, se è protetto solo l'allegato e non il messaggio di posta elettronica, il client di posta elettronica non visualizzare in anteprima l'allegato, neanche i per destinatari autorizzati.

> [!TIP]
> Per i client di posta elettronica che non supportano la protezione della posta elettronica, valutare la possibilità di usare [regole del flusso di posta elettronica di Exchange Online per applicare questa protezione](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8).

### <a name="supported-text-and-image-file-types"></a>Tipi di file di testo e di immagine supportati

I tipi di file diversi dai messaggi di posta elettronica e dai file di Office includono file di testo e di immagine con estensioni quali **txt**, **xml**, **jpg** e **jpeg**. 

Dopo che i file vengono protetti in modo nativo da Rights Management l'estensione cambia e i file diventano di sola lettura. 

I file che non possono essere protetti in modo nativo, dopo essere stati protetti in modo generico da Rights Management hanno un'estensione di tipo **pfile**.

Per altre informazioni, vedere [Tipi di file supportati](./rms-client/client-admin-guide-file-types.md).

### <a name="microsoft-365-app-support"></a>Supporto delle app di Microsoft 365

Include: 
- App di Office per le versioni elencate nella [tabella delle versioni supportate di Microsoft 365 App in base al canale di aggiornamento](/officeupdates/update-history-microsoft365-apps-by-date), da Microsoft 365 Apps for business o Microsoft 365 Business Premium quando all'utente è assegnata una licenza per Azure Rights Management (noto anche come Azure Information Protection per Office 365)
- Microsoft 365 Apps for enterprise

### <a name="viewing-protected-documents-in-office-for-the-web"></a>Visualizzazione di documenti protetti in Office per il Web

Supportata solo con Microsoft SharePoint e OneDrive e i documenti devono essere non protetti prima di essere caricati in una libreria protetta.

### <a name="web-browser-support"></a>Supporto Web browser

- I Web browser sono supportati per i file di **Word, Excel e PowerPoint** quando gli [allegati di Office](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM) sono protetti usando la [crittografia dei messaggi di Microsoft 365 con le nuove funzionalità](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801).

- Per i **messaggi di posta elettronica**, i Web browser sono supportati solo negli scenari seguenti:

    - Se il mittente e il destinatario fanno parte della stessa organizzazione
    - Se il mittente o il destinatario usa Exchange Online
    - Se il mittente usa Exchange locale in una configurazione ibrida 

### <a name="email-clients-using-exchange-activesync-irm"></a>Client di posta elettronica che usano IRM in Exchange ActiveSync

I client di posta elettronica seguenti usano IRM in Exchange ActiveSync, che deve essere abilitato dall'amministratore di Exchange:

- Windows Mail
- 9Folders
- GigaTrust App for Android
- NitroDesk
- Outlook per Android
- Samsung Email (S3 e versioni successive)
- Office per iPad e iPhone
- Posta elettronica Blackberry

Gli utenti possono visualizzare i messaggi di posta elettronica protetti, rispondere al mittente di questi e rispondere a tutti, ma non sono in grado di proteggere i nuovi messaggi.
 
Se l'applicazione di posta elettronica non riesce a eseguire il rendering del messaggio perché Exchange ActiveSync IRM non è abilitato, il destinatario può visualizzare il messaggio in un Web browser se il mittente usa Exchange Online o Exchange locale in una configurazione ibrida. 

## <a name="azure-rms-support-for-office"></a>Supporto di Azure RMS per Office

Azure RMS si integra perfettamente nelle applicazioni Word, Excel, PowerPoint e Outlook, dove questa funzionalità viene spesso denominata Information Rights Management (IRM). 

- [Computer Windows per Information Rights Management (IRM)](#windows-computers-for-information-rights-management-irm)
- [Computer Mac per Information Rights Management (IRM)](#mac-computers-for-information-rights-management-irm)

Vedere anche: [Descrizione del servizio per le applicazioni di Office](/office365/servicedescriptions/office-applications-service-description/office-applications-service-description)

### <a name="windows-computers-for-information-rights-management-irm"></a>Computer Windows per Information Rights Management (IRM)

Le famiglie di prodotti client di Office seguenti supportano la protezione dei file e dei messaggi di posta elettronica nei computer Windows tramite il servizio Azure Rights Management:

- **App di Office** per le versioni elencate nella [tabella delle versioni supportate di Microsoft 365 App in base al canale di aggiornamento](/officeupdates/update-history-microsoft365-apps-by-date), da Microsoft 365 Apps for business o Microsoft 365 Business Premium quando all'utente è assegnata una licenza per Azure Rights Management (noto anche come Azure Information Protection per Office 365)

- **Microsoft 365 Apps for enterprise**

    Queste edizioni di Office sono incluse nella maggior parte, ma non in tutte le sottoscrizioni che includono la protezione dati di Azure Information Protection. Controllare le informazioni sulla sottoscrizione per verificare se Microsoft 365 Apps for enterprise ProPlus è incluso. Queste informazioni si possono trovare anche nel [foglio dati di Azure Information Protection](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

- **Office Professional Plus 2019**

- **Office Professional Plus 2016**

- **Office Professional Plus 2013**

- **Office Professional Plus 2010 con Service Pack 2**

Tutte le edizioni di Office, ad eccezione di Office 2007, possono utilizzare il contenuto protetto.

#### <a name="azure-rights-management-service-with-office-professional-plus-2010-and-service-pack-2-or-office-professional-2010-with-service-pack-2"></a>Servizio Azure Rights Management con Office Professional Plus 2010 e Service Pack 2 o Office Professional 2010 con Service Pack 2

Quando si usa il servizio Azure Rights Management con Office Professional Plus 2010 e Service Pack 2 o Office Professional 2010 con Service Pack 2, è necessario avere anche il client AIP per Windows.

Inoltre, questa configurazione:

- Non è supportata in Windows 10.
- Non supporta l'autenticazione basata su moduli per gli account utente federati. Questi account devono usare l'autenticazione integrata di Windows.
- Non supporta la possibilità di eseguire l'override della protezione dei modelli mediante autorizzazioni personalizzate selezionate con il client AIP. In questo scenario, prima di applicare autorizzazioni personalizzate è necessario rimuovere la protezione originaria.

### <a name="mac-computers-for-information-rights-management-irm"></a>Computer Mac per Information Rights Management (IRM)

Le famiglie di prodotti client di Office seguenti supportano la protezione dei file e dei messaggi di posta elettronica in macOS tramite Azure RMS:

- Microsoft 365 Apps for enterprise
- Office Standard 2019 per Mac
- Office Standard 2016 per Mac

Tutte le edizioni di Office per Mac 2019 e Office for Mac 2016 supportano l'utilizzo di contenuto protetto.

> [!TIP]
> per iniziare a proteggere i documenti usando Office per Mac può essere utile leggere la sezione [Come configurare un computer Mac per proteggere e tracciare i documenti?](faqs-rms.md#how-do-i-configure-a-mac-computer-to-protect-and-track-documents) delle domande frequenti.
> 
## <a name="azure-information-protection-apps-for-ios-and-android"></a>App Azure Information Protection per iOS e Android

L'app Azure Information Protection per iOS e Android fornisce un visualizzatore per i messaggi di posta elettronica protetti con RMS (file con estensione **rpmsg**) quando questi dispositivi mobili non dispongono di un'app di posta elettronica che supporti l'apertura di messaggi protetti. Questa app consente anche di aprire file PDF, file di testo e di immagini protetti con RMS.

Se i dispositivi iOS e Android sono registrati da Microsoft Intune, gli utenti possono installare l'app dal portale aziendale e si può gestire l'app con i [criteri di protezione delle app](/intune/apps/app-protection-policies) di Intune.

Per altre informazioni su come usare l'app, vedere [Domande frequenti sull'app Azure Information Protection per iOS e Android](./rms-client/mobile-app-faq.md).

## <a name="the-azure-information-protection-client-for-windows"></a>Client Azure Information Protection per Windows

Il client Azure Information Protection (AIP) include due versioni, con guide per dell'amministratore e dell'utente per ogni versione:

- **Client di etichettatura unificata**:
    - [Guida dell'amministratore](./rms-client/clientv2-admin-guide.md)
    - [Manuale dell'utente](./rms-client/clientv2-user-guide.md)

- **Client classico**:
    - [Guida dell'amministratore](./rms-client/client-admin-guide.md)
    - [Manuale dell'utente](./rms-client/client-user-guide.md)

Scaricare l'app desiderata dalla [pagina di Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970).

> [!NOTE]
> Non si è certi delle differenze tra queste due versioni? Vedere le [domande frequenti](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients) in merito.
> 
## <a name="rights-management-sharing-app"></a>Applicazione di condivisione Rights Management

Per i computer Mac, l'app di condivisione Rights Management offre un visualizzatore per file PDF protetti (con estensione **ppdf**), immagini con testo protetto e file protetti in modo generico. Consente anche di proteggere i file di immagine, ma non altri file. Per proteggere i file di Office in questi computer, usare Office per Mac oppure Microsoft 365 Apps for enterprise. 

Per altre informazioni, vedere le [Domande frequenti sull'applicazione di condivisione Microsoft Rights Management per piattaforme mobili](/previous-versions/msdn10/dn451248(v=msdn.10))

Scaricare l'app di condivisione Rights Management per computer Mac dalla [pagina di Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970).

## <a name="other-applications-that-support-azure-information-protection"></a>Altre applicazioni che supportano Azure Information Protection

Oltre alle applicazioni elencate in precedenza, tutte le applicazioni che supportano le API per il servizio Azure Rights Management possono essere integrate con Azure Information Protection. 

Esempi possono includere applicazioni line-of-business scritte internamente oppure applicazioni di fornitori di software scritte usando gli SDK di RSM.

Per altre informazioni, vedere la [Guida per gli sviluppatori di Azure Information Protection](./develop/developers-guide.md).

## <a name="applications-that-are-not-supported-by-azure-rms"></a>Applicazioni non supportate da Azure RMS

Le applicazioni attualmente non supportate da Azure RMS includono:

- Microsoft OneDrive per SharePoint Server 2013
- XPS Viewer
- Applicazioni eseguite in versioni di Windows precedenti a Windows 7, Service Pack 1


## <a name="next-steps"></a>Passaggi successivi

Vedere anche:

- [Requisiti per Azure Information Protection](requirements.md).
- [Supporto del servizio Azure Rights Management da parte delle applicazioni](./applications-support.md).
- [Configurazione di applicazioni per Azure Rights Management](configure-applications.md).

Per le informazioni più aggiornate sulle soluzioni che supportano il servizio Azure Rights Management e Azure Information Protection, vedere il post di blog [Microsoft Ignite 2019 – Microsoft Information Protection solutions Partner ecosystem showcase](https://techcommunity.microsoft.com/t5/Microsoft-Information-Protection/Microsoft-Ignite-2019-Microsoft-Information-Protection-solutions/ba-p/967024) (Microsoft Ignite 2019 – Presentazione dell'ecosistema di partner per le soluzioni Microsoft Information Protection).