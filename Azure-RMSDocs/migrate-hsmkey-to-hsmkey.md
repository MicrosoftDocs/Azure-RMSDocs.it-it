---
title: Eseguire la migrazione da una chiave protetta tramite HSM a un'altra - AIP
description: Istruzioni che fanno parte del percorso di migrazione da AD RMS ad Azure Information Protection e si applicano solo se la chiave di AD RMS è protetta tramite HSM e si vuole eseguire la migrazione ad Azure Information Protection con una chiave del tenant protetta tramite HSM in Insieme di credenziali delle chiavi di Azure.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/13/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: c5bbf37e-f1bf-4010-a60f-37177c9e9b39
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 7ddaf0a54aa116a317cee8699caf437faae9676f
ms.sourcegitcommit: bcc9e0f9ae8512bf48d819533cf8ef3b667eb298
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52330333"
---
# <a name="step-2-hsm-protected-key-to-hsm-protected-key-migration"></a>Passaggio 2: Migrazione da una chiave protetta tramite HSM a un'altra

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*


Queste istruzioni fanno parte del [percorso di migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md) e si applicano solo se la chiave di AD RMS è protetta tramite HSM e si vuole eseguire la migrazione ad Azure Information Protection con una chiave del tenant protetta tramite HSM in Insieme di credenziali delle chiavi di Azure. 

Se non si tratta dello scenario di configurazione scelto, tornare al [Passaggio 4. Esportare i dati di configurazione da AD RMS e importarli in Azure RMS](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection), quindi scegliere una configurazione diversa.

> [!NOTE]
> Queste istruzioni presuppongono che la chiave di AD RMS sia protetta da modulo. Questo è il caso più tipico. 

Si tratta di una procedura in due parti per importare la chiave protetta tramite HSM e la configurazione di AD RMS in Azure Information Protection. La chiave del tenant di Azure Information Protection verrà gestita dall'utente (BYOK).

Poiché la chiave del tenant di Azure Information Protection verrà archiviata e gestita da Insieme di credenziali delle chiavi di Azure, questa parte della migrazione richiede l'amministrazione in Insieme di credenziali delle chiavi di Azure oltre ad Azure Information Protection. Se Azure Key Vault viene gestito da un amministratore diverso da quello dell'organizzazione, è necessario coordinare e collaborare con tale amministratore per completare queste procedure.

Prima di iniziare, assicurarsi che l'organizzazione disponga di un insieme di credenziali delle chiavi creato in Insieme di credenziali delle chiavi di Azure che supporta le chiavi protette tramite HSM. Sebbene non sia obbligatorio, si consiglia di avere un insieme di credenziali delle chiavi dedicato per Azure Information Protection. Questo insieme di credenziali delle chiavi verrà configurato per consentire al servizio Azure Rights Management di accedervi, pertanto le chiavi archiviate in questo insieme di credenziali devono essere limitate alle sole chiavi di Azure Information Protection.


> [!TIP]
> Se è necessario eseguire i passaggi di configurazione per Azure Key Vault e non si ha familiarità con questo servizio di Azure, può risultare utile consultare prima di tutto [Introduzione ad Azure Key Vault](/azure/key-vault/key-vault-get-started). 


## <a name="part-1-transfer-your-hsm-key-to-azure-key-vault"></a>Parte 1: Trasferire la chiave protetta tramite HSM a Insieme di credenziali delle chiavi di Azure

Queste procedure vengono eseguite dall'amministratore di Insieme di credenziali delle chiavi di Azure.

1. Per ogni chiave del certificato concessore di licenze server da archiviare in Azure Key Vault, seguire le istruzioni della documentazione di Azure Key Vault, usando [Implementazione di BYOK (Bring Your Own Key) per Azure Key Vault](/azure/key-vault/key-vault-hsm-protected-keys#implementing-bring-your-own-key-byok-for-azure-key-vault) con l'eccezione seguente:

    - Non eseguire la procedura per **generare la chiave del tenant**, perché ne esiste già una equivalente nella distribuzione di AD RMS. È invece necessario identificare la chiave usata dal server AD RMS dall'installazione di Thales e usare questa chiave durante la migrazione. I file di chiave crittografati di Thales sono in genere denominati **key<*nomeAppChiave*><*identificatoreChiave*>** in locale nel server.

    Quando la chiave viene caricata in Insieme di credenziali delle chiavi di Azure, vengono visualizzate le proprietà della chiave visualizzata, incluso l'ID della chiave. Sarà simile a https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333. Prendere nota dell'URL perché è necessario all'amministratore di Azure Information Protection per indicare al servizio Azure Rights Management di usare questa chiave per la chiave del tenant.

2. Nella workstation connessa a Internet, in una sessione di PowerShell, usare il cmdlet [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) per autorizzare l'entità di servizio di Azure Rights Management ad accedere all'insieme di credenziali delle chiavi in cui verrà archiviata la chiave del tenant di Azure Information Protection. Le autorizzazioni necessarie sono decrypt, encrypt, unwrapkey, wrapkey, verify e sign.
    
    Se ad esempio l'insieme di credenziali delle chiavi creato per Azure Information Protection è denominato contoso-byok-ky e il gruppo di risorse è denominato contoso-byok-rg, eseguire il comando seguente:
    
        Set-AzureRmKeyVaultAccessPolicy -VaultName "contoso-byok-kv" -ResourceGroupName "contoso-byok-rg" -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,sign,get


Ora che la chiave HSM è stata preparata in Insieme di credenziali delle chiavi di Azure per il servizio Azure Rights Management di Azure Information Protection, si è pronti per importare i dati di configurazione di AD RMS.

## <a name="part-2-import-the-configuration-data-to-azure-information-protection"></a>Parte 2: Importare i dati di configurazione in Azure Information Protection

Queste procedure vengono eseguite dall'amministratore di Azure Information Protection.

1. Nella workstation connessa a Internet e nella sessione di PowerShell connettersi al servizio Azure Rights Management usando il cmdlet [Connect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice).
    
    Caricare quindi ogni file del dominio di pubblicazione trusted (con estensione xml) tramite il cmdlet [Import-AadrmTpd](/powershell/aadrm/vlatest/import-aadrmtpd). Ad esempio, è necessario avere almeno un file aggiuntivo da importare in caso di aggiornamento del cluster AD RMS per la modalità di crittografia 2.
    
    Per eseguire questo cmdlet, sono necessari la password specificata in precedenza per ogni file di dati di configurazione e l'URL della chiave identificato nel passaggio precedente.
    
    Ad esempio, usando il file di dati di configurazione C:\contoso-tpd1.xml e il valore dell'URL della chiave dal passaggio precedente, eseguire prima di tutto il comando seguente per archiviare la password:
    
    ```
    $TPD_Password = Read-Host -AsSecureString
    ```
    
    Immettere la password specificata per esportare il file di dati di configurazione. Eseguire quindi il comando seguente e confermare che si vuole eseguire questa azione:
    
    ```
    Import-AadrmTpd -TpdFile "C:\contoso-tpd1.xml" -ProtectionPassword $TPD_Password –KeyVaultKeyUrl https://contoso-byok-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 -Verbose
    ```
    
    Durante l'importazione, la chiave del certificato concessore di licenze server viene importata e impostata automaticamente come archiviata.

2.  Dopo aver caricato ogni file, eseguire [Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties) per specificare quale chiave importata corrisponde alla chiave del certificato concessore di licenze server attualmente attiva nel cluster AD RMS. Questa chiave diventa la chiave del tenant attiva per il servizio Azure Rights Management.

3.  Usare il cmdlet [Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice) per disconnettersi dal servizio Azure Rights Management:

    ```
    Disconnect-AadrmService
    ```

Se successivamente si deve confermare quale chiave viene usata dal tenant di Azure Information Protection in Insieme di credenziali delle chiavi di Azure, usare il cmdlet [Get-AadrmKeys](/powershell/aadrm/vlatest/get-aadrmkeys) di Azure RMS.

È ora possibile andare al [Passaggio 5. Attivare il servizio Azure Rights Management](migrate-from-ad-rms-phase2.md#step-5-activate-the-azure-rights-management-service).


