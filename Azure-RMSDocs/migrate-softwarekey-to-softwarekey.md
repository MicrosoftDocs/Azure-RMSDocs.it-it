---
title: Eseguire la migrazione da una chiave protetta tramite software a un'altra - AIP
description: Istruzioni che fanno parte del percorso di migrazione da AD RMS ad Azure Information Protection e si applicano solo se la chiave di AD RMS è protetta tramite software e si vuole eseguire la migrazione ad Azure Information Protection con una chiave del tenant protetta tramite software.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 81a5cf4f-c1f3-44a9-ad42-66e95f33ed27
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 6b96c9d12277ec85ca1a726907eb5d8c6ca7c391
ms.sourcegitcommit: c20c7f114ae58ed6966785d8772d0bf1c1d39cce
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/08/2019
ms.locfileid: "74935419"
---
# <a name="step-2-software-protected-key-to-software-protected-key-migration"></a>Passaggio 2: Migrazione da una chiave protetta tramite software a un'altra

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Queste istruzioni fanno parte del [percorso di migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md) e si applicano solo se la chiave di AD RMS è protetta tramite software e si vuole eseguire la migrazione ad Azure Information Protection con una chiave del tenant protetta tramite software. 

Se non si tratta dello scenario di configurazione scelto, tornare al [passaggio 4. Esportare i dati di configurazione da AD RMS e importarli in Azure RMS](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection) e scegliere una configurazione diversa.

Usare la procedura seguente per importare la configurazione di AD RMS in Azure Information Protection. La chiave del tenant di Azure Information Protection verrà gestita da Microsoft.

## <a name="to-import-the-configuration-data-to-azure-information-protection"></a>Per importare i dati di configurazione in Azure Information Protection

1. In una workstation connessa a Internet usare il cmdlet [Connect-AipService](/powershell/module/aipservice/connect-aipservice) per connettersi al servizio Rights Management di Azure:

    ```
    Connect-AipService
    ```
    Quando viene richiesto, immettere le credenziali di amministratore del tenant Azure Rights Management. In genere, viene usato un account amministratore globale per Azure Active Directory o Office 365.

2. Usare il cmdlet [Import-AipServiceTpd](/powershell/module/aipservice/import-aipservicetpd) per caricare ogni file di dominio di pubblicazione trusted esportato (con estensione XML). Ad esempio, è necessario avere almeno un file aggiuntivo da importare in caso di aggiornamento del cluster AD RMS per la modalità di crittografia 2. 
    
    Per eseguire questo cmdlet, sarà necessaria la password specificata in precedenza per ogni file di dati di configurazione. 
    
    Ad esempio, eseguire prima di tutto il comando seguente per archiviare la password:
    
        $TPD_Password = Read-Host -AsSecureString
    
    Immettere la password specificata per esportare il primo file di dati di configurazione. Usando E:\contosokey1.xml come esempio per il file di configurazione, eseguire quindi il comando seguente e confermare che si vuole eseguire questa azione:
    ```
    Import-AipServiceTpd -TpdFile E:\contosokey1.xml -ProtectionPassword $TPD_Password -Verbose
    ```
    
3. Dopo aver caricato ogni file, eseguire [set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties) per identificare la chiave importata corrispondente alla chiave SLC attualmente attiva in ad RMS. Questa chiave diventerà la chiave del tenant attiva per il servizio Azure Rights Management.

4.  Usare il cmdlet [Disconnect-AipServiceService](/powershell/module/aipservice/disconnect-aipservice) per disconnettersi dal servizio Rights Management di Azure:

    ```
    Disconnect-AipServiceService
    ```

A questo punto è possibile procedere con il [passaggio 5. Attivare il servizio Rights Management di Azure](migrate-from-ad-rms-phase2.md#step-5-activate-the-azure-rights-management-service).


