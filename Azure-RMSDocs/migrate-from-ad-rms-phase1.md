---
title: Eseguire la migrazione da AD RMS ad Azure Information Protection - Fase 1
description: Fase 1 della migrazione da AD RMS ad Azure Information Protection che include i passaggi da 1 a 3 della migrazione da AD RMS ad Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/26/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: d954d3ee-3c48-4241-aecf-01f4c75fa62c
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 13c63f2e96b27a31b9afb91fbc8c03b9b198f9c1
ms.sourcegitcommit: d31cb53de64bafa2097e682550645cadc612ec3e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/30/2020
ms.locfileid: "96316824"
---
# <a name="migration-phase-1---preparation"></a>Fase 1 della migrazione: preparazione

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Usare le informazioni seguenti per la fase 1 della migrazione da AD RMS ad Azure Information Protection. Queste procedure illustrano i passaggi da 1 a 3 della [migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md) e preparano l'ambiente per la migrazione senza influenzare il lavoro degli utenti.

## <a name="step-1-install-the-aipservice-powershell-module-and-identify-your-tenant-url"></a>Passaggio 1: installare il modulo PowerShell AIPService e identificare l'URL del tenant

Installare il modulo **AIPService** per consentire la configurazione e la gestione del servizio che fornisce la protezione dei dati per Azure Information Protection.

Per istruzioni, vedere [installazione del modulo PowerShell AIPService](./install-powershell.md).

Per completare alcune delle istruzioni di migrazione, è necessario conoscere l'URL del servizio Rights Management di Azure per il tenant, in modo da poterlo sostituire quando vengono visualizzati i riferimenti a *\<Your Tenant URL\>* . 

L'URL del servizio Azure Rights Management ha il formato seguente: **{GUID}.rms.[Region].aadrm.com**. Ad esempio: **5c6bb73b-1038-4EEC-863D-49bded473437.RMS.na.AADRM.com**

### <a name="to-identify-your-azure-rights-management-service-url"></a>Per identificare l'URL del servizio Azure Rights Management

1. Connettersi al servizio Azure Rights Management e, quando richiesto, immettere le credenziali di amministratore globale del tenant:

    ```PowerShell
    Connect-AipService
    ```

2. Ottenere la configurazione del tenant:

    ```PowerShell
    Get-AipServiceConfiguration
    ```

3. Copiare il valore visualizzato per **LicensingIntranetDistributionPointUrl** e, da questa stringa, rimuovere `/_wmcs\licensing`.

    Il valore restante corrisponde all'URL del servizio Azure Rights Management per il tenant di Azure Information Protection. Questo valore viene spesso abbreviato in *URL del tenant* nelle istruzioni di migrazione seguenti.

    È possibile verificare di avere il valore corretto eseguendo il comando PowerShell seguente:

    ```PowerShell
    (Get-AipServiceConfiguration).LicensingIntranetDistributionPointUrl -match "https:\/\/[0-9A-Za-z\.-]*" | Out-Null; $matches[0]
    ```

## <a name="step-2-prepare-for-client-migration"></a>Passaggio 2: Preparare la migrazione client

Nella maggior parte delle migrazioni, non è pratico eseguire la migrazione di tutti i client in una sola volta, è preferibile piuttosto eseguire la migrazione dei client in batch. 

Ciò significa che per un periodo di tempo, alcuni client useranno Azure Information Protection e altri continueranno a usare AD RMS. Per supportare gli utenti non ancora migrati e gli utenti migrati, usare i controlli di onboarding e distribuire uno script di pre-migrazione. 

> [!NOTE]
> Questo passaggio è obbligatorio durante il processo di migrazione in modo che gli utenti non ancora migrati possano usare contenuto che è stato protetto da utenti migrati che già usano Azure Rights Management.
> 

**Per preparare la migrazione client**

1. Ad esempio, creare un gruppo denominato **AIPMigrated**. Questo gruppo può essere creato in Active Directory e sincronizzato nel cloud oppure può essere creato in Microsoft 365 o Azure Active Directory. 

    Non assegnare utenti al gruppo per il momento. In una fase successiva, dopo la migrazione degli utenti, è possibile aggiungere gli utenti al gruppo.

1. Prendere nota dell'ID oggetto di questo gruppo usando uno dei metodi seguenti:

    - **Usare Azure AD PowerShell.** Per la versione 1,0 del modulo, ad esempio, usare il comando [Get-MsolGroup](/powershell/msonline/v1/Get-MsolGroup) . 
    - **Copiare l'ID oggetto** del gruppo dal portale di Azure.

1. Configurare il gruppo per i controlli di onboarding per consentire solo agli utenti di questo gruppo di usare Azure Rights Management per proteggere il contenuto. 

    A tale scopo, in una sessione di PowerShell connettersi al servizio Rights Management di Azure. Quando richiesto, specificare le credenziali di amministratore globale:

    ```PowerShell
    Connect-AipService
    ```

    Configurare questo gruppo per i controlli di onboarding, sostituendo l'ID oggetto del gruppo con quello riportato in questo esempio. Quando richiesto, immettere **Y** per confermare.

    ```PowerShell
    Set-AipServiceOnboardingControlPolicy -UseRmsUserLicense $False -SecurityGroupObjectId "fba99fed-32a0-44e0-b032-37b419009501" -Scope WindowsApp
    ```

1. Scaricare il file di [**Migration-Scripts.zip**](https://go.microsoft.com/fwlink/?LinkId=524619) .

1. Estrarre i file e seguire le istruzioni in **Prepare-client. cmd**, in modo che contenga il nome del server per l'URL di gestione licenze Extranet del cluster ad RMS. Per individuare il nome, eseguire le operazioni seguenti:

    1. nella console di Active Directory Rights Management Services fare clic sul nome del cluster. 

    1. Nelle informazioni **Dettagli cluster**, copiare il nome del server dal valore **Gestione licenze** della sezione degli URL del cluster Extranet. Ad esempio: **rmscluster.contoso.com**.

    > [!IMPORTANT]
    > Le istruzioni includono la sostituzione degli indirizzi di esempio di **adrms.contoso.com** con gli indirizzi del server di AD RMS. 
    >
    > Quando si esegue questa operazione, assicurarsi che non siano presenti spazi aggiuntivi prima o dopo gli indirizzi. Gli spazi aggiuntivi interrompono lo script di migrazione ed è molto difficile da identificare come la causa principale del problema. 
    >
    > Alcuni strumenti di modifica aggiungono automaticamente uno spazio dopo aver incollato il testo.
    >

5. Distribuire questo script a tutti i computer Windows per assicurarsi che, quando si avvia la migrazione dei client, i client non ancora migrati continuino a comunicare con AD RMS, anche se usano contenuto protetto dai client migrati che invece usano il servizio Azure Rights Management.

    Per distribuire questo script è possibile usare Criteri di gruppo o un altro meccanismo di distribuzione software.

## <a name="step-3-prepare-your-exchange-deployment-for-migration"></a>Passaggio 3. Preparare la distribuzione di Exchange per la migrazione

Se si usa Exchange locale o Exchange online, è possibile che Exchange sia stato precedentemente integrato nella distribuzione di AD RMS. In questo passaggio verranno configurati entrambi in modo che usino la configurazione di AD RMS esistente per supportare il contenuto protetto da Azure RMS.

Assicurarsi di avere gli [URL del servizio Azure Rights Management del tenant](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url) in modo che sia possibile sostituire questo valore in *&lt;URL tenant&gt;* nei comandi seguenti.

Eseguire una delle operazioni seguenti, a seconda che sia stato integrato Exchange locale o Exchange Online con AD RMS:

- [Exchange locale integrato con AD RMS](#if-you-have-integrated-exchange-on-premises-with-ad-rms)
- [Exchange Online integrato con AD RMS](#if-you-have-integrated-exchange-online-with-ad-rms)
### <a name="if-you-have-integrated-exchange-online-with-ad-rms"></a>Se Exchange Online è stato integrato con AD RMS

1. Aprire una sessione di PowerShell per Exchange Online.

1. Eseguire i seguenti comandi di PowerShell uno alla volta o in uno script:

    ```PowerShell
    $irmConfig = Get-IRMConfiguration
    $list = $irmConfig.LicensingLocation
    $list += "<YourTenantURL>/_wmcs/licensing"
    Set-IRMConfiguration -LicensingLocation $list
    Set-IRMConfiguration -internallicensingenabled $false
    Set-IRMConfiguration -internallicensingenabled $true 
    ```

### <a name="if-you-have-integrated-exchange-on-premises-with-ad-rms"></a>Se Exchange locale è stato integrato con AD RMS

Per ogni organizzazione di Exchange, aggiungere i valori del registro di sistema in ogni server Exchange, quindi eseguire i comandi di PowerShell:

1. Se si dispone di Exchange 2013 o Exchange 2016, aggiungere il valore del registro di sistema seguente:

    - **Percorso del registro di sistema:**`HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection`

    - **Tipo:** Reg_SZ

    - **Valore:** `https://\<Your Tenant URL\>/_wmcs/licensing`

    - **Dati:**`https://\<AD RMS Extranet Licensing URL\>/_wmcs/licensing`

1. Eseguire i comandi di PowerShell seguenti, uno alla volta o in uno script:

    ```PowerShell
    $irmConfig = Get-IRMConfiguration
    $list = $irmConfig.LicensingLocation
    $list += "<YourTenantURL>/_wmcs/licensing"
    Set-IRMConfiguration -LicensingLocation $list
    Set-IRMConfiguration -internallicensingenabled $false
    Set-IRMConfiguration -RefreshServerCertificates
    Set-IRMConfiguration -internallicensingenabled $true
    IISReset
    ```

Dopo aver eseguito questi comandi per Exchange Online o Exchange locale, se la distribuzione di Exchange è configurata per supportare contenuto protetto da AD RMS, dopo la migrazione supporterà anche contenuto protetto da Azure RMS. 

La distribuzione di Exchange continuerà a usare AD RMS per supportare il contenuto protetto fino a un passaggio successivo nel processo di migrazione.

## <a name="next-steps"></a>Passaggi successivi

Passare a [Fase 2: configurazione lato server](migrate-from-ad-rms-phase2.md).
