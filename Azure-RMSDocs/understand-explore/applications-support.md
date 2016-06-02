---
# required metadata

title: Supporto di Azure Rights Management da parte delle applicazioni | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/13/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 2cdc7bde-4044-4021-b887-11476f99afd9

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Supporto di Microsoft Azure Rights Management da parte delle applicazioni

*Si applica a: Azure Rights Management, Office 365*

Questo articolo contiene informazioni sulla modalità in cui le applicazioni (ad esempio le applicazioni Office quali Word, Excel, PowerPoint e Outlook) e i servizi (ad esempio Exchange e SharePoint) più comunemente usati dagli utenti sfruttano Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] per proteggere i dati dell'organizzazione. 
> [!NOTE] Per verificare le applicazioni e le versioni supportate da [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS), vedere [Requisiti per Azure Rights Management](../get-started/requirements-azure-rms.md).

In alcuni casi, la protezione delle informazioni viene applicata automaticamente in base ai criteri configurati dall'utente, ad esempio nel caso di raccolte SharePoint, file classificati e regole di trasporto di Exchange. In altri casi, gli utenti devono applicare in modo autonomo la protezione delle informazioni selezionando un modello oppure opzioni specifiche, ad esempio nel caso in cui condividono un file tramite e-mail o proteggono un file in locale limitandone l'accesso o l'uso a utenti selezionati oppure a utenti esterni all'organizzazione.

I modelli semplificano agli utenti e agli amministratori che configurano i criteri l'applicazione del livello corretto di protezione e la limitazione dell'accesso a persone all'interno dell'organizzazione. Sebbene in [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] siano disponibili due modelli predefiniti, sarà possibile creare modelli personalizzati per ridurre i tempi qualora sia necessario specificare opzioni singole. Per altre informazioni, vedere [Configurazione di modelli personalizzati per Azure Rights Management](../deploy-use/configure-custom-templates.md).

Nei casi in cui gli utenti debbano applicare in modo autonomo la protezione delle informazioni, assicurarsi di fornire loro istruzioni e linee guida sulle modalità e sul momento in cui eseguire l'operazione. Le istruzioni devono essere specifiche per l'applicazione e le versioni usate e per le modalità di uso, mentre le linee guida relative al momento e alle modalità di applicazione della protezione delle informazioni devono essere appropriate per l'azienda. Per altre informazioni, vedere [Consentire agli utenti di proteggere i file tramite Azure Rights Management](../deploy-use/help-users.md).

Per altre informazioni sulle modalità di configurazione di queste applicazioni per Azure RMS, vedere [Configurazione di applicazioni per Azure Rights Management](../deploy-use/configure-applications.md).

> [!TIP] Per esempi e screenshot delle applicazioni che usano Azure RMS, vedere [Azure RMS in azione: Cosa vedono gli amministratori e gli utenti](what-admins-users-see.md).

I servizi di ricerca si integrano con Rights Management in modi diversi. Ad esempio: 

- Exchange Online ed Exchange Server usano l'indicizzazione del lato del servizio per visualizzare automaticamente i messaggi di posta elettronica protetti tramite RMS dell'utente nei risultati delle ricerche. 

- SharePoint Online e SharePoint Server applicano la protezione RMS ai file solo durante il download. Ciò significa che questa soluzione di protezione dei documenti non ha alcun effetto sull'indicizzazione e i risultati di ricerca in SharePoint. Tuttavia, se si vuole archiviare un documento in SharePoint senza restituirlo nei risultati di ricerca, proteggere il file tramite RMS prima di caricarlo in SharePoint.

- Poiché Windows Desktop Search usa un indice condiviso tra i diversi utenti del dispositivo, per garantire la sicurezza dei dati dei documenti protetti non esegue l'indicizzazione dei file protetti da RMS. Ciò significa che anche se i risultati di ricerca non includono i file che sono stati protetti, sia ha la garanzia che i file contenenti dati sensibili non vengono visualizzati nei risultati di ricerca di altri utenti che possono accedere o connettersi al PC. 



## Passaggi successivi

Altre informazioni sul supporto di Azure RMS da parte delle applicazioni seguenti:

-   [Applicazione RMS sharing per piattaforme Windows e mobili](sharing-app-support.md)

-   [Applicazioni e servizi Office](office-apps-services-support.md)

-   [File server che eseguono Windows Server e usano l'infrastruttura di classificazione file](file-server-support.md)

-   [Altre applicazioni che supportano le API RMS](api-support.md)



<!--HONumber=May16_HO3-->


