---
# metadati obbligatori

titolo: Procedura: Consentire all'applicazione di servizio di usare RMS basato su cloud | Descrizione di Azure RMS: questo argomento descrive i passaggi per la configurazione dell'applicazione di servizio per l'uso di Azure Rights Management.
keywords: author: bruceperlerms manager: mbaldwin ms.date: 04/28/2016 ms.topic: article ms.prod: azure ms.service: rights-management ms.technology: techgroup-identity ms.assetid: EA1457D1-282F-4CF3-A23C-46793D2C2F32
# metadati facoltativi

#ROBOT:
destinatari: sviluppatori
#ms.devlang:
ms.reviewer: shubhamp ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Procedura: Consentire all'applicazione di servizio di usare RMS basato su cloud

Questo argomento descrive i passaggi per la configurazione dell’applicazione di servizio per l’uso di Azure Rights Management. Per altre informazioni, vedere [Introduzione a Azure Rights Management](https://technet.microsoft.com/en-us/library/jj585016.aspx).

**Importante**  
Per usare l'applicazione di servizio Rights Management Services SDK 2.1 con Azure RMS, è necessario creare i propri tenant. Per altre informazioni vedere [Azure RMS requirements: Cloud subscriptions that support Azure RMS](/rights-management/get-started/requirements-subscriptions.md) (Requisiti per Azure RMS: sottoscrizioni cloud che supportano Azure RMS)

## Prerequisiti

-   RMS SDK 2.1 deve essere installato e configurato. Per altre informazioni, vedere [Introduzione a RMS SDK 2.1](getting-started-with-ad-rms-2-0.md).
-   È necessario [creare un'identità del servizio tramite ACS](https://msdn.microsoft.com/en-us/library/gg185924.aspx) usando l'opzione della chiave simmetrica o tramite altri mezzi e registrare le informazioni sulla chiave ottenute da tale processo.

## Connessione al servizio Rights Management di Azure

-   Chiamare [**IpcInitialize**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize).
-   Impostare [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty).

        C++
        int mode = IPC_API_MODE_SERVER;
        IpcSetGlobalProperty(IPC_EI_API_MODE, &(mode));


  **Nota** Per altre informazioni, vedere [Impostazione della modalità di sicurezza dell’API](setting-the-api-security-mode-api-mode.md)

     
-   La procedura seguente rappresenta la configurazione per la creazione dell'istanza di una struttura [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx) con il membro **pcCredential** ([**IPC\_CREDENTIAL**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential)) popolato con le informazioni di connessione ottenute dal servizio di Azure Rights Management.
-   Usare le informazioni ottenute con la creazione dell'identità del servizio tramite chiave simmetrica (vedere i prerequisiti riportati in precedenza in questo argomento) per impostare i parametri **wszServicePrincipal**, **wszBposTenantId** e **cbKey** quando si crea l'istanza di una struttura [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key).

**Nota** A causa di una condizione esistente presso il nostro servizio di individuazione, le credenziali tramite chiave simmetrica vengono accettate solo se provenienti dal Nord America e di conseguenza è necessario specificare l'URL del tenant direttamente. Questa operazione viene eseguita tramite il parametro [**IPC\_CONNECTION\_INFO**](/rights-management/sdk/2.1/api/win/ipc_connection_info#msipc_ipc_connection_info) di [**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist) oppure [**IpcGetTemplateIssuerList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist).

## Generare una chiave simmetrica e raccogliere le informazioni necessarie

### Istruzioni per generare una chiave simmetrica

-   Installare [Assistente per l’accesso ai Microsoft Online Services](http://go.microsoft.com/fwlink/p/?LinkID=286152)
-   Installare il [modulo Azure AD Powershell](https://bposast.vo.msecnd.net/MSOPMW/8073.4/amd64/AdministrationConfig-en.msi).

**Nota** Per usare i cmdlet di Powershell, è necessario essere un amministratore tenant.

-   Avviare Powershell ed eseguire i comandi seguenti per generare una chiave         `Import-Module MSOnline`
            `Connect-MsolService` (digitare le credenziali di amministratore)         `New-MsolServicePrincipal` (digitare un nome visualizzato)
-   Dopo la generazione di una chiave simmetrica, verranno visualizzate le informazioni sulla chiave, tra cui la chiave stessa e **AppPrincipalId**.


    La chiave simmetrica seguente è stata creata come la chiave non fornita ZYbF/lTtwE28qplQofCpi2syWd11D83+A3DRlb2Jnv8=

    DisplayName : RMSTestApp ServicePrincipalNames : {7d9c1f38-600c-4b4d-8249-22427f016963} ObjectId : 0ee53770-ec86-409e-8939-6d8239880518 AppPrincipalId : 7d9c1f38-600c-4b4d-8249-22427f016963


### Istruzioni per individuare **TenantBposId** e **URL**

-   Installare il [modulo Powershell per Azure RMS](https://technet.microsoft.com/en-us/library/jj585012.aspx).
-   Avviare Powershell ed eseguire i comandi seguenti per ottenere la configurazione RMS del tenant.

    `Import-Module aadrm`

    `Connect-AadrmService` (digitare le credenziali di amministratore)

    `Get-AadrmConfiguration`


-   Creare un'istanza di  [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key) e impostare alcuni membri.

    // Creare una struttura di chiave.
    IPC_CREDENTIAL_SYMMETRIC_KEY symKey = {0}.

    // Impostare ogni membro con le informazioni ottenute con la creazione del servizio.
    symKey.wszBase64Key = "chiave dell'entità servizio"; symKey.wszAppPrincipalId = "identificatore dell'entità app"; symKey.wszBposTenantId = "identificatore del tenant";


Per altre informazioni, vedere [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key).

-   Creare l'istanza di una struttura [**IPC\_CREDENTIAL**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential) contenente l'istanza di [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key).

**Nota** I membri *conectionInfo* sono impostati con gli URL ottenuti dalla chiamata precedente a `Get-AadrmConfiguration` e indicati con tali nomi di campo.

    // Create a credential structure.
    IPC_CREDENTIAL cred = {0};

    IPC_CONNECTION_INFO connectionInfo = {0};
    connectionInfo.wszIntranetUrl = LicensingIntranetDistributionPointUrl;
    connectionInfo.wszExtranetUrl = LicensingExtranetDistributionPointUrl;

    // Set each member.
    cred.dwType = IPC_CREDENTIAL_TYPE_SYMMETRIC_KEY;
    cred.pcCertContext = (PCCERT_CONTEXT)&symKey;

    // Create your prompt control.
    IPC_PROMPT_CTX promptCtx = {0};

    // Set each member.
    promptCtx.cbSize = sizeof(IPC_PROMPT_CTX);
    promptCtx.hwndParent = NULL;
    promptCtx.dwflags = IPC_PROMPT_FLAG_SILENT;
    promptCtx.hCancelEvent = NULL;
    promptCtx.pcCredential = &cred;

### Identificare un modello e quindi crittografare

-   Selezionare un modello da usare per la crittografia.
    Chiamare [**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist) passando la stessa istanza di [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx).


    PCIPC_TIL pTemplates = NULL; IPC_TEMPLATE_ISSUER templateIssuer = (pTemplateIssuerList->aTi)[0];

    hr = IpcGetTemplateList(&(templateIssuer.connectionInfo),        IPC_GTL_FLAG_FORCE_DOWNLOAD,        0,        &promptCtx,        NULL,        &pTemplates);


-   Con il modello citato in precedenza in questo argomento, chiamare [**IpcfEncrcyptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile) passando la stessa istanza di [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx).

Esempio d’uso di [**IpcfEncrcyptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile):

    LPCWSTR wszContentTemplateId = pTemplates->aTi[0].wszID;
    hr = IpcfEncryptFile(wszInputFilePath,
           wszContentTemplateId,
           IPCF_EF_TEMPLATE_ID,
           IPC_EF_FLAG_KEY_NO_PERSIST,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

Esempio d’uso di [**IpcfDecryptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfdecryptfile):

    hr = IpcfDecryptFile(wszInputFilePath,
           IPCF_DF_FLAG_DEFAULT,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

La procedura necessaria per consentire all'applicazione di usare Azure Rights Management è stata completata.

## Argomenti correlati

* [Introduzione a Azure Rights Management](https://technet.microsoft.com/en-us/library/jj585016.aspx)
* [Introduzione a RMS SDK 2.1](getting-started-with-ad-rms-2-0.md)
* [Creare un'identità del servizio tramite ACS](https://msdn.microsoft.com/en-us/library/gg185924.aspx)
* [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty)
* [**IpcInitialize**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize)
* [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx)
* [**IPC\_CREDENTIAL**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential)
* [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key)
* [**IpcGetTemplateIssuerList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist)
* [**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
* [**IpcfDecryptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfdecryptfile)
* [**IpcfEncrcyptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile)
* [**IpcCreateLicenseFromScratch**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch)
* [**IpcCreateLicenseFromTemplateID**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromtemplateid)
 

 


<!--HONumber=Jun16_HO2-->


