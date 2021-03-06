---
title: 'Eseguire la migrazione da AD RMS ad Azure Information Protection: Fase 4'
description: Fase 4 della migrazione da AD RMS ad Azure Information Protection che include i passaggi 8 e 9 della migrazione da AD RMS ad Azure Information Protection
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8b039ad5-95a6-4c73-9c22-78c7b0e12cb7
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 0b13ccec5c4ca4fcdad1ac145a289a727fddd38a
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97382021"
---
# <a name="migration-phase-4---supporting-services-configuration"></a>Fase 4 della migrazione: configurazione dei servizi di supporto

>***Si applica a**: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Pertinente per**: [AIP Unified Labeling client e client classico](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Usare le informazioni seguenti per la fase 4 della migrazione da AD RMS ad Azure Information Protection. Di seguito vengono illustrati i passaggi 8 e 9 dell'operazione descritta in [Migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

## <a name="step-8-configure-irm-integration-for-exchange-online"></a>Passaggio 8. Configurare l'iterazione IRM per Exchange Online

> [!IMPORTANT]
> Non è possibile controllare quali destinatari migrati utenti possono selezionare per i messaggi di posta elettronica protetti.
>
> Assicurarsi pertanto che tutti gli utenti e i gruppi abilitati alla posta dell'organizzazione dispongano di un account in Azure AD utilizzabile con Azure Information Protection.
>
> Per altre informazioni, vedere [Preparazione di utenti e gruppi per Azure Information Protection](prepare.md).

Indipendentemente dalla topologia della chiave del tenant Azure Information Protection scelta, procedere come segue:

1. **Prerequisito**: affinché Exchange Online sia in grado di decrittografare i messaggi di posta elettronica protetti da ad RMS, è necessario che l'URL del ad RMS per il cluster corrisponda alla chiave disponibile nel tenant. 

    Questa operazione viene eseguita con il record DNS SRV per il cluster di AD RMS che viene usato anche per riconfigurare i client di Office per l'uso di Azure Information Protection. 

    Se non è stato creato il record DNS SRV per la riconfigurazione client nel [passaggio 7](migrate-from-ad-rms-phase3.md#step-7-reconfigure-windows-computers-to-use-azure-information-protection), creare questo record ora per supportare Exchange Online. [Istruzioni](migrate-from-ad-rms-phase3.md#client-reconfiguration-by-using-dns-redirection)
    
    Quando questo record DNS è applicato, gli utenti che usano Outlook nei client di posta elettronica Web e per dispositivi mobili potranno visualizzare i messaggi di posta elettronica protetti da AD RMS in tali app ed Exchange potrà usare la chiave importata da AD RMS per decrittografare, indicizzare, registrare e proteggere il contenuto protetto da AD RMS.  

1. **Eseguire il comando [Get-IRMConfiguration](/powershell/module/exchange/get-irmconfiguration) di Exchange Online.** 

    Se occorre assistenza per l'esecuzione di questo comando, vedere le istruzioni dettagliate in [Exchange Online: configurazione di IRM](configure-office365.md#exchangeonline-irm-configuration).
    
    Nell'output controllare se il parametro **AzureRMSLicensingEnabled** è impostato su **True**:
    
    - Se **AzureRMSLicensingEnabled** è impostato su **true**, non è necessaria alcuna configurazione aggiuntiva per questo passaggio. 
    
    - Se **AzureRMSLicensingEnabled** è impostato su **false**, eseguire `Set-IRMConfiguration -AzureRMSLicensingEnabled $true` e confermare che Exchange Online è ora pronto per l'uso del servizio Azure Rights Management. 
    
        Per ulteriori informazioni, vedere i passaggi di verifica da [configurare nuove funzionalità di crittografia dei messaggi Microsoft 365 basate su Azure Information Protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e).

## <a name="step-9-configure-irm-integration-for-exchange-server-and-sharepoint-server"></a>Passaggio 9. Configurare l'integrazione IRM per Exchange Server e SharePoint Server

Se è stata usata la funzionalità Information Rights Management (IRM) di Exchange Server o di SharePoint Server con AD RMS, sarà necessario distribuire il connettore Rights Management (RMS).

Il connettore funge da interfaccia di comunicazione (inoltro) tra i server locali e il servizio di protezione per Azure Information Protection.

Questa procedura esegue l'installazione e la configurazione del connettore, disabilita IRM per Exchange e SharePoint e configura i server per l'uso del connettore. 

Infine, se sono stati importati AD RMS file di configurazione dei dati con estensione XML usati per proteggere i messaggi di posta elettronica in Azure Information Protection, è necessario modificare manualmente il registro di sistema nei computer Exchange Server per reindirizzare tutti gli URL del dominio di pubblicazione trusted al connettore RMS.

> [!NOTE]
> Prima di iniziare, verificare le versioni dei server locali supportate dal servizio Azure Rights Management in [Server locali che supportano Azure RMS](requirements.md#supported-on-premises-servers-for-azure-rights-management-data-protection).

### <a name="install-and-configure-the-rms-connector"></a>Installare e configurare il connettore RMS

Usare le istruzioni riportate nell'articolo [distribuzione del connettore Azure Rights Management](./deploy-rms-connector.md) ed eseguire i passaggi da 1 a 4. 

Non eseguire ancora il passaggio 5 delle istruzioni del connettore.

### <a name="disable-irm-on-exchange-servers-and-remove-ad-rms-configuration"></a>Disabilitare IRM nei computer che eseguono Exchange Server e rimuovere la configurazione di AD RMS

> [!IMPORTANT]
> Se IRM non è stato ancora configurato su uno dei server Exchange, eseguire solo i passaggi 2 e 6.
> 
> Eseguire tutti questi passaggi se tutti gli URL di gestione licenze di tutti i cluster di AD RMS non vengono visualizzati nel parametro *LicensingLocation* quando si esegue [Get-IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/get-irmconfiguration).

1. In ogni Exchange Server individuare la cartella seguente ed eliminare tutte le voci nella cartella: **\programdata\microsoft\drm\server\s-1-5-18**

2. Da uno dei server Exchange, eseguire i comandi di PowerShell seguenti per assicurarsi che gli utenti saranno in grado di leggere i messaggi di posta elettronica protetti con Azure Rights Management.

    Prima di eseguire questi comandi, sostituire con l'URL del servizio Rights Management di Azure *\<Your Tenant URL>* .

    ```PowerShell
    $irmConfig = Get-IRMConfiguration
    $list = $irmConfig.LicensingLocation 
    $list += "<Your Tenant URL>/_wmcs/licensing"
    Set-IRMConfiguration -LicensingLocation $list
    ```

    A questo punto, quando si esegue [Get-IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/get-irmconfiguration), verranno visualizzati tutti gli URL di licenze del cluster ad RMS e l'URL del servizio Rights Management di Azure visualizzato per il parametro *LicensingLocation* .

3.  Disattivare ora le funzionalità IRM per i messaggi inviati a destinatari interni:

    ```PowerShell
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

4. Usare quindi lo stesso cmdlet per disabilitare IRM in Microsoft Office Outlook Web App e in Microsoft Exchange ActiveSync:

    ```PowerShell
    Set-IRMConfiguration -ClientAccessServerEnabled $false
    ```

5.  Infine, usare lo stesso cmdlet per cancellare tutti i certificati memorizzati nella cache:

    ```PowerShell
    Set-IRMConfiguration -RefreshServerCertificates
    ```

6.  A questo punto, in ogni computer che esegue Exchange Server reimpostare IIS, accedendo ad esempio a un prompt dei comandi come amministratore e digitando **iisreset**.

### <a name="disable-irm-on-sharepoint-servers-and-remove-ad-rms-configuration"></a>Disabilitare IRM nei computer che eseguono SharePoint Server e rimuovere la configurazione di AD RMS

1.  Assicurarsi che non ci siano documenti estratti da librerie protetti da RMS. In tal caso, non saranno più accessibili alla fine di questa procedura.

2.  Nel sito Web di Amministrazione centrale SharePoint, nella sezione **Avvio veloce** fare clic su **Sicurezza**.

3.  Nella pagina **Sicurezza**, nella sezione **Criteri informazioni** fare clic su **Configura Information Rights Management**.

4.  Nella sezione **Information Rights Management** della pagina **Information Rights Management** selezionare **Non utilizzare IRM in questo server**, quindi fare clic su **OK**.

5.  In ognuno dei computer server SharePoint eliminare il contenuto della cartella \programdata\microsoft\msipc\server\ \\ < *SID dell'account che esegue SharePoint Server>*.

### <a name="configure-exchange-and-sharepoint-to-use-the-connector"></a>Configurare Exchange e SharePoint per l'uso del connettore

1. Tornare alle istruzioni per la distribuzione del connettore RMS: [Passaggio 5: configurazione dei server per l'uso del connettore RMS](./configure-servers-rms-connector.md)

    Se è installato solo SharePoint Server, andare direttamente ai [passaggi successivi](#next-steps) per continuare la migrazione. 

2. In ogni Exchange Server aggiungere manualmente le chiavi del Registro di sistema nella sezione successiva per ogni file di dati di configurazione (con estensione xml) importato per reindirizzare gli URL dei domini di pubblicazione trusted al connettore RMS. Queste voci del Registro di sistema sono specifiche per la migrazione e non vengono aggiunte dallo strumento di configurazione server per il connettore Microsoft RMS.

    Quando si apportano queste modifiche al Registro di sistema, attenersi alle istruzioni seguenti:

    -   Sostituire *nome di dominio completo del connettore* con il nome definito per il connettore in DNS, ad esempio **rmsconnector.contoso.com**.

    -   Usare il prefisso HTTP o HTTPS per l'URL del connettore, a seconda che sia stato configurato per comunicare con i server locali usando HTTP o HTTPS.

#### <a name="registry-edits-for-exchange"></a>Modifiche al Registro di sistema per Exchange

Per tutti i server di Exchange, aggiungere i valori del Registro di sistema seguenti a LicenseServerRedirection, a seconda delle versioni di Exchange:

1. Per **exchange 2013 ed exchange 2016**, aggiungere il valore del registro di sistema seguente:

    - **Percorso del registro di sistema**: `HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection`

    - **Tipo**: REG_SZ

    - **Valore**: `https://\<AD RMS Intranet Licensing URL\>/_wmcs/licensing`

    - **Data**: uno dei seguenti, a seconda che si usi http o HTTPS da Exchange Server al connettore RMS:

        - `http://\<connector FQDN\>/_wmcs/licensing`
        
        - `https://\<connector FQDN\>/_wmcs/licensing`

1. Per Exchange 2013, aggiungere il seguente valore del registro di sistema aggiuntivo:

    - **Percorso del registro di sistema**: `HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection` 

    - **Tipo**: REG_SZ

    - **Valore**: https:// \<AD RMS Extranet Licensing URL\> /_wmcs/licensing

    - **Data**: uno dei seguenti, a seconda che si usi http o HTTPS da Exchange Server al connettore RMS:

        - `http://\<connector FQDN\>/_wmcs/licensing`

        - `https://\<connector FQDN\>/_wmcs/licensing`

## <a name="next-steps"></a>Passaggi successivi
Per continuare la migrazione, passare a [Fase 5: attività post-migrazione](migrate-from-ad-rms-phase5.md).