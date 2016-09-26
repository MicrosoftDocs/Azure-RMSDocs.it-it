---
title: Passaggio 2&colon; Migrazione da una chiave protetta tramite software a una chiave protetta tramite HSM | Azure RMS
description: "Istruzioni che fanno parte del percorso di migrazione da AD RMS ad Azure Rights Management e si applicano solo se la chiave di AD RMS è protetta tramite software e se si vuole eseguire la migrazione ad Azure Rights Management con una chiave del tenant protetta tramite HSM in Insieme di credenziali delle chiavi di Azure."
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c5f4c6ea-fd2a-423a-9fcb-07671b3c2f4f
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ada00b6f6298e7d359c73eb38dfdac169eacb708
ms.openlocfilehash: f4341d648b591922df93a4d2ba5e14151743fcdb


---

# Passaggio 2: Migrazione da una chiave protetta tramite software a una chiave protetta tramite HSM

>*Si applica a: Active Directory Rights Management Services, Azure Rights Management*


Queste istruzioni fanno parte del [percorso di migrazione da AD RMS ad Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) e si applicano solo se la chiave di AD RMS è protetta dal software e se si vuole eseguire la migrazione ad Azure Rights Management con una chiave del tenant protetta tramite HSM in Insieme di credenziali delle chiavi di Azure. 

Se non si tratta dello scenario di configurazione prescelto, tornare al [Passaggio 2. Esportare i dati di configurazione da AD RMS e importarli in Azure RMS](migrate-from-ad-rms-phase1.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms), quindi scegliere una configurazione diversa.

Questa procedura in quattro parti consente di importare la configurazione di AD RMS in Azure RMS. La chiave del tenant di Azure RMS verrà gestita dall'utente (BYOK) in Insieme di credenziali delle chiavi di Azure.

È innanzitutto necessario estrarre la chiave del certificato concessore di licenze server (SLC) dai dati di configurazione di AD RMS e trasferire la chiave in un modulo di protezione hardware di Thales locale, quindi creare il pacchetto e trasferire la chiave del proprio modulo di protezione hardware in Insieme di credenziali delle chiavi di Azure, autorizzare Azure RMS per l'accesso all'insieme di credenziali e infine importare i dati di configurazione.

Poiché la chiave del tenant di Azure RMS verrà archiviata e gestita da Insieme di credenziali delle chiavi di Azure, questa parte della migrazione richiede l'amministrazione in Insieme di credenziali delle chiavi di Azure oltre alla chiave di Azure RMS. Se Insieme di credenziali delle chiavi di Azure viene gestito da un amministratore diverso da quello dell'organizzazione, sarà necessario coordinare e collaborare con tale amministratore per completare queste procedure.

Prima di iniziare, assicurarsi che l'organizzazione disponga di un insieme di credenziali delle chiavi creato in Insieme di credenziali delle chiavi di Azure che supporta le chiavi protette tramite HSM. Sebbene non sia obbligatorio, si consiglia di avere un insieme di credenziali delle chiavi dedicato per Azure RMS. Questo insieme di credenziali delle chiavi verrà configurato per consentire l'accesso ad Azure RMS, pertanto le chiavi archiviate da questo insieme di credenziali delle chiavi devono essere limitate alle sole chiavi di Azure RMS.


> [!TIP]
> Se è necessario eseguire i passaggi di configurazione per Insieme di credenziali delle chiavi di Azure e non si ha familiarità con questo servizio, può risultare utile prima consultare [Introduzione all'insieme di credenziali delle chiavi di Azure](https://azure.microsoft.com/documentation/articles/key-vault-get-started/). 


## Parte 1: Estrarre la chiave del certificato concessore di licenze server (SLC) dai dati di configurazione e importare la chiave nel modulo di protezione hardware locale

1.  Amministratore di Insieme di credenziali delle chiavi di Azure: usare i passaggi seguenti nella sezione [Implementazione di BYOK (Bring Your Own Key) per l'insieme di credenziali delle chiavi di Azure](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#implementing-bring-your-own-key-byok-for-azure-key-vault) della documentazione di Insieme di credenziali delle chiavi di Azure:

    -   **Generare e trasferire la propria chiave al modulo di protezione hardware di Insieme di credenziali delle chiavi di Azure**: [Passaggio 1: Preparare la workstation connessa a Internet](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-1-prepare-your-internet-connected-workstation)

    -   **Generare e trasferire la propria chiave del tenant tramite Internet**: [Passaggio 2: Preparare la workstation disconnessa](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-2-prepare-your-disconnected-workstation)

    Non attenersi a questa procedura per generare la chiave del tenant, perché è già disponibile una chiave equivalente nel file di dati di configurazione (con estensione XML) esportati. Si eseguirà invece uno strumento per estrarre la chiave dal file e importarla nel modulo di protezione hardware locale. Quando viene eseguito, lo strumento crea due file:

    - Un nuovo file dei dati di configurazione senza chiave, che è quindi pronto per essere importato nel tenant di Azure RMS.

    - Un file PEM (contenitore di chiavi) con la chiave, che è quindi pronto per essere importato nel modulo di protezione hardware locale.

2. Amministratore di Azure RMS o di Insieme di credenziali delle chiavi di Azure: nella workstation disconnessa, eseguire lo strumento TpdUtil dal [toolkit di migrazione di Azure RMS](https://go.microsoft.com/fwlink/?LinkId=524619). Ad esempio, se lo strumento è installato nell'unità E in cui si copia il file dei dati di configurazione denominato ContosoTPD.xml:

    ```
        E:\TpdUtil.exe /tpd:ContosoTPD.xml /otpd:ContosoTPD.xml /opem:ContosoTPD.pem
    ```

    Se è disponibile più di un file dei dati di configurazione di RMS, eseguire tale strumento per i file restanti.

    Per visualizzare la Guida per questo strumento, che include una descrizione, istruzioni sull'utilizzo ed esempi, eseguire TpdUtil.exe senza parametri

    Informazioni aggiuntive per questo comando:

    - **/tpd**: specifica il percorso completo e il nome del file dei dati di configurazione di AD RMS esportato. Il nome del parametro completo è **TpdFilePath**.

    - **/otpd**: specifica il nome del file di output per il file dei dati di configurazione senza la chiave. Il nome del parametro completo è **OutPfxFile**. Se non si specifica questo parametro, l'impostazione predefinita del file di output è il nome del file originale con il suffisso **_keyless** e viene archiviato nella cartella corrente.

    - **/opem**: specifica il nome del file di output per il file PEM, che contiene la chiave estratta. Il nome del parametro completo è **OutPemFile**. Se non si specifica questo parametro, l'impostazione predefinita del file di output è il nome del file originale con il suffisso **_key** e viene archiviato nella cartella corrente.

    - Se non si specifica la password quando si esegue questo comando (tramite il nome completo del parametro **TpdPassword** o il nome breve del parametro **pwd**), verrà richiesto di specificarla.

3. Nella stessa workstation disconnessa, collegare e configurare il modulo di protezione hardware Thales, in base alla documentazione di Thales. È ora possibile importare la chiave nel modulo di protezione hardware Thales collegato usando il comando seguente in cui è necessario sostituire il proprio nome di file per ContosoTPD.pem:

        generatekey --import simple pemreadfile=e:\ContosoTPD.pem plainname=ContosoBYOK protect=module ident=contosobyok type=RSA

    > [!NOTE]
    >Se si hanno più file, selezionare quello che corrisponde alla chiave HSM che si vuole usare in Azure RMS per proteggere il contenuto dopo la migrazione.

    Questo genera una visualizzazione di output simile alla seguente:

    **key generation parameters:**

    **operation &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Operation to perform &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; import**

    **application &nbsp;&nbsp;&nbsp;&nbsp;Application&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; simple**

    **verify &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Verify security of configration key&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; yes**

    **type &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Key type &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; RSA**

    **pemreadfile &nbsp;&nbsp; PEM file containing RSA key &nbsp;&nbsp; e:\ContosoTPD.pem**

    **ident &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Key identifier &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; contosobyok**

    **plainname &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Key name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ContosoBYOK**

    **Key successfully imported.**

    **Path to key: C:\ProgramData\nCipher\Key Management Data\local\key_simple_contosobyok**

Questo output conferma che la chiave privata è stata migrata al dispositivo di protezione hardware di Thales locale con una copia crittografata salvata in una chiave (nell'esempio, "key_simple_contosobyok"). 

Ora che la chiave del certificato concessore di licenze server (SLC) è stata estratta e importata nel modulo di protezione hardware locale, si è pronti per creare un pacchetto della chiave protetta tramite HSM e trasferirlo in Insieme di credenziali delle chiavi di Azure.

> [!IMPORTANT]
> Una volta completato questo passaggio, cancellare in modo sicuro questi file PEM dalla workstation disconnessa per garantire che non siano accessibili da utenti non autorizzati. Per eliminare in modo sicuro tutti i file dall'unità E, eseguire ad esempio "cipher /w:E".

## Parte 2: Creare il pacchetto e trasferire la chiave del modulo di protezione hardware in Insieme di credenziali delle chiavi di Azure

1.  Amministratore di Insieme di credenziali delle chiavi di Azure: usare i passaggi seguenti dalla sezione [Implementazione di BYOK (Bring Your Own Key) per l'insieme di credenziali delle chiavi di Azure](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#implementing-bring-your-own-key-byok-for-azure-key-vault) della documentazione di Insieme di credenziali delle chiavi di Azure:

    -   [Passaggio 4: Preparare la chiave per il trasferimento](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-4-prepare-your-key-for-transfer)

    -   [Passaggio 5: Trasferire la chiave a Insieme di credenziali delle chiavi di Azure](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#step-5-transfer-your-key-to-azure-key-vault)

    Non seguire i passaggi per generare la coppia di chiavi, perché si dispone già della chiave. Al contrario, eseguire un comando per trasferire tale chiave (in questo esempio, il parametro KeyIdentifier usa "contosobyok") dal modulo di protezione hardware locale.

    Prima di trasferire la chiave a Insieme di credenziali delle chiavi di Azure, assicurarsi che l'utilità KeyTransferRemote.exe restituisca **Result: SUCCESS** (Risultato: ESITO POSITIVO) quando si crea una copia della chiave con autorizzazioni ridotte (passaggio 4.1) e quando si esegue la crittografia della chiave (passaggio 4.3).

    Quando la chiave viene caricata in Insieme di credenziali delle chiavi di Azure, vengono visualizzate le proprietà della chiave visualizzata, incluso l'ID della chiave. Avrà un aspetto simile a **https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333**. Prendere nota dell'URL perché l'amministratore di Azure RMS ne avrà bisogno per indicare ad Azure RMS di usare questa chiave per la chiave del tenant.

    Ora che la chiave HSM è stata trasferita in Insieme di credenziali delle chiavi di Azure, si è pronti per importare i dati di configurazione di AD RMS.

## Parte 3: Importare i dati di configurazione in Azure RMS

1.  Amministratore di Azure RMS: nella workstation connessa a Internet e nella sessione di PowerShell, copiare i nuovi file di dati di configurazione (con estensione xml) che dispongono della chiave del certificato concessore di licenze server rimossa dopo l'esecuzione dello strumento TpdUtil.

2. Caricare il primo file con estensione xml, usando il cmdlet [Import-AadrmTpd](https://msdn.microsoft.com/library/dn857523.aspx). Se si hanno più file, perché erano disponibili più domini di pubblicazione trusted, scegliere il file che corrisponde alla chiave di HSM che si vuole usare in Azure RMS per proteggere il contenuto dopo la migrazione.

    Per eseguire questo cmdlet, è necessario l'URL della chiave identificata nel passaggio precedente.

    Ad esempio, usando il valore dell'URL della chiave dal passaggio precedente e un file dei dati di configurazione di C:\contoso_keyless.xml, eseguire:

    ```
    Import-AadrmTpd -TpdFile "C:\contoso_keyless.xml" -ProtectionPassword –KeyVaultStringUrl https://contoso-byok-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333 -Active $True -Verbose
    ```

    Quando richiesto, immettere la password specificata in precedenza per il file dei dati di configurazione e confermare che si vuole eseguire questa azione.

    Se è disponibile più di un file di dati di configurazione, ripetere questo comando per i file restanti. Per questi file impostare **-Active** su **false** quando si esegue il comando di importazione.



3.  Usare il cmdlet [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) per disconnettersi dal servizio Azure RMS:

    ```
    Disconnect-AadrmService
    ```

    > [!NOTE]
    > Se successivamente si vuole verificare la chiave del tenant di Azure RMS da usare in Insieme di credenziali delle chiavi di Azure, usare il cmdlet [Get-AadrmKeys](https://msdn.microsoft.com/library/dn629420.aspx) di Azure RMS.


È ora possibile andare al [Passaggio 3. Attivare il tenant di RMS](migrate-from-ad-rms-phase1.md#step-3-activate-your-rms-tenant).






<!--HONumber=Aug16_HO4-->

