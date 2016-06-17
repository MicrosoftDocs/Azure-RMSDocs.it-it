---
# required metadata

title: Autenticazione ADAL per l'applicazione abilitata per RMS | Azure RMS
description: Descrive il processo per l'autenticazione con ADAL
keywords: authentication, RMS, ADAL
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f89f59b7-33d1-4ab3-bb64-1e9bda269935

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Procedura: Usare l'autenticazione ADAL

Autenticazione con Azure RMS per l'app usando Azure Active Directory Authentication Library (ADAL).

Eseguendo l'aggiornamento dell'applicazione per l'uso dell'autenticazione ADAL anziché dell'Assistente per l'accesso a Microsoft Online, l'utente e i clienti potranno:

- Usare Multi-Factor Authentication
- Installare il client RMS 2.1 senza necessità di privilegi amministrativi sul computer
- Certificare l'applicazione per Windows 10

## Due approcci per l'autenticazione

In questo argomento sono descritti due approcci per l'autenticazione con i relativi esempi di codice.

- **Autenticazione interna**: autenticazione OAuth gestita da RMS SDK.

  Usare questo approccio per fare in modo che il client RMS visualizzi una richiesta di autenticazione ADAL quando è necessaria l'autenticazione. Per informazioni dettagliate sulla configurazione dell'applicazione, vedere la sezione "Autenticazione interna".

  > [!Note] Se l'applicazione usa AD RMS SDK 2.1 con l'Assistente per l'accesso, è consigliabile utilizzare il metodo di autenticazione interna come percorso di migrazione dell'applicazione.

- **Autenticazione esterna**: autenticazione OAuth gestita dall'applicazione.

  Usare questo approccio per fare in modo che l'applicazione gestisca la propria autenticazione OAuth. Con questo approccio, il client RMS eseguirà un callback definito dall'applicazione quando è necessaria l'autenticazione. Per un esempio dettagliato, vedere "Autenticazione esterna" alla fine di questo argomento.

  > [!Note] L'autenticazione esterna non implica la possibilità di modificare gli utenti: il client RMS usa sempre l'utente predefinito per un determinato tenant RMS.

## Autenticazione interna

1. Attenersi alla procedura di configurazione di Azure in [Configurare Azure RMS per l'autenticazione ADAL](adal-auth.md) e tornare al passaggio di inizializzazione delle app seguente.
2. È ora possibile configurare l'applicazione per l'uso dall'autenticazione ADAL interna inclusa in RMS SDK 2.1.

Per configurare il client RMS, aggiungere una chiamata a [IpcSetGlobalProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty) dopo la chiamata a [IpcInitialize](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize) per configurare il client RMS. Usare il frammento di codice seguente come esempio.

      C++
      IpcInitialize();

      IPC_AAD_APPLICATION_ID applicationId = { 0 };
      applicationId.cbSize = sizeof(IPC_AAD_APPLICATION_ID);
      applicationId.wszClientId = L"GUID-provided-by-AAD-for-your-app-(no-brackets)";
      applicationId.wszRedirectUri = L"RedirectionUriWeProvidedAADForOurApp://authorize";
      HRESULT hr = IpcSetGlobalProperty(IPC_EI_APPLICATION_ID, &applicationId);
      if (FAILED(hr)) {
        //Handle the error
      }

## Autenticazione esterna

Usare il codice seguente come esempio per la gestione dei token di autenticazione.
C++ extern HRESULT GetADALToken(LPVOID pContext, const IPC_NAME_VALUE_LIST& Parameters, __out wstring wstrToken) throw();

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

## Argomenti correlati

* [Tipi di dati](/rights-management/sdk/2.1/api/win/datatypes)
* [Proprietà di ambiente](/rights-management/sdk/2.1/api/win/environmentproperties)
* [IpcCreateOAuth2Token](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreateoauth2token)
* [IpcGetKey](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey)
* [IpcInitialize](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize)
* [IPC_CREDENTIAL](/rights-management/sdk/2.1/api/win/IPC_CREDENTIAL)
* [IPC_NAME_VALUE_LIST](/rights-management/sdk/2.1/api/win/IPC_NAME_VALUE_LIST)
* [IPC_OAUTH2_CALLBACK_INFO](/rights-management/sdk/2.1/api/win/IIPC_OAUTH2_CALLBACK_INFO)
* [IPC_PROMPT_CTX](/rights-management/sdk/2.1/api/win/IPC_PROMPT_CTX)
* [IPC_AAD_APPLICATION_ID](/rights-management/sdk/2.1/api/win/IIPC_AAD_APPLICATION_ID)


<!--HONumber=Jun16_HO2-->


