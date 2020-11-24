---
title: Autenticazione ADAL per l'applicazione abilitata per RMS | Azure RMS
description: Vedere come autenticare l'app con Azure RMS usando la libreria di autenticazione di Azure Active Directory (ADAL).
keywords: autenticazione, RMS, ADAL
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f89f59b7-33d1-4ab3-bb64-1e9bda269935
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev, has-adal-ref
ms.openlocfilehash: a7cf207b0976db31ffa4df83d20e172876c7ee88
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "95568316"
---
# <a name="how-to-use-adal-authentication"></a>Procedura: Usare l'autenticazione ADAL

Autenticazione con Azure RMS per l'app usando Azure Active Directory Authentication Library (ADAL).

Eseguendo l'aggiornamento dell'applicazione per l'uso dell'autenticazione ADAL anziché dell'Assistente per l'accesso a Microsoft Online, l'utente e i clienti potranno:

- Usare Multi-Factor Authentication
- Installare il client RMS 2.1 senza necessità di privilegi amministrativi sul computer
- Certificare l'applicazione per Windows 10

## <a name="two-approaches-to-authentication"></a>Due approcci per l'autenticazione

In questo argomento sono descritti due approcci per l'autenticazione con i relativi esempi di codice.

- **Autenticazione interna**: autenticazione OAuth gestita da RMS SDK.

  Usare questo approccio per fare in modo che il client RMS visualizzi una richiesta di autenticazione ADAL quando è necessaria l'autenticazione. Per informazioni dettagliate sulla configurazione dell'applicazione, vedere la sezione "Autenticazione interna".

  > [!Note]
  > Se l'applicazione usa AD RMS SDK 2.1 con l'Assistente per l'accesso, è consigliabile utilizzare il metodo di autenticazione interna come percorso di migrazione dell'applicazione.

- **Autenticazione esterna**: autenticazione OAuth gestita dall'applicazione.

  Usare questo approccio per fare in modo che l'applicazione gestisca la propria autenticazione OAuth. Con questo approccio, il client RMS eseguirà un callback definito dall'applicazione quando è necessaria l'autenticazione. Per un esempio dettagliato, vedere "Autenticazione esterna" alla fine di questo argomento.

  > [!Note]
  > L'autenticazione esterna non implica la possibilità di modificare gli utenti: il client RMS usa sempre l'utente predefinito per un determinato tenant RMS.

## <a name="internal-authentication"></a>Autenticazione interna

1. Attenersi alla procedura di configurazione di Azure in [Configurare Azure RMS per l'autenticazione ADAL](adal-auth.md) e tornare al passaggio di inizializzazione delle app seguente.
2. È ora possibile configurare l'applicazione per l'uso dall'autenticazione ADAL interna inclusa in RMS SDK 2.1.

Per configurare il client RMS, aggiungere una chiamata a [IpcSetGlobalProperty](/previous-versions/windows/desktop/msipc/ipcsetglobalproperty) dopo la chiamata a [IpcInitialize](/previous-versions/windows/desktop/msipc/ipcinitialize) per configurare il client RMS. Usare il frammento di codice seguente come esempio.

```cpp
IpcInitialize();

IPC_AAD_APPLICATION_ID applicationId = { 0 };
applicationId.cbSize = sizeof(IPC_AAD_APPLICATION_ID);
applicationId.wszClientId = L"GUID-provided-by-AAD-for-your-app-(no-brackets)";
applicationId.wszRedirectUri = L"RedirectionUriWeProvidedAADForOurApp://authorize";
HRESULT hr = IpcSetGlobalProperty(IPC_EI_APPLICATION_ID, &applicationId);
if (FAILED(hr)) {
  //Handle the error
}
```

## <a name="external-authentication"></a>Autenticazione esterna

Usare il codice seguente come esempio per la gestione dei token di autenticazione.

```cpp
extern HRESULT GetADALToken(LPVOID pContext, const IPC_NAME_VALUE_LIST& Parameters, __out wstring wstrToken) throw();

HRESULT GetLicenseKey(PCIPC_BUFFER pvLicense, __in LPVOID pContextForAdal, __out IPC_KEY_HANDLE &hKey)
{
    IPC_OAUTH2_CALLBACK pfGetADALToken =
    [](LPVOID pvContext, PIPC_NAME_VALUE_LIST pParameters, IPC_AUTH_TOKEN_HANDLE* phAuthToken) -> HRESULT
    {
        wstring wstrToken;
        HRESULT hr = GetADALToken(pvContext, *pParameters, wstrToken);
        return SUCCEEDED(hr) ? IpcCreateOAuth2Token(wstrToken.c_str(), OUT phAuthToken) : hr;
    };

    IPC_OAUTH2_CALLBACK_INFO callbackCredentialContext =
    {
        sizeof(IPC_OAUTH2_CALLBACK_INFO),
        pfGetADALToken,
        pContextForAdal
    };

    IPC_CREDENTIAL credentialContext =
    {
        IPC_CREDENTIAL_TYPE_OAUTH2,
        NULL
    };
    credentialContext.pcOAuth2 = &callbackCredentialContext;

    IPC_PROMPT_CTX promptContext =
    {
        sizeof(IPC_PROMPT_CTX),
        NULL,
        IPC_PROMPT_FLAG_SILENT | IPC_PROMPT_FLAG_HAS_USER_CONSENT,
        NULL,
        &credentialContext
    };

    hKey = 0L;
    return IpcGetKey(pvLicense, 0, &promptContext, NULL, &hKey);
}
```

## <a name="related-topics"></a>Argomenti correlati

- [Tipi di dati](/previous-versions/windows/desktop/msipc/microsoft-information-protection-and-control-client-data-types)
- [Proprietà dell'ambiente](/previous-versions/windows/desktop/msipc/environment-properties)
- [IpcCreateOAuth2Token](/previous-versions/windows/desktop/msipc/ipccreateoauth2token)
- [IpcGetKey](/previous-versions/windows/desktop/msipc/ipcgetkey)
- [IpcInitialize](/previous-versions/windows/desktop/msipc/ipcinitialize)
- [IPC_CREDENTIAL](/previous-versions/windows/desktop/msipc/ipc-credential)
- [IPC_NAME_VALUE_LIST](/previous-versions/windows/desktop/msipc/ipc-name-value-list)
- [IPC_OAUTH2_CALLBACK_INFO](/previous-versions/windows/desktop/msipc/ipc-oath2-callback-info)
- [IPC_PROMPT_CTX](/previous-versions/windows/desktop/msipc/ipc-prompt-ctx)
- [IPC_AAD_APPLICATION_ID](/previous-versions/windows/desktop/msipc/ipc-aad-application-id)