---
title: Supporto dei server locali per la protezione dati | Azure Information Protection
description: Identificare i prodotti server locali che possono usare il servizio Azure Rights Management di Azure Information Protection tramite il connettore di Rights Management.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e7d91f2d-d6a7-4c7e-821f-c94e4be9967d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: e4bf159cea6298e5a5577a2fa4de3dd3beeb47d9


---


# <a name="onpremises-servers-that-support-azure-rights-management-data-protection"></a>Server locali che supportano la protezione dati di Azure Rights Management

>*Si applica a: Azure Information Protection, Office 365*

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

-   **File server che eseguono Windows Server e usano la funzionalità Infrastruttura di classificazione file (FCI, File Classification Infrastructure)**:

    -   Windows Server 2012 R2

    -   Windows Server 2012

    > [!NOTE]
    > Poiché i file server che eseguono Windows Server 2008 R2 non includono un'azione predefinita per le attività di gestione file per l'applicazione della protezione Rights Management, non sarà possibile usare il connettore di Rights Management per questo scenario. È tuttavia possibile usare Infrastruttura di classificazione file e Azure RMS in questi sistemi operativi se si configura un'attività personalizzata di gestione file per l'esecuzione di un file eseguibile o di uno script in grado di proteggere i file tramite Azure RMS. Ad esempio, uno script di Windows PowerShell che usa i [cmdlet di protezione RMS](https://msdn.microsoft.com/library/azure/mt433195.aspx).
    > 
    > È inoltre possibile utilizzare questi cmdlet con server che eseguono versioni successive di Windows Server, con il vantaggio che questi cmdlet possono proteggere tutti i tipi di file. Il connettore RMS protegge solo i file di Office. Per le istruzioni d'uso, vedere [Protezione RMS con l'infrastruttura di classificazione file (FCI, File Classification Infrastructure) per Windows Server&#40;FCI&#41;](../rms-client/configure-fci.md).

Il connettore di Rights Management è supportato in Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2.

Per altre informazioni sulla modalità di configurazione del connettore di Rights Management per questi server locali, vedere [Distribuzione del connettore di Azure Rights Management](../deploy-use/deploy-rms-connector.md).

## <a name="next-steps"></a>Passaggi successivi
Per verificare gli altri requisiti, vedere [Requisiti per Azure Rights Management](requirements-azure-rms.md).



<!--HONumber=Nov16_HO2-->


