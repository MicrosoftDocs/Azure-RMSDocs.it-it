---
# required metadata

title: Migrazione da AD RMS ad Azure Rights Management - Fase 3 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8b039ad5-95a6-4c73-9c22-78c7b0e12cb7


# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Fase 3 della migrazione: configurazione di servizi di supporto

*Si applica a: Active Directory Rights Management Services, Azure Rights Management*


Usare le seguenti informazioni per la fase 3 della migrazione da AD RMS ad Azure Rights Management (Azure RMS). Queste procedure descrivono i passaggi da 6 a 7 di [Migrazione da AD RMS ad Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md).


## Passaggio 6. Configurare l'iterazione IRM per Exchange Online

Se in precedenza si è importato il dominio di pubblicazione trusted da AD RMS a Exchange Online, è necessario rimuovere questo dominio per evitare conflitti di modelli e criteri dopo la migrazione in Azure RMS. A tale scopo, usare il cmdlet [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/en-us/library/jj200720%28v=exchg.150%29.aspx) da Exchange Online.

Se si è scelta una topologia di chiave del tenant di Azure RMS **gestita da Microsoft**:

-   Vedere la sezione [Exchange Online: configurazione di IRM](../deploy-use/configure-office365.md#exchange-online-irm-configuration) nell'articolo [Office 365: configurazione di client e servizi online](../deploy-use/configure-office365.md). Questa sezione include i normali comandi da eseguire per connettersi al servizio Exchange Online, importa la chiave del tenant da Azure RMS e abilita la funzionalità di IRM per Exchange Online. Dopo aver completato questi passaggi, si avrà la funzionalità RMS completa con Exchange Online.

Se si è scelta una topologia di chiave del tenant di Azure RMS **gestita dal cliente (BYOK)**:

-   La funzionalità di RMS con Exchange Online risulterà ridotta, come descritto nell'articolo [Prezzi e restrizioni della modalità BYOK](byok-price-restrictions.md).

## Passaggio 7. Distribuire il connettore RMS
Se è stata usata la funzionalità Information Rights Management (IRM) di Exchange Server o di SharePoint Server con AD RMS, è innanzitutto necessario disabilitare IRM su questi server e rimuovere la configurazione di AD RMS. Distribuire quindi il connettore Rights Management (RMS), che funziona come interfaccia di comunicazione (inoltro) tra i server locali e Azure RMS.

Infine, per questo passaggio, se in Azure RMS sono stati importati più domini di pubblicazione trusted usati per proteggere i messaggi di posta elettronica, è necessario modificare manualmente il Registro di sistema nei computer che eseguono Exchange Server per reindirizzare tutti gli URL dei domini di pubblicazione trusted al connettore RMS.

> [!NOTE]
> Prima di iniziare, verificare le versioni dei server locali supportate da Azure RMS in [Server locali che supportano Azure RMS](../get-started/requirements-servers.md).

### Disabilitare IRM nei computer che eseguono Exchange Server e rimuovere la configurazione di AD RMS

1.  In ogni computer che esegue Exchange Server trovare la cartella seguente ed eliminare tutte le voci che contiene: \ProgramData\Microsoft\DRM\Server\S-1-5-18

2.  In uno dei computer che eseguono Exchange Server usare il cmdlet [Set_IRMConfiguration](http://technet.microsoft.com/library/dd979792.aspx) di Exchange per disabilitare prima di tutto le funzionalità IRM per i messaggi inviati a destinatari interni:

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $false
    ```

3.  Usare quindi lo stesso cmdlet per disabilitare le funzionalità IRM per i messaggi inviati a destinatari esterni:

    ```
    Set-IRMConfiguration -ExternalLicensingEnabled $false
    ```

4.  Si userà poi lo stesso cmdlet per disabilitare IRM in Microsoft Office Outlook Web App e in Microsoft Exchange ActiveSync:

    ```
    Set-IRMConfiguration -ClientAccessServerEnabled $false
    ```

5.  Infine, usare lo stesso cmdlet per cancellare tutti i certificati memorizzati nella cache:

    ```
    Set-IRMConfiguration -RefreshServerCertificates
    ```

6.  In ogni Exchange Server reimpostare IIS, accedendo ad esempio a un prompt dei comandi come amministratore e digitando **iisreset**.

### Disabilitare IRM nei computer che eseguono SharePoint Server e rimuovere la configurazione di AD RMS

1.  Assicurarsi che non ci siano documenti estratti da librerie protetti da RMS. In tal caso, non saranno più accessibili alla fine di questa procedura.

2.  Nel sito Web Amministrazione centrale SharePoint, nella sezione **Avvio veloce** fare clic su **Sicurezza**.

3.  Nella pagina **Sicurezza** nella sezione **Criteri informazioni** fare clic su **Configura Information Rights Management**.

4.  Nella pagina **Information Rights Management** nella sezione **Information Rights Management** selezionare **Non utilizzare IRM in questo server**, quindi fare clic su **OK**.

5.  In ogni computer che esegue SharePoint Server eliminare il contenuto della cartella \ProgramData\Microsoft\MSIPC\Server\*&lt;SID dell'account che esegue SharePoint Server&gt;*.

#### Installare e configurare il connettore RMS

-   Usare le istruzioni riportate in [Distribuzione del connettore di Azure Rights Management](../deploy-use/deploy-rms-connector.md).

#### Solo per Exchange e più domini di pubblicazione trusted: Modificare il Registro di sistema

-   In ogni computer che esegue Exchange Server aggiungere manualmente le chiavi del Registro di sistema seguenti per ogni dominio di pubblicazione trusted aggiuntivo importato, per reindirizzare gli URL dei domini di pubblicazione trusted al connettore RMS. Queste voci del Registro di sistema sono specifiche per la migrazione e non vengono aggiunte dallo strumento di configurazione server per il connettore Microsoft RMS.

    Quando si apportano queste modifiche al Registro di sistema, attenersi alle istruzioni seguenti:

    -   Sostituire *ConnectorFQDN* con il nome definito per il connettore in DNS, Ad esempio, **rmsconnector.contoso.com**.

    -   Usare il prefisso HTTP o HTTPS per l'URL del connettore, a seconda che sia stato configurato per comunicare con i server locali usando HTTP o HTTPS.

Per Exchange 2013 - modifica 1 del Registro di sistema:


**Percorso del Registro di sistema:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection

**Digitare il comando seguente:**

Reg_SZ

**Valore:**

https://<AD RMS Intranet Licensing URL>/_wmcs/licensing

**Dati:**

Uno dei seguenti, in base all'uso del protocollo HTTP o HTTPS per le comunicazioni dal server di Exchange al connettore RMS:

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorName>/_wmcs/licensing


---

Per Exchange 2013 - modifica 2 del Registro di sistema:

**Percorso del Registro di sistema:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v15\IRM\LicenseServerRedirection 


**Digitare il comando seguente:**

Reg_SZ

**Valore:**

https://<AD RMS Extranet Licensing URL>/_wmcs/licensing


**Dati:**

Uno dei seguenti, in base all'uso del protocollo HTTP o HTTPS per le comunicazioni dal server di Exchange al connettore RMS:

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorFQDN>/_wmcs/licensing

---

Per Exchange 2010 - modifica 1 del Registro di sistema:



**Percorso del Registro di sistema:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection

**Digitare il comando seguente:**

Reg_SZ

**Valore:**

https://<AD RMS Intranet Licensing URL>/_wmcs/licensing

**Dati:**

Uno dei seguenti, in base all'uso del protocollo HTTP o HTTPS per le comunicazioni dal server di Exchange al connettore RMS:

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorName>/_wmcs/licensing


---

Per Exchange 2010 - modifica 2 del Registro di sistema:


**Percorso del Registro di sistema:**

HKLM\SOFTWARE\Microsoft\ExchangeServer\v14\IRM\LicenseServerRedirection
 

**Digitare il comando seguente:**

Reg_SZ

**Valore:**

https://<AD RMS Extranet Licensing URL>/_wmcs/licensing


**Dati:**

Uno dei seguenti, in base all'uso del protocollo HTTP o HTTPS per le comunicazioni dal server di Exchange al connettore RMS:

- http://<connectorFQDN>/_wmcs/licensing

- https://<connectorFQDN>/_wmcs/licensing

---

Dopo aver completato queste procedure, si è pronti a passare alla sezione **Passaggi successivi** dell'articolo [Distribuzione del connettore di Azure Rights Management](../deploy-use/deploy-rms-connector.md).

## Passaggi successivi
Per continuare la migrazione, passare a [Fase 4: attività post-migrazione](migrate-from-ad-rms-phase4.md).

<!--HONumber=Apr16_HO4-->


