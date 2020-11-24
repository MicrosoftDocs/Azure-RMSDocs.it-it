---
title: Come consentire all'applicazione di servizio di usare RMS basato su cloud | Azure RMS
description: Questo argomento descrive i passaggi per la configurazione dell’applicazione di servizio per l’uso di Azure Rights Management.
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: EA1457D1-282F-4CF3-A23C-46793D2C2F32
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: a760f59effa09cf55f7618e6ab965c5e95f015d3
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "95568304"
---
# <a name="how-to-enable-your-service-application-to-work-with-cloud-based-rms"></a>Procedura: Consentire all'applicazione di servizio di usare RMS basato su cloud

[!INCLUDE [deprecation notice](../includes/deprecation-warning.md)]

Questo argomento descrive i passaggi per la configurazione dell’applicazione di servizio per l’uso di Azure Rights Management. Per altre informazioni, vedere [Introduzione a Azure Rights Management](../requirements.md).

**Importante**  
Per usare l'applicazione di servizio Rights Management Services SDK 2.1 con Azure RMS, è necessario creare i propri tenant. Per ulteriori informazioni, vedere [Azure RMS Requirements: sottoscrizioni cloud che supportano Azure RMS](../requirements.md)

## <a name="prerequisites"></a>Prerequisiti

-   RMS SDK 2.1 deve essere installato e configurato. Per altre informazioni, vedere [Introduzione a RMS SDK 2.1](getting-started-with-ad-rms-2-0.md).
-   È necessario [creare un'identità del servizio tramite ACS](/previous-versions/azure/azure-services/gg185924(v=azure.100)) usando l'opzione della chiave simmetrica o tramite altri mezzi e registrare le informazioni sulla chiave ottenute da tale processo.

## <a name="connecting-to-the-azure-rights-management-service"></a>Connessione al servizio Rights Management di Azure

- Chiamare [IpcInitialize](/previous-versions/windows/desktop/msipc/ipcinitialize).
- Impostare [IpcSetGlobalProperty](/previous-versions/windows/desktop/msipc/ipcsetglobalproperty).

  ```cpp
  int mode = IPC_API_MODE_SERVER;
  IpcSetGlobalProperty(IPC_EI_API_MODE, &(mode));
  ```

  **Nota** Per altre informazioni, vedere [Impostazione della modalità di sicurezza dell’API](setting-the-api-security-mode-api-mode.md)


-   La procedura seguente è la configurazione per la creazione di un'istanza di una struttura del [ \_ prompt dei comandi \_ IPC](/previous-versions/windows/desktop/msipc/ipc-prompt-ctx) con il membro *membro pccredential*  ([IPC \_ Credential](/previous-versions/windows/desktop/msipc/ipc-credential)) popolato con le informazioni di connessione dal servizio Rights Management di Azure.
-   Usare le informazioni della creazione di identità del servizio chiavi simmetriche (vedere i prerequisiti elencati in precedenza in questo argomento) per impostare i parametri *parametri wszserviceprincipal*, *wszBposTenantId* e *cbKey* quando si crea un'istanza di una struttura [di \_ \_ \_ chiave simmetrica di IPC Credential](/previous-versions/windows/desktop/msipc/ipc-credential-symmetric-key) .

**Nota**: a causa di una condizione esistente con il servizio di individuazione, vengono accettate le credenziali tramite chiave simmetrica solo se provenienti dall'America del Nord, per cui è necessario specificare direttamente l'URL del tenant. Questa operazione viene eseguita tramite il tipo [IPC\_CONNECTION\_INFO](/previous-versions/windows/desktop/msipc/ipc-connection-info) del parametro *pConnectionInfo* in [IpcGetTemplateList](/previous-versions/windows/desktop/msipc/ipcgettemplatelist) o [IpcGetTemplateIssuerList](/previous-versions/windows/desktop/msipc/ipcgettemplateissuerlist).

## <a name="generate-a-symmetric-key-and-collect-the-needed-information"></a>Generare una chiave simmetrica e raccogliere le informazioni necessarie

### <a name="instructions-to-generate-a-symmetric-key"></a>Istruzioni per generare una chiave simmetrica

-   Installare [Assistente per l’accesso ai Microsoft Online Services](https://go.microsoft.com/fwlink/p/?LinkID=286152)
-   Installare il [modulo Azure AD Powershell](https://bposast.vo.msecnd.net/MSOPMW/8073.4/amd64/AdministrationConfig-en.msi).

**Nota**: per usare i cmdlet di Powershell, è necessario essere un amministratore tenant.

- Avviare Powershell ed eseguire i comandi seguenti per generare una chiave

    `Import-Module MSOnline`

    `Connect-MsolService` (digitare le credenziali di amministratore)

    `New-MsolServicePrincipal` (digitare un nome visualizzato)

- Dopo la generazione di una chiave simmetrica, verranno visualizzate le informazioni sulla chiave, tra cui la chiave stessa e *AppPrincipalId*.

  ```output
  The following symmetric key was created as one was not supplied
  ZYbF/lTtwE28qplQofCpi2syWd11D83+A3DRlb2Jnv8=

  DisplayName : RMSTestApp
  ServicePrincipalNames : {7d9c1f38-600c-4b4d-8249-22427f016963}
  ObjectId : 0ee53770-ec86-409e-8939-6d8239880518
  AppPrincipalId : 7d9c1f38-600c-4b4d-8249-22427f016963
  ```


### <a name="instructions-to-find-out-tenantbposid-and-urls"></a>Istruzioni per individuare **TenantBposId** e **URL**

-   Installare il [modulo Powershell per Azure RMS](../install-powershell.md).
-   Avviare Powershell ed eseguire i comandi seguenti per ottenere la configurazione RMS del tenant.

    `Import-Module AIPService`

    `Connect-AipService` (digitare le credenziali di amministratore)

    `Get-AipServiceConfiguration`


- Creare un'istanza di una  [ \_ \_ \_ chiave simmetrica della credenziale IPC](/previous-versions/windows/desktop/msipc/ipc-credential-symmetric-key) e impostare alcuni membri.

  ```cpp
  // Create a key structure.
  IPC_CREDENTIAL_SYMMETRIC_KEY symKey = {0};

  // Set each member with information from service creation.
  symKey.wszBase64Key = "your service principal key";
  symKey.wszAppPrincipalId = "your app principal identifier";
  symKey.wszBposTenantId = "your tenant identifier";
  ```

Per altre informazioni, vedere [IPC \_ Credential \_ Symmetric \_ Key](/previous-versions/windows/desktop/msipc/ipc-credential-symmetric-key).

- Creare un'istanza di una struttura di [ \_ credenziali IPC](/previous-versions/windows/desktop/msipc/ipc-credential) contenente l'istanza della [ \_ \_ \_ chiave simmetrica di IPC Credential](/previous-versions/windows/desktop/msipc/ipc-credential-symmetric-key) .

  **Nota**   -I membri *ConnectionInfo* vengono impostati con gli URL della chiamata precedente a `Get-AipServiceConfiguration` e indicati con tali nomi di campo.

  ```cpp
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
  ```

### <a name="identify-a-template-and-then-encrypt"></a>Identificare un modello e quindi crittografare

- Selezionare un modello da usare per la crittografia.
    Chiamare [IpcGetTemplateList](/previous-versions/windows/desktop/msipc/ipcgettemplatelist) passando la stessa istanza di [IPC \_ prompt \_ ctx](/previous-versions/windows/desktop/msipc/ipc-prompt-ctx).

  ```cpp
  PCIPC_TIL pTemplates = NULL;
  IPC_TEMPLATE_ISSUER templateIssuer = (pTemplateIssuerList->aTi)[0];

  hr = IpcGetTemplateList(&(templateIssuer.connectionInfo),
         IPC_GTL_FLAG_FORCE_DOWNLOAD,
         0,
         &promptCtx,
         NULL,
         &pTemplates);
  ```

- Con il modello riportato in precedenza in questo argomento, chiamare [IpcfEncrcyptFile](/previous-versions/windows/desktop/msipc/ipcfencryptfile)passando la stessa istanza di [IPC \_ prompt \_ ctx](/previous-versions/windows/desktop/msipc/ipc-prompt-ctx).

  Esempio d’uso di [IpcfEncrcyptFile](/previous-versions/windows/desktop/msipc/ipcfencryptfile):

  ```cpp
  LPCWSTR wszContentTemplateId = pTemplates->aTi[0].wszID;
  hr = IpcfEncryptFile(wszInputFilePath,
         wszContentTemplateId,
         IPCF_EF_TEMPLATE_ID,
         IPC_EF_FLAG_KEY_NO_PERSIST,
         &promptCtx,
         NULL,
         &wszOutputFilePath);
  ```

  Esempio d’uso di [IpcfDecryptFile](/previous-versions/windows/desktop/msipc/ipcfdecryptfile):

  ```cpp
  hr = IpcfDecryptFile(wszInputFilePath,
         IPCF_DF_FLAG_DEFAULT,
         &promptCtx,
         NULL,
         &wszOutputFilePath);
  ```

La procedura necessaria per consentire all'applicazione di usare Azure Rights Management è stata completata.

## <a name="related-topics"></a>Argomenti correlati

* [Introduzione a Azure Rights Management](../requirements.md)
* [Introduzione a RMS SDK 2.1](getting-started-with-ad-rms-2-0.md)
* [Creare un'identità del servizio tramite ACS](/previous-versions/azure/azure-services/gg185924(v=azure.100))
* [IpcSetGlobalProperty](/previous-versions/windows/desktop/msipc/ipcsetglobalproperty)
* [IpcInitialize](/previous-versions/windows/desktop/msipc/ipcinitialize)
* [\_prompt dei comandi IPC \_](/previous-versions/windows/desktop/msipc/ipc-prompt-ctx)
* [\_credenziali IPC](/previous-versions/windows/desktop/msipc/ipc-credential)
* [\_chiave simmetrica della credenziale IPC \_ \_](/previous-versions/windows/desktop/msipc/ipc-credential-symmetric-key)
* [IpcGetTemplateIssuerList](/previous-versions/windows/desktop/msipc/ipcgettemplateissuerlist)
* [IpcGetTemplateList](/previous-versions/windows/desktop/msipc/ipcgettemplatelist)
* [IpcfDecryptFile](/previous-versions/windows/desktop/msipc/ipcfdecryptfile)
* [IpcfEncrcyptFile](/previous-versions/windows/desktop/msipc/ipcfencryptfile)
* [IpcCreateLicenseFromScratch](/previous-versions/windows/desktop/msipc/ipccreatelicensefromscratch)
* [IpcCreateLicenseFromTemplateID](/previous-versions/windows/desktop/msipc/ipccreatelicensefromtemplateid)