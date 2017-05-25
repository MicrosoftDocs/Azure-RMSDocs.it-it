---
title: Supporto di Azure Rights Management da parte delle app - AIP
description: "Informazioni su come le applicazioni (ad esempio, le applicazioni di Office come Word, Excel, PowerPoint e Outlook) e i servizi (ad esempio, Exchange e SharePoint) più comunemente usati dagli utenti sfruttano il servizio Azure Rights Management di Azure Information Protection per proteggere i documenti e i messaggi di posta elettronica dell&quot;organizzazione."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/26/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 2cdc7bde-4044-4021-b887-11476f99afd9
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: db9f67c5baeea678bf288f4f10237ff4517d905b
ms.sourcegitcommit: 3ff6c072a228994308402778c493727cc682c6b7
ms.translationtype: HT
ms.contentlocale: it-IT
---
# <a name="how-applications-support-the-azure-rights-management-service"></a>Supporto del servizio Azure Rights Management da parte delle applicazioni

>*Si applica a: Azure Information Protection, Office 365*

Usare le informazioni seguenti per comprendere come le applicazioni (ad esempio le applicazioni di Office come Word, Excel, PowerPoint e Outlook) e i servizi (ad esempio, Exchange e SharePoint) più comunemente usati dagli utenti sfruttano il servizio Azure Rights Management di Azure Information Protection per proteggere i documenti e i messaggi di posta elettronica dell'organizzazione. 
> [!NOTE]
> Per verificare le applicazioni e le versioni supportate dal servizio Azure Rights Management, vedere [Requisiti per Azure RMS: applicazioni](../get-started/requirements-applications.md).

In alcuni casi, il servizio Azure Rights Management applica automaticamente la protezione, in base ai criteri configurati dagli amministratori, ad esempio nel caso di raccolte di SharePoint e regole di trasporto di Exchange. In altri casi, gli utenti finali devono applicare in modo autonomo la protezione delle informazioni dalle loro applicazioni, ad esempio selezionando un'etichetta di classificazione configurata per applicare un modello, selezionando direttamente un modello o selezionando opzioni specifiche. Un caso tipico di protezione applicata dagli utenti si verifica quando gli utenti proteggono un file da condividere limitandone l'accesso o l'uso a utenti selezionati oppure a utenti esterni all'organizzazione.

I modelli semplificano agli utenti e agli amministratori che configurano i criteri l'applicazione del livello corretto di protezione e la limitazione dell'accesso a persone all'interno dell'organizzazione. Anche se nel servizio Azure Rights Management sono disponibili due modelli predefiniti, sarà possibile creare modelli personalizzati per ridurre i tempi qualora sia necessario specificare opzioni singole. Per altre informazioni, vedere [Configurazione di modelli personalizzati per il servizio Azure Rights Management](../deploy-use/configure-custom-templates.md).

Nei casi in cui gli utenti debbano applicare in modo autonomo la protezione delle informazioni, assicurarsi di fornire loro istruzioni e linee guida sulle modalità e sul momento in cui eseguire l'operazione. Le istruzioni devono essere specifiche per l'applicazione e le versioni usate e per le modalità di uso, mentre le linee guida relative al momento e alle modalità di applicazione della protezione delle informazioni devono essere appropriate per l'azienda. Per altre informazioni, vedere [Consentire agli utenti di proteggere i file tramite Azure Rights Management](../deploy-use/help-users.md).

Per altre informazioni sulle modalità di configurazione di queste applicazioni per il servizio Azure Rights Management di Azure Information Protection, vedere [Configurazione di applicazioni per Azure Rights Management](../deploy-use/configure-applications.md).

I servizi di ricerca si integrano con Rights Management in modi diversi. Ad esempio: 

- Exchange Online ed Exchange Server usano l'indicizzazione del lato del servizio per visualizzare automaticamente i messaggi di posta elettronica protetti tramite RMS dell'utente nei risultati delle ricerche. 

- SharePoint Online e SharePoint Server applicano la protezione Rights Management ai file solo durante il download. Ciò significa che questa soluzione di protezione dei documenti non ha alcun effetto sull'indicizzazione e sui risultati di ricerca in SharePoint. Tuttavia, se si vuole archiviare un documento in SharePoint senza restituirlo nei risultati di ricerca, proteggere il file tramite RMS prima di caricarlo in SharePoint.

- Poiché Windows Desktop Search usa un indice condiviso tra i diversi utenti del dispositivo, per garantire la sicurezza dei dati dei documenti protetti non esegue l'indicizzazione dei file protetti da RMS. Ciò significa che anche se i risultati di ricerca non includono i file che sono stati protetti, sia ha la garanzia che i file contenenti dati sensibili non vengono visualizzati nei risultati di ricerca di altri utenti che possono accedere o connettersi al PC. 



## <a name="next-steps"></a>Passaggi successivi

Altre informazioni sul supporto del servizio Azure Rights Management da parte delle applicazioni seguenti:

-   [Applicazione RMS sharing per piattaforme Windows e mobili](sharing-app-support.md)

-   [Applicazioni e servizi Office](office-apps-services-support.md)

-   [File server che eseguono Windows Server e usano l'infrastruttura di classificazione file](file-server-support.md)

-   [Altre applicazioni che supportano le API RMS](api-support.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
