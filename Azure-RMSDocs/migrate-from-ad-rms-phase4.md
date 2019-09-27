---
title: 'Eseguire la migrazione da AD RMS ad Azure Information Protection: Fase 4'
description: Fase 4 della migrazione da AD RMS ad Azure Information Protection che include i passaggi 8 e 9 della migrazione da AD RMS ad Azure Information Protection
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/09/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8b039ad5-95a6-4c73-9c22-78c7b0e12cb7
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 1ef0421c63489e8cd0706a77001ba611a929d1b1
ms.sourcegitcommit: a091cabd5ad24b4534b5f69f029843037c7872d3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71314377"
---
# <a name="migration-phase-4---supporting-services-configuration"></a>Fase 4 della migrazione: configurazione dei servizi di supporto

>*Si applica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Usare le informazioni seguenti per la fase 4 della migrazione da AD RMS ad Azure Information Protection. Di seguito vengono illustrati i passaggi 8 e 9 dell'operazione descritta in [Migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

## <a name="step-8-configure-irm-integration-for-exchange-online"></a>Passaggio 8. Configurare l'iterazione IRM per Exchange Online

> [!IMPORTANT]
> Poiché non è possibile controllare i destinatari che gli utenti di cui è stata eseguita la migrazione potrebbero selezionare per i messaggi di posta elettronica protetti, verificare che tutti gli utenti e i gruppi abilitati alla posta elettronica all'interno dell'organizzazione dispongano di un account in Azure AD che possa essere usato con Azure Information Protection. [Altre informazioni](prepare.md)

Indipendentemente dalla topologia di chiave del tenant di Azure Information Protection scelta, eseguire le operazioni seguenti:

1. Per decrittografare i messaggi di posta elettronica protetti da AD RMS, Exchange Online deve sapere che l'URL di AD RMS per il cluster corrisponde alla chiave disponibile nel tenant. Questa operazione viene eseguita con il record DNS SRV per il cluster di AD RMS che viene usato anche per riconfigurare i client di Office per l'uso di Azure Information Protection. Se non è stato creato il record DNS SRV per la riconfigurazione dei client nel passaggio 7, è possibile creare ora questo record per il supporto di Exchange Online. [Istruzioni](migrate-from-ad-rms-phase3.md#client-reconfiguration-by-using-dns-redirection)
    
    Quando questo record DNS è applicato, gli utenti che usano Outlook nei client di posta elettronica Web e per dispositivi mobili potranno visualizzare i messaggi di posta elettronica protetti da AD RMS in tali app ed Exchange potrà usare la chiave importata da AD RMS per decrittografare, indicizzare, registrare e proteggere il contenuto protetto da AD RMS.  

2. Eseguire il comando di Exchange Online [Get-IRMConfiguration](https://technet.microsoft.com/library/dd776120(v=exchg.160).aspx). Se occorre assistenza per l'esecuzione di questo comando, vedere le istruzioni dettagliate in [Exchange Online: configurazione di IRM](configure-office365.md#exchangeonline-irm-configuration).
    
    Nell'output controllare se il parametro **AzureRMSLicensingEnabled** è impostato su **True**:
    
    - Se AzureRMSLicensingEnabled è impostato su **True**, non è necessaria alcuna configurazione aggiuntiva per questo passaggio. 
    
    - Se AzureRMSLicensingEnabled è impostato su **False**, eseguire `Set-IRMConfiguration -AzureRMSLicensingEnabled $true` e quindi seguire i passaggi per la verifica descritti in [Set up new Office 365 Message Encryption capabilities built on top of Azure Information Protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e) (Impostare le nuove funzionalità di Office 365 Message Encryption basate su Azure Information Protection) per verificare che Exchange Online sia pronto per usare il servizio Azure Rights Management. 

## <a name="step-9-configure-irm-integration-for-exchange-server-and-sharepoint-server"></a>Passaggio 9. Configurare l'integrazione IRM per Exchange Server e SharePoint Server

Se è stata usata la funzionalità Information Rights Management (IRM) di Exchange Server o di SharePoint Server con AD RMS, è necessario distribuire il connettore di Rights Management (RMS), che funge da interfaccia di comunicazione (inoltro) tra i server locali e il servizio di protezione per Azure Information Protection.

Questa procedura esegue l'installazione e la configurazione del connettore, disabilita IRM per Exchange e SharePoint e configura i server per l'uso del connettore. Infine, se in Azure Information Protection sono stati importati file di configurazione di dati di AD RMS (con estensione xml) usati per proteggere i messaggi di posta elettronica, è necessario modificare manualmente il Registro di sistema nei computer in cui viene eseguito Exchange Server per reindirizzare tutti gli URL dei domini di pubblicazione trusted al connettore RMS.

> [!NOTE]
> Prima di iniziare, verificare le versioni dei server locali supportate dal servizio Azure Rights Management in [Server locali che supportano Azure RMS](./requirements-servers.md).

### <a name="install-and-configure-the-rms-connector"></a>Installare e configurare il connettore RMS

Usare le istruzioni incluse nell'articolo [Distribuzione del connettore di Azure Rights Management](./deploy-rms-connector.md) ed eseguire i passaggi da 1 a 4. Non eseguire ancora il passaggio 5 delle istruzioni del connettore.

### <a name="disable-irm-on-exchange-servers-and-remove-ad-rms-configuration"></a>Disabilitare IRM nei computer che eseguono Exchange Server e rimuovere la configurazione di AD RMS

> [!IMPORTANT]
> Se IRM non è stato ancora configurato su uno dei server Exchange, eseguire solo i passaggi 2 e 6.
> 
> Eseguire tutti questi passaggi se tutti gli URL di gestione licenze di tutti i cluster di AD RMS non vengono visualizzati nel parametro *LicensingLocation* quando si esegue [Get-IRMConfiguration](https://docs.microsoft.com/powershell/module/exchange/encryption-and-certificates/get-irmconfiguration?view=exchange-ps).

1. In ogni Exchange Server trovare la cartella seguente ed eliminare tutte le voci incluse: **\ProgramData\Microsoft\DRM\Server\S-1-5-18**

2. Da uno dei server Exchange, eseguire i comandi di PowerShell seguenti per assicurarsi che gli utenti saranno in grado di leggere i messaggi di posta elettronica protetti con Azure Rights Management.

    Prima di eseguire questi comandi, sostituire *\<URL tenant>* con l'URL del servizio Azure Rights Management della propria organizzazione.

        $irmConfig = Get-IRMConfiguration
        $list = $irmConfig.LicensingLocation 
        $list += "<Your Tenant URL>/_wmcs/licensing"
        Set-IRMConfiguration -LicensingLocation $list
    
    A questo punto, quando si esegue [Get-IRMConfiguration](https://docs.microsoft.com/powershell/module/exchange/encryption-and-certificates/get-irmconfiguration?view=exchange-ps), verranno visualizzati tutti gli URL di licenze del cluster ad RMS e l'URL del servizio Rights Management di Azure visualizzato per il parametro *LicensingLocation* .

3.  Disattivare ora le funzionalità IRM per i messaggi inviati a destinatari interni:

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

4. Usare quindi lo stesso cmdlet per disabilitare IRM in Microsoft Office Outlook Web App e in Microsoft Exchange ActiveSync:

    ```
    Set-IRMConfiguration -ClientAccessServerEnabled $false
    ```

5.  Infine, usare lo stesso cmdlet per cancellare tutti i certificati memorizzati nella cache:

    ```
    Set-IRMConfiguration -RefreshServerCertificates
    ```

6.  A questo punto, in ogni computer che esegue Exchange Server reimpostare IIS, accedendo ad esempio a un prompt dei comandi come amministratore e digitando **iisreset**.

### <a name="disable-irm-on-sharepoint-servers-and-remove-ad-rms-configuration"></a>Disabilitare IRM nei computer che eseguono SharePoint Server e rimuovere la configurazione di AD RMS

1.  Assicurarsi che non ci siano documenti estratti da librerie protetti da RMS. In tal caso, non saranno più accessibili alla fine di questa procedura.

2.  Nel sito Web di Amministrazione centrale SharePoint, nella sezione **Avvio veloce** fare clic su **Sicurezza**.

3.  Nella pagina **Sicurezza** , nella sezione **Criteri informazioni** fare clic su **Configura Information Rights Management**.

4.  Nella pagina **Information Rights Management** , nella sezione **Information Rights Management** selezionare **Non utilizzare IRM in questo server**, quindi fare clic su **OK**.

5.  In ogni computer che esegue SharePoint Server eliminare il contenuto della cartella \ProgramData\Microsoft\MSIPC\Server\\<*SID dell'account che esegue SharePoint Server>* .

### <a name="configure-exchange-and-sharepoint-to-use-the-connector"></a>Configurare Exchange e SharePoint per l'uso del connettore

1. Tornare alle istruzioni per la distribuzione del connettore RMS: [Passaggio 5: Configurazione dei server per l'uso del connettore RMS](./configure-servers-rms-connector.md)

    Se è installato solo SharePoint Server, andare direttamente ai [passaggi successivi](#next-steps) per continuare la migrazione. 

2. In ogni Exchange Server aggiungere manualmente le chiavi del Registro di sistema nella sezione successiva per ogni file di dati di configurazione (con estensione xml) importato per reindirizzare gli URL dei domini di pubblicazione trusted al connettore RMS. Queste voci del Registro di sistema sono specifiche per la migrazione e non vengono aggiunte dallo strumento di configurazione server per il connettore Microsoft RMS.

    Quando si apportano queste modifiche al Registro di sistema, attenersi alle istruzioni seguenti:

    -   Sostituire *nome di dominio completo del connettore* con il nome definito per il connettore in DNS, ad esempio **rmsconnector.contoso.com**.

    -   Usare il prefisso HTTP o HTTPS per l'URL del connettore, a seconda che sia stato configurato per comunicare con i server locali usando HTTP o HTTPS.

#### <a name="registry-edits-for-exchange"></a>Modifiche al Registro di sistema per Exchange

Per tutti i server di Exchange, aggiungere i valori del Registro di sistema seguenti a LicenseServerRedirection, a seconda delle versioni di Exchange:

---

Per Exchange 2013 ed Exchange 2016: modifica 1 del Registro di sistema:


**Percorso del Registro di sistema:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**Tipo:** Reg_SZ

**Valore:** https://\<URL di gestione licenze Intranet AD RMS\>/_wmcs/licensing

**Dati:**

Uno dei seguenti, in base all'uso del protocollo HTTP o HTTPS per le comunicazioni dal server di Exchange al connettore RMS:

- http://\<nome di dominio completo del connettore\>/_wmcs/licensing

- https://\<nome di dominio completo del connettore\>/_wmcs/licensing


---

Exchange 2013 - modifica 2 del Registro di sistema:

**Percorso del Registro di sistema:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection 

**Tipo:** Reg_SZ

**Valore:** https://\<URL di gestione licenze Extranet AD RMS\>/_wmcs/licensing

**Dati:**

Uno dei seguenti, in base all'uso del protocollo HTTP o HTTPS per le comunicazioni dal server di Exchange al connettore RMS:

- http://\<nome di dominio completo del connettore\>/_wmcs/licensing

- https://\<nome di dominio completo del connettore\>/_wmcs/licensing

---

Per Exchange 2010 - modifica 1 del Registro di sistema:


**Percorso del Registro di sistema:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**Tipo:** Reg_SZ

**Valore:** https://\<URL di gestione licenze Intranet AD RMS\>/_wmcs/licensing

**Dati:**

Uno dei seguenti, in base all'uso del protocollo HTTP o HTTPS per le comunicazioni dal server di Exchange al connettore RMS:

- http://\<nome di dominio completo del connettore\>/_wmcs/licensing

- https://\<nome connettore\>/_wmcs/licensing


---

Per Exchange 2010 - modifica 2 del Registro di sistema:


**Percorso del Registro di sistema:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**Tipo:** Reg_SZ

**Valore:** https://\<URL di gestione licenze Extranet AD RMS\>/_wmcs/licensing

**Dati:**

Uno dei seguenti, in base all'uso del protocollo HTTP o HTTPS per le comunicazioni dal server di Exchange al connettore RMS:

- http://\<nome di dominio completo del connettore\>/_wmcs/licensing

- https://\<nome di dominio completo del connettore\>/_wmcs/licensing

---


## <a name="next-steps"></a>Passaggi successivi
Per continuare la migrazione, passare a [Fase 5: attività post-migrazione](migrate-from-ad-rms-phase5.md).
