---
title: Passaggio 2&colon; Migrazione da una chiave protetta tramite HSM a un'altra | Azure RMS
description: "Queste istruzioni fanno parte del percorso di migrazione da AD RMS ad Azure Rights Management e si applicano solo se la chiave di AD RMS è protetta tramite HSM e se si vuole eseguire la migrazione ad Azure Rights Management con una chiave del tenant protetta tramite HSM in Insieme di credenziali delle chiavi di Azure."
author: cabailey
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c5bbf37e-f1bf-4010-a60f-37177c9e9b39
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: 690729d16358b7b997d9cd1fd8cabed22ce78df4


---

# Passaggio 2: Migrazione da una chiave protetta tramite HSM a un'altra

>*Si applica a: Active Directory Rights Management Services, Azure Rights Management*


Queste istruzioni fanno parte del [percorso di migrazione da AD RMS ad Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) e si applicano solo se la chiave di AD RMS è protetta tramite HSM e se si vuole eseguire la migrazione ad Azure Rights Management con una chiave del tenant protetta tramite HSM in Insieme di credenziali delle chiavi di Azure. 

Se non si tratta dello scenario di configurazione prescelto, tornare al [Passaggio 2. Esportare i dati di configurazione da AD RMS e importarli in Azure RMS](migrate-from-ad-rms-phase1.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms), quindi scegliere una configurazione diversa.

> [!NOTE]
> Queste istruzioni presuppongono che la chiave di AD RMS sia protetta da modulo. Questo è il caso più tipico. 

Questa procedura in due parti consente di importare la chiave HSM e la configurazione di AD RMS in Azure RMS. La chiave del tenant di Azure RMS verrà gestita dall'utente (BYOK).

Poiché la chiave del tenant di Azure RMS verrà archiviata e gestita da Insieme di credenziali delle chiavi di Azure, questa parte della migrazione richiede l'amministrazione in Insieme di credenziali delle chiavi di Azure oltre alla chiave di Azure RMS. Se Insieme di credenziali delle chiavi di Azure viene gestito da un amministratore diverso da quello dell'organizzazione, sarà necessario coordinare e collaborare con tale amministratore per completare queste procedure.

Prima di iniziare, assicurarsi che l'organizzazione disponga di un insieme di credenziali delle chiavi creato in Insieme di credenziali delle chiavi di Azure che supporta le chiavi protette tramite HSM. Sebbene non sia obbligatorio, si consiglia di avere un insieme di credenziali delle chiavi dedicato per Azure RMS. Questo insieme di credenziali delle chiavi verrà configurato per consentire l'accesso ad Azure RMS, pertanto le chiavi archiviate da questo insieme di credenziali delle chiavi devono essere limitate alle sole chiavi di Azure RMS.


> [!TIP]
> Se è necessario eseguire i passaggi di configurazione per Insieme di credenziali delle chiavi di Azure e non si ha familiarità con questo servizio, può risultare utile prima consultare [Introduzione all'insieme di credenziali delle chiavi di Azure](https://azure.microsoft.com/documentation/articles/key-vault-get-started/). 


## Parte 1: Trasferire la chiave protetta tramite HSM a Insieme di credenziali delle chiavi di Azure

Queste procedure vengono eseguite dall'amministratore di Insieme di credenziali delle chiavi di Azure.

1.  Seguire le istruzioni della documentazione di Insieme di credenziali delle chiavi di Azure, usando [Implementazione di BYOK (Bring Your Own Key) per l'insieme di credenziali delle chiavi di Azure](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#implementing-bring-your-own-key-byok-for-azure-key-vault) con l'eccezione seguente:

    - Non eseguire la procedura per **generare la chiave del tenant**, perché ne esiste già una equivalente nella distribuzione di AD RMS. È invece necessario identificare la chiave usata dal server AD RMS dall'installazione di Thales e usare questa chiave durante la migrazione. I file di chiave crittografati di Thales sono in genere denominati **key<*nomeAppChiave*><*identificatoreChiave*>** in locale nel server.

    Quando la chiave viene caricata in Insieme di credenziali delle chiavi di Azure, vengono visualizzate le proprietà della chiave visualizzata, incluso l'ID della chiave. Avrà un aspetto simile a https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333. Prendere nota dell'URL perché l'amministratore di Azure RMS ne avrà bisogno per indicare ad Azure RMS di usare questa chiave per la chiave del tenant.

2. Nella workstation connessa a Internet, in una sessione di PowerShell, usare il cmdlet [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx ) per autorizzare l'entità di servizio di Azure RMS (Microsoft.Azure.RMS) per accedere all'insieme di credenziali delle chiavi in cui verrà archiviata la chiave del tenant di Azure RMS. Le autorizzazioni necessarie sono decrypt, encrypt, unwrapkey, wrapkey, verify e sign.
    
    Ad esempio, se l'insieme di credenziali delle chiavi creato per Azure RMS è denominato contoso-byok-ky e il gruppo di risorse è denominato contoso-byok-rg, eseguire il comando seguente:
    
        Set-AzureRmKeyVaultAccessPolicy -VaultName "contoso-byok-kv" -ResourceGroupName "contoso-byok-rg" -ServicePrincipalName Microsoft.Azure.RMS -PermissionsToKeys decrypt,encrypt,unwrapkey,wrapkey,verify,sign


Ora che la chiave HSM è stata preparata in Insieme di credenziali delle chiavi di Azure per Azure RMS, si è pronti per importare i dati di configurazione di AD RMS.

## Parte 2: Importare i dati di configurazione in Azure RMS

Queste procedure vengono eseguite dall'amministratore di Azure RMS.

1.  Nella workstation connessa a Internet e nella sessione di PowerShell, connettersi ad Azure RMS usando il cmdlet [Connnect-AadrmService](https://msdn.microsoft.com/library/dn629415.aspx ).
    
    Caricare quindi il file del primo dominio di pubblicazione trusted esportato (con estensione xml) tramite il cmdlet [Import-AadrmTpd](https://msdn.microsoft.com/library/dn857523.aspx). Se si hanno più un file XML, perché avevi più domini di pubblicazione trusted, scegliere il file che contiene il dominio di pubblicazione trusted esportato che corrisponde alla chiave di HSM che si desidera utilizzare in Azure RMS per proteggere il contenuto dopo la migrazione. 
    
    Per eseguire questo cmdlet, è necessario l'URL della chiave identificata nel passaggio precedente.
    
    Ad esempio, usando il valore dell'URL della chiave dal passaggio precedente e un file di dominio di pubblicazione trusted di C:\contoso-tpd1.xml, eseguire:
    
    ```
    Import-AadrmTpd -TpdFile "C:\contoso-tpd1.xml" -ProtectionPassword –KeyVaultStringUrl https://contoso-byok-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 -Active $True -Verbose
    ```
    
    Quando richiesto, immettere la password specificata in precedenza e confermare che si desidera eseguire questa azione.

2.  Al termine del comando, ripetere il passaggio 1 per ogni restante file XML creato esportando il tuo domini di pubblicazione trusted. Per questi file impostare **-Active** su **false** quando si esegue il comando di importazione.  

3.  Usare il cmdlet [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) per disconnettersi dal servizio Azure RMS:

    ```
    Disconnect-AadrmService
    ```

    > [!NOTE]
    > Se successivamente si vuole verificare la chiave del tenant di Azure RMS da usare in Insieme di credenziali delle chiavi di Azure, usare il cmdlet [Get-AadrmKeys](https://msdn.microsoft.com/library/dn629420.aspx) di Azure RMS.

È ora possibile andare al [Passaggio 3. Attivare il tenant di RMS](migrate-from-ad-rms-phase1.md#step-3-activate-your-rms-tenant).




<!--HONumber=Aug16_HO4-->


