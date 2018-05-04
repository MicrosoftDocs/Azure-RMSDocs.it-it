---
title: Configurare IRM di Exchange Online per il servizio Azure Rights Management da Azure Information Protection
description: Informazioni e istruzioni per gli amministratori per la configurazione di Exchange Online per il servizio Azure Rights Management nel caso in cui il tenant di Office 365 non supporti le nuove funzionalità di Office 365 Message Encryption.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/11/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ''
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: e452f5ac4e3297106a54a2034d64f57d8f6d5302
ms.sourcegitcommit: affda7572064edaf9e3b63d88f4a18d0d6932b13
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2018
---
# <a name="exchange-online-irm-configuration-to-import-a-trusted-publishing-domain"></a>Configurazione di IRM di Exchange Online per l'importazione di un dominio di pubblicazione trusted

>*Si applica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Usare queste istruzioni solo se il tenant non è in grado di usare le nuove funzionalità di Office 365 Message Encryption. Per verificare, eseguire il comando [Get-IRMConfiguration](https://technet.microsoft.com/library/dd776120(v=exchg.160\).aspx) di Exchange Online e verificare se è presente un parametro **AzureRMSLicensingEnabled**. Se viene visualizzato questo parametro, il tenant può usare le nuove funzionalità di Office 365 Message Encryption:

- Se **AzureRMSLicensingEnabled** è impostato su **True**, il tenant sta già usando le nuove funzionalità di Office 365 Message Encryption e non è necessario seguire le istruzioni nella sezione successiva.

- Se **AzureRMSLicensingEnabled** è impostato su **False**, il tenant supporta le nuove funzionalità di Office 365 Message Encryption, ma non è ancora configurato per farlo. Per configurare il tenant per le nuove funzionalità, vedere [Set up new Office 365 Message Encryption capabilities built on top of Azure Information Protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e) (Impostare le nuove funzionalità di Office 365 Message Encryption basate su Azure Information Protection). 

Solo se il tenant non può supportare le nuove funzionalità di Office 365 Message Encryption, usare le istruzioni seguenti.

## <a name="exchange-online-irm-configuration"></a>Configurazione di IRM di Exchange Online

Per configurare IRM di Exchange Online si può usare Windows PowerShell (senza bisogno di installare un modulo separato) ed eseguire i [comandi PowerShell per Exchange Online](https://technet.microsoft.com/library/jj200677.aspx).

> [!NOTE]
> Fino a quando non viene eseguita la migrazione del tenant di Office 365 da parte di Microsoft per il supporto delle nuove funzionalità, non è possibile configurare Exchange Online per il supporto del servizio Azure Rights Management se si usa una chiave del tenant gestita dal cliente (BYOK) per Azure Information Protection anziché la configurazione predefinita di una chiave del tenant gestita da Microsoft.
>
> Se si prova a configurare Exchange Online quando il servizio Azure Rights Management usa BYOK, il comando per l'importazione della chiave (passaggio 5, nella procedura seguente) avrà esito negativo con messaggio di errore **[FailureCategory=Cmdlet-FailedToGetTrustedPublishingDomainFromRmsOnlineException]**.

I passaggi seguenti offrono un set tipico di comandi da eseguire per abilitare IRM di Exchange Online:

1.  Se questa è la prima volta che si usa Windows PowerShell per Exchange Online nel computer, sarà necessario configurare Windows PowerShell per l'esecuzione degli script firmati. Avviare la sessione di Windows PowerShell usando l'opzione **Esegui come amministratore** e quindi digitare:

    ```
    Set-ExecutionPolicy RemoteSigned
    ```

2.  Nella sessione di Windows PowerShell accedere a Exchange Online usando un account abilitato per l'accesso alla shell remota. Per impostazione predefinita, tutti gli account creati in Exchange Online sono abilitati per l'accesso alla Shell remota. L'accesso può essere disabilitato o abilitato usando il comando [Set-User &lt;UserIdentity&gt; -RemotePowerShellEnabled](https://technet.microsoft.com/library/jj984292%28v=exchg.160%29.aspx).

    Per accedere, digitare quanto segue:

    ```
    $UserCredential = Get-Credential
    ```
    Nella finestra di dialogo **Richiesta credenziali di Windows PowerShell** specificare il nome utente e la password di Office 365.

3.  Connettersi al servizio Exchange Online eseguendo i due comandi seguenti:

    ```
    $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection
    ```

    ```
    Import-PSSession $Session
    ```

4.  Specificare la posizione della chiave del tenant di Azure Information Protection, in base alla posizione in cui è stato creato il tenant dell'organizzazione:

    America del Nord

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.na.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    Europa

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.eu.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    Asia

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.ap.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    Per l'America meridionale:

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.sa.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    Per Office 365 Government (Government Community Cloud):

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.govus.aadrm.com/TenantManagement/ServicePartner.svc"
    ```

5.  Importare i dati di configurazione dal servizio Azure Rights Management a Exchange Online, sotto forma di dominio di pubblicazione trusted. I dati includono la chiave del tenant di Azure Information Protection e i modelli di Azure Rights Management:

    ```
    Import-RMSTrustedPublishingDomain -RMSOnline -name "RMS Online"
    ```
    In questo comando è stato usato il nome **RMS Online** come nome base del dominio di pubblicazione trusted per Azure Rights Management in Exchange Online. Dopo aver importato il dominio di pubblicazione trusted, viene denominato **RMS Online - 1** in Exchange Online.

6.  Abilitare Azure Rights Management in modo che le funzionalità di IRM siano disponibili per Exchange Online:

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $true
    ```
    Dopo aver eseguito questo comando, Rights Management viene automaticamente abilitato per il client di Outlook, Outlook Web app e Exchange Active Sync.

7.  Facoltativamente, verificare che la configurazione sia riuscita con il comando seguente:

    ```
    Test-IRMConfiguration -Sender <user email address>
    ```
    Ad esempio: **Test-IRMConfiguration -Sender  adams@contoso.com**

    Questo comando esegue una serie di controlli, inclusi la verifica della connettività al servizio, il recupero della configurazione, il recupero di URI, licenze ed eventuali modelli. Nella sessione di Windows PowerShell verranno visualizzati i risultati di ogni controllo e, se tutti gli elementi superano positivamente i controlli, verrà visualizzato un messaggio analogo a: **RISULTATO COMPLESSIVO: ESITO POSITIVO**

8.  Disconnettersi dalla sessione remota di PowerShell:

    ```
    Remove-PSSession $Session
    ```

Gli utenti possono ora proteggere i propri messaggi di posta elettronica usando il servizio Azure Rights Management. Ad esempio, in Outlook Web App scegliere **Imposta autorizzazioni** dal menu esteso (**...**) e quindi fare clic su **Non inoltrare** o su uno dei modelli disponibili per applicare la protezione delle informazioni ai messaggi di posta elettronica e a eventuali allegati. Dal momento che, tuttavia, Outlook Web App memorizza nella cache l'interfaccia utente per un giorno, attendere che sia trascorso questo periodo di tempo prima di provare ad applicare la protezione delle informazioni ai messaggi di posta elettronica dopo l'esecuzione di questi comandi di configurazione. Prima che gli aggiornamenti dell'interfaccia utente riflettano la nuova configurazione, non verranno visualizzate opzioni nel menu **Imposta autorizzazioni** .

> [!IMPORTANT]
> Se si creano nuovi [modelli personalizzati](configure-custom-templates.md) per Azure Rights Management o si aggiornano modelli, ogni volta è necessario eseguire il comando seguente di Exchange Online PowerShell (se necessario, eseguire prima i passaggi 2 e 3) per sincronizzare le modifiche con Exchange Online: `Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates –RMSOnline`

In qualità di amministratore di Exchange, è ora possibile configurare le funzionalità che applicano automaticamente la protezione delle informazioni, ad esempio le [regole di trasporto](https://technet.microsoft.com/library/dd302432.aspx), i [criteri di prevenzione della perdita dei dati](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx)e la [casella vocale protetta](https://technet.microsoft.com/library/dn198211%28v=exchg.150%29.aspx) (messaggistica unificata).


### <a name="office-365-message-encryption"></a>Crittografia messaggi di Office 365
Eseguire gli stessi passaggi illustrati nella sezione precedente, ma se non si vuole che vengano visualizzati i modelli, prima del passaggio 6, eseguire il comando seguente per impedire che i modelli IRM siano disponibili in Outlook Web App e nel client di Outlook: `Set-IRMConfiguration -ClientAccessServerEnabled $false`

Si è quindi pronti per configurare le [regole di trasporto](https://technet.microsoft.com/library/dd302432.aspx) per modificare automaticamente la sicurezza dei messaggi quando i destinatari sono esterni all'organizzazione e selezionare l'opzione **Applica crittografia Office 365** .

Per altre informazioni sulla crittografia dei messaggi, vedere [Crittografia in Office 365](https://technet.microsoft.com/library/dn569286.aspx) nella libreria di Exchange.


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
