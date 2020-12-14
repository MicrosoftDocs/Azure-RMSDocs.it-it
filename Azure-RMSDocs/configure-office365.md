---
title: Configurazione per i servizi di Microsoft 365 per l'uso di Azure RMS-AIP
description: Informazioni e istruzioni per gli amministratori per configurare i servizi di Microsoft 365 per l'uso con il servizio Azure Rights Management da Azure Information Protection.
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0a6ce612-1b6b-4e21-b7fd-bcf79e492c3b
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 2caaf42c764b80f0ccba8b9c74191cbd6bd23c88
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97383500"
---
# <a name="microsoft-365-configuration-for-online-services-to-use-the-azure-rights-management-service"></a>Microsoft 365: configurazione per Servizi online usare il servizio Azure Rights Management

>Si applica a **: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***Pertinente per**: [AIP Unified Labeling client e client classico](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Usare le sezioni seguenti per configurare Exchange Online, Microsoft SharePoint e Microsoft OneDrive per l'uso del servizio Rights Management di Azure da Azure Information Protection.

## <a name="exchange-online-irm-configuration"></a>Exchange Online: configurazione di IRM

Per informazioni sull'utilizzo di Exchange Online con il servizio Rights Management di Azure, vedere la sezione [Exchange Online ed Exchange Server](office-apps-services-support.md#exchange-online-and-exchange-server) di [supporto di Azure Rights Management per le applicazioni e i servizi di Office](office-apps-services-support.md).

Exchange Online potrebbe già essere abilitato per l'uso del servizio Azure Rights Management. Per controllare, eseguire i comandi seguenti:

1. Se questa è la prima volta che si usa Windows PowerShell per Exchange Online nel computer, sarà necessario configurare Windows PowerShell per l'esecuzione degli script firmati. Avviare la sessione di Windows PowerShell usando l'opzione **Esegui come amministratore** e quindi digitare:

    ```md
    Set-ExecutionPolicy RemoteSigned
    ```

    Premere **S** per confermare.

2. Nella sessione di Windows PowerShell accedere a Exchange Online usando un account abilitato per l'accesso alla shell remota. Per impostazione predefinita, tutti gli account creati in Exchange Online sono abilitati per l'accesso alla Shell remota. L'accesso può essere disabilitato o abilitato usando il comando [Set-User &lt;UserIdentity&gt; -RemotePowerShellEnabled](/powershell/exchange/disable-access-to-exchange-online-powershell).

    Per accedere, digitare prima di tutto:

    ```markdown
    $Cred = Get-Credential
    ```

    Quindi, nella finestra di dialogo **richiesta credenziali di Windows PowerShell** specificare il nome utente e la password del Microsoft 365.

3. Connettersi al servizio Exchange Online impostando prima di tutto una variabile:

    ```md
    $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://ps.outlook.com/powershell/ -Credential $Cred -Authentication Basic –AllowRedirection
    ```

    Quindi, eseguire il comando seguente:

    ```md
    Import-PSSession $Session
    ```

4. Eseguire il comando [Get-IRMConfiguration](/powershell/module/exchange/get-irmconfiguration) per visualizzare la configurazione di Exchange Online per il servizio di protezione:

    ```md
    Get-IRMConfiguration
    ```

    Nell'output individuare il valore di **AzureRMSLicensingEnabled**:

    - Se il parametro AzureRMSLicensingEnabled è impostato su **True**, Exchange Online è già abilitato per il servizio Azure Rights Management.

    - Se il parametro AzureRMSLicensingEnabled è impostato su **False**, eseguire il comando seguente per abilitare Exchange Online per il servizio Azure Rights Management: `Set-IRMConfiguration -AzureRMSLicensingEnabled $true`

5. Per verificare che Exchange Online sia configurato correttamente, eseguire il comando seguente:

    ```md
    Test-IRMConfiguration -Sender <user email address>
    ```

    Ad esempio: **Test-IRMConfiguration-sender adams \@ contoso.com**

    Questo comando esegue una serie di controlli, inclusi la verifica della connettività al servizio, il recupero della configurazione, il recupero di URI, licenze ed eventuali modelli. Nella sessione di Windows PowerShell verranno visualizzati i risultati di ogni controllo e, se tutti gli elementi superano positivamente i controlli, verrà visualizzato un messaggio analogo a: **RISULTATO COMPLESSIVO: ESITO POSITIVO**

Se Exchange Online è abilitato per l'uso del servizio Azure Rights Management, è possibile configurare funzionalità che applicano automaticamente la protezione delle informazioni, ad esempio [regole del flusso di posta](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8), [criteri di prevenzione della perdita dei dati (DLP)](/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention) e [casella vocale protetta](/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/protect-voice-mail) (messaggistica unificata).

## <a name="sharepoint-in-microsoft-365-and-onedrive-irm-configuration"></a>SharePoint in Microsoft 365 e OneDrive: configurazione di IRM

Per informazioni sull'utilizzo di SharePoint IRM con il servizio Rights Management di Azure, vedere [SharePoint in Microsoft 365 e SharePoint Server](office-apps-services-support.md#sharepoint-in-microsoft-365-and-sharepoint-server) dalla sezione **protezione Rights Management** della presente documentazione.

Per configurare SharePoint in Microsoft 365 e OneDrive per supportare il servizio Azure Rights Management, è necessario abilitare prima il servizio IRM (Information Rights Management) per SharePoint usando l'interfaccia di amministrazione di SharePoint. I proprietari del sito possono quindi proteggere con IRM i propri elenchi e le raccolte documenti di SharePoint e gli utenti possono proteggere con IRM la propria libreria OneDrive in modo che i documenti salvati in tale posizione e condivisi con altri utenti vengano protetti automaticamente dal servizio Azure Rights Management.

> [!NOTE]
> Le librerie protette con IRM per SharePoint in Microsoft 365 e OneDrive richiedono la versione più recente del nuovo client di sincronizzazione di OneDrive (OneDrive.exe) e la versione del [client RMS dall'area download Microsoft](https://www.microsoft.com/download/details.aspx?id=38396). Installare questa versione del client RMS anche se è stato installato il client Azure Information Protection. Per altre informazioni su questo scenario di distribuzione, vedere [Distribuire il nuovo client di sincronizzazione di OneDrive in un ambiente aziendale](https://support.office.com/article/Deploy-the-new-OneDrive-sync-client-in-an-enterprise-environment-3f3a511c-30c6-404a-98bf-76f95c519668).

Per abilitare il servizio IRM (Information Rights Management) per SharePoint, vedere le istruzioni seguenti dalla documentazione di Office:

- [Configurare Information Rights Management (IRM) nell'interfaccia di amministrazione di SharePoint](/microsoft-365/compliance/set-up-irm-in-sp-admin-center)

Questa configurazione viene eseguita dall'amministratore Microsoft 365.

### <a name="configuring-irm-for-libraries-and-lists"></a>Configurazione di IRM per elenchi e raccolte

Dopo l'abilitazione del servizio IRM per SharePoint, i proprietari dei siti possono proteggere con IRM le proprie raccolte documenti e i propri elenchi di SharePoint. Per le istruzioni, vedere le informazioni seguenti disponibili nel sito Web di Office:

- [Applicare la protezione Information Rights Management a un elenco o a una raccolta](https://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)

Questa configurazione viene eseguita dall'amministratore del sito di SharePoint.

### <a name="configuring-irm-for-onedrive"></a>Configurazione di IRM per OneDrive

Dopo aver abilitato il servizio IRM per SharePoint, è possibile configurare la raccolta documenti OneDrive degli utenti o le singole cartelle per la protezione Rights Management. Gli utenti possono configurarla autonomamente usando il sito Web OneDrive. Anche se gli amministratori non possono configurare questa protezione per gli utenti usando il centro di amministrazione di SharePoint, è possibile farlo tramite Windows PowerShell.

> [!NOTE]
> Per ulteriori informazioni sulla configurazione di OneDrive, vedere la documentazione di [OneDrive](https://support.office.com/article/Set-up-OneDrive-for-Business-in-Office-365-3e21f8f0-e0a1-43be-aa3e-8c0236bf11bb) .

#### <a name="configuration-for-users"></a>Configurazione per gli utenti

Fornire agli utenti le istruzioni seguenti per poter configurare i OneDrive per proteggere i file aziendali.

1. Accedere a Microsoft 365 con l'account aziendale o dell'Istituto di istruzione e passare al [sito Web OneDrive](https://admin.microsoft.com/onedrive).

2. Nella parte inferiore del riquadro di spostamento selezionare **Return to classic OneDrive** (Torna a OneDrive classico).

3. Selezionare l'icona **Impostazioni** . Nel riquadro **Impostazioni**, se **Barra multifunzione** è impostato su **No**, selezionare questa impostazione per attivare la barra multifunzione.

4. Per configurare tutti i file OneDrive da proteggere, selezionare la scheda **libreria** nella barra multifunzione e quindi selezionare **Impostazioni libreria**.

5. Nella pagina **Documenti > Impostazioni**, nella sezione **Autorizzazioni e gestione** selezionare **Information Rights Management**.

6. Nella pagina **Impostazioni Information Rights Management** selezionare la casella di controllo **Limita autorizzazioni per la libreria durante il download**. Specificare il nome scelto e una descrizione per le autorizzazioni e, facoltativamente, fare clic su **MOSTRA OPZIONI** per impostare le configurazioni facoltative e quindi fare clic su **OK**.

    Per altre informazioni sulle opzioni di configurazione, vedere le istruzioni in [Applicare la protezione Information Rights Management a un elenco o a una raccolta](https://support.office.com/article/Apply-Information-Rights-Management-to-a-list-or-library-3bdb5c4e-94fc-4741-b02f-4e7cc3c54aa1) nella documentazione di Office.

Poiché questa configurazione si basa sugli utenti anziché su un amministratore per proteggere con IRM i file OneDrive, informare gli utenti sui vantaggi della protezione dei file e su come eseguire questa operazione. Ad esempio, spiegare che quando condividono un documento da OneDrive, solo le persone autorizzate possono accedervi con le restrizioni configurate, anche se il file viene rinominato e copiato altrove.

#### <a name="configuration-for-administrators"></a>Configurazione per gli amministratori

Sebbene non sia possibile configurare IRM per OneDrive degli utenti usando l'interfaccia di amministrazione di SharePoint, è possibile eseguire questa operazione usando Windows PowerShell. Per abilitare IRM per queste raccolte, attenersi alla procedura seguente:

1. Scaricare e installare l' [SDK dei componenti client di SharePoint](https://www.microsoft.com/download/details.aspx?id=42038).

2. Scaricare e installare la [Shell di gestione di SharePoint](https://www.microsoft.com/download/details.aspx?id=35588).

3. Copiare il contenuto del seguente script e denominare il file Set-IRMOnOneDriveForBusiness.ps1 nel computer in uso.

   *&#42;&#42;Dichiarazione di non responsabilità&#42;&#42;*: questo script di esempio non è supportato in alcun programma o servizio di supporto standard Microsoft. Questo script di esempio viene fornito "nello stato in cui si trova" senza garanzia di alcun tipo.

   ```ps
   # Requires Windows PowerShell version 3

   <#
     Description:

       Configures IRM policy settings for OneDrive and can also be used for SharePoint libraries and lists

    Script Installation Requirements:

      SharePoint Client Components SDK
      https://www.microsoft.com/download/details.aspx?id=42038

      SharePoint Management Shell
      https://www.microsoft.com/download/details.aspx?id=35588

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
                   Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: https://www.microsoft.com/download/details.aspx?id=42038"
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
                           Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: https://www.microsoft.com/download/details.aspx?id=35588"
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

   # Add the credentials to the client context and SharePoint service connection

       # check for cached credentials to use
       $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin

       if(-not $o365TenantAdminCredential)
       {
           # when credentials are not cached, prompt for the tenant admin credentials
           $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Microsoft 365 admin"

           if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 )
           {
               Write-Error -Message "Could not validate the supplied tenant admin credentials"
               return
           }

           # add the credentials to the cache
           Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential
       }

   # connect to Office365 first, required for SharePoint cmdlets to run

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

4. Rivedere lo script e apportare le modifiche seguenti:

   1. Cercare `$sharepointAdminCenterUrl` e sostituire il valore di esempio con il proprio URL dell'interfaccia di amministrazione di SharePoint.

      Questo valore viene trovato come URL di base quando si accede all'interfaccia di amministrazione di SharePoint e ha il formato seguente: https://*&lt; tenant_name &gt;*-admin.SharePoint.com

      Ad esempio, se il nome del tenant è "contoso", è necessario specificare: **https://contoso-admin.sharepoint.com**

   2. Cercare `$tenantAdmin` e sostituire il valore di esempio con il proprio account amministratore globale completo per Microsoft 365.

      Questo valore corrisponde a quello usato per accedere all'interfaccia di amministrazione di Microsoft 365 come amministratore globale e ha il formato seguente: user_name@*&lt; &gt; nome di dominio tenant*. com

      Se, ad esempio, il nome utente dell'amministratore globale Microsoft 365 è "admin" per il dominio del tenant "contoso.com", è necessario specificare: **admin@contoso.com**

   3. Cercare `$webUrls` e sostituire i valori di esempio con gli URL Web di OneDrive degli utenti, aggiungendo o eliminando tutte le voci necessarie.

      In alternativa, leggere i commenti nello script su come sostituire questa matrice importando un file con estensione csv contenente tutti gli URL da configurare.  È stato fornito un altro script di esempio per cercare ed estrarre automaticamente gli URL per popolare questo file con estensione csv. Quando si è pronti a eseguire questa operazione, usare lo [script aggiuntivo per restituire tutti gli URL di OneDrive a un. Sezione del file CSV](#additional-script-to-output-all-onedrive-urls-to-a-csv-file) immediatamente dopo questi passaggi.

      L'URL Web per l'OneDrive dell'utente è nel formato seguente:*&lt; nome &gt; tenant* https://-My.SharePoint.com/Personal/*&lt; &gt; user_name* _ *&lt; nome &gt; tenant* _com

      Ad esempio, se l'utente nel tenant Contoso ha un nome utente "rsimone", è necessario specificare: **https://contoso-my.sharepoint.com/personal/rsimone_contoso_com**

   4. Poiché si sta usando lo script per configurare OneDrive, non modificare il valore dei **documenti** per la `$listTitle` variabile.

   5. Cercare `ADMIN INSTRUCTIONS`. Se non si apportano modifiche a questa sezione, il OneDrive dell'utente verrà configurato per IRM con il titolo dei criteri "file protetti" e la descrizione "questo criterio limita l'accesso agli utenti autorizzati".  Non verranno impostate altre opzioni di IRM, condizione appropriata per la maggior parte degli ambienti. Tuttavia, si può modificare il titolo del criterio suggerito e la descrizione e anche aggiungere eventuali altre opzioni IRM appropriate per l'ambiente. Vedere l'esempio commentato nello script per facilitare la creazione del proprio set di parametri per il comando Set-IrmConfiguration.

5. Salvare lo script e firmarlo. Se non si firma lo script (condizione più sicura), Windows PowerShell deve essere configurato nel computer in uso per eseguire script non firmati. A tal fine eseguire la sessione di Windows PowerShell con l'opzione **Esegui come amministratore** e digitare: **Set-ExecutionPolicy Unrestricted**. Questa configurazione, tuttavia, consente l'esecuzione di tutti gli script non firmati (condizione meno sicura).

   Per altre informazioni sulla firma degli script di Windows PowerShell, vedere [about_Signing](/powershell/module/microsoft.powershell.core/about/about_signing) nella raccolta documenti di PowerShell.

6. Eseguire lo script e, se richiesto, specificare la password per l'account amministratore Microsoft 365. Se si modifica lo script e lo si esegue nella stessa sessione di Windows PowerShell, le credenziali non verranno richieste.

> [!TIP]
> È inoltre possibile utilizzare questo script per configurare IRM per una raccolta di SharePoint. Per questa configurazione, probabilmente si desidererà attivare l'opzione aggiuntiva **Non consentire il caricamento di documenti che non supportano IRM**, per assicurare che la libreria contenga solo documenti protetti.    A tale scopo aggiungere il parametro `-IrmReject` al comando Set-IrmConfiguration nello script.
>
> È anche necessario modificare la `$webUrls` variabile (ad esempio, **https: \/ /contoso.SharePoint.com**) e la  `$listTitle` variabile (ad esempio, **$Reports**).

Se è necessario disabilitare IRM per le librerie OneDrive dell'utente, vedere la sezione [script per disabilitare IRM per OneDrive](#script-to-disable-irm-for-onedrive) .

##### <a name="additional-script-to-output-all-onedrive-urls-to-a-csv-file"></a>Script aggiuntivo per l'output di tutti gli URL di OneDrive in un. File CSV

Per il passaggio 4c precedente, è possibile usare il seguente script di Windows PowerShell per estrarre gli URL per le librerie OneDrive di tutti gli utenti, che è quindi possibile controllare, modificare, se necessario, quindi importare nello script principale.

Questo script richiede anche l' [SDK dei componenti client di SharePoint](https://www.microsoft.com/download/details.aspx?id=42038) e la [Shell di gestione di SharePoint](https://www.microsoft.com/download/details.aspx?id=35588). Seguire le stesse istruzioni per copiarlo e incollarlo, quindi salvare il file in locale, ad esempio "Report-OneDriveForBusinessSiteInfo.ps1", modificare i valori `$sharepointAdminCenterUrl` e `$tenantAdmin` come in precedenza e quindi eseguire lo script.

*&#42;&#42;Dichiarazione di non responsabilità&#42;&#42;*: questo script di esempio non è supportato in alcun programma o servizio di supporto standard Microsoft. Questo script di esempio viene fornito "nello stato in cui si trova" senza garanzia di alcun tipo.

```ps
# Requires Windows PowerShell version 3

<#
  Description:

    Queries the search service of a Microsoft 365 tenant to retrieve all OneDrive sites.  
    Details of the discovered sites are written to a .CSV file (by default,"OneDriveForBusinessSiteInfo_<date>.csv").

 Script Installation Requirements:

   SharePoint Client Components SDK
   https://www.microsoft.com/download/details.aspx?id=42038

   SharePoint Management Shell
   https://www.microsoft.com/download/details.aspx?id=35588

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
                Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: https://www.microsoft.com/download/details.aspx?id=42038"
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
                        Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: https://www.microsoft.com/download/details.aspx?id=35588"
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

# Add the credentials to the client context and SharePoint service connection

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

# run a query against the Microsoft 365 tenant search service to retrieve all OneDrive URLs

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

##### <a name="script-to-disable-irm-for-onedrive"></a>Script per disabilitare IRM per OneDrive

Usare lo script di esempio seguente se è necessario disabilitare IRM per OneDrive degli utenti.

Questo script richiede anche l' [SDK dei componenti client di SharePoint](https://www.microsoft.com/download/details.aspx?id=42038) e la [Shell di gestione di SharePoint](https://www.microsoft.com/download/details.aspx?id=35588). Copiare e incollare il contenuto, salvare il file in locale, ad esempio "Disable-IRMOnOneDriveForBusiness.ps1", e modificare i valori `$sharepointAdminCenterUrl` e `$tenantAdmin`. Specificare manualmente gli URL OneDrive o usare lo script nella sezione precedente per poterli importare, quindi eseguire lo script.

*&#42;&#42;Dichiarazione di non responsabilità&#42;&#42;*: questo script di esempio non è supportato in alcun programma o servizio di supporto standard Microsoft. Questo script di esempio viene fornito "nello stato in cui si trova" senza garanzia di alcun tipo.

```ps
# Requires Windows PowerShell version 3

<#
  Description:

    Disables IRM for OneDrive and can also be used for SharePoint libraries and lists

 Script Installation Requirements:

   SharePoint Client Components SDK
   https://www.microsoft.com/download/details.aspx?id=42038

   SharePoint Management Shell
   https://www.microsoft.com/download/details.aspx?id=35588

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
                Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: https://www.microsoft.com/download/details.aspx?id=42038"
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
                        Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: https://www.microsoft.com/download/details.aspx?id=35588"
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

# Add the credentials to the client context and SharePoint service connection

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

# connect to Office365 first, required for SharePoint cmdlets to run

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
