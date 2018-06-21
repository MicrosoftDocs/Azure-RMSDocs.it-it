---
title: Eseguire la migrazione da una chiave protetta tramite software a una chiave protetta tramite HSM - AIP
description: Istruzioni che fanno parte del percorso di migrazione da AD RMS ad Azure Information Protection e si applicano solo se la chiave di AD RMS è protetta tramite software e si vuole eseguire la migrazione ad Azure Information Protection con una chiave del tenant protetta tramite HSM in Insieme di credenziali delle chiavi di Azure.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/19/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: c5f4c6ea-fd2a-423a-9fcb-07671b3c2f4f
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 659fbe634326e7571f489b1ae2e1bc4176eadb0a
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
ms.locfileid: "30208074"
---
# <a name="step-2-software-protected-key-to-hsm-protected-key-migration"></a>Passaggio 2: Migrazione da una chiave protetta tramite software a una chiave protetta tramite HSM

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*


Istruzioni che fanno parte del [percorso di migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md) e si applicano solo se la chiave di AD RMS è protetta tramite software e si vuole eseguire la migrazione ad Azure Information Protection con una chiave del tenant protetta tramite HSM in Insieme di credenziali delle chiavi di Azure. 

Se non si tratta dello scenario di configurazione scelto, tornare al [Passaggio 4. Esportare i dati di configurazione da AD RMS e importarli in Azure RMS](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection), quindi scegliere una configurazione diversa.

Si tratta di una procedura in quattro parti per importare la configurazione di AD RMS in Azure Information Protection. La chiave del tenant di Azure Information Protection verrà gestita dall'utente (BYOK) in Insieme di credenziali delle chiavi di Azure.

È innanzitutto necessario estrarre la chiave del certificato concessore di licenze server (SLC) dai dati di configurazione di AD RMS e trasferire la chiave in un modulo HSM di Thales locale, quindi creare il pacchetto e trasferire la chiave HSM in Insieme di credenziali delle chiavi di Azure, autorizzare il servizio Azure Rights Management di Azure Information Protection per l'accesso all'insieme di credenziali delle chiavi e infine importare i dati di configurazione.

Poiché la chiave del tenant di Azure Information Protection verrà archiviata e gestita da Insieme di credenziali delle chiavi di Azure, questa parte della migrazione richiede l'amministrazione in Insieme di credenziali delle chiavi di Azure oltre ad Azure Information Protection. Se Azure Key Vault viene gestito da un amministratore diverso da quello dell'organizzazione, è necessario coordinare e collaborare con tale amministratore per completare queste procedure.

Prima di iniziare, assicurarsi che l'organizzazione disponga di un insieme di credenziali delle chiavi creato in Insieme di credenziali delle chiavi di Azure che supporta le chiavi protette tramite HSM. Sebbene non sia obbligatorio, si consiglia di avere un insieme di credenziali delle chiavi dedicato per Azure Information Protection. Questo insieme di credenziali delle chiavi verrà configurato per consentire al servizio Azure Rights Management di Azure Information Protection di accedervi, pertanto le chiavi archiviate in questo insieme di credenziali devono essere limitate alle sole chiavi di Azure Information Protection.


> [!TIP]
> Se è necessario eseguire i passaggi di configurazione per Azure Key Vault e non si ha familiarità con questo servizio di Azure, può risultare utile consultare prima di tutto [Introduzione ad Azure Key Vault](/azure/key-vault/key-vault-get-started). 


## <a name="part-1-extract-your-slc-key-from-the-configuration-data-and-import-the-key-to-your-on-premises-hsm"></a>Parte 1: Estrarre la chiave del certificato concessore di licenze server (SLC) dai dati di configurazione e importare la chiave nel modulo di protezione hardware locale

1.  Amministratore di Azure Key Vault: per ogni chiave del certificato concessore di licenze server esportata che si vuole archiviare in Azure Key Vault usare i passaggi seguenti nella sezione [Implementazione di BYOK (Bring Your Own Key) per Azure Key Vault](/azure/key-vault/key-vault-hsm-protected-keys#implementing-bring-your-own-key-byok-for-azurekey-vault) della documentazione di Azure Key Vault:

    -   **Generare e trasferire la propria chiave al modulo di protezione hardware di Insieme di credenziali delle chiavi di Azure**: [Passaggio 1: Preparare la workstation connessa a Internet](/azure/key-vault-hsm-protected-keys/#step-1-prepare-your-internet-connected-workstation)

    -   **Generare e trasferire la propria chiave del tenant tramite Internet**: [Passaggio 2: Preparare la workstation disconnessa](/azure/key-vault-hsm-protected-keys/#step-2-prepare-your-disconnected-workstation)

    Non attenersi a questa procedura per generare la chiave del tenant, perché è già disponibile una chiave equivalente nel file di dati di configurazione (con estensione XML) esportati. Si eseguirà invece uno strumento per estrarre la chiave dal file e importarla nel modulo di protezione hardware locale. Quando viene eseguito, lo strumento crea due file:

    - Un nuovo file dei dati di configurazione senza chiave, che è quindi pronto per essere importato nel tenant di Azure Information Protection.

    - Un file PEM (contenitore di chiavi) con la chiave, che è quindi pronto per essere importato nel modulo di protezione hardware locale.

2. Amministratore di Azure Information Protection o di Insieme di credenziali delle chiavi di Azure: nella workstation disconnessa eseguire lo strumento TpdUtil dal [toolkit di migrazione di Azure RMS](https://go.microsoft.com/fwlink/?LinkId=524619). Ad esempio, se lo strumento è installato nell'unità E in cui si copia il file dei dati di configurazione denominato ContosoTPD.xml:

    ```
        E:\TpdUtil.exe /tpd:ContosoTPD.xml /otpd:ContosoTPD.xml /opem:ContosoTPD.pem
    ```

    Se è disponibile più di un file dei dati di configurazione di RMS, eseguire tale strumento per i file restanti.

    Per visualizzare la Guida per questo strumento, che include una descrizione, istruzioni sull'utilizzo ed esempi, eseguire TpdUtil.exe senza parametri

    Informazioni aggiuntive per questo comando:

    - **/tpd**: specifica il percorso completo e il nome del file dei dati di configurazione di AD RMS esportato. Il nome del parametro completo è **TpdFilePath**.

    - **/otpd**: specifica il nome del file di output per il file dei dati di configurazione senza la chiave. Il nome del parametro completo è **OutPfxFile**. Se non si specifica questo parametro, l'impostazione predefinita del file di output è il nome del file originale con il suffisso **_keyless** e viene archiviato nella cartella corrente.

    - **/opem**: specifica il nome del file di output per il file PEM, che contiene la chiave estratta. Il nome del parametro completo è **OutPemFile**. Se non si specifica questo parametro, l'impostazione predefinita del file di output è il nome del file originale con il suffisso **_key** e viene archiviato nella cartella corrente.

    - Se non si specifica la password quando si esegue questo comando (tramite il nome completo del parametro **TpdPassword** o il nome breve del parametro **pwd**), viene richiesto di specificarla.

3. Nella stessa workstation disconnessa, collegare e configurare il modulo di protezione hardware Thales, in base alla documentazione di Thales. È ora possibile importare la chiave nel modulo di protezione hardware Thales collegato usando il comando seguente in cui è necessario sostituire il proprio nome di file per ContosoTPD.pem:

        generatekey --import simple pemreadfile=e:\ContosoTPD.pem plainname=ContosoBYOK protect=module ident=contosobyok type=RSA

    > [!NOTE]
    >Se si hanno più file, selezionare quello che corrisponde alla chiave HSM che si vuole usare in Azure RMS per proteggere il contenuto dopo la migrazione.

    Questo genera una visualizzazione di output simile alla seguente:

    **key generation parameters:**

    **operation &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Operation to perform &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; import**

    **application &nbsp;&nbsp;&nbsp;&nbsp;Application&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; simple**

    **verify &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Verify security of configuration key&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; yes**

    **type &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Key type &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; RSA**

    **pemreadfile &nbsp;&nbsp; PEM file containing RSA key &nbsp;&nbsp; e:\ContosoTPD.pem**

    **ident &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Key identifier &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; contosobyok**

    **plainname &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Key name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ContosoBYOK**

    **Key successfully imported.**

    **Path to key: C:\ProgramData\nCipher\Key Management Data\local\key_simple_contosobyok**

Questo output conferma che la chiave privata è stata migrata al dispositivo di protezione hardware di Thales locale con una copia crittografata salvata in una chiave (nell'esempio, "key_simple_contosobyok"). 

Ora che la chiave del certificato concessore di licenze server (SLC) è stata estratta e importata nel modulo di protezione hardware locale, si è pronti per creare un pacchetto della chiave protetta tramite HSM e trasferirlo in Insieme di credenziali delle chiavi di Azure.

> [!IMPORTANT]
> Una volta completato questo passaggio, cancellare in modo sicuro questi file PEM dalla workstation disconnessa per garantire che non siano accessibili da utenti non autorizzati. Per eliminare in modo sicuro tutti i file dall'unità E, eseguire ad esempio "cipher /w: E".

## <a name="part-2-package-and-transfer-your-hsm-key-to-azure-key-vault"></a>Parte 2: Creare il pacchetto e trasferire la chiave del modulo di protezione hardware in Insieme di credenziali delle chiavi di Azure

Amministratore di Azure Key Vault: per ogni chiave del certificato concessore di licenze server esportata che si vuole archiviare in Azure Key Vault usare i passaggi seguenti nella sezione [Implementazione di BYOK (Bring Your Own Key) per Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#implementing-bring-your-own-key-byok-for-azurekey-vault) della documentazione di Azure Key Vault:

- [Passaggio 4: Preparare la chiave per il trasferimento](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-4-prepare-your-key-for-transfer)

- [Passaggio 5: Trasferire la chiave a Insieme di credenziali delle chiavi di Azure](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-5-transfer-your-key-to-azurekey-vault)

Non seguire i passaggi per generare la coppia di chiavi, perché si dispone già della chiave. Al contrario, eseguire un comando per trasferire tale chiave (in questo esempio, il parametro KeyIdentifier usa "contosobyok") dal modulo di protezione hardware locale.

Prima di trasferire la chiave a Insieme di credenziali delle chiavi di Azure, assicurarsi che l'utilità KeyTransferRemote.exe restituisca **Result: SUCCESS** (Risultato: ESITO POSITIVO) quando si crea una copia della chiave con autorizzazioni ridotte (passaggio 4.1) e quando si esegue la crittografia della chiave (passaggio 4.3).

Quando la chiave viene caricata in Insieme di credenziali delle chiavi di Azure, vengono visualizzate le proprietà della chiave visualizzata, incluso l'ID della chiave. Sarà simile a **https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333**. Prendere nota dell'URL perché sarà necessario all'amministratore di Azure Information Protection per indicare al servizio Azure Rights Management di Azure Information Protection di usare questa chiave per la chiave del tenant.

Usare quindi il cmdlet [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) per autorizzare l'entità di servizio di Azure Rights Management ad accedere all'insieme di credenziali delle chiavi. Le autorizzazioni necessarie sono decrypt, encrypt, unwrapkey, wrapkey, verify e sign.

Se ad esempio l'insieme di credenziali delle chiavi creato per Azure Information Protection è denominato contosorms-byok-kv e il gruppo di risorse è denominato contosorms-byok-rg, eseguire il comando seguente:
    
    Set-AzureRmKeyVaultAccessPolicy -VaultName "contosorms-byok-kv" -ResourceGroupName "contosorms-byok-rg" -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,encrypt,unwrapkey,wrapkey,verify,sign,get

Ora che la chiave HSM è stata trasferita in Insieme di credenziali delle chiavi di Azure, si è pronti per importare i dati di configurazione di AD RMS.

## <a name="part-3-import-the-configuration-data-to-azure-information-protection"></a>Parte 3: Importare i dati di configurazione in Azure Information Protection

1. Amministratore di Azure Information Protection: nella workstation connessa a Internet e nella sessione di PowerShell copiare i nuovi file di dati di configurazione (con estensione xml) la cui chiave del certificato concessore di licenze server è stata rimossa dopo l'esecuzione dello strumento TpdUtil.

2. Caricare ogni file con estensione xml usando il cmdlet [Import-AadrmTpd](/powershell/aadrm/vlatest/import-aadrmtpd). Ad esempio, è necessario avere almeno un file aggiuntivo da importare in caso di aggiornamento del cluster AD RMS per la modalità di crittografia 2.

    Per eseguire questo cmdlet, sono necessari la password specificata in precedenza per il file di dati di configurazione e l'URL della chiave identificato nel passaggio precedente.

    Ad esempio, usando il file di dati di configurazione C:\contoso_keyless.xml e il valore dell'URL della chiave dal passaggio precedente, eseguire prima di tutto il comando seguente per archiviare la password:
    
    ```
    $TPD_Password = Read-Host -AsSecureString
    ```
    
   Immettere la password specificata per esportare il file di dati di configurazione. Eseguire quindi il comando seguente e confermare che si vuole eseguire questa azione:

    ```
    Import-AadrmTpd -TpdFile "C:\contoso_keyless.xml" -ProtectionPassword $TPD_Password –KeyVaultStringUrl https://contoso-byok-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 -Verbose
    ```

    Durante l'importazione, la chiave del certificato concessore di licenze server viene importata e impostata automaticamente come archiviata.

3. Dopo aver caricato ogni file, eseguire [Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties) per specificare quale chiave importata corrisponde alla chiave del certificato concessore di licenze server attualmente attiva nel cluster AD RMS.

4. Usare il cmdlet [Disconnect-AadrmService](/powershell/aadrm/vlatest/disconnect-aadrmservice) per disconnettersi dal servizio Azure Rights Management:

    ```
    Disconnect-AadrmService
    ```

Se successivamente si deve confermare quale chiave viene usata dal tenant di Azure Information Protection in Insieme di credenziali delle chiavi di Azure, usare il cmdlet [Get-AadrmKeys](/powershell/aadrm/vlatest/get-aadrmkeys) di Azure RMS.


È ora possibile andare al [Passaggio 5. Attivare il servizio Azure Rights Management](migrate-from-ad-rms-phase2.md#step-5-activate-the-azure-rights-management-service).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

