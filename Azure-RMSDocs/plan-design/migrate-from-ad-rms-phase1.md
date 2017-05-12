---
title: Eseguire la migrazione da AD RMS ad Azure Information Protection - Fase 1
description: Fase 1 della migrazione da AD RMS ad Azure Information Protection che include i passaggi da 1 a 3 della migrazione da AD RMS ad Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/27/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: d954d3ee-3c48-4241-aecf-01f4c75fa62c
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 587d24a005452874ca06b8fc179b25e91a7f0130
ms.sourcegitcommit: ed954c84c9009d205638f0ad54fdbfc02ef5b92c
ms.translationtype: HT
ms.contentlocale: it-IT
---
# <a name="migration-phase-1---preparation"></a>Fase 1 della migrazione: preparazione

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Office 365*

Usare le informazioni seguenti per la fase 1 della migrazione da AD RMS ad Azure Information Protection. Queste procedure illustrano i passaggi da 1 a 3 della [migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md) e preparano l'ambiente per la migrazione senza influenzare il lavoro degli utenti.


## <a name="step-1-download-the-azure-rights-management-administration-tool-and-identify-your-tenant-url"></a>Passaggio 1: scaricare Azure Rights Management Administration Tool e identificare l'URL tenant

Passare all'Area download Microsoft e [scaricare Azure Rights Management Administration Tool](https://go.microsoft.com/fwlink/?LinkId=257721), contenente il modulo di amministrazione di Azure Rights Management per Windows PowerShell. Azure Rights Management (Azure RMS) è il servizio che assicura la protezione dei dati per Azure Information Protection.

Installare lo strumento. Per le istruzioni, vedere [Installazione di Windows PowerShell per Microsoft Azure Rights Management](../deploy-use/install-powershell.md).

> [!NOTE]
> Se il modulo Windows PowerShell è stato scaricato in precedenza, eseguire il comando seguente per verificare che il numero di versione in uso sia almeno **2.9.0.0**: `(Get-Module aadrm -ListAvailable).Version`

Per completare alcune delle istruzioni di migrazione, è necessario conoscere l'URL del servizio Azure Rights Management del tenant in modo che sia possibile sostituirlo quando vengono visualizzati i riferimenti all'*\<URL del tenant\>*. L'URL del servizio Azure Rights Management ha il formato seguente: **{GUID}.rms.[Region].aadrm.com**.

Ad esempio, : **5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

### <a name="to-identify-your-azure-rights-management-service-url"></a>Per identificare l'URL del servizio Azure Rights Management

1. Connettersi al servizio Azure Rights Management e, quando richiesto, immettere le credenziali di amministratore globale del tenant:
    
        Connect-AadrmService
    
2. Ottenere la configurazione del tenant:
    
        Get-AadrmConfiguration
    
3. Copiare il valore visualizzato per **LicensingIntranetDistributionPointUrl** e, da questa stringa, rimuovere `/_wmcs\licensing`. 
    
    Ciò che rimane è l'URL del servizio Azure Rights Management del tenant di Azure Information Protection, abbreviato in *URL tenant* nelle istruzioni di migrazione seguenti.

## <a name="step-2-prepare-for-client-migration"></a>Passaggio 2: Preparare la migrazione client

Nella maggior parte delle migrazioni, non è pratico eseguire la migrazione di tutti i client in una sola volta, è preferibile piuttosto eseguire la migrazione dei client in batch. Ciò significa che per un periodo di tempo, alcuni client useranno Azure Information Protection e altri continueranno a usare AD RMS. Per supportare gli utenti non ancora migrati e gli utenti migrati, usare i controlli di onboarding e distribuire uno script di pre-migrazione. Questo passaggio è obbligatorio durante il processo di migrazione in modo che gli utenti non ancora migrati possano usare contenuto che è stato protetto da utenti migrati che già usano Azure Rights Management.

1. Ad esempio, creare un gruppo denominato **AIPMigrated**. Questo gruppo può essere creato in Active Directory e sincronizzato nel cloud oppure può essere creato in Office 365 o in Azure Active Directory. Non assegnare utenti al gruppo per il momento. In una fase successiva, dopo la migrazione degli utenti, è possibile aggiungere gli utenti al gruppo.

    Prendere nota dell'ID oggetto del gruppo. A tale scopo, è possibile usare Azure AD PowerShell, ad esempio usare il comando [Get-MsolGroup](/powershell/msonline/v1/Get-MsolGroup) nella versione 1.0 del modulo. Oppure è possibile copiare l'ID oggetto del gruppo dal portale di Azure.

2. Configurare il gruppo per i controlli di onboarding per consentire solo agli utenti di questo gruppo di usare Azure Rights Management per proteggere il contenuto. A tale scopo, in una sessione di PowerShell, connettersi al servizio Azure Rights Management e, quando richiesto, specificare le credenziali di amministratore globale:

        Connect-Aadrmservice

    Configurare quindi il gruppo per i controlli di onboarding, sostituendo l'ID oggetto del gruppo con quello usato in questo esempio, quindi immettere **Y** per confermare, quando viene richiesto:

        Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $False -SecurityGroupObjectId "fba99fed-32a0-44e0-b032-37b419009501"

3. [Scaricare il file seguente](https://go.microsoft.com/fwlink/?LinkId=524619) che contiene gli script di migrazione client:
    
    **ClientMigration.zip**
    
4. Estrarre i file e seguire le istruzioni in **PrepareClient.cmd** in modo che contenga il nome del server per l'URL di gestione licenze Extranet del cluster di AD RMS. 
    
    Per individuare il nome del server: dalla console di Active Directory Rights Management Services, fare clic sul nome del cluster. Nelle informazioni **Dettagli cluster**, copiare il nome del server dal valore **Gestione licenze** della sezione degli URL del cluster Extranet. Ad esempio: **rmscluster.contoso.com**.

    > [!IMPORTANT]
    > Le istruzioni includono la sostituzione degli indirizzi di esempio di **adrms.contoso.com** con gli indirizzi del server di AD RMS. Quando si esegue questa operazione, assicurarsi che non siano presenti spazi aggiuntivi prima o dopo gli indirizzi, che interrompono lo script di migrazione e sono molto difficili da identificare come la causa principale del problema. Alcuni strumenti di modifica aggiungono automaticamente uno spazio dopo aver incollato il testo.
    >

5. Distribuire questo script a tutti i computer Windows per assicurarsi che, quando si avvia la migrazione dei client, i client non ancora migrati continuino a comunicare con AD RMS, anche se usano contenuto protetto dai client migrati che invece usano il servizio Azure Rights Management.

    Per distribuire questo script è possibile usare Criteri di gruppo o un altro meccanismo di distribuzione software.

## <a name="step-3-prepare-your-exchange-deployment-for-migration"></a>Passaggio 3. Preparare la distribuzione di Exchange per la migrazione

Se si usa Exchange locale o Exchange online, è possibile che Exchange sia stato precedentemente integrato nella distribuzione di AD RMS. In questo passaggio verranno configurati entrambi in modo che usino la configurazione di AD RMS esistente per supportare il contenuto protetto da Azure RMS. 

Assicurarsi di avere gli [URL del servizio Azure Rights Management del tenant](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url) in modo che sia possibile sostituire questo valore in *&lt;URL tenant&gt;* nei comandi seguenti. 

**Se Exchange Online è stato integrato con AD RMS**: aprire una sessione di PowerShell per Exchange Online ed eseguire i comandi seguenti di PowerShell uno alla volta o in uno script:

    $irmConfig = Get-IRMConfiguration
    $list = $irmConfig.LicensingLocation
    $list += "<YourTenantURL>/_wmcs/licensing"
    Set-IRMConfiguration -LicensingLocation $list
    Set-IRMConfiguration -internallicensingenabled $false
    Set-IRMConfiguration -internallicensingenabled $true 

**Se Exchange locale è integrato con AD RMS**: per ogni organizzazione di Exchange, prima aggiungere i valori indicati di seguito nel Registro di sistema di ogni server Exchange e quindi eseguire i comandi PowerShell specificati. 

Valori del registro di sistema per Exchange 2013 ed Exchange 2016:

**Percorso del Registro di sistema:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**Tipo:** Reg_SZ

**Valore:** https://\<URL tenant\>/_wmcs/licensing

**Dati:** https://\<URL di gestione licenze Extranet AD RMS\>/_wmcs/licensing

---

Valori del Registro di sistema per Exchange 2010:

**Percorso del Registro di sistema:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**Tipo:** Reg_SZ

**Valore:** https://\<URL tenant\>/_wmcs/licensing

**Dati:** https://\<URL di gestione licenze Extranet AD RMS>/_wmcs/licensing

---

Comandi PowerShell da eseguire uno alla volta o in uno script

    $irmConfig = Get-IRMConfiguration
    $list = $irmConfig.LicensingLocation
    $list += "<YourTenantURL>/_wmcs/licensing"
    Set-IRMConfiguration -LicensingLocation $list
    Set-IRMConfiguration -internallicensingenabled $false
    Set-IRMConfiguration -RefreshServerCertificates
    Set-IRMConfiguration -internallicensingenabled $true
    IISReset


Dopo aver eseguito questi comandi per Exchange Online o Exchange locale, se la distribuzione di Exchange è configurata per supportare contenuto protetto da AD RMS, dopo la migrazione supporterà anche contenuto protetto da Azure RMS. La distribuzione di Exchange continuerà a usare AD RMS per supportare il contenuto protetto fino a un passaggio successivo nel processo di migrazione.


## <a name="next-steps"></a>Passaggi successivi
Passare a [Fase 2: configurazione lato server](migrate-from-ad-rms-phase2.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
