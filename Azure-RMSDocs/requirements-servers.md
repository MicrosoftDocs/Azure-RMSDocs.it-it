---
title: Supporto dei server per la protezione dati di Azure RMS - AIP
description: Identificare i prodotti server locali che possono usare il servizio Azure Rights Management di Azure Information Protection tramite il connettore di Rights Management.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/30/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: e7d91f2d-d6a7-4c7e-821f-c94e4be9967d
ms.subservice: prereqs
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 1cff4a483d8e8d8e14dc6c8159d70655b7b71009
ms.sourcegitcommit: 319c0691509748e04aecf839adaeb3b5cac2d2cf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/30/2019
ms.locfileid: "71684483"
---
# <a name="on-premises-servers-that-support-azure-rights-management-data-protection"></a>Server locali che supportano la protezione dati di Azure Rights Management

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

I prodotti server locali seguenti sono supportati con Azure Information Protection quando si usa il connettore di Azure Rights Management. Il connettore funziona come interfaccia di comunicazione (inoltro) tra i server locali e il servizio Azure Rights Management che è usato da Azure Information Protection per proteggere messaggi di posta elettronica e documenti di Office. 

Per usare questo connettore, è necessario configurare la sincronizzazione delle directory tra le foreste Active Directory e Azure Active Directory.

-   **Exchange Server**:

    -   Exchange Server 2016

    -   Exchange Server 2013

    -   Exchange Server 2010

-   **Office SharePoint Server**:

    -   Office SharePoint Server 2016

    -   Office SharePoint Server 2013

    -   Office SharePoint Server 2010

-   **File server che eseguono Windows Server e usano la funzionalità Infrastruttura di classificazione file (FCI, File Classification Infrastructure)** :

    -   Windows Server 2016

    -   Windows Server 2012 R2

    -   Windows Server 2012

    > [!NOTE]
    > Poiché i file server che eseguono Windows Server 2008 R2 non includono un'azione predefinita per le attività di gestione file per l'applicazione della protezione Rights Management, non sarà possibile usare il connettore di Rights Management per questo scenario. È tuttavia possibile usare Infrastruttura di classificazione file e Azure RMS in questi sistemi operativi se si configura un'attività personalizzata di gestione file per l'esecuzione di un file eseguibile o di uno script in grado di proteggere i file tramite Azure RMS. Ad esempio, uno script di Windows PowerShell che usa i [cmdlet di AzureInformationProtection](/powershell/azureinformationprotection/vlatest/aip).
    > 
    > È inoltre possibile utilizzare questi cmdlet con server che eseguono versioni successive di Windows Server, con il vantaggio che questi cmdlet possono proteggere tutti i tipi di file. Il connettore RMS protegge solo i file di Office. Per le istruzioni d'uso, vedere [Protezione RMS con l'infrastruttura di classificazione file (FCI, File Classification Infrastructure) per Windows Server&#40;FCI&#41;](./rms-client/configure-fci.md).

Il connettore Rights Management è supportato in Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2.

Per altre informazioni sulla modalità di configurazione del connettore di Rights Management per questi server locali, vedere [Distribuzione del connettore di Azure Rights Management](deploy-rms-connector.md).

## <a name="next-steps"></a>Passaggi successivi
Per verificare gli altri requisiti, vedere [Requisiti per Azure Information Protection](requirements.md).
