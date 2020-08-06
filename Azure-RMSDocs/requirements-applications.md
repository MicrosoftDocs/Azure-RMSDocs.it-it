---
title: Supporto delle applicazioni per la protezione dei dati RMS per Azure Information Protection
description: Identificare le applicazioni e le soluzioni con supporto nativo per il servizio Azure Rights Management (Azure RMS). Azure RMS fornisce la protezione dei dati per Azure Information Protection (AIP).
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/04/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 7b33bcb8-63da-46be-ad56-b06de97822fa
ms.subservice: prereqs
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 37cb3b1f3c3eb60459cabe813f0cb00fb69b7d5b
ms.sourcegitcommit: dec5df81b569283a72f0a983d3f53b82cbbc562c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/05/2020
ms.locfileid: "87802165"
---
# <a name="applications-that-support-azure-rights-management-data-protection"></a>Applicazioni che supportano la protezione dati di Azure Rights Management

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Le applicazioni e le soluzioni elencate in questa pagina dispongono del supporto nativo per il servizio Azure Rights Management (Azure RMS), che fornisce la protezione dei dati per Azure Information Protection.

Queste applicazioni e soluzioni sono note come "con RMS" e hanno [restrizioni di utilizzo](configure-usage-rights.md) e di Rights Management strettamente integrate con Rights Management API.

> [!NOTE]
> Se non diversamente indicato, le funzionalità supportate sono valide sia per Azure RMS che per AD RMS. 
>
> AD RMS supporto in iOS, Android, macOS e Windows Phone 8,1 richiede anche l' [estensione per dispositivi mobili Active Directory Rights Management Services](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\)).
> 

## <a name="windows-rms-enlightened-applications"></a>Applicazioni abilitate per Windows RMS

|Type  |Applicazioni supportate   |
|---------|---------|
|**Word, Excel, PowerPoint**    | - [App di Office 365](#office-365-app-support) <br />- Office 2010 <br />-Office 2013<br />- Office 2016 <br />-Office 2019 <br />- [Office per il Web (visualizzazione di documenti protetti)](#viewing-protected-documents-in-office-for-the-web)<br />- [Web browser](#web-browser-support)        |
|[**Posta elettronica**](#viewing-protected-content-in-email-clients)      |   -Outlook 2010<br />-Outlook 2013<br />-Outlook 2016 <br />-Outlook 2019 <br />-Outlook da Office 365 ProPlus<br />- [Web browser](#web-browser-support)<br />- [Windows Mail](#email-clients-using-exchange-activesync-irm)|
|[**Altri tipi di file**](#supported-text-and-image-file-types)    |  -Visio dalle app di Office 365, Office 2019 e Office 2016: **. vsdm,** **. vsdx,** **. vssm**, **. vstm**, **. vssx**,. **vstx** <br />-Client Azure Information Protection per Windows: testo, immagini, **Pfile** <br />-Plug-in RMS SealPath per AutoCAD: **. dwg**       |
| | |

## <a name="macos-rms-enlightened-applications"></a>applicazioni abilitate per macOS RMS

|Type  |Applicazioni supportate   |
|---------|---------|
|**Word, Excel, PowerPoint**    |  -App Office 365<br />-Office 2019 per Mac<br />-Office 2016 per Mac<br />- [Office per il Web](#viewing-protected-documents-in-office-for-the-web)<br />- [Web browser](#web-browser-support)    |
|[**Posta elettronica**](#viewing-protected-content-in-email-clients)   |   -Outlook 2019 per Mac<br />-Outlook 2016 per Mac<br />- [Web browser](#web-browser-support)     |
|[**Altri tipi di file**](#supported-text-and-image-file-types)    | App RMS sharing (visualizzazione di testo e immagini protetti e di file protetti in modo generico)   |
| | |

## <a name="android-rms-enlightened-applications"></a>Applicazioni abilitate per Android RMS

|Type  |Applicazioni supportate   |
|---------|---------|
|**Word, Excel, PowerPoint**    |-App GigaTrust per Android<br />- [Office per il Web](#viewing-protected-documents-in-office-for-the-web)<br />-Office Mobile (a meno che non si utilizzino etichette di riservatezza, limitate alla visualizzazione e alla modifica di documenti protetti) <br />- [Web browser](#web-browser-support)      |
|[**Posta elettronica**](#viewing-protected-content-in-email-clients)     | - [9Folders](#email-clients-using-exchange-activesync-irm)<br />-Azure Information Protection app (visualizzazione di messaggi di posta elettronica protetti)<br />-Lavoro BlackBerry <br />- [App GigaTrust per Android](#email-clients-using-exchange-activesync-irm) <br />-Citrix WorxMail <br />- [NitroDesk](#email-clients-using-exchange-activesync-irm)<br />- [Outlook per Android](#email-clients-using-exchange-activesync-irm)<br />- [Samsung email (S3 e versioni successive)](#email-clients-using-exchange-activesync-irm)<br />-Classificazione TITUS per dispositivi mobili <br /><br />- [Web browser](#web-browser-support)       |
|[**Altri tipi di file**](#supported-text-and-image-file-types)    |  App Azure Information Protection (visualizzazione di testo e immagini protetti)  |
| | |


## <a name="ios-rms-enlightened-applications"></a>applicazioni abilitate per iOS RMS

|Type  |Applicazioni supportate   |
|---------|---------|
|**Word, Excel, PowerPoint**    |  -GigaTrust<br />-Office Mobile <br />- [Office per il Web](#viewing-protected-documents-in-office-for-the-web)<br />-TITUS docs<br />- [Web browser](#web-browser-support)    |
|[**Posta elettronica**](#viewing-protected-content-in-email-clients)     |   -Azure Information Protection app (visualizzazione di messaggi di posta elettronica protetti)<br />-Lavoro BlackBerry<br />-Citrix WorxMail <br />- [NitroDesk](#email-clients-using-exchange-activesync-irm)<br />- [Outlook per iPad e iPhone](#email-clients-using-exchange-activesync-irm)<br />-TITUS mail <br />- [Web browser](#web-browser-support)     |
|[**Altri tipi di file**](#supported-text-and-image-file-types)     | -Azure Information Protection app (visualizzazione della protezione di testo e immagini)<br />-Tito docs: **Pfile**  |
| | |

## <a name="windows-10-mobile-rms-enlightened-applications"></a>Applicazioni abilitate per Windows 10 Mobile RMS

|Type  |Applicazioni supportate   |
|---------|---------|
|**Word, Excel, PowerPoint**    | -App Office per dispositivi mobili (visualizzazione di documenti protetti con Azure RMS) <br />- [Web browser](#web-browser-support)    |
|[**Posta elettronica**](#viewing-protected-content-in-email-clients)    |  -Citrix WorxMail <br />-Posta di Outlook (visualizzazione di messaggi di posta elettronica protetti) <br />- [Web browser](#web-browser-support)     |
|[**Altri tipi di file**](#supported-text-and-image-file-types)    | Non supportate   |
| | |

## <a name="blackberry-10-rms-enlightened-applications"></a>Applicazioni abilitate per RMS BlackBerry 10

|Type  |Applicazioni supportate   |
|---------|---------|
|**Word, Excel, PowerPoint**    | - [Web browser](#web-browser-support)    |
|[**Posta elettronica**](#viewing-protected-content-in-email-clients)   | - [Posta elettronica BlackBerry](#email-clients-using-exchange-activesync-irm) <br />- [Web browser](#web-browser-support)      |
|[**Altri tipi di file**](#supported-text-and-image-file-types)    | Non supportate   |
| | |


## <a name="additional-details-about-rms-enlightened-applications"></a>Altre informazioni sulle applicazioni abilitate per RMS

Per ulteriori informazioni sulle tabelle riportate nelle applicazioni abilitate per RMS elencate in precedenza, vedere:

- [Visualizzazione di contenuto protetto nei client di posta elettronica](#viewing-protected-content-in-email-clients)
- [Tipi di file di testo e di immagine supportati](#supported-text-and-image-file-types)
- [Supporto delle app di Office 365](#office-365-app-support)
- [Visualizzazione di documenti protetti in Office per il Web](#viewing-protected-documents-in-office-for-the-web)
- [Supporto Web browser](#web-browser-support)
- [Messaggi di posta elettronica client con Information Rights Management di Exchange ActiveSync (IRM)](#email-clients-using-exchange-activesync-irm)

### <a name="viewing-protected-content-in-email-clients"></a>Visualizzazione di contenuto protetto nei client di posta elettronica

Quando un client di posta elettronica protegge un messaggio, i file di Office allegati al messaggio e attualmente non protetti vengono protetti insieme al messaggio di posta elettronica. In questi casi, il messaggio di posta elettronica e gli allegati possono essere visualizzati nel client di posta elettronica solo da destinatari autorizzati.

Tuttavia, se solo l'allegato è protetto, ma non il messaggio di posta elettronica, l'allegato non può essere visualizzato in anteprima dal client di posta elettronica, neanche dai destinatari autorizzati.

> [!TIP]
> Per i client di posta elettronica che non supportano la protezione della posta elettronica, valutare la possibilità di usare [regole del flusso di posta elettronica di Exchange Online per applicare questa protezione](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8).

### <a name="supported-text-and-image-file-types"></a>Tipi di file di testo e di immagine supportati

I tipi di file diversi dai file di Office e i messaggi di posta elettronica includono tipi di file di testo e di immagine, con estensioni quali **txt,** **XML** , **jpg** e **JPEG.** 

Questi file modificano l'estensione del nome file dopo che sono protetti in modo nativo da Rights Management e quindi diventano di sola lettura. 

I file che non possono essere protetti in modo nativo hanno un'estensione del nome di file **. Pfile** dopo essere stati protetti in modo generico da Rights Management.

Per ulteriori informazioni, vedere [tipi di file supportati](./rms-client/client-admin-guide-file-types.md).

### <a name="office-365-app-support"></a>Supporto delle app di Office 365

Include: 
- App di Office versione minima 1805, Build 9330,2078 da Office 365 business o Microsoft 365 Business. Supportato solo quando all'utente viene assegnata una licenza per Azure Rights Management (noto anche come Azure Information Protection per Office 365).
- App Office 365 ProPlus.

### <a name="viewing-protected-documents-in-office-for-the-web"></a>Visualizzazione di documenti protetti in Office per il Web

Supportato solo con Microsoft SharePoint e OneDrive e i documenti non sono protetti prima di essere caricati in una libreria protetta.

### <a name="web-browser-support"></a>Supporto Web browser

- I Web browser sono supportati per i file di **Word, Excel e PowerPoint** , quando gli [allegati di Office](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM) sono protetti usando [la crittografia dei messaggi di Office 365 con le nuove funzionalità](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801).

- Per i **messaggi di posta elettronica,** i Web browser sono supportati solo negli scenari seguenti:

    - Se il mittente e il destinatario fanno parte della stessa organizzazione
    - Se il mittente o il destinatario usa Exchange Online
    - Se il mittente usa Exchange locale in una configurazione ibrida 

### <a name="email-clients-using-exchange-activesync-irm"></a>Client di posta elettronica con Exchange ActiveSync IRM

I client di posta elettronica seguenti usano Exchange ActiveSync IRM, che deve essere abilitato dall'amministratore di Exchange:

- Windows Mail
- 9Folders
- GigaTrust App for Android
- NitroDesk
- Outlook per Android
- Samsung Email (S3 e versioni successive)
- Office per iPad e iPhone
- Posta elettronica BlackBerry

Gli utenti possono visualizzare, rispondere e rispondere a tutti i messaggi di posta elettronica protetti, ma non possono proteggere i nuovi messaggi di posta elettronica.
 
Se l'applicazione di posta elettronica non riesce a eseguire il rendering del messaggio perché Exchange ActiveSync IRM non è abilitato, il destinatario può visualizzare il messaggio in un Web browser se il mittente usa Exchange Online o Exchange locale in una configurazione ibrida. 

## <a name="azure-rms-support-for-office"></a>Supporto Azure RMS per Office

Azure RMS si integra perfettamente nelle applicazioni Word, Excel, PowerPoint e Outlook, dove questa funzionalità viene spesso denominata Information Rights Management (IRM). 

- [Computer Windows per Information Rights Management (IRM)](#windows-computers-for-information-rights-management-irm)
- [Computer Mac per Information Rights Management (IRM)](#mac-computers-for-information-rights-management-irm)

Vedere anche: [Descrizione del servizio per le applicazioni di Office](https://technet.microsoft.com/library/office-applications-service-description.aspx)

### <a name="windows-computers-for-information-rights-management-irm"></a>Computer Windows per Information Rights Management (IRM)

Le famiglie di prodotti client di Office seguenti supportano la protezione dei file e dei messaggi di posta elettronica nei computer Windows tramite il servizio Azure Rights Management:

- **App di Office versione minima 1805, build 9330,2078 da office 365 business o Microsoft 365 business** quando all'utente viene assegnata una licenza per Azure Rights Management (noto anche come Azure Information Protection per Office 365)

- **Office 365 ProPlus**

    Queste edizioni di Office sono incluse nella maggior parte, ma non in tutte le sottoscrizione di Office 365 che includono la protezione dati di Azure Information Protection. Controllare le informazioni sulla sottoscrizione per verificare se Office 365 ProPlus è incluso. Queste informazioni si possono trovare anche nel [foglio dati di Azure Information Protection](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

- **Office Professional Plus 2019**

- **Office Professional Plus 2016**

- **Office Professional Plus 2013**

- **Office Professional Plus 2010 con Service Pack 2**

Tutte le edizioni di Office, ad eccezione di Office 2007, possono utilizzare il contenuto protetto.

#### <a name="azure-rights-management-service-with-office-professional-plus-2010-and-service-pack-2-or-office-professional-2010-with-service-pack-2"></a>Servizio Rights Management di Azure con Office Professional Plus 2010 e Service Pack 2 o Office Professional 2010 con Service Pack 2

Quando si usa il servizio Rights Management di Azure con Office Professional Plus 2010 e Service Pack 2 o Office Professional 2010 con Service Pack 2, è necessario avere anche il client AIP per Windows.

Questa configurazione è inoltre:

- Non è supportato in Windows 10.
- Non supporta l'autenticazione basata su moduli per gli account utente federati. Questi account devono usare l'autenticazione integrata di Windows.
- Non supporta la possibilità di eseguire l'override della protezione dei modelli usando le autorizzazioni personalizzate selezionate con il client AIP. In questo scenario, prima di applicare autorizzazioni personalizzate è necessario rimuovere la protezione originaria.

### <a name="mac-computers-for-information-rights-management-irm"></a>Computer Mac per Information Rights Management (IRM)

Le famiglie di prodotti client di Office seguenti supportano la protezione dei file e dei messaggi di posta elettronica in macOS tramite Azure RMS:

- Office 365 ProPlus
- Office Standard 2019 per Mac
- Office Standard 2016 per Mac

Tutte le edizioni di Office per Mac 2019 e Office for Mac 2016 supportano l'utilizzo di contenuto protetto.

> [!TIP]
> Per iniziare a proteggere i documenti usando Office per Mac, è possibile trovare le domande frequenti seguenti: [ricerca per categorie configurare un computer Mac per proteggere e tenere traccia dei documenti?](faqs-rms.md#how-do-i-configure-a-mac-computer-to-protect-and-track-documents)
> 
## <a name="azure-information-protection-apps-for-ios-and-android"></a>App Azure Information Protection per iOS e Android

L'app Azure Information Protection per iOS e Android fornisce un visualizzatore per i messaggi di posta elettronica protetti da diritti (file con **estensione rpmsg** ) quando questi dispositivi mobili non dispongono di un'app di posta elettronica in grado di aprire messaggi di posta elettronica protetti. Questa app consente anche di aprire file PDF, file di testo e di immagini protetti con RMS.

Se i dispositivi iOS e Android sono registrati da Microsoft Intune, gli utenti possono installare l'app dal portale aziendale e si può gestire l'app con i [criteri di protezione delle app](/intune/app-protection-policies) di Intune.

Per altre informazioni su come usare l'app, vedere [Domande frequenti sull'app Azure Information Protection per iOS e Android](./rms-client/mobile-app-faq.md).

## <a name="the-azure-information-protection-client-for-windows"></a>Client di Azure Information Protection per Windows

Il client Azure Information Protection (AIP) include due versioni, con guide dell'amministratore e dell'utente per ogni versione:

- **Client di etichetta unificata**:
    - [Guida dell'amministratore](./rms-client/clientv2-admin-guide.md)
    - [Manuale dell'utente](./rms-client/clientv2-user-guide.md)

- **Client classico**:
    - [Guida dell'amministratore](./rms-client/client-admin-guide.md)
    - [Manuale dell'utente](./rms-client/client-user-guide.md)

Scaricare l'app pertinente dalla [pagina Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970).

> [!NOTE]
> Non si è certi delle differenze tra queste due versioni? Vedere le [domande frequenti](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)pertinenti.
> 
## <a name="rights-management-sharing-app"></a>Applicazione di condivisione Rights Management

Per i computer Mac, l'app di condivisione Rights Management offre un visualizzatore per i file PDF protetti **(con estensione Ppdf),** le immagini di testo protette e i file protetti in modo generico. Consente anche di proteggere i file di immagine, ma non altri file. Per proteggere i file di Office in questi computer, usare Office per Mac oppure Office 365 ProPlus. 

Per ulteriori informazioni, vedere le [domande frequenti sull'applicazione Microsoft Rights Management sharing per piattaforme mobili](https://technet.microsoft.com/dn451248)

Scaricare l'app Rights Management sharing per computer Mac dalla [pagina Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970).

## <a name="other-applications-that-support-azure-information-protection"></a>Altre applicazioni che supportano Azure Information Protection

Oltre alle applicazioni elencate in precedenza, tutte le applicazioni che supportano le API per il servizio Azure Rights Management possono essere integrate con Azure Information Protection. 

Esempi possono includere applicazioni line-of-business scritte internamente o applicazioni di fornitori di software, scritte usando gli SDK di RSM.

Per altre informazioni, vedere la [Guida per gli sviluppatori di Azure Information Protection](./develop/developers-guide.md).

## <a name="applications-that-are-not-supported-by-azure-rms"></a>Applicazioni non supportate da Azure RMS

Le applicazioni attualmente supportate da Azure RMS includono:

- Microsoft OneDrive per SharePoint Server 2013
- XPS Viewer
- Applicazioni in esecuzione in versioni di Windows precedenti a Windows 7, Service Pack 1


## <a name="next-steps"></a>Passaggi successivi

Vedere anche la pagina relativa alla

- [Requisiti per Azure Information Protection](requirements.md).
- [Supporto del servizio Rights Management di Azure da parte delle applicazioni](./applications-support.md).
- [Configurazione di applicazioni per Azure Rights Management](configure-applications.md).

Per le informazioni più aggiornate sulle soluzioni che supportano il servizio Azure Rights Management e Azure Information Protection, vedere il post di Blog [Microsoft ignite 2019 – microsoft Information Protection Solutions Partner Ecosystem Showcase](https://techcommunity.microsoft.com/t5/Microsoft-Information-Protection/Microsoft-Ignite-2019-Microsoft-Information-Protection-solutions/ba-p/967024).
