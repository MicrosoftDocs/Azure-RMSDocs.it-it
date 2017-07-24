---
title: 'Eseguire la migrazione da AD RMS ad Azure Information Protection: Fase 4'
description: Fase 4 della migrazione da AD RMS ad Azure Information Protection che include i passaggi 8 e 9 della migrazione da AD RMS ad Azure Information Protection
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/18/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8b039ad5-95a6-4c73-9c22-78c7b0e12cb7
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 6c93f38b0ae725c1bc1d3423baf64931593af3b7
ms.sourcegitcommit: 64ba794e7844a74b1e25db0d44b90060e3ae1468
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2017
---
# <a name="migration-phase-4---supporting-services-configuration"></a>Fase 4 della migrazione: configurazione dei servizi di supporto

>*Si applica a: Active Directory Rights Management Services, Azure Information Protection, Office 365*


Usare le informazioni seguenti per la fase 4 della migrazione da AD RMS ad Azure Information Protection. Di seguito vengono illustrati i passaggi 8 e 9 dell'operazione descritta in [Migrazione da AD RMS ad Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).



## <a name="step-8-configure-irm-integration-for-exchange-online"></a>Passaggio 8. Configurare l'iterazione IRM per Exchange Online

Se in precedenza si è importato il dominio di pubblicazione trusted da AD RMS ad Exchange Online, è necessario rimuovere questo dominio per evitare conflitti di modelli e criteri dopo la migrazione ad Azure Information Protection. A tale scopo, usare il cmdlet [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx) da Exchange Online.

Se si è scelta una topologia di chiave del tenant di Azure Information Protection **gestita da Microsoft**:

1. Usare le istruzioni nella sezione [Exchange Online: configurazione di IRM](../deploy-use/configure-office365.md#exchange-online-irm-configuration) dell'articolo [Office 365: configurazione di client e servizi online](../deploy-use/configure-office365.md). Questa sezione include i normali comandi da eseguire per connettersi al servizio Exchange Online, importa la chiave del tenant da Azure Information Protection e abilita la funzionalità di IRM per Exchange Online. Al termine di questi passaggi, si disporrà della funzionalità di protezione Azure Rights Management completa con Exchange Online.

2. Oltre alla configurazione standard per abilitare IRM per Exchange Online, eseguire i comandi di PowerShell seguenti per assicurarsi che gli utenti saranno in grado di leggere i messaggi di posta elettronica inviati con la protezione di AD RMS.

    Sostituire *\<dominio.impresa>* con il nome di dominio dell'organizzazione.

        $irmConfig = Get-IRMConfiguration
        $list = $irmConfig.LicensingLocation
        $list += "https://adrms.<yourcompany.domain>/_wmcs/licensing"
        Set-IRMConfiguration -LicensingLocation $list
        Set-IRMConfiguration -internallicensingenabled $false
        Set-IRMConfiguration -internallicensingenabled $true


Se si è scelta una topologia di chiave del tenant di Azure Information Protection **gestita dal cliente (BYOK)**:

-   La funzionalità di protezione Rights Management con Exchange Online sarà ridotta, come descritto nell'articolo [Prezzi e restrizioni della modalità BYOK](byok-price-restrictions.md).


## <a name="step-9-configure-irm-integration-for-exchange-server-and-sharepoint-server"></a>Passaggio 9. Configurare l'integrazione IRM per Exchange Server e SharePoint Server

Se è stata usata la funzionalità Information Rights Management (IRM) di Exchange Server o di SharePoint Server con AD RMS, è necessario distribuire il connettore di Rights Management (RMS), che funge da interfaccia di comunicazione (relè) tra i server locali e il servizio di protezione per Azure Information Protection.

Questa procedura esegue l'installazione e la configurazione del connettore, disabilita IRM per Exchange e SharePoint e configura i server per l'uso del connettore. Infine, se in Azure Information Protection sono stati importati file di configurazione di dati di AD RMS (con estensione xml) usati per proteggere i messaggi di posta elettronica, è necessario modificare manualmente il Registro di sistema nei computer in cui viene eseguito Exchange Server per reindirizzare tutti gli URL dei domini di pubblicazione trusted al connettore RMS.

> [!NOTE]
> Prima di iniziare, verificare le versioni dei server locali supportate dal servizio Azure Rights Management in [Server locali che supportano Azure RMS](../get-started/requirements-servers.md).

### <a name="install-and-configure-the-rms-connector"></a>Installare e configurare il connettore RMS

Usare le istruzioni incluse nell'articolo [Distribuzione del connettore di Azure Rights Management](../deploy-use/deploy-rms-connector.md) ed eseguire i passaggi da 1 a 4. Non eseguire ancora il passaggio 5 delle istruzioni del connettore. 

### <a name="disable-irm-on-exchange-servers-and-remove-ad-rms-configuration"></a>Disabilitare IRM nei computer che eseguono Exchange Server e rimuovere la configurazione di AD RMS

1.  In ogni Exchange Server trovare la cartella seguente ed eliminare tutte le voci incluse: **\ProgramData\Microsoft\DRM\Server\S-1-5-18**

2. Da uno dei server Exchange, eseguire i comandi di PowerShell seguenti per assicurarsi che gli utenti saranno in grado di leggere i messaggi di posta elettronica protetti con Azure Rights Management.

    Prima di eseguire questi comandi, sostituire *\<URL tenant>* con l'URL del servizio Azure Rights Management della propria organizzazione.

        $irmConfig = Get-IRMConfiguration
        $list = $irmConfig.LicensingLocation 
        $list += "<Your Tenant URL>/_wmcs/licensing"
        Set-IRMConfiguration -LicensingLocation $list

3.  Disattivare ora le funzionalità IRM per i messaggi inviati a destinatari interni:

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

4. Usare quindi lo stesso cmdlet per disabilitare IRM in Microsoft Office Outlook Web App e in Microsoft Exchange ActiveSync:

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

5.  In ogni computer che esegue SharePoint Server eliminare il contenuto della cartella \ProgramData\Microsoft\MSIPC\Server\\<*SID dell'account che esegue SharePoint Server>*.

### <a name="configure-exchange-and-sharepoint-to-use-the-connector"></a>Configurare Exchange e SharePoint per l'uso del connettore

1. Tornare alle istruzioni per la distribuzione del connettore RMS: [Passaggio 5: configurazione dei server per l'uso del connettore RMS](../deploy-use/configure-servers-rms-connector.md)

    Se è installato solo SharePoint Server, andare direttamente ai [passaggi successivi](#next-steps) per continuare la migrazione. 

2. In ogni Exchange Server aggiungere manualmente le chiavi del Registro di sistema nella sezione successiva per ogni file di dati di configurazione (con estensione xml) importato per reindirizzare gli URL dei domini di pubblicazione trusted al connettore RMS. Queste voci del Registro di sistema sono specifiche per la migrazione e non vengono aggiunte dallo strumento di configurazione server per il connettore Microsoft RMS.

    Quando si apportano queste modifiche al Registro di sistema, attenersi alle istruzioni seguenti:

    -   Sostituire *nome di dominio completo del connettore* con il nome definito per il connettore in DNS, ad esempio **rmsconnector.contoso.com**.

    -   Usare il prefisso HTTP o HTTPS per l'URL del connettore, a seconda che sia stato configurato per comunicare con i server locali usando HTTP o HTTPS.

#### <a name="registry-edits-for-exchange"></a>Modifiche al Registro di sistema per Exchange

In tutti i server Exchange, rimuovere i valori del Registro di sistema aggiunti per LicenseServerRedirection durante la fase di preparazione. Questi valori sono stati aggiunti nei percorsi seguenti:

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection


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

Per Exchange 2013 - modifica 2 del Registro di sistema:

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

[!INCLUDE[Commenting house rules](../includes/houserules.md)]