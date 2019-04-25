---
title: Eseguire la migrazione da una chiave protetta tramite software a un'altra - AIP
description: Istruzioni che fanno parte del percorso di migrazione da AD RMS ad Azure Information Protection e si applicano solo se la chiave di AD RMS è protetta tramite software e si vuole eseguire la migrazione ad Azure Information Protection con una chiave del tenant protetta tramite software.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 12/11/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 81a5cf4f-c1f3-44a9-ad42-66e95f33ed27
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ee5ee97c6ff7a1bc3f817fa5ce6a086e7e691dd4
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "60184145"
---
# <a name="step-2-software-protected-key-to-software-protected-key-migration"></a>Passaggio 2: Migrazione da una chiave protetta tramite software a un'altra

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Queste istruzioni fanno parte del [percorso di migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md) e si applicano solo se la chiave di AD RMS è protetta tramite software e si vuole eseguire la migrazione ad Azure Information Protection con una chiave del tenant protetta tramite software. 

Se non si tratta dello scenario di configurazione scelto, tornare al [Passaggio 4. Esportare i dati di configurazione da AD RMS e importarli in Azure RMS](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection), quindi scegliere una configurazione diversa.

Usare la procedura seguente per importare la configurazione di AD RMS in Azure Information Protection. La chiave del tenant di Azure Information Protection verrà gestita da Microsoft.

## <a name="to-import-the-configuration-data-to-azure-information-protection"></a>Per importare i dati di configurazione in Azure Information Protection

1. In una workstation connessa a Internet, usare il cmdlet [Connect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice) per connettersi al servizio Azure Rights Management:

    ```
    Connect-AadrmService
    ```
    Quando viene richiesto, immettere le credenziali di amministratore del tenant Azure Rights Management. In genere, viene usato un account amministratore globale per Azure Active Directory o Office 365.

2. Usare il cmdlet [Import-AadrmTpd](/powershell/aadrm/vlatest/import-aadrmtpd) per caricare ogni file di dominio di pubblicazione trusted esportato (con estensione xml). Ad esempio, è necessario avere almeno un file aggiuntivo da importare in caso di aggiornamento del cluster AD RMS per la modalità di crittografia 2. 
    
    Per eseguire questo cmdlet, sarà necessaria la password specificata in precedenza per ogni file di dati di configurazione. 
    
    Ad esempio, eseguire prima di tutto il comando seguente per archiviare la password:
    
        $TPD_Password = Read-Host -AsSecureString
    
    Immettere la password specificata per esportare il primo file di dati di configurazione. Usando E:\contosokey1.xml come esempio per il file di configurazione, eseguire quindi il comando seguente e confermare che si vuole eseguire questa azione:
    ```
    Import-AadrmTpd -TpdFile E:\contosokey1.xml -ProtectionPassword $TPD_Password -Verbose
    ```
    
3. Dopo aver caricato ogni file, eseguire [Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties) per identificare la chiave importata corrispondente alla chiave del certificato concessore di licenze server attualmente attiva in AD RMS. Questa chiave diventerà la chiave del tenant attiva per il servizio Azure Rights Management.

4.  Usare il cmdlet [Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice) per disconnettersi dal servizio Azure Rights Management:

    ```
    Disconnect-AadrmService
    ```

È ora possibile andare al [Passaggio 5. Attivare il servizio Azure Rights Management](migrate-from-ad-rms-phase2.md#step-5-activate-the-azure-rights-management-service).


