---
title: Eseguire la migrazione da una chiave protetta tramite software a un'altra - AIP
description: Istruzioni che fanno parte del percorso di migrazione da AD RMS ad Azure Information Protection e si applicano solo se la chiave di AD RMS è protetta tramite software e si vuole eseguire la migrazione ad Azure Information Protection con una chiave del tenant protetta tramite software.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 81a5cf4f-c1f3-44a9-ad42-66e95f33ed27
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: f8aef51156bb92d7d37da300ae2fccd51d739de1
ms.sourcegitcommit: a2542aec8cd2bf96e94923740bf396badff36b6a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/03/2019
ms.locfileid: "67535116"
---
# <a name="step-2-software-protected-key-to-software-protected-key-migration"></a>Passaggio 2: Migrazione da una chiave protetta tramite software a un'altra

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Queste istruzioni fanno parte del [percorso di migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md) e si applicano solo se la chiave di AD RMS è protetta tramite software e si vuole eseguire la migrazione ad Azure Information Protection con una chiave del tenant protetta tramite software. 

Se non si tratta dello scenario di configurazione scelto, tornare al [Passaggio 4. Esportare i dati di configurazione da AD RMS e importarli in Azure RMS](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection), quindi scegliere una configurazione diversa.

Usare la procedura seguente per importare la configurazione di AD RMS in Azure Information Protection. La chiave del tenant di Azure Information Protection verrà gestita da Microsoft.

## <a name="to-import-the-configuration-data-to-azure-information-protection"></a>Per importare i dati di configurazione in Azure Information Protection

1. In una workstation connessa a Internet, usare il [Connect-AipService](/powershell/module/aipservice/connect-aipservice) per connettersi al servizio Azure Rights Management:

    ```
    Connect-AipService
    ```
    Quando viene richiesto, immettere le credenziali di amministratore del tenant Azure Rights Management. In genere, viene usato un account amministratore globale per Azure Active Directory o Office 365.

2. Usare la [Import-AipServiceTpd](/powershell/module/aipservice/import-aipservicetpd) esportato di cmdlet per caricare ogni file (con estensione XML) di dominio di pubblicazione trusted. Ad esempio, è necessario avere almeno un file aggiuntivo da importare in caso di aggiornamento del cluster AD RMS per la modalità di crittografia 2. 
    
    Per eseguire questo cmdlet, sarà necessaria la password specificata in precedenza per ogni file di dati di configurazione. 
    
    Ad esempio, eseguire prima di tutto il comando seguente per archiviare la password:
    
        $TPD_Password = Read-Host -AsSecureString
    
    Immettere la password specificata per esportare il primo file di dati di configurazione. Usando E:\contosokey1.xml come esempio per il file di configurazione, eseguire quindi il comando seguente e confermare che si vuole eseguire questa azione:
    ```
    Import-AipServiceTpd -TpdFile E:\contosokey1.xml -ProtectionPassword $TPD_Password -Verbose
    ```
    
3. Dopo aver caricato ogni file, eseguire [Set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties) per identificare la chiave importata corrisponde alla chiave del certificato concessore di licenze attualmente attiva in AD RMS. Questa chiave diventerà la chiave del tenant attiva per il servizio Azure Rights Management.

4.  Usare la [Disconnect-AipServiceService](/powershell/module/aipservice/disconnect-aipservice) cmdlet per disconnettersi dal servizio Azure Rights Management:

    ```
    Disconnect-AipServiceService
    ```

È ora possibile andare al [Passaggio 5. Attivare il servizio Azure Rights Management](migrate-from-ad-rms-phase2.md#step-5-activate-the-azure-rights-management-service).


