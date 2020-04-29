---
title: Supporto di Azure Rights Management da parte delle app da AIP
description: Informazioni sul modo in cui le applicazioni usate più di frequente, ad esempio le app di Office, e i servizi (ad esempio Exchange e SharePoint) possono usare il servizio Rights Management di Azure Azure Information Protection per proteggere i documenti e i messaggi di posta elettronica dell'organizzazione.
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 04/28/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 2cdc7bde-4044-4021-b887-11476f99afd9
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 9e14cd34dd31dda6942c028fa9a68778eaaaed3a
ms.sourcegitcommit: 479b3aaea7011750ff85a217298e5ae9185c1dd1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2020
ms.locfileid: "82224581"
---
# <a name="how-applications-support-the-azure-rights-management-service"></a>Supporto del servizio Azure Rights Management da parte delle applicazioni

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Usare le informazioni seguenti per comprendere in che modo le applicazioni e i servizi dell'utente finale usati più di frequente possono usare il servizio Azure Rights Management da Azure Information Protection per proteggere i documenti e i messaggi di posta elettronica dell'organizzazione. Tali applicazioni includono Word, Excel, PowerPoint e Outlook. I servizi includono Exchange e SharePoint.

> [!NOTE]
> Per verificare le applicazioni e le versioni supportate dal servizio Azure Rights Management, vedere [Requisiti per Azure RMS: applicazioni](./requirements-applications.md).

In alcuni casi, il servizio Azure Rights Management applica automaticamente la protezione, in base ai criteri configurati dagli amministratori, ad esempio nel caso di raccolte di SharePoint e regole di trasporto di Exchange. In altri casi, gli utenti finali stessi devono applicare la protezione dalle rispettive applicazioni. Ad esempio, gli utenti selezionano un'etichetta di classificazione configurata per applicare la protezione oppure selezionano un modello o opzioni specifiche. Un caso tipico di protezione applicata dagli utenti si verifica quando gli utenti proteggono un file da condividere limitandone anche l'accesso o l'uso a utenti selezionati oppure a utenti esterni all'organizzazione.

I modelli semplificano agli utenti e agli amministratori che configurano i criteri l'applicazione del livello corretto di protezione e la limitazione dell'accesso a persone all'interno dell'organizzazione. Anche se nel servizio Azure Rights Management sono disponibili due modelli predefiniti, sarà possibile creare modelli personalizzati per ridurre i tempi qualora sia necessario specificare opzioni singole. Per altre informazioni sui modelli, vedere [Configurazione e gestione dei modelli per Azure Information Protection](configure-policy-templates.md).

Nei casi in cui gli utenti debbano applicare in modo autonomo la protezione, assicurarsi di fornire loro istruzioni e linee guida sulle modalità e sul momento in cui eseguire l'operazione. Verificare le istruzioni specifiche per l'applicazione, le versioni usate e come usarle. Fornire anche indicazioni su come e quando gli utenti devono applicare la protezione appropriata per l'azienda. Per altre informazioni, vedere [Consentire agli utenti di proteggere i file tramite Azure Rights Management](help-users.md).

Per altre informazioni sulle modalità di configurazione di queste applicazioni per il servizio Azure Rights Management di Azure Information Protection, vedere [Configurazione di applicazioni per Azure Rights Management](configure-applications.md).

I servizi di ricerca si integrano con Rights Management in modi diversi. Ad esempio: 

- Exchange Online ed Exchange Server usano l'indicizzazione del lato del servizio per visualizzare automaticamente i messaggi di posta elettronica protetti dell'utente nei risultati delle ricerche. 

- SharePoint Online e SharePoint Server applicano la protezione di Rights Management ai file solo durante il download. Questa implementazione significa che i risultati di indicizzazione e ricerca in SharePoint non sono interessati da questa soluzione di protezione del documento. Tuttavia, se si vuole archiviare un documento in SharePoint senza restituirlo nei risultati di ricerca, proteggerlo tramite RMS prima di caricarlo in SharePoint.

- Poiché Windows Desktop Search usa un indice condiviso tra i diversi utenti del dispositivo, per garantire la sicurezza dei dati dei documenti protetti non esegue l'indicizzazione dei file protetti. Ciò significa che anche se i risultati della ricerca non includono i file protetti, è possibile assicurarsi che i file che contengono dati sensibili non vengano visualizzati nei risultati della ricerca per altri utenti che possono accedere al PC o connettersi al PC. 

## <a name="next-steps"></a>Passaggi successivi

Altre informazioni sul supporto del servizio Azure Rights Management da parte delle applicazioni e dei servizi seguenti:

-   [Applicazioni e servizi Office](office-apps-services-support.md)

-   [File server che eseguono Windows Server e usano la funzionalità Infrastruttura di classificazione file](file-server-support.md)

-   [Altre applicazioni che supportano le API RMS](api-support.md)

