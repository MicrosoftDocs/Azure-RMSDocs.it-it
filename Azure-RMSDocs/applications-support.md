---
title: Supporto di Azure Rights Management da parte delle app da AIP
description: Informazioni su come le applicazioni (ad esempio, le applicazioni di Office come Word, Excel, PowerPoint e Outlook) e i servizi (ad esempio, Exchange e SharePoint) più comunemente usati dagli utenti sfruttano il servizio Azure Rights Management di Azure Information Protection per proteggere i documenti e i messaggi di posta elettronica dell'organizzazione.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 2cdc7bde-4044-4021-b887-11476f99afd9
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: f529b761ef757612b621e948a49805448f9414ba
ms.sourcegitcommit: 949bf02d5d12bef8e26d89ad5d6a0d5cc7826135
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/02/2018
ms.locfileid: "39474668"
---
# <a name="how-applications-support-the-azure-rights-management-service"></a>Supporto del servizio Azure Rights Management da parte delle applicazioni

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Usare le informazioni seguenti per comprendere come le applicazioni e i servizi più comunemente usati dagli utenti sfruttano il servizio Azure Rights Management di Azure Information Protection per proteggere i documenti e i messaggi di posta elettronica dell'organizzazione. Tali applicazioni includono Word, Excel, PowerPoint e Outlook. I servizi includono Exchange e SharePoint.

> [!NOTE]
> Per verificare le applicazioni e le versioni supportate dal servizio Azure Rights Management, vedere [Requisiti per Azure RMS: applicazioni](./requirements-applications.md).

In alcuni casi, il servizio Azure Rights Management applica automaticamente la protezione, in base ai criteri configurati dagli amministratori, ad esempio nel caso di raccolte di SharePoint e regole di trasporto di Exchange. In altri casi, gli utenti finali stessi devono applicare la protezione dalle rispettive applicazioni. Ad esempio, gli utenti selezionano un'etichetta di classificazione configurata per applicare la protezione oppure selezionano un modello o opzioni specifiche. Un caso tipico di protezione applicata dagli utenti si verifica quando gli utenti proteggono un file da condividere limitandone anche l'accesso o l'uso a utenti selezionati oppure a utenti esterni all'organizzazione.

I modelli semplificano agli utenti e agli amministratori che configurano i criteri l'applicazione del livello corretto di protezione e la limitazione dell'accesso a persone all'interno dell'organizzazione. Anche se nel servizio Azure Rights Management sono disponibili due modelli predefiniti, sarà possibile creare modelli personalizzati per ridurre i tempi qualora sia necessario specificare opzioni singole. Per altre informazioni sui modelli, vedere [Configurazione e gestione dei modelli per Azure Information Protection](./deploy-use/configure-policy-templates.md).

Nei casi in cui gli utenti debbano applicare in modo autonomo la protezione, assicurarsi di fornire loro istruzioni e linee guida sulle modalità e sul momento in cui eseguire l'operazione. Verificare le istruzioni specifiche per l'applicazione, le versioni usate e come usarle. Fornire anche indicazioni su come e quando gli utenti devono applicare la protezione appropriata per l'azienda. Per altre informazioni, vedere [Consentire agli utenti di proteggere i file tramite Azure Rights Management](./deploy-use/help-users.md).

Per altre informazioni sulle modalità di configurazione di queste applicazioni per il servizio Azure Rights Management di Azure Information Protection, vedere [Configurazione di applicazioni per Azure Rights Management](./deploy-use/configure-applications.md).

I servizi di ricerca si integrano con Rights Management in modi diversi. Ad esempio: 

- Exchange Online ed Exchange Server usano l'indicizzazione del lato del servizio per visualizzare automaticamente i messaggi di posta elettronica protetti dell'utente nei risultati delle ricerche. 

- SharePoint Online e SharePoint Server applicano la protezione di Rights Management ai file solo durante il download. Questa implementazione significa che i risultati di indicizzazione e ricerca in SharePoint non sono interessati da questa soluzione di protezione del documento. Tuttavia, se si vuole archiviare un documento in SharePoint senza restituirlo nei risultati di ricerca, proteggerlo tramite RMS prima di caricarlo in SharePoint.

- Poiché Windows Desktop Search usa un indice condiviso tra i diversi utenti del dispositivo, per garantire la sicurezza dei dati dei documenti protetti non esegue l'indicizzazione dei file protetti. Ciò significa che anche se i risultati di ricerca non includono i file che sono stati protetti, sia ha la garanzia che i file contenenti dati sensibili non vengono visualizzati nei risultati di ricerca di altri utenti che possono accedere o connettersi al PC. 

## <a name="next-steps"></a>Passaggi successivi

Altre informazioni sul supporto del servizio Azure Rights Management da parte delle applicazioni e dei servizi seguenti:

-   [Applicazione RMS sharing per piattaforme Windows e mobili](sharing-app-support.md)

-   [Applicazioni e servizi Office](office-apps-services-support.md)

-   [File server che eseguono Windows Server e usano l'infrastruttura di classificazione file](file-server-support.md)

-   [Altre applicazioni che supportano le API RMS](api-support.md)
