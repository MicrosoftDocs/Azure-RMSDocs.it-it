---
title: Office 365&colon; configurazione di client e servizi online | Azure RMS
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 0a6ce612-1b6b-4e21-b7fd-bcf79e492c3b
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0f355da35dff62ecee111737eb1793ae286dc93e
ms.openlocfilehash: 7a2436a6ebb17e4336f1321b8f3742e34ea59689


---

# Office 365: configurazione di client e servizi online

*Si applica a: Azure Rights Management, Office 365*

Poiché Office 365 supporta in modo nativo Azure RMS, non è necessario eseguire alcuna attività di configurazione dei computer client per supportare le funzionalità IRM (Information Rights Management) per le applicazioni come Word, Excel, PowerPoint, Outlook e Outlook Web App. Tutti gli utenti devono solo eseguire l'accesso alle applicazioni di Office con le proprie credenziali di [!INCLUDE[o365_1](../includes/o365_1_md.md)] per poter proteggere file e messaggi e-mail e per usare file e messaggi e-mail protetti da altri.

È tuttavia consigliabile usare tali applicazioni insieme all'applicazione di condivisione Rights Management, in modo che gli utenti possano beneficiare dei vantaggi offerti dal componente aggiuntivo di Office. Per ulteriori informazioni, vedere [Applicazione di condivisione Rights Management: installazione e configurazione dei client](configure-sharing-app.md).

## Exchange Online: configurazione di IRM
Per configurare Exchange Online per supportare Azure RMS, è necessario configurare il servizio IRM (Information Rights Management) per Exchange Online. A tale scopo, è possibile usare Windows PowerShell (senza bisogno di installare un modulo separato) ed eseguire i [comandi PowerShell per Exchange Online](https://technet.microsoft.com/library/jj200677.aspx).

> [!NOTE]
> Non è attualmente possibile configurare Exchange Online per il supporto di Azure RMS se si usa una chiave del tenant gestita dal cliente (BYOK) per Azure RMS, invece della configurazione predefinita con una chiave del tenant gestita da Microsoft. Per ulteriori informazioni, vedere [Prezzi e restrizioni della modalità BYOK](../plan-design/byok-price-restrictions.md).
>
> Se si prova a configurare Exchange Online quando Azure RMS usa BYOK, il comando per l'importazione della chiave (passaggio 5, nella procedura seguente) avrà esito negativo con messaggio di errore **[FailureCategory=Cmdlet-FailedToGetTrustedPublishingDomainFromRmsOnlineException]**.

I passaggi seguenti offrono un set tipico di comandi da eseguire per abilitare Exchange Online per l'uso di Azure RMS:

1.  Se questa è la prima volta che si usa Windows PowerShell per Exchange Online nel computer, sarà necessario configurare Windows PowerShell per l'esecuzione degli script firmati. Avviare la sessione di Windows PowerShell usando l'opzione **Esegui come amministratore** e quindi digitare:

    ```
    Set-ExecutionPolicy RemoteSigned
    ```

2.  Nella sessione di Windows PowerShell accedere a Exchange Online usando un account abilitato per l'accesso alla shell remota. Per impostazione predefinita, tutti gli account creati in Exchange Online sono attivati per l'accesso alla Shell remota. L'accesso può essere disattivato o attivato usando il comando [Set-User &lt;UserIdentity&gt; -RemotePowerShellEnabled](https://technet.microsoft.com/library/jj984292%28v=exchg.160%29.aspx)

    Per accedere, digitare quanto segue:

    ```
    $Cred = Get-Credential
    ```
    Nella finestra di dialogo **Richiesta credenziali di Windows PowerShell** specificare il nome utente e la password di Office 365.

3.  Connettersi al servizio Exchange Online eseguendo i due comandi seguenti:

    ```
    $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://ps.outlook.com/powershell/ -Credential $Cred -Authentication Basic –AllowRedirection
    ```

    ```
    Import-PSSession $Session
    ```

4.  Specificare la posizione della chiave del tenant di Azure RMS, in base alla posizione in cui è stato creato il tenant dell'organizzazione:

    Per l'America del Nord (e sottoscrizioni Government):

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

5.  Importare i dati di configurazione da Azure RMS a Exchange Online, sotto forma di dominio di pubblicazione trusted. I dati includono la chiave del tenant di Azure RMS e i modelli di Azure RMS:

    ```
    Import-RMSTrustedPublishingDomain -RMSOnline -name "RMS Online"
    ```
    In questo comando è stato usato il nome **RMS Online** come nome base del dominio di pubblicazione trusted per Azure RMS in Exchange Online. Dopo aver importato il dominio di pubblicazione trusted, viene denominato **RMS Online - 1** in Exchange Online.

6.  Abilitare la funzionalità di Azure RMS in modo che le funzionalità di IRM siano disponibili per Exchange Online:

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

Gli utenti possono ora proteggere i propri messaggi di posta elettronica con Azure RMS. Ad esempio, in Outlook Web App scegliere **Imposta autorizzazioni** dal menu esteso (**...**) e quindi fare clic su **Non inoltrare** o su uno dei modelli disponibili per applicare la protezione delle informazioni ai messaggi di posta elettronica e a eventuali allegati. Dal momento che, tuttavia, Outlook Web App memorizza nella cache l'interfaccia utente per un giorno, attendere che sia trascorso questo periodo di tempo prima di provare ad applicare la protezione delle informazioni ai messaggi di posta elettronica dopo l'esecuzione di questi comandi di configurazione. Prima che gli aggiornamenti dell'interfaccia utente riflettano la nuova configurazione, non verranno visualizzate opzioni nel menu **Imposta autorizzazioni** .

> [!IMPORTANT]
> Se vengono creati nuovi [modelli personalizzati](configure-custom-templates.md) per Azure RMS o si aggiornano modelli, ogni volta, è necessario eseguire il seguente comando di Exchange Online PowerShell (se necessario, eseguire i passaggi 2 e 3 in primo luogo) per sincronizzare le modifiche con Exchange Online: `Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates –RMSOnline`

In qualità di amministratore di Exchange, è ora possibile configurare le funzionalità che applicano automaticamente la protezione delle informazioni, ad esempio le [regole di trasporto](https://technet.microsoft.com/library/dd302432.aspx), i [criteri di prevenzione della perdita dei dati](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx)e la [casella vocale protetta](https://technet.microsoft.com/library/dn198211%28v=exchg.150%29.aspx) (messaggistica unificata).

Per istruzioni dettagliate per configurare Exchange Online in modo da abilitare la funzionalità IRM, vedere la documentazione nella libreria Exchange. Ad esempio:

-   [Connettersi a Exchange Online usando PowerShell remoto](https://technet.microsoft.com/library/jj984289%28v=exchg.160%29.aspx)

-   [Configurare IRM per usare Azure Rights Management](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx)

### Crittografia messaggi di Office 365
Eseguire gli stessi passaggi illustrati nella sezione precedente, ma se non si vuole che vengano visualizzati i modelli, prima del passaggio 6, eseguire il comando seguente per impedire che i modelli IRM siano disponibili in Outlook Web App e nel client di Outlook: `Set-IRMConfiguration -ClientAccessServerEnabled $false`

Si è quindi pronti per configurare le [regole di trasporto](https://technet.microsoft.com/library/dd302432.aspx) per modificare automaticamente la sicurezza dei messaggi quando i destinatari sono esterni all'organizzazione e selezionare l'opzione **Applica crittografia Office 365** .

Per altre informazioni sulla crittografia dei messaggi, vedere [Crittografia in Office 365](https://technet.microsoft.com/library/dn569286.aspx) nella libreria di Exchange.

## SharePoint Online e OneDrive for Business: configurazione di IRM
Per configurare SharePoint Online e OneDrive for Business allo scopo di supportare Azure RMS, è necessario abilitare prima il servizio IRM (Information Rights Management) per SharePoint Online usando l'interfaccia di amministrazione di SharePoint. I proprietari del sito possono quindi proteggere con IRM i propri elenchi e le proprie raccolte documenti di SharePoint e gli utenti possono proteggere con IRM la propria raccolta di OneDrive for Business, in modo che i documenti salvati in tale posizione e condivisi con altri utenti vengano protetti automaticamente da Azure RMS.

Per abilitare il servizio IRM (Information Rights Management) per SharePoint Online, vedere le istruzioni seguenti dal sito Web di Office:

-   [Configurare Information Rights Management (IRM) nell'interfaccia di amministrazione di SharePoint](http://office.microsoft.com/office365-sharepoint-online-enterprise-help/set-up-information-rights-management-irm-insharepoint-online-HA102895193.aspx)

Questa configurazione viene eseguita dall'amministratore di Office 365.

### Configurazione di IRM per le raccolte e gli elenchi
Dopo l'abilitazione del servizio IRM per SharePoint, i proprietari dei siti possono proteggere con IRM le proprie raccolte documenti e i propri elenchi di SharePoint. Per le istruzioni, vedere le informazioni seguenti nel sito Web Office:

-   [Applicare Information Rights Management a un elenco o a una raccolta](http://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)

Questa configurazione viene eseguita dall'amministratore del sito di SharePoint.

### Configurazione di IRM per OneDrive for Business
Dopo aver attivato il servizio IRM per SharePoint Online, è possibile configurare la libreria dei documenti OneDrive for Business degli utenti per la protezione di Rights Management.  Gli utenti possono configurarla autonomamente usando l’icona **Impostazioni** in OneDrive. Anche se gli amministratori non possono configurare Rights Management per OneDrive for Business degli utenti usando il centro di amministrazione di SharePoint, è possibile farlo tramite Windows PowerShell.

> [!NOTE]
> Per ulteriori informazioni sulla configurazione di OneDrive for Business, vedere la documentazione di Office [Impostare OneDrive for Business in Office 365](https://support.office.com/article/Set-up-OneDrive-for-Business-in-Office-365-3e21f8f0-e0a1-43be-aa3e-8c0236bf11bb).

#### Configurazione per gli utenti
Dare agli utenti queste istruzioni affinché essi possano configurare la loro copia di OneDrive for Business e proteggere i propri file di lavoro tramite IRM.

1.  In OneDrive fare clic sull'icona **Impostazioni** per aprire il menu Impostazioni e quindi fare clic su **Contenuto del sito**.

2.  Posizionare il puntatore del mouse sul riquadro **Documenti** fare clic sui puntini di sospensione (**...**) e quindi fare clic su **IMPOSTAZIONI.**

3.  Nella pagina **Impostazioni** nella sezione **Autorizzazioni e gestione** , fare clic su **Information Rights Management**.

4.  Nella pagina **Impostazioni Information Rights Management** selezionare la casella di controllo **Limita autorizzazioni per la libreria durante il download** specificare il nome scelto e una descrizione per le autorizzazioni, quindi, facoltativamente, fare clic su **MOSTRA OPZIONI** per definire configurazioni facoltative e quindi fare clic su **OK**.

    Per altre informazioni sulle opzioni di configurazione, vedere le istruzioni in [Applicare la protezione Information Rights Management a un elenco o una raccolta](https://support.office.com/article/Apply-Information-Rights-Management-to-a-list-or-library-3bdb5c4e-94fc-4741-b02f-4e7cc3c54aa1) nella documentazione di Office.

Poiché questa configurazione si basa sugli utenti e non è l’amministratore a proteggere tramite IRM la loro libreria OneDrive for Business, è necessario informare gli utenti sui benefici derivanti dal proteggere i propri file e come farlo. Ad esempio, spiegare agli utenti che quando condividono un documento da OneDrive for Business solo le persone da loro autorizzate potranno accedere al documento con le restrizioni configurate, anche se il file viene rinominato e copiato altrove.

#### Configurazione per gli amministratori
Anche se non è possibile configurare IRM per OneDrive for Business per gli utenti per le aziende usando il centro di amministrazione di SharePoint, è possibile farlo tramite Windows PowerShell. Per attivare IRM per queste librerie, attenersi alla seguente procedura:

1.  Scaricare e installare l’[SDK dei componenti client di SharePoint Online](http://www.microsoft.com/en-us/download/details.aspx?id=42038).

2.  Scaricare e installare [SharePoint Online Management Shell](http://www.microsoft.com/en-us/download/details.aspx?id=35588).

3.  Copiare il contenuto del seguente script e denominare il file Set-IRMOnOneDriveForBusiness.ps1 nel computer in uso.

    *&#42;&#42;Dichiarazione di non responsabilità&#42;&#42;*: questo script di esempio non è supportato in alcun programma o servizio di supporto standard Microsoft. Questo script di esempio viene fornito "nello stato in stato in cui si trova" senza garanzia di alcun tipo.

    ```
    # Requires Windows PowerShell version 3

    <#
      Description:

        Configures IRM policy settings for OneDrive for Business and can also be used for SharePoint Online libraries and lists

     Script Installation Requirements:

       SharePoint Online Client Components SDK
       http://www.microsoft.com/en-us/download/details.aspx?id=42038

       SharePoint Online Management Shell
       http://www.microsoft.com/en-us/download/details.aspx?id=35588

    ======
    #>

    # URL will be in the format https://<tenant-name>-admin.sharepoint.com
    $sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com"

    $tenantAdmin = "admin@contoso.com"

    $webUrls = @("https://contoso-my.sharepoint.com/personal/user1_contoso_com",
                 "https://contoso-my.sharepoint.com/personal/user2_contoso_com",
                 "https://contoso-my.sharepoint.com/personal/user3_contoso_com")

    <# As an alternative to specifying the URLs as an array, you can import them from a CSV file (no header, single value per row).
       Then, use: $webUrls = Get-Content -Path "File_path_and_name.csv"

    #>

    $listTitle = "Documents"

    function Load-SharePointOnlineClientComponentAssemblies
    {
        [cmdletbinding()]
        param()

        process
        {
            # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI
            try
            {
                Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
                [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

                return $true
            }
            catch
            {
                if($_.Exception.Message -match "Could not load file or assembly")
                {
                    Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=42038"
                }
                else
                {
                    Write-Error -Exception $_.Exception
                }
                return $false
            }
        }
    }

    function Load-SharePointOnlineModule
    {
        [cmdletbinding()]
        param()

        process
        {
            do
            {
                # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell
                $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue

                if(-not $spoModule)
                {
                    try
                    {
                        Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking
                        return $true
                    }
                    catch
                    {
                        if($_.Exception.Message -match "Could not load file or assembly")
                        {
                            Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=35588"
                        }
                        else
                        {
                            Write-Error -Exception $_.Exception
                        }
                        return $false
                    }
                }
                else
                {
                    return $true
                }
            }
            while(-not $spoModule)
        }
    }

    function Set-IrmConfiguration
    {
        [cmdletbinding()]
        param(
            [parameter(Mandatory=$true)][Microsoft.SharePoint.Client.List]$List,
            [parameter(Mandatory=$true)][string]$PolicyTitle,
            [parameter(Mandatory=$true)][string]$PolicyDescription,
            [parameter(Mandatory=$false)][switch]$IrmReject,
            [parameter(Mandatory=$false)][DateTime]$ProtectionExpirationDate,
            [parameter(Mandatory=$false)][switch]$DisableDocumentBrowserView,
            [parameter(Mandatory=$false)][switch]$AllowPrint,
            [parameter(Mandatory=$false)][switch]$AllowScript,
            [parameter(Mandatory=$false)][switch]$AllowWriteCopy,
            [parameter(Mandatory=$false)][int]$DocumentAccessExpireDays,
            [parameter(Mandatory=$false)][int]$LicenseCacheExpireDays,
            [parameter(Mandatory=$false)][string]$GroupName
        )

        process
        {
            Write-Verbose "Applying IRM Configuration on '$($List.Title)'"

            # reset the value to the default settings
            $list.InformationRightsManagementSettings.Reset()

            $list.IrmEnabled = $true

            # IRM Policy title and description

                $list.InformationRightsManagementSettings.PolicyTitle       = $PolicyTitle
                $list.InformationRightsManagementSettings.PolicyDescription = $PolicyDescription

            # Set additional IRM library settings

                # Do not allow users to upload documents that do not support IRM
                $list.IrmReject = $IrmReject.IsPresent

                $parsedDate = Get-Date
                if([DateTime]::TryParse($ProtectionExpirationDate, [ref]$parsedDate))
                {
                    # Stop restricting access to the library at <date>
                    $list.IrmExpire = $true
                    $list.InformationRightsManagementSettings.DocumentLibraryProtectionExpireDate = $ProtectionExpirationDate
                }

                # Prevent opening documents in the browser for this Document Library
                $list.InformationRightsManagementSettings.DisableDocumentBrowserView = $DisableDocumentBrowserView.IsPresent

            # Configure document access rights

                # Allow viewers to print
                $list.InformationRightsManagementSettings.AllowPrint = $AllowPrint.IsPresent

                # Allow viewers to run script and screen reader to function on downloaded documents
                $list.InformationRightsManagementSettings.AllowScript = $AllowScript.IsPresent

                # Allow viewers to write on a copy of the downloaded document
                $list.InformationRightsManagementSettings.AllowWriteCopy = $AllowWriteCopy.IsPresent

                if($DocumentAccessExpireDays)
                {
                    # After download, document access rights will expire after these number of days (1-365)
                    $list.InformationRightsManagementSettings.EnableDocumentAccessExpire = $true
                    $list.InformationRightsManagementSettings.DocumentAccessExpireDays   = $DocumentAccessExpireDays
                }

            # Set group protection and credentials interval

                if($LicenseCacheExpireDays)
                {
                    # Users must verify their credentials using this interval (days)
                    $list.InformationRightsManagementSettings.EnableLicenseCacheExpire = $true
                    $list.InformationRightsManagementSettings.LicenseCacheExpireDays   = $LicenseCacheExpireDays
                }

                if($GroupName)
                {
                    # Allow group protection. Default group:
                    $list.InformationRightsManagementSettings.EnableGroupProtection = $true
                    $list.InformationRightsManagementSettings.GroupName             = $GroupName
                }
        }
        end
        {
            if($list)
            {
                Write-Verbose "Committing IRM configuration settings on '$($list.Title)'"
                $list.InformationRightsManagementSettings.Update()
                $list.Update()
                $script:clientContext.Load($list)
                $script:clientContext.ExecuteQuery()
            }
        }
    }

    function Get-CredentialFromCredentialCache
    {
        [cmdletbinding()]
        param([string]$CredentialName)

        #if( Test-Path variable:\global:CredentialCache )
        if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue )
        {
            if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName))
            {
                Write-Verbose "Credential Cache Hit: $CredentialName"
                return $global:O365TenantAdminCredentialCache[$CredentialName]
            }
        }
        Write-Verbose "Credential Cache Miss: $CredentialName"
        return $null
    }

    function Add-CredentialToCredentialCache
    {
        [cmdletbinding()]
        param([System.Management.Automation.PSCredential]$Credential)

        if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue))
        {
            Write-Verbose "Initializing the Credential Cache"
            $global:O365TenantAdminCredentialCache = @{}
        }

        Write-Verbose "Adding Credential to the Credential Cache"
        $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential
    }

    # load the required assemblies and Windows PowerShell modules

        if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return }

    # Add the credentials to the client context and SharePoint Online service connection

        # check for cached credentials to use
        $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin

        if(-not $o365TenantAdminCredential)
        {
            # when credentials are not cached, prompt for the tenant admin credentials
            $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin"

            if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 )
            {
                Write-Error -Message "Could not validate the supplied tenant admin credentials"
                return
            }

            # add the credentials to the cache
            Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential
        }

    # connect to Office365 first, required for SharePoint Online cmdlets to run

        Connect-SPOService -Url $sharepointAdminCenterUrl -Credential $o365TenantAdminCredential

    # enumerate each of the specified site URLs

        foreach($webUrl in $webUrls)
        {
            $grantedSiteCollectionAdmin = $false

            try
            {
                # establish the client context and set the credentials to connect to the site
                $script:clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($webUrl)
                $script:clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password)

                # initialize the site and web context
                $script:clientContext.Load($script:clientContext.Site)
                $script:clientContext.Load($script:clientContext.Web)
                $script:clientContext.ExecuteQuery()

                # load and ensure the tenant admin user account if present on the target SharePoint site
                $tenantAdminUser = $script:clientContext.Web.EnsureUser($o365TenantAdminCredential.UserName)
                $script:clientContext.Load($tenantAdminUser)
                $script:clientContext.ExecuteQuery()

                # check if the tenant admin is a site admin
                if( -not $tenantAdminUser.IsSiteAdmin )
                {
                    try
                    {
                        # grant the tenant admin temporary admin rights to the site collection
                        Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $true | Out-Null
                        $grantedSiteCollectionAdmin = $true
                    }
                    catch
                    {
                        Write-Error $_.Exception
                        return
                    }
                }

                try
                {
                    # load the list orlibrary using CSOM

                    $list = $null
                    $list = $script:clientContext.Web.Lists.GetByTitle($listTitle)
                    $script:clientContext.Load($list)
                    $script:clientContext.ExecuteQuery()

                    # **************  ADMIN INSTRUCTIONS  **************
                    # If necessary, modify the following Set-IrmConfiguration parameters to match your required values
                    # The supplied options and values are for example only
                    # Example that shows the Set-IrmConfiguration command with all parameters: Set-IrmConfiguration -List $list -PolicyTitle "Protected Files" -PolicyDescription "This policy restricts access to authorized users" -IrmReject -ProtectionExpirationDate $(Get-Date).AddDays(180) -DisableDocumentBrowserView -AllowPrint -AllowScript -AllowWriteCopy -LicenseCacheExpireDays 25 -DocumentAccessExpireDays 90

                    Set-IrmConfiguration -List $list -PolicyTitle "Protected Files" -PolicyDescription "This policy restricts access to authorized users"  
                }
                catch
                {
                    Write-Error -Message "Error setting IRM configuration on site: $webUrl.`nError Details: $($_.Exception.ToString())"
                }
           }
           finally
           {
                if($grantedSiteCollectionAdmin)
                {
                    # remove the temporary admin rights to the site collection
                    Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $false | Out-Null
                }
           }
        }

    Disconnect-SPOService -ErrorAction SilentlyContinue
    ```

4.  Rivedere lo script e apportare le seguenti modifiche:

    1.  Cercare `$sharepointAdminCenterUrl` e sostituire il valore di esempio con il proprio URL del centro di amministrazione di SharePoint.

        Questo valore è disponibile come URL di base quando si accede al centro di amministrazione di SharePoint e ha il formato seguente: https://*&lt;nome_tenant&gt;*-admin.sharepoint.com

        Ad esempio, se il nome del tenant è "contoso", sarà necessario specificare: **https://contoso-admin.sharepoint.com**

    2.  Cercare `$tenantAdmin` e sostituire il valore di esempio con il proprio account di amministratore globale completo per Office 365.

        Questo valore corrisponde a quello usato per accedere come amministratore globale al portale di amministrazione di Office 365 e ha il seguente formato: nome_utente@*&lt;nome dominio tenant&gt;*.com

        Ad esempio, se il nome utente dell’amministratore globale di Office 365 è "admin" per il dominio del tenant " contoso.com", si specificherà: **admin@contoso.com**

    3.  Cercare `$webUrls` e sostituire i valori di esempio con gli URL Web di OneDrive for Business degli utenti, aggiungendo o eliminando il numero di voci in base alle esigenze.

        In alternativa, vedere i commenti nello script su come sostituire questa matrice importando un file CSV contenente tutti gli URL che è necessario configurare.  È stato fornito un altro script di esempio per cercare automaticamente ed estrarre gli URL per popolare questo. file CSV. Quando si è pronti per eseguire questa operazione, espandere la sezione [Script aggiuntivo per l'output di tutti gli URL di OneDrive for Business per un file CSV](#BKMK_Script_OD4B_URLS) immediatamente dopo questi passaggi.

        L'URL Web di OneDrive for Business dell'utente è nel formato seguente: https://*&lt;nome tenant&gt;*-my.sharepoint.com/personal/*&lt;nome_utente&gt;*_*&lt;nome tenant&gt;*_com

        Ad esempio, se l'utente nel tenant contoso dispone di un nome utente di "rsimone", si specificherà: **https://contoso-my.sharepoint.com/personal/rsimone_contoso_com**

    4.  Poiché si sta usando lo script per configurare OneDrive for Business, non modificare il valore di **Documenti** per la variabile `$listTitle`.

    5.  Cercare `ADMIN INSTRUCTIONS`. Se non si apportano modifiche a questa sezione, OneDrive  for Business dell’utente verrà configurato per IRM con il titolo di criterio di "File protetto" e la descrizione "Questo criterio limita l'accesso agli utenti autorizzati".  Non verrà impostata alcun’altra opzione IRM, condizione valida per la maggior parte degli ambienti. Tuttavia, si può modificare il titolo del criterio suggerito e la descrizione e anche aggiungere eventuali altre opzioni IRM appropriate per l'ambiente. Vedere l'esempio commentato nello script per ottenere un aiuto per creare il proprio set di parametri per il comando Set-IrmConfiguration.

5.  Salvare lo script e firmarlo. Se non si firma lo script (condizione più sicura), Windows PowerShell deve essere configurato nel computer in uso per eseguire script non firmati. Per questa operazione, eseguire la sessione di Windows PowerShell con l'opzione **Esegui come amministratore** e digitare: **Set-ExecutionPolicy Unrestricted**. Questa configurazione, tuttavia, consente l'esecuzione di tutti gli script non firmati (meno sicuri).

    Per altre informazioni sulla firma degli script di Windows PowerShell, vedere [about_Signing](https://technet.microsoft.com/library/hh847874.aspx) nella raccolta di documentazione di PowerShell.

6.  Eseguire lo script e se richiesto, immettere la password per l'account di amministratore di Office 365. Se si modifica lo script e lo si esegue nella stessa sessione di Windows PowerShell, le credenziali non verranno richieste.

> [!TIP]
> È inoltre possibile usare questo script per configurare IRM per una libreria di SharePoint Online. Per questa configurazione, probabilmente si desidererà attivare l'opzione aggiuntiva **Non consentire il caricamento di documenti che non supportano IRM**, per assicurare che la libreria contenga solo documenti protetti.    A tale scopo, aggiungere il parametro `-IrmReject` per il comando Set-IrmConfiguration nello script.
>
> Inoltre potrebbe essere necessario modificare la variabile `$webUrls` (ad esempio, **https://contoso.sharepoint.com**) e la variabile `$listTitle` (ad esempio, **$Reports**).

Se è necessario disabilitare IRM per le librerie OneDrive for Business dell'utente, vedere la sezione [Script per disattivare IRM per OneDrive for Business](#script-to-disable-irm-for-onedrive-for-business).

##### Script aggiuntivo per l'output di tutti gli URL di OneDrive for Business per un file CSV
Per il passaggio 4c riportato sopra, è possibile usare il seguente script di Windows PowerShell per estrarre gli URL per le librerie di OneDrive for Business degli utenti che sarà quindi possibile controllare e modificare, se necessario, quindi importare nello script principale.

Questo script richiede anche l’[SDK dei componenti client di SharePoint Online](http://www.microsoft.com/en-us/download/details.aspx?id=42038) e [SharePoint Online Management Shell](http://www.microsoft.com/en-us/download/details.aspx?id=35588). Seguire le stesse istruzioni per copiare e incollare, quindi salvare il file in locale (ad esempio, “Report-OneDriveForBusinessSiteInfo.ps1”), modificare i valori `$sharepointAdminCenterUrl` e `$tenantAdmin` come prima e quindi eseguire lo script.

*&#42;&#42;Dichiarazione di non responsabilità&#42;&#42;*: questo script di esempio non è supportato in alcun programma o servizio di supporto standard Microsoft. Questo script di esempio viene fornito "nello stato in stato in cui si trova" senza garanzia di alcun tipo.

```
# Requires Windows PowerShell version 3

<#
  Description:

    Queries the search service of an Office 365 tenant to retrieve all OneDrive for Business sites.  
    Details of the discovered sites are written to a .CSV file (by default,"OneDriveForBusinessSiteInfo_<date>.csv").

 Script Installation Requirements:

   SharePoint Online Client Components SDK
   http://www.microsoft.com/en-us/download/details.aspx?id=42038

   SharePoint Online Management Shell
   http://www.microsoft.com/en-us/download/details.aspx?id=35588

======
#>

# URL will be in the format https://<tenant-name>-admin.sharepoint.com
$sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com"

$tenantAdmin = "admin@contoso.onmicrosoft.com"                           

$reportName = "OneDriveForBusinessSiteInfo_$((Get-Date).ToString("yyyy-MM-dd_hh.mm.ss")).csv"

$oneDriveForBusinessSiteUrls= @()
$resultsProcessed = 0

function Load-SharePointOnlineClientComponentAssemblies
{
    [cmdletbinding()]
    param()

    process
    {
        # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI
        try
        {
            Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            return $true
        }
        catch
        {
            if($_.Exception.Message -match "Could not load file or assembly")
            {
                Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=42038"
            }
            else
            {
                Write-Error -Exception $_.Exception
            }
            return $false
        }
    }
}

function Load-SharePointOnlineModule
{
    [cmdletbinding()]
    param()

    process
    {
        do
        {
            # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell
            $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue

            if(-not $spoModule)
            {
                try
                {
                    Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking
                    return $true
                }
                catch
                {
                    if($_.Exception.Message -match "Could not load file or assembly")
                    {
                        Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=35588"
                    }
                    else
                    {
                        Write-Error -Exception $_.Exception
                    }
                    return $false
                }
            }
            else
            {
                return $true
            }
        }
        while(-not $spoModule)
    }
}

function Get-CredentialFromCredentialCache
{
    [cmdletbinding()]
    param([string]$CredentialName)

    #if( Test-Path variable:\global:CredentialCache )
    if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue )
    {
        if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName))
        {
            Write-Verbose "Credential Cache Hit: $CredentialName"
            return $global:O365TenantAdminCredentialCache[$CredentialName]
        }
    }
    Write-Verbose "Credential Cache Miss: $CredentialName"
    return $null
}

function Add-CredentialToCredentialCache
{
    [cmdletbinding()]
    param([System.Management.Automation.PSCredential]$Credential)

    if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue))
    {
        Write-Verbose "Initializing the Credential Cache"
        $global:O365TenantAdminCredentialCache = @{}
    }

    Write-Verbose "Adding Credential to the Credential Cache"
    $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential
}

# load the required assemblies and Windows PowerShell modules

    if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return }

# Add the credentials to the client context and SharePoint Online service connection

    # check for cached credentials to use
    $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin

    if(-not $o365TenantAdminCredential)
    {
        # when credentials are not cached, prompt for the tenant admin credentials
        $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin"

        if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 )
        {
            Write-Error -Message "Could not validate the supplied tenant admin credentials"
            return
        }

        # add the credentials to the cache
        Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential
    }

# establish the client context and set the credentials to connect to the site

    $clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($sharepointAdminCenterUrl)
    $clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password)

# run a query against the Office 365 tenant search service to retrieve all OneDrive for Business URLs

    do
    {
        # build the query object
        $query = New-Object Microsoft.SharePoint.Client.Search.Query.KeywordQuery($clientContext)
        $query.TrimDuplicates        = $false
        $query.RowLimit              = 500
        $query.QueryText             = "SPSiteUrl:'/personal/' AND contentclass:STS_Site"
        $query.StartRow              = $resultsProcessed
        $query.TotalRowsExactMinimum = 500000

        # run the query
        $searchExecutor = New-Object Microsoft.SharePoint.Client.Search.Query.SearchExecutor($clientContext)
        $queryResults = $searchExecutor.ExecuteQuery($query)
        $clientContext.ExecuteQuery()

        # enumerate the search results and store the site URLs
        $queryResults.Value[0].ResultRows | % {
            $oneDriveForBusinessSiteUrls += $_.Path
            $resultsProcessed++
        }
    }
    while($resultsProcessed -lt $queryResults.Value.TotalRows)

$oneDriveForBusinessSiteUrls | Out-File -FilePath $reportName
```

##### Script per disattivare IRM per OneDrive for Business
Usare il seguente script di esempio, se è necessario disattivare IRM per OneDrive for Business degli utenti.

Questo script richiede anche l’[SDK dei componenti client di SharePoint Online](http://www.microsoft.com/en-us/download/details.aspx?id=42038) e [SharePoint Online Management Shell](http://www.microsoft.com/en-us/download/details.aspx?id=35588). Copiare e incollare il contenuto, salvare il file in locale (ad esempio, "Disable-IRMOnOneDriveForBusiness.ps1") e modificare i valori `$sharepointAdminCenterUrl` e `$tenantAdmin`. Specificare manualmente gli URL di OneDrive for Business o usare lo script nella sezione precedente, per importarli ed eseguire lo script manualmente.

*&#42;&#42;Dichiarazione di non responsabilità&#42;&#42;*: questo script di esempio non è supportato in alcun programma o servizio di supporto standard Microsoft. Questo script di esempio viene fornito "nello stato in stato in cui si trova" senza garanzia di alcun tipo.

```
# Requires Windows PowerShell version 3

<#
  Description:

    Disables IRM for OneDrive for Business and can also be used for SharePoint Online libraries and lists

 Script Installation Requirements:

   SharePoint Online Client Components SDK
   http://www.microsoft.com/en-us/download/details.aspx?id=42038

   SharePoint Online Management Shell
   http://www.microsoft.com/en-us/download/details.aspx?id=35588

======
#>

$sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com"

$tenantAdmin = "admin@contoso.com"

$webUrls = @("https://contoso-my.sharepoint.com/personal/user1_contoso_com",
             "https://contoso-my.sharepoint.com/personal/user2_contoso_com",
             "https://contoso-my.sharepoint.com/personal/person3_contoso_com")

<# As an alternative to specifying the URLs as an array, you can import them from a CSV file (no header, single value per row).
   Then, use: $webUrls = Get-Content -Path "File_path_and_name.csv"

#>

$listTitle = "Documents"

function Load-SharePointOnlineClientComponentAssemblies
{
    [cmdletbinding()]
    param()

    process
    {
        # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI
        try
        {
            Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            return $true
        }
        catch
        {
            if($_.Exception.Message -match "Could not load file or assembly")
            {
                Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=42038"
            }
            else
            {
                Write-Error -Exception $_.Exception
            }
            return $false
        }
    }
}

function Load-SharePointOnlineModule
{
    [cmdletbinding()]
    param()

    process
    {
        do
        {
            # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell
            $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue

            if(-not $spoModule)
            {
                try
                {
                    Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking
                    return $true
                }
                catch
                {
                    if($_.Exception.Message -match "Could not load file or assembly")
                    {
                        Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=35588"
                    }
                    else
                    {
                        Write-Error -Exception $_.Exception
                    }
                    return $false
                }
            }
            else
            {
                return $true
            }
        }
        while(-not $spoModule)
    }
}

function Remove-IrmConfiguration
{
    [cmdletbinding()]
    param(
        [parameter(Mandatory=$true)][Microsoft.SharePoint.Client.List]$List
    )

    process
    {
        Write-Verbose "Disabling IRM Configuration on '$($List.Title)'"

        $List.IrmEnabled = $false
        $List.IrmExpire  = $false
        $List.IrmReject  = $false
        $List.InformationRightsManagementSettings.Reset()
    }
    end
    {
        if($List)
        {
            Write-Verbose "Committing IRM configuration settings on '$($list.Title)'"
            $list.InformationRightsManagementSettings.Update()
            $list.Update()
            $script:clientContext.Load($list)
            $script:clientContext.ExecuteQuery()
        }
    }
}

function Get-CredentialFromCredentialCache
{
    [cmdletbinding()]
    param([string]$CredentialName)

    #if( Test-Path variable:\global:CredentialCache )
    if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue )
    {
        if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName))
        {
            Write-Verbose "Credential Cache Hit: $CredentialName"
            return $global:O365TenantAdminCredentialCache[$CredentialName]
        }
    }
    Write-Verbose "Credential Cache Miss: $CredentialName"
    return $null
}

function Add-CredentialToCredentialCache
{
    [cmdletbinding()]
    param([System.Management.Automation.PSCredential]$Credential)

    if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue))
    {
        Write-Verbose "Initializing the Credential Cache"
        $global:O365TenantAdminCredentialCache = @{}
    }

    Write-Verbose "Adding Credential to the Credential Cache"
    $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential
}

# load the required assemblies and Windows PowerShell modules

    if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return }

# Add the credentials to the client context and SharePoint Online service connection

    # check for cached credentials to use
    $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin

    if(-not $o365TenantAdminCredential)
    {
        # when credentials are not cached, prompt for the tenant admin credentials
        $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin"

        if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 )
        {
            Write-Error -Message "Could not validate the supplied tenant admin credentials"
            return
        }

        # add the credentials to the cache
        Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential
    }

# connect to Office365 first, required for SharePoint Online cmdlets to run

    Connect-SPOService -Url $sharepointAdminCenterUrl -Credential $o365TenantAdminCredential

# enumerate each of the specified site URLs

    foreach($webUrl in $webUrls)
    {
        $grantedSiteCollectionAdmin = $false

        try
        {
            # establish the client context and set the credentials to connect to the site
            $script:clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($webUrl)
            $script:clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password)

            # initialize the site and web context
            $script:clientContext.Load($script:clientContext.Site)
            $script:clientContext.Load($script:clientContext.Web)
            $script:clientContext.ExecuteQuery()

            # load and ensure the tenant admin user account if present on the target SharePoint site
            $tenantAdminUser = $script:clientContext.Web.EnsureUser($o365TenantAdminCredential.UserName)
            $script:clientContext.Load($tenantAdminUser)
            $script:clientContext.ExecuteQuery()

            # check if the tenant admin is a site admin
            if( -not $tenantAdminUser.IsSiteAdmin )
            {
                try
                {
                    # grant the tenant admin temporary admin rights to the site collection
                    Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $true | Out-Null
                    $grantedSiteCollectionAdmin = $true
                }
                catch
                {
                    Write-Error $_.Exception
                    return
                }
            }

            try
            {
                # load the list orlibrary using CSOM

                $list = $null
                $list = $script:clientContext.Web.Lists.GetByTitle($listTitle)
                $script:clientContext.Load($list)
                $script:clientContext.ExecuteQuery()

               Remove-IrmConfiguration -List $list                 
            }
            catch
            {
                Write-Error -Message "Error setting IRM configuration on site: $webUrl.`nError Details: $($_.Exception.ToString())"
            }
       }
       finally
       {
            if($grantedSiteCollectionAdmin)
            {
                # remove the temporary admin rights to the site collection
                Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $false | Out-Null
            }
       }
    }

Disconnect-SPOService -ErrorAction SilentlyContinue
```




<!--HONumber=Jun16_HO4-->


