---
title: Passaggio 2&colon; Migrazione da una chiave protetta tramite HSM a un&quot;altra| Azure Information Protection
description: "Istruzioni che fanno parte del percorso di migrazione da AD RMS ad Azure Information Protection e si applicano solo se la chiave di AD RMS è protetta tramite HSM e si vuole eseguire la migrazione ad Azure Information Protection con una chiave del tenant protetta tramite HSM in Insieme di credenziali delle chiavi di Azure."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/14/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: c5bbf37e-f1bf-4010-a60f-37177c9e9b39
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 5f75e36e5939b23a9d077a6fcd659c59d0f71a68
ms.openlocfilehash: 9db60e1e841cd1f821501d402986dbd05a577f6f


---

# <a name="step-2-hsm-protected-key-to-hsm-protected-key-migration"></a>Passaggio 2: Migrazione da una chiave protetta tramite HSM a un'altra

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection*


Queste istruzioni fanno parte del [percorso di migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md) e si applicano solo se la chiave di AD RMS è protetta tramite HSM e si vuole eseguire la migrazione ad Azure Information Protection con una chiave del tenant protetta tramite HSM in Insieme di credenziali delle chiavi di Azure. 

Se non si tratta dello scenario di configurazione prescelto, tornare al [Passaggio 2. Esportare i dati di configurazione da AD RMS e importarli in Azure RMS](migrate-from-ad-rms-phase1.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection), quindi scegliere una configurazione diversa.

> [!NOTE]
> Queste istruzioni presuppongono che la chiave di AD RMS sia protetta da modulo. Questo è il caso più tipico. 

Si tratta di una procedura in due parti per importare la chiave protetta tramite HSM e la configurazione di AD RMS in Azure Information Protection. La chiave del tenant di Azure Information Protection verrà gestita dall'utente (BYOK).

Poiché la chiave del tenant di Azure Information Protection verrà archiviata e gestita da Insieme di credenziali delle chiavi di Azure, questa parte della migrazione richiede l'amministrazione in Insieme di credenziali delle chiavi di Azure oltre ad Azure Information Protection. Se Insieme di credenziali delle chiavi di Azure viene gestito da un amministratore diverso da quello dell'organizzazione, sarà necessario coordinare e collaborare con tale amministratore per completare queste procedure.

Prima di iniziare, assicurarsi che l'organizzazione disponga di un insieme di credenziali delle chiavi creato in Insieme di credenziali delle chiavi di Azure che supporta le chiavi protette tramite HSM. Sebbene non sia obbligatorio, si consiglia di avere un insieme di credenziali delle chiavi dedicato per Azure Information Protection. Questo insieme di credenziali delle chiavi verrà configurato per consentire al servizio Azure Rights Management di accedervi, pertanto le chiavi archiviate in questo insieme di credenziali devono essere limitate alle sole chiavi di Azure Information Protection.


> [!TIP]
> Se è necessario eseguire i passaggi di configurazione per Insieme di credenziali delle chiavi di Azure e non si ha familiarità con questo servizio, può risultare utile prima consultare [Introduzione all'insieme di credenziali delle chiavi di Azure](https://azure.microsoft.com/documentation/articles/key-vault-get-started/). 


## <a name="part-1-transfer-your-hsm-key-to-azure-key-vault"></a>Parte 1: Trasferire la chiave protetta tramite HSM a Insieme di credenziali delle chiavi di Azure

Queste procedure vengono eseguite dall'amministratore di Insieme di credenziali delle chiavi di Azure.

1.  Seguire le istruzioni della documentazione di Insieme di credenziali delle chiavi di Azure, usando [Implementazione di BYOK (Bring Your Own Key) per l'insieme di credenziali delle chiavi di Azure](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#implementing-bring-your-own-key-byok-for-azure-key-vault) con l'eccezione seguente:

    - Non eseguire la procedura per **generare la chiave del tenant**, perché ne esiste già una equivalente nella distribuzione di AD RMS. È invece necessario identificare la chiave usata dal server AD RMS dall'installazione di Thales e usare questa chiave durante la migrazione. I file di chiave crittografati di Thales sono in genere denominati **key<*nomeAppChiave*><*identificatoreChiave*>** in locale nel server.

    Quando la chiave viene caricata in Insieme di credenziali delle chiavi di Azure, vengono visualizzate le proprietà della chiave visualizzata, incluso l'ID della chiave. Avrà un aspetto simile a https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333. Prendere nota dell'URL perché sarà necessario all'amministratore di Azure Information Protection per indicare al servizio Azure Rights Management di usare questa chiave per la chiave del tenant.

2. Nella workstation connessa a Internet, in una sessione di PowerShell, usare il cmdlet [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/en-us/library/mt603625(v=azure.300\).aspx) per autorizzare l'entità servizio Azure Rights Management ad accedere all'insieme di credenziali delle chiavi in cui verrà archiviata la chiave del tenant di Azure Information Protection. Le autorizzazioni necessarie sono decrypt, encrypt, unwrapkey, wrapkey, verify e sign.
    
    Se ad esempio l'insieme di credenziali delle chiavi creato per Azure Information Protection è denominato contoso-byok-ky e il gruppo di risorse è denominato contoso-byok-rg, eseguire il comando seguente:
    
        Set-AzureRmKeyVaultAccessPolicy -VaultName "contoso-byok-kv" -ResourceGroupName "contoso-byok-rg" -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,encrypt,unwrapkey,wrapkey,verify,sign,get


Ora che la chiave HSM è stata preparata in Insieme di credenziali delle chiavi di Azure per il servizio Azure Rights Management di Azure Information Protection, si è pronti per importare i dati di configurazione di AD RMS.

## <a name="part-2-import-the-configuration-data-to-azure-information-protection"></a>Parte 2: Importare i dati di configurazione in Azure Information Protection

Queste procedure vengono eseguite dall'amministratore di Azure Information Protection.

1.  Nella workstation connessa a Internet e nella sessione di PowerShell connettersi al servizio Azure Rights Management usando il cmdlet [Connect-AadrmService](https://msdn.microsoft.com/library/dn629415.aspx).
    
    Caricare quindi il file del primo dominio di pubblicazione trusted esportato (con estensione xml) tramite il cmdlet [Import-AadrmTpd](https://msdn.microsoft.com/library/dn857523.aspx). Se si hanno più un file XML, perché avevi più domini di pubblicazione trusted, scegliere il file che contiene il dominio di pubblicazione trusted esportato che corrisponde alla chiave di HSM che si desidera utilizzare in Azure RMS per proteggere il contenuto dopo la migrazione. 
    
    Per eseguire questo cmdlet, è necessario l'URL della chiave identificata nel passaggio precedente.
    
    Ad esempio, usando il valore dell'URL della chiave dal passaggio precedente e un file di dominio di pubblicazione trusted di C:\contoso-tpd1.xml, eseguire:
    
    ```
    Import-AadrmTpd -TpdFile "C:\contoso-tpd1.xml" -ProtectionPassword –KeyVaultStringUrl https://contoso-byok-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 -Active $True -Verbose
    ```
    
    Quando richiesto, immettere la password specificata in precedenza e confermare che si desidera eseguire questa azione.

2.  Al termine del comando, ripetere il passaggio 1 per ogni restante file XML creato esportando il tuo domini di pubblicazione trusted. Per questi file impostare **-Active** su **false** quando si esegue il comando di importazione.  

3.  Usare il cmdlet [Disconnect-AadrmService](https://msdn.microsoft.com/library/azure/dn629416.aspx) per disconnettersi dal servizio Azure Rights Management:

    ```
    Disconnect-AadrmService
    ```

    > [!NOTE]
    > Se successivamente si deve confermare quale chiave viene usata dal tenant di Azure Information Protection in Insieme di credenziali delle chiavi di Azure, usare il cmdlet [Get-AadrmKeys](https://msdn.microsoft.com/library/dn629420.aspx) di Azure RMS.

È ora possibile andare al [Passaggio 3. Attivare il tenant di Azure Information Protection](migrate-from-ad-rms-phase1.md#step-3-activate-your-azure-information-protection-tenant).




<!--HONumber=Nov16_HO2-->


