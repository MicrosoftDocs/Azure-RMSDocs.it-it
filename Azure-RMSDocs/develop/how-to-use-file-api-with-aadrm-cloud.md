---
title: Come consentire all&quot;applicazione di servizio di usare RMS basato su cloud | Azure RMS
description: "Questo argomento descrive i passaggi per la configurazione dell’applicazione di servizio per l’uso di Azure Rights Management."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: EA1457D1-282F-4CF3-A23C-46793D2C2F32
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7df62371ba4a2eea0227c731cf90b3454993f533
ms.openlocfilehash: 28b85313e278455391040797ea2886bd9247abe2


---

# Procedura: Consentire all'applicazione di servizio di usare RMS basato su cloud

Questo argomento descrive i passaggi per la configurazione dell’applicazione di servizio per l’uso di Azure Rights Management. Per altre informazioni, vedere [Requisiti per Azure Rights Management](https://technet.microsoft.com/library/jj585016.aspx).

**Importante**  
Per usare l'applicazione di servizio Rights Management Services SDK 2.1 con Azure RMS, è necessario creare i propri tenant. Per altre informazioni vedere [Requisiti per Azure RMS: sottoscrizioni cloud che supportano Azure RMS](../get-started/requirements-subscriptions.md)

## Prerequisiti

-   RMS SDK 2.1 deve essere installato e configurato. Per altre informazioni, vedere [Introduzione a RMS SDK 2.1](getting-started-with-ad-rms-2-0.md).
-   È necessario [creare un'identità del servizio tramite ACS](https://msdn.microsoft.com/en-us/library/gg185924.aspx) usando l'opzione della chiave simmetrica o tramite altri mezzi e registrare le informazioni sulla chiave ottenute da tale processo.

## Connessione al servizio Rights Management di Azure

-   Chiamare [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx).
-   Impostare [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx).

        C++
        int mode = IPC_API_MODE_SERVER;
        IpcSetGlobalProperty(IPC_EI_API_MODE, &(mode));


  **Nota** Per altre informazioni, vedere [Impostazione della modalità di sicurezza dell’API](setting-the-api-security-mode-api-mode.md)

     
-   La procedura seguente indica come creare un'istanza di una struttura [IPC\_PROMPT\_CTX](https://msdn.microsoft.com/library/hh535278.aspx) con il membro *pcCredential*  ([IPC\_CREDENTIAL](https://msdn.microsoft.com/library/hh535275.aspx)) popolato con le informazioni di connessione ottenute dal servizio Azure Rights Management.
-   Usare le informazioni ottenute dalla creazione dell'identità del servizio tramite chiave simmetrica (vedere i prerequisiti riportati in precedenza in questo argomento) per impostare i parametri *wszServicePrincipal*, *wszBposTenantId* e *cbKey* quando si crea l'istanza di una struttura [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx).

**Nota**: a causa di una condizione esistente con il servizio di individuazione, vengono accettate le credenziali tramite chiave simmetrica solo se provenienti dall'America del Nord, per cui è necessario specificare direttamente l'URL del tenant. Questa operazione viene eseguita tramite il tipo [IPC\_CONNECTION\_INFO](https://msdn.microsoft.com/library/hh535274.aspx) del parametro *pConnectionInfo* in [IpcGetTemplateList](https://msdn.microsoft.com/library/hh535267.aspx) o [IpcGetTemplateIssuerList](https://msdn.microsoft.com/library/hh535266.aspx).

## Generare una chiave simmetrica e raccogliere le informazioni necessarie

### Istruzioni per generare una chiave simmetrica

-   Installare [Assistente per l’accesso ai Microsoft Online Services](http://go.microsoft.com/fwlink/p/?LinkID=286152)
-   Installare il [modulo Azure AD Powershell](https://bposast.vo.msecnd.net/MSOPMW/8073.4/amd64/AdministrationConfig-en.msi).

**Nota**: per usare i cmdlet di Powershell, è necessario essere un amministratore tenant.

- Avviare Powershell ed eseguire i comandi seguenti per generare una chiave

    `Import-Module MSOnline`

    `Connect-MsolService` (digitare le credenziali di amministratore)

    `New-MsolServicePrincipal` (digitare un nome visualizzato)

- Dopo la generazione di una chiave simmetrica, verranno visualizzate le informazioni sulla chiave, tra cui la chiave stessa e *AppPrincipalId*.

      The following symmetric key was created as one was not supplied
      ZYbF/lTtwE28qplQofCpi2syWd11D83+A3DRlb2Jnv8=

      DisplayName : RMSTestApp
      ServicePrincipalNames : {7d9c1f38-600c-4b4d-8249-22427f016963}
      ObjectId : 0ee53770-ec86-409e-8939-6d8239880518
      AppPrincipalId : 7d9c1f38-600c-4b4d-8249-22427f016963


### Istruzioni per individuare **TenantBposId** e **URL**

-   Installare il [modulo Powershell per Azure RMS](https://technet.microsoft.com/en-us/library/jj585012.aspx).
-   Avviare Powershell ed eseguire i comandi seguenti per ottenere la configurazione RMS del tenant.

    `Import-Module aadrm`

    `Connect-AadrmService` (digitare le credenziali di amministratore)

    `Get-AadrmConfiguration`


- Creare un'istanza di [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx) e impostare alcuni membri.

      // Create a key structure.
      IPC_CREDENTIAL_SYMMETRIC_KEY symKey = {0};

      // Set each member with information from service creation.
      symKey.wszBase64Key = "your service principal key";
      symKey.wszAppPrincipalId = "your app principal identifier";
      symKey.wszBposTenantId = "your tenant identifier";


Per altre informazioni, vedere [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx).

-   Creare un'istanza di struttura [IPC\_CREDENTIAL](https://msdn.microsoft.com/library/hh535275.aspx) che contenga l'istanza [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx).

**Nota**: i membri di *conectionInfo* sono impostati con gli URL ottenuti dalla chiamata precedente a `Get-AadrmConfiguration` e indicati con tali nomi di campo.

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
    Chiamare [IpcGetTemplateList](https://msdn.microsoft.com/library/hh535267.aspx) passando la stessa istanza di [IPC\_PROMPT\_CTX](https://msdn.microsoft.com/library/hh535278.aspx).


    PCIPC_TIL pTemplates = NULL; IPC_TEMPLATE_ISSUER templateIssuer = (pTemplateIssuerList->aTi)[0];

    hr = IpcGetTemplateList(&(templateIssuer.connectionInfo),        IPC_GTL_FLAG_FORCE_DOWNLOAD,        0,        &promptCtx,        NULL,        &pTemplates);


-   Con il modello citato in precedenza in questo argomento, chiamare [IpcfEncrcyptFile](https://msdn.microsoft.com/library/dn133059.aspx) passando la stessa istanza di [IPC\_PROMPT\_CTX](https://msdn.microsoft.com/library/hh535278.aspx).

Uso dell'esempio di [IpcfEncrcyptFile](https://msdn.microsoft.com/library/dn133059.aspx):

    LPCWSTR wszContentTemplateId = pTemplates->aTi[0].wszID;
    hr = IpcfEncryptFile(wszInputFilePath,
           wszContentTemplateId,
           IPCF_EF_TEMPLATE_ID,
           IPC_EF_FLAG_KEY_NO_PERSIST,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

Uso dell'esempio di [IpcfDecryptFile](https://msdn.microsoft.com/library/dn133058.aspx):

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
* [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx)
* [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx)
* [IPC\_PROMPT\_CTX](https://msdn.microsoft.com/library/hh535278.aspx)
* [IPC\_CREDENTIAL](https://msdn.microsoft.com/library/hh535275.aspx)
* [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx)
* [IpcGetTemplateIssuerList](https://msdn.microsoft.com/library/hh535266.aspx)
* [IpcGetTemplateList](https://msdn.microsoft.com/library/hh535267.aspx)
* [IpcfDecryptFile](https://msdn.microsoft.com/library/dn133058.aspx)
* [IpcfEncrcyptFile](https://msdn.microsoft.com/library/dn133059.aspx)
* [IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx)
* [IpcCreateLicenseFromTemplateID](https://msdn.microsoft.com/library/hh535257.aspx)
 

 



<!--HONumber=Oct16_HO4-->


